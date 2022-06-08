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
  var report = reportPage.CurrentReport();

  // Assert
  Assert.IsNotNull(report);
  Assert.Equals(ReportTypes.Honeybee, report.ReportType);
  Assert.Equals(1, report.Data.Count);
  Assert.Equals(sighting, report.Data[0] as BeeSighting);
  Assert.Equals(Formats.Pdf, report.PrimaryFormat);
  Assert.True(report.HasHtmlFormat);
  Assert.Equals($"https://rpt01.testing.example.com/reports/bee?id=${report.Id}", report.HtmlVersionLink);
}
```