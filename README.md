```bash
#startup
docker-compose up -d

# test call app1
curl -v -H Host:web1 localhost:2080
curl localhost:2080/apps/web1

# test call app2
curl -v -H Host:web2 localhost:2080
curl localhost:2080/apps/web2
```

```
d22ae8d83869    traefik/whoami       "/whoami"                6 minutes ago   Up 6 minutes       80/tcp      traefik_web2_2
b53a14ec6d2a    traefik/whoami       "/whoami"                6 minutes ago   Up 6 minutes       80/tcp      traefik_web2_1
5ccbd3005281    traefik/whoami       "/whoami"                6 minutes ago   Up 6 minutes       80/tcp      traefik_web1_1
1da05cd9c65e    traefik/whoami       "/whoami"                6 minutes ago   Up 6 minutes       80/tcp      traefik_web1_2
2110b688a5fc    traefik:v2.6         "/entrypoint.sh --ap…"   8 minutes ago   Up 8 minutes       0.0.0.0:2080->80/tcp, :::2080->80/tcp, 0.0.0.0:28080->8080/tcp, :::28080->8080/tcp      traefik

```

```
#web1
Hostname: 5ccbd3005281
IP: 127.0.0.1
IP: 172.22.0.2
RemoteAddr: 172.22.0.6:58360
GET / HTTP/1.1
Host: web1
User-Agent: curl/7.58.0
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: 172.22.0.1
X-Forwarded-Host: web1
X-Forwarded-Port: 80
X-Forwarded-Proto: http
X-Forwarded-Server: 2110b688a5fc
X-Real-Ip: 172.22.0.1

Hostname: 1da05cd9c65e
IP: 127.0.0.1
IP: 172.22.0.3
RemoteAddr: 172.22.0.6:55350
GET / HTTP/1.1
Host: web1
User-Agent: curl/7.58.0
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: 172.22.0.1
X-Forwarded-Host: web1
X-Forwarded-Port: 80
X-Forwarded-Proto: http
X-Forwarded-Server: 2110b688a5fc
X-Real-Ip: 172.22.0.1
```

```
# web2
Hostname: b53a14ec6d2a
IP: 127.0.0.1
IP: 172.22.0.4
RemoteAddr: 172.22.0.6:53582
GET / HTTP/1.1
Host: web2
User-Agent: curl/7.58.0
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: 172.22.0.1
X-Forwarded-Host: web2
X-Forwarded-Port: 80
X-Forwarded-Proto: http
X-Forwarded-Server: 2110b688a5fc
X-Real-Ip: 172.22.0.1

Hostname: d22ae8d83869
IP: 127.0.0.1
IP: 172.22.0.5
RemoteAddr: 172.22.0.6:47348
GET / HTTP/1.1
Host: web2
User-Agent: curl/7.58.0
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: 172.22.0.1
X-Forwarded-Host: web2
X-Forwarded-Port: 80
X-Forwarded-Proto: http
X-Forwarded-Server: 2110b688a5fc
X-Real-Ip: 172.22.0.1
```

### Swarm Mode with custom network

```bash
docker swarm init
docker network create -d overlay traefik-net
docker stack deploy demo  -c docker-compose.swarm.network.yml
```

### Swarm Mode with default network

```bash
docker swarm init
docker stack deploy demo  -c docker-compose.swarm.yml
```
