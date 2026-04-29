# Azure Cognitive Services
---

[Prev: Azure Notification Hubs](notification-hubs.md) | [Next: Azure API for FHIR](api-for-fhir.md)

**Definicja:**
- Zestaw usług AI (analiza obrazu, tekstu, mowy, tłumaczenia, rozpoznawanie twarzy).

**Znaczenie na egzaminie AZ-204:**
- Często pytania o wywołanie API, autoryzację, pricing.

## Kluczowe pojęcia
- **Resource** – instancja Cognitive Services (np. Vision, Speech).
- **Key/Endpoint** – klucz API i adres endpointu.
- **Pricing Tier** – poziom cenowy, limity.
- **SDK/REST API** – wywołania z poziomu kodu.

## Scenariusze egzaminacyjne
- Wywołanie API Vision, Text Analytics, Translator.
- Konfiguracja klucza i endpointu.
- Ograniczenia pricing tier.

## Przykład użycia
- Analiza obrazu przez REST API.
- Wykrywanie sentymentu przez SDK.

## Komendy
- Tworzenie Cognitive Services:
  `az cognitiveservices account create --name mycog --resource-group rg --kind TextAnalytics --sku S`

## Przykład kodu C# (.NET 8)
```csharp
using Azure.AI.TextAnalytics;
var client = new TextAnalyticsClient(new Uri(endpoint), new AzureKeyCredential(key));
var result = await client.AnalyzeSentimentAsync("To jest super!");
```

```csharp
// Przykład: Rozpoznawanie języka
var languageResult = await client.DetectLanguageAsync("Bonjour tout le monde");
Console.WriteLine(languageResult.Value.Iso6391Name); // "fr"

// Przykład: Rozpoznawanie obrazów (Computer Vision)
using Azure.AI.Vision.ImageAnalysis;
var visionClient = new ImageAnalyzerClient(new Uri(endpoint), new AzureKeyCredential(key));
var imageResult = await visionClient.AnalyzeImageAsync("https://example.com/image.jpg", new[] { VisualFeature.Tags });
foreach (var tag in imageResult.Value.Tags)
  Console.WriteLine(tag.Name);

// Przykład: Tłumaczenie tekstu (Translator)
using Azure.AI.Translation.Text;
var translator = new TextTranslationClient(new Uri(endpoint), new AzureKeyCredential(key));
var translation = await translator.TranslateAsync("en", new[] { "Witaj świecie" });
Console.WriteLine(translation.Value[0].Translations[0].Text); // "Hello world"

// Przykład: Rozpoznawanie mowy (Speech to Text)
using Azure.AI.Speech;
var speechConfig = SpeechConfig.FromSubscription(key, region);
using var recognizer = new SpeechRecognizer(speechConfig);
var speechResult = await recognizer.RecognizeOnceAsync();
Console.WriteLine(speechResult.Text);
```

## Wskazówka egzaminacyjna
- Najczęstszy błąd: brak klucza lub zły endpoint.
- Pricing tier ogranicza liczbę wywołań na minutę.
