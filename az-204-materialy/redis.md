

# Azure Cache for Redis
---

[Prev: Monitor](monitor.md) | [Next: Service Bus](service-bus.md)

- Szybka, w pełni zarządzana pamięć podręczna w chmurze (Redis as a Service).
- Wspiera operacje klucz-wartość, pub/sub, listy, sety, hash.
- Integracja z .NET przez StackExchange.Redis, obsługa wielu języków.

## Znaczenie na AZ-204
- Przyspiesza dostęp do danych, zmniejsza obciążenie baz danych.
- Umożliwia implementację cache, sesji, kolejek, blokad rozproszonych.
- Wspiera wysoką dostępność, replikację, skalowanie.

## Kluczowe pojęcia
- **Instance**: pojedyncza instancja Redis (Basic, Standard, Premium, Enterprise).
- **Key-Value Store**: przechowywanie danych jako pary klucz-wartość.
- **TTL (Time To Live)**: czas życia klucza w cache.
- **Persistence**: trwałość danych (Premium, Enterprise).
- **Geo-replication**: replikacja między regionami (Premium, Enterprise).
- **Redis Cluster**: partycjonowanie danych, skalowanie poziome.
- **Firewall, VNet**: ochrona dostępu do cache.
- **SSL**: szyfrowanie połączenia.
- **Connection Multiplexer**: zarządzanie połączeniem w StackExchange.Redis.

## Scenariusze egzaminacyjne
- Implementacja cache w aplikacji .NET.
- Przechowywanie sesji użytkownika w Redis.
- Ustawienie TTL dla kluczy.
- Konfiguracja replikacji i wysokiej dostępności.
- Ograniczenie dostępu do cache przez VNet/firewall.

## Przykład użycia
- Pobranie i zapis wartości przez StackExchange.Redis.
- Ustawienie TTL dla klucza.
- Przechowywanie sesji ASP.NET w Redis.

## Komendy
- Tworzenie instancji Redis:
    `az redis create --name myredis --resource-group rg --location westeurope --sku Basic --vm-size c0`
- Pobranie klucza dostępu:
    `az redis list-keys --name myredis --resource-group rg`

## Przykład C# (.NET 8, pobranie i zapis wartości)
```csharp
using StackExchange.Redis;

public async Task<string> GetValueAsync(string connectionString, string key)
{
        var redis = await ConnectionMultiplexer.ConnectAsync(connectionString);
        var db = redis.GetDatabase();
        return await db.StringGetAsync(key);
}

public async Task SetValueAsync(string connectionString, string key, string value, TimeSpan? ttl = null)
{
        var redis = await ConnectionMultiplexer.ConnectAsync(connectionString);
        var db = redis.GetDatabase();
        await db.StringSetAsync(key, value, ttl);
}
```

## Wskazówka egzaminacyjna
- Redis Premium/Enterprise obsługuje geo-replikację i persistence.
- Najczęstszy błąd: brak TTL powoduje przepełnienie cache.
- Połączenie powinno być współdzielone (ConnectionMultiplexer jako singleton).

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

