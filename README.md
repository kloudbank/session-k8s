# session-k8s
session architecture sample application for k8s manifest

# session-redis
- redis 를 배포한다.
```
$ cd session-k8s
$ kubectl apply -k ./dev/redis/session
$ kubectl apply -k ./dev/redis/cache
```
- local 에서 redis port 를 연결한다.
```
$ kubectl port-forward service/redis-session 7000:6379
$ kubectl port-forward service/redis-cache 7001:6379
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
redis-session.session-dev.svc.cluster.local:6379
redis-cache.session-dev.svc.cluster.local:6379
```

# session-mariadb
- mariadb 를 배포한다. (2ea: employees, world)
```
$ cd session-k8s
$ kubectl apply -k ./dev/mariadb/employees
$ kubectl apply -k ./dev/mariadb/world
```

- sample data 생성 참조 URL
```
# employees
https://dev.mysql.com/doc/employee/en/employees-installation.html
# world
https://dev.mysql.com/doc/world-setup/en/world-setup-installation.html
```

- local에서 접속 시,, 아래 실행 후, db 접속 프로그램으로 접속 (sequel pro 등)
```
kubectl port-forward service/mariadb-emp 3300:3306 -n session-dev
kubectl port-forward service/mariadb-world 3301:3306 -n session-dev
```
- 혹은 container 실행하여 아래처럼 cli 로 접속
```
kubectl run -it --rm --image=mariadb:latest -n session-dev --restart=Never mysql-client -- mysql -h mariadb-<db name> -pskcc
```

- database scheme 확인
  1. mariadb-emp
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

  2. mariadb-world
```
MariaDB [(none)]> use world;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [world]> show tables;
+-----------------+
| Tables_in_world |
+-----------------+
| city            |
| country         |
| countrylanguage |
+-----------------+
3 rows in set (0.001 sec)
```
