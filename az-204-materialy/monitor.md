

# Azure Monitor
---

[Prev: Managed Identity](managed-identity.md) | [Next: Redis](redis.md)

- Monitorowanie zasobów i aplikacji w Azure (infrastruktura, PaaS, aplikacje).
- Zbieranie logów, metryk, alertów, śledzenie zmian, diagnostyka.
- Integracja z Application Insights, Log Analytics, Event Hub, Automation.

## Znaczenie na AZ-204
- Pozwala na szybkie wykrywanie i diagnozowanie problemów.
- Umożliwia automatyczne reakcje na zdarzenia (alerty, akcje).
- Wspiera DevOps, SRE, compliance.

## Kluczowe pojęcia
- **Metrics**: liczbowe dane o stanie zasobu (CPU, RAM, liczba żądań).
- **Logs**: szczegółowe dane o zdarzeniach, działaniach, błędach.
- **Log Analytics Workspace**: centralne miejsce przechowywania i analizy logów (KQL).
- **Alert**: powiadomienie o przekroczeniu progu lub zdarzeniu.
- **Action Group**: zestaw akcji wywoływanych przez alert (np. email, webhook).
- **Diagnostic Settings**: konfiguracja, które logi/metryki są zbierane i gdzie trafiają.
- **Workbooks**: interaktywne dashboardy do analizy danych.
- **Autoscale**: automatyczne skalowanie na podstawie metryk.
- **Activity Log**: log operacji na zasobach (kto, co, kiedy).
- **KQL (Kusto Query Language)**: język zapytań do analizy logów.

## Scenariusze egzaminacyjne
- Tworzenie alertów na metryki (np. CPU, liczba błędów).
- Analiza logów przez Log Analytics (KQL).
- Konfiguracja diagnostyki dla App Service, Functions, VM.
- Wysyłanie logów do Event Hub, Storage, SIEM.
- Ustawienie autoskalowania na podstawie metryk.

## Przykład użycia
- Konfiguracja alertu na CPU przez portal lub CLI.
- Analiza logów aplikacji przez Log Analytics.
- Tworzenie workbooka do wizualizacji metryk.

## Komendy
- Tworzenie alertu:
	`az monitor metrics alert create --name cpuAlert --resource-group rg --scopes <resourceId> --condition "avg Percentage CPU > 80" --window-size 5m --evaluation-frequency 1m --action <actionGroupId>`
- Tworzenie Log Analytics Workspace:
	`az monitor log-analytics workspace create --resource-group rg --workspace-name mylogs`
- Wysyłanie logów do Event Hub:
	`az monitor diagnostic-settings create --resource <resourceId> --name sendToEventHub --event-hub <eventHubId> --logs '[{"category": "AllLogs", "enabled": true}]'`

## Wskazówka egzaminacyjna
- Alerty mogą wywoływać akcje automatyczne (np. restart, webhook).
- Najczęstszy błąd: brak przypisania Action Group do alertu lub brak uprawnień do workspace.
- KQL jest wymagany do zaawansowanej analizy logów.

## Przykład użycia

- Konfiguracja przez portal Azure.
- Tworzenie alertów na podstawie metryk.
- Brak kodu C#, konfiguracja graficzna.

---

