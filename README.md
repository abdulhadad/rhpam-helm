#  RHPAM 7 Openshift Template ke Helm Charts

Konversi RHPAM 7 Openshift Template ke Helm Chart

## Jalankan

```sh
minikube start

helm init
cd rhpam-helm/
helm install --name rhpam --namespace helm-test . # ulangi jika pod tiller belum siap

kubectl get pod --namespace helm-test
kubectl get deployment --namespace helm-test
kubectl get service --namespace helm-test
kubectl get all --namespace helm-test

kubectl expose deployment myapp-rhpamcentr --name rhpamcentr --type=NodePort --namespace helm-test
kubectl expose deployment myapp-kieserver --name kieserver --type=NodePort --namespace helm-test

kubectl get all --namespace helm-test
minikube service rhpamcentr --url --namespace helm-test # cari yg url port internalnya 8080
minikube service kieserver --url --namespace helm-test  # cari yg url port internalnya 8080

# hapus
helm delete rhpam
helm delete --purge rhpam # hapus dengan konfigurasinya
```

### Tes project RH PAM

- Buka urlnya misal http://192.168.99.100:31874,  u:adminUser p:RedHat
- Menu > Design > Projects > Import  https://github.com/jbossdemocentral/rhpam7-mortgage-demo-repo.git > Mortgage Demo > OK > 31 asset imported
- filter > Process, MortgageApplication > close
- project > Deploy > Success, KJAR
- Menu > Deploy > Execution Servers , yang hostname:8080 ganti ke url service kieserver, misal http://192.168.99.100:30509/services/rest/server  u:adminUser p:RedHat (password asumsi dari environment)


## Referensi

- https://blog.openshift.com/from-templates-to-openshift-helm-charts/
- https://github.com/rgordill/helm-repo/tree/master/incubator/mysql