
# Artifactory (Azure)
---

[Prev: Azure Kubernetes Service (AKS)](azure-aks.md) | [Next: Azure Service Fabric](service-fabric.md)

- Repozytorium artefaktów (np. NuGet, Maven, Docker) do przechowywania i dystrybucji pakietów.
- Najczęściej używane: **JFrog Artifactory** (może być hostowane w Azure VM, AKS, App Service).

## Znaczenie na AZ-204
- Umożliwia zarządzanie cyklem życia pakietów i kontenerów.
- Wspiera DevOps, CI/CD, automatyzację buildów i deploymentów.
- Integracja z Azure DevOps, GitHub Actions, AKS.

## Kluczowe pojęcia
- **Repository**: miejsce przechowywania artefaktów (local, remote, virtual).
- **Artifact**: plik binarny, pakiet, obraz kontenera.
- **Promotion**: przenoszenie artefaktów między środowiskami.
- **Retention Policy**: polityka przechowywania i czyszczenia starych artefaktów.
- **Access Token/API Key**: uwierzytelnianie do repozytorium.
- **Replication**: synchronizacja artefaktów między repozytoriami.

## Scenariusze egzaminacyjne
- Przechowywanie i pobieranie pakietów NuGet, Docker, npm.
- Integracja z pipeline CI/CD (np. Azure DevOps).
- Ustawienie retention policy i uprawnień.

## Przykład użycia
- Push obrazu Docker:
  `docker push myartifactory.azurecr.io/myimage:1.0`
- Pobranie pakietu NuGet:
  `nuget install MyPackage -Source "https://myartifactory/artifactory/api/nuget/v3/nuget-local"`

## Komendy
  `docker push/pull ...`
  `nuget install ...`
  (przez UI lub REST API Artifactory)

Push/pull Docker:
  `docker push/pull ...`
Pobranie pakietu:
  `nuget install ...`
Ustawienie retention policy:
  (przez UI lub REST API Artifactory)

Pobranie artefaktu przez PowerShell:
  `Invoke-RestMethod -Uri "https://myartifactory/artifactory/myrepo/myfile.zip" -Headers @{Authorization = "Bearer $token"} -OutFile myfile.zip`

## Przykład kodu C# (.NET 8)
```csharp
// Przykład 1: Pobranie artefaktu przez REST API
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

public class ArtifactoryDownload
{
    public async Task DownloadArtifactAsync(string url, string token, string outputPath)
    {
        using var client = new HttpClient();
        client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
        var response = await client.GetAsync(url);
        response.EnsureSuccessStatusCode();
        await using var fs = File.Create(outputPath);
        await response.Content.CopyToAsync(fs);
    }
}
```

```csharp
// Przykład 2: Upload artefaktu przez REST API
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

public class ArtifactoryUpload
{
    public async Task UploadArtifactAsync(string url, string token, string filePath)
    {
        using var client = new HttpClient();
        client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
        using var content = new StreamContent(File.OpenRead(filePath));
        var response = await client.PutAsync(url, content);
        response.EnsureSuccessStatusCode();
    }
}
```

## Wskazówka egzaminacyjna
- Artifactory nie jest natywną usługą Azure, ale często używane w projektach DevOps.
- Najczęstszy błąd: brak uprawnień lub zła konfiguracja endpointu.
- W Azure preferowane jest ACR do kontenerów, ale Artifactory obsługuje wiele typów artefaktów.
