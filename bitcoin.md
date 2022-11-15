# 비트코인 플랫폼 설치

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
</br> -rpcuser : RCP 요청 
