## Useful command


### Test with a temporary pod

```
k run tmp --restart Never --rm --image nginx:alpine -i -- curl http://project-plt-6cc-svc.pluto:3333
```