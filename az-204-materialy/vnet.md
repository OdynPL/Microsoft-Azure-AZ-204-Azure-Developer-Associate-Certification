

# Azure Virtual Network (VNet)
---

[Prev: Cloud Shell](cloud-shell.md) | [Next: API Authorization](api-authorization.md)

**Definicja:**
- **Azure Virtual Network (VNet)** to logiczna izolacja sieci w chmurze Azure.
- Pozwala na segmentację, kontrolę ruchu i łączenie zasobów.

**Znaczenie na egzaminie AZ-204:**
- Wymagana znajomość konfiguracji, zabezpieczeń i integracji VNet z innymi usługami.
- Często pytania o NSG, połączenia hybrydowe, integrację z App Service, Functions, bazami danych.

## Kluczowe pojęcia i komponenty

- **VNet** – główna sieć wirtualna, izoluje zasoby.
- **Subnet** – podsieć, dzieli VNet na logiczne segmenty.
- **NSG (Network Security Group)** – filtruje ruch do/z podsieci lub VM.
- **Peering** – łączy różne VNet w tej samej lub innej subskrypcji.
- **VPN Gateway** – umożliwia połączenie on-premises z Azure przez VPN.
- **Service Endpoint** – bezpieczny dostęp do usług PaaS z VNet.
- **Private Endpoint** – prywatny adres IP dla usługi PaaS w VNet.
- **Route Table** – niestandardowe trasy ruchu w VNet.

## Scenariusze egzaminacyjne

- Tworzenie VNet i podsieci dla aplikacji webowych i baz danych.
- Konfiguracja NSG dla ograniczenia ruchu (np. tylko port 443).
- Połączenie App Service z VNet (VNet Integration, Private Endpoint).
- Dostęp do Azure SQL Database tylko z wybranej podsieci (Service Endpoint/Private Endpoint).
- Łączenie VNet z inną siecią (VNet Peering, VPN Gateway).

## Przykłady użycia

### Tworzenie VNet i podsieci – Azure CLI

```powershell
az network vnet create \
	--name myVNet \
	--resource-group myRG \
	--address-prefix 10.1.0.0/16 \
	--subnet-name mySubnet \
	--subnet-prefix 10.1.1.0/24
```

### Tworzenie NSG i przypisanie do podsieci – Azure CLI

```powershell
az network nsg create --resource-group myRG --name myNSG
az network vnet subnet update \
	--vnet-name myVNet \
	--name mySubnet \
	--resource-group myRG \
	--network-security-group myNSG
```

### Przykład Bicep – VNet z podsiecią i NSG

```bicep
resource vnet 'Microsoft.Network/virtualNetworks@2023-04-01' = {
	name: 'myVNet'
	location: resourceGroup().location
	properties: {
		addressSpace: {
			addressPrefixes: [ '10.1.0.0/16' ]
		}
		subnets: [
			{
				name: 'mySubnet'
				properties: {
					addressPrefix: '10.1.1.0/24'
					networkSecurityGroup: {
						id: nsg.id
					}
				}
			}
		]
	}
}

resource nsg 'Microsoft.Network/networkSecurityGroups@2023-04-01' = {
	name: 'myNSG'
	location: resourceGroup().location
}
```

### Przykład C# (.NET 8) – pobranie listy VNet przez SDK

```csharp
using Azure.Identity;
using Azure.ResourceManager;
using Azure.ResourceManager.Network;

var credential = new DefaultAzureCredential();
var armClient = new ArmClient(credential);
var subscription = await armClient.GetDefaultSubscriptionAsync();
await foreach (var vnet in subscription.GetVirtualNetworksAsync())
{
		Console.WriteLine($"VNet: {vnet.Data.Name}, Address: {string.Join(", ", vnet.Data.AddressSpace.AddressPrefixes)}");
}
```

## Komendy i konfiguracja

- Tworzenie VNet: `az network vnet create ...`
- Tworzenie NSG: `az network nsg create ...`
- Przypisanie NSG do podsieci: `az network vnet subnet update ...`
- Peering: `az network vnet peering create ...`
- Service Endpoint: `az network vnet subnet update --service-endpoints ...`
- Private Endpoint: `az network private-endpoint create ...`

## Wskazówki i pułapki egzaminacyjne

- NSG nie filtruje ruchu wychodzącego do usługi przez Private Endpoint (ruch jest prywatny).
- Service Endpoint nie ukrywa publicznego IP usługi PaaS – tylko ogranicza dostęp.
- Peering nie pozwala na automatyczne propagowanie tras niestandardowych (trzeba skonfigurować ręcznie).
- App Service VNet Integration nie pozwala na dostęp do zasobów on-premises bez Gateway.
- Private Endpoint wymaga DNS (np. Azure Private DNS Zone) do poprawnego działania.

---

