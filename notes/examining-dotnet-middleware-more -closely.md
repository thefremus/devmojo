# Examining dotnet middleware more closely

It goes without saying (or does it) having a solid understanding of how ASP.NET Core's middleware works. Specifically with regards to [Filters in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-7.0). My idea here is to go through the documentation above as slowly as possible - to gain a better understanding. Sometimes I get so caught up in madness of deadlines in our day-to-day project work - I fail to just take a moment to gain a better understanding of the technology.

## ASP.NET Core Filters

What are filters? As per [the official documentation](https://learn.microsoft.com/en-us/aspnet/core/mvc/controllers/filters?view=aspnetcore-7.0) filters allow you to run another piece of code during request processing. In my mind request processing refers to an HTTPContext - its the thing coming in or going out when an andpoint in your ASP.NET Core application is hit. If you take a look at a vanilla ASP.Core WebAPI project with the `WeatherForecastController` you will notice the controllers are configured as middleware by looking at the namespace.

```csharp

namespace AspNetCoreMiddleware.Controllers;

[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    private static readonly string[] Summaries = new[]
    {
        "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
    };

    private readonly ILogger<WeatherForecastController> _logger;

    public WeatherForecastController(ILogger<WeatherForecastController> logger)
    {
        _logger = logger;
    }

    [HttpGet(Name = "GetWeatherForecast")]
    public IEnumerable<WeatherForecast> Get()
    {
        return Enumerable.Range(1, 5).Select(index => new WeatherForecast
        {
            Date = DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
            TemperatureC = Random.Shared.Next(-20, 55),
            Summary = Summaries[Random.Shared.Next(Summaries.Length)]
        })
        .ToArray();
    }
}

```

The method `Get` above returns a list of `WeatherForecast` - when you call it from a client application such as Postman it will return a JSON response. But getting to the response ASP.NET Core does pipeline processing on the HTTPRequest. If you look at the abstract `ControllerBase` class you will see it has an HTTPContext property. The HTTPRequest object in turn has an HttpRequest and HttpResponse property - they are part of the processing pipeline. I think of it as someone making a request to a resource and the web server hosting the resource sending back a response. 