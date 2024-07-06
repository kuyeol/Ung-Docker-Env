

# Dev_Zero

> ### https://www.devzero.io/dashboard
> 브라우저 접속


현재 환경에서 접속하기 위해 CLI 설치
```bash
curl -fsSL https://get.devzero.io | sh
```

접속 커맨드

```bash
# Kafka && Kube Container 

 dz ws connect ruling-skylark-sggm
```
```bash
#Minio Container

 dz ws connect brash-filly-xmci
```


# ip 외부 노출

리모트 컨테이너 접속 -> host 확인 

```bash
dz network status
```

> 기존 IP <-> 리모트 컨테이너 IP
>
> 노출중 or 가능한 아이피 와 포트
> PREROUTING -d 180.210.130.220 -p tcp --dport 9000

> 가져올 아이피와 포트 DevZero 연결 인증 후 바인딩 가능 
> -j DNAT --to-destination 100.60.10.10:9000




## 적용 커맨드

```bash
sudo iptables -t nat -A PREROUTING -d 180.210.130.220 -p tcp --dport 9000 -j DNAT --to-destination 100.64.1.14:9000
sudo iptables -t nat -A POSTROUTING -j MASQUERADE

sudo iptables -t nat -A PREROUTING -d 180.210.130.220 -p tcp --dport 9200 -j DNAT --to-destination 100.64.1.38:9200
sudo iptables -t nat -A POSTROUTING -j MASQUERADE

sudo iptables -t nat -A PREROUTING -d 180.210.130.220 -p tcp --dport 8083 -j DNAT --to-destination 100.64.1.38:8083
sudo iptables -t nat -A POSTROUTING -j MASQUERADE

sudo iptables -t nat -A PREROUTING -d 180.210.130.220 -p tcp --dport 9092 -j DNAT --to-destination 100.64.1.38:9092
sudo iptables -t nat -A POSTROUTING -j MASQUERADE

sudo iptables -t nat -A PREROUTING -d 180.210.130.220 -p tcp --dport 80 -m addrtype --dst-type LOCAL -j DNAT --to-destination 199.00.11.1:9000
sudo iptables -t nat -A POSTROUTING -m addrtype --dst-type LOCAL -j MASQUERADE

sudo iptables -t nat -A PREROUTING -d 180.210.130.220  -m addrtype --dst-type LOCAL -j DNAT --to-destination 199.00.11.1:9000
sudo iptables -t nat -A POSTROUTING -j MASQUERADE
```

# 규칙 핸들링

```bash
# 적용 규칙 리스트

sudo iptables -L -t nat --line-numbers
```

```
# 적용 규칙 삭제 
sudo iptables -t nat -D PREROUTING 2 <-- 규칙 넘버
sudo iptables -t nat -D POSTROUTING 2
```



