# Azure with Docker
---

[Prev: Azure PowerShell](powershell.md)

**Definicja:**
- **Docker w Azure** – uruchamianie i zarządzanie kontenerami Docker na platformie Azure (App Service, Container Instances, AKS, Container Apps).

**Znaczenie na egzaminie AZ-204:**
- Pytania o deployment kontenerów, integrację z rejestrami, skalowanie, bezpieczeństwo.

## Kluczowe pojęcia
- **Azure Container Registry (ACR)** – prywatny rejestr obrazów Docker.
- **Azure Container Instances (ACI)** – szybkie uruchamianie pojedynczych kontenerów.
- **Azure App Service for Containers** – hostowanie aplikacji webowych jako kontener.
- **Azure Kubernetes Service (AKS)** – orkiestracja kontenerów na dużą skalę.
- **Azure Container Apps** – serverless dla kontenerów.

## Scenariusze egzaminacyjne
- Deployment obrazu z ACR do ACI, App Service lub AKS.
- Uwierzytelnianie do ACR z poziomu usługi.
- Skalowanie kontenerów.

## Przykład użycia
- Push obrazu do ACR:
  `az acr build --registry myacr --image myapp:v1 .`
- Deployment do ACI:
  `az container create --resource-group myRG --name myapp --image myacr.azurecr.io/myapp:v1 --registry-login-server myacr.azurecr.io --registry-username <user> --registry-password <pass>`

## Przykład kodu C# (.NET 8)
```csharp
// Brak bezpośredniego SDK do zarządzania Dockerem, użycie Azure SDK do zarządzania ACI/AKS/ACR.
```

## Wskazówka egzaminacyjna
- Najczęstszy błąd: brak uprawnień do ACR lub zła konfiguracja image pull.
- Kontenery mogą być uruchamiane w różnych usługach – wybierz odpowiednią do scenariusza.
