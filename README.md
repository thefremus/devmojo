# Dev Mojo

## Introduction

The purpose of this particular repository is to keep track of my learning. I want to keep a journal/log style record of the things I read or watch. I often find myself reading articles or watching video without enough cognisance of what I actually just saw. I feel at times there is a need to take things a bit slower - giving yourself the time to understand the topic at hand. I find myself rushing through an article or video too often. Getting to the end result prematurely often leaves me disatisfied. If you take the time - it doesn't matter how long either - to learn about something is a better approach. I think the reason we prematurely get to the endpoint too quickly is possibly a lack of consistency. A commitment to consistency over a period of time will lead to a better outcome in the long term. 

## Goals

The goal is to develop a consistent developer-focused learning discipline. I feel you do not have to spend massive amounts of time focused on 'learning'. You can allocate a small portion of time everyday to read about things. Often it is the small pieces of knowledge with the biggest impact. Reading about one small piece of technology can change the way you do things. So my goal is to set aside the same amount of time everyday for learning. The other goal stemming from this is to rather focus on the detail as much as possible and to avoid skimming things. You cannot get to a great level of expertise by skimming things. 

## Full Stack Software Engineering

Not sure if Full Stack Software Engineering is a thing or not. Either way software engineering as a practice covers certain disciplines. You can build a front-end using web technologies such as Angular or React. You could also build a front-end for mobile or desktop using technologies such as Xamarin. The majority of front-end applications integrate with a backend. A backend can be something such as an RESTful API. A RESTful API exposes HTTP endpoints. The backend itself also typically connects to a data persistence technology such as SQL Server. In addition to the afforementioned areas most applications are run in the cloud. Cloud computing is an area of focus in its own right - I see it as something separate. 

## Sources of learning

I have been asked in many interviews how I remain up-to-date on the latest trends. The latest trends are not always the best thing for me in the moment. Sometimes even the "older" things remain relevant. Many software engineering books written 20 or more years ago provide very relevant learning for today. To me it feels like focusing on achieving consistency is more relevant. It is important to know about the newer ways of doing things - often they build on the older ways too though. In saying I find several ways of learning to be extremely useful.

1. Reading code from repositories
2. Watching video material
3. Reading books/articles
4. Writing your own code

## .NET

### ASP.NET Core

