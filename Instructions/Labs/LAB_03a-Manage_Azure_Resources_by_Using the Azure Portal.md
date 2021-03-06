﻿---
lab:
    title: '03a - Azure Portal을 사용하여 Azure 리소스 관리'
    module: '모듈 03 - Azure 관리'
---

# 랩 03a - Azure Portal을 사용하여 Azure 리소스 관리
# 학생 랩 매뉴얼

## 랩 시나리오

리소스 그룹 간 리소스 이동을 비롯해 리소스 그룹에 기반하여 리소스를 프로비전하고 구성하는 것과 관련된 기본 Azure 관리 기능을 탐색해야 합니다. 또한 디스크 리소스가 실수로 삭제되지 않도록 보호하는 동시에 성능 특성 및 크기를 수정할 수 있는 옵션을 탐색하고자 합니다.

## 목적

이 랩에서는 다음과 같이 다룹니다.

+ 작업 1: 리소스 그룹을 만들고 리소스 그룹에 리소스를 배포
+ 작업 2: 리소스 그룹 간에 리소스 이동
+ 작업 3: 리소스 잠금 구현 및 테스트

## 예상 시간: 20분

## 지침

### 연습 1

#### 작업 1: 리소스 그룹을 만들고 리소스 그룹에 리소스를 배포

이 작업에서는 Azure Portal을 사용하여 리소스 그룹을 만들고 리소스 그룹에 디스크를 만듭니다.

