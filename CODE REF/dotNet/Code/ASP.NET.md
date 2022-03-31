## Getting started
## What is .NET
![[Screenshot 2022-03-05 015921.png]]
### MVC project
```c#
	//make sure asp.NET and database module is installed
	//choose MVC c# project
```

## Routing
![[Screenshot 2022-03-05 112622.png]]
```c#
//routing middleware is location at program.cs
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");//the pattern is https://localhost:55555/Home/Index/{id}
```

## Database
### SQL Server Config
```c#
//make a sql server authentication user
//enable tcp/id through sql server management (not ss management software)
```
### Entity Framework ORM
```c#
//Mircost.Entity.FramworkCore is the .net ORM
```
### Install NuGet packages
```c#
/* 
	1. Mircost.Entity.FramworkCore.sqlServer
	2. Mircost.Entity.FramworkCore.Tools
*
```
### Connection string
```c#
/*
	1. Create the database
	2. In vs --> tools > connect to database > select: Microsoft SQL Server (SqlClient)
	3. Now once database explore is selected you can see connection string in properties -> Data Source=.;Initial Catalog=BikeStores;Integrated Security=True
*
```
![[Screenshot 2022-03-05 133404.png]]

### Approaches
#### Code first
```json
//add this inside appsettings.json
"ConnectionStrings": {
	"codexDB": "Data Source=.;Initial Catalog=BikeStores;Integrated Security=True"
}
```

```c#
// create the entity-models with DB annotations

namespace dbFirst_MVC.Models
{
    [Table("product")]
    public partial class Product
    {
        [Key]
        [Column("id")]
        public int Id { get; set; }

        [Required]
        [Column("name")]
        [StringLength(20)]
        public string Name { get; set; }

        [Column("display_order")]
        public int? DisplayOrder { get; set; }

        [Column("created_at", TypeName = "datetime")]
        public DateTime CreatedAt { get; set; }
    }
}
```

```shell
# run this in NuGet command line
# migrating tables to the DB
add-migration Add{ModelClassName}ToDatabse
```
#### DB first
```c#
//create models with existing database 
```
```shell
# run this in NuGet command line

# change the connection string, and output directories
#using windows authentication
Scaffold-DbContext "Data Source=.;Initial Catalog=BikeStores;Integrated Security=True" Microsoft.EntityFrameWorkCore.SqlServer -outputdir Models -context BikeStoreDbContext -contextdir Data -DataAnnotations -Force

#using SQL server authentication
Scaffold-DbContext "Data Source=faisal;User ID=dylan;Password=sa;Initial Catalog=test" Microsoft.EntityFrameWorkCore.SqlServer -outputdir Models -context testDbContext -contextdir Data -DataAnnotations -Force


# mysql
Scaffold-DbContext "server=localhost;user=root;database=mydb;password=root;port=3306" Pomelo.EntityFrameworkCore.MySql -outputdir Models -context CmsDbContext -contextdir Data -DataAnnotations -Force


```

### Adiing Db Context
```c#
/*
	- if you went with code first: You must create the database context file
	- DB first will create the file for you
*/

namespace dbFirst_MVC.Data
{
    public partial class codexDbContext : DbContext
    {
        public codexDbContext()
        {
        }

        public codexDbContext(DbContextOptions<codexDbContext> options): base(options)
        {
        }

        public virtual DbSet<Product> Products { get; set; }
	}
}
```

```c#
//adding the database context
builder.Services.AddDbContext<codexDbContext>(options => options.UseSqlServer(
        builder.Configuration.GetConnectionString("codexDB")//comes from appsettings json that we set up
));
```

### Accessing data
```c#
//inside our controller

namespace aspnet_ecommerce_mvc.Controllers
{
    public class ActorController : Controller//inherits controller
    {
        private readonly AppDbContext appDbContext;//declare db context to interact with our data


        public ActorController(AppDbContext appDbContext)//we can grab dependecies from constrcutor
        {
               this.appDbContext = appDbContext;//get the injected dbContext
        }

        
        public IActionResult Index()//this is synchronos
        {
            List<Actor> actors = appDbContext.Actors.ToList();
            return View();
        }
    }
}
```

#### Async controller method
```c#
public async Task<IActionResult> Index()//async
{
	List<Actor> actors = await appDbContext.Actors.ToListAsync();
	return View();
}
```

## Serilog
### Packages 
Serilog.AspNetCore
Serilog.Settings.Configuration
Serilog.Sinks.MSSqlServer

### appsettings.json
```json
"Serilog": {
    "MinimumLevel": "Warning",
    "WriteTo": [
      {
        "Name": "MSSqlServer",
        "Args": {
          "connectionString": "Data Source=.;Initial Catalog=Anthera;User ID=dylan;Password=sa",
          "tableName": "Logs",
          "autoCreateSqlTable": true
        },
        "timeStamp": {
          "columnName": "Timestamp",
          "convertToUtc": true
        }
      }
    ]
  }
```

### ConfigureServices
```c#
services.AddLogging();
```

### Program.cs
```c#
public class Program
{
	public static void Main(string[] args)
	{
		 IConfigurationRoot configuration = new ConfigurationBuilder()
			.AddJsonFile("appsettings.json", optional: false, reloadOnChange: true).Build();

		Log.Logger = new LoggerConfiguration().ReadFrom.Configuration(configuration).CreateLogger();

		CreateHostBuilder(args).Build().Run();
	}

	public static IHostBuilder CreateHostBuilder(string[] args) =>
		Host.CreateDefaultBuilder(args)
			.ConfigureWebHostDefaults(webBuilder =>
			{
				webBuilder.UseStartup<Startup>().UseSerilog();
			});
}
```