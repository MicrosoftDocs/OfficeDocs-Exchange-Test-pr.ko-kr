---
title: '계층 구조 주소록: Exchange 2013 Help'
TOCTitle: 계층 구조 주소록
ms:assetid: a1d277a0-5437-40af-aade-e4730a0d1308
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff629379(v=EXCHG.150)
ms:contentKeyID: 50483779
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 계층 구조 주소록

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-03-26_

HAB(계층 구조 주소록)를 사용하면 최종 사용자가 조직 계층 구조를 사용하여 주소록에서 받는 사람을 찾을 수 있습니다. 일반적으로 사용자는 기본 GAL(전체 주소록) 및 해당 받는 사람 속성만 사용할 수 있습니다. 또한 GAL의 구조가 조직 내 받는 사람의 관리 또는 연공서열 관계를 반영하지 않을 때도 있습니다. 조직의 고유 비즈니스 구조에 매핑되는 HAB를 사용자 지정할 수 있게 되면 사용자는 내부에서 받는 사람을 효과적으로 찾을 수 있습니다.

## 계층 구조 주소록 사용

HAB에서 루트 조직(예를 들어, Contoso, Ltd)은 최상위 층으로 사용됩니다. 이 최상위 층에서 몇몇 하위 층을 추가하여 부, 부서 또는 지정할 다른 조직 층으로 세그먼트화된 사용자 지정된 HAB를 만들 수 있습니다. 다음 그림에서는 다음 구조를 가진 Contoso, Ltd의 HAB에 대해 설명합니다.

  - 최상위 층은 루트 조직 Contoso, Ltd를 나타냅니다.

  - 두 번째 수준의 하위 층에는 Contoso, Ltd 내의 영업부인 회사 사무실, 제품 지원 조직 및 판매 & 마케팅 조직이 포함됩니다.

  - 세 번째 수준의 하위 층에는 회사 사무실 내의 부서인 인사, 회계 그룹 및 관리 그룹의 세 가지 하위 그룹이 포함됩니다.

**Contoso, Ltd의 예제 HAB**

![계층 구조 주소록 대화 상자](images/Ff607473.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "계층 구조 주소록 대화 상자")

*SeniorityIndex* 매개 변수를 사용하여 계층 구조의 추가 수준을 제공할 수 있습니다. HAB를 만들 때 *SeniorityIndex* 매개 변수를 사용하여 받는 사람 개개인의 순위 또는 이들 조직 층 내의 연공 서열로 조직 그룹을 지정합니다. 이 순위는 받는 사람 또는 그룹이 HAB에 표시되는 순서를 지정합니다. 예를 들어, 이전 예에서 회사 사무실의 받는 사람에 대한 *SeniorityIndex* 매개 변수가 다음으로 설정됩니다.

  - David Hamilton에 대해 `100`

  - Rajesh M. Patel에 대해 `50`

  - Amy Alberts에 대해 `25`


> [!NOTE]
> <EM>SeniorityIndex</EM> 매개 변수가 설정되지 않았거나 2명 이상의 사용자에 대해 동일할 경우 HAB 정렬 순서가 <EM>PhoneticDisplayName</EM> 매개 변수 값을 사용하여 사용자를 사전 순서에 따라 오름차순으로 나열합니다. <EM>PhoneticDisplayName</EM> 매개 변수 값이 설정되지 않은 경우 HAB 정렬 순서가 <EM>DisplayName</EM> 매개 변수 값을 기본값으로 사용하여 사용자를 사전 순서에 따라 오름차순으로 나열합니다.



## 계층 구조 주소록 구성

HAB 생성에 대한 자세한 내용은 [계층 구조 주소록을 사용 하지 않도록 설정 하거나 사용](enable-or-disable-hierarchical-address-books-exchange-2013-help.md) 항목에 포함되어 있습니다. 일반적인 단계는 다음과 같습니다.

1.  루트 조직(최상위 층)으로 사용될 메일 그룹을 만듭니다. 원할 경우에는 Exchange 포리스트에서 기존 조직 단위를 메일 그룹으로 사용할 수 있습니다.

2.  하위 층의 메일 그룹을 만들고 HAB의 구성원으로 지정합니다. 루트 조직 내에 적절한 계층 구조 순서로 나열되도록 이 그룹의 *SeniorityIndex* 매개 변수를 수정합니다.

3.  조직 구성원을 추가합니다. 하위 층 내에 적절한 계층 구조 순서로 나열되도록 이 구성원의 *SeniorityIndex* 매개 변수를 수정합니다.

4.  내게 필요한 옵션 용도로 *DisplayName* 매개 변수의 음성 단어를 지정하는 *PhoneticDisplayName* 매개 변수를 사용할 수 있습니다.

