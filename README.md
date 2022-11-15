# docker
using docker

도커 이미지 파일 검색

docker search [image name]

<img width="794" alt="image" src="https://user-images.githubusercontent.com/52357235/200452094-2323cced-7a84-49c8-98d4-b8e553a54dd4.png">

도커 이미지 설치

docker pull [image name]

<img width="564" alt="image" src="https://user-images.githubusercontent.com/52357235/200452203-1b058ac0-17ee-4698-8620-1c1f76015f0b.png">

도커 이미지 삭제

docker rmi [image name]

<img width="669" alt="image" src="https://user-images.githubusercontent.com/52357235/200452266-2dea25ef-7b10-4d20-b59d-ce4e18f331bf.png">

컨테이너까지 같이 지우고 싶으면

docker rmi -f [image name]

도커에 다운받은 이미지 검색

docker images

<img width="353" alt="image" src="https://user-images.githubusercontent.com/52357235/200452335-c7c3146c-2082-49fd-9e56-025f3d64ea84.png">

docker images -a 

<img width="420" alt="image" src="https://user-images.githubusercontent.com/52357235/201247203-fb553e57-42c5-49bc-bcd1-827e773f56e6.png">

시스템 관리자 도커 실행 관리

service docker restart

service docker stop

service docker start

컨테이너 생성

docker run [option] [image name]

<img width="323" alt="image" src="https://user-images.githubusercontent.com/52357235/200453237-ea16d251-eb9c-4322-b14f-488b02db975d.png">

-d : Container 유지
-p : 서버가 사용할 포트포워드(호스트 포트: 컨테이너 포트)
-e : 이미지에서 설정할 옵션

컨테이너 조회

docker ps 

<img width="864" alt="image" src="https://user-images.githubusercontent.com/52357235/200456413-56cebd34-abbf-49f9-bf4a-544ae4f71bc4.png">

-a : 
docker ps -a 

<img width="838" alt="image" src="https://user-images.githubusercontent.com/52357235/201247060-f818c9a5-fa16-4003-82d0-b71116fe7ae6.png">

httpd 설지 후 컨테이너 생성

<img width="451" alt="image" src="https://user-images.githubusercontent.com/52357235/201248354-ffcdad40-b5c8-46f8-888e-cdf361122d9d.png">

웹서버 테스트

<img width="228" alt="image" src="https://user-images.githubusercontent.com/52357235/201248405-cbf88484-2ad5-45e9-bfb5-38373cb23c05.png">

컨테이너 종료하기

docker stop [container ID | name]

<img width="190" alt="image" src="https://user-images.githubusercontent.com/52357235/201248979-2f23c1a7-b8b4-49ce-80d5-0f4d3346a38a.png">

컨테이너 조회 

<img width="763" alt="image" src="https://user-images.githubusercontent.com/52357235/201249048-4d30107f-177d-4806-b1d0-89a9c4d46e6b.png">

모든 컨테이너 조회

<img width="778" alt="image" src="https://user-images.githubusercontent.com/52357235/201249098-f0af8da8-8c58-4dda-b1c6-eed66516957d.png">

컨테이너 실행하기

docker start [container ID | name]

<img width="205" alt="image" src="https://user-images.githubusercontent.com/52357235/201249586-77003866-0339-4d8b-b50f-16dee5e73d09.png">

콘솔에서 Docker 컨테이너 접속 

docker exec -it [name] bash

<img width="269" alt="image" src="https://user-images.githubusercontent.com/52357235/201249766-bac53c66-8ff4-49d4-b995-d603dd77fbb3.png">

index.html 수정하기

<img width="414" alt="image" src="https://user-images.githubusercontent.com/52357235/201250185-adbecaf0-274b-48ca-8739-dd16bba099df.png">

오류가 뜨기에 아래 커맨드를 입력해서 vim을 설치합니다.

apt-get update
apt-get nano
apt-get vim

vim에서 index.html을 열어보자

<img width="497" alt="image" src="https://user-images.githubusercontent.com/52357235/201250446-70cceb83-0cca-4f62-9688-8a7fc0507edf.png">

수정을 하고 다시 웹사이트에 접속

<img width="395" alt="image" src="https://user-images.githubusercontent.com/52357235/201250550-1478e6b3-31ae-4bef-a748-024c3745c36e.png">

호스트 시스템과 도커 컨테이너 간에 디렉토리 공유

docker -v <host directory>:<container direcotry> [image name]
  
루트 컨테이너 패스워드 변경

systemctl 등록 
  
docker run --name [name] --privileged --restart=always 

maria db 컨테이너 접속 하고 db 조회까지
  
<img width="770" alt="image" src="https://user-images.githubusercontent.com/52357235/201253033-4e602ece-f114-4976-8312-046fc0bedbd1.png">

db 생성
  
<img width="324" alt="image" src="https://user-images.githubusercontent.com/52357235/201253373-d085860d-8943-4c29-88ac-ade3957f9095.png">

디비버로 연결하여 디비 조회
  
<img width="739" alt="image" src="https://user-images.githubusercontent.com/52357235/201253501-5a305528-60a5-4bdf-a5ca-c83641e39e7c.png">

컨테이너로 실행시키고 바로 접속하는 방법

docker run -it --name [container name] [image name] /bin/bash

<img width="1057" alt="image" src="https://user-images.githubusercontent.com/52357235/201799146-897a9385-2b3c-4dad-9c8f-398b3b3a0d02.png">

근데 위와 같은 방법으로 접속하고 exit로 종료를 하면 컨테이너가 꺼지게 된다.
  
exit로 종료해도 다시 켜지게 하는 방법은
  
docker start [container name]

docker exec -it [container name] /bin/bash
  
로 시작하면 exit를 해도 컨테이너가 종료되지 않는다.
  
