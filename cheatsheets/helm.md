# Helm Cheatsheets

## List releases
```
helm -n <namepsace> ls
```

- By default releases in `pending-upgrade` state aren't listed
```
helm -n <namepsace> ls -a
```

## Install release
```
helm -n <namepsace> install <release> <chart>

helm -n <namepsace> install <release> <chart> --set key=value
```


## Uninstall release
```
helm -n <namepsace> uninstall <release>
```

## List repo
```
helm repo list
```

## Search chart
```
helm search repo <chart-name>
```

## Upgrade release
```
helm -n <namepsace> upgrade <release> <chart-name>
```

## Show values in chart
```
helm show values <chart>
```
