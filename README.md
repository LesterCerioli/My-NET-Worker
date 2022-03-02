# My-NET-Worker

#### Worker builded with NET CLI

#### The Worker Service template is available to the .NET CLI, and Visual Studio. For more information, see .NET CLI, dotnet new worker - template. The template consists of a Program and Worker class.

using App.WorkerService;

IHost host = Host.CreateDefaultBuilder(args)
    .ConfigureServices(services =>
    {
        services.AddHostedService<Worker>();
    })
    .Build();

await host.RunAsync();


