# What The Bread (WTB) — Unreal Engine

3D 협동 베이커리 시뮬레이션 · Unreal Engine · Steam 출시 예정

## 📁 폴더 구조

```
WTB_Project/
├── WhatTheBread.uproject   # 언리얼 프로젝트 파일 (에디터에서 프로젝트 생성 시 자동 생성됨)
├── Config/                 # DefaultEngine.ini, DefaultGame.ini 등 프로젝트 설정
├── Content/                # 게임에서 쓰는 모든 애셋 (블루프린트, 메시, 텍스처, 맵 등)
│   ├── _Game/              # 우리 팀이 만든 애셋 전부
│   └── ThirdParty/         # 마켓플레이스 / 외부 애셋
├── Source/                 # C++ 코드 (블루프린트만 쓸 거면 비어있어도 됨)
│   └── WhatTheBread/
│       ├── Public/         # 헤더 (.h)
│       └── Private/        # 구현 (.cpp)
├── Plugins/                # 커스텀/서드파티 플러그인
├── Docs/                   # 기획 문서
├── DevLog/                 # 일자별 개발일지
└── .gitignore
```

> **Binaries/, Intermediate/, Saved/, DerivedDataCache/** 폴더는 언리얼 에디터가
> 프로젝트를 열 때 자동으로 생성합니다. 깃허브에는 올리지 않으므로(.gitignore 처리)
> 이 zip 안에는 포함되어 있지 않습니다.

## 🔧 개발 환경
- Unreal Engine (5.x)
- Firebase 또는 Unreal 자체 세이브 시스템 (검토 필요 — Firebase REST 연동 or GameplayAbilitySystem+SaveGame)
- Blender + Meshy AI (3D 에셋)
- Git / GitHub (대용량 바이너리는 Git LFS 권장)

## ⚠️ Git LFS 필수
언리얼은 메시, 텍스처, 사운드 등 바이너리 파일이 매우 커서 일반 git으로 관리하면
저장소가 금방 무거워집니다. 아래 확장자는 Git LFS로 관리하는 걸 강력 추천합니다.
`*.uasset`, `*.umap`, `*.fbx`, `*.wav`, `*.png`, `*.tga`
(자세한 설정은 `.gitattributes` 참고)
