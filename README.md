# TIL
Today I Learn

매일 배운 내용을 기록하고 정리합니다!
<br>
## 12.26
### 블록체인 세미나
- Hyperledger Fabric<br>
- Peer, Node<br>

## 2020.1.1
### 블록체인 공부

- 블록체인<br>
일정 주기로 데이터가 담긴 블록을 생성한 후 이전 블록들에 체인처럼 연결하는 기술<br>
이때, 데이터는 거래 기록이 담긴 장부

- 1세대 블록체인<br>
비트코인 : 사토시 나카모토(가명)가 만든 제 3의 중앙기관이 보증해주지 않아도 개인과 개인이 안전하게 주고받을 수 있는 전자 화폐<br>
네트워크 사이에서 데이터로서만 존재하는 전자화폐 ( 동전이나 지폐처럼 만질 수 없음)<br>
컴퓨터 프로그램을 활용하여 거래장부를 노드 참여자 전체가 공유<br>
->이중지불 방지 -> 분산원장기술<br>

- 2세대 블록체인<br>
이더리움 : 비탈릭부테린이 만든 차세대 스마트계약과 탈중앙화된 어플리케이션 플랫폼<br>
이때, 스마트계약은 어떤 조건을 충족하면 자동으로 다음 절차를 실행하는 것<br>
스마트계약 : 계약의 절차가 미리 작성되어 블록체인 상에 배포된 '코드'를 통해 자동으로 실행, 분산 처리<br>

- 블록체인의 4가지 기술적 특성<br>
탈중앙성<br>
투명성<br>
불변성<br>
가용성<br>

## 2020.1.2
### 1day 1commit

- 1일1커밋 하고싶다.
- 리눅스<br>
.은 현재위치(경로)<br>
..은 상위폴더(부모폴더?)<br>
~은 사용자경로 == home/computer(사용자이름)/<br>
/는 c드라이브(가장 바깥 경로)<br>
cd는 change directory, ls는 list<br>
.파일이름 == 숨겨진 파일 -> -a나 --all 명령어 실행 시, 숨겨진 파일도 보여줌<br>
--help는 flag 옵션 설명해줌<br>
- 도리야 고마워


## 2020.1.6
### 1day 1commit
- 진리언니 출국 전 다같이 밥!!
- 북촌갈비!! 진로!!
## 2020.1.7
## 1day 1commit^^
- Hyperledger Fabric <br>
CA(Certificate Authority) : 네트워크 멤버 및 사용자에게 PKI기반 인증서를 발급하는 인증 컴퍼넌트<br>
-> 각 구성원에게 루트 인증서 하나를 발급하고 각 인증된 사용자에게 하나의 인증서를 발급<br>
실제 구성시) Fabric-CA server/client를 이용하여 인증서 발급<br>
전자서명알고리즘 이용 -> 전자서명 생성은 ECDSA가 빠르고, 전자서명 검증은 RSA가 빠름<br>

- 피어(peer)<br>
분산 원장 데이터의 보증(Endorsement)과 검증(validation)이 이뤄지는 기본적인 노드<br>
원장데이터 및 스마트계약(Smart Contract)이 이뤄지는 블록체인 컴포넌트<br>
다뤄지는 원장은 스마트계약에 의해 생성된 모든 트랜잭션을 변치않는 형태로 만들어진 기록<br>
스마트계약과 원장은 각각 네트워크에서 블록체인의 분산 처리 및 분산 저장하는데 (블록체인화) 사용<br>
피어의 P2P구성으로 인해 다중화 분산원장과 스마트계약이 존재하게되므로 단일장애지점(Single Point of Failure)을 방지하는 수단(분산화)<br>

-  보증과정(Endorsement)<br>
피어는 보증과정을 처리하기위해 체인코드를 실행하여 트랜잭션의 유효성을 검사<br>
이 때,<br>
피어 = ESCC를 실행하는 엔도서<br>
체인코드 = ESCC(Endorsement System Chain Code)<br>
- 검증과정(Validation)<br>
피어는 검증과정을 처리하기위해 체인코드를 실행하여 트랜잭션의 2차검사를 진행 후 원장에 반영<br>
이 때, <br>
피어 = VSCC를 실행하는 커미터<br>
체인코드 = VSCC(Validation System Chain Code)<br>

