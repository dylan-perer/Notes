## Controller and a view
```c#
/*
	> Make a controller[TestController] (make sure you have the name 'Controller' at the end)
	> Make a View foler[Test] with the name of the controller
	> Make a razorpage 
	> Vist the page by going > test/GoToTestView
*/
//inside of teh controller

public ActionResult GoToTestView()
{
	return View("MyTestView");//name of the razor view, if the ActionName is the same as the razor page, dont need to specify the name
}

```

## Passing data
### Controller to view
```c#
//inside the controller
public IActionResult Index()
{
	ViewData["date"] = DateTime.Now.ToString();
	
	//using view bag
	ViewBag.MyTime = DateTime.Now.ToString();
	return View();
}
```

```cshtml
@*inside the view*@
<h1>Welcome to to test</h1>
<p>@ViewData["date"]</p>
@*using view bag*@
<p>@ViewBag.date</p>
```

### Temp data 
```c#
/** Controller to Controller (survie only one request) **/
/* 	Temp data will persist, if its is not read by a view*/
//inside the controller
//passing data from Action Index to Test2
public IActionResult Index()
{
	TempData["date"] = DateTime.Now.ToString();
	return View();
}

public IActionResult Test2()
{
	ViewData["date"] = TempData["date"];
	return View();
}
```
```cshtml
<div>
	@TempData["t1"] @*Reading the temp data*@
	@{
		TempData.Keep("t1") //Calling to persist the temp data, now it wont drop temp data after the read
	}
</div>

<div>
	@{
		string str = TempData.Peek("t1").ToString //value is considered not read
	}
</div>
```
## Sessions
```c#
/*
	1. Add nuGet package asp.NET sessions
	2. add service and middleware (see 1s code below)
*/
public void ConfigureServices(IServiceCollection services)
{
	services.AddControllersWithViews();
	services.AddSession(options => {//add this
		options.IdleTimeout = TimeSpan.FromMinutes(1);//You can set Time   
	});
}

 public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
	 ....
	app.UseStaticFiles();
	app.UseSession(); // add this
	app.UseRouting();
	 ....
}
```

### Session Objects
```c#
//create new .cs file
using Microsoft.AspNetCore.Http;
using Newtonsoft.Json;

namespace MVC_Training.Extensions
{
    public static class SessionExtensions
    {
        public static void SetObject(this ISession session, string key, object value)
        {
            session.SetString(key, JsonConvert.SerializeObject(value));
        }

        public static T GetObject<T>(this ISession session, string key)
        {
            var value = session.GetString(key);
            return value == null ? default(T) : JsonConvert.DeserializeObject<T>(value);
        }
    }
}

//inside the controller | import the extension
List<Customer> customers = HttpContext.Session.GetObject<List<Customer>>("Customers");//get object
HttpContext.Session.SetObject("Customers", customers);//set object
```

```c#
//inside the controller
public IActionResult Index()
{
	HttpContext.Session.SetString("NAME", "Dyalan");
	HttpContext.Session.SetInt32("AGE", 24);
	return View();
}

public IActionResult Test2()
{
	ViewData["NAME"] = HttpContext.Session.GetString("NAME");
	ViewData["AGE"] = HttpContext.Session.GetInt32("AGE");
	return View();
}

```

## Models CRUD
```c#
/*
	1. create a model (i.e. customer)
	2. add a new view ==>< choose RAZOR VIEW > for the TEMPLATE choose the model
	3. choose a crud operation adn hit create
*/
```

```c#
//our simple model
public class Customer
{
	public int Id { get; set; }
	public string Name { get; set; }
}
```

### View
```c#
//inside the controller
public IActionResult Customers()//shows the current list of customers
{
	List<Customer> customers = HttpContext.Session.GetObject<List<Customer>>("Customers");
	if(customers == null)//if no session exists, create one
	{
		customers = new List<Customer>();
		customers.Add(new Customer { Id=1, Name="Elise"});
		HttpContext.Session.SetObject("Customers", customers);
	}
	return View(customers);
}
```

```cshtml
@model IEnumerable<MVC_Training.Models.Customer>

@{
    Layout = null;
}

<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Customers</title>
</head>
<body>
<p>
    <a asp-action="NewCustomer">Create New</a>
</p>
<table class="table">
    <thead>
        <tr>
            <th>
                @Html.DisplayNameFor(model => model.Id)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Name)
            </th>
            <th></th>
        </tr>
    </thead>
    <tbody>
@foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Id)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.ActionLink("Edit", "Edit", new { /* id=item.PrimaryKey */ }) |
                @Html.ActionLink("Details", "Details", new { /* id=item.PrimaryKey */ }) |
                @Html.ActionLink("Delete", "Delete", new { /* id=item.PrimaryKey */ })
            </td>
        </tr>
}
    </tbody>
</table>
</body>
</html>

```
### Create
```c#
public IActionResult NewCustomer()//shows a form new customer form 
{
	return View();
}

[HttpPost]
public IActionResult CreateCustomer(int Id, string Name)//create form calls to this action
{
	Customer customer = new Customer { Id = Id, Name = Name };
	List<Customer> customers = HttpContext.Session.GetObject<List<Customer>>("Customers");
	customers.Add(customer);
	HttpContext.Session.SetObject("Customers", customers);
	return Redirect("Customers");
}

//REMEBER: make sure asp tags are right and forms method is set to POST
<form asp-action="CreateCustomer" method="post">
```

