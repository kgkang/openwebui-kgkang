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

### OpenWebUI 접속

브라우저에서 http://localhost:3000 접속한다.