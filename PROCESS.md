# 학습 진행 기록

## 전체 로드맵

| 단계 | 내용 | 상태 |
|---|---|---|
| 1단계 | 이론 (HTTP, REST, JSON 등) | ✅ 완료 |
| 2단계 | Django + MariaDB API 서버 | ✅ 완료 |
| 3단계 | Next.js에서 API 호출 | 🔄 진행중 |
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

## 2단계 완료 ✅

- [x] 환경 세팅 (가상환경, 패키지 설치)
- [x] Django 프로젝트 생성
- [x] MariaDB 연결 (settings.py + .env)
- [x] migrate (기본 테이블 생성)
- [x] posts 앱 생성
- [x] Post 모델 정의
- [x] makemigrations & migrate (posts_post 테이블 생성)
- [x] Serializer 작성
- [x] View & URL 연결
- [x] 서버 실행 & API 테스트 (201 Created 확인)

## 2단계 최종 구조

```
backend/
├── config/
│   ├── settings.py   ← DB 연결, 앱 등록 설정
│   └── urls.py       ← 루트 URL (api/ → posts.urls)
├── posts/
│   ├── models.py     ← Post 테이블 설계
│   ├── serializers.py ← JSON ↔ Python 변환
│   ├── views.py      ← CRUD 로직 (ModelViewSet)
│   ├── urls.py       ← posts/ URL 연결
│   └── migrations/   ← 마이그레이션 파일
├── .env              ← DB 비밀번호 (git 제외)
├── .env.example      ← 비밀번호 없는 템플릿
└── manage.py
```

## API 엔드포인트

| 메서드 | URL | 기능 |
|---|---|---|
| GET | `/api/posts/` | 목록 조회 |
| POST | `/api/posts/` | 게시글 생성 |
| GET | `/api/posts/1/` | 단건 조회 |
| PUT | `/api/posts/1/` | 전체 수정 |
| PATCH | `/api/posts/1/` | 일부 수정 |
| DELETE | `/api/posts/1/` | 삭제 |

## 3단계 진행 예정

- [ ] Next.js 프로젝트 생성
- [ ] API 호출 (fetch)
- [ ] 게시글 목록 화면
- [ ] 게시글 작성 화면

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
