# CLAUDE.md 구조 옵션 — 두 변형 비교

목표: **공통 협업 규칙을 단일 소스로 두고 여러 프로젝트에 재사용**하되, 프로젝트별로 `@` import로 **선택적 opt-in**(쓰기 싫으면 import 한 줄 제거)한다. 여기 두 변형을 나란히 두고 비교 후 채택한다.

공통점: 둘 다 **import 방식**이고, 공통규칙 본문(`collaboration-rules` / 루트 `CLAUDE.md`)은 **동일 텍스트**다. *무엇이 루트 `CLAUDE.md`에 오느냐*만 뒤집힌다.

## A — 규칙이 루트 (`A-rules-at-root/`)

```
CLAUDE.md                ← 공통 협업 규칙 본문 + @docs/project-info.md
docs/project-info.md     ← init 산출물(프로젝트 정보)
```

- 루트 `CLAUDE.md` = 공통규칙. 프로젝트 정보는 `docs/`로 내려 import.
- **장점**: 공통규칙이 가장 앞·항상 로드. 규칙 중심 레포(하네스 자체)에 자연스럽다.
- **단점**: `claude init`이 루트 `CLAUDE.md`를 프로젝트 정보로 덮어쓰는 컨벤션과 어긋난다. init 재실행 시 충돌 주의.

## B — 정보가 루트 (`B-info-at-root/`)

```
CLAUDE.md                     ← 프로젝트 정보 본문 + @docs/collaboration-rules.md
docs/collaboration-rules.md   ← 공통 협업 규칙(배포용 단일 소스)
```

- 루트 `CLAUDE.md` = 프로젝트 정보(`claude init` 컨벤션 그대로). 공통규칙은 `docs/`에서 import.
- **장점**: init 컨벤션과 일치. 프로젝트 정보가 1급 시민. 공통규칙 끄기 = import 한 줄 제거로 명확.
- **단점**: 공통규칙이 본문 아래로 밀려 시야에서 덜 부각.

## 배포(복붙) 절차 — 두 변형 공통

1. 공통규칙 파일(`collaboration-rules.md` / A의 경우 루트 규칙 블록)을 대상 프로젝트에 복사.
2. 대상 `CLAUDE.md`에 `@<상대경로>/collaboration-rules.md` 한 줄 추가.
3. 끄고 싶으면 그 import 줄만 제거.
4. 규칙 업데이트 시 → 각 프로젝트에 **다시 복사**(복붙 방식의 트레이드오프). 단일 소스 참조(`@~/...`)로 가면 전파는 되나 레포 자기완결성이 깨진다.

## 선택 기준

- **이 하네스 레포처럼 규칙이 곧 산출물** → A가 자연스럽다.
- **일반 프로젝트에 규칙을 얹는 용도** → `claude init`과 안 싸우는 **B 권장**.
