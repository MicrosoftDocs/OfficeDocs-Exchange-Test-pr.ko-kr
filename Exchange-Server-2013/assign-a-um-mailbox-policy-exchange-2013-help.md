---
title: 'UM 사서함 정책 할당: Exchange 2013 Help'
TOCTitle: UM 사서함 정책 할당
ms:assetid: c8da6cbe-3d22-4fff-8b5a-416b1c8adb6c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201728(v=EXCHG.150)
ms:contentKeyID: 50484160
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 사서함 정책 할당

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-30_

사용자가 UM(통합 메시징) 및 음성 사서함을 사용할 수 있도록 설정하는 경우에는 해당 사용자의 사서함에 연결할 UM 사서함 정책을 선택해야 합니다. 사용자가 UM을 사용할 수 있도록 설정한 후에 해당 사용자 사서함에 연결된 UM 사서함 정책을 변경할 수 있습니다.

UM 사서함 정책을 만들어 일련의 공용 정책이나 보안 설정을 UM 사용 가능 사용자의 사서함 모음에 적용할 수 있습니다. UM 사서함 정책을 사용하여 다음과 같은 설정을 적용할 수 있습니다.

  - PIN 정책

  - 전화 걸기 제한

  - 기타 일반적인 UM 사서함 정책 속성


> [!NOTE]
> UM 다이얼 플랜을 만들 때마다 기본 UM 사서함 정책이 하나씩 만들어집니다. 조직의 요구 사항에 따라 기본 UM 사서함 정책을 삭제하거나 추가 UM 사서함 정책을 만들 수 있습니다.



음성 메일을 사용하도록 설정된 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 사용자가 통합 메시징을 사용하도록 설정되었는지 확인하십시오. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 사용이 가능한 사용자에게 할당되는 UM 사서함 정책 변경

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 UM 사서함 정책을 변경할 사서함을 선택합니다.

3.  세부 정보 창의 **전화 및 음성 기능** \> **통합 메시징**에서 **세부 정보 보기**를 클릭합니다.

4.  **UM 사서함** 페이지에서 **UM 사서함 설정**을 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

5.  **UM 사서함** 페이지의 **UM 사서함 정책**에서 **찾아보기**를 클릭하여 사용자에 대한 UM 사서함 정책을 찾습니다.

6.  **저장**을 클릭합니다.

## 셸을 사용하여 UM 사용 가능 사용자에게 할당되는 UM 사서함 정책 변경

이 예에서는 Tony Smith라는 UM 사용 가능 사용자를 `MyUMMailboxPolicy`라는 UM 사서함 정책과 연결합니다.

    Set-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy

