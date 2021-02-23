# session-k8s
session architecture sample application for k8s manifest

# session-redis
- redis 를 배포한다.
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

# session-mariadb
- mariadb 를 배포한다.
```
$ cd session-k8s
$ kubectl apply -k ./dev/redis
```

- sample data 생성 참조 URL
```
https://dev.mysql.com/doc/employee/en/employees-installation.html
```

- local에서 접속 시,,
```
kubectl run -it --rm --image=mariadb:latest -n session-dev --restart=Never mysql-client -- mysql -h session-mariadb -pskcc
```

- database scheme 확인
```
MariaDB [(none)]> use employees;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [employees]> show tables;
+----------------------+
| Tables_in_employees  |
+----------------------+
| current_dept_emp     |
| departments          |
| dept_emp             |
| dept_emp_latest_date |
| dept_manager         |
| employees            |
| salaries             |
| titles               |
+----------------------+
8 rows in set (0.001 sec)
```
