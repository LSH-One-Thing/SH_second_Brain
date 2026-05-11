---
작성일: 2026-05-11
작성자: Claude Sonnet 4.6
상태: 계획 단계 — 실행 전 검토 필요
버전: 1.0
---

# 옵시디언 보관소 재정리 계획서

## 0. 전제 조건 및 사전 확인 사항

| 항목 | 현재 값 | 비고 |
|------|--------|------|
| 보관소 루트 (Obsidian 기준) | `One_thing_valut/One_thing/` | `.obsidian/`이 여기에 위치 |
| 기본 새 파일 경로 (`app.json`) | `raw/` | 재정리 후 `04_Inbox/`로 변경 필요 |
| 링크 자동 업데이트 (`app.json`) | `true` | Obsidian 내부 이동 시 링크 자동 갱신됨 |
| 건드리지 않는 폴더 | `.obsidian/`, `.trash/`, `wiki/` | |

> **⚠️ 실행 전 필수**: `git add -A && git commit -m "재정리 전 스냅샷"` 으로 현 상태 백업  
> **⚠️ 이동 방법**: 파일 이동은 반드시 **Obsidian 파일 탐색기**를 통해 수행  
> → `alwaysUpdateLinks: true` 덕분에 `[[링크]]`가 자동 갱신됨. CLI/파일탐색기로 이동 시 링크 깨짐.

---

## 1. 새 폴더 구조 (목표 상태)

```
One_thing/
├── .obsidian/                        ← 건드리지 않음
│
├── 00_Assets/                        ← 이미지·첨부파일 전용 (Obsidian attachmentFolderPath 설정)
│
├── 01_Personal/                      ← 개인: 자기분석, 학습, 마인드셋
│   ├── 01_Self_Analysis/             ← 자기성찰, 직업탐색
│   ├── 02_Mindset_Philosophy/        ← 마인드셋, 철학 (100+ 예상 → 내부 서브폴더는 001_ 형식)
│   ├── 03_Dev_Python/                ← 개발 학습
│   ├── 04_Lang_English/              ← 영어 학습
│   └── 05_Reading_Notes/             ← 독서 노트
│
├── 02_Work/                          ← 업무: 콘텐츠 제작, 프로젝트, 비즈니스
│   ├── 01_Projects/                  ← 진행 중 프로젝트
│   │   ├── 01_소설_아랫것들/
│   │   └── 02_1인사업기획/
│   ├── 02_Content_Creator/           ← 유튜브/콘텐츠 제작 레퍼런스 (100+ 예상 → 001_ 형식 대기)
│   ├── 03_Business_Ideas/            ← 사업 아이디어
│   ├── 04_Insight_Sources/           ← 인사이트 원천 자료
│   ├── 05_Concepts/                  ← 개념 정리 (클루지, 심리 이론 등)
│   ├── 06_Thinking_Writing/          ← 글쓰기·사고법
│   └── 07_References/                ← 기타 레퍼런스
│
├── 03_Templates/                     ← 옵시디언 템플릿, 스니펫, 프롬프트
│
├── 04_Inbox/                         ← 임시 캡처 (처리 후 위 폴더로 분류)
│
├── 99_Archive/                       ← 종료된 프로젝트, 오래된 기록
│   ├── 01_Brain_Dumps/
│   ├── 02_General/
│   ├── 03_Past_Business_Phone/
│   ├── 04_Social_Uploads/
│   └── 05_Trash_Thoughts/
│
└── wiki/                             ← Claude 관리 영역 (CLAUDE.md 운영 규칙, 건드리지 않음)
    ├── index.md
    ├── log.md
    └── (개념 파일 44개)
```

### 5레벨 검증

