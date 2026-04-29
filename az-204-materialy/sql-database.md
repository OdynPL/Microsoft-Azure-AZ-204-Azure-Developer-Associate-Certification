
# Azure SQL Database

- Relacyjna baza danych w chmurze (PaaS, DBaaS).
- Wysoka dostępność (HA), automatyczne backupy, geo-replikacja, skalowanie.
- Integracja z aplikacjami .NET przez ADO.NET, EF Core, Dapper.

## Znaczenie na AZ-204
- Pozwala na szybkie wdrożenie i zarządzanie relacyjną bazą bez VM.
- Wspiera bezpieczeństwo, automatyzację, skalowanie, disaster recovery.
- Umożliwia integrację z Azure AD, Managed Identity, Key Vault.

## Kluczowe pojęcia
- **Single Database**: pojedyncza baza, niezależne zasoby.
- **Elastic Pool**: współdzielone zasoby dla wielu baz.
- **DTU/vCore**: modele wydajności (DTU - uproszczony, vCore - elastyczny).
- **Geo-replication**: replikacja do innego regionu.
- **Active Directory Authentication**: logowanie przez Azure AD.
- **Firewall Rules**: kontrola dostępu do bazy.
- **Transparent Data Encryption (TDE)**: szyfrowanie danych w spoczynku.
- **Automatic Tuning**: automatyczna optymalizacja zapytań.
- **Auditing**: rejestrowanie operacji na bazie.
- **Failover Group**: automatyczne przełączanie na zapasową bazę.

## Scenariusze egzaminacyjne
- Połączenie z bazą przez ADO.NET, EF Core, Managed Identity.
- Konfiguracja firewall, TDE, auditing.
- Ustawienie geo-replikacji i failover group.
- Uwierzytelnianie przez Azure AD.
- Automatyczne backupy i odtwarzanie bazy.

## Przykład użycia
- Połączenie przez connection string (SQL Auth lub Azure AD).
- Odczyt/zapis danych przez ADO.NET, EF Core.
- Uwierzytelnianie przez Managed Identity.

## Komendy
- Tworzenie bazy:
    `az sql server create --name myserver --resource-group rg --location westeurope --admin-user admin --admin-password pass`
    `az sql db create --resource-group rg --server myserver --name mydb --service-objective S0`
- Dodanie reguły firewall:
    `az sql server firewall-rule create --resource-group rg --server myserver --name AllowAll --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255`
- Dodanie użytkownika AD:
    `CREATE USER [user@contoso.com] FROM EXTERNAL PROVIDER;`
- Włączenie TDE:
    `az sql db tde set --resource-group rg --server myserver --database mydb --status Enabled`

## Przykład C# (.NET 8, zapytanie SQL i Managed Identity)
```csharp
using Microsoft.Data.SqlClient;

// SQL Auth
public async Task<int> GetCountAsync(string connectionString)
{
        await using var conn = new SqlConnection(connectionString);
        await conn.OpenAsync();
        await using var cmd = conn.CreateCommand();
        cmd.CommandText = "SELECT COUNT(*) FROM Users";
        return (int)await cmd.ExecuteScalarAsync();
}

// Managed Identity
public async Task<int> GetCountWithMIAsync(string server, string db)
{
        var connStr = $"Server=tcp:{server}.database.windows.net,1433;Database={db};Authentication=Active Directory Managed Identity;";
        await using var conn = new SqlConnection(connStr);
        await conn.OpenAsync();
        await using var cmd = conn.CreateCommand();
        cmd.CommandText = "SELECT COUNT(*) FROM Users";
        return (int)await cmd.ExecuteScalarAsync();
}
```

## Wskazówka egzaminacyjna
- Managed Identity wymaga nadania uprawnień w bazie (CREATE USER ... FROM EXTERNAL PROVIDER).
- Najczęstszy błąd: brak reguły firewall lub złe dane logowania.
- TDE i auditing są domyślnie włączone, ale można je skonfigurować.

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