- 커미터는 ESCC의 결과값 해시값을 가지고 VSCC의 결과값과 비교하여 이중교차검증을 진행<br>

## 2020.1.8
### 1day 1commit
- 블록체인 **블록 연결 방법**<br>
다수의 거래내역이 묶인 블록들이 있다. 이러한 블록들을 **해시**를 이용하여 체인처럼 연결하고, 다수의 사람들이 복사하여 **분산 저장**한다.<br>
- 비트코인에서 블록 생성 속도<br>
블록 하나 당 10분<br>
- **POW(Poof of work)알고리즘(작업증명)**<br>
비트코인의 합의 알고리즘<br>
- wallet(지갑)<br>
암호화폐에서 **개인 키를 관리**하는 프로그램<br>
- 이더리움과 비트코인의 차이점<br>
스마트 컨트랙트의 유무<br>
- 스마트계약(스마트 컨트랙트)<br>
**중개자 없이 계약을 체결하고 수정**할 수 있는 기술<br>
- 게스(Gas)<br>
이더리움에서 코드를 실행시킬 수 있는 가치의 단위<br>
- **CA** 서버<br>
**하이퍼레저에서 신원을 확인**하기 위해 사용되는 것<br>
- **Orderer** <br>
**하이퍼레저에서 블록을 생성**하는 객체<br>
- **Commiting Peer(커미팅 피어) 또는 Committer** <br> 
**하이퍼레저에서 트랜잭션의 검증**을 진행하는 객체<br>

## 2020.1.12
### 1day 1commit
< 블록체인 > <br>
- 분산 원장<br>
   : 블록체인을 구성하는 가장 중요한 요소들 중 하나<br>
	 : 블록체인을 탈중앙화 시스템으로 만들어주는 핵심 기술<br>
	 : 블록체인에 참여하는 모든 사람이 동일한 원장을 소유&관리<br>
	 : 해시화되어 수정이 불가능 -> 불가변성<br>
- 스마트 컨트랙트<br>
  : 스마트 컨트랙트를 통해 분산 원장에 정보를 기록하고, 불러오기<br>
  : 프로그래밍 가능<br>
- 분산 애플리케이션 : 스마트 컨트랙트를 편리하게 사용하기위해 개발되는 프로그램<br>
- 합의 알고리즘<br>
비트코인, 이더리움)<br>
PoW(Proof of Work) : 암호화된 퍼즐의 답을 가장 먼저 찾아내는 노드의 블록을 최신 블록으로 업데이트<br>
하이퍼레저 패브릭)<br>
:	보증 정책 확인<br>
:	트랜잭션을 정해진 순서에 맞춰 정렬<br>
:	정렬된 트랜잭션의 유효성 검증 후 최신 블록 업데이트<br><br>
< 하이퍼레저 패브릭 ><br>
하이퍼레저 = 블록체인 플랫폼 (by 리눅스)<br> 
허가형 프라이빗 블록체인으로 퍼블릭 블록체인(비트코인, 이더리움)과는 달리 MSP(Membership Service Provider)라는 인증 관리 시스템에 등록된 사용자만이 하이퍼레저 패브릭 블록체인에 참여 가능<br> 
채널(channel) : 참여자들 간의 프라이버시 강화<br>
**하이퍼레저 프레임워크** : 분산원장, 스마트 컨트랙트, 합의 알고리즘 등 블록체인에 대한 원천적인 기술을 개발하는 프로젝트<br>
**하이퍼레저 툴** : 블록체인 시스템의 성능 측정, 운영, 개발을 쉽게 할 수 있도록 도와주는 툴을 개발하는 프로젝트<br>
원장 :<br> 
**월드 스테이트** : 원장의 현재 상태<br>
**블록체인** : 원장의 전체 기록<br>
체인 코드 : 기존의 스마트 컨트랙트와 같이 원장에 데이터를 읽고 쓰기 위해 사용될 수 있음<br>
시스템 체인 코드 : 블록체인 시스템 설정<br>
합의 과정 : 트랜잭션의 생성부터 새로운 블록 생성까지 모든 과정을 통칭<br>
**데이터 처리 과정 :  Execute -> Order -> Validation**<br>
:	실행(Execute) 단계 : 트랜잭션을 실행하고 결괏값을 검증<br>
:	정렬(Order) 단계 : 실행 단계에서 검증이 끝난 트랜잭션을 취합하여 순서에 맞게 정렬한 후 블록을 생성하는 작업을 수행<br>
: 검증(Validation) 단계 : 블록에 포함된 모든 트랜잭션에 대한 결괏값 검증을 수행하고, 각종 디지털 인증서 등을 확인한 후 이상이 없을 시 최신 블록을 업데이트<br>
특징 : <br>
:	프라이버시와 기밀성<br>
:	작업 구간별 병렬 처리<br>
:	체인 코드<br>
:	모듈화된 디자인<br>

