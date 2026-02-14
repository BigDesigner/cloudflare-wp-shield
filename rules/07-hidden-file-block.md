# Rule — Hidden File Block

Action: Block

```cf
(
  http.request.uri.path contains "/."
  and not http.request.uri.path contains "/.well-known/"
)
```
