---
title: '사용자에 대 한 부재중된 전화 알림을 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: 사용자에 대 한 부재중된 전화 알림을 사용 하지 않도록 설정
ms:assetid: e54937d5-3074-454f-b561-e601fecfc6ad
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673570(v=EXCHG.150)
ms:contentKeyID: 52058038
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자에 대 한 부재중된 전화 알림을 사용 하지 않도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-12-09_

셸 또는 EAC를 사용 하 여 UM (통합 메시징) 사서함 정책에 대 한 부재중된 전화 알림을 사용 하지 않도록 설정 하거나 설정할 수 있습니다. 부재중된 전화 알림 사용자는 수신 전화에 응답 하지 때 사용자에 게 전송 된 전자 메일 메시지 이며 호출자가 음성 메시지를 남길 하지 않습니다. 다른 전자 메일 메시지를 사용자에 대 한 남아 있는 음성 메시지를 포함 하는 것입니다.

UM 사서함 정책에서 부재 중 전화 알림을 사용하지 않도록 설정하면 UM 사서함 정책과 연관된 모든 사용자가 수신 전화를 받지 않고 발신자가 음성 메시지를 남기지 않는 경우 전자 메일 메시지를 받지 못하게 됩니다. 기본적으로 부재 중 전화 알림은 각 UM 사서함 정책이 만들어질 때 사용하도록 설정됩니다. 또한 기본적으로 UM 다이얼 플랜을 만들 때마다 UM 사서함 정책이 만들어집니다.


> [!NOTE]
> 통합 메시징과 Microsoft Lync Server를 통합하는 경우 Exchange 2007 또는 Exchange 2010 사서함 서버에 사서함이 있는 사용자는 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버로 통화가 전송되기 전에 연결을 끊으면 부재 중 전화 알림을 사용할 수 없습니다.



UM 사서함 정책에 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 사서함 정책 관리](manage-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 UM 사서함 정책에 대 한 부재중된 전화 알림을 사용 하지 않도록 설정 하려면

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 관리할 UM 사서함 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지에서 \> **일반**, 확인란의 선택을 취소 옆의 확인란 **허용 부재중 전화 알림** 입니다.

4.  **저장**을 클릭합니다.

## 셸을 사용 하 여 UM 사서함 정책에 대 한 부재중된 전화 알림을 사용 하지 않도록 설정 하려면

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책에 대 한 부재중된 전화 알림을 사용 하지 않도록 설정 합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMissedCallNotifications $false

