# Wdrażanie rozwiązań Azure Functions

- Azure Functions to serverless compute.
- Kod uruchamiany na żądanie (event-driven).
- Obsługa wielu języków, m.in. C#.
- Skalowanie automatyczne.
- Płatność za wykonanie.

## Przykład C# (.NET 8)

```csharp
public class MyFunction
{
    private readonly ILogger<MyFunction> _logger;
    public MyFunction(ILogger<MyFunction> logger)
    {
        _logger = logger;
    }

    [Function("HttpExample")]
    public async Task<HttpResponseData> Run(
        [HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req)
    {
        _logger.LogInformation("Request received");
        var response = req.CreateResponse(HttpStatusCode.OK);
        await response.WriteStringAsync("Hello from Azure Function!");
        return response;
    }
}
```

- Wstrzykiwanie zależności przez konstruktor.
- Obsługa HTTP trigger.
- Logowanie przez ILogger.

---

[Prev: Blob Storage](blob-storage.md) | [Next: CDN](cdn.md)
