## What is Web APi
```c#
/*
	> API, application programming interface is a bunch of exposed functions that we can use to interact with data
	> WEB APi, is when those function are accesseable remotely through HTTP Portocol
	> REMOTLY HOSTED FUNCTIONS OVER HTTP PROTOCOL
*
```
![[Screenshot 2022-03-19 130514.png]]

## What makes a RESTful Api
```c#
/*
	> Uniform Interface
	> Client-server
	> Stateless
	> Layered system
*
```

## Swagger UI
https://docs.microsoft.com/en-us/aspnet/core/tutorials/getting-started-with-swashbuckle?view=aspnetcore-3.1&tabs=visual-studio
### Packages
```shell
Install-Package Swashbuckle.AspNetCore -Version 5.6.3
```

### Middleware
```c#
// Enable middleware to serve generated Swagger as a JSON endpoint.
app.UseSwagger(c =>
{
	c.SerializeAsV2 = true;
});

// Enable middleware to serve swagger-ui (HTML, JS, CSS, etc.),
// specifying the Swagger JSON endpoint.
app.UseSwaggerUI(c =>
{
	c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
});
```
### Service Config
```c#
// Register the Swagger generator, defining 1 or more Swagger documents
services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new OpenApiInfo
    {
        Version = "v1",
        Title = "ToDo API",
        Description = "A simple example ASP.NET Core Web API",
        TermsOfService = new Uri("https://example.com/terms"),
        Contact = new OpenApiContact
        {
            Name = "Shayne Boyer",
            Email = string.Empty,
            Url = new Uri("https://twitter.com/spboyer"),
        },
        License = new OpenApiLicense
        {
            Name = "Use under LICX",
            Url = new Uri("https://example.com/license"),
        }
    });
});
```

## Middleware
![[Screenshot 2022-03-19 133810.png]]

## Simple controller
```c#
namespace REST_APi.Controllers
{
    [ApiController]
    [Route("api/[controller]")]//base url = tickects
    public class TicketsController : Controller
    {
        [HttpGet]
        public IActionResult Get()
        {
            return Ok("Returning all tickets");
        }

        [HttpGet]
        [Route("{Id}")]
        public IActionResult GetById(int Id)
        {
            return Ok($"Returning ticket id {Id}");
        }

        [HttpPost]//we can specify where the data is coming from, here it is the body (complex object, default is the body request)
        public IActionResult Create([FromBody]Ticket ticket)
        {
            return Ok($"Creating ticket {ticket}");
        }

        [HttpPut]
        [Route("{Id}")]
        public IActionResult Update(int Id)
        {
            return Ok($"Updating ticket id {Id}");
        }

        [HttpDelete]
        [Route("{Id}")]
        public IActionResult Delete(int Id)
        {
            return Ok($"Deleting ticket id {Id}");
        }
    }
}

```
## Model Validation
```c#
public class Ticket { 

	[Required(ErrorMessage = "Id is required")]
	public int? Id { get; set; }// ? will make the default value null rather than a 0
	[Required(ErrorMessage = "Title is required")]
	public string Title { get; set; }
	[Required(ErrorMessage = "Description is required")]
	public string Desc { get; set; }

	public override string ToString()
	{
		return $"ID: {this.Id} Title: {this.Title} DESC: {this.Desc}";
	}
}
```

### Custom Validation
#### Strongly typed class

```c#
//custom validation where checks against db for unique email
using CommunityDrivenSocialPlatform_APi.Data;
using CommunityDrivenSocialPlatform_APi.Model;
using System.ComponentModel.DataAnnotations;
using System.Linq;

namespace CommunityDrivenSocialPlatform_APi.Validaton
{
    public class UserEnsureUniqueEmail : ValidationAttribute
    {
        protected override ValidationResult IsValid(object value, ValidationContext validationContext)
        {
            User user = validationContext.ObjectInstance as User;
            CDSPdB dbContext = (CDSPdB)validationContext.GetService(typeof(CDSPdB));

            if(dbContext.User.FirstOrDefault(r=> r.EmailAddress == user.EmailAddress) == null)
            {
                return ValidationResult.Success;
            }
            return new ValidationResult("Sorry, Email address is already in use. Please login or try again.");
        }
    }
}
```
#### Using value
```c#
public class EnsureUqniqueUsername : ValidationAttribute
{
	protected override ValidationResult IsValid(object value, ValidationContext validationContext)
	{
		DataContext dbContext = (DataContext)validationContext.GetService(typeof(DataContext));

		if (dbContext.User.FirstOrDefault(r => r.Username == value.ToString()) == null)
		{
			return ValidationResult.Success;
		}
		return new ValidationResult("Sorry, Email address is already in use. Please login or try again.");
	}
}
```

## Filters
![[Screenshot 2022-03-19 165451.png]]![[Screenshot 2022-03-19 165528.png]]

