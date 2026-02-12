# Rule 1 — Block XMLRPC

**Action:** Block

```cf
(http.request.uri.path eq "/xmlrpc.php")
```

## Why
XML-RPC is frequently abused. If you don't rely on XML-RPC features, blocking it is typically safe.
