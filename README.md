# redis-cluster-manifest-k8s
Kubernetes/Openshift manifest YAML build by my OWN
TLS ENABLE WITH PORT 6380

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

Jika ingin buat custom certificate sendiri jalankan perintah ini:

openssl req -x509 -nodes -newkey rsa:4096 -keyout redis.key -out redis.crt -days 3650 -subj "/CN=redis"
openssl req -x509 -nodes -newkey rsa:4096 -keyout ca.key -out ca.crt -days 3650 -subj "/CN=redis-ca"
atau CN dapat disesuaikan sesuai nama domain atau IP yang kamu ingin allow. Atau gunakan SAN !

