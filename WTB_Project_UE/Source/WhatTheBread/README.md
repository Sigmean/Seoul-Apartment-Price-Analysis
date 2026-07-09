# Source/WhatTheBread 구조 가이드

언리얼 C++ 모듈은 `Public/`(헤더)과 `Private/`(구현)를 분리하는 것이 표준입니다.
다른 모듈/플러그인에서 이 클래스를 참조해야 하면 `Public`에, 내부에서만 쓰면
`Private`에 두면 됩니다 (블루프린트에서만 쓸 거면 대부분 `Public`에 헤더를 둡니다).

```
Source/WhatTheBread/
├── WhatTheBread.Build.cs      # 모듈 빌드 설정 (에디터가 프로젝트 생성 시 자동 생성)
├── Public/
│   ├── Data/                  # UDataAsset, FTableRowBase 구조체 등 (예: UIngredientData.h)
│   ├── Systems/                # 게임 로직 인터페이스/베이스 클래스
│   └── UI/                      # UUserWidget 상속 C++ 베이스 클래스
└── Private/
    ├── Data/                     # 위 헤더의 .cpp 구현
    ├── Systems/
    └── UI/
```

## 블루프린트 vs C++ 역할 분담 (실무 관례)
- **C++**: 성능이 중요하거나 재사용되는 코어 로직 (오븐 타이머, 인벤토리 데이터 구조,
  멀티플레이 리플리케이션 등) — `Source/` 쪽
- **블루프린트**: 레벨 디자이너/기획자가 직접 수치를 조정하거나 비주얼 스크립팅이
  편한 부분 (연출, UI 배치, 손님 스폰 타이밍 등) — `Content/_Game/Blueprints/` 쪽
- 일반적인 패턴: **C++로 베이스 클래스를 만들고, 블루프린트로 상속받아 디테일 조정**
  (예: `ACatCharacterBase` (C++) → `BP_Cat_Tabby`, `BP_Cat_Sphynx` (블루프린트))

## 참고
1인 개발이고 블루프린트 위주로 작업하실 계획이면 `Source/` 폴더는 최소한만
채우고(예: 데이터 구조, 세이브 시스템 정도) 나머지는 블루프린트로 진행하는 것도
충분히 실무에서 쓰는 전략입니다.
