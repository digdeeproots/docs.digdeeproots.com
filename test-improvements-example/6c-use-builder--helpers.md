---
title: Simpler Helpers
description: Extracted code out of the helpers into the builders
---

```csharp
public class InitialData : DisposableBase
{
  public Transaction TestContext = new Transaction();
  public InitialData()
  {
    SightingsData.Clear();
  }

  public void DisposeOfManagedResources()
  {
    TestContext.RollBack();
    TestContext.Dispose();
  }
}

public class IncludeData
{
  public static BeeSightingBuilder BeeSighting(Date when)
  {
    return new BeeSightingBuilder(when);
  }
}

public static class Helpers
{
  public static ReportPage CreateReportPage()
  {
    var reportPage = new ReportPage();
    reportPage.ShowReports();
    return ReportPage;
  }
}
```