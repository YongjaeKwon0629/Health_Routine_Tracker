---


# 🐙 Git 협업 초보자 가이드 (미니 프로젝트용)

> Git을 처음 쓰는 사람도 이 문서만 보면 협업할 수 있습니다.  
> **규칙: main 직접 수정 ❌ / feature 브랜치에서 작업 ✅**

---

## 📌 0. Git이 뭔데?
- Word 파일 여러 명이 수정하면 `최종본.docx`, `최종진짜.docx` 이런 거 생기죠?  
- Git은 그걸 막아주는 **코드 버전 관리 프로그램**이에요.  
- GitHub는 Git으로 관리하는 코드를 올려두는 "온라인 공유 폴더"라고 생각하면 됩니다.  

---

## 🛠 1. 준비 단계

### 1.1 Git 설치
- [Git 다운로드](https://git-scm.com/downloads) → 설치  

### 1.2 GitHub 계정 만들기
- [GitHub](https://github.com/) 접속 → 회원가입  

### 1.3 내 정보 등록
```bash
git config --global user.name "내이름"
git config --global user.email "내이메일@example.com"
````

---

## 📂 2. 프로젝트 시작하기

### 2.1 저장소 내려받기 (처음 1번만)

```bash
git clone https://github.com/username/project.git
cd project
```

**👉 이제 이 `project` 폴더 안에서만 작업하면 됩니다.**

---

## 🌲 3. Git 기본 개념

* **브랜치(branch)** → 평행우주. 내 작업은 feature 브랜치에서만.
* **commit** → 저장하기 (사진 찍듯 코드 기록)
* **push** → 내 코드 GitHub에 올리기
* **pull** → 다른 사람 코드 가져오기
* **merge** → 브랜치 합치기

---

## 🔄 4. 하루 작업 흐름 (실전 예시)

### 4.1 작업 시작 전 (매일 아침)

```bash
git checkout develop          # develop 브랜치로 이동
git pull origin develop       # 최신 코드 받기
```

### 4.2 내 브랜치 만들기

```bash
git checkout -b feature/login
```

### 4.3 코딩 후 저장하기

```bash
git status                     # 변경된 파일 확인
git add .                      # 모든 변경 추가
git commit -m "feat: 로그인 화면 추가"  # 저장
```

### 4.4 GitHub에 업로드

```bash
git push origin feature/login
```

### 4.5 Pull Request 만들기

1. GitHub 저장소 접속
2. `Compare & Pull Request` 클릭
3. 제목 예시: `feat: 로그인 화면 추가`
4. 팀원 리뷰 후 `develop`에 merge

---

## ⚡️ 5. 충돌(Conflict) 해결하기

충돌이 나면 파일에 이런 표시가 생깁니다:

```txt
<<<<<<< HEAD
내가 수정한 코드
=======
팀원이 수정한 코드
>>>>>>> develop
```

👉 이때 직접 보고 맞는 코드로 수정 → 저장 → 다시 commit & push

---

## 📝 6. 커밋 메시지 규칙

* `feat:` 새 기능 추가
* `fix:` 버그 수정
* `docs:` 문서 수정
* `style:` 코드 스타일 변경
* `refactor:` 코드 개선

예시:

```bash
git commit -m "feat: 회원가입 API 구현"
git commit -m "fix: 로그인 토큰 검증 오류 수정"
```

---

## 📖 7. 자주 쓰는 Git 명령어

| 상황         | 명령어                                 | 설명          |
| ---------- | ----------------------------------- | ----------- |
| 프로젝트 처음 시작 | `git clone URL`                     | 저장소 복사      |
| 작업 시작 전    | `git pull origin develop`           | 최신 코드 받기    |
| 브랜치 만들기    | `git checkout -b feature/기능명`       | 새 작업 공간     |
| 상태 확인      | `git status`                        | 변경 확인       |
| 저장         | `git add .` → `git commit -m "메시지"` | 변경 기록       |
| 업로드        | `git push origin 브랜치명`              | GitHub에 올리기 |
| 브랜치 이동     | `git checkout 브랜치명`                 | 다른 브랜치로 이동  |

---

## 📋 8. 이번 프로젝트 협업 규칙

1. 🚫 `main` 직접 수정 금지
2. ✅ 모든 작업은 `feature/*` 브랜치에서 진행
3. ✅ 작업 전 무조건 `git pull origin develop`
4. ✅ commit 메시지 규칙 지키기
5. ✅ Pull Request(PR) 만들고 팀원 리뷰 후 merge

---

## 🎯 정리

👉 **작업 전 → pull**
👉 **작업 중 → feature 브랜치에서 commit**
👉 **작업 후 → push & PR**

이 3가지만 지키면 협업이 깨끗하게 돌아갑니다.



---



원하시면 제가 여기에 **그림(워크플로우 다이어그램)**을 추가해서 시각적으로 이해하기 쉽게 만들어드릴 수도 있어요. 그림 버전도 드릴까요?
```