```
루트(0) → One_thing(1) → 02_Work(2) → 01_Projects(3) → 01_소설_아랫것들(4) → file.md(5)  ✓
루트(0) → One_thing(1) → 01_Personal(2) → 02_Mindset_Philosophy(3) → file.md(4)          ✓
루트(0) → One_thing(1) → 99_Archive(2) → 01_Brain_Dumps(3) → file.md(4)                  ✓
```

모든 경로가 5레벨 이내. 위반 없음.

---

## (a) 폴더/파일 매핑 테이블 (현재 → 새 위치)

### A-1. 폴더 단위 매핑

| 현재 경로 (`One_thing/` 기준) | 새 경로 | 파일 수 | 비고 |
|------------------------------|---------|--------|------|
| `raw/20_Areas/Self_Analysis/` | `01_Personal/01_Self_Analysis/` | 19 | |
| `raw/20_Areas/Mindset_Philosophy/` | `01_Personal/02_Mindset_Philosophy/` | 55 | 향후 100+ 가능 |
| `raw/20_Areas/Dev_Python/` | `01_Personal/03_Dev_Python/` | 10 | |
| `raw/20_Areas/Lang_English/` | `01_Personal/04_Lang_English/` | 10 | |
| `raw/30_Resources/Reading_Notes/` | `01_Personal/05_Reading_Notes/` | 13 | |
| `raw/10_Projects/소설_아랫것들/` | `02_Work/01_Projects/01_소설_아랫것들/` | 18 | |
| `raw/10_Projects/1인_사업기획/` | `02_Work/01_Projects/02_1인사업기획/` | 2 | |
| `raw/30_Resources/Content_Creator/` | `02_Work/02_Content_Creator/` | 51 | 향후 100+ 가능 |
| `raw/30_Resources/Business_Ideas/` | `02_Work/03_Business_Ideas/` | 47 | |
| `raw/30_Resources/Insight_Sources/` | `02_Work/04_Insight_Sources/` | 22 | |
| `raw/30_Resources/Concepts/` | `02_Work/05_Concepts/` | 9 | |
| `raw/20_Areas/Thinking_Writing/` | `02_Work/06_Thinking_Writing/` | 48 | ※ 주의사항 참조 |
| `raw/30_Resources/References/` | `02_Work/07_References/` | 3 | |
| `raw/99_System/Templates/` | `03_Templates/` | 1 | |
| `raw/00_Inbox/` | `04_Inbox/` | 9 | |
| `수집함/` | `04_Inbox/` | 1 | `raw/` 루트 동명 파일과 중복 확인 필요 |
| `raw/40_Archives/Brain_Dumps/` | `99_Archive/01_Brain_Dumps/` | 4 | |
| `raw/40_Archives/General_Archive/` | `99_Archive/02_General/` | 9 | |
| `raw/40_Archives/Past_Business_Phone/` | `99_Archive/03_Past_Business_Phone/` | 4 | |
| `raw/40_Archives/Social_Uploads/` | `99_Archive/04_Social_Uploads/` | 1 | |
| `raw/40_Archives/Trash_Thoughts/` | `99_Archive/05_Trash_Thoughts/` | 5 | |

### A-2. `raw/99_System/Attachments/` 세분 처리

이 폴더는 이미지·텍스트·마크다운이 혼재한 catch-all 폴더. 유형별로 분리한다.

| 파일 유형 | 대상 파일 | 새 위치 |
|----------|----------|--------|
| PNG/JPG (Pasted image, KakaoTalk) | 이미지 전체 (약 40개) | `00_Assets/` |
| `태블릿 팁 모음.md` | 활용 팁 | `01_Personal/01_Self_Analysis/` |
| `사업 아이디어 추론.md` | 비즈니스 | `02_Work/03_Business_Ideas/` |
| `래퍼런스 분석 프롬프트 모음.md` | 프롬프트 | `03_Templates/` |
| `창업,사업 아이템 찾기 프롬프트.md` | 프롬프트 | `03_Templates/` |
| `창의적인 글쓰기 프롬프트 팁.md` | 프롬프트 | `03_Templates/` |
| `상위 0.1%의 사람들만 아는 챗gpt...md` | 참고 자료 | `02_Work/07_References/` |
| `자청 글쓰기 4가지 꿀팁.txt`, `1.txt` | 글쓰기 | `02_Work/06_Thinking_Writing/` (`.md`로 변환 권장) |
| `자청 표본이론.txt` | 개념 | `02_Work/05_Concepts/` (`.md`로 변환 권장) |
| `모텔이론.txt` | 개념 | `02_Work/05_Concepts/` (`.md`로 변환 권장) |
| `돈버는 글쓰기 공식.txt` | 글쓰기 | `02_Work/06_Thinking_Writing/` (`.md`로 변환 권장) |

