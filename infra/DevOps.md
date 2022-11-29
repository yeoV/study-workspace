# DevOps
Keyword : *CICD, Jenkins, SonarQube, DevOps*
## DevOps
- 개발부터 운영까지의 프로세스 속도를 높이는 접근 방식
- CALMS
<img width="400" alt="Pasted image 20221009161717" src="https://user-images.githubusercontent.com/59818703/194895430-4116dae0-31f8-4aca-af36-d8a3a0d87f76.png">

출처:https://www.xalt.de/calms/

***
## CI / CD
어플리케이션 개발 단계부터 배포까지 자동화를 통해서 효울적이고 빈번하게 진행

**Continuous Integration (CI)**
- 지속적인 통합
- commit code to a shared repo frequently
1. 코드 변경사항을 주기적으로 빈번하게 Merge
	- 코드 충돌 / 병합 시 번거로움 감소
	- 최대한 작은 단위로 빈번하게 진행
2. 통합을 위한 단계 (Merge, Build, Test)의 자동화
	- 개발 생산성 향상 (Merge 충돌 방지) -> **코드 퀄리티 향상**
	- 버그 수정 용이 
	- <img width="500" alt="Pasted image 20221009153926" src="https://user-images.githubusercontent.com/59818703/194897229-6b3dff2f-d532-4380-93f1-2f68fb259177.png">
		


**Continuous Delivery / Deployment (CD)**
- Continuous Delivery : 지속적 제공
	- CI -> Rrepare Release(Stage) -> Deploy Release
	- 최종적으로 배포하기 전 확인 후 수동적 배포
	- <img width="500" alt="Pasted image 20221009154406" src="https://user-images.githubusercontent.com/59818703/194897258-f47f59c7-d255-448e-8711-fc71d13ebf90.png">

- Continuous Deployment : 지속적 배포
	- 배포까지의 과정이 자동화
	- <img width="500" alt="Pasted image 20221009155621" src="https://user-images.githubusercontent.com/59818703/194897796-4c0d2588-bb3f-467a-8e33-3fa1deb8e472.png">

  사진 출처 : https://www.youtube.com/watch?v=0Emq5FypiMM

***
## CI / CD vs DevOps
 - DevOps는 개발+운영 통합 프로세스 속도 높이는 접근 방식 , 문화
 - CI/CD는 지속적으로 통합.테스트.배포 흐름 자동화

***

### 1. GitAction 을 이용한 CI / CD 구축
- **GitAction**
	- Github 저장소를 기반으로 소프트웨어 개발 workflow를 자동화 할 수 있는 도구
	- CI/CD platform / build, test, deployment
	- Automate, customize, and execute your **software development workflows** right in your repository with GitHub Actions
	- Each job will run  Virtual Machine *Runner*
		- Runner : Github에서 호스팅하는 Linux, MacOs,Window 환경 구동 or Self-Hosted Runner

	
	**Workflows**
	- `yaml` file
	- `.github/workflows`
	- Commit / PR / open issue  Events

- GitAction을 이용한 FastAPI 컨테이너 배포
https://github.com/yeoV/fastapi-tutorial

***

### 2. Jenkins 을 이용한 CI/CD 구축


### Jenkins 
소스코드 repo와 다양한 PL에 대해 **지속적인 통합**과 **지속적인 전달** 환경을 구축하기 위한 방식을 제공하는 오픈소스

*"Nightly Build를 망가뜨리지 말라!"*

### Jenkins 구조
<img width="500" alt="Pasted image 20221010141212" src="https://user-images.githubusercontent.com/59818703/194897405-299bbe6a-3ef6-4651-a753-b06434b96a5a.png">
- JNLP (Java Network Launch Protocol)
	- The Java Network Launch Protocol (JNLP) enables an application to be launched on a client desktop by using resources that are hosted on a remote web server.

**Jenkins Master (Server)**
- Jenkins Pipeline 으로 정의된 모든 흐름을 담당하는 컨트롤 서버
- <img width="500" alt="Pasted image 20221010141536" src="https://user-images.githubusercontent.com/59818703/194897426-91989c70-8215-4af4-b329-6a8d222f7abe.png">
- 형상관리에서 Hook을 통해 코드 변경사항 확인
- Agent 에서 독자적인 테스트 환경을 만듬
- Agent의 결과물을 Master가 받아 보고

***
## SonarQube
- docker-compose file (for m1 mac)  
https://github.com/yeoV/study-workspace/blob/main/infra/sonarqube.yaml
- 버그, 코드 스멜, 보안 취악점을 발견할 목적으로 **코드 정적 분석**
- 중복 코딩, 코딩 표준, 유닛 테스트, 코드 커버리지, 코드 복잡도, 주석, 버그 등 보안 취약점 보고서 제공
- SonarLint : IDE 에서 사용 가능한 feedback


***
## GitLab CICD vs Jenkins

**GitLab CI**
- On-prem 방식으로 설치하여 사용
- GitLab CIaks Runner를 직접 호스팅하여 사용
- Gitlab과의 손쉬운 연동
- Auto-Scaling CI Runner 제공 -> 클라우드 일 경우 절감 효과
- 이슈 트래킹 제공
- REST API & GraphQL API 사용 가능
- Jenkins 보다 Plugin 확장성이 낮음

**Jenkins**
- 다양한 IDE, 커스터마이징이 다양
- 많은 사용자들을 보유, 관련 문서가 다양
- 다양한 Plugin을 보유하고 있음
- 규모가 작은 프로젝트의 경우 Build Server를 직접 구매 및 운영해야 하기에
서버를 관리하는데 발생하는 비용이 낭비(각종 방화벽 작업, 서버 관리, 운용 등)될 수 있다.


***
**기타 사항**
* **Ngrok**
	* 외부(Public)에서 로컬에 접속할 수 있게 도와주는 터널링 프로그램
	* 간단한 테스트 용도로 사용 가능 -> 회원 가입시 세션 유지, 1개의 호스트 무료
	* https://ngrok.com/

* 설치
```bash
$ brew install --cask ngrok
```

- 사용 예
```bash
$ ngrok http 8080
```


***
## 3. Jetbrain Space
- docker-compose file (for m1 mac)

https://github.com/yeoV/study-workspace/blob/main/infra/jetbrain-space.yml

