# NFS
- 네트워크 파일 시스템
- 네트워크 상에 연결된 다른 컴퓨터의 하드디스크를 내 컴퓨터의 하드디스크처럼 사용하는 것

<img width="350" src="./img/NFS VFS 1.png">

위 그림처럼 IP주소를 이용하여 다른 네트워크의 저장소를 연결

**단점**
- 네트워크 트래픽을 이용해 속도 / 대용량 파일 처리시 문제
- 네트워크가 끊길 시 마운트 된 서버 다죽음



## NAS
- 네트워크로 연결된 외장하드 느낌
- NFS 프로토콜 제공
- 자체에서 백업 / 복구 하드웨어 제공 -> 가용성이 좀 더 높음
- 비쌈

***

# VFS
- Virtual File System
- 실제 파일 시스템이 무엇이냐에 관계없이 공통된 인터페이스로 접근하도록 하는 계층

<img width="350" src="./img/NFS VFS 2.png">

기존에는 위와 같이 각기 다른 파일시스템마다 open, read, write 함수를 구현하였다.

<img width="350" src="./img/NFS VFS 3.png">

하지만, VFS 층을 거치게 하여 특정 파일 시스템에 맞는 함수를 사용하게 한다.
***

### 4가지 Object가 존재
1. super block object
	 각 연결되어 있는 저장 매체나 파티션의 단일 시스템 하나당 하나의 super block 객체 유지.
	 이 object를 통해서 자신이 관리하고 있는 파일 시스템 파악 및 적절한 행동 가능
2. inode object
	요구된 파일들의 정보를 담기 위한 객체. 메타 데이터 정보를 가진 구조체
3. file object
	fseek과 같은 파일 내용이 저장되어 있음
4. dentry object
	task와 inode object를 빨리 연결하기 위한 캐시 개념의 entry