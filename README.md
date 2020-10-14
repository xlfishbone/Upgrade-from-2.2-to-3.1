# Upgrade to net core 3.1

## TargetFramework
- <TargetFramework>netcoreapp3.1</TargetFramework>

## Nuget
- remove
<PackageReference Include="Microsoft.AspNetCore.App"/>
 <PackageReference Include="Microsoft.AspNetCore.Razor.Design" Version="2.2.0" PrivateAssets="All" />
 
 - add
<PackageReference Include="Microsoft.AspNetCore.Mvc.NewtonsoftJson" Version="3.1.1" />
<PackageReference Include="Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation" Version="3.1.1" Condition="'$(Configuration)' == 'Debug'" />

* Note
Projects that target Microsoft.NET.Sdk or Microsoft.NET.Sdk.Razor SDK, should add an explicit FrameworkReference to Microsoft.AspNetCore.App:

 <!--b/c we just use Microsoft.NET.Sdk-->
<ItemGroup>
  <FrameworkReference Include="Microsoft.AspNetCore.App" />
</ItemGroup>


## Program.cs

public class Program
    {
        public static void Main(string[] args)
        {
            CreateHostBuilder(args).Build().Run();
        }

        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
				webBuilder.UseDCALogging();
                webBuilder.UseStartup<Startup>();
            });
    }
	

## Startup

### Configure 
- order 
app.UseStaticFiles();

app.UseRouting();
app.UseCors();

app.UseAuthentication();
app.UseAuthorization();

-- replaces useMVC or UserSignalR
app.UseEndpoints(endpoints => {
    endpoints.MapControllers();
});


### App Settings

- SsoApiOptions
- SsoClientOptions



## Angular
- publish dist to wwwroot
-- change angular.json to ../wwwroot/
