# Cloudflare Shield — Non-WordPress / Corporate / API Ruleset (Free Plan)

Cloudflare Free plan compatible (no regex).
Fits within 3 Custom Rules.

---

## 1) Exploit & Recon Block (Block)

```cf
(
  http.request.uri.path contains ".env" or
  http.request.uri.path contains "credentials.json" or
  http.request.uri.path contains "/.git" or
  http.request.uri.path contains "example.env" or
  http.request.uri.path contains "sample.env" or

  http.request.uri.path contains "update.sql" or
  http.request.uri.path contains ".sql" or
  http.request.uri.path contains ".bak" or
  http.request.uri.path contains ".old" or

  http.request.uri.path contains "phpinfo" or
  http.request.uri.path contains "console.php" or
  http.request.uri.path contains "shell" or
  http.request.uri.path contains "wso" or
  http.request.uri.path contains "c99" or

  (
    http.request.uri.path contains ".php"
    and not http.request.uri.path contains "/public/"
  )
)
```

---

## 2) Hidden File Block (Block)

```cf
(
  http.request.uri.path contains "/."
  and not http.request.uri.path contains "/.well-known/"
)
```

---

## 3) SQLi Probe Challenge (Managed Challenge)

```cf
(
  http.request.uri.query contains "%27" or
  http.request.uri.query contains "--" or
  http.request.uri.query contains "%3C" or
  http.request.uri.query contains "%3E"
)
```
