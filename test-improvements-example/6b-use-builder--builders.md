---
title: Define builders
subtitle: Builders provide a flexible way to set up a complex state
---

```csharp
public class BeeSightingBuilder
{
  Date when;
  string County = "Fremont";
  public BeeSightingBuilder(Date when)
  {
    When = when;
  }

  public BeeSightingBuilder InCounty(string county)
  {
    County = county;
  }

  public BeeSighting Build()
  {
    var location = new Location()
    {
      Name = "Testing Bee Farm";
      Coordinates = LatLong.From(32.12, 45.67);
      LocationType = LocationTypes.Client;
      Address = "";
      County = County;
      ZipCode = "";
    };
    var sighting = new BeeSighting()
    {
      Location = location;
      SightingDate = When;
      Duration = TimeSpan.FromHours(3);
      Quantity = "swarm";
      ObservedBy = "farmer";
      // ... a dozen more fields
    };
    SightingsData.AddSighting(sighting, location);
    return sighting;
  }
}
```
