---
title: '활성화 하거나 금지 자동 전화 교환에서 통화를 전송 합니다.: Exchange 2013 Help'
TOCTitle: 활성화 하거나 금지 자동 전화 교환에서 통화를 전송 합니다.
ms:assetid: ca961cc8-cc24-4e05-b72d-79979c155cf9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423558(v=EXCHG.150)
ms:contentKeyID: 52057968
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 활성화 하거나 금지 자동 전화 교환에서 통화를 전송 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

발신자가 자동 전화 교환을 통해 사용자에게 통화를 전송할 수 있도록 설정하거나 전송할 수 없도록 차단할 수 있습니다. 이 옵션은 기본적으로 사용하도록 설정되므로 발신자가 UM(통합 메시징) 자동 전화 교환과 연결된 UM 다이얼 플랜의 UM 사용 가능 사용자에게 통화를 전송할 수 있습니다.

UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 자동 전화 교환에서 사용자에게 통화를 전송하도록 설정하거나 전송할 수 없도록 차단

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 통화 전송을 구성할 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지 \> **주소록 및 교환원 액세스**의 **사용자 연락 옵션**에서 **발신자가 사용자에게 전화를 걸 수 있도록 허용** 옆의 확인란을 선택하여 통화를 전송할 수 있도록 설정합니다. 통화 전송을 차단하려면 확인란의 선택을 취소합니다.

4.  **저장**을 클릭합니다.


> [!NOTE]
> 이 확인란과 <STRONG>발신자가 사용자에 대한 음성 메시지를 남기도록 허용</STRONG> 확인란의 선택을 모두 취소하면 <STRONG>주소록 검색 옵션</STRONG>이 사용하지 않도록 설정됩니다.



## 셸을 사용하여 UM 자동 전화 교환에서 사용자에게 통화를 전송하도록 설정하거나 전송할 수 없도록 차단

이 예에서는 `MyUMAutoAttendant`라는 UM 자동 전화 교환에서 통화 전송을 차단합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $false

이 예에서는 `MyUMAutoAttendant`라는 UM 자동 전화 교환에서 통화 전송을 사용하도록 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $true

