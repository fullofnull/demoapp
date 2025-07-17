# 1단계: 빌드 이미지
FROM eclipse-temurin:21-jdk-jammy AS builder

WORKDIR /app

# Gradle wrapper와 소스 복사
COPY . .

# Gradle wrapper 실행 권한 부여
RUN chmod +x gradlew

# 애플리케이션 빌드
RUN ./gradlew clean bootJar --no-daemon

# 2단계: 경량 실행 이미지
FROM eclipse-temurin:21-jre-jammy

WORKDIR /app

# 빌드 결과 JAR 복사
COPY --from=builder /app/build/libs/*.jar app.jar

# 실행
ENTRYPOINT ["java", "-jar", "app.jar"]
