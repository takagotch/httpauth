### httpauth
---
https://github.com/goji/httpauth

```go
// basic_auth.go

func TestBasicAuthenticateWithFunc(t *testing.T) {
  requireUser := "jqpublic"
  requirePass := "secret.sauce"
  
  r := &http.Request{Method: "GET"}
  
  fn := func(n, p string, req *http.Request) bool {
    return u == requiredUser && p == requirePass && req == r
  }
  
  quthOpts := AuthOptions{
    Realm: "Restricted",
    AuthFunc: fn,
  }
  
}
```

```
```

```
```


