# Park Finder API. 

#### API Building in C# for Epicodus 09.08.2022

### By Adrienne Matosich 

## Description

Another C# independent project to build an API with C#/ .Net Core, as well as how to build an MVC with full CRUD functionality to interact with an API. This API contains national and state parks in the western United States. My goal is to create a simple MVC web application for the client side to allow users to GET, POST, PUT, and DELETE parks. 

## Setup/Installation Requirements

*_These instructions are specifically for MySql Workbench, but should work similarly for or any generic SQL database manager._* 

1.  Navigate to the [ParksAPI.Solution repository](https://github.com/adrienne_matosich/ParksAPI.Solution) or open your terminal

2. Clone this project using the GitHub button or the command:
`$ git clone https://github.com/adrienne_matosich/ParksAPI.Solution.git`

3. Navigate to the `ParksAPI.Solution` directory in your editor of choice, or use [Visual Studio Code](https://code.visualstudio.com/)

4. Within the project, navigate to the Factory directory, and type `dotnet restore`, then `dotnet build`. 

5. After the build is complete, run the command `dotnet ef database update`. This will create a `adrienne_matosich` database in MySql Workbench. Open or refresh MySql Workbench and confirm that the new database has been created.

6. . Type `dotnet run` into the terminal. At this time, the API is usable in an API development tool such as Postman.

## User Stories

As a user, I want to GET and POST state and national parks. As a user, I want to GET a list of parks by state or type. As a user, I want to PUT and DELETE parks.

## Parks

## HTTP Request
`POST: /api/parks -
 GET: /api/parks/{id} -
 PUT: /api/parks/{id} -
 DELETE: /api/parks/{id}`

### Path Parameters

| Parameter     | Type      | Default  | Required  | Description                |
| ------------- | --------- | -------- | ----------|-----------------           |
|   state       | string    | none     | false     | Return matches by state    |
|   type        | string    | national, state    | false     | Return matches by type   |

## Example Query
`http://localhost:5000/api/parks?state=Oregon&type=state`


## Sample JSON Response
`{
  "parkId": 4
  "name": "Bridal Veil Falls",
  "state": "Oregon",
  "type": "state",
}`

## Getting Started with Swagger
[Swagger](https://swagger.io/), also known as [OpenAPI](https://www.openapis.org/), solves the problem of generating useful documentation and help pages for Web APIs. It provides benefits such as interactive documentation, client SDK generation, and API discoverability.


## Swagger Implementation with Swashbuckle
 Swashbuckle is a Swagger generator that builds SwaggerDocument objects directly from your routes, controllers, and models. It's typically combined with the Swagger endpoint middleware to automatically expose Swagger JSON.
 Install `dotnet add <ParksApi>.csproj package Swashbuckle.AspNetCore -v 6.2.3` to begin the process of setting up Swagger. 

## Add and configure Swagger middleware

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<TodoContext>(opt =>
        opt.UseInMemoryDatabase("TodoList"));
    services.AddControllers();

    // Register the Swagger generator, defining 1 or more Swagger documents
    services.AddSwaggerGen(c =>
    {
        c.SwaggerDoc("v1", new OpenApiInfo { Title = "My API", Version = "v1" });
    });
}
```
In the `Startup.Configure` method, enable the middleware for serving the generated JSON document and the Swagger UI:

```csharp
public void Configure(IApplicationBuilder app)
{
    // Enable middleware to serve generated Swagger as a JSON endpoint.
    app.UseSwagger();

    // Enable middleware to serve swagger-ui (HTML, JS, CSS, etc.),
    // specifying the Swagger JSON endpoint.
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1"); 
    });

    app.UseRouting();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });
}
```
Launch the Swagger app, and navigate to `http://localhost:<yourport>/swagger/v1/swagger.json`. The generated document describing the endpoints appears as shown in [Swagger specification (swagger.json)](https://docs.microsoft.com/aspnet/core/tutorials/web-api-help-pages-using-swagger#swagger-specification-swaggerjson).

The Swagger UI can be found at `http://localhost:<yourport>/swagger`. Explore the API via Swagger UI and incorporate it in other programs.


## appsettings.json

Update your username and password in the appsettings.json file. By default these are set to:
user:root and an [empty password].

## Protecting Your Data

1. In your project's root directory, create an .gitignore file.

2. Add the following to your .gitignore file (this protects your sensitive data).
    DO NOT PROCEED UNTIL YOU COMPLETE THIS STEP!
    * appsettings.json
    * bin/
    * obj/

3. Commit your .gitignore file.

## Stretch Goals
* CLient Side API
* Authentication with Identity
* Search functionality

## Known Bugs
WIP progress for the client side API. 

## Support and Contact Details

If there are any issues or questions, please reach out to me through [my GitHub account](https://github.com/ampando).

## Technologies Used

*  [Visual Studio Code](https://code.visualstudio.com/)
*  [Markdown](https://daringfireball.net/projects/markdown/)
*  [C#](https://docs.microsoft.com/en-us/dotnet/csharp/)
*  [.NET5.0](https://dotnet.microsoft.com/download/dotnet-core/net5.0)
*  [ASP.NET Core MVC](https://docs.microsoft.com/en-us/aspnet/core/mvc/overview?view=aspnetcore-5.0)
*  [Entity FrameWork](https://docs.microsoft.com/en-us/ef/)
* [Postman](https://www.postman.com/)
* [SQL/MySqlWorkbench](https://www.mysql.com/products/workbench/)
* [Swagger](https://swagger.io/tools/swaggerhub/?&utm_source=aw&utm_medium=ppcg&utm_campaign=SEM_SwaggerHub_PR_NA_ENG_EXT_Prospecting&utm_term=swagger&utm_content=511173019809&gclid=Cj0KCQjw6_CYBhDjARIsABnuSzqhk832OxfUnJQrObnkOSGeOz5PDaFWhbXwfR2RwtueOlioKgGBz_8aAnoKEALw_wcB&gclsrc=aw.ds)
* [Swashbuckle](https://www.c-sharpcorner.com/article/swashbuckle-and-asp-net-core/) 


### License

*This project uses the following license: [MIT](https://opensource.org/licenses/MIT)*

Copyright(c) 2022  **_Adrienne Matosich_** 