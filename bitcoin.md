# 비트코인 플랫폼 설치

콘테이너 실행 안될 때 docker start bitcoin <<

 비트코인 도커 이미지 다운로드

```
docker pull pjt3591oo/bitcoin:0.17.01
```

![image](https://user-images.githubusercontent.com/52357235/201944614-2e169738-72de-4132-9a66-63e5ee0238cd.png)

 비트코인 도커 이미지 실행 과 동시에 접속

```
docker run -it --name bitcoin pjt3591oo/bitcoin:0.17.01 /bin/bash
```

![image](https://user-images.githubusercontent.com/52357235/201945211-5e8d36e4-b4d5-435b-bb12-43497bc535f5.png)

위 커맨드로 접속하여 exit으로 종료를 하면 컨테이너까지 같이 종료된다.
</br> 그러는걸 방지하기 위해 docker start bitcoin 으로 컨테이너 실행하고 exec 로 실행시킨다.

```
docker exec -it bitcoin /bin/bash
```

비트코인 디렉토리를 ls 명령어로 리스트를 보겠습니다.

![image](https://user-images.githubusercontent.com/52357235/201946048-a7db7813-aef2-4bee-9cd4-b9448a0f200b.png)

비트코인의 환경변수 $HOME을 확인해보겠습니다.

```
echo $HOME
```

![image](https://user-images.githubusercontent.com/52357235/201946777-5e31ffe1-d689-45e8-ae10-8e3b9f90bff2.png)

# bitcoin 실행

![image](https://user-images.githubusercontent.com/52357235/201947152-b72113d0-dee9-4ea0-a06c-3d59980e3078.png)

start.sh을 실행시키면 비트코인이 실행됩니다. 종료하려면 ctrl + c로 종료하면 됩니다.

![image](https://user-images.githubusercontent.com/52357235/201947457-263a6ce5-72f0-44a9-b7e4-e00823657b96.png)

start.sh 내부 옵션을 살펴보겠습니다.
</br> -regtest : main or test network와 연결되지 않음.
</br> -server : RCP 요청 허용
</br> -rpcuser : RCP 요청 시 필요한 유저 이름
</br> -rpcpassword : RCP 요청 시 필요한 비밀번호
</br> -rpcport : RCP 요청 시 사용할 포트 번호
</br> -port : 노드끼리 연결 시 사용되는 포트 번호
</br> --datadir : 블록과 같은 데이터가 저장되는 위치(.bitcoin)
</br> conf : 설정 파일 경로
</br> daemon : 노드를 백그라운드에 띄워줌

Bitcoin 수동 실행 

```
mkdir test
bitcoind -regtest -rpcuser=test -rpcpassword=test -server -rpcport=12345 --datadir=$PWD/test
```

![image](https://user-images.githubusercontent.com/52357235/201949028-cda9f97d-8df5-4795-b666-4de3a8e8f632.png)

비트코인 멀티노드 운영
1. Data 디렉토리 생성: node1, node2
2. Docker bitcoin container에서 나간다.
3. 2개의 터미널에서 docker bitcoin container에 각 접속한다.
4. node1, node2를 실행한다(rpcport, port, datadir은 다르다).

![image](https://user-images.githubusercontent.com/52357235/201949865-bfa4da85-2d6b-4057-b0d9-d37e4856f114.png)

멀티 노드를 생성한다.

![image](https://user-images.githubusercontent.com/52357235/201950504-a84410f9-722e-40d6-9a7d-cfb931f9dc43.png)

bitcoin-cli 기능
- 계정생성
- 트랜잭션 발생
- 잔액 조회
- 피어 연결

bitcoin-cli 실행 - 명령어
사용방법

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=/bitcoin/node1 [명령어]
```

node1 에 지갑 계정생성

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 getnewaddress
```

![image](https://user-images.githubusercontent.com/52357235/201951830-c0042238-8f0e-4cbb-ae2c-e5f401be771a.png)

bitcoin-cli 실행 - 계정생성[lable] 추가 

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 getnewaddress 2N2kdga6
```

![image](https://user-images.githubusercontent.com/52357235/201952256-a1c92ee1-fe7c-4f8d-ad55-cc6b8cf8bee0.png)

bitcoin-cli 실행 - 라벨주소 확인

에러 발생 : -deprecatedrpc=accounts

![image](https://user-images.githubusercontent.com/52357235/201952360-90e920a1-89ce-4218-ba08-b9261002d6b9.png)

오류를 해결하기 위해 -deprecatedrpc=accounts 명령어 실행
**명령어 실행할 때는 node1의 노드를 중지하고 명령어 입력**

```
bitcoind -regtest -rpcuser=test -rpcpassword=test -server -rpcport=12345 -port=12346 -datadir=$PWD/node1 -deprecatedrpc=accounts
```

![image](https://user-images.githubusercontent.com/52357235/201952806-c75785fd-0eb8-478b-807d-5d5a88039cc7.png)

이제 라벨 주소를 다시 조회하겠습니다.

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 listaccounts
```

![image](https://user-images.githubusercontent.com/52357235/201954579-8ef5b745-93c1-44f9-9131-9bf407738a78.png)

bitcoin-cli 실행 - 블록생성

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 generate [생성할 블록 개수]
```

![image](https://user-images.githubusercontent.com/52357235/201954996-4aefbe1b-a5b9-4153-a0bb-00c706b22a80.png)

지갑에 블록이 추가되었다고 로그도 뜨시는걸 확인할 수 있습니다

![image](https://user-images.githubusercontent.com/52357235/201955120-dd0795fb-da62-4861-8f85-906f5667b3a0.png)

bitcoin-cli 실행 - 계정잔액 확인

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 listaccounts
```

![image](https://user-images.githubusercontent.com/52357235/201955327-13557fd3-64ea-4370-9c3a-0e1060f1b573.png)

- 블록을 생성하였지만 보상이 주어지지 않았다.
- Bitcoin은 101번째 블록부터 보상이 주어진다.

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 generate 100
```

![image](https://user-images.githubusercontent.com/52357235/201955927-29787740-e16e-4aaa-a8c4-9c43e1a2fdde.png)

블록 100개 생성하여서 초기보상 50bitcoin이 생성된걸 listaccounts로 확인할 수 있습니다.

![image](https://user-images.githubusercontent.com/52357235/201956014-b96d2c92-43e7-4d6c-9e8a-3215147f7f53.png)

블록 개수를 조회 해보겠습니다.

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 getblockcount
```

![image](https://user-images.githubusercontent.com/52357235/201956385-39ea3046-2390-43d6-a5e4-da9bf013aacd.png)

블록 해시를 조회 해보겠습니다.

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 getblockhash [블록 번호]
```

![image](https://user-images.githubusercontent.com/52357235/201956719-3906896a-a644-4310-b8de-fa410530e7bb.png)

블록 정보를 조회 해보겠습니다.
tx는 트랜잭션이다.

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 getblock [블록 해시]
```

![image](https://user-images.githubusercontent.com/52357235/201957052-0cddf0bd-304f-47ad-b6fa-449377624ca4.png)

라벨로 지갑주소 조회하겠습니다.
라벨은 listaccounts 명령어로 조회합니다.

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 getaccountaddress [라벨 이름]
```

![image](https://user-images.githubusercontent.com/52357235/201957896-21a4a537-3671-4ecf-a6e1-43aba0d32dc6.png)

비트코인 전송을 해보겠습니다.
라벨을 입력한 주소에 보내겠습니다.

```
bitcoin-cli -regtest -rpcuser=test -rpcpassword=test -rpcport=12345 -rpcconnect=127.0.0.1 -datadir=$PWD/node1 sendtoaddress [받는 주소] [전송량]
```

![image](https://user-images.githubusercontent.com/52357235/201959430-41fe4953-9484-4bbb-a2c2-327e11d0bf0b.png)

비트코인 전송읋 확인하겠습니다.
- 새로운 블록이 생성되어야 비트코인 전송 트랜잭션이 처리가 되어진다.

![image](https://user-images.githubusercontent.com/52357235/201960122-ec94066d-3737-4b73-994c-f388b9521c78.png)

비트코인 콘테이너의 네트워크 주소 확인하자

<img width="804" alt="image" src="https://user-images.githubusercontent.com/52357235/202600553-57c564ca-7c86-4ede-a4e6-548203a5d9f2.png">