### A-3. `raw/` 루트 낱개 파일 64개 분류

루트에 바로 떨어진 파일을 주제별로 분류. 제목 기반 추정이며, **실행 전 내용 확인 후 최종 결정**.

#### → `02_Work/02_Content_Creator/` (약 20개)

| 파일명 |
|--------|
| 85만명의 구독자를 만든 비법 (유료강의 같은거 듣지 마세요).md |
| AI 댓글 수집.md |
| 세바시- 롱런하는 창작자들이 절대 놓치지 않는 새로운 부의 공식...md |
| 취미조차 없는 평범한 사람이 유튜브 주제 정하는 법.md |
| 유튜브 미루지 말고 이렇게 시작하세요....md |
| 마케팅 제목 짓기.md |
| 편집 팁 ㅡ 자막 작성 팁.md |
| 해외 천재유튜버들이 몰래 쓰는 니치밴딩 전략.md |
| 자청 AI로 100억 버는 6개 질문, 모두 공개합니다.md |
| 자청- 마케팅 설계자 해석.md |
| 자청 6가지 이론.md |
| 자청-본능분석 & 반박제거.md |
| 자청의 모든걸 8분안에 담은 영상 (9단계 상승나선이론).md |
| 자청의 인생책, 14년만에 새 책 나왔는데 ㄷㄷ.md |
| 자청- 하버드생들의 인생책, 아까워서 7년간 리뷰안했다(생각에 관한 생각).md |
| 북튜버 기획서.md |
| 심리학고양이댓글.md |
| 정서불안김햄찌댓글.md |

#### → `01_Personal/02_Mindset_Philosophy/` (약 12개)

| 파일명 |
|--------|
| 99%가 인생을 낭비하는 이유.md |
| 도망친 곳에 행복이 없는 이유.md |
| 삶이 소풍이라는것에 대하여.md |
| 대혐오의 시대인 이유.md |
| 밖에서는 참는데 집에 오면 폭발하는 이유.md |
| 본질이 안 보이는 사람들의 공통점.md |
| 인간의 본성을 이해한다면.md |
| 이거 모르면 평생 시간에 쫓기며 살게 됨.md |
| 일 잘하는 사람  특징.md |
| 쎈척하는 사람과 진짜 강한사람의 '차이'.md |
| 자의식 과잉.md |
| 모든 사람의 마음이 보이니 인생 쉽더군요. 뇌욕망의 비밀을 풀다.md |
| 도파민의 역설.md |

#### → `02_Work/03_Business_Ideas/` (약 5개)

| 파일명 |
|--------|
| AI활용 1인기업 실행 전략이 궁금해.md |
| INTP 수익화 모델 찾기.md |
| 인디 해커 전략.md |
| 리뷰 분석 자동화 및 리포트 작성 서비스.md |
| 월 1000 부업 이걸 믿는게 지능이 낮은거죠(6가지 부업에 대하여).md |

#### → `02_Work/05_Concepts/` (약 3개)

| 파일명 |
|--------|
| 심리적 우위란 무엇인가.md |
| 클루지 - 승자의 저주.md |
| 클루지 - 악플러.md |

