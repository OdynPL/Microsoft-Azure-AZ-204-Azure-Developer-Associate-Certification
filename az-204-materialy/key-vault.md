# Azure Key Vault

- Bezpieczne przechowywanie sekretów, kluczy, certyfikatów.
- Dostęp przez SDK, REST API, Azure CLI.
- Integracja z aplikacjami .NET przez Managed Identity.

## Przykład C# (.NET 8, pobranie sekretu)

```csharp
public async Task<string> GetSecretAsync(string vaultUrl, string secretName, TokenCredential credential)
{
    var client = new SecretClient(new Uri(vaultUrl), credential);
    KeyVaultSecret secret = await client.GetSecretAsync(secretName);
    return secret.Value;
}
```

- Użycie Azure.Security.KeyVault.Secrets.
- Wsparcie dla Azure.Identity.
- Async/await.

---

[Prev: Front Door](front-door.md) | [Next: Logic Apps](logic-apps.md)
