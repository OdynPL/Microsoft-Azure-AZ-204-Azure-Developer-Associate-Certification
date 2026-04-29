


# Azure Key Vault
---

[Prev: Front Door](front-door.md) | [Next: Logic Apps](logic-apps.md)

## Definicja
- Bezpieczne przechowywanie sekretów, kluczy, certyfikatów.
- Dostęp przez SDK, REST API, Azure CLI, PowerShell.
- Centralne miejsce do zarządzania tajnymi danymi i kluczami kryptograficznymi.

## Znaczenie na AZ-204
- Ochrona tajnych danych aplikacji (connection string, API key, certyfikaty).
- Integracja z Managed Identity, App Service, Functions, Azure DevOps.
- Automatyczna rotacja sekretów i certyfikatów.

## Kluczowe pojęcia
- **Secret**: dowolny tekstowy sekret (np. connection string, API key).
- **Key**: klucz szyfrujący, obsługa operacji kryptograficznych (RSA, EC).
- **Certificate**: certyfikat SSL, obsługa cyklu życia, automatyczna odnowa.
- **Access Policy**: uprawnienia do odczytu/zapisu dla użytkowników i aplikacji.
- **RBAC**: kontrola dostępu oparta o role (rola Key Vault Reader, Contributor).
- **Managed Identity**: bezpieczny dostęp bez haseł, automatyczna integracja z Azure.
- **Soft Delete**: odzyskiwanie usuniętych sekretów/kluczy.
- **Purge Protection**: ochrona przed trwałym usunięciem.
- **Audit Logging**: rejestrowanie operacji na zasobach.
- **Key Rotation**: automatyczna rotacja kluczy/certyfikatów.

## Scenariusze egzaminacyjne
- Pobieranie sekretu w kodzie .NET przez DefaultAzureCredential lub Managed Identity.
- Ustawianie uprawnień (Access Policy, RBAC) dla aplikacji.
- Automatyczna rotacja sekretów/certyfikatów.
- Integracja z App Service, Functions, Azure DevOps.
- Odczyt certyfikatu do TLS/SSL.

## Przykład użycia
- Odczyt sekretu przez SDK (DefaultAzureCredential, SecretClient).
- Użycie Key Vault w Functions przez Managed Identity.
- Automatyczna rotacja certyfikatu dla App Service.

## Komendy
- Tworzenie Key Vault:
        `az keyvault create --name myvault --resource-group rg --location westeurope`
- Dodanie sekretu:
        `az keyvault secret set --vault-name myvault --name MySecret --value "tajnehaslo"`
- Nadanie uprawnień aplikacji:
        `az keyvault set-policy --name myvault --object-id <appId> --secret-permissions get list`
- Dodanie certyfikatu:
        `az keyvault certificate create --vault-name myvault --name mycert --policy "@policy.json"`

## Przykład kodu C# (.NET 8)
```csharp
using Azure.Identity;
using Azure.Security.KeyVault.Secrets;

public async Task<string> GetSecretAsync(string vaultUrl, string secretName)
{
        var credential = new DefaultAzureCredential();
        var client = new SecretClient(new Uri(vaultUrl), credential);
        try
        {
                KeyVaultSecret secret = await client.GetSecretAsync(secretName);
                return secret.Value;
        }
        catch (RequestFailedException ex)
        {
                // Obsługa błędów dostępu, brak uprawnień, itp.
                throw;
        }
}
```

## Zarządzanie sekretami i certyfikatami – przykłady C#

```csharp
// Dodawanie/aktualizacja sekretu
public async Task SetSecretAsync(string vaultUrl, string secretName, string value)
{
        var credential = new DefaultAzureCredential();
        var client = new SecretClient(new Uri(vaultUrl), credential);
        await client.SetSecretAsync(secretName, value);
}

// Usuwanie sekretu
public async Task DeleteSecretAsync(string vaultUrl, string secretName)
{
        var credential = new DefaultAzureCredential();
        var client = new SecretClient(new Uri(vaultUrl), credential);
        await client.StartDeleteSecretAsync(secretName);
}

// Odczyt certyfikatu jako Base64 (np. do TLS)
using Azure.Security.KeyVault.Certificates;
public async Task<string> GetCertificateAsync(string vaultUrl, string certName)
{
        var credential = new DefaultAzureCredential();
        var client = new CertificateClient(new Uri(vaultUrl), credential);
        KeyVaultCertificateWithPolicy cert = await client.GetCertificateAsync(certName);
        return Convert.ToBase64String(cert.Cer);
}

// Dodanie certyfikatu (np. z pliku PFX)
public async Task ImportCertificateAsync(string vaultUrl, string certName, string pfxPath, string pfxPassword)
{
        var credential = new DefaultAzureCredential();
        var client = new CertificateClient(new Uri(vaultUrl), credential);
        byte[] pfxBytes = File.ReadAllBytes(pfxPath);
        var importOptions = new ImportCertificateOptions(certName, pfxBytes)
        {
                Password = pfxPassword
        };
        await client.ImportCertificateAsync(importOptions);
}
```

## Wskazówka egzaminacyjna
- Managed Identity wymaga nadania uprawnień w Key Vault (Access Policy lub RBAC).
- Soft delete domyślnie włączony (odzyskiwanie sekretów).
- RBAC i Access Policy nie są tym samym (nie łączą się, wybierz jeden model).
- Najczęstszy błąd: brak uprawnień lub zła nazwa sekretu.


---

