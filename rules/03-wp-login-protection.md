# Rule 3 — WP Login Protection

**Action:** Managed Challenge

Recommended:
```cf
(http.request.uri.path eq "/wp-login.php" and http.request.method eq "POST")
```

Optional:
```cf
(
  (http.request.uri.path eq "/wp-login.php" or http.request.uri.path eq "/wp-admin/")
  and http.request.method eq "POST"
)
```
