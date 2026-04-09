# 04. HTTP 상태코드

## 상태코드란?

서버가 응답할 때 **"요청이 어떻게 처리됐는지"** 알려주는 3자리 숫자입니다.

---

## 상태코드 분류

| 범위 | 의미 | 설명 |
|---|---|---|
| `1xx` | 정보 | 요청 처리 중 (거의 안 씀) |
| `2xx` | **성공** | 요청이 정상 처리됨 |
| `3xx` | 리다이렉션 | 다른 URL로 이동 |
| `4xx` | **클라이언트 오류** | 요청이 잘못됨 |
| `5xx` | **서버 오류** | 서버에서 문제 발생 |

---

## 자주 쓰는 상태코드

### 2xx — 성공

| 코드 | 이름 | 언제 쓰는지 |
|---|---|---|
| `200 OK` | 성공 | GET, PUT, PATCH 성공 |
| `201 Created` | 생성됨 | POST로 데이터 생성 성공 |
| `204 No Content` | 내용 없음 | DELETE 성공 (응답 바디 없음) |

---

### 4xx — 클라이언트 잘못

| 코드 | 이름 | 언제 쓰는지 |
|---|---|---|
| `400 Bad Request` | 잘못된 요청 | 필수값 누락, 형식 오류 |
| `401 Unauthorized` | 인증 필요 | 로그인 안 된 상태 |
| `403 Forbidden` | 접근 금지 | 권한 없음 (로그인은 됐지만) |
| `404 Not Found` | 찾을 수 없음 | 해당 자원이 존재하지 않음 |
| `405 Method Not Allowed` | 메서드 불허 | 해당 URL에 그 메서드 없음 |
| `409 Conflict` | 충돌 | 이미 존재하는 데이터 (중복 이메일 등) |
| `422 Unprocessable Entity` | 처리 불가 | 유효성 검사 실패 |

---

### 5xx — 서버 잘못

| 코드 | 이름 | 언제 쓰는지 |
|---|---|---|
| `500 Internal Server Error` | 서버 내부 오류 | 예상치 못한 버그 |
| `502 Bad Gateway` | 게이트웨이 오류 | 프록시/서버 간 통신 오류 |
| `503 Service Unavailable` | 서비스 불가 | 서버 과부하, 점검 중 |

---

## 401 vs 403 — 헷갈리는 차이

```
401 Unauthorized  → "누구세요? 로그인부터 하세요"
403 Forbidden     → "누군지 알지만, 여긴 들어올 수 없어요"
```

**예시:**
- 로그인 없이 마이페이지 접근 → `401`
- 일반 유저가 관리자 페이지 접근 → `403`

---

## 실제 API 응답 예시

### 성공 (200)
```json
HTTP/1.1 200 OK

{
  "id": 1,
  "title": "첫 번째 글",
  "content": "안녕하세요"
}
```

### 생성 성공 (201)
```json
HTTP/1.1 201 Created

{
  "id": 5,
  "title": "새 게시글",
  "created_at": "2026-04-08T12:00:00Z"
}
```

### 없는 데이터 조회 (404)
```json
HTTP/1.1 404 Not Found

{
  "error": "Post not found"
}
```

### 유효성 검사 실패 (400)
```json
HTTP/1.1 400 Bad Request

{
  "error": {
    "title": ["이 필드는 필수입니다."],
    "content": ["내용은 10자 이상이어야 합니다."]
  }
}
```

---

## Django에서 상태코드 지정하기 (미리보기)

```python
from rest_framework.response import Response
from rest_framework import status

# 200 OK (기본값)
return Response(data)

# 201 Created
return Response(data, status=status.HTTP_201_CREATED)

# 404 Not Found
return Response({"error": "Not found"}, status=status.HTTP_404_NOT_FOUND)
```

---

## 정리

```
요청 성공  →  2xx
내 요청 잘못  →  4xx
서버 문제  →  5xx
```

---

## ✅ 확인 퀴즈

1. 새 유저를 회원가입 시켰을 때 적절한 상태코드는?
2. 존재하지 않는 게시글을 조회 요청했을 때 상태코드는?
3. 로그인은 됐지만 관리자 전용 기능에 접근했을 때 상태코드는?
4. 서버 내부에서 예상치 못한 오류가 났을 때 상태코드는?

> 이전 주제: [03. HTTP 메서드](./03_HTTP_메서드.md)  
> 다음 주제: [05. JSON](./05_JSON.md)
