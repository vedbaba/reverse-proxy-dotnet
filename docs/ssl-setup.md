Serving pages via HTTPS, SSL setup
==================================

The service is designed to be deployed as an 
[Azure Web App](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-tutorial-custom-SSL),
reusing the SSL encryption provided by the platform, to expose, for example,
private services hosted in Azure VMs, Cloud Apps, etc.

However, you can easily extend the code to use a custom certificate, editing
[Program.cs](https://github.com/Azure/reverse-proxy-dotnet/blob/master/ProxyAgent/Program.cs)
and using something like:

```c#
var host = new WebHostBuilder()
    .UseKestrel(options =>
    {
        options.UseHttps("my-cert.pfx", "my-cert-password");
    })
    .UseUrls("https://*:" + config.Port)
    .UseContentRoot(Directory.GetCurrentDirectory())
    .UseIISIntegration()
    .UseStartup<Startup>()
    .Build();
```

See the
[Kestrel documentation](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel)
for more information about this setup and other options.

Site content
============

* [Project overview](index.md)
* [How to add static files](add-static-files.md)
* [SSL setup](ssl-setup.md)
* [Contributing to the project](https://github.com/Azure/reverse-proxy-dotnet/blob/master/CONTRIBUTING.md)