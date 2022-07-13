# 쿠버네티스(**kubernetes )**

## 1. 쿠버네티스 개념

- Pod
    
  ![image](https://user-images.githubusercontent.com/73684562/178758920-da025f32-f723-456c-8ae6-0a95d08eebaf.png)
    
    - 배포할수 있는 가장 작은 단위
    - 한개 이상의 컨테이너와 스토리지, 네트워크 속성을 가진다.
    - pod안에 컨테이너는 네트워크와 스토리지를 공유한다.
- ReplicaSet
    - pod를 여러개로 복제하여 관리(생성, 유지)
    - 직접적으로 사용하기보다는 Deploymet등 오브젝트에 의해서 사용된다.
- Service
    - Pod를 외부 네트워크와 연결해주고 여러개의 pod를 바라보는 내부 loadbalacer를 생성
    - 서비스 디스커버리 역할
- Volume
    - 저장소

## 2. 쿠버네티스 클러스터 아키텍쳐

![image](https://user-images.githubusercontent.com/73684562/178758969-6682336b-05ab-4d70-8fb3-7662670ce3ce.png)

- 여러대의 서버가 하나의 클러스터로 연결되어 있고
- 클러스터 Master 와 클러스터 work Node로 구성된다.

## 3. 구성요소

### 클러스터 마스터 (Cluster Master)

![image](https://user-images.githubusercontent.com/73684562/178759033-864756d7-9c70-4c59-b829-5180e3b2d938.png)

- 클러스터의 두뇌
- 컨테이너를 스케쥴링, 서비스 관리, api서비서 호출 및 수행
- pod와 resource를 컨트롤하고, loadbalacer를 관리
- etcd
    - key-value의 분산  데이터 저장소
    - 분산 및 복제 가능하여 안정성 및 속도가 높다.
    - 상태가 변경되면 확인하여 로직 실행
- API server
    - 들어오는 모든 요청을 처리
    - 원하는 상태를 key-value 저장소에 저장하고 상태를 조회
    - 노드에 실행중인 컨테이너의 로그확인, 명령 전달 (디버거)
- scheduler
    - 할당되지 않은 pod를 필요한 자원,라벨에 따라 적절한 노드서버로 할당
- controller
    - 오브젝트 상태 관리
    - Deployment : ReplicaSet 생성
    - ReplicaSet : Pod생성
    - Pod:  스케쥴러가 관리

### 클러스터 워커 노드(Cluster Worker Node)

![image](https://user-images.githubusercontent.com/73684562/178759076-6d1a6e2d-f55a-4019-a653-7164ad1ea4c8.png)

- 사용자의 워커로드를 실행
- master의 관리아래 실제 pod와 같은 resource가 실행되는 노드
- 큐블릿 (kubelet )
    - pod의 생명주기 관리
    - pod를 생성하고 컨테이너에 이상 유무를 마스터에 전달
    - api서버의 요청으로 컨테이너의 로그전달, 명령수행 역할
- 프록시(proxy)
    - pod로 연결되는 네트워크 관리

## 4. 동작과정

![image](https://user-images.githubusercontent.com/73684562/178759134-dab2a18c-3d61-499f-826d-5b7fa2149609.png)

- kubectl도구를 이용하여 api 서버에 명령전달 후 object를 etcd저장소에 저장
- contoller에서 조건에 만족하는 pod존재 유무 체크 후 없으면 api server가 pod생성
- scheduler는 조건에 맞는 전체노드에 대해node를 찾아 pod할당
- kubelet는 자기 노드에 할당된 pod생성 , pod상태를 주기적으로 api에 전달

- 참고