#### → `01_Personal/01_Self_Analysis/` (약 3개)

| 파일명 |
|--------|
| 나는 왜 글을 쓰는가.md |
| 직업 탐색 - 명사가 아닌 동사를 떠올려라.md |
| 불편함 찾기.md |

#### → `01_Personal/05_Reading_Notes/` (약 6개)

| 파일명 |
|--------|
| 2024년 단 한 권만 100번을 읽어야 한다면 (뇌 욕망의 비밀을 풀다).md |
| 책 읽는게 제일 재밌는 사람의 하루  독서 브이로그.md |
| 책고리즘.md |
| 가난한 사람은 모르는 12가지 독서법 (세이노의 가르침).md |
| 인간의 운명은 정해져 있을까  『토지』 박경리 작가의 숨겨진 명작.md |
| 우리가 세상을 오해하는 10가지 이유ㅣ빌게이츠의 인생책 『팩트풀니스』.md |

#### → `02_Work/04_Insight_Sources/` (약 4개)

| 파일명 |
|--------|
| (NEW) 민★사의 매출 206억이 가능했던 이유...md |
| 작은 차이가 '명품'을 만든다, 서울시장후보 김정철의 고려대학교 강연.md |
| ❌-1분만 같이 있어도 느껴지는 '그릇 큰 사람'의 5가지 특징.md |
| (Kor, Chi) 연봉 5천을 버는 사람 vs 10억을 버는 사람, 차이는 이것 단 한 가지입니다.md |

#### → `02_Work/07_References/` (약 11개)

| 파일명 |
|--------|
| 💀 미국🇺🇸이 원유를 수입해야 하는 이유  💀 세계 1위 산유국인데….md |
| 1500억으로 슈친 좀 사주세요.md |
| 3만년 전 영하 40도에서 인류는 어떻게 얼어죽지 않고 잠을 잤을까.md |
| AI가 다 번역 해줄텐데 영어 꼭 배워야 함 (비트겐슈타인).md |
| AI로 딸깍하면 안 되는 이유.md |
| 국내 주식 FOMO.md |
| 로봇이 로봇을 생산하는 시대.md |
| 수학여행 금지.md |
| 석유 생산량 1위 미국이 석유를 수입하는 이유.md |
| 여자 영포티가 결혼을 못 하는 이유｜40대 결혼 시장의 현실.md |
| 주식 개미 투자자가 무조건 망하는 이유  358만 계좌 데이터 분석 결과.md |
| 시총 11위 먹은 월마트의 비결.md |

---

## (b) 새로 만들 폴더 목록

아래 폴더를 새로 생성한다 (`One_thing/` 기준, 순서대로):

```
00_Assets/
01_Personal/
01_Personal/01_Self_Analysis/
01_Personal/02_Mindset_Philosophy/
01_Personal/03_Dev_Python/
01_Personal/04_Lang_English/
01_Personal/05_Reading_Notes/
02_Work/
02_Work/01_Projects/
02_Work/01_Projects/01_소설_아랫것들/
02_Work/01_Projects/02_1인사업기획/
02_Work/02_Content_Creator/
02_Work/03_Business_Ideas/
02_Work/04_Insight_Sources/
02_Work/05_Concepts/
02_Work/06_Thinking_Writing/
02_Work/07_References/
03_Templates/
04_Inbox/
99_Archive/
99_Archive/01_Brain_Dumps/
99_Archive/02_General/
99_Archive/03_Past_Business_Phone/
99_Archive/04_Social_Uploads/
99_Archive/05_Trash_Thoughts/
```

### 이전 완료 후 삭제 예정 폴더