1. [Azure Portal](https://portal.azure.com)에 로그인합니다.

1. **리소스 그룹**을 검색하여 선택합니다. 

1. **리소스 그룹** 블레이드에서 **+ 추가**를 클릭하고 다음 설정을 사용하여 리소스 그룹을 만듭니다.

    |설정|값|
    |---|---|
    |구독| 이 랩에서 사용할 Azure 구독의 이름 |
    |리소스 그룹| **az104-03a-rg1**|
    |영역| 이 랩에서 사용할 구독에서 사용할 수 있는 Azure 지역의 이름 |

1. **검토+만들기**를 클릭한 다음 **만들기**를 클릭합니다.

1. Azure Portal에서 **디스크**를 검색하여 선택하고 **+ 추가**를 클릭한 후 다음 설정을 지정합니다.

    |설정|값|
    |---|---|
    |구독| 리소스 그룹을 만든 Azure 구독의 이름 |
    |리소스 그룹| **az104-03a-rg1** |
    |디스크 이름| **az104-03a-disk1** |
    |영역| 리소스 그룹을 만든 Azure 영역 이름 |
    |가용성 영역| **없음** |
    |원본 유형| **없음** |

    >**참고**: 리소스를 만들 때 새 리소스 그룹을 만들거나 기존 리소스 그룹을 사용할 수 있습니다.

1. 디스크 유형과 크기를 각각 **표준 HDD** 및 **32 GiB**로 변경합니다.

1. **검토+만들기**를 클릭한 다음 **만들기**를 클릭합니다.

    >**참고**: 디스크가 만들어질 때까지 기다립니다. 1분 미만이면 이 작업을 수행할 수 있습니다.

#### 작업 2: 리소스 그룹 간에 리소스 이동 

본 작업에서는 이전 작업에서 만든 디스크 리소스를 새 리소스 그룹으로 이동합니다. 

1. **리소스 그룹**을 검색하여 선택합니다. 

1. **리소스 그룹** 블레이드에서 이전 작업에서 만든 **az104-03a-rg1** 리소스 그룹을 나타내는 항목을 클릭합니다.

1. 리소스 그룹의 **개요** 블레이드에서 리소스 그룹 리소스 목록 중 새로 만든 디스크를 나타내는 항목을 선택하고 도구 모음에서 **이동**을 클릭하고 드롭다운 목록에서 **다른 리소스 그룹으로 이동**을 선택합니다.

    >**참고**: 이 방법으로 동시에 여러 리소스를 이동할 수 있습니다. 

1. **리소스 이동** 블레이드에서 **새 그룹 만들기**를 클릭합니다.

1. **리소스 그룹** 텍스트 상자에서 **az104-03a-rg2**를 입력하고 **새 리소스 ID를 사용하려는 경우 이동한 리소스와 연결된 도구 및 스크립트를 업데이트하지 않으면 정상적으로 작동하지 않는다는 점을 이해합니다**. 확인란을 선택하고 **확인**을 클릭합니다.

    >**참고**: 이동이 완료될 때까지 기다리지 말고 다음 작업을 진행합니다. 이동은 약 10분이 소요될 수 있습니다. 원본 또는 대상 리소스 그룹의 활동 로그 항목을 모니터링하여 작업이 완료되었는지 확인할 수 있습니다. 다음 작업을 완료하면 이 단계를 다시 수행합니다.

#### 작업 3: 리소스 잠금 구현

이 작업에서는 디스크 리소스를 포함하는 Azure 리소스 그룹에 리소스 잠금을 적용합니다.

1. Azure Portal에서 **디스크**를 검색하여 선택하고 **+ 추가**를 클릭한 후 다음 설정을 지정합니다.

    |설정|값|
    |---|---|
    |구독| 이 랩에서 사용 중인 구독 이름 |
    |리소스 그룹| 새 리소스 그룹 **az104-03a-rg3**의 이름 |
    |디스크 이름| **az104-03a-disk2** |
    |영역| 본 랩에서 다른 리소스 그룹을 만든 Azure 지역의 이름 |
    |가용성 영역| **없음** |
    |원본 유형| **없음** |

1. 디스크 유형과 크기를 각각 **표준 HDD** 및 **32 GiB**로 설정합니다.

1. **검토+만들기**를 클릭한 다음 **만들기**를 클릭합니다.

1. Azure Portal에서 **리소스 그룹**을 검색하고 선택합니다. 

1. 리소스 그룹 목록에서 **az104-03a-rg3** 리소스 그룹을 나타내는 항목을 클릭합니다.

1. **az104-03a-rg3** 리소스 그룹 블레이드에서 **잠금**을 클릭하고 다음 설정으로 잠금을 추가합니다.

    |설정|값|
    |---|---|
    |잠금 이름| **az104-03a-delete-lock** |
    |잠금 유형| **삭제** |

1. **az104-03a-rg3** 리소스 그룹 블레이드에서 **개요**를 클릭하고 리소스 그룹 리소스 목록에서 이 작업의 앞에서 만든 디스크를 나타내는 항목을 선택하고 도구 모음에서 **삭제**를 클릭합니다. 

1. **선택한 모든 리소스를 삭제하시겠습니까?** 라는 메시지가 표시되면 **삭제 확인** 텍스트 상자에서 **예**를 입력하고 **삭제**를 클릭합니다.

1. 작업을 삭제하지 못했음을 알리는 오류 메시지가 표시됩니다. 

    >**참고**: 오류 메시지에 표시된 대로, 리소스 그룹 수준에 적용된 삭제 잠금으로 인한 것으로 예상됩니다.

1. **az104-03a-rg3** 리소스 그룹의 리소스 목록으로 돌아가 **az104-03a-disk2** 리소스를 나타내는 항목을 클릭합니다. 

1. **az104-03a-disk2** 블레이드의 **설정** 섹션에서 **구성**을 클릭하고 디스크 유형과 크기를 각각 **프리미엄 SSD** 및 **64 GiB**로 설정하고 변경 내용을 저장합니다. 변경이 성공했는지 확인합니다.

    >**참고**: 리소스 그룹 수준 잠금은 삭제 작업에만 적용되므로 변경이 예상됩니다. 

#### 리소스 정리

   >**참고**: 이 랩에 배포된 리소스는 삭제하지 마세요. 이 모듈의 다음 랩에서 사용해야 합니다. 이 랩에서 만든 리소스 잠금만 제거합니다.

1. **az104-03a-rg3** 리소스 그룹 블레이드로 이동하여 **잠금** 블레이드를 표시하고 **삭제** 잠금 항목의 오른쪽에 있는 **삭제** 링크를 클릭하여 잠금 **az104-03a-delete-lock**을 제거합니다.

#### 리뷰

이 랩에서는 다음 작업을 했습니다.

- 리소스 그룹을 만들고 리소스 그룹에 리소스 배포
- 리소스 그룹 간 리소스 이동
- 리소스 잠금 구현 및 테스트