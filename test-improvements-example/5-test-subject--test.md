---
title: Clear test subject
description: Designate exactly one object or method as the test subject
---

```csharp
[Fact]
void RunBeeReport()
{
  SightingsData.Clear();
  var sightingDate = Arbitrary.DateTime();
  var sighting = Helpers.AddBeeSighting(sightingDate, Arbitrary.ForeignCounty);

  var testSubject = Helpers.CreateReportPage();
  testSubject.DoRunReport(ReportTypes.Honeybee,
    Arbitrary.DateBefore(sightingDate),
    Arbitrary.DateAfter(sightingDate),
    Arbitrary.ForeignCounty);

  testSubject.CurrentReport().Should()
    .BeValidBeReport()
    .WithData(sighting);
}
```