# 사용법 — 공통규칙 import 예시

공통 협업 규칙(`docs/collaboration-rules.md`)을 프로젝트에 끌어 쓰는 방법. 핵심은 **CLAUDE.md 최상단에 import 한 줄**이다.

## 1. 파일 배치

```
<프로젝트 루트>/
├─ CLAUDE.md                     ← 프로젝트 정보 (import 한 줄 추가)
└─ docs/
   └─ collaboration-rules.md     ← 이 규칙 파일을 복사해 둠
```

## 2. CLAUDE.md 최상단에 import 추가

제목 바로 아래에 `@<상대경로>` 한 줄을 넣는다. **위 배치(`docs/`)면 경로는 `@docs/collaboration-rules.md`.**

```markdown
# CLAUDE.md

@docs/collaboration-rules.md

## 개요 (Overview)
이 프로젝트가 무엇이고 왜 존재하는지...

## 빌드 · 실행 · 테스트
...
```

## 3. 경로는 배치 위치에 맞춘다

import 경로는 **CLAUDE.md 기준 상대경로**다.

| 규칙 파일 위치 | import 줄 |
| --- | --- |
| `docs/collaboration-rules.md` | `@docs/collaboration-rules.md` |
| 루트 `collaboration-rules.md` | `@collaboration-rules.md` |
| `.claude/collaboration-rules.md` | `@.claude/collaboration-rules.md` |

## 4. 끄기 / 갱신

- **끄기**: import 줄만 지운다 (규칙 본문은 안 건드림).
- **갱신**: `collaboration-rules.md`만 고치면 import한 모든 곳에 반영. 복붙 배포면 각 프로젝트에 파일을 **다시 복사**해야 한다.

## 주의 — `/init`은 import를 자동으로 안 넣는다

`/init`은 코드베이스를 분석해 CLAUDE.md를 **새로 덮어쓴다**. 규칙 파일에 지시를 박아도 읽지 않으므로 import는 **손으로** 넣어야 한다. 이미 import가 든 CLAUDE.md에 `/init`을 다시 돌리면 import가 날아갈 수 있으니, init 후 한 줄을 다시 확인한다.
