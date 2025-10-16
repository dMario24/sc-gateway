# SCG

# 도커빌드
```bash
# 명령어 형식: docker build -t <도커허브아이디>/<이미지 이름>:<태그> <빌드 컨텍스트 경로>

$ docker build -t datamario24/sc-gateway:0.2.0 .
$ docker push datamario24/sc-gateway:0.2.0
```

# 도커허브 경로 및 사용
- https://hub.docker.com/r/datamario24/sc-gateway
```bah
$ docker pull datamario24/sc-gateway:0.2.0
```

# 도커 컴포즈 라우터 설정 환경 변수
- 설정 예시
- atamario24/sc-gateway:0.3.0 버전 이후 부터 적용 가능
```bash
services:
  # 게이트웨이 서비스 (sc-gateway)
  gateway:
    image: my-spring-app:1.0 # 빌드된 Docker 이미지 이름
    ports:
      - "9000:9000"
    environment:
      # 💡 Compose 내부의 다른 서비스 이름을 사용하여 URI를 설정합니다.
      - HELLO_SERVICE_URI=http://hello-service:8080 
    depends_on:
      - hello-service
    networks:
      - my-network

  # 타겟 서비스 (hello-service)
  hello-service:
    image: my-target-app:1.0
    ports:
      - "8765:8080" # 외부로 8765 포트 노출 (선택 사항)
    networks:
      - my-network
    # Compose 내부에서는 서비스 이름(hello-service)이 DNS 역할을 합니다.

networks:
  my-network:
    driver: bridge
```
