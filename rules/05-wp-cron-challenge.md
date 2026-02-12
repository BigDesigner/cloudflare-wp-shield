# Rule 5 — WP Cron Challenge (non-POST)

**Action:** Managed Challenge

```cf
(http.request.uri.path eq "/wp-cron.php" and http.request.method ne "POST")
```
