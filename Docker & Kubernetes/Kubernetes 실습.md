이 코스는 **kind** 클러스터(로컬 환경 기준)에서 **기본 → 핵심 리소스 → 네트워킹 → 스토리지 → 고급 개념** 순으로 진행됩니다.

---

## 🧭 전체 로드맵

|단계|주제|키워드|난이도|
|---|---|---|---|
|1단계|쿠버네티스 구조 이해|Node, Pod, Control Plane|🌱 기본|
|2단계|Pod 실습|YAML, Pod 생성/삭제, 로그|🌱|
|3단계|ReplicaSet & Deployment|롤링업데이트, 스케일링|🌿|
|4단계|Service 이해|ClusterIP, NodePort, LoadBalancer|🌿|
|5단계|ConfigMap / Secret|환경변수, 보안 설정|🍀|
|6단계|Volume & PVC|데이터 유지, 볼륨 마운트|🍀|
|7단계|Ingress|외부 트래픽 라우팅|🌳|
|8단계|Helm / 네임스페이스 / 리소스 관리|효율적 관리|🌳|
|9단계|고급 개념|taint, affinity, rolling update, probes|🌲|

---

## 🧩 1단계. 클러스터 구성 & 노드 확인

`kubectl cluster-info kubectl get nodes kubectl describe node study-worker`

👉 쿠버네티스 클러스터가 어떤 노드로 구성되어 있는지 감을 잡습니다.  
(Control Plane / Worker 구분)

---

## 🧱 2단계. Pod 실습

**nginx Pod 생성**

`kubectl run my-nginx --image=nginx --port=80 kubectl get pods kubectl describe pod my-nginx kubectl logs my-nginx`

**YAML로 생성**

`kubectl get pod my-nginx -o yaml > nginx.yaml kubectl delete pod my-nginx kubectl apply -f nginx.yaml`

👉 Pod는 쿠버네티스의 가장 작은 실행 단위입니다.  
컨테이너를 감싸는 “관리 껍데기”라고 보면 됩니다.

---

## 🌱 3단계. ReplicaSet & Deployment

**Deployment 생성**

`kubectl create deployment web --image=nginx --replicas=3 kubectl get pods kubectl get deployment`

**롤링 업데이트 실습**

`kubectl set image deployment/web nginx=nginx:1.25 kubectl rollout status deployment/web kubectl rollout history deployment/web`

**스케일 아웃**

`kubectl scale deployment web --replicas=5`

👉 Deployment는 Pod 개수를 관리하고, 자동 롤백/업데이트를 담당합니다.

---

## 🌐 4단계. Service 실습

**Service 생성**

`kubectl expose deployment web --type=NodePort --port=80 kubectl get svc`

**포트 확인 후 접속**

`kubectl describe svc web`

👉 Service는 클러스터 내외부 트래픽을 Pod에 라우팅하는 Load Balancer 역할.

---

## 🔑 5단계. ConfigMap & Secret

**ConfigMap**

`kubectl create configmap app-config --from-literal=APP_MODE=debug kubectl get configmap app-config -o yaml`

**Secret**

`kubectl create secret generic db-secret --from-literal=DB_PASSWORD=1234 kubectl get secret db-secret -o yaml`

👉 환경 변수, 민감 정보 관리의 핵심.

---

## 💾 6단계. Volume & PVC

**YAML 예시 (nginx + 볼륨)**

`apiVersion: v1 kind: Pod metadata:   name: nginx-volume spec:   containers:     - name: nginx       image: nginx       volumeMounts:         - mountPath: "/usr/share/nginx/html"           name: web-data   volumes:     - name: web-data       emptyDir: {}`

`kubectl apply -f nginx-volume.yaml`

👉 Pod 재시작 시 사라지는 데이터 / 유지되는 데이터 차이 학습.

---

## 🌍 7단계. Ingress

**Ingress Controller 설치 (nginx)**

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml`

**간단한 Ingress 예시**

`apiVersion: networking.k8s.io/v1 kind: Ingress metadata:   name: web-ingress spec:   rules:   - host: myapp.local     http:       paths:       - path: /         pathType: Prefix         backend:           service:             name: web             port:               number: 80`

👉 Ingress는 도메인 기반 트래픽 라우팅.

---

## 🪄 8단계. 네임스페이스, 리소스 관리, Helm

`kubectl create namespace dev kubectl config set-context --current --namespace=dev`

**Helm 예시**

`brew install helm helm repo add bitnami https://charts.bitnami.com/bitnami helm install my-redis bitnami/redis`

👉 Helm은 “쿠버네티스용 패키지 매니저”입니다.

---

## ⚙️ 9단계. 고급 주제 체험

- **livenessProbe / readinessProbe**
    
- **nodeSelector / affinity**
    
- **taint / toleration**
    
- **Horizontal Pod Autoscaler**
    
- **Rolling Update 전략**
    

예:

`kubectl autoscale deployment web --min=2 --max=10 --cpu-percent=70`

---

## 🧠 진행 팁

- 각 단계마다 `kubectl describe`, `kubectl get ... -o yaml`로 구조 확인
    
- `kubectl delete all --all`로 깨끗이 리셋 가능
    
- `kubectl explain <리소스명>`으로 문서 확인 가능 (예: `kubectl explain pod.spec`)