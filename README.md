# Obsidian CS Vault Generator

YAML 스펙 파일을 기반으로 **Obsidian Computer Science Knowledge Graph Vault 구조를 자동 생성하는 Python 도구**입니다.

이 프로젝트는 컴퓨터공학 전공 지식을 **Graph 기반 Knowledge System**으로 정리하기 위한 Obsidian Vault 구조를 자동으로 생성하기 위해 만들어졌습니다.

폴더 구조, Markdown 노트, 템플릿 등을 YAML 문서로 정의하면 Python 스크립트가 이를 읽어 Obsidian Vault 내부에 자동으로 생성합니다.

---

# 목적

컴퓨터공학 전공 노트를 단순한 교재 요약이 아니라 다음과 같은 **Knowledge Graph 형태**로 구축하는 것을 목표로 합니다.

- 개념 중심 노트 구조
- Obsidian Graph View 활용
- 학부 ~ 대학원 수준 CS Knowledge Base 구축
- 알고리즘 / 시스템 / 네트워크 / DB / AI 등 전공 전반 연결

예시 구조

```

CS
├─ 00_HOME
├─ 01_CONCEPTS
│  ├─ algorithms
│  ├─ systems
│  ├─ theory
│  ├─ ai_ml
│  └─ math_foundations
├─ 02_MOC
├─ 03_COURSES
├─ 04_REFERENCES
├─ 05_PROOFS_AND_DERIVATIONS
├─ 06_IMPLEMENTATIONS
├─ 07_LABS_AND_EXPERIMENTS
└─ 99_INBOX

```

---

# 주요 기능

## 1. Obsidian Vault 폴더 자동 생성

YAML에 정의된 구조를 기반으로 폴더를 생성합니다.

예

```

01_CONCEPTS/systems
01_CONCEPTS/algorithms
02_MOC
03_COURSES

```

---

## 2. Markdown 노트 자동 생성

다음과 같은 노트 타입을 자동 생성할 수 있습니다.

- Concept Note
- MOC (Map of Content)
- Course Note
- Reference Note
- Home Note

---

## 3. 템플릿 기반 노트 생성

각 노트는 기본 템플릿을 기반으로 생성됩니다.

예: Concept Note

```

---

type: concept
domain: systems
topics: [concurrency]
---------------------

# mutex

## Definition

## Intuition

## Key Properties

## Common Pitfalls

```

---

## 4. 덮어쓰기 방지

기존 노트가 존재하면 자동으로 **생성을 건너뜁니다.**

옵션을 통해 기존 파일을 덮어쓰는 것도 가능합니다.

---

## 5. Obsidian Knowledge Graph 구축 지원

이 도구로 생성된 구조는 Obsidian의 Graph View에서 **지식 네트워크 형태로 연결되는 노트 구조**를 만들 수 있도록 설계되었습니다.

예

```

Operating System
├ Process
│   └ Thread
├ CPU Scheduling
├ Memory Management
│   └ Virtual Memory
└ File System

```

---

# 프로젝트 구조

```

obsidian-cs-vault-generator
│
├─ generate.py
├─ templates
│  ├─ concept.md
│  ├─ moc.md
│  ├─ reference.md
│  └─ home.md
│
└─ examples
└─ spec_cs.yaml

```

---

# 설치 방법

Python 3.9 이상을 권장합니다.

가상환경 생성

```

python3 -m venv .venv

```

가상환경 활성화

```

source .venv/bin/activate

```

필요 패키지 설치

```

pip install pyyaml

````

---

# 사용 방법

## 1. YAML 스펙 파일 작성

예

```yaml
vault_root: "/Users/jinius36/Documents/Obsidian Vault/CS"

folders:
  - "00_HOME"
  - "01_CONCEPTS/algorithms"
  - "01_CONCEPTS/systems"
  - "02_MOC"

files:
  - path: "00_HOME/HOME.md"
    template: "home"
    vars:
      title: "CS HOME"

  - path: "02_MOC/MOC_CS.md"
    template: "moc"
    vars:
      title: "MOC: Computer Science"

  - path: "01_CONCEPTS/systems/mutex.md"
    template: "concept"
    vars:
      title: "mutex"
      domain: "systems"
````

---

## 2. 생성 실행

```
python generate.py examples/spec_cs.yaml
```

---

## 3. 생성 결과

지정된 Vault 경로에 폴더와 Markdown 노트가 자동으로 생성됩니다.

예

```
/Users/.../Obsidian Vault/CS
```

내부 구조

```
00_HOME
01_CONCEPTS
02_MOC
03_COURSES
```

---

# 추천 사용 방식

다음 workflow를 권장합니다.

1. YAML로 Knowledge Graph 구조 설계
2. Python Generator 실행
3. Obsidian에서 노트 작성 및 확장
4. Graph View를 통해 지식 연결 확인

---

# 향후 개선 예정

* 파일명 자동 slug 생성
* Concept 간 자동 링크 생성
* MOC 자동 업데이트
* Dry-run 모드
* CLI 옵션 확장

---

# License

MIT License