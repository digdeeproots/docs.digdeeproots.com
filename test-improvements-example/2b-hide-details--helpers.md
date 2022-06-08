```csharp
public static class Helpers
{
  public static BeeSighting AddBeeSighting(Date when, string county="Fremont")
  {
    var location = new Location()
    {
      Name = "Testing Bee Farm";
      Coordinates = LatLong.From(32.12, 45.67);
      LocationType = LocationTypes.Client;
      Address = "";
      County = county;
      ZipCode = "";
    };
    var sighting = new BeeSighting()
    {
      Location = location;
      SightingDate = when;
      Duration = TimeSpan.FromHours(3);
      Quantity = "swarm";
      ObservedBy = "farmer";
      // ... a dozen more fields
    };
    SightingsData.AddSighting(sighting, location);
    return sighting;
  }

  public static ReportPage CreateReportPage()
  {
    var reportPage = new ReportPage();
    reportPage.ShowReports();
    return ReportPage;
  }
}
```