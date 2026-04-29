# Azure Durable Functions
---

[Prev: Azure Container Apps](container-apps.md) | [Next: Azure Policy](policy.md)

**Definicja:**
- Rozszerzenie Azure Functions do budowy workflow, orchestratorów, sag.

**Znaczenie na egzaminie AZ-204:**
- Często pytania o wzorce orchestrator, activity, suborchestration.

## Kluczowe pojęcia
- **Orchestrator Function** – steruje przepływem, wywołuje activity.
- **Activity Function** – pojedyncza operacja w workflow.
- **Durable Entity** – trwały obiekt z własnym stanem.
- **Suborchestration** – wywołanie innego orchestratora.
- **Fan-out/fan-in** – równoległe zadania.

## Scenariusze egzaminacyjne
- Budowa workflow z retry, timeout, compensation.
- Różnice względem klasycznych Functions.
- Monitorowanie stanu instancji.

## Przykład użycia
- Tworzenie orchestratora i activity w .NET 8.
- Monitorowanie instancji przez portal.

## Komendy
- Instalacja rozszerzenia:
  `func extensions install --package Microsoft.Azure.WebJobs.Extensions.DurableTask --version 2.x`

## Przykład kodu C# (.NET 8)
```csharp
[Function("Orchestrator")]
public async Task RunOrchestrator([OrchestrationTrigger] IDurableOrchestrationContext context)
{
    var outputs = new List<string>();
    outputs.Add(await context.CallActivityAsync<string>("SayHello", "Tokyo"));
    outputs.Add(await context.CallActivityAsync<string>("SayHello", "Seattle"));
    outputs.Add(await context.CallActivityAsync<string>("SayHello", "London"));
    return outputs;
}

[Function("SayHello")]
public string SayHello([ActivityTrigger] string name) => $"Hello {name}!";
```

## Wskazówka egzaminacyjna
- Durable Functions = workflow, retry, compensation, fan-out/fan-in.
- Najczęstszy błąd: brak await lub złe powiązanie triggerów.
