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

시스템 관리자 도커 실행 관리

service docker restart

service docker stop

service docker start

컨테이너 생성

docker run [option] [image name]