**Peer** <br>
     : 하이퍼레저 패브릭 블록체인을 구성하는 네트워크 노드 중 하나<br>
     : 분산원장과 스마트 컨트랙트(=체인 코드)를 관리<br>
     : 참여자는 peer를 통해서만 분산원장과 체인코드에 접근 가능<br>
(한번 기록된 데이터는 위/변조가 불가능한 분산 원장에 존재)<br>
분산원장에 데이터를 기록하거나 읽기 위해서 체인 코드 필요<br>
Peer에 설치된 시스템 체인코드 :<br>
:	**QSCC(Query System ChainCode)** : 블록체인의 저장된 데이터를 읽어옴<br>
:	**ESCC(Endorsement System ChainCode)** : 보증 정책을 담당<br>
:	**VSCC(Validation System ChainCode)** : 블록을 검증<br>
:	**CSCC(Configuration System ChainCode)** : 채널 설정 시 사용<br>
:	**LSCC(Lifecycle System ChainCode)** : 체인코드의 설치부터 인스턴스화까지 모든 과정 수행<br>
QSCC, CSCC, LSCC는 사용자에 의해 CLI 명령어로 실행<br>
ESCC – Endorsing peer(트랜잭션의 보증을 담당) <br>
VSCC – Committing peer(블록에 대한 검증을 담당)<br>

## 2020.1.8
### 1day 1commit

