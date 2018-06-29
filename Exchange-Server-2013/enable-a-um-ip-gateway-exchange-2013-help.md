---
title: 'UM IP 게이트웨이 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: UM IP 게이트웨이 사용 하도록 설정
ms:assetid: 2706ae06-c45d-41b7-abbe-378a9fca104a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996857(v=EXCHG.150)
ms:contentKeyID: 50482676
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM IP 게이트웨이 사용 하도록 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-11-05_

기본적으로 UM (통합 메시징) IP 게이트웨이 만들 때 해당 상태를 설정 사용 합니다. 그러나 오프 라인 상태로 들어오거나 나가는 호출을 수행할 수 없도록 하는 UM IP 게이트웨이 사용 하지 않도록 설정 해야 합니다. UM IP 게이트웨이 만든 후에 변수를 사용 또는 사용 안함 상태를 설정 하 여 해당 작업 및 기능을 제어할 수 있습니다.

UM IP 게이트웨이와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM IP 게이트웨이 절차](um-ip-gateway-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM IP 게이트웨이" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행 하기 전에 UM IP 게이트웨이 만들어진 및 사용 하지 않도록 설정 되었는지 확인 합니다. 자세한 단계 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)을 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 UM IP 게이트웨이 사용 하도록 설정 하려면

1.  EAC에서 이동 \> **통합 메시징** \> **UM IP 게이트웨이** 사용 하도록 설정 하려는 UM IP 게이트웨이 선택 하 고 다음![위쪽 화살표 아이콘](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "위쪽 화살표 아이콘")의 **위쪽 화살표** 클릭 합니다.

2.  **경고** 페이지에서 **예**를 클릭합니다.

## 셸을 사용 하 여 UM IP 게이트웨이 사용 하도록 설정 하려면

`MyUMIPGateway`라는 UM IP 게이트웨이 설정 하는이 예제입니다.

    Enable-UMIPGateway -Identity MyUMIPGateway

