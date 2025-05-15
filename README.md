# API 테스트 자동화 프로젝트
- 이 프로젝트는 솔루션 Motion T API를 대상으로 기능 검증 수행하기 위해 구성된 테스트 자동화 저장소입니다.


## 테스트 목적 및 범위
- 공통코드 정보 조회 API
- 로그인/접수/대시보드/환자상세/조회 API 테스트
- 펜차트 CRUD API 테스트
- 인증 방식(Bearer 토큰) 테스트
- 에러 응답 및 rate-limit 대응 테스트


## 사용 기술 및 도구
- 언어: Javascript
- 테스트 도구: Postman
- CI/CD: Github Webhook / Github Submodule / Jenkins / nCloud / Newman


## 테스트 실행 방법
1. `env.postman_environment.json.json` 파일에 MOTION_T_ENV을 설정합니다.
2. Postman/Newman 을 사용하여 테스트 스크립트를 실행합니다.
3. newman run MOTION_T_API_TEST.postman_collection.json -e ./api_env_private/env.postman_environment.json --env-var IMAGE_PATH=./image/

## 인증 정보 및 호출 도메인
```markdown
호출 도메인은 .env 파일 내 domain 을 사용해야하며 로그인을 제외한 모든 API 호출은 인증이 되어있어야합니다.
.env 파일에 존재하는 MOTION_T_ENV의 `accessToken`이 사용되며, accessToken 은 로그인 시 자동으로 세팅됩니다.
```


## 디렉토리 구조

```markdown
apiTest/
├── api_env_private/
|   ├──  env.postman_environment.json.json
├── image/
|   ├──  updateImage
|   |    ├──  updateImageFiles
|   ├──  imageFiles
├── node_modules/
├── MOTION_T_API_TEST.postman_collection.json
├── .gitignore
├── .gitmodules
├── package.json
├── package-lock.json
└── README.md
```

## CI/CD 플로우
![2025-04-28 16 25 10](https://github.com/user-attachments/assets/22087462-951e-44fb-afee-3639900e0054)

- master branch push 이벤트 발생 시 jenkins 에서는 자동으로 빌드되어 실행하게 되며, 테스트 결과를 slack 으로 발송되게됩니다.
