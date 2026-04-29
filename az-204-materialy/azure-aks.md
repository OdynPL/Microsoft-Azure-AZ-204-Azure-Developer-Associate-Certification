#
[Prev: Azure Containers](azure-containers.md) | [Next: Artifactory (Azure)](artifactory.md)
# Azure Kubernetes Service (AKS)

- Zarządzany klaster Kubernetes w Azure.
- Automatyzuje deployment, skalowanie i zarządzanie kontenerami.

## Znaczenie na AZ-204
- Umożliwia uruchamianie aplikacji w wielu kontenerach.
- Wsparcie dla DevOps, CI/CD, autoskalowania.
- Integracja z ACR, Azure Monitor, Key Vault.

## Kluczowe pojęcia
- **Pod**: najmniejsza jednostka uruchomieniowa w Kubernetes.
- **Node**: VM w klastrze AKS.
- **Cluster**: zbiór node'ów zarządzanych przez Azure.
- **Deployment**: deklaracja stanu aplikacji (YAML).
- **Service**: ekspozycja aplikacji (np. LoadBalancer, ClusterIP).
- **Namespace**: logiczna separacja zasobów.
- **Ingress**: routing ruchu HTTP/HTTPS.
- **kubectl**: narzędzie CLI do zarządzania klastrem.
- **Helm**: menedżer pakietów dla Kubernetes.

## Scenariusze egzaminacyjne
- Tworzenie klastra AKS.
- Wdrażanie aplikacji przez kubectl apply.
- Integracja z ACR (pull image).
- Skalowanie podów i node'ów.
- Monitorowanie i logowanie (Azure Monitor).

## Przykład użycia
- Tworzenie klastra:
  `az aks create --resource-group rg --name myaks --node-count 2 --generate-ssh-keys`
- Połączenie z klastrem:
  `az aks get-credentials --resource-group rg --name myaks`
- Wdrażanie aplikacji:
  `kubectl apply -f deployment.yaml`

## Komendy
- Tworzenie AKS:
  `az aks create --resource-group rg --name myaks --node-count 2 --generate-ssh-keys`
- Pobranie kubeconfig:
  `az aks get-credentials --resource-group rg --name myaks`
- Skalowanie node'ów:
  `az aks scale --resource-group rg --name myaks --node-count 3`

## Wskazówka egzaminacyjna
- AKS wymaga ACR lub publicznego rejestru do pobierania obrazów.
- Najczęstszy błąd: brak uprawnień do ACR lub zła konfiguracja deploymentu.
- Monitorowanie przez Azure Monitor for Containers.
