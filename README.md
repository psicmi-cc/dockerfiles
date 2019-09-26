# 常用命令

- **portainer docker-web-ui**

```
docker run -d --name portainer -p 18000:8000 -p 19000:9000 \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /your/persistent/dir/portainer_data:/data portainer/portainer
```

---

- **sonatype/nexus3**

```
mkdir /your/persistent/dir/nexus-data && chown -R 200 /your/persistent/dir/nexus-data
docker run -d -p 8081:8081 --name nexus -v /your/persistent/dir/nexus-data:/nexus-data sonatype/nexus3
```

---

- **mysql 5.7.23**

```
docker run -d -p 3306:3306 -p 33060:33060 --name mysql5723 \
-v /your/persistent/dir/mysql5723/:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=your-passwd -d mysql:5.7.23 \
--character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```