## Database connection
[[MVC#Database]]
## JWT
```c#
/*
	> Packages to install
		- Microsoft.AspNetCore.Authentication.JwtBearer v 3.1.20
		- Microsoft.IdentityModel.Tokens 
		- System.IdentityModel.Tokens.Jwt
*
```

### Appsettings.json
```json
{
  ...
  "Jwt": {
    "Key": "9kYUNluWP616FpMGr6j9yl",
    "Issuer": "https://localhost:44324/",//host address
    "Audience": "https://localhost:44324/" //consumer address
  }
}
```
### Startup.cs
```c#
public void ConfigureServices(IServiceCollection services)
{
	services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)// configuring jwt & passing in properties set on settings file
		.AddJwtBearer(options => {
			options.TokenValidationParameters = new TokenValidationParameters
			{
				ValidateIssuer = true,
				ValidateAudience = true,
				ValidateLifetime = true,
				ValidateIssuerSigningKey = true,
				ValidIssuer = Configuration["Jwt:Issuer"],
				ValidAudience = Configuration["Jwt:Audience"],
				IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(Configuration["Jwt:Key"]))

			};
		});

	services.AddControllers();
}
```
### AuthenticateController.cs
```c#
namespace CommunityDrivenSocialPlatform_APi.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class AuthenticateController : ControllerBase
    {
        private readonly IConfiguration Configuration;
        private readonly CDSPdB dbContext;


        public AuthenticateController(IConfiguration configuration, CDSPdB dbContext)//get depedecients
        {
            this.Configuration = configuration;
            this.dbContext = dbContext;
        }

        [AllowAnonymous]//allows access to any user
        [HttpPost]
        public IActionResult Login([FromBody]UserLogin userLogin)//logs user in & generate token
        {
            //Authenticate user
            User user = Authenticate(userLogin);

            //generate token
            if(user != null)
            {
                var token = GenerateToken(user);
                return Ok(token);
            }
            return NotFound("Sorry, Username or Password was incorrect. Please try again.");
        }


        private string GenerateToken (User user)
        {
            SymmetricSecurityKey securityKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(Configuration["Jwt:Key"]));
            SigningCredentials credintials = new SigningCredentials(securityKey, SecurityAlgorithms.HmacSha256);

            Role role = dbContext.Role.FirstOrDefault(r => user.RoleId == r.Id);

            var claims = new[]
            {
                new Claim(ClaimTypes.NameIdentifier, user.Username),
                new Claim(ClaimTypes.Role, role.RoleName),
            };

            JwtSecurityToken token = new JwtSecurityToken(
                Configuration["Jwt:Issuer"], 
                Configuration["Jwt:Audience"], 
                claims, expires: DateTime.Now.AddMinutes(15), 
                signingCredentials: credintials
            );

            return new JwtSecurityTokenHandler().WriteToken(token);
        }

        private User Authenticate(UserLogin userLogin)
        {
            if (userLogin != null)
            {
                User  user = dbContext.User.FirstOrDefault(user => user.Username == userLogin.Username && user.Password == userLogin.Password);
                if (user != null)
                {
                    Debug.WriteLine($"User found {user.Id}, {user.Username}");
                    return user;
                }
            }
            return null;

        }
    }
}
```

### Login in
```c#
/*
	Use Content-Type application/json
*
```
![[Screenshot 2022-03-20 165251.png]]
### Authorized Routes
![[Screenshot 2022-03-20 165104.png]]

## EF Core - CRUD 
[[MVC#Enity Framework CRUD]]

## Jason String to object
```c#
public static class SerializedJson
{
	public static object SerializedJsonList(IDictionary<string, object> dictionary)
	{
		JavaScriptSerializer serializer = new JavaScriptSerializer();
		string jsonStr = "{";

		foreach (KeyValuePair<string, object> kvp in dictionary)
		{
			jsonStr += $"\"{kvp.Key}\":\"{kvp.Value}\",";
		}

		jsonStr = jsonStr.Substring(0, jsonStr.Length - 1);
		jsonStr += "}";

		return serializer.Deserialize<object>(jsonStr);
	}
}

//using 
IDictionary<string, object> dictionary = new Dictionary<string, object>();
dictionary.Add("Username", user.Username);
dictionary.Add("ProfilePictureUrl", user.ProfilePictureUrl);
```

### Get logged user
```c#
string loggedUser = User.Claims.FirstOrDefault(c => c.Type == ClaimTypes.NameIdentifier)?.Value;
```

## Intergration testing
### Packages
```c#
/*
	- MVC core testing
	- AspNetCore.app
*
```

## Refactoring
### Service configurations
```c#
public interface IServiceConfig
{
	public void Configure(IServiceCollection services, IConfiguration configuration);
}
```

```c#
public class DbService : IServiceConfig
{
	public void Configure(IServiceCollection services, IConfiguration configuration)
	{
		services.AddDbContext<CDSPdB>(options =>
				options.UseSqlServer(configuration.GetConnectionString("CDSPdB")));
	}
}
```

```c#
public static class ServiceConfigExtension
{
	public static void ConfigureAll(IServiceCollection services, IConfiguration configuration)
	{
		var serviceConfigs = typeof(Startup).Assembly.ExportedTypes.Where(t =>
			typeof(IServiceConfig).IsAssignableFrom(t) && !t.IsInterface && !t.IsAbstract)
			.Select(Activator.CreateInstance).Cast<IServiceConfig>().ToList();

		serviceConfigs.ForEach(service => service.Configure(services, configuration));
	}
}
```

```c#
//everything is just one line now ins startup.configuration method
public void ConfigureServices(IServiceCollection services)
{
	ServiceConfigExtension.ConfigureAll(services, Configuration);
}
```
