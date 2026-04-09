# 06. REST 원칙

## REST 란?

**Representational State Transfer** — 웹 API를 설계하는 **아키텍처 스타일(원칙)**입니다.

REST를 따르는 API를 **RESTful API** 라고 합니다.

---

## REST의 핵심 원칙 6가지

### 1. 자원(Resource) 기반

모든 것은 **자원**으로 표현되고, URL로 식별합니다.

```
✅ /posts/1        → "1번 게시글" 이라는 자원
✅ /users/5/posts  → "5번 유저의 게시글들" 이라는 자원

❌ /getPost?id=1   → 동사(행위) 사용 금지
❌ /deleteUser/5   → 행위를 URL에 넣으면 안 됨
```

---

### 2. HTTP 메서드로 행위 표현

자원에 대한 행위는 URL이 아닌 **HTTP 메서드**로 표현합니다.

```
GET    /posts     → 게시글 목록 조회
POST   /posts     → 게시글 생성
GET    /posts/1   → 1번 게시글 조회
PUT    /posts/1   → 1번 게시글 수정
DELETE /posts/1   → 1번 게시글 삭제
```

---

### 3. Stateless (무상태)

서버는 클라이언트의 **이전 요청을 기억하지 않습니다**.

각 요청은 독립적이고, 필요한 모든 정보를 요청에 담아야 합니다.

```
# 매 요청마다 인증 토큰을 직접 보냄
GET /posts
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGci...
```

> 덕분에 서버를 여러 대로 늘리기(Scale-out) 쉬워집니다.

---

### 4. 일관된 인터페이스 (Uniform Interface)

URL 규칙이 일관성 있어야 합니다.

```
# 일관성 있는 설계 ✅
GET    /users
GET    /users/1
POST   /users
DELETE /users/1

# 일관성 없는 설계 ❌
GET    /getAllUsers
POST   /createNewUser
GET    /user?id=1
```

---

### 5. 계층 구조 (Layered System)

클라이언트는 서버와 직접 통신하는지,  
중간에 프록시/로드밸런서가 있는지 알 필요 없습니다.

```
클라이언트 → 로드밸런서 → 서버1
                       → 서버2
                       → 서버3
```

---

### 6. 표현(Representation)으로 통신

자원 자체가 아니라 **자원의 표현**을 주고받습니다.  
같은 자원을 JSON, XML, HTML 등 다양한 형식으로 표현할 수 있습니다.

```
GET /posts/1
Accept: application/json   → JSON으로 응답
Accept: application/xml    → XML로 응답
```

현실에서는 대부분 JSON만 씁니다.

---

## RESTful URL 설계 원칙 정리

| 원칙 | 예시 |
|---|---|
| 명사 사용 (복수형 권장) | `/posts`, `/users` |
| 계층 구조로 관계 표현 | `/users/1/posts` |
| 소문자 사용 | `/user-profiles` ✅ `/UserProfiles` ❌ |
| 하이픈 사용 (언더바 X) | `/user-profiles` ✅ `/user_profiles` ❌ |
| 마지막 슬래시 없애기 | `/posts` ✅ `/posts/` ❌ |
| 파일 확장자 X | `/posts` ✅ `/posts.json` ❌ |

---

## 흔한 실수

```
❌ /getPosts          → 동사 사용
❌ /post/delete/1     → URL에 행위 포함
❌ /Posts             → 대문자
❌ /get-all-the-posts → 너무 장황
✅ /posts             → 명사, 소문자, 복수형
```

---

## 지금까지 배운 것 종합

```
클라이언트 (Next.js)
    │
    │  GET /posts/1
    │  Authorization: Bearer <token>
    │  Content-Type: application/json
    ▼
서버 (Django)
    │
    │  HTTP/1.1 200 OK
    │  Content-Type: application/json
    │
    │  { "id": 1, "title": "첫 번째 글" }
    ▼
클라이언트 (Next.js)
```

---

## ✅ 확인 퀴즈

1. 아래 URL들 중 RESTful하지 않은 것을 찾고 올바르게 고쳐보세요:
   - `/getAllUsers`
   - `/users/1`
   - `/deletePost/5`
   - `/Users/Profile`

2. REST의 Stateless 원칙이란 무엇인가요?

3. "5번 유저가 작성한 댓글 목록"을 RESTful URL로 표현해보세요.

---

## 이론 완료! 다음 단계

이론 6개를 모두 배웠습니다.

```
✅ 01. HTTP 기초       - 요청/응답 구조
✅ 02. URL 구조        - 자원의 주소
✅ 03. HTTP 메서드     - GET, POST, PUT, DELETE
✅ 04. HTTP 상태코드   - 200, 201, 404, 500
✅ 05. JSON            - 데이터 교환 형식
✅ 06. REST 원칙       - RESTful API 설계 원칙
```

**다음 단계: Django + MariaDB로 API 서버 만들기** 🚀

> 이전 주제: [05. JSON](./05_JSON.md)