블록체인 참여자는 체인코드를 통해서 분산원장에 데이터를 기록하고 읽어온다.<br>
대부분의 경우는 비즈니스 모델에 맞는 분산 애플리케이션과 함께 개발되어 사용<br>
**분산 애플리케이션** <br>
분산 환경에서 비즈니스 거래 등을 편리하게 해주기 위해 사용되는 애플리케이션<br>
다양한 종류의 SDK(Software Development Kit)제공<br>
SDK를 통해 트랜잭션을 생성하고 체인코드 함수를 불러옴<br>
peer 네트워크에 설치된 체인코드 실행 가능<br>
**체인코드**<br>
- 읽기(query)-5단계, 쓰기(write/update)-9단계<br>
Ex) **읽기** - A는 peer 네트워크의 peer1과 연결<br>
1. 분산 애플리케이션은 분산원장에 접근하기 위해서 사용자A의 인증서를 이용해 인증 과정을 통과한 후 peer1과 연결<br>
2. 정상적으로 연결되고, 분산 애플리케이션은 peer1에 설치된 체인코드의 query 함수 호출<br>
3. peer1은 요청받은 체인코드의 query 함수를 실행하여 자신의 로컬 저장소에 저장되어있는 분산원장의 데이터를 분산 애플리케이션에 전달<br>
-> Query 함수 실행을 요청받은 peer1 외 다른 peer는 동작 X<br>
Ex) **쓰기** - A는 peer 네트워크의 peer1과 연결<br>
위의 과정과 동일 + <br>
1. peer1이 트랜잭션 입력값에 대한 결과값과 보증 정책을 확인<br>
2. 트랜잭션 실행 결과값이 정상적이고 peer1의 보증조건을 충족시키면 peer1은 결과값과 함께 peer1의 디지털 인증서를 분산 애플리케이션에 전달<br>
3. 분산 애플리케이션은 트랜잭션 결과값과 peer1의 디지털 인증서와 함께 트랜잭션을 orderer 노드로 전송<br>
4. Orderer는 수신한 트랜잭션을 순서에 맞게 정렬하여 블록체인의 최신 블록을 생성, 생성한 블록을 자신이 속한 네트워크의 모든 peer에게 전달<br>
-> Orderer는 트랜잭션을 순서에 맞게 정렬하여 블록을 생성 (트랜잭션의 내용 확인 or 검증X)<br>
5. 모든 peer는 해당 블록에 포함된 모든 트랜잭션에 대한 결과값과 인증서를 검증<br>
6. 검증에 문제 없을 시, 로컬 저장소에 저장된 분산원장 업데이트<br>
7. peer는 블록 업데이트 결과를 분산 애플리케이션에 알려줌<br>
**보증 정책(Endorsement Policy)**<br>
- 트랜잭션이 블록에 포함되려면 peer의 허가를 받아야함 <br>
- 보증 정책은 트랜잭션을 생성하는 클라이언트(분산 애플리케이션)와 peer간에 작용<br>
- 트랜잭션 보증과 블록에 대한 검증을 하는 peer노드를 각 조직마다 소유<br>
→ 어느 한 조직에서 분산원장에 대한 기록을 독단적으로 변경/조작 X<br>
→ 탈중앙화 네트워크로 만들어주는 핵심 요소<br>
- 채널을 통한 연결 (서로 다른 채널에 있는 peer간에는 서로 다른 분산원장에 대한 정보 공유X)<br>
**CSCC**<br>
→ 채널 생성<br>
→ Genesis block 생성(채널 구성원, 채널 정책, 각 peer의 역할)<br>
**분산원장**<br>
→ World state : 현재 상태를 나타냄<br>
→ 블록체인 : 원장의 생성 시점부터 현재까지의 사용기록<br>
- World state<br>
: 데이터베이스 형태로 블록체인과 분리되어 구축(데이터의 기록, 수정, 읽기 등이 빈번하게 발생하기때문)<br>
: 저장된 데이터는 합의 과정에 의해 블록체인에 포함되기 전까지 체인코드를 통해 조회/변경/삭제 가능<br>
: 합의에 의해 결정된 블록 및 블록체인은 절대 수정 X<br>
: 블록체인은 데이터 요청이 거의 X, append-only 방식의 저장이 목적이기 때문에 파일 시스템 형태로 저장<br>
- Version : World state가 업데이트될 때마다 증가<br>
→ 트랜잭션의 version 값과 World state의 version값이 같아야 트랜잭션 내용 업데이트<br>
- 블록체인<br>
: 블록들이 합의 과정을 마친 후 암호학적 기법을 통해 생성된 순서대로 연결되어 저장<br>
- 블록 : Header, Data, Metadata 로 구성<br>
→ Header : 현재 발생하고 있는 트랜잭션에 대한 해시값, 이전 단계에서 생성된 블록의 해시값 포함<br>
: Block number : 0부터 시작하여 합의 과정에 의해 블록이 생성될 때마다 숫자가 1씩 증가<br>
: Current block hash : 트랜잭션의 해시값<br>
: Previous block hash : 이전 블록에 대한 해시값<br>
→ Data : 트랜잭션<br>
: Header : 트랜잭션의 version 정보와 트랜잭션이 실행되는 체인코드의 이름 등 명시<br>
: Signature : 트랜잭션 생성자의 Identity 관련 디지털 인증서 정보<br>
: Proposal : 체인코드에 들어가는 트랜잭션의 입력값이 저장<br>
: Response : 트랜잭션 처리 결과값을 Read/Write set 형태로 변환<br>
: Endorsement : 트랜잭션을 보증해 준 peer의 Identity 정보가 포함<br>
: Chain name : 체인코드 구분<br>
→ Metadata : 블록 생성자의 Identity 정보, 블록에 포함되어있는 Transaction 보증 여부<br><br>
**Gossip 프로토콜**<br>
: Leader peer를 대표로 orderer와 통신<br>
**Identity**<br>
: PKI 기반의 디지털 인증서 : 네트워크 노드들의 서로 신원 확인 (peer, orderer, client)<br>
**PKI** : 디지털 인증서를 안전하게 제공/생성/관리<br>
- 디지털 인증서<br>
- 공개키/비밀키<br>
- CA(Certificate Authority)<br>
- Certificate Revocation List<br>
**디지털 인증서**<br>
: Certificate Serial Number : 각각의 인증서를 구분하는 고유의 시리얼 번호를 포함하는 필드 <br>
: Signature Algorithm Identifer for CA : 인증서의 위/변조를 방지하기위해 사용되는 암호화 알고리즘 <br>
: Issuer Name : 인증서를 발급한 CA의 정보<br>
: Validity Period : 인증서의 유효기간의 시작일, 만료일<br>
: Subject Public Key Information : 인증서 사용자의 공개키<br>
: Etension(s) : 인증서의 추가적인 정보와 정책에 관한 내용<br>
: A Signature : CA의 디지털 인증서 정보<br>
**공개키/비밀키**<br>
: 신원 인증/데이터 암호화 만족<br>
: 공개키를 이용해 암호화를 수행 → 원하는 상대에게만 데이터 공개 가능<br>
: 비밀키를 이용해 암호화를 수행 → 신원 인증<br>
**CA(Certificate Authority)**<br>
: MITM(중간자 공격 = Man in the Middle Attack)
**CRL(Certificate Revocation Lists)**<br>
: 폐기된 인증서에 대한 목록<br>
: CA가 관리<br><br>
**MSP(Membership Service Provider)** : peer, orderer, Fabric-CA, Admin 등의 역할과 소속, 권한 등 정의<br>
- Local MSP<br>
: 어떤 노드가 peer, orderer,client인지 정의<br>
: client가 Admin인지 일반 유저인지 노드별 권한 정의 가능<br>
- Channel MSP<br>
: 채널 구성원들에 대한 멤버십 정의와 권한을 부여<br><br>
**Orderer** : 블록을 생성하여 peer에게 전달<br>
1. 트랜잭션 제출<br>
 : 분산 애플리케이션이 트랜잭션 보증을 담당하는 Endorsing peer에게 트랜잭션을 제출<br>
 : Endorsing peer들은 Proposal 값을 바탕으로 체인코드를 시뮬레이션<br>
 : 올바른 결과값이 나오면 Endorsing peer는 자신의 Identity를 이용해 서명한 디지털 인증서와 Read/Write set를 함께 분산 애플리케이션에 전송<br>
