# 01. Nginx 컨테이너 실행

## 목표
서버에 직접 설치하지 않고 Docker로 Nginx를 실행해 보고, 컨테이너가 어떻게 동작하는지 확인한다.

## 실행한 명령어
`docker run -d --name web -p 8080:80 nginx`
`docker ps`
`docker logs web`

## 결과
- localhost:8080에서 Nginx 기본 페이지가 뜬다.
![nginx 화면](/docs/imges/2-1.nginx-browser.png)
![docker ps](/docs/imges/3.docker-ps.png)

## 확인한 점
- 명령 한 줄로 웹서버 실행
- `-p 8080:80`은 내 컴퓨터 8080 포트를 컨테이너 80 포트로 연결한다.

## 로그와 컨테이너 내부 확인
`docker logs web`
`docker exec -it web bash`
`cat /etc/nginx/conf.d/default.conf`

- 브라우저를 새로고침할 때마다 access 로그가 한 줄씩 쌓인다.
![docker logs](/docs/imges/4.docker-logs.png)
- 컨테이너 안에서 Nginx 설정 파일을 확이한다.
![nginx 화면](/docs/imges/5.nginx-conf.png)





