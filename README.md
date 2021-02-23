# session-k8s
session architecture sample application for k8s manifest


# session-redis
- resis 를 배포한다.
```
$ cd session-k8s
$ kubectl apply -k ./dev/redis
```
- local 에서 redis port 를 연결한다.
```
$ kubectl port-forward service/redis-master 7000:6379
```
- local 에서 redis-cli 로 접속하여 테스트 한다.
```
$ redis-cli -p 7000
127.0.0.1:7000> get mykey
"myvalue"
127.0.0.1:7000> set mykey myvalue2
OK
127.0.0.1:7000> get mykey
"myvalue2"
127.0.0.1:7000> 
```
- cluster 내부에서는 아래와 같이 접속한다.
```
session-redis.session-dev.svc.cluster.local:6379
```