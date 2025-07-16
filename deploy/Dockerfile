# 1) 빌드 시 사용되는 이미지
FROM eclipse-temurin:21-jdk-jammy AS builder

WORKDIR /app

COPY . .

# Gradle wrapper로 빌드 실행 (build/libs/*.jar 생성)
RUN ./gradlew clean bootJar --no-daemon

# 2) 실제 실행할 경량 이미지
FROM eclipse-temurin:21-jre-jammy

WORKDIR /app

# 빌드한 JAR 복사
COPY --from=builder /app/build/libs/*.jar app.jar

# 애플리케이션 실행
ENTRYPOINT ["java", "-jar", "app.jar"]
