# Helm POC

```
helm upgrade --install helm-poc .
```

Then call the function:

```
kubeless function call hello
Connecting to function...
Forwarding from 127.0.0.1:30000 -> 8080
Forwarding from [::1]:30000 -> 8080
Handling connection for 30000
happy helming!
```


Steps to reproduce issue with helm upgrade:
```
# install function:
helm upgrade --install helm-poc .
kubeless function call hello
# outputs "unhappy helming!"

# modify function template:
# NOTE: use -i without empty string if using gnused
# instead of bsd sed
sed -i '' 's/unhappy/happy/g' templates/function.yaml

# update function:
helm upgrade --install helm-poc .
kubeless function call hello
# still outputs "unhappy helming!"
```
