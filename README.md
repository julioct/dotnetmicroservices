# Building Microservices With .NET (Week 1)
Source code for the first week of the [Building Microservices With .NET Online Course](https://dotnetmicroservices.com).

## Repo structure
* **Play.Catalog**. Catalog microservice.
* **Play.Common**. Common reusable library.
* **Play.Frontend**. React frontend.
* **Play.Infra**. Docker Compose file.
* **Play.Inventory**. Inventory microservice.


## Prerequisites
* [.NET 5 SDK](https://dotnet.microsoft.com/download/dotnet/5.0)
* [Docker Desktop](https://docs.docker.com/get-docker)
* [Latest Node.JS LTS version](https://nodejs.org/en/download)

## To build the microservices
1. Create a local directory to place generated NuGet packages:
```
md packages
```

2. Add a local NuGet source that points to the new packages directory: 
```
dotnet nuget add source [path to your local packages directory] -n PlayEconomy
```
Example:
```
dotnet nuget add source D:\Repos\dotnetmicroservices\packages -n PlayEconomy
```

3. Generate the Play.Common NuGet package into your local packages directory:
```
dotnet pack Play.Common\src\Play.Common\Play.Common.csproj -p:PackageVersion=0.1.0 -o packages
```

4. Build the microservices:
```
dotnet build Play.Catalog\src\Play.Catalog.Service\Play.Catalog.Service.csproj
dotnet build Play.Inventory\src\Play.Inventory.Service\Play.Inventory.Service.csproj
```

## To run the microservices
1. Start the MongoDB and RabbitMQ docker containers:
```
docker-compose -f Play.Infra\docker-compose.yml up -d
```

2. Run the microservices (use a new terminal window for each command):
```
dotnet run --project Play.Catalog\src\Play.Catalog.Service\Play.Catalog.Service.csproj
dotnet run --project Play.Inventory\src\Play.Inventory.Service\Play.Inventory.Service.csproj
```

## To build the frontend
1. Switch to the Play.Frontend directory
2. Install all dependencies:
```
npm install
```

## To run the frontend
1. Start the web server
```
npm start
```
2. Navigate to http://localhost:3000 in your browser.