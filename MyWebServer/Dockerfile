FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["MyWebServer/MyWebServer.csproj", "MyWebServer/"]
RUN dotnet restore "MyWebServer/MyWebServer.csproj"
COPY . .
WORKDIR "/src/MyWebServer"
RUN dotnet build "MyWebServer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyWebServer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyWebServer.dll"]
