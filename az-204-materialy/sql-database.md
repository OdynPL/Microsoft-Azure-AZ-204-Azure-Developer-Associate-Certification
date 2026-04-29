# Azure SQL Database

- Relacyjna baza danych w chmurze.
- Wysoka dostępność, backup, skalowanie.
- Integracja z aplikacjami .NET przez ADO.NET, EF Core.

## Przykład C# (.NET 8, zapytanie SQL)

```csharp
public async Task<int> GetCountAsync(string connectionString)
{
    await using var conn = new SqlConnection(connectionString);
    await conn.OpenAsync();
    await using var cmd = conn.CreateCommand();
    cmd.CommandText = "SELECT COUNT(*) FROM Users";
    return (int)await cmd.ExecuteScalarAsync();
}
```

- Użycie Microsoft.Data.SqlClient.
- Async/await.
- Proste zapytanie SELECT.

---

[Prev: SignalR](signalr.md) | [Next: Storage Queue](storage-queue.md)
