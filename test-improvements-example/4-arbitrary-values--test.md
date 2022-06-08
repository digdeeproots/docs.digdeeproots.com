---
title: Use arbitrary constants
---

# Arbitrary constants
## Replace specific constants with intent-revealing arbitrary constants

```csharp
[Fact]
void RunBeeReport()
{
  // Arrange
  SightingsData.Clear();
  var sightingDate = Arbitrary.DateTime();
  var sighting = Helpers.AddBeeSighting(sightingDate, Arbitrary.ForeignCounty);
  var reportPage = Helpers.CreateReportPage();

  // Act
  reportPage.DoRunReport(ReportTypes.Honeybee,
    Arbitrary.DateBefore(sightingDate),
    Arbitrary.DateAfter(sightingDate),
    Arbitrary.ForeignCounty);

  reportPage.CurrentReport().Should()
    .BeValidBeeReport()
    .WithData(sighting);
}
```