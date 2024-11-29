FROM node:22-alpine

# 작업 디렉토리 설정
WORKDIR /app

# 의존성 파일 복사 및 설치
COPY package*.json ./

RUN npm install

# 애플리케이션 소스 코드 복사
COPY . .

# 컨테이너에서 실행할 포트 지정
EXPOSE 80

# 서버 실행 명령
ENTRYPOINT ["node", "server.js"]