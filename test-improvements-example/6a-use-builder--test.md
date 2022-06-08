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