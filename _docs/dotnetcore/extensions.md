---
title: ASP.NET Core
category: .NET Core
order: 2
---

## Extension method to detect ajax-like requests:

``` cs
using Microsoft.AspNetCore.Http;
using Microsoft.Net.Http.Headers;

// ..

public static class HttpRequestExtensions
{
    public static bool IsApiCall(this HttpRequest request)
    {
        var isJson = request.GetTypedHeaders().Accept.Contains(new MediaTypeHeaderValue("application/json"));

        return isJson || request.Path.Value.StartsWith("/api/");
    }
}
    
```
