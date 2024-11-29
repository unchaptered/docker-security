FROM node:22-alpine

RUN addgroup --system --gid 1001 nodejs && \
    adduser --system --uid 1001 expressjs --ingroup nodejs

# 작업 디렉토리 설정
WORKDIR /app

# 의존성 파일 복사 및 설치
COPY package*.json ./

RUN npm install

# 애플리케이션 소스 코드 복사
COPY . .

# 컨테이너에서 실행할 포트 지정
EXPOSE 80

RUN chown -R expressjs:nodejs /app

USER expressjs

# 서버 실행 명령
ENTRYPOINT ["node", "server.js"]