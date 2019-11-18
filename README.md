# Test OpenFaaS Cloud

https://github.com/openfaas/openfaas-cloud/tree/master/docs#test-it-out

```
#echo -n $PASSWORD | faas-cli login -g $OPENFAAS_URL -u admin --password-stdin

faas-cli new --lang python3 hello-python
echo """def handle(req):
    print('Hello! You said: ' + req)""" > hello-python/handler.py
mv hello-python.yml stack.yml

#faas-cli deploy -g $OPENFAAS_URL

git add hello-python stack.yml
git commit -m "ofc test"
git push
```

`$HOME/.gitconfig`

```
[alias]
  yolo = !git add -A && git commit -am \"$(curl -s http://whatthecommit.com/index.txt)\" && git push -f origin master
```

```
curl -s http://whatthecommit.com/index.txt > yolo.txt && git yolo
```

```
kubectl logs -f deploy/github-event -n openfaas-fn
kubectl logs -f deploy/github-push -n openfaas-fn
kubectl logs -f deploy/git-tar -n openfaas-fn
kubectl logs -f deploy/buildshiprun -n openfaas-fn
kubectl get events --sort-by=.metadata.creationTimestamp -n openfaas-fn
```

```
export OPENFAAS_URL=https://gateway.iot-dev.sda-dev-projects.nl

curl $OPENFAAS_URL/function/salekd-hello-python -d "$(cowsay -s hello)"
```