```
raw/00_Inbox/
raw/10_Projects/1인_사업기획/
raw/10_Projects/소설_아랫것들/
raw/10_Projects/            ← 비면 삭제
raw/20_Areas/Dev_Python/
raw/20_Areas/Lang_English/
raw/20_Areas/Mindset_Philosophy/
raw/20_Areas/Self_Analysis/
raw/20_Areas/Thinking_Writing/
raw/20_Areas/               ← 비면 삭제
raw/30_Resources/Business_Ideas/
raw/30_Resources/Concepts/
raw/30_Resources/Content_Creator/
raw/30_Resources/Insight_Sources/
raw/30_Resources/Reading_Notes/
raw/30_Resources/References/
raw/30_Resources/           ← 비면 삭제
raw/40_Archives/Brain_Dumps/
raw/40_Archives/General_Archive/
raw/40_Archives/Past_Business_Phone/
raw/40_Archives/Social_Uploads/
raw/40_Archives/Trash_Thoughts/
raw/40_Archives/            ← 비면 삭제
raw/99_System/Attachments/
raw/99_System/Templates/
raw/99_System/              ← 비면 삭제
raw/                        ← 루트 파일 64개 이동 후 비면 삭제
수집함/                      ← 비면 삭제
```

---

## (c) 이름을 바꿀 파일 목록

### C-1. 이모지/상태 접두어 제거 (파일명 정리)

| 현재 파일명 | 새 파일명 | 이유 |
|-----------|----------|------|
| `❌-1분만 같이 있어도 느껴지는...md` | `1분만 같이 있어도 느껴지는...md` | 이모지 접두어 → 검색 방해 |
| `💀 미국🇺🇸이 원유를 수입해야 하는 이유  💀 세계 1위...md` | `미국이 원유를 수입해야 하는 이유.md` | 이모지 제거 + 중복 표현 정리 |
| `(Kor, Chi) 연봉 5천을 버는 사람...md` | `연봉 5천을 버는 사람 vs 10억을 버는 사람.md` | 언어 태그 제거 (태그로 관리) |
| `(NEW) 민★사의 매출 206억이 가능했던 이유...md` | `민★사의 매출 206억이 가능했던 이유.md` | 상태 접두어 제거 |

### C-2. 날짜 포함 파일명 현황

현재 파일명에 날짜가 포함된 파일: **발견되지 않음**  
(이미지 파일의 `Pasted image 20251208011225.png` 형식은 Obsidian 자동 생성이며 변경 불필요)

### C-3. 향후 날짜 포함 파일 생성 시 준수 형식

```
YYYY_MM_DD_제목.md          예: 2026_05_11_주간회고.md
YYYY_MM_제목.md             예: 2026_05_월간리뷰.md
YYYY_Q1_제목.md             예: 2026_Q2_사업계획.md
```

### C-4. `.txt` → `.md` 변환 권장 파일

`99_System/Attachments/` 내 .txt 파일 4개:

| 현재 파일명 | 새 파일명 | 이동 위치 |
|-----------|----------|----------|
| `자청 글쓰기 4가지 꿀팁.txt` | `자청 글쓰기 4가지 꿀팁.md` | `02_Work/06_Thinking_Writing/` |
| `자청 글쓰기 4가지 꿀팁 1.txt` | `자청 글쓰기 4가지 꿀팁 보완.md` | `02_Work/06_Thinking_Writing/` |
| `자청 표본이론.txt` | `자청 표본이론.md` | `02_Work/05_Concepts/` |
| `모텔이론.txt` | `모텔이론.md` | `02_Work/05_Concepts/` |
| `돈버는 글쓰기 공식.txt` | `돈버는 글쓰기 공식.md` | `02_Work/06_Thinking_Writing/` |

---

## (d) 위반 사항 및 처리 방안

### D-1. 5레벨 초과 (현재 구조)

| 위반 경로 | 레벨 | 처리 방안 |
|---------|------|----------|
| `One_thing/raw/.trash/홍보물 제작 가이드/홍보물 사이즈 모음/파일.md` | 6 | `.trash/`는 Obsidian 관리 폴더 → 건드리지 않음. 신규 구조에서는 발생하지 않음. |
| `One_thing/raw/.trash/R- 독서노트/파일.md` 외 여러 경로 | 5~6 | 동일 — `.trash/` 내부 예외 처리 |