2. 블록 패키징<br>
 : 위의 제출 과정에서 제출한 트랜잭션을 orderer가 수집하여 순서대로 정렬하여 새로운 블록 생성
3. 검증<br>
 : orderer가 생성한 최신 블록을 각 조직의 peer들에게 전달, 최신 블록을 전달받은 peer는 해당 블록이 올바르게 생성됐는지 검증<br>

## 2020.1.16
### 1day 1commit
**리눅스 명령어**
- cd(change directory)<br>
: 디렉토리 이동<br>
- .. <br>
: 이전 폴더로<br>
- ls(list)<br>
: 목록 폴더 보기<br>
- mkdir(make directory)<br>
: 디렉토리 생성<br>
- vi (vi editor)<br>
: i -> 입력 모드<br>
: q -> 종료<br>
: wq -> 저장 후 종료<br>
- rm(remove)<br>
: 삭제<br>
- --help<br> 
: 도움말<br>

## 2020.1.30
### 1day 1commit
**Kafka와 Solo 비교**
- Kafka<br>
: 데이터 피드를 관리하는 분산형 스트리밍 플랫폼(A distributed streaming platform)<br>
: Producer, Consumer, Broker로 구성<br>
**Producer** : 특정 topic의 메시지를 생성하고, 해당 메시지를 broker에게 전달<br>
**Broker** : topic을 기준으로 메시지를 관리(분류)<br>
**Consumer** : 구독하는 topic의 메시지를 직접 가져감<br>
: Kafka는 여러개의 broker들로 이루어진 클러스터라고 할 수 있..다..<br>

- Solo<br>
: 쉽게 이용되도록 만들어진 극히 간단한 서비스 <br>
: 싱글 프로세스로 구성<br>
: 사실상 합의라는 것이 없음<br>
*테스트용으로 생각할 수 있다!!*

