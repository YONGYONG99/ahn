# 02. URL 구조

## URL 이란?

**Uniform Resource Locator** — 인터넷 상의 특정 자원(페이지, 데이터)의 **주소**입니다.

---

## URL 분해하기

```
https://api.example.com:8000/users/1?sort=asc#section1
```

| 부분 | 이름 | 설명 |
|---|---|---|
| `https` | **프로토콜** | 어떤 규칙으로 통신할지 |
| `api.example.com` | **호스트(도메인)** | 어떤 서버에 요청할지 |
| `:8000` | **포트** | 서버의 어떤 문(포트)으로 들어갈지 |
| `/users/1` | **경로(Path)** | 서버 안의 어떤 자원인지 |
| `?sort=asc` | **쿼리 파라미터** | 추가 조건 (필터, 정렬 등) |
| `#section1` | **프래그먼트** | 페이지 내 특정 위치 (API에서는 거의 안 씀) |

---

## API에서 URL이 중요한 이유

RESTful API에서 URL은 **자원(Resource)을 표현**합니다.

```
/users          → 사용자 목록
/users/1        → 1번 사용자
/users/1/posts  → 1번 사용자의 게시글 목록
/posts          → 전체 게시글 목록
/posts/5        → 5번 게시글
```

URL만 봐도 **"어떤 데이터에 접근하는지"** 알 수 있어야 합니다.

---

## 쿼리 파라미터 vs 경로 파라미터

### 경로 파라미터 (Path Parameter)
특정 자원을 **식별**할 때 사용합니다.

```
/users/1        → 1번 유저
/users/42       → 42번 유저
/posts/7        → 7번 게시글
```

### 쿼리 파라미터 (Query Parameter)
자원을 **필터링/정렬/검색**할 때 사용합니다.

```
/users?role=admin           → 관리자 유저만 조회
/posts?page=2&limit=10      → 2페이지, 10개씩
/products?search=노트북      → "노트북" 검색
```

---

## 포트 번호

| 포트 | 용도 |
|---|---|
| `80` | HTTP 기본 포트 (생략 가능) |
| `443` | HTTPS 기본 포트 (생략 가능) |
| `8000` | Django 개발 서버 기본 포트 |
| `3000` | Next.js 개발 서버 기본 포트 |
| `3306` | MariaDB/MySQL 기본 포트 |

우리가 실습할 때:
- Django: `http://localhost:8000`
- Next.js: `http://localhost:3000`

---

## 실제 예시 — 인스타그램 같은 서비스라면?

```
GET  /posts              → 전체 게시글 조회
GET  /posts/3            → 3번 게시글 조회
POST /posts              → 게시글 작성
PUT  /posts/3            → 3번 게시글 수정
DELETE /posts/3          → 3번 게시글 삭제

GET  /posts/3/comments   → 3번 게시글의 댓글 목록
POST /posts/3/comments   → 3번 게시글에 댓글 작성
```

URL + HTTP 메서드 조합으로 모든 기능이 표현됩니다.

---

## 정리

- URL = 자원의 주소
- 경로 파라미터 = 자원 식별 (`/users/1`)
- 쿼리 파라미터 = 조건/필터 (`?page=2`)
- RESTful API에서 URL은 **명사(자원)** 로 표현

---

## ✅ 확인 퀴즈

1. `/products/5?color=red` 에서 경로 파라미터와 쿼리 파라미터는 각각 무엇인가요?
2. "3번 유저가 쓴 댓글 목록"을 표현하는 URL을 직접 만들어보세요.
3. Django 개발 서버의 기본 포트는 몇 번인가요?

> 이전 주제: [01. HTTP 기초](./01_HTTP_기초.md)  
> 다음 주제: [03. HTTP 메서드](./03_HTTP_메서드.md)
