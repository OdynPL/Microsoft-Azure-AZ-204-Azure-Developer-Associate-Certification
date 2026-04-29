# Sposoby deployowania aplikacji na Azure

**Definicja:**
- **Deployment** to proces wdrażania aplikacji lub zasobów do środowiska Azure.
- Obejmuje automatyzację, zarządzanie konfiguracją, wersjonowanie i rollback.

**Znaczenie na egzaminie AZ-204:**
- Wymagana znajomość różnych metod wdrażania: ręcznych, automatycznych, CI/CD, ARM/Bicep, CLI, portalu.
- Często pytania o wybór narzędzia, automatyzację, rollback, deployment sloty.

## Kluczowe pojęcia i komponenty

- **Azure Portal** – ręczne wdrażanie, szybkie testy, niezalecane do produkcji.
- **Azure CLI** – skrypty automatyzujące deployment, np. `az webapp deploy`.
- **Azure PowerShell** – automatyzacja wdrożeń, szczególnie dla Windows.
- **ARM Template** – deklaratywne szablony JSON, infrastruktura jako kod.
- **Bicep** – nowoczesny język IaC, prostszy od ARM, kompiluje się do ARM.
- **GitHub Actions** – CI/CD, automatyczne buildy i deploymenty.
- **Azure DevOps Pipelines** – zaawansowane CI/CD, integracja z repozytoriami.
- **Deployment Slot** – środowiska testowe (np. staging) dla App Service.
- **Zip Deploy** – szybkie wdrożenie paczki ZIP do App Service.
- **Container Registry** – wdrażanie kontenerów z ACR do AKS, App Service, Functions.

## Scenariusze egzaminacyjne

- Wdrożenie Web App przez portal, CLI, ARM/Bicep.
- Automatyzacja deploymentu przez GitHub Actions lub Azure DevOps.
- Rollback do poprzedniej wersji (np. swap slotów, redeploy).
- Wdrożenie kontenera do App Service lub AKS.
- Parametryzacja szablonów ARM/Bicep.
- Weryfikacja deploymentu (np. test endpointu, sprawdzenie statusu).

## Przykłady użycia

### Deployment przez Azure CLI
```powershell
az webapp up --name mywebapp --resource-group myRG --runtime "DOTNET:8"
```

### Deployment przez GitHub Actions (fragment workflow)
```yaml
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: azure/login@v2
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}
      - uses: azure/webapps-deploy@v3
        with:
          app-name: mywebapp
          package: ./publish
```

### Deployment przez ARM Template
```powershell
az deployment group create \
  --resource-group myRG \
  --template-file azuredeploy.json \
  --parameters @azuredeploy.parameters.json
```

### Deployment przez Bicep
```powershell
az deployment group create \
  --resource-group myRG \
  --template-file main.bicep
```

### Deployment slot swap (App Service)
```powershell
az webapp deployment slot swap \
  --resource-group myRG \
  --name mywebapp \
  --slot staging
```

### Zip Deploy (App Service)
```powershell
az webapp deployment source config-zip \
  --resource-group myRG \
  --name mywebapp \
  --src myapp.zip
```

### Przykład C# (.NET 8) – wywołanie deploymentu ARM przez SDK
```csharp
using Azure.Identity;
using Azure.ResourceManager;
using Azure.ResourceManager.Resources;

var credential = new DefaultAzureCredential();
var armClient = new ArmClient(credential);
var resourceGroup = await armClient.GetDefaultSubscription().GetResourceGroups().GetAsync("myRG");
var deployment = await resourceGroup.Value.GetDeployments().CreateOrUpdateAsync(
    WaitUntil.Completed,
    "myDeployment",
    new Deployment {
        Properties = new DeploymentProperties(DeploymentMode.Incremental) {
            TemplateLink = new TemplateLink("https://myurl/azuredeploy.json"),
            Parameters = BinaryData.FromObjectAsJson(new { param1 = "value" })
        }
    });
```

## Dobre praktyki

- Używaj IaC (Bicep/ARM) do powtarzalnych wdrożeń.
- Automatyzuj deployment przez CI/CD (GitHub Actions, Azure DevOps).
- Testuj deployment na slotach lub środowiskach testowych.
- Używaj parametrów i sekretnych wartości z Key Vault.
- Monitoruj status deploymentu i logi.
- Stosuj rollback (swap slotów, redeploy) przy błędach.
- Nie wdrażaj ręcznie do produkcji.
- Dokumentuj proces deploymentu.

## Wskazówki i pułapki egzaminacyjne

- ARM/Bicep nie wdraża kodu aplikacji, tylko infrastrukturę.
- Zip Deploy nadpisuje całą aplikację – nie używaj do częściowych aktualizacji.
- Deployment sloty pozwalają na bezpieczny swap bez downtime.
- GitHub Actions wymaga skonfigurowania sekretów (np. AZURE_CREDENTIALS).
- Błędy deploymentu często wynikają z brakujących uprawnień lub złych parametrów.
- W Azure DevOps preferuj YAML pipelines zamiast klasycznych buildów.
