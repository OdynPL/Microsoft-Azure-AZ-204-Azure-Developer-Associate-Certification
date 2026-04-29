#
[Prev: Azure Cloud Shell](cloud-shell.md) | [Next: Azure Kubernetes Service (AKS)](azure-aks.md)
# Azure Containers

- Uruchamianie aplikacji w kontenerach bez zarządzania infrastrukturą VM.
- Najważniejsze usługi: **Azure Container Instances (ACI)**, **Azure Container Registry (ACR)**.

## Znaczenie na AZ-204
- Szybkie uruchamianie pojedynczych kontenerów.
- Przechowywanie i zarządzanie obrazami kontenerów.
- Integracja z CI/CD, App Service, AKS.

## Kluczowe pojęcia
- **ACI**: uruchamianie kontenerów na żądanie, bez VM.
- **ACR**: prywatny rejestr obrazów Docker.
- **Container Group**: grupa współdzieląca sieć i storage.
- **Image**: obraz kontenera (np. Docker).
- **Registry**: repozytorium obrazów.
- **YAML**: definicja kontenera do wdrożenia.

## Scenariusze egzaminacyjne
- Wdrażanie kontenera przez ACI.
- Przechowywanie obrazu w ACR.
- Autoryzacja dostępu do ACR (np. Managed Identity).

## Przykład użycia
- Uruchomienie kontenera:
  `az container create --resource-group rg --name mycontainer --image mcr.microsoft.com/azuredocs/aci-helloworld --dns-name-label myaci --ports 80`
- Push obrazu do ACR:
  `az acr login --name myacr`
  `docker tag myapp myacr.azurecr.io/myapp:v1`
  `docker push myacr.azurecr.io/myapp:v1`

## Komendy
- Tworzenie ACR:
  `az acr create --resource-group rg --name myacr --sku Basic`
- Tworzenie ACI:
  `az container create --resource-group rg --name mycontainer --image myacr.azurecr.io/myapp:v1 --registry-login-server myacr.azurecr.io --registry-username <user> --registry-password <pass>`

## Wskazówka egzaminacyjna
- ACI nie obsługuje orkiestracji (tylko pojedyncze kontenery lub proste grupy).
- ACR może być zintegrowany z Managed Identity.
- Najczęstszy błąd: brak autoryzacji do ACR lub zła nazwa obrazu.
