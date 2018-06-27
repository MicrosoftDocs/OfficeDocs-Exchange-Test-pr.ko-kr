---
title: '음성 메일에 대해 사용자를 사용할 때 전송 되는 전자 메일 메시지와 텍스트를 포함 합니다.: Exchange 2013 Help'
TOCTitle: 음성 메일에 대해 사용자를 사용할 때 전송 되는 전자 메일 메시지와 텍스트를 포함 합니다.
ms:assetid: 3e8292fb-0cdb-445d-8048-a59af7c38d63
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201679(v=EXCHG.150)
ms:contentKeyID: 51407684
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메일에 대해 사용자를 사용할 때 전송 되는 전자 메일 메시지와 텍스트를 포함 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-12-16_

사용자의 사서함이 UM(통합 메시징) 음성 메일을 사용할 수 있도록 설정되어 있는 경우 통합 메시징 사용자를 환영하는 전자 메일 메시지가 보내집니다. 이 메시지에는 사용자가 음성 메일 시스템에 처음 액세스하는 데 사용할 PIN 정보가 들어 있습니다.

UM 사서함 정책의 **사용자가 통합 메시징을 사용할 수 있는 경우** 상자에 텍스트를 추가하여 환영 전자 메일 메시지에 보낼 텍스트를 사용자 지정할 수 있습니다. UM 기술 지원 서비스 전화 번호나 추가 Outlook Voice Access 번호와 같은 정보를 포함할 수 있습니다. 추가한 텍스트는 UM 사서함 정책과 연결된 사용자가 통합 메시징을 사용할 수 있는 경우 보내는 전자 메일 메시지에 포함됩니다.


> [!NOTE]
> 환영 메시지에 추가할 사용자 지정 텍스트는 512자로 제한되며 간단한 HTML 텍스트를 포함할 수 있습니다.



UM 사서함 정책에 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 사서함 정책 절차](um-mailbox-policy-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함이 통합 메시징을 사용하도록 설정된 경우 보내는 텍스트 사용자 지정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 관리할 UM 사서함 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지 \> **메시지 텍시트**에서 **사용자가 통합 메시징을 사용할 수 있는 경우** 텍스트 상자에 사용자가 통합 메시징 음성 메일을 사용할 수 있을 경우 보내는 전자 메일 메시지에 포함할 텍스트를 입력합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 사서함이 통합 메시징을 사용하도록 설정된 경우 보내는 텍스트 사용자 지정

이 예에서는 UM 사서함 정책과 연결된 UM 사용 가능 사용자가 전화로 사서함에 액세스하는 데 사용할 수 있는 Outlook Voice Access 번호 및 UM에 대한 추가 지침을 받을 수 있도록 합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You've been enabled for Unified Messaging voice mail. To access your Exchange mailbox, call your internal telephone extension number. From outside your office, call 425-555-1234."

