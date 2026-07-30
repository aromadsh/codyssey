# 1. 베이스 이미지 설정 (가벼운 nginx 알핀 버전 사용)
FROM nginx:alpine

# 2. 작성한 소스 코드를 컨테이너 내부의 nginx 웹 루트 경로로 복사
COPY ./app /usr/share/nginx/html

# 3. 80번 포트 개방
EXPOSE 80

# 4. 컨테이너 실행 시 nginx를 백그라운드가 아닌 포그라운드에서 실행 (컨테이너 유지용)
CMD ["nginx", "-g", "daemon off;"]
