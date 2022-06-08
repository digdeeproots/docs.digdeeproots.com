---
title: Define custom asserts
subtitle: Custom asserts translate intention into verifications
---

```csharp
public class ReportAssertions : ObjectAssertions<Report, ReportAssertions>
{
  public ReportAssertions BeValidBeeReport()
  {
    Subject.Should()
      .HavePrimaryFormat(Formats.Pdf).And
      .SupportHtmlFormat($"bee?id=${Subject.Id}");
    Subject.ReportType.Should()
      .Be(ReportTypes.Honeybee);
    return this;
  }

  public ReportAssertions WithData(params Sighting[] sightings)
  {
    Subject.Data.Should()
      .ContainExactly(sightings);
    return this;
  }

  public void HavePrimaryFormat(Format expectedFormat)
  {
    report.PrimaryFormat.Should().Be(expectedFormat);
  }

  public void SupportHtmlFormat(string reportLink)
  {
    Subject.Should()
      .HaveProperties({
        HasHtmlFormat = true,
        HtmlVersionLink = "https://rpt01.testing.example.com/reports/" + reportLink
      });
  }

  // framework-specific details elided...
}
```