# Podman /  Buildah / Skopeo

## 등장 배경

- 도커가 가지고 있는 여러 문제점을 해결하기 위해서 등장

### 도커의 문제점

1. High & Low Level Runtime Container
    
    모든 런타임 환경을 가지고 있는 것은 장점이지만, 무겁고 하나의 기능만을 원하는 경우 (컨테이너 기동, 도커 이미지 빌드, 이미지 pull & push 등) 만을 사용하려는 경우에도 전체를 활용해야 하는 단점이 존재.
    

1. SPOF
    
    Docker Demon 하위에 여러 컨테이너를 기동하고 관리한다. k8s master / worker 노드안에 Demon에 장애가 발생할 경우 장애가 전파되어 single point of failure를 대표하는 장애 포인트가 될 수 있다.
    
2. Audit
    
    Linux 커널에 존재하는 Audit 이라는 기능이 존재 → 시스템의 보안 이벤트를 감시하고 외부로부터 침입 감시
    
    Docker는 Client / Server 모델을 활용하기 때문에 Docker demon 및 하위 child 컨테이너들은 모두 같은 uid를 가진다. 따라서 audit을 활용한 보안 기능을 사용할 수 없다.
    

<img width="800" src="./img/podman 0.png">

## Podman

<img width="650" src="./img/podman 1.png">


- docker cli와 비슷한 역할을 수행하는 tool
- container생성, 유지 및 관리 도구
- docker와는 다르게 각 container들을 **fork/exec 방식**으로 실행해서 별도로 구동
- daemon-less 형태로 실행
- root권한을 요구하지 않음 -> 단, 컨테이너간 프라이빗 네트워크 설정 시 권한 필요
  - Docker Demon과는 달리 리눅스에 직접 격리된 프로세스를 생성하기 때문

## Buildah

- Buildah는 OCI 이미지를 생성하는 도구
- docker build를 대체하여 CRI-O 환경에서 container image를 build할 때 사용됨.

## Skopeo

- Skopeo는 docker의 Docker Content Trust (DCT) 기능을 대체
- image registry에 대해서 이미지 검사, 인증을 진행
- 기존 docker에서 image를 docker registry에 push하기 위해서는 pull, tag, push등 좀 번거로운 과정을 거쳤다면 Skopeo는 간단하게 copy 명령으로 간단하게 push 가능

### 3가지 툴 정리

<img width="800" src="./img/podman 2.png">

### 참조

CRI-O와 함께 사용되는 툴들

[https://ikcoo.tistory.com/193](https://ikcoo.tistory.com/193)
