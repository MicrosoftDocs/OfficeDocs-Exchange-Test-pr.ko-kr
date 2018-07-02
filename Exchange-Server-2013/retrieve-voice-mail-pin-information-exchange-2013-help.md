---
title: '음성 메일 PIN 정보를 검색 합니다.: Exchange 2013 Help'
TOCTitle: 음성 메일 PIN 정보를 검색 합니다.
ms:assetid: 01517cca-99fe-46b2-b586-19e8d2707728
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa995900(v=EXCHG.150)
ms:contentKeyID: 54651775
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메일 PIN 정보를 검색 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-04-03_

UM(통합 메시징) 사용이 가능한 사용자의 PIN 정보를 검색할 수 있습니다. 사용자가 UM을 사용하도록 설정한 후 PIN이 생성되거나 만들어진 다음 암호화되어 사용자 사서함에 저장됩니다.

UM 사용 가능 사용자의 PIN 정보를 검색할 때 반환되는 정보는 사용자 사서함에 저장되어 있는 암호화된 PIN 데이터를 사용하여 계산됩니다. 이 작업을 사용하면 사용자의 사서함에서 정보를 볼 수 있을 뿐만 아니라 사용자가 자신의 사서함을 잠갔는지 여부를 알 수 있습니다.

PIN 보안과 관련된 추가 작업에 대한 자세한 내용은 [PIN 보안 절차](pin-security-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 절차를 수행하기 전에 사용자 사서함에서 UM을 사용하도록 설정했는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 사용 가능 사용자의 PIN 정보 검색

1.  EAC에서 **받는 사람**으로 이동합니다. 목록 보기에서 보려는 사용자 사서함을 선택합니다.

2.  세부 정보 창의 **전화 및 음성 기능**에서 **자세히 보기**를 클릭합니다.

3.  **UM 사서함** 페이지 \> **UM 사서함 설정**에서 사용자의 **PIN 상태**를 확인합니다. 이 페이지에서 사용자의 음성 메일 PIN을 다시 설정할 수도 있습니다.

## 셸을 사용하여 UM 사용 가능 사용자의 PIN 정보 검색

이 예에서는 사용자 ID, PIN 만료 여부, UM 사서함 잠김 여부 및 Tony가 처음 사용자인지 여부를 표시합니다.

    Get-UMMailboxPIN -identity tony@contoso.com

