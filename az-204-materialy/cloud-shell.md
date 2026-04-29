


# Azure Cloud Shell
---

[Prev: Web PubSub](webpubsub.md) | [Next: VNet](vnet.md)

## Definicja
- Wbudowany terminal w portalu Azure (Bash, PowerShell).
- Preinstalowane narzędzia: Azure CLI, PowerShell, Git, edytory, języki skryptowe.

## Znaczenie na AZ-204
- Umożliwia zarządzanie zasobami bez instalacji narzędzi lokalnie.
- Automatyzacja i testowanie poleceń w chmurze.
- Szybkie wdrażanie, testowanie, troubleshooting.

## Kluczowe pojęcia
- **Azure CLI**: narzędzie do zarządzania zasobami Azure przez komendy `az`.
- **PowerShell**: automatyzacja i skrypty, cmdlety `Az.*`.
- **Azure Files**: persistent storage dla Cloud Shell.
- **Preinstalowane narzędzia**: Git, edytory (code, vim, nano), języki skryptowe (Python, Node.js).

## Scenariusze egzaminacyjne
- Tworzenie i zarządzanie zasobami przez CLI (np. VM, Storage, App Service).
- Automatyzacja deploymentów (ARM/Bicep, skrypty).
- Praca z plikami w Azure Files.
- Szybkie testowanie komend i troubleshooting.

## Przykład użycia
- Tworzenie grupy zasobów:
	`az group create --name myrg --location westeurope`
- Wdrażanie Bicep:
	`az deployment group create --resource-group myrg --template-file main.bicep`
- Pobranie listy VM:
	`az vm list -o table`
- Ustawienie zmiennej środowiskowej:
	`export MYVAR=wartosc`

## Najważniejsze grupy komend AZ

| Grupa komend | Opis | Najważniejsze parametry |
|--------------|------|------------------------|
| az group     | Zarządzanie grupami zasobów | --name, --location |
| az vm        | Zarządzanie maszynami wirtualnymi | --name, --resource-group, --image, --size |
| az webapp    | Zarządzanie App Service | --name, --resource-group, --plan, --runtime |
| az storage   | Zarządzanie kontami i zasobami Storage | --account-name, --resource-group, --name, --container-name |
| az functionapp | Zarządzanie Azure Functions | --name, --resource-group, --plan, --storage-account |
| az keyvault  | Zarządzanie Key Vault | --name, --resource-group, --location |
| az sql       | Zarządzanie bazami SQL | --server, --name, --resource-group |
| az deployment | Wdrażanie szablonów ARM/Bicep | --resource-group, --template-file, --parameters |
| az monitor   | Monitorowanie zasobów | --resource-group, --name, --action-group |
| az identity  | Zarządzanie tożsamościami | --name, --resource-group |
| az acr       | Zarządzanie Azure Container Registry | --name, --resource-group |
| az aks       | Zarządzanie Azure Kubernetes Service | --name, --resource-group |
| az appconfig | Zarządzanie App Configuration | --name, --resource-group, --key, --value |
| az cosmosdb  | Zarządzanie Cosmos DB | --name, --resource-group, --database-name, --key |
| az eventgrid | Zarządzanie Event Grid | --name, --resource-group, --topic-name, --endpoint |
| az eventhubs | Zarządzanie Event Hub | --name, --resource-group, --namespace-name, --eventhub-name |
| az servicebus| Zarządzanie Service Bus | --name, --resource-group, --namespace-name, --queue-name |
| az policy    | Zarządzanie politykami | --name, --resource-group, --definition, --assignment |
| az blueprint | Zarządzanie Blueprints | --name, --resource-group |
| az logicapp  | Zarządzanie Logic Apps | --name, --resource-group |
| az marketplace | Przeglądanie Marketplace | --publisher, --offer |

## Przykładowe parametry

| Parametr | Opis |
|----------|------|
| --name | Nazwa zasobu |
| --resource-group | Grupa zasobów |
| --location | Lokalizacja (np. westeurope) |
| --plan | Plan App Service/Functions |
| --image | Obraz VM |
| --size | Rozmiar VM |
| --template-file | Plik szablonu ARM/Bicep |
| --parameters | Parametry wdrożenia |
| --account-name | Nazwa konta Storage |
| --container-name | Nazwa kontenera Storage |
| --runtime | Środowisko uruchomieniowe (np. DOTNET:8) |
| --storage-account | Konto Storage dla Functions |

## Przykład kodu C# (.NET 8)
```csharp
// Przykład: Wywołanie polecenia w Cloud Shell przez REST API (Automation)
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

public class CloudShellExample
{
	public async Task<string> RunCloudShellCommandAsync(string bearerToken, string command)
	{
		using var client = new HttpClient();
		client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
		var url = "https://management.azure.com/providers/Microsoft.Portal/consoles/default/executeCommand?api-version=2020-04-01-preview";
		var body = $"{{\"command\":\"{command}\"}}";
		var response = await client.PostAsync(url, new StringContent(body, System.Text.Encoding.UTF8, "application/json"));
		response.EnsureSuccessStatusCode();
		return await response.Content.ReadAsStringAsync();
	}
}
```

## Wskazówka egzaminacyjna
- Cloud Shell wymaga storage account (tworzy się automatycznie).
- Dane w Cloud Shell są trwałe dzięki Azure Files.
- Można korzystać z własnych skryptów i repozytoriów Git.
- Najczęstszy błąd: brak podania --resource-group lub literówka w nazwie parametru.


---