→ **신규 구조에서는 모든 경로가 5레벨 이내.**

### D-2. 모호한 분류

| 대상 | 모호한 이유 | 결정 및 근거 |
|------|-----------|------------|
| `raw/20_Areas/Thinking_Writing/` (48파일) | 개인 글쓰기인지 업무 콘텐츠 제작인지 불명확 | `02_Work/06_Thinking_Writing/`으로 분류. 콘텐츠 제작이 주업이므로 Work. 순수 일기성 글이 있다면 실행 시 `01_Personal/`로 분리 |
| `raw/30_Resources/Concepts/` (9파일) | Resources인지 Work용 개념 정리인지 불명확 | `02_Work/05_Concepts/`로 통합. 콘텐츠 제작용 개념 분석 목적 |
| `수집함/` vs `raw/` 루트의 중복 파일 | `AI가 다 번역 해줄텐데 영어 꼭 배워야 함 (비트겐슈타인).md`가 양쪽에 존재 | 실행 전 내용 비교 후 최신본 1개만 유지, 나머지 삭제 |
| `raw/00_Inbox/` 9개 파일 | 이미 분류됐을 수도, 아닐 수도 | 실행 전 내용 확인: 분류 가능하면 해당 폴더로 직행, 불명확하면 `04_Inbox/`에 임시 보관 |

### D-3. 첨부파일 경로 불일치

| 현상 | 원인 | 처리 방안 |
|------|------|----------|
| `app.json`에 `attachmentFolderPath` 미설정 | Obsidian 기본값 사용 중 (vault 루트에 저장) | 이미지를 `00_Assets/`로 이동 후, Obsidian 설정 → Files & Links → Attachment folder path를 `00_Assets`로 변경 |
| `raw/99_System/Attachments/`에 Pasted image 파일 약 40개 존재 | 과거 다른 설정이었을 때 누적된 파일 | `00_Assets/`로 이동. 이미지를 참조하는 노트가 있을 경우 Obsidian 내부 이동으로 링크 자동 갱신 |

### D-4. `app.json` 설정 변경 필요

| 설정 항목 | 현재 값 | 변경 값 | 이유 |
|---------|--------|--------|------|
| `newFileFolderPath` | `"raw"` | `"04_Inbox"` | `raw/` 폴더 삭제 후 새 파일이 Inbox로 가도록 |
| `attachmentFolderPath` | (없음, 기본값) | `"00_Assets"` | 첨부파일 경로 명시 |

### D-5. 세 자리 넘버링 적용 기준

규칙 6: "100개 이상 쌓일 가능성이 있는 콘텐츠성 폴더는 001_ 사용"

| 폴더 | 이동 후 예상 파일 수 | 판단 |
|------|-----------------|------|
| `01_Personal/02_Mindset_Philosophy/` | ~67개 (55 기존 + raw 루트 12개) | 100+ 가능 → **향후 서브폴더 생성 시 `001_`, `002_` 형식 사용** |
| `02_Work/02_Content_Creator/` | ~71개 (51 기존 + raw 루트 20개) | 100+ 가능 → 동일 |
| `02_Work/03_Business_Ideas/` | ~52개 (47 기존 + 5개) | 경계값 → 우선 두 자리 유지, 초과 시 전환 |

> 현 시점에서는 파일에 넘버링을 붙이지 않음.  
> 해당 폴더에 서브폴더가 필요해지는 시점에 `001_Script/`, `002_Reference/` 형식으로 분류.

### D-6. wiki/ 편입 여부

| 선택지 | 장점 | 단점 |
|-------|------|------|
| 현 위치 유지 (`One_thing/wiki/`) | CLAUDE.md 운영 규칙과 일관성 유지 | 넘버링 체계에서 빠짐 |
| `02_Work/00_Wiki/`로 편입 | 넘버링 체계 통일 | CLAUDE.md 수정 필요, 46개 파일의 링크 재확인 필요 |

