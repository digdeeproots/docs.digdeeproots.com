---
title: Use builders
---

# Test with builders
## Builders clarify the initial state

The builders can also be used in your production code &mdash; they aren't just test helpers. In this example, we extracted the code that creates a new test context (empty data).

```csharp
[Fact]
void RunBeeReport()
{
  var sightingDate = Arbitrary.DateTime();
  using InitialData.Empty();
  IncludeData.BeeSighting(sightingDate)
    .InCounty(Arbitrary.ForeignCounty)
    .Build();

  var testSubject = Helpers.CreateReportPage();
  testSubject.DoRunReport(ReportTypes.Honeybee,
    Arbitrary.DateBefore(sightingDate),
    Arbitrary.DateAfter(sightingDate),
    Arbitrary.ForeignCounty);

  testSubject.CurrentReport().Should()
    .BeValidBeeReport()
    .WithData(sighting);
}
```