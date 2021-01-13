Running:

```basb
$ gopls imports mypkg/misses-the-import.go
```

Gives:

```
--- mypkg/misses-the-import.go.orig
+++ mypkg/misses-the-import.go
@@ -1,3 +1,5 @@
 package mypkg
+
+import "github.com/stripe/stripe-go/v71"

 var _ = stripe.PriceRecurringIntervalWeek
```

While `import "github.com/stripe/stripe-go/v72"` would've been expected, as it
is in `go.mod`: `github.com/stripe/stripe-go/v72 v72.28.0`.

Other:

```
$ gopls version
golang.org/x/tools/gopls master
    golang.org/x/tools/gopls@v0.0.0-20210113180300-f96436850f18 h1:rKsQZP3itf3QcmSiYv0td+LXXZxSzQfp+9mvEcNp5EA=
$ go version
go version go1.15.6 darwin/amd64
$ ls ~/go/pkg/mod/github.com/stripe/stripe-go
v71@v71.48.0  v72@v72.27.0  v72@v72.28.0  v72@v72.29.0
```

Removing `v71@v71.48.0` from `$GOPATH/pkg/mod/github.com/stripe/stripe-go`
resolves it. Bringing v71 back to `pkg/mod` enables it.
