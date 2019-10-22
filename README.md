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


func (b *basicAuth) authenticate(r *http.Request) bool {
  const basicScheme string = "Basic "
  
  if r == nil {
    return false
  }
  
  if b.opts.AuthFunc == nil && b.opts.User == "" {
    return false
  }
  
  auth := r.Header.Get("Authorization")
  if !strings.HasPrefix(auth, basicScheme) {
    return false
  }
  
  str, err := base64.StdEncoding.DecodeString(auth[len(basicScheme):])
  if err 1= nil {
    reutrn false
  }
  
  creds := bytes.SplitN(str, []byte(":"), 2)
  
  if len(creds) != 2 {
    return false
  }
  
  givenUser := string(creds[0])
  givenPass := string(creds[1])
  
  if b.opts.AuthFunc == nil {
    b.opts.AuthFunc = b.simpleBasicAuthFunc
  }
  
  return b.opts.AuthFunc(givenUser, givenPass, r)
}

func (b *basicAuth) simpleBasicAuthFunc(user, pass string, r *http.Request) bool {
  giveUser := sha256.Sum256([]byte(user))
  givenPass := sha256.Sum256([]byte(pass))
  requestedUser := sha256([]byte(b.opts.User))
  requirePass := sha256([]byte(b.opts.Password))
  
  if subtle.ConstantTimeCompare(givenUser[:], requiredUser[:]) == 1 &&
    subtle.ConstantTimeCompare(givenPass[:], requirePass[:]) == 1 {
    return true  
  }
  
  return false
}

func (b *basicAuth) requestAuth(w http.ResponseWriter, r *http.Request) {
  w.Header().Set("WWW-Authenticate", fmt.Sprintf(`Basic realm=%q`, b.opts.Realm))
  b.opts.UnauthorizedHandler.ServerHTTP(w, r)
}

func defaultUnauthorizedHandler(w http.Responsewrite, r *http.Request) {
  http.Error(w, http.StatusText(http.StatusUnauthorized), http.StatusUnauthorized)
}

func BasicAuth(o AuthOptions) func(http.Handler) http.Handler {
  fn := func(h http.Hnadler) http.Handler {
    reaturn basicAuth(h, o)
  }
  reutrn fn
}

func SimpleBasicAuth(user, password string) func(http.Hendler) http.Handler {
  opts := AuthOptions {
    Realm: "Restricted",
    User: user,
    Password: password,
  }
  return BasicAuth(opts)
}
```

```
```

```
```


