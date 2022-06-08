```csharp
[Fact]
void RunBeeReport()
{
  // Arrange
  var location = new Location()
  {
    Name = "Testing Bee Farm";
    Coordinates = LatLong.From(32.12, 45.67);
    LocationType = LocationTypes.Client;
    Address = "";
    County = "Madison";
    ZipCode = "";
  };
  var sighting = new BeeSighting()
  {
    Location = location;
    SightingDate = new DateTime("5/22/2021");
    Duration = TimeSpan.FromHours(3);
    Quantity = "swarm";
    ObservedBy = "farmer";
    // ... a dozen more fields
  };
  SightingsData.Clear();
  SightingsData.AddSighting(sighting, location);
  var reportPage = new ReportPage();
  reportPage.ShowReports();

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