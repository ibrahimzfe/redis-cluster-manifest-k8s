# redis-cluster-manifest-k8s
Kubernetes/Openshift manifest YAML build by my OWN

Step 1:

1. Deploy dengan cara: kubectl create secret generic redis-tls --from-file=redis.crt --from-file=redis.key --from-file=ca.crt -n NAMANAMESPACE
2. Jalankan kubectl apply -f redis-cluster.yaml -n NAMANAMESPACE
3. Jalankan perintah berikut untuk JOIN
   kubectl exec -it redis-cluster-0 -n redis-cluster -- redis-cli --tls \
  --cert /tls/redis.crt --key /tls/redis.key --cacert /tls/ca.crt -a ADDPASSWORD \
  --cluster create \
  redis-cluster-0.redis-cluster.redis-cluster.svc.cluster.local:6380 \
  redis-cluster-1.redis-cluster.redis-cluster.svc.cluster.local:6380 \
  redis-cluster-2.redis-cluster.redis-cluster.svc.cluster.local:6380 \
  redis-cluster-3.redis-cluster.redis-cluster.svc.cluster.local:6380 \
  redis-cluster-4.redis-cluster.redis-cluster.svc.cluster.local:6380 \
  redis-cluster-5.redis-cluster.redis-cluster.svc.cluster.local:6380 \
  redis-cluster-6.redis-cluster.redis-cluster.svc.cluster.local:6380 \
  redis-cluster-7.redis-cluster.redis-cluster.svc.cluster.local:6380 \
  redis-cluster-8.redis-cluster.redis-cluster.svc.cluster.local:6380 \
  --cluster-replicas 2


