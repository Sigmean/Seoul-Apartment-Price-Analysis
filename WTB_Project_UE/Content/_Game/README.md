# Content/_Game 구조 가이드 (Unreal 컨텐츠 브라우저 기준)

## 왜 `_Game` 폴더로 감싸나요?
언리얼 컨텐츠 브라우저는 알파벳순 정렬됩니다. 마켓플레이스 애셋(`ThirdParty`)이나
플러그인 콘텐츠와 우리 팀 애셋이 섞이면 찾기 힘들어지므로, 언더바를 붙여
항상 맨 위로 오게 하는 것이 Epic 공식 권장사항이자 실무 표준입니다.
(Epic 공식 가이드: "Unreal Engine Directory Structure" 참고)

```
Content/
├── _Game/                  ← 우리 팀 애셋 전부 (항상 최상단 정렬)
│   ├── Blueprints/          # 로직 블루프린트 (기능별 하위 폴더)
│   │   ├── Core/             # GameMode, GameState, PlayerController 등
│   │   ├── Characters/        # 캐릭터 블루프린트 (BP_CatBase 등)
│   │   └── Systems/            # Cooking / Customer / Inventory / RushTime
│   ├── Characters/          # 캐릭터 관련 애셋 (스켈레탈 메시, 리그, 애님)
│   │   ├── Cats/
│   │   └── Customers/
│   ├── Maps/                # 레벨(.umap) 파일
│   ├── UI/                  # UMG 위젯 + UI 전용 텍스처
│   ├── Materials/           # 머티리얼 / 머티리얼 인스턴스
│   ├── Textures/            # 일반 텍스처
│   ├── Meshes/               # 스태틱 메시 (Props / Environment)
│   ├── Animations/            # 애니메이션 시퀀스, 몽타주, 블렌드 스페이스
│   ├── Audio/                 # 사운드 큐, 웨이브
│   ├── Data/                   # DataTable, DataAsset, Curve 등
│   └── FX/                      # 나이아가라/파티클 이펙트
└── ThirdParty/               # 마켓플레이스 / 외부 플러그인 콘텐츠 (수정 금지, 원본 유지)
```

## 폴더 구성 방식: 타입별 vs 기능별
언리얼 프로젝트도 Unity와 마찬가지로 두 방식이 갈립니다.

- **타입별 (지금 이 구조)**: `Blueprints/`, `Meshes/`, `Materials/`처럼 애셋 종류로 먼저 나누고
  그 안에서 기능별 하위 폴더. 1인/소규모 개발, 애셋 수가 아직 적을 때 추천.
- **기능별**: `Content/_Game/Cooking/` 폴더 하나에 그 기능의 블루프린트+메시+머티리얼+
  애니메이션을 전부 몰아넣는 방식. 팀이 커지고 기능이 많아지면 이 쪽으로 전환 고려.

> 지금 1인 개발 + 6~7개월 일정이면 타입별로 시작 → 특정 시스템(예: Cooking)이
> 애셋이 너무 많아지면 그 부분만 기능별 폴더로 분리하는 걸 추천합니다.

## 네이밍 컨벤션 (Unreal 공식 접두사 표준)
언리얼은 애셋 타입을 파일명 접두사로 구분하는 게 사실상 표준입니다.
컨텐츠 브라우저에서 섬네일만 봐도 무슨 애셋인지 바로 알 수 있어서 꼭 지키는 걸 추천해요.

| 접두사 | 애셋 종류 | 예시 |
| --- | --- | --- |
| `BP_` | 블루프린트 클래스 | `BP_CatBase`, `BP_OvenActor` |
| `WBP_` | 위젯 블루프린트 (UI) | `WBP_MainHUD`, `WBP_RushTimeResult` |
| `M_` | 머티리얼 | `M_BreadCrust` |
| `MI_` | 머티리얼 인스턴스 | `MI_BreadCrust_Golden` |
| `T_` | 텍스처 | `T_BreadCrust_D` (Diffuse), `T_BreadCrust_N` (Normal) |
| `SM_` | 스태틱 메시 | `SM_DisplayShelf` |
| `SK_` | 스켈레탈 메시 | `SK_Cat_Tabby` |
| `A_` | 애니메이션 시퀀스 | `A_Cat_Knead` |
| `AM_` | 애니메이션 몽타주 | `AM_Cat_Serve` |
| `DT_` | 데이터 테이블 | `DT_IngredientTable` |
| `DA_` | 데이터 애셋 | `DA_Ingredient_Flour` |
| `S_` | 사운드 큐/웨이브 | `S_Oven_Timer` |
| `NS_` | 나이아가라 시스템 | `NS_FlourPuff` |
| `L_` (or 그냥 이름) | 레벨/맵 | `L_MainBakery`, `L_Tutorial` |

## Unity → Unreal 데이터 구조 참고
전에 보내주신 `IngredientData.cs`(Unity ScriptableObject)는 언리얼에서는
`UDataAsset` 상속 클래스(C++) 또는 `DataTable`(FTableRowBase 구조체)로
대응됩니다. C++ 코드로 옮길 때는 `Source/WhatTheBread/Public/Data/` 쪽을 참고하세요.
