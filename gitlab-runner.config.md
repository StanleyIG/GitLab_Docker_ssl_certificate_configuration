# При создании (инициализации) gitlab-runner

### Когда runner запускает job контейнеры (например, для выполнения CI/CD), они:

 - НЕ получают extra_hosts от runner'а
 - НЕ видят запись в /etc/hosts
 - НЕ могут резолвить gitlab.example.com

Решение - регистрация с правильными параметрами:

```
docker exec -it gitlab-runner gitlab-runner register \
  --non-interactive \
  --url "https://gitlab.example.com" \
  --token "glrt-jAuqSawK9OgLAhN_gz_ON286MQpwOjEKdDozCnU6MQ8.01.1709smqco" \
  --description "docker-runner-fixed" \
  --executor "docker" \
  --docker-image "alpine:latest" \
  --docker-volumes "/var/run/docker.sock:/var/run/docker.sock" \
  --docker-volumes "/cache" \
  --docker-extra-hosts "gitlab.example.com:172.20.0.10" \
  --docker-network-mode "gitlab_net" \
  --docker-pull-policy "if-not-present" \
  --env "GIT_SSL_NO_VERIFY=1"
```
#### Ключевые параметры:
- ```--docker-extra-hosts``` - добавит gitlab.example.com:172.20.0.10 в /etc/hosts job контейнеров
- ```--docker-network-mode "gitlab_net"``` - job контейнеры будут в той же Docker сети
- ```--env "GIT_SSL_NO_VERIFY=1"``` - игнорировать SSL ошибки для self-signed сертификатов