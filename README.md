# 한국 정당 관점 시뮬레이션 프롬프트 템플릿

대한민국 주요 정당의 공식 입장·강령·정책·공약·의정활동을 조사하여,  
LLM이 특정 정당의 관점에서 글을 쓸 수 있도록 설계된 **정당 관점 시뮬레이션 프롬프트** 저장소입니다.

---

## 목적

- 각 정당의 공식 입장과 실제 정치적 행태를 구분해 정리한다.
- 정당의 핵심 가치, 정책 우선순위, 지지층, 정치적 언어 습관을 구조화한다.
- 최신 자료 기준으로 업데이트 가능한 정당별 프롬프트를 만든다.
- 확인되지 않은 추정, 풍문, 편향적 평가를 배제한다.
- LLM이 특정 정당의 관점에서 글을 쓰되, 사실과 의견을 구분하도록 만든다.

> **이 저장소는 특정 정당을 홍보하거나 비난하지 않습니다.**  
> 모든 자료는 공식 출처 기반이며, 분석자의 해석과 공식 입장을 구분합니다.

---

## 레포 구조

```
political-ideology-prompts-kr/
├── README.md                         ← 이 파일
├── templates/
│   ├── party-research-prompt.md      ← 정당 조사 프롬프트 템플릿
│   ├── party-simulation-prompt.md    ← 정당 시뮬레이션 프롬프트 템플릿
│   └── party-metadata.schema.yaml    ← 메타데이터 YAML 스키마
├── parties/
│   ├── minjoo/                       ← 더불어민주당
│   │   ├── research.md
│   │   ├── prompt.md
│   │   └── metadata.yaml
│   ├── ppp/                          ← 국민의힘
│   │   ├── research.md
│   │   ├── prompt.md
│   │   └── metadata.yaml
│   ├── rebuilding-korea/             ← 조국혁신당
│   │   ├── research.md
│   │   ├── prompt.md
│   │   └── metadata.yaml
│   └── gaehyeok/                     ← 개혁신당
│       ├── research.md
│       ├── prompt.md
│       └── metadata.yaml
└── sources/
    └── source-policy.md              ← 출처 사용 원칙
```

---

## 포함된 정당 (2026년 5월 기준)

| 정당명 | 슬러그 | 의석수 | 교섭단체 | 조사 기준일 |
|--------|--------|--------|----------|-------------|
| 더불어민주당 | `minjoo` | 175석 | O | 2026-05-24 |
| 국민의힘 | `ppp` | 108석 | O | 2026-05-24 |
| 조국혁신당 | `rebuilding-korea` | 12석 | X | 2026-05-24 |
| 개혁신당 | `gaehyeok` | 3석 | X | 2026-05-24 |

> 의석수는 22대 총선(2024년 4월) 결과 기준이며, 보궐선거·탈당·입당으로 변동될 수 있습니다.

---

## 파일 역할

### `templates/`

| 파일 | 역할 |
|------|------|
| `party-research-prompt.md` | LLM에 정당 조사를 지시하는 프롬프트 템플릿. 변수(`{PARTY_NAME}` 등)를 채워 사용. |
| `party-simulation-prompt.md` | 조사 결과를 바탕으로 정당 관점 시뮬레이션을 수행하는 시스템 프롬프트 템플릿. |
| `party-metadata.schema.yaml` | `parties/*/metadata.yaml`이 따라야 하는 YAML 스키마 정의. |

### `parties/{slug}/`

| 파일 | 역할 |
|------|------|
| `research.md` | 정당 기본 정보, 이념, 정책 입장, 문체 분석, 지지 기반 조사 보고서. |
| `prompt.md` | 해당 정당 관점에서 글을 쓰도록 LLM에 제공하는 완성된 시스템 프롬프트. |
| `metadata.yaml` | 정당 식별 정보, 출처, 신뢰도, 업데이트 이력. |

---

## 사용 방법

### 1. 기존 정당 프롬프트 바로 사용

`parties/{slug}/prompt.md` 파일을 LLM의 시스템 프롬프트로 사용합니다.

```
# 예: 더불어민주당 관점 시뮬레이션
cat parties/minjoo/prompt.md
```

### 2. 새 정당 추가

1. `templates/party-research-prompt.md`의 변수를 채워 LLM에 조사를 지시합니다.
2. 조사 결과를 `parties/{slug}/research.md`에 저장합니다.
3. `templates/party-simulation-prompt.md`의 변수를 채워 `parties/{slug}/prompt.md`를 만듭니다.
4. `templates/party-metadata.schema.yaml`을 참고해 `parties/{slug}/metadata.yaml`을 작성합니다.

### 3. 업데이트

- `metadata.yaml`의 `last_checked` 날짜를 확인합니다.
- 지도부·의석수·주요 입장이 변경되었으면 `research.md`와 `prompt.md`를 수정합니다.
- `update_notes`에 변경 이력을 추가합니다.

---

## 조사 원칙 요약

1. **최신성**: 조사 기준일 기준으로 정당명, 지도부, 의석수, 교섭단체 여부를 확인합니다.
2. **출처 우선순위**: 공식 홈페이지 → 선관위 → 국회 공개자료 → 공신력 있는 언론 → 학술자료 순서.
3. **사실·해석 분리**: "공식 입장"과 "분석자의 해석"을 구분합니다.
4. **과잉 일반화 금지**: 한 정치인의 발언을 정당 전체 입장으로 단정하지 않습니다.
5. **불확실성 표시**: 확인되지 않은 항목은 별도로 표시합니다.

자세한 원칙은 [`templates/party-research-prompt.md`](templates/party-research-prompt.md)를 참고하세요.

---

## 기여 방법

- 오래된 정보 수정: `research.md`와 `metadata.yaml`의 `last_checked`를 업데이트합니다.
- 새 정당 추가: 위 "새 정당 추가" 절차를 따릅니다.
- 출처 정책 변경: `sources/source-policy.md`를 수정합니다.

---

## 라이선스 및 주의사항

이 저장소의 모든 프롬프트와 조사 자료는 **교육·연구·언론 목적**으로만 사용합니다.  
특정 정당의 선거 운동, 홍보, 비방에 사용하지 않습니다.  
각 정당 공식 자료의 저작권은 해당 정당에 있습니다.
