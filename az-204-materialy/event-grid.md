
# Azure Event Grid

- Usługa do obsługi zdarzeń (**eventing**) w Azure.
- Umożliwia routing zdarzeń między usługami, aplikacjami i zasobami.
- Wspiera subskrypcje, filtrowanie, wysoką dostępność i niskie opóźnienia.

## Znaczenie na AZ-204
- Pozwala na budowę architektur event-driven.
- Integruje się z wieloma usługami (Storage, Functions, Service Bus, Logic Apps).
- Umożliwia automatyczne reakcje na zdarzenia w chmurze.

## Kluczowe pojęcia
- **Event**: pojedyncze zdarzenie (np. utworzenie pliku, zmiana stanu).
- **Event Source**: źródło zdarzeń (np. Storage, własny topic).
- **Event Grid Topic**: punkt publikacji zdarzeń (systemowy lub custom).
- **Event Subscription**: subskrypcja na zdarzenia, określa endpoint odbiorcy.
- **Event Handler**: odbiorca zdarzenia (np. Function, Webhook).
- **Filtering**: filtrowanie zdarzeń po typie, danych, źródle.
- **Dead-lettering**: obsługa nieprzetworzonych zdarzeń.
- **Retry Policy**: automatyczne ponawianie dostarczenia.
- **System Topics**: wbudowane źródła zdarzeń Azure.
- **Custom Topics**: własne źródła zdarzeń.

## Scenariusze egzaminacyjne
- Publikacja zdarzenia do custom topic.
- Subskrypcja na zdarzenia Storage/Resource Group.
- Filtrowanie zdarzeń po typie lub danych.
- Integracja z Azure Functions jako handler.
- Obsługa dead-lettering i retry policy.

## Przykład użycia
- Publikacja zdarzenia do custom topic.
- Subskrypcja na zdarzenia Storage (np. utworzenie blob).
- Filtrowanie zdarzeń po typie (np. Microsoft.Storage.BlobCreated).

## Komendy
- Tworzenie custom topic:
    `az eventgrid topic create --resource-group rg --name mytopic --location westeurope`
- Tworzenie subskrypcji:
    `az eventgrid event-subscription create --source-resource-id <topicId> --name mysub --endpoint <endpointUrl>`
- Lista system topics:
    `az eventgrid system-topic list --resource-group rg`

## Przykład C# (.NET 8, wysyłanie zdarzenia)

## Przykład C# (.NET 8, wysyłanie zdarzenia)


```csharp
using Azure;
using Azure.Messaging.EventGrid;

public async Task SendEventAsync(string topicEndpoint, string key, EventGridEvent eventGridEvent)
{
    var credentials = new AzureKeyCredential(key);
    var client = new EventGridPublisherClient(new Uri(topicEndpoint), credentials);
    await client.SendEventAsync(eventGridEvent);
}
```

// Odbiór zdarzenia w Azure Function:
```csharp
[Function("EventGridHandler")]
public void Run([EventGridTrigger] EventGridEvent eventGridEvent)
{
    // obsługa zdarzenia
}
```


- Użycie Azure.Messaging.EventGrid.
- Async/await.
- Przekazanie obiektu EventGridEvent.
- Odbiór przez Azure Function lub Webhook.

## Wskazówka egzaminacyjna
- Event Grid nie przechowuje zdarzeń — tylko przekazuje.
- Najczęstszy błąd: brak uprawnień do topic lub zły endpoint subskrypcji.
- Filtrowanie pozwala ograniczyć liczbę wywołań handlera.

---

[Prev: Deployment (Bicep)](deployment-bicep.md) | [Next: Event Hub](event-hub.md)
