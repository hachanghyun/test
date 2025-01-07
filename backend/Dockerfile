# (1) Gradle 빌드 단계 (multi-stage build)
FROM gradle:7.6-jdk17 AS builder
WORKDIR /app

# backend 폴더의 모든 소스 복사
COPY . .

# Gradle을 이용하여 Spring Boot JAR 생성
RUN gradle clean bootJar

# (2) 실행 단계
FROM openjdk:17-jdk-slim
WORKDIR /app

# 빌드 단계에서 생성된 JAR 복사
COPY --from=builder /app/build/libs/*.jar app.jar

# 8080 포트를 컨테이너 외부로 열어준다
EXPOSE 8080

# 컨테이너가 실행될 때 Java -jar 명령을 실행
ENTRYPOINT ["java","-jar","/app/app.jar"]
