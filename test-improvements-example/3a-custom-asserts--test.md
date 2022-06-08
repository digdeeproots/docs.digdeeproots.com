---
title: Use custom asserts
---

# Test with custom asserts
## Custom asserts reveal the test's intention

```csharp
[Fact]
void RunBeeReport()
{
  // Arrange
  SightingsData.Clear();
  var sighting = Helpers.AddBeeSighting(new DateTime("5/22/2021"), county="Madison");
  var reportPage = Helpers.CreateReportPage();

  // Act
  reportPage.DoRunReport(ReportTypes.Honeybee, "1/15/2020", "3/15/2022", "Madison");

  reportPage.CurrentReport().Should()
    .BeValidBeeReport()
    .WithData(sighting);
}
```