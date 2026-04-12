# 내 개인적인 메모임

posts/
├── models.py    ← 비어있음 (DB 테이블 설계)
├── views.py     ← 비어있음 (API 로직)
├── admin.py     ← 비어있음
├── tests.py     ← 비어있음
└── migrations/  ← 비어있음
이 틀 안에 코드를 채워서 CRUD API를 만드는 게 앞으로 할 일이에요.

순서

1. models.py     → Post 테이블 설계 (제목, 내용, 날짜 등)
2. migrate       → DB에 실제 테이블 생성
3. serializers.py → JSON ↔ Python 변환 설정
4. views.py      → GET/POST/PUT/DELETE 처리 로직
5. urls.py       → URL 연결

