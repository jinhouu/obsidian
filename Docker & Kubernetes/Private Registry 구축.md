## Privete Registry가 필요한 이유

기업 또는 개인이 빌드한 이미지에는 OS 및 미들웨어 설정 등의 정보가 포함되어 있으므로,
보안상 Docker Hub 에 공개적으로 올릴 수 없는 경우에 구축하여 사용한다.

회사 인프라 내에 private docker registry 를 구축하기 위해서 `registry` image를 사용한다.

## Docker Registry 구성하기

### 1. Registry Image Pull
```bash
docker pull registry
```
Docker Hub로부터 `registry` 이미지를 받아온다.
### 2. Run Registry Contrainer

``` bash
docker run -d \
-v /home/user/registry_data:/var/lib/registry \
-p 5000:5000 \
--restart=always \
--name=local-regisrtry \
registry
```
옵션 설명
- `-v /home/user/registry_data:/var/lib/registry` :
host(로컬머신) /home/user/registry_data 경로와 컨테이너의 /var/lib/registry 경로 동기화
- `-p 5000:5000` :
docker-proxy를 이용하여 5000번 포트로의 요청을 컨테이너 내부 5000번의 포트로 전달
- `--restart=always` :
컨테이너가 종료되면 항상 재시작함. 시스템 재부팅 시에도 자동으로 다시 실행됨
- `--name=local-regisrtry` :
컨테이너의 이름을 "local-registry"로 지정함

### 3. docker에 private registry 등록

docker는 local-registry에 대해 모르고 있기 때문에, 이를 등록하는 과정이 필요하다.


```bash
sudo vi /etc/docker/daemon.json 
```

```json
// daemon.json 
{
  "insecure-registries": ["localhost:5000"]
}
```
```bash
# 변경 후 Docker 재시작
sudo systemctl restart docker

docker info | grep -A1 "Insecure Registries"

# 출력내용 확인하기
# Insecure Registries:
#  localhost:5000
```
Docker Desktop의 경우
```
Preferences → Docker Engine
아래 JSON에 "insecure-registries": ["localhost:5000"] 추가
“Apply & Restart” 클릭
```

### 4. private registry로 이미지 push 하기

```bash
docker pull nginx:latest
docker tag nginx:latest localhost:5000/nginx-test
docker push localhost:5000/nginx-test

curl http://localhost:5000/v2/_catalog

# 출력내용 확인하기
# {"repositories":["nginx-test"]}
```

### 5. private registry에서 이미지 pull
```bash
# 이미지 확인 후 기존 태그 변경한 이미지 삭제
docker images
docker rmi localhost:5000/nginx-test

# 이미지 받은 후 확인하기
docker pull localhost:5000/nginx-test
docker images
```



