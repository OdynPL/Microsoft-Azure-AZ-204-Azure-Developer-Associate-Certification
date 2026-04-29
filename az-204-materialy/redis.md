# Azure Cache for Redis

- Szybka pamięć podręczna w chmurze.
- Wspiera operacje klucz-wartość.
- Integracja z .NET przez StackExchange.Redis.

## Przykład C# (.NET 8, pobranie wartości)

```csharp
public async Task<string> GetValueAsync(string connectionString, string key)
{
    var redis = await ConnectionMultiplexer.ConnectAsync(connectionString);
    var db = redis.GetDatabase();
    return await db.StringGetAsync(key);
}
```

- Użycie StackExchange.Redis.
- Async/await.
- Pobranie wartości przez klucz.

---

[Prev: Monitor](monitor.md) | [Next: Service Bus](service-bus.md)
