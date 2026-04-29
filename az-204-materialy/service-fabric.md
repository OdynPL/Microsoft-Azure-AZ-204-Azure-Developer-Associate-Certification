
# Azure Service Fabric
---

[Prev: Artifactory (Azure)](artifactory.md) | [Next: Azure Functions](azure-functions.md)

- Platforma do budowy i zarządzania mikrousługami oraz aplikacjami rozproszonymi.
- Obsługuje kontenery, aplikacje .NET, Java, Linux, Windows.
- Umożliwia automatyczne skalowanie, aktualizacje bez przestoju, monitoring.

## Znaczenie na AZ-204
- Pozwala na wdrażanie złożonych systemów mikrousług.
- Wsparcie dla stateful/stateless services.
- Integracja z CI/CD, Azure DevOps, monitoringiem.

## Kluczowe pojęcia
- **Cluster**: zbiór maszyn (VM/VMSS) zarządzanych przez Service Fabric.
- **Node**: pojedyncza maszyna w klastrze.
- **Application**: logiczna grupa usług.
- **Service**: jednostka wdrożeniowa (stateful/stateless).
- **Partition**: podział usługi dla skalowalności.
- **Replica/Instance**: kopia usługi na node.
- **Reliable Collection**: trwałe kolekcje danych dla stateful services.
- **Upgrade Domain**: strefa aktualizacji bez przestoju.
- **Health Monitoring**: monitorowanie stanu klastra i usług.

## Scenariusze egzaminacyjne
- Tworzenie klastra Service Fabric.
- Wdrażanie aplikacji .NET jako mikrousług.
- Aktualizacja aplikacji bez przestoju.
- Monitoring i diagnostyka klastra.

## Przykład użycia
- Tworzenie klastra:
  `az sf cluster create --resource-group rg --location westeurope --cluster-name mycluster --vm-password <pass>`
- Wdrażanie aplikacji:
  `az sf application create --resource-group rg --cluster-name mycluster --application-name fabric:/myapp --application-type mytype --application-version 1.0`

## Komendy
- Tworzenie klastra:
  `az sf cluster create ...`
- Dodanie aplikacji:
  `az sf application create ...`
- Monitoring:
  `az sf cluster health --resource-group rg --cluster-name mycluster`

## Wskazówka egzaminacyjna
- Service Fabric obsługuje zarówno kontenery, jak i klasyczne aplikacje .NET.
- Najczęstszy błąd: brak quorum lub zła konfiguracja node/partition.
- Monitoring i diagnostyka są kluczowe dla stabilności klastra.
