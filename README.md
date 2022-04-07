```bash
#startup
docker-compose up -d

# test call app1
curl -v -H Host:web1 localhost:2080

# test call app2
curl -v -H Host:web2 localhost:2080
```