An interesting way to do [API Versioning](https://github.com/dotnet/aspnet-api-versioning/wiki/API-Documentation). 

### SpecFlow

[SpecFlow](https://specflow.org/)

### Mapster

Most or many of the projects I have been working on use AutoMapper - a popular library used to map object properties. What is the basic idea? Well in most .NET projects you usually have entities mapping to a database. You also have classes with very similar properties to the entity classes. You might not always want to expose all the properties of your entity class to a front-end application - so you use a transformation class (DTO). A DTO (Data Transformation Object) is a lightweight object used typically in API endpoints. The endpoints produce JSON in many cases. While you theoretically can expose an entity to an endpoint it does mean you are potentially rendering irrelevant information to an endpoint. You might also want to apply some logic somewhere in your layered application to return specific pieces of information. The entity class can in some cases act as a conditional variable. You can then use the entity to return a DTO based the state of an entity class. 

Typically then a mapper library is used to take an entity class as an source and a DTO as a target. Most mappers also perform reverse mapping - from the DTO to the entity. Question is why would you want to do this? Well two schools of thought around mapping exist - manual mapping or auto mapping. Manual mapping is the process of generating a DTO from an entity class by using your own transformation methods. 

After watching [Mapster, the best .NET mapper that you are (probably) not using](https://www.youtube.com/watch?v=UIslFVEHkzA) and reading [Enjoy Using Mapster in .Net 6](https://medium.com/@M-S-2/enjoy-using-mapster-in-net-6-2d3f287a0989) I felt the need to explore the word of mapping for myself. To be honest up to this point I have only seen mapping as a necessary evil - in the projects I worked on I keep using them where they are used. In some cases though I use manual mapping, especially when writing projections from an EF Core DbContext. The thing that struck me most in the video is the performance gains - the difference performance difference between manual mapping seems very little.

So to get going I am going to create a small project - with a test project, and a class library. The goal is to get to the heart of the functionality - but to understand what is happening as well.

## Video Learning

- [What is Span in C# and why you should be using it](https://www.youtube.com/watch?v=FM5dpxJMULY)
- [How Controller behaviour changed in .NET 7](https://www.youtube.com/watch?v=r5VJIz25PPY)
- [Mapster, the best .NET mapper that you are (probably) not using](https://www.youtube.com/watch?v=UIslFVEHkzA)
- [4 C# features that you (probably) shouldn't be using](https://www.youtube.com/watch?v=yzg5-T67FCc)
- [8 await async mistakes that you SHOULD avoid in .NET](https://www.youtube.com/watch?v=lQu-eBIIh-w)
- [C# 11's NEW elegant string conversion](https://www.youtube.com/watch?v=uoIbKO-zKeQ)

### 16 May 2022

- [What is .NET MAUI? - .NET Maui Crash Course #0](https://www.youtube.com/watch?v=mgW6xviirQk)

## Reading

- [Enjoy Using Mapster in .Net 6](https://medium.com/@M-S-2/enjoy-using-mapster-in-net-6-2d3f287a0989)
- [8 quick tips to improve your .NET API](https://medium.com/neogrid/8-quick-tips-to-improve-your-net-api-6c44faf258e0)
- [.Net 6 vs .Net 5: How .Net 6 Has Changed the Game of Software Development?](https://blogs.ashutec.com/net-6-vs-net-5-how-net-6-has-changed-the-game-of-software-development-8b3503de7643)
- [A common mistake almost all the developer does in the Entity Framework](https://medium.com/abhima-c-programming/a-common-mistake-almost-all-the-developer-does-in-the-entity-framework-41b52d3d3193)
- [C# 6 Performance Tricks](https://ikbalkazanc.medium.com/c-6-performance-tricks-ae749a7a8c45)
- [5 Good Practices for Error Handling in C#](https://medium.com/dotnetsafer/5-good-practices-for-error-handling-in-c-9faee15404fa)
- [Setting up JWT Bearer authentication in ASP.NET Core](https://blog.devgenius.io/jwt-bearer-authentication-for-machine-to-machine-and-single-page-applications-1c8ba1211a90)
- [Dependency Inversion vs. Dependency Injection](https://betterprogramming.pub/straightforward-simple-dependency-inversion-vs-dependency-injection-7d8c0d0ed28e)
- [Real-world open-source project based on .NET 6 with DDD, ES, CQRS, Testing concepts](https://medium.com/@hamed.shirbandi/real-world-open-source-project-based-on-ddd-es-cqrs-af261cc24353)
- [The 10 Commandments .NET Developers Must apply for Secure Applications](https://medium.com/dotnetsafer/the-10-commandments-net-developers-must-apply-for-secure-applications-a11bee856e9a)
- [Generating Class Diagrams for .Net Core](https://medium.com/better-programming/generating-class-diagrams-for-net-core-c4913db9398b)
- [C# programming — Top 10 useful features you should know](https://medium.com/whatfix-techblog/c-programming-top-10-useful-features-you-should-know-ef5ea1fb7c69)
- [C# — Action vs Func](https://medium.com/@serhat21zor/c-action-vs-func-62fe917da43f)
- [C# Type Converter](https://medium.com/c-sharp-progarmming/c-type-converter-2fec57bb1a13)
- [C# 11 is Coming! 5 Features that will Blow your Mind 🤯](https://medium.com/dotnetsafer/c-11-is-coming-5-features-that-will-blow-your-mind-be8a736e8f71)
- [Dependency Inversion Principle: How Google Developers write code](https://paigeshin1991.medium.com/dependency-inversion-principle-how-google-developers-write-code-f6cbd3b530a6)
- [How to use CancellationToken in your .NET API requests](https://medium.com/geekculture/how-to-use-cancellationtoken-in-your-net-api-requests-4bdfaa9f8511)
- [The Big Fight — Dapper vs Entity Framework 6 Detailed Benchmark](https://medium.com/@salihcantekin/the-big-fight-dapper-vs-entity-framework-detailed-benchmark-2345af933382)
- [Different ways to implement IHttpClientFactory in .NET core apps](https://mahesh-more.medium.com/different-ways-to-implement-ihttpclientfactory-in-net-core-apps-5fd3f547a206)
- [3 Horrible Techniques in C# You Should Avoid To Save Your Job](https://medium.com/codex/3-horrible-techniques-in-c-you-should-avoid-to-save-your-job-bc52b8ba5183)
- [Using yield keyword to write better code in c#](https://medium.com/@amrelsher07/using-yield-keyword-to-write-better-code-in-c-1919267e5327)
- [Creating a ASP.NET Core Web API in .NET 6 with NUXT 3](https://medium.com/@iliescu.dorin/creating-a-asp-net-core-web-api-in-net-6-with-nuxt-3-template-5720baad0530)
- [How I refactored a nested if/else validation using a design pattern](https://medium.com/@arnab.sen44/how-i-refactored-a-nested-if-else-validation-using-a-design-pattern-ce287c32851d)
- [10 Best C# NuGet Packages to Improve Your Productivity in 2022](https://medium.com/syncfusion/10-best-c-nuget-packages-to-improve-your-productivity-in-2022-593825ecd0b0)
- [.NET MAUI Closer Than Ever (Discover +5 New Features)](https://medium.com/dotnetsafer/net-maui-closer-than-ever-discover-5-new-features-70386d83e56f)
- [.NET Top NuGet Packages Every Developer Should Know In 2022](https://medium.com/@kylia669/net-top-nuget-packages-every-developer-should-know-in-2022-8929cbe178da)

### 13 May 2022

- [Microsoft .NET 6: Top 10 New Features](https://medium.com/accedia/microsoft-net-6-top-10-new-features-7464cd8c6549)
- [Heap, Stack and Garbage Collector — A practical guide to .NET memory management system.](https://andresantarosa.medium.com/heap-stack-e-garbage-collector-a-practical-guide-to-net-memory-management-system-7e60bbadf199)
- [.NET Core Best Practices](https://medium.com/@nilebits/net-core-best-practices-6a2a4f25de8e)
- [A simple way to validate the data in C#](https://medium.com/abhima-c-programming/a-simple-way-to-validate-the-data-in-c-2fafb797b956)
- [Essential 10 .NET Libraries every developer must know!](https://medium.com/dev-genius/essential-10-net-libraries-every-developer-must-know-fc413cbfab05)

### 16 May 2022

- [CSharpCodingStandard](https://github.com/hassanhabib/CSharpCodingStandard/blob/master/Methods.md#115-chaining-uglificationbeautification)
- [An Elegant Way to Mock DateTime.Now in Your C# Application](https://levelup.gitconnected.com/an-elegant-way-to-mock-datetime-now-in-your-c-application-a81e59e62836)
- [Method Code Smells and Refactorings](https://amrelsher07.medium.com/method-code-smells-and-refactorings-bd9383ee6432)
- [Difference between IOptions, IOptionsSnapshot and IOptionsMonitor In Asp.netCore](https://alirezafarokhi.medium.com/difference-between-ioptions-ioptionssnapshot-and-ioptionsmonitor-in-asp-netcore-587954bbcea)
- [An Introduction to Writing High-Performance C# Using Span<T> Struct](https://medium.com/@nishanc/an-introduction-to-writing-high-performance-c-using-span-t-struct-b859862a84e4)

### 17 May 2022

- [7 Features of Blazor That Make It an Outstanding Framework for Web Development](https://medium.com/syncfusion/7-features-of-blazor-that-make-it-an-outstanding-framework-for-web-development-205352330b8f)
- [Using MassTransit to manage message queues](https://medium.com/geekculture/using-masstransit-to-manage-message-queues-4a4bf4103466)
- [Experience the Adaptive UI Layout of Blazor DataGrid for All Devices](https://medium.com/syncfusion/experience-the-adaptive-ui-layout-of-blazor-datagrid-for-all-devices-7173e6c68e43)
- [Why you shouldn’t call .Result when dealing with async code in C#](https://medium.com/@jamie-burns/why-you-shouldnt-call-result-when-dealing-with-async-code-in-c-affee2142c86)
- [What is Method Idempotence?](https://medium.com/@yildiraygemuk/what-is-method-idempotence-cfedf2c0194d)

### 18 May 2022

|Article                                                                                                                         |Tags                   |
|--------------------------------------------------------------------------------------------------------------------------------|-----------------------|
|[ASP.NET Core Http Security Header](https://muratsuzen.medium.com/asp-net-core-http-security-header-cf4d0fb61df8)               |ASP.NET Core, Security |
|[Best Linq Performance](https://medium.com/@hussein.nm/best-linq-performance-2dfe7fc7eff2)                                      |.NET Core, Lambda, Linq|
|[OpenTelemetry with Jaeger in .NET Core](https://medium.com/@niteshsinghal85/opentelemetry-with-jaeger-in-net-core-9b1e009a73dc)|ASP.NET Core, Telemetry|
|[Different Ways to Inject Dependencies in .NET Core](https://medium.com/@AzilenTech/different-ways-to-inject-dependencies-in-net-core-d147ad0279cd)                               |.NET Core, Dependency Injection, Inversion of Control|
|[Using Multiple DbContext on .NET 6 Web API With Repository Pattern](https://muratsuzen.medium.com/using-multiple-dbcontext-on-net-6-web-api-with-repository-pattern-3d223874e625)                |ASP.NET Core, EF Core, Dependency Injection  |

### 19 May 2022

|Article                                                                                                        |Source |Tags               |
|---------------------------------------------------------------------------------------------------------------|-------|-------------------|
|[Scoped, Transient and Singleton](https://taylancanh.medium.com/scoped-transient-and-singleton-e6c4f8811b52)   |Medium |.NET Core, Scopes  |
|[Good API design, bad API design](https://levelup.gitconnected.com/good-api-design-bad-api-design-2405dcdde24c)|Medium |API Design         |
|[How to use C# delegates to sanitise your codebase](https://mina-pecheux.medium.com/how-to-use-c-delegates-to-sanitise-your-codebase-424835e8ce28)              |Medium |.NET, C#, Delegates|
|[Clean Code — A practical approach](https://medium.com/clarityai-engineering/clean-code-a-practical-approach-896546435235)|Medium|Clean Code|
|[Why I “hate” optional parameters in C#](https://medium.com/@thecodewrapper/why-i-hate-optional-parameters-in-c-82bc0d17a2e6)|Medium|C#, .NET, Optional Parameters|
|[Framework libraries](https://docs.microsoft.com/en-us/dotnet/standard/framework-libraries)|Microsoft Docs|.NET,Framework|


## Course Material

### Microsoft Learn

- [Build Apps With .NET MAUI](https://docs.microsoft.com/en-us/learn/paths/build-apps-with-dotnet-maui/)
    - [Introduction](https://docs.microsoft.com/en-us/learn/dotnet-maui/build-mobile-and-desktop-apps/1-introduction)
    - [Describe the .NET MAUI architecture](https://docs.microsoft.com/en-us/learn/dotnet-maui/build-mobile-and-desktop-apps/2-describe-maui-architecture)
    - [Exercise: Create your first .NET MAUI app](https://docs.microsoft.com/en-us/learn/dotnet-maui/build-mobile-and-desktop-apps/4-exercise-create-your-first-maui-app)
    - [Add visual controls to a .NET MAUI app](https://docs.microsoft.com/en-us/learn/dotnet-maui/build-mobile-and-desktop-apps/5-add-controls-to-the-ui)
    - [Exercise: Create the phone number translator app](https://docs.microsoft.com/en-us/learn/dotnet-maui/build-mobile-and-desktop-apps/6-exercise-create-phone-number-translator-app)
    - [Summary](https://docs.microsoft.com/en-us/learn/dotnet-maui/build-mobile-and-desktop-apps/7-summary)

## Writing

### Notes

### 18 May 2022

- [Introducing .NET MAUI](/notes/introducing-net-maui.md)