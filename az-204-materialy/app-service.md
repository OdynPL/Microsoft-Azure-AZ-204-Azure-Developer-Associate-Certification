# Azure App Service

- Usługa hostingu aplikacji webowych w Azure.
- Obsługuje .NET, Java, Node.js, Python.
- Automatyczne skalowanie i zarządzanie.
- Wsparcie dla CI/CD.

## Przykład C# (.NET 8, minimal API)

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Hello from App Service!");

app.Run();
```

- Prosta aplikacja webowa.
- Gotowa do wdrożenia na App Service.

---

[Prev: Application Insights](application-insights.md) | [Next: App Configuration](app-configuration.md)
