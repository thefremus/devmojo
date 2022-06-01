# A perspective on mapping objects in .NET

![Image post](img/a-perspective-on-dotnet-mapping.jpg)

## Introduction

After watching [Mapster, the best .NET mapper that you are (probably) not using](https://www.youtube.com/watch?v=UIslFVEHkzA) and reading [Enjoy Using Mapster in .Net 6](https://medium.com/@M-S-2/enjoy-using-mapster-in-net-6-2d3f287a0989) I felt the need to explore the world of mapping for myself. To be honest up to this point I have only seen mapping as a necessary evil - in the projects I worked on I keep using them where they are used. In some cases though I use manual mapping, especially when writing projections from an EF Core DbContext. The thing that struck me most in the video is the performance gains - the difference in performance compared to manual mapping seems to make it worth considering. 

Most or many of the projects I have worked on in the past have predominantly used AutoMapper for object mapping. AutoMapper is a very popular .NET library used to map objects in your application. But first lets try to understand the basic idea. Many .NET projects use an ORM, such as EFCore, to map objects to database tables. The objects mapping to your database is typically referred to as entity classes - or just entities. In most .NET projects the persistence of data lives in a different abstraction layer to the rest of your application. Entity classes are usually transformed into other classes. The transformed classes are used to render data in an API endpoint, for instance. The transformed classes can have similar properties - or not at all. You might have an entity class of type `Person` with a `FirstName` and `LastName` property. The entity class maps to a table in your database - `People`. The table contains columns for `FirstName` and `LastName`. When you expose a list of people to an API endpoint you might display a `FullName`. The `FullName` property could be a concatenation of the `FirstName` and `LastName` properties. But typically you would then have a entity class `Person` mapping to a "presentation class" `PersonDTO`. You have two choices when it comes to mapping - you can do it manually or you can let a mapping library such as AutoMapper do it for you. I am not in either camp. I think both approaches work depending on your scenario. The focus will be on one mapping library - Mapster.

## Using Mapster

Lets start with a simple solution - a test project and a class library. The class library will consist of an EFCore context with a single entity - `Person`. I will also add a data transformation class (DTO) `PersonDto`. I created three tests - one to test the context, another to do a manual projection and one to do a projection using Mapster. The DbContext will be using SQLite - not in-memory but an actual file. At present the code doesn't do any heavy validation in terms of checking for duplicates. 

You can view the code for the classes used in the [GitHub repo](https://github.com/thefremus/devimojo-code/blob/main/source/Mapping/Mapping.Data/)

The `Person` entity contains exactly the same properties as `PersonDto`. In the first test I keep it really simple - I insert some data into the SQLite database. In the second test I perform a manual projection using a select loading. In the third test I perform a projection using Mapster's `ProjectToType` extension method. All the tests pass. But what have we really learned? 

```csharp

    [Fact]
    public async Task People_Insert_Test_Expect_Data_To_Be_Present()
    {
        //arrange
        var builder = new DbContextOptionsBuilder<PeopleContext>()
            .UseSqlite("Data Source=people.db;");

        var context = new PeopleContext(builder.Options);

        var json = await File.ReadAllTextAsync("people.json");
        var peopleList = JsonSerializer.Deserialize<List<Person>>(json);

        foreach (var person in peopleList)
        {
            person.Id = Guid.NewGuid();
            context.People.Add(person);
        }

        //act
        await context.SaveChangesAsync();

        //assert
        var personActual = context.People.First();
        Assert.NotNull(personActual);
    }

    [Fact]
    public async Task GetPeople_Manual_Mapping()
    {
        //arrange
        var builder = new DbContextOptionsBuilder<PeopleContext>()
            .UseSqlite("Data Source=people.db;");

        var context = new PeopleContext(builder.Options);

        //act
        var peopleList = await context.People.Select(p => new PersonDto { 
            EmailAddress = p.EmailAddress, 
            FirstName = p.FirstName, 
            Id = p.Id, 
            LastName = p.LastName }).ToListAsync();

        //assert
        Assert.NotNull(peopleList);
    }

    [Fact]
    public async Task GetPeopleList_Mapster_Mapping()
    {
        //arrange
        var builder = new DbContextOptionsBuilder<PeopleContext>()
            .UseSqlite("Data Source=people.db;");

        var context = new PeopleContext(builder.Options);

        //act
        var peopleList = await context.People.ProjectToType<PersonDto>().ToListAsync();

        //assert
        Assert.NotNull(peopleList);
    }

```

I would like to run a few benchmarks using BenchMark.NET to see the performance difference between the two. For the benchmark I'll create a console application - I'm not sure if you can run BenchMark.NET in your tests. Anyway I setup a small .NET Core console app. It has a class called `PeopleService` with a method for manual mapping and mapping using Mapster. 

```csharp

var summary = BenchmarkRunner.Run(typeof(Program).Assembly);

public class PeopleService
{
    private readonly PeopleContext _context;
    public PeopleService()
    {
        var builder = new DbContextOptionsBuilder<PeopleContext>()
                            .UseSqlite("Data Source=people.db;");

        _context = new PeopleContext(builder.Options);
    }

    [Benchmark]
    public IList<PersonDto> GetPeopleListFromManualMapping() 
    {
        return _context.People.Select(p => new PersonDto
        {
            EmailAddress = p.EmailAddress,
            FirstName = p.FirstName,
            Id = p.Id,
            LastName = p.LastName
        }).ToList();
    }

    [Benchmark]
    public IList<PersonDto> GetPeopleListFromMapster()
    {
        return _context.People.ProjectToType<PersonDto>().ToList();
    }
}

```

The result from running the benchmark appears to show little to no difference between the two approaches. 

![BenchMark](img/benchmark-dotnet-mapping.png)

## What have we learned?

So what did we really learn? Having to manually write projections for EFCore can be counter productive. In some cases it could possibly lead to a duplication of code. Lets say, using the example above, you have a projection using a filter. Would you repeat the same projection? We also learned, I think, to not avoid using a mapping library. Or should I say stick your head in the sand. One reason I do find mappers tricky is the usage. You can use a mapper in many different ways - not all of them are necessarily good. If you read through [Jimmy Bogard's post](https://jimmybogard.com/automapper-usage-guidelines/) he gives some good advice when using AutoMapper. I just feel mappers can be tricky - in such cases it is so easy to fallback to writing manual transformations.