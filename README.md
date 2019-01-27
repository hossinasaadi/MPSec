## Overview

### 프로젝트의 목적
다중 경로 전송 기술인 MPTCP를 활용하여 네트워크 장애 상황에 효과적으로 대처가 가능한 고신뢰 네트워킹을 제공하며, Dashboard를 통한 실시간 모니터링을 통해 사용자가 효과적으로 관리할 수 있도록 한다.

### 핵심 기능
크게 3가지의 핵심 기능이 있다. 첫 번째는 다중 경로 전송을 통해 장애 상황에 네트워크가 끊기지 않게 네트워크의 생존성을 증가해준다. 두 번째는 비슷한 대역폭으로 여러 개의 경로를 통해 데이터를 전송할 시 2개의 대역폭 당 약 1.8배의 속도로 데이터를 전달한다. 마지막으로 IPSec을 통한 Packet 암호화를 통해 목적지까지 데이터가 전달되는 동안 Packet의 내용을 볼 수 없도록 한다.

### 주요 사용지
첫 번째 예시로 군대와 같이 중요한 서버가 있는 네트워크가 끊겨서는 안 되는 장소에서 다중 경로 전송을 통해 만약 하나의 인터페이스가 끊겨도 다른 인터페이스로 데이터를 전송함으로써 네트워크의 생존성을 증가시킬 수 있다. 또한 IPSec을 통해 보안이 중요한 군시설에 Packet의 내용을 볼 수 없도록 할 수 있다. 두 번째 예시로 고화질 영상의 경우 끊기지 않게 빨리 보내져야 하는데 다중 경로 전송을 이용해 여러 개의 인터페이스를 연결하여 끊기지 않게 영상을 전송할 수 있다.

### MPTCP 기본 구조
MPTCP는 전송 계층 프로토콜의 한 종류이며 사용자와 서버 사이의 2가지 이상의 네트워킹 인터페이스를 활용하여 하나의 TCP 스트림을 다중 경로로 전송할 수 있는 프로토콜이다. 만약 둘 중 하나의 경우만 MPTCP 프로토콜이 이용 가능할 경우 기존 TCP 방식을 통해 통신하기 때문에 호환성 또한 뛰어나다고 할 수 있다.

### 구현사항
- ubuntu 16.04 OS에 mptcp 커널 부팅
- network 환경 구축
- ffmpeg를 이용한 스트리밍 환경 구축
- dashboard 구현
- 자동화와 GUI bash 명령어 실행을 위한 각종 스크립트 코드 구현
- packet capture program 구현
- system config output program 구현
- 문서화


<br/><br/>

## Dashboard

### 테스트 베드 환경 설명
PC1과 PC2에 mptcp kernel을 부팅한다. 먼저 Multi Path 동작 확인의 경우, PC2에서 동영상 파일을 PC1으로 가져와 FFMpeg와 FFServer를 통해 WebM 코덱으로 인코딩하여 브라우저에 실시간으로 스트리밍 한다. 1초마다 PC1의 각 인터페이스 대역폭을 측정한다. 측정한 데이터를 Chart JS를 이용해 그래프로 그려준다. Single Path일 때와 Multi Path일 때의 대역폭 현황을 실시간으로 확인할 수 있다. 두 번째로 IPSec 동작 확인의 경우, PC1에서 PC2의 해당 파일을 ftp 프로토콜을 이용해 가져온다. 구현한 Packet Capture Program과 Shell Script 코드를 동작시켜 Packet의 내용을 캡쳐하여 브라우저에 보여준다. IPSec이 동작된 경우 암호화된 Packet을 아닐 경우 해당 데이터의 내용이 그대로 나오는 것을 확인할 수 있다.

### 가상 머신을 이용 (mptcp kernel)

![vm](/md_images/vm.png)

### TestBed 구성 예시

![TestBed](/md_images/testSet.png)

### Single Path

![Single Path](/md_images/sptcp.png)

### Multi Path

![Multi Path](/md_images/mptcp.png)

### IPSec

![IPSec](/md_images/ipsec.png)



<br/>

### [Development description for contribute](/Dev.md)
