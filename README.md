# My-NET-Worker

#### Worker builded with NET CLI

#### The Worker Service template is available to the .NET CLI, and Visual Studio. For more information, see .NET CLI, dotnet new worker - template. The template consists of a Program and Worker class.
    
    

```sh
using App.WorkerService;

IHost host = Host.CreateDefaultBuilder(args)
    .ConfigureServices(services =>
    {
        services.AddHostedService<Worker>();
    })
    .Build();

await host.RunAsync();

```

#### The preceding Program class:

* Creates the default IHostBuilder.
* Calls ConfigureServices to add the Worker class as a hosted service with AddHostedService.
* Builds an IHost from the builder.
* Calls Run on the host instance, which runs the app.

```sh
<PropertyGroup>
     <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>

```

#### The Program.cs file from the template can be rewritten using top-level statements:

```sh

using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using App.WorkerService;

using IHost host = Host.CreateDefaultBuilder(args)
    .ConfigureServices((hostContext, services) =>
    {
        services.AddHostedService<Worker>();
    })
    .Build();

await host.RunAsync();


```

#### This is functionally equivalent to the original template. For more information on C# 9 features, see What's new in C# 9.0.

As for the Worker, the template provides a simple implementation.

```sh

namespace App.WorkerService
{
    public class Worker : BackgroundService
    {
        private readonly ILogger<Worker> _logger;

        public Worker(ILogger<Worker> logger)
        {
            _logger = logger;
        }

        protected override async Task ExecuteAsync(CancellationToken stoppingToken)
        {
            while (!stoppingToken.IsCancellationRequested)
            {
                _logger.LogInformation("Worker running at: {time}", DateTimeOffset.Now);
                await Task.Delay(1000, stoppingToken);
            }
        }
    }
}


```

#### The preceding Worker class is a subclass of BackgroundService, which implements IHostedService. The BackgroundService is an abstract class and requires the subclass to implement BackgroundService.ExecuteAsync(CancellationToken). In the template implementation the ExecuteAsync loops once per second, logging the current date and time until the process is signaled to cancel.


## The project file

#### The Worker Service template relies on the following project file Sdk:

```sh

<Project Sdk="Microsoft.NET.Sdk.Worker">

```
