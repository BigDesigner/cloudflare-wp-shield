# Cloudflare WP Shield — Free Plan Ruleset

> Cloudflare Free plan friendly (no regex).  
> Recommended order: **1 → 5**.

---

## 1) Block XMLRPC (Action: Block)

```cf
(http.request.uri.path eq "/xmlrpc.php")
```

---

## 2) Exploit & Recon Block (Action: Block)

```cf
(
  (
    http.request.uri.path contains ".env" or
    http.request.uri.path contains "wp-config" or
    http.request.uri.path contains "credentials.json" or
    http.request.uri.path contains "/.well-known/credentials" or
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

    http.request.uri.path contains "/admin/files" or
    http.request.uri.path contains "/api/v1/upload" or
    http.request.uri.path contains "/api/content/upload" or
    http.request.uri.path contains "/api/v1/media" or

    (
      (http.request.uri.path contains "install" or
       http.request.uri.path contains "upgrade" or
       http.request.uri.path contains "upgrader")
      and not (http.request.uri.path contains "/wp-admin/")
    ) or

    (
      http.request.uri.path contains ".php" and
      not http.request.uri.path contains "/wp-" and
      not http.request.uri.path contains "/wp-content/" and
      not http.request.uri.path contains "/wp-includes/" and
      not (http.request.uri.path contains "/wp-admin/")
    )
  )
  and not (
    http.request.uri.path contains ".css" or
    http.request.uri.path contains ".js" or
    http.request.uri.path contains ".map" or

    http.request.uri.path contains ".png" or
    http.request.uri.path contains ".jpg" or
    http.request.uri.path contains ".jpeg" or
    http.request.uri.path contains ".gif" or
    http.request.uri.path contains ".svg" or
    http.request.uri.path contains ".webp" or
    http.request.uri.path contains ".ico" or

    http.request.uri.path contains ".woff" or
    http.request.uri.path contains ".woff2" or
    http.request.uri.path contains ".ttf" or
    http.request.uri.path contains ".otf" or
    http.request.uri.path contains ".eot" or

    http.request.uri.path contains ".pdf" or
    http.request.uri.path contains ".doc" or
    http.request.uri.path contains ".docx"
  )
)
```

---

## 3) WP Login Protection (Action: Managed Challenge)

Default (recommended):

```cf
(http.request.uri.path eq "/wp-login.php" and http.request.method eq "POST")
```

Optional variant (include `/wp-admin/` POST too):

```cf
(
  (http.request.uri.path eq "/wp-login.php" or http.request.uri.path eq "/wp-admin/")
  and http.request.method eq "POST"
)
```

---

## 4) SQLi Probe Challenge (Action: Managed Challenge)

```cf
(
  http.request.uri.query contains "%27" or
  http.request.uri.query contains "--" or
  http.request.uri.query contains "%3C" or
  http.request.uri.query contains "%3E"
)
```

---

## 5) WP Cron Challenge (non-POST) (Action: Managed Challenge)

```cf
(http.request.uri.path eq "/wp-cron.php" and http.request.method ne "POST")
```