## 2020.2.3
### 1day 1commit
- 기술동향 세미나!!!!!!!!!!!! 
**<SPRI=소프트웨어정책연구소>**
- 자율형 IoT 기대감 증대
- 교육을 위한 인공지능
- 금융권 AI 투자 본격화
- 의료 빅데이터 개방
- 지능형 물류 로봇 시장의 성장
- xAI 기술 현실화
- 모바일 폼팩터의 혁신
요즘 폼팩터 혁신은 접이식 스마트폰<br>
- 에너지 산업의 SW융합
- 클라우드 게임 시장의 선점 경쟁
우리나라는 5G망 보급이 최고<br>
- 언택트(untact) 서비스 영역 확대
언택트 서비스는 비대면 서비스를 칭함


## 2020.2.5
### 1day 1commit
- 블록체인 세미나<br>
Hyperledger에서 ..<br>

**CA** : peer가 어떤 채널에 접속할 수 있는 권한을 부여 하는 인증서 관리<br>
**Orderer** : 트랜잭션을 블록화<br>
**Peer** : 블록체인 네트워크를 구성하는 요소<br>

우리는? → docker로 local에서 실행<br>
 
peer를 local이 아닌 외부로 보내려면?<br>
1. config.yaml 실행<br>
2. 접속할 채널의 인증서 발급 받음 (cryptogen.sh)<br>
3. 채널 생성<br>
4. 채널에 가입<br>

하나의 IP에서 여러개의 Peer 존재 가능<br>
외부의 peer가 채널에 접속하길 원하면? 그 peer의 IP주소를 알고있어야하고 이용할 수 있게 허용 가능<br>

peer를 추가할 때마다 네트워크 구성을 수정해야해 → 근데 처음부터 잘 구성하면 돼<br>


- 스포츠산업 창업준비

## 2020.2.6
### 1day 1commit
- 스포츠산업 경진대회 발표 및 피드백


## 2020.2.8
### 1day 1commit
- 통신(communication) : 소식을 전하는 것(정확한 사람에게, 정확한 시간에 맞춰, 다른사람이 모르게)<br>
- HTTP(Hyper Text Transfer Protocol)통신<br>
: Hyper Text(ex. HTML)를 전송하기위한 프로토콜<br>
* 요청(request)과 응답(reponse)으로 이루어짐<br>
1. 클라이언트가 서버에 요청<br>
2. 서버가 응답<br>
3. 사용자에게 보여줌<br>
→ 연결 종료(connection close)<br>
* 단방향적 통신 → 서버의 부하를 줄여 다른 접속을 원활하게 처리하기 위함 (DDOS공격 방지)<br>
* 하지만 누군가 네트워크에서 신호를 가로챈다면 내용이 노출되는 보안상의 문제 발생(ex. id, password)<br>
- HTTPS(HyperText Transfer Protocol over Secure Socket layer)<br>
: 보안이 강화된 HTTP프로토콜 (완전히 새로운 프로토콜X) <br>
: 증명서를 통해 서버 또는 클라이언트의 신원을 확인하고, 데이터를 암호화, 인증, 안정성을 보호할 수 있는 프로토콜<br>
: HTTP통신의 소켓연결부분을 SSL로 대체한 것<br>
: HTTP는 직접 TCP와 통신하지만, HTTPS는 SSL과 통신하고, SSL이 TCP와 통신 → 이는 성능이 조금 더 느리지만, 보안이 중요하기 때문에 사용 권장<br>
* SSL : 일종의 보안 계층<br>
+ SSL이 보편화되면서 국제표준화기구(IETF)에서 이를 관리하기 시작했고, TLS로 이름 변경(== SSL과 TLS는 같다고 봐도 무방, 실제로 SSL이 사용됨)<br>
* SSL인증서 목적<br>
1. 클라이언트가 접속하련느 서버가 신뢰할 수 있는 사이트인지 보장<br>
→ 사이트가 CA로부터 SSL인증서를 발급받았는지 확인<br>
2. SSL통신에 사용할 공개키를 클라이언트에게 제공<br>


## 2020.2.9
### 1day 1commit
- 블록체인 통신<br>

## 2020.2.11
### 1day 1commit
- 하이퍼렛저 체인코드 공유?<br>

