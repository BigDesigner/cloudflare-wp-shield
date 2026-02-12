# Troubleshooting

## Legitimate root PHP endpoint blocked by Rule 2
If you have endpoints like `/api.php`, `/gateway.php` in the root, add whitelist exceptions inside the `.php` block.

Example:
```cf
(
  http.request.uri.path contains ".php" and
  not http.request.uri.path contains "/api.php" and
  not http.request.uri.path contains "/gateway.php" and
  not http.request.uri.path contains "/wp-" and
  not http.request.uri.path contains "/wp-content/" and
  not http.request.uri.path contains "/wp-includes/"
)
```

## Free plan limitation
Cloudflare Free plan does not support regex via the `matches` operator. This ruleset avoids regex entirely.
