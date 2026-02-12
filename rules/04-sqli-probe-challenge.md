# Rule 4 — SQLi Probe Challenge

**Action:** Managed Challenge

```cf
(
  http.request.uri.query contains "%27" or
  http.request.uri.query contains "--" or
  http.request.uri.query contains "%3C" or
  http.request.uri.query contains "%3E"
)
```
