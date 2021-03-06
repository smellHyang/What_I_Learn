# Docker

### 기존방식

- 하나의 서버에 여러개의 프로그램을 설치하는 과정의 복잡합
- 서버 내 서로 사용하는 라이브러리 버전 및 포트 관리의 까다로움
- 다른 서버에서 각각 관리하면 자원은 남비..
- Devops의 등장하면서 개발주기는 down, 배포는 자주, msa 등장으로 관리가 더욱 복잡해짐

→ 서버 관리 방식 : docker

### 1. 도커란

- 컨테이너 기반의 오픈소스 가상화 플랫폼
- 다양한 프로그램, 실행환경을 컨테이너로 추상화하고 동일 인터페이스를 제공하여 프로그램 배포 및 관리 용이

### 컨테이너

![image](https://user-images.githubusercontent.com/73684562/177720372-193d2262-469c-4d0b-8015-90d0dc450d90.png)

- 격리된 공간에서 프로세스가 동작하는 기술(os가상화)
- 기존 VMware나 VirtualBox는 호스트OS위에 게스트 os전체를 가상화하여 사용 → 무겁고 느리다.
- 프로세스를 격리시켜 cpu, 메모리는 프로세스가 필요한 만큼만 사용하는 방식
    - 하나의 서버에 여러 컨테이너를 실행하여 서로 영향x, 독립접

### 이미지

![image](https://user-images.githubusercontent.com/73684562/177720517-02703b6f-cc12-4693-abbb-ce8b41a0895a.png)

- 컨테이너 실행에 필요한 파일과 설정값들을 포함하고 있는것(Immutable)
- 컨테이너는 이미지를 실행한 상태이고 추가되거나 변하는 값은 컨테이너에 저장

→ 의존성 파일을 컴파일하고 설치하지 않아도된다. 새로운 서버가 추가되면 이미지를 다운받고 컨테이너 생성만하면된다.

## 2. 동작방식

### 레이어 저장방식

![image](https://user-images.githubusercontent.com/73684562/177720555-e08a2c81-c520-4590-90eb-75d2922f2753.png)

- 하나의 이미지에 파일하나를 추가할때 기존이미지를 다운받고 추가하면 비효율
- 따라서 레이어 개념을 사용하여 여러개의 레이어를 하나의 파일시스템으로 사용
- 각 레이어만 다운받거나 추가하면된다.
- ex) ubuntu 이미지가 [A + B + C]의 집합이라면, ubuntu 이미지를 베이스로 만든 nginx 이미지는  [A + B + C + nginx]
- 컨테이너 생성도 레이어 방식 사용 → 기존의 이미지 레이어 위에 읽기/쓰기read-write
 레이어를 추가 → 이미지 레이어를 그대로 사용하묜소 컨테이너가 실행중에 생성하는 파일이나 변경된 내용은 읽기/쓰기 레이어에 저장

### +) 컨테이너 변경

- 컨테이너를 삭제하는건 컨테이너에 생성된 데이터가 모두 사라진다는 것
- 따라서 삭제시 유지해야하는 데이터는 컨테이너 외부스토리지에 저장 (s3, data volumes..)
[---
# before
docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  mysql:5.7

# after
docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  -v /my/own/datadir:/var/lib/mysql \ # <- volume mount
  mysql:5.7
---](https://www.notion.so/flab-kein/Docker-f46dfce1d033460c97c37c4054e60592#20d2f01fa8674665854303b9e6e4b653)
