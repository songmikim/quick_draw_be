# Quick Draw Backend

Spring Boot 기반으로 작성된 그림 인식 백엔드 서버입니다. 이미지를 업로드하면 Python 모델을 이용해 예측 결과를 반환합니다.

## 요구 사항
- **Java 21** (Gradle Toolchain 사용)
- **Gradle 8** (프로젝트에 `gradlew` 포함)
- Python 환경 및 예측 스크립트(`predict.py`)
- 실행 시 필요한 환경 변수 또는 `application.yml` 설정
  - `file.url` : 업로드 파일 접근 URL
  - `file.path` : 파일 저장 경로
  - `python.base` : Python 가상환경 위치
  - `python.model` : 모델 스크립트가 위치한 경로

## 빌드 및 실행
```bash
./gradlew build       # 프로젝트 빌드
./gradlew bootRun     # 애플리케이션 실행 (포트 3001 기본 사용)
```

또는 완성된 JAR 파일을 실행할 수도 있습니다.

```bash
java -jar build/libs/quickdraw-0.0.1-SNAPSHOT.jar
```

## 주요 기능
- **POST `/quickdraw/predict`**
  - `multipart/form-data`로 이미지를 전송하면 예측 결과(`List<String[]>`)를 반환합니다.
  - 예시:
    ```bash
    curl -F "image=@sample.jpg" http://localhost:3001/quickdraw/predict
    ```

- **TruncateService**
  - 매일 00:00에 업로드 디렉터리의 파일을 자동으로 정리합니다.

## 테스트
단위 테스트와 통합 테스트는 `./gradlew test`로 실행할 수 있습니다. 테스트 중에는 로컬에 존재하는 예제 이미지 경로를 사용하므로 필요 시 경로를 수정해야 합니다.
