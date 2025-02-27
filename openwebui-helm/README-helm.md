## Helm을 통해 설치하기

### chart 파일 다운로드

```bash
$ helm repo add open-webui https://helm.openwebui.com
$ helm repo update open-webui
$ helm pull open-webui/open-webui --version 5.10.0
```

### 설치

AWS 설치

```bash
$ helm install openwebui open-webui-5.10.0.tgz -f values-aws.yaml
```

### 업데이트

values-aws.yaml을 수정 후 아래 명령으로 업데이트 한다.

```bash
$ helm upgrade openwebui open-webui-5.10.0.tgz -f values-aws.yaml
```

## 