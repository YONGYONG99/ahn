# 05. JSON

## JSON 이란?

**JavaScript Object Notation** — API에서 데이터를 주고받을 때 사용하는 **텍스트 기반 데이터 형식**입니다.

사람도 읽기 쉽고, 기계도 파싱하기 쉬워서 현재 웹 API의 표준입니다.

---

## JSON 기본 문법

### 기본 타입

```json
{
  "문자열": "안녕하세요",
  "숫자": 42,
  "소수": 3.14,
  "불리언": true,
  "null값": null
}
```

### 배열

```json
{
  "tags": ["python", "django", "rest"],
  "scores": [100, 95, 88]
}
```

### 중첩 객체

```json
{
  "user": {
    "id": 1,
    "name": "홍길동",
    "address": {
      "city": "서울",
      "district": "강남구"
    }
  }
}
```

---

## 실제 API 응답 예시

### 단일 게시글 조회

```json
{
  "id": 1,
  "title": "첫 번째 글",
  "content": "안녕하세요!",
  "author": {
    "id": 3,
    "username": "hong"
  },
  "tags": ["일상", "공부"],
  "created_at": "2026-04-08T09:00:00Z",
  "is_published": true
}
```

### 게시글 목록 조회

```json
{
  "count": 100,
  "next": "/posts?page=2",
  "previous": null,
  "results": [
    {
      "id": 1,
      "title": "첫 번째 글"
    },
    {
      "id": 2,
      "title": "두 번째 글"
    }
  ]
}
```

---

## JSON vs 다른 형식들

과거에는 XML을 많이 썼지만, JSON이 훨씬 간결합니다.

**XML (구식)**
```xml
<user>
  <id>1</id>
  <name>홍길동</name>
  <email>hong@example.com</email>
</user>
```

**JSON (현재 표준)**
```json
{
  "id": 1,
  "name": "홍길동",
  "email": "hong@example.com"
}
```

---

## 언어별 JSON 처리

### Python (Django)

```python
import json

# Python dict → JSON 문자열
data = {"name": "홍길동", "age": 30}
json_str = json.dumps(data)
# '{"name": "홍길동", "age": 30}'

# JSON 문자열 → Python dict
parsed = json.loads(json_str)
print(parsed["name"])  # 홍길동
```

Django REST Framework를 쓰면 이 변환이 자동으로 됩니다.

### JavaScript (Next.js)

```javascript
// JSON 문자열 → JS 객체
const data = JSON.parse('{"name": "홍길동"}')
console.log(data.name)  // 홍길동

// JS 객체 → JSON 문자열
const str = JSON.stringify({ name: "홍길동" })

// fetch API로 JSON 받기
const response = await fetch('/api/posts')
const posts = await response.json()  // 자동으로 파싱
```

---

## Content-Type 헤더

API 요청/응답 시 데이터 형식을 헤더로 알려줍니다.

```
# 요청 헤더 (JSON 데이터를 보낼 때)
Content-Type: application/json

# 응답 헤더 (서버가 JSON으로 응답할 때)
Content-Type: application/json
```

---

## 정리

- JSON = 데이터를 텍스트로 표현하는 형식
- `{ }` = 객체, `[ ]` = 배열
- 웹 API의 사실상 표준
- Python ↔ JSON ↔ JavaScript 변환이 쉬움

---

## ✅ 확인 퀴즈

1. 아래를 JSON으로 표현해보세요:
   - 이름: 김철수, 나이: 25, 취미: ["독서", "코딩"]

2. JSON에서 사용 가능한 기본 타입 5가지는 무엇인가요?

3. API 요청 시 JSON 데이터를 보낼 때 설정해야 하는 헤더는 무엇인가요?

> 이전 주제: [04. HTTP 상태코드](./04_HTTP_상태코드.md)  
> 다음 주제: [06. REST 원칙](./06_REST_원칙.md)