## 2020.2.12
### 1day 1commit
- 블록체인 세미나<br>
**우분투에서 두개의 Virture Box(가상컴퓨터)를 만들어 서로의(자기 컴퓨터 안에서의) 채널에 조인**
- 블록체인에서 수정과 삭제는?<br>
: 월드스테이트에서 일어남<br>
+ 근데 누가 요청하고 누가 검증하는지?<br>
- 월드 스테이트는 현재 상태......<br>

- HTTP통신과 블록체인통신 비교<br>
: HTTP통신에서 hand shaker 공부 더 해오기<br>

## 2020.2.13
### 1day 1commit
- HTTP통신에서 사용하는 TCP 연결 3 way handshake방법<br>
클라이언트와 서버 또는 P2P Socket통신 등, 네트워크를 사용한 통신시 TCP통신을 많이 사용<br>
TCP통신을 위한 네트워크 연결은 3way handshake라는 방식으로 연결<br>

먼저, 클라이언트는 Closed상태, 서버는 LISTEN상태<br>
1. 클라이언트가 서버에게 연결을 요청하기위해 SYN데이터를 보낸다.<br>
2. 서버는 LISTEN상태였다가 SYN데이터를 받고 SYN_RCV상태로 변경된다.<br>
3. 상태가 변경된 후, 요청을 정상적으로 받았다는 대답 ACK와 클라이언트도 포트를 열어달라는 SYN을 보낸다. (ACK+SYN) <br>
위의 과정이 정상적으로 종료되면 서로의 포트가 ESTABLISHED되면서 연결된다.<br>

- 상태<br>
**Closed** : 닫힌 상태<br>
**LISTEN** : 포트가 열린 상태로 연결 요청 대기 중<br>
**SYN_RCV** : SYNC요청을 받고 상대방의 응답을 기다리는 중<br>
**ESTABLISHED** : 포트 연결 상태<br>

## 2020.2.14
### 1day 1commit
**<객체지향>**<br>
- 다형성 (in JAVA)<br>
: 여러가지 형태를 가질 수 있는 능력 == 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 하는 능력<br>
: 하나의 객체를 여러가지 타입으로 선언할 수 있다?<br>
: 하나의 클래스가 다양한 동작 방법을 가지고 있다?<br>
: 상속과 인터페이스를 통해 주로 이루어짐<br>
내가 코드보면서 이해한 다형성은...<br>
- **상속**에서<br>
1. A class(x 메소드)와 B class(y 메소드)가 있다.
2. B class가 A class를 상속받았다.
3. 그리고 다음과 같이 main함수에서 실행하였다.
: A obj = new B(); (== 클래스 B의 데이터 타입을 클래스 A로 인스턴스화한것)<br>
: obj.x(); -> 실행<br>
: obj.y(); -> 실행되지않음<br>
: B class의 y함수를 실행하려면 B obj = new B(); 로 선언해야한다. obj.y(); -> 실행됨<br>
- **오버라이딩 이용**에서<br>
1. A class(x 메소드)와 B class(x 메소드, y 메소드)가 있다.
2. B class가 A class를 상속받았다.
3.  그리고 다음과 같이 main함수에서 실행하였다.
: A obj = new B();<br>
: obj.x(); -> B class의 x 메소드가 실행된다.<br>
**이는 하위클래스를 상위클래스로 인스턴스화 했을때의 경우이당**<br>
- **인터페이스**<br>
1. A Interface(x 메소드)와 B Interface(y 메소드)가 있다.
2. S라는 class가 A,B 인터페이스를 상속받았다.
3. 그리고 다음과 같이 main함수에서 실행하였다.
: S obj = new S();<br> 
: A obj = new S();<br>
: B obj = new S();<br>
: 이때 A,B인터페이스의 메소드가 실행되는 경우는 두 인터페이스를 상속받은 S class로 선언했을때이다!? <br>

말로 설명하려니까 어렵넹 잘하고있는건지 모르겠지만 다음번에는 캡슐화에대해서 공부할거다<br>
c언어로 행렬의 곱 nXn도 풀어봐야겠다<br>

