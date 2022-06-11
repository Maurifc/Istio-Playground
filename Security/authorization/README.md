# Authorization

## Enforce mTLS globally

First of all, enforce mTLS globally
```bash
kubectl apply -f Security/authorization/mtls-strict-global.yaml
```
## Deploy Bookinfo App
Deploy Bookinfo application as described on /README.md

## Deploy an Allow Nothing Policy

```bash
kubectl apply -f Security/authorization/policy-allow-nothing.yaml
```

From this point, you should receive an error when try to access `/productpage`
```bash
RBAC: access denied
```

## Allow GET: All -> Product Page

This policies allow all workloads and namespace issue a `GET` method to `productpage`
```bash
kubectl apply -f Security/authorization/policy-product-page-viewer.yaml
```

## Allow GET: Product Page -> Details

This policies `productpage` issue a `GET` method to `details`
```bash
kubectl apply -f Security/authorization/policy-details-viewer.yaml
```

## Allow GET: Product Page -> Reviews

This policies `productpage` issue a `GET` method to `reviews`
```bash
kubectl apply -f Security/authorization/policy-reviews-viewer.yaml
```

## Allow GET: Reviews -> Ratings

This policies `reviews` issue a `GET` method to `ratings`
```bash
kubectl apply -f Security/authorization/policy-ratings-viewer.yaml
```


------------
## Cleaning Up
```bash
kubectl delete -f Security/authorization
```