**권장: 현 위치 유지.** 재정리 후 CLAUDE.md의 폴더 구조 섹션만 업데이트.

---

## 5. Obsidian 설정 파일 변경 사항 (`app.json`)

재정리 실행 후 `One_thing/.obsidian/app.json`에 아래 내용 추가/변경:

```json
{
  "promptDelete": false,
  "alwaysUpdateLinks": true,
  "newFileLocation": "folder",
  "newFileFolderPath": "04_Inbox",
  "attachmentFolderPath": "00_Assets"
}
```

---

## 6. CLAUDE.md 수정 내용

재정리 실행 후 `CLAUDE.md`의 폴더 구조 섹션을 아래와 같이 업데이트:

**수정 전:**
```
One_thing/
├── raw/              # 원본 자료 (사용자가 추가, Claude는 읽기만)
└── wiki/             # 정리된 지식 (Claude가 작성·관리)
```

**수정 후:**
```
One_thing/
├── 00_Assets/        # 이미지·첨부파일
├── 01_Personal/      # 개인 학습·자기분석 (사용자가 추가, Claude는 읽기만)
├── 02_Work/          # 콘텐츠 제작·프로젝트 (사용자가 추가, Claude는 읽기만)
├── 03_Templates/     # 옵시디언 템플릿
├── 04_Inbox/         # 임시 캡처 (처리 후 분류)
├── 99_Archive/       # 종료 프로젝트·오래된 기록
└── wiki/             # 정리된 지식 (Claude가 작성·관리)
```

---

## 7. 실행 순서 (검토 후 진행)

```
Step 1  git commit — 현 상태 스냅샷 저장
Step 2  새 폴더 생성 — 섹션 (b) 목록 순서대로
Step 3  폴더 단위 이동 — A-1 매핑 테이블 순서대로 (Obsidian 파일 탐색기 사용)
Step 4  99_System/Attachments/ 분리 — A-2 기준으로 유형별 이동
Step 5  raw/ 루트 64개 파일 분류 — A-3 기준으로 이동
Step 6  .txt → .md 변환 — C-4 목록
Step 7  파일명 변경 — C-1 목록 (이모지·접두어 제거)
Step 8  중복 파일 제거 — 수집함/ vs raw/ 루트 동명 파일 확인 후 정리
Step 9  빈 폴더 삭제 — raw/, 수집함/ 등
Step 10 app.json 업데이트 — 섹션 5 내용 반영
Step 11 CLAUDE.md 업데이트 — 섹션 6 내용 반영
Step 12 링크 검증 — Obsidian 그래프 뷰 및 깨진 링크 플러그인으로 확인
Step 13 git commit — 재정리 완료 커밋
```

---

## 8. 미결 사항 (실행 전 확인 필요)

- [ ] `수집함/AI가 다 번역 해줄텐데 영어 꼭 배워야 함 (비트겐슈타인).md`와 `raw/` 루트 동명 파일 내용 비교 → 최신본 1개만 유지
- [ ] `raw/20_Areas/Thinking_Writing/` 48개 파일 내 순수 일기·성찰 글 확인 → 해당 파일은 `01_Personal/`로 분리
- [ ] `raw/00_Inbox/` 9개 파일 내용 확인 → 이미 분류 가능한 파일은 해당 폴더로 직행
- [ ] 이미지 파일(`Pasted image...`)을 참조하는 노트 존재 여부 확인 → Obsidian 내부 이동으로 링크 자동 갱신 확인
- [ ] `wiki/` 현 위치 유지 여부 최종 결정
- [ ] `.trash/` 경로가 Obsidian 기본 경로(`One_thing/.trash/`)인지 확인 — 이동 금지
```