## Data Annotations (Validations)
```c#
//inside the model
using System.ComponentModel.DataAnnotations;

namespace MVC_Training.Models
{
    public class Customer
    {
        [Required]public int Id { get; set; }
        [Required][StringLength(10, MinimumLength = 3)]public string Name { get; set; }
    }
}
```

```c#
//inside the action
public IActionResult CreateCustomer(Customer customer)
{
	if (ModelState.IsValid)//check if any validation errors
	{
		....
		return Redirect("Customers");
	}
	return View("NewCustomer");//if not valid return back with errors
}
```

```cshtml
@Html.ValidationSummary(); @*inside the view, we can see the errors*@
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

using ContosoUniversity.Models;
using Microsoft.EntityFrameworkCore;

namespace ContosoUniversity.Data
{
    public class SchoolContext : DbContext
    {
        public SchoolContext(DbContextOptions<SchoolContext> options) : base(options)
        {
        }

        public DbSet<Course> Courses { get; set; }
        public DbSet<Enrollment> Enrollments { get; set; }
        public DbSet<Student> Students { get; set; }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Course>().ToTable("Course");
            modelBuilder.Entity<Enrollment>().ToTable("Enrollment");
            modelBuilder.Entity<Student>().ToTable("Student");
        }
    }
}
```

```c#
//adding the database context
public void ConfigureServices(IServiceCollection services)
{
	services.AddDbContext<SchoolContext>(options =>
		options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

	services.AddControllersWithViews();
}
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

## TODO: crud async with db context--
## MVC Authentication & Authorize
```c#
//Add auth service
public void ConfigureServices(IServiceCollection services)
{
	...
	services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme).AddCookie(options =>
	{
		options.Events = new CookieAuthenticationEvents()//hooking into events on logings, signouts and validate user executions
		{
			OnSigningIn = async async =>
			{
				await Task.CompletedTask;
			},
			OnSignedIn = async async =>
			{
				await Task.CompletedTask;
			},
			OnValidatePrincipal = async async =>
			{
				await Task.CompletedTask;
			},
		};
	});
}

public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
	...
	app.UseAuthentication();//add these 2 middleware
	app.UseAuthorization();
	...
}
```

```c#
//add secured routes
[Authorize]
public IActionResult Secured()
{
	return View();
}

[Authorize(Roles = "Admin")]//user must have the role of admin to enter this page
public IActionResult Admin()
{
	return View();
}
```

```c#
//Create Account controller
public class AccountController : Controller
{
	public IActionResult Login(string returnUrl)
	{
		ViewData["ReturnUrl"] = returnUrl;//capturing url user was in before redirected to authorize
		return View();
	}

	[HttpPost]
	public async Task<IActionResult> Validate(string username, string password, string returnUrl)
	{
		if (username == "Bob" && password=="pizza") {//add db lookup here

			List<Claim> claims = new List<Claim>();//creating the policy with cookie
			claims.Add(new Claim("username", username));//our own type
			claims.Add(new Claim(ClaimTypes.Name, username));//using claim type

			claims.Add(new Claim(ClaimTypes.Role, "Admin"));//giving ROLE, access to admin pages

			ClaimsIdentity identity = new ClaimsIdentity(claims, CookieAuthenticationDefaults.AuthenticationScheme);
			ClaimsPrincipal claimsPricicle = new ClaimsPrincipal(identity);

			await HttpContext.SignInAsync(claimsPricicle);

			return Redirect(returnUrl);//redirect user where they were
		}
		//on invalid user
		ViewData["ReturnUrl"] = returnUrl;//pass back the return url (user was originaly trying to get in)
		TempData["Error"] = "Invalid Username or Password";
		return View("Login");//return the form view
	}

	[Authorize] //needs to be logged in to logout
	public async Task<IActionResult> Logout()
	{
		await HttpContext.SignOutAsync();
		return Redirect("/");
	}

	public IActionResult AccessDenied()
	{
		return View();
	}
}
```

```cshtml
@*Secured page*@
<h1>This is top secret!</h1>
<h2>Welcome @User.Identity.Name</h2>
<ul>
    @foreach(var c in User.Claims)
    {
        <li>@c.Type: @c.Value</li>
    }
</ul>
```

```cshtml
@*Create login form*@
<h1>Login</h1>

@{
    string returnUrl = ViewData["ReturnUrl"] as string;
    string error = TempData["Error"] as string;
}
<form action="Validate?ReturnUrl=@System.Net.WebUtility.UrlEncode(returnUrl)" method="post">
    <input type="text" name="username" placeholder="username" />
    <input type="password" name="password" placeholder="password" />
    <input type="submit" value="Submit">
    @if (!string.IsNullOrEmpty(error))
    {
        <h4 class="alert-danger" style="padding:20px">@error</h4>
    }
</form>
```

```cshtml
@*Create access denied page*@
<h1>Access Denied</h1>
```

```cshtml
@*Show logout link if user is loged in*@
@if (User.Identity.IsAuthenticated)
{
	<li class="nav-item">
		<a class="nav-link text-dark" asp-area="" asp-controller="Account" asp-action="Logout">Logout</a>
	</li>
}
```
## Action overloading
```c#
public IActionResult NewCustomer()
{
	return View();
}
[ActionName("NewCustomerWithCustomerCode")]//newly mapped url
public IActionResult NewCustomer(string CustomerCode)
{
	return View();
}
```