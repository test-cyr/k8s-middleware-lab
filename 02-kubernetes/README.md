# 02. Kubernetes (kind) 기본 구성

## 목표
kind로 로컬 클러스터를 만들고, Deployment로 Nginx 파드를 2개 유지하게 한 뒤, 파드를 지웠을 때 자동으로 복구되는지 확인한다.

## 클러스터 생성
`kind create cluster --name lab`     
![nodes](/docs/imges/23.create-cluster.png)   
`kubectl get nodes`   
![nodes](/docs/imges/24.kind-nodes.png)  

## Deployment 적용
설정 파일: [deployment.yaml](deployment.yaml)

`kubectl apply -f deployment.yaml` 
`kubectl get pods` 
![pods](/docs/imges/25.pods-running.png)  

- replicas를 2로 설정해서 Nginx 파드 2개가 실행됐다.

## 파드 삭제 후 자동 복구
`kubectl delete pod (pod name)` 
![self heal](/docs/imges/26.pods-recovered.png)  

- 파드를 지우자 바로 새 파드가 만들어져, 지운 직후 조회에서도 `Running` 파드가 2개였다.

## 확인한 점
- 파드를 지운 직후에도 `kubectl get pods`에 파드가 2개로 유지됐고, 새 파드는 AGE가 7초였고, 기존 파드는 5분 24초였다.
- 지운 파드와 이름이 다른 파드가 새로 만들어졌다. 같은 파드를 되살리는 게 아니라 새로 만든다는 점을 알 수 있었다.
- 어제 compose에서는 Tomcat을 `stop`하면 직접 `start`할 때까지 멈춰 있었는데, Kubernetes는 지워도 자동으로 개수를 맞췄다.
