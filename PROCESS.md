# 학습 진행 기록

## 전체 로드맵

| 단계 | 내용 | 상태 |
|---|---|---|
| 1단계 | 이론 (HTTP, REST, JSON 등) | ✅ 완료 |
| 2단계 | Django + MariaDB API 서버 | 🔄 진행중 |
| 3단계 | Next.js에서 API 호출 | ⬜ 예정 |
| 4단계 | CRUD 전체 흐름 완성 | ⬜ 예정 |
| 5단계 | 배포 고도화 (Docker + docker-compose) | ⬜ 예정 |

## 폴더 구조

```
ahn/
├── theory/        ← 이론 정리
├── backend/       ← Django 프로젝트
├── frontend/      ← Next.js 프로젝트
├── infra/         ← Docker, 배포 설정 (5단계)
└── PROCESS.md     ← 이 파일
```

## 2단계 진행 순서

- [x] 환경 세팅 (가상환경, 패키지 설치)
- [x] Django 프로젝트 생성
- [x] MariaDB 연결 (settings.py + .env)
- [x] migrate (기본 테이블 생성)
- [x] posts 앱 생성
- [x] Post 모델 정의
- [ ] makemigrations & migrate (posts 테이블 생성)
- [ ] Serializer 작성
- [ ] View & URL 연결
- [ ] API 테스트

## 2단계 현재 구조

```
backend/
├── config/
│   ├── settings.py   ← DB 연결, 앱 등록 설정
│   └── urls.py       ← 루트 URL
├── posts/
│   ├── models.py     ← Post 테이블 설계 (완료)
│   ├── views.py      ← API 로직 (미작성)
│   └── migrations/   ← 마이그레이션 파일
├── .env              ← DB 비밀번호 (git 제외)
├── .env.example      ← 비밀번호 없는 템플릿
└── manage.py
```

## 5단계 배포 고도화 개요

```
[로컬]
docker build → 이미지 생성
docker push  → Docker Registry에 업로드

[서버]
docker pull         → Registry에서 이미지 다운로드
docker-compose up   → 컨테이너 실행 (백엔드 + 프론트 + DB)
```

관리 파일 (infra/ 폴더):
- docker-compose.yml      → 로컬 개발용
- docker-compose.prod.yml → 운영 서버용
- .env.example            → 환경변수 템플릿