## 2020.2.15
### 1day 1commit
- 캡슐화<br>
: 객체의 속성(data fields)과 행위(메서드, methods)를 하나로 묶고, 실제 구현 내용 일부를 외부에 감추어 은닉한다.<br>
: 이 말을 자판기로 예를 들어 보면<br>
: **속성(Attribute>**은 자판기에 필요한 자료<br>
1) 음료수목록<br>
2) 음료수의가격<br>
3) 사용자가 선택한 음료수<br>
4) 사용자가 투입한금액<br>
: **행위(Method)**는 자판기내부적으로 일어나는 행위 그리고 외부적으로 보이는 행위 모두 포함<br>
1) 해당음료수가 있는지 확인<br>
2) 잔액확인<br>
3) 음료수 가져오기<br>
4) 잔액 반환<br>
응집도는 강하게.. 결합도는 약하게... 메모...<br>

## 2020.2.16
### 1day 1commit
- RSA
초기부터 지금까지 **치환**(:평문의 원소를 다른 원소로 사상시키는 것)과 **순열**(:원소들의 순서를 재배치하는 것)을 이용한 관용 암호(=대칭 암호)를 사용하였다.<br>
RSA는 수학적인 함수를 기본으로 하고 두개의 독립된 키를 사용하는 공개키 암호(비대칭 암호)이다.<br>
1. 기밀성을 보장한다.
2. 키 분배 시스템을 이용한다.
3. 인증을 제공한다.
- 비대칭 알고리즘의 키는 쌍(공개키,개인키)으로 이루어져있는데, 하나가 암호화에 쓰이면 다른 하나는 복호화에 쓰인다.<br>
철수가 영희에게 데이터를 보내려고 가정한다.<br>
이때 철수는 철수의 개인키와 공개키, 그리고 영희의 공개키를 가지고 있다.<br>
그래서 철수는 자신의 개인키로 평문을 암호화하거나 영희의 공개키로 암호화하여 영희에게 전송할 수 있다.<br>
또한 공개키 구조를 중복 사용해보면,<br>
철수의 개인키로 암호화를 하고, 영희의 공개키로 또 암호화를 한다. 이때 영희는 영희의 개인키와 철수의 공개키를 가지고 있기 때문에 복호화가 가능하다.<br>
**인증과 기밀성을 모두 제공한다.**<br>

**관용 암호(대칭 암호) vs 공개키 암호(비대칭 암호)**<br>
관용 암호<br>
- 암/복호화에 같은 키 사용
- 알고리즘과 키 공유
- 키는 비밀로 유지<br>
공개키 암호<br>
- 암/복호화에 다른 키 사용
- 알고리즘과 키를 공유하지 않고, 키의 쌍을 보유
- 두 개의 키중 하나만 비밀로 유지


## 2020.2.18
### 1day 1commit
**HTTP통신**<br>
http통신에 있어서 클라이언트와 서버가 요청하고 응답하는 방식<br>
- 3-way-handshake
:TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정<br>
1. Client와 Server는 CLOSED상태
2. Client가 Server에게 접속을 요청하는 SYN플래그 전송
3. Server는 Client에게 확인했다는 SYN+ACK플래그 전송
4. Client가 Server에게 확인했다는 ACK플래그 전송<br>
**양쪽 모두 데이터를 전송할 준비가 되었다는것을 보장**<br>

- 4-way-handshake
: 세션을 종료하기위해 수행되는절차<br>
1. Client와 Server는 ESTABLISHED상태
2. Client가 Server에게 연결을 끊자는 FIN플래그 전송
3. Server는 Client에게 일단 확인 메시지 ACK플래그를 보내고 자신의 통신이 끝날때까지 기다림
4. 통신이끝나면 Server가 Client에게 FIN플래그 전송
5. Client가 Server에게 확인했다는 메시지 ACK플래그를 보내고 연결종료<br>
: 만약 클라이언트에 뒤늦게 도착하는 패킷이 있다면?<br> 데이터 유실<br>
이를 대비하여 클라이언트는 서버로부터 FIN플래그를 수신해도 일정시간(디폴트 240초>동안 세션을 남겨놓고 잉여패킷을 기다림(TIME-WAIT)<br>

## 2020.2.19
### 1day 1commit
