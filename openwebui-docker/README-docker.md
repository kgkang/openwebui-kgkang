## Docker를 이용해서 로컬에 설치하기

### Docker-compose 파일

* volumes에 데이터를 저장하기 위한 자기 local 폴더 명을 설정한다.

```yaml
version: "3.8"

services: # OpenWebUI
  openwebui:
    image: ghcr.io/open-webui/open-webui:main
    ports:
      - "3000:8080"
    volumes:
      - /Users/kkg/ai/openwebui-dify/openwebui:/app/backend/data
    restart: always
    networks:
      - shared_bridge_network

  # pipelines
  pipelines:
    image: ghcr.io/open-webui/pipelines:main
    ports:
      - "9099:9099"
    volumes:
      - /Users/kkg/ai/openwebui-dify/pipelines:/app/pipelines
    extra_hosts:
      - "host.docker.internal:host-gateway"
    restart: always
    networks:
      - shared_bridge_network

networks:
  shared_bridge_network:
    driver: bridge
```

### docker compose를 통해 로컬 설치하기

```
$ docker compose up -d -f docker-compose.yaml 
```

### docker compose 중지 및 종료

```bash
# 서비스 중지
$ docker compose stop
# 서비스 다시 시작
$ docker compose start
# 서비스 종료
$ docker compose down
# 서비스 종료 (docker volume 같이 삭제)
$ docker compose down -v
```

* 아래와 같이 익명 볼륨을 사용하면 `docker compose down`  시 익명 볼륨이 자동 삭제됨

  ```
  ...
  services:
    openwebui:
      image: ghcr.io/open-webui/open-webui:main
      ports:
        - "3000:8080"
      volumes:
        - /shared_data/openwebui  # 익명 볼륨 (자동 삭제됨)
  ...
  ```


### OpenWebUI 접속

브라우저에서 http://localhost:3000 접속한다.