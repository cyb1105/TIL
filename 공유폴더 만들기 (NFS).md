## 공유폴더 만들기 (NFS)

### server(10.0.0.130)

- nfs 설치 확인

```shell
rpm -qa nfs-utils
```

- nfs 환경 설정

````
vi /etc/exports

/share 10.0.0.*(rw,sync)
````

- 공유폴더 생성

```
mkdir /share
chmod 707 /share - 권한부여

cd /share/
vi file1 - hello
```

- nfs서버 시작

```
systemctl restart nfs-server
systemctl enable nfs-server
```

- nfs공유폴더 설정 확인

```
exportfs -v 
```

- 방화벽 멈추기

```
systemctl stop firewalld
```

--------

### client(10.0.0.132)

- nfs 설치확인

```
rpm -qa nfs-utils
```

- 서버에 마운트되어있는 폴더 확인

```
[root@localhost ~]# showmount -e 10.0.0.130
Export list for 10.0.0.130:
/share 10.0.0.*
```

- 마운트할 폴더 생성

```
mkdir myshare
```

- 마운트

```
[root@localhost ~]# mount -t nfs 10.0.0.130:/share myshare
									서버쪽          클라이언트
[root@localhost ~]# ls -l myshare/
합계 4
-rw-r--r--. 1 root root 6  5월 27 13:58 file1 <- 마운트확인
```





