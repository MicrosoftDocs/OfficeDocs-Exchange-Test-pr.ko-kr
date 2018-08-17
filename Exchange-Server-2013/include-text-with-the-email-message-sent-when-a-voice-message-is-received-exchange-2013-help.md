---
title: '음성 메시지를 받을 때 전송 되는 전자 메일 메시지와 텍스트를 포함 합니다.: Exchange 2013 Help'
TOCTitle: 음성 메시지를 받을 때 전송 되는 전자 메일 메시지와 텍스트를 포함 합니다.
ms:assetid: b2eec29c-e5eb-4263-80d8-0b9813dd56dc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201718(v=EXCHG.150)
ms:contentKeyID: 51407732
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메시지를 받을 때 전송 되는 전자 메일 메시지와 텍스트를 포함 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-12-16_

UM(통합 메시징) 음성 메일을 사용할 수 있는 사용자가 음성 메일 메시지 수신 시 전송되는 전자 메일 메시지에 추가 텍스트를 포함할 수 있습니다. 기본적으로 음성 메시지에 포함되는 텍스트는 사용자가 음성 메시지를 받았다는 사실만을 나타냅니다. 그러나 UM 사서함 정책의 **사용자가 음성 메시지를 받는 경우** 상자에 텍스트를 추가하면 사용자 지정 메시지를 만들 수 있습니다. 예를 들어 이 텍스트는 시스템 보안 정책 관련 정보를 포함할 수 있으며 조직에서 음성 메시지를 올바르게 처리하는 방법에 대해 설명할 수 있습니다. 추가한 텍스트는 UM 사서함 정책과 연결된 UM 사용 가능 사용자가 음성 메시지 수신 시 전송되는 각 전자 메일 메시지에 포함됩니다.


> [!NOTE]
> 음성 메시지에 포함되는 사용자 지정 텍스트는 최대 512자까지 입력할 수 있으며 단순 HTML 텍스트를 포함할 수 있습니다.



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

## EAC를 사용하여 음성 메시지에 포함되는 텍스트 변경

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 관리할 UM 사서함 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지 \> **메시지 텍스트**에서 **사용자가 음성 메시지를 받는 경우** 텍스트 상자에 사용자가 음성 메시지 수신 시 전송되는 전자 메일 메시지에 포함할 텍스트를 입력합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 음성 메시지에 포함되는 텍스트 변경

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책과 연결된 사용자에게 전송되는 음성 메시지에 "조직 외부의 사용자에게 음성 메시지를 전달하지 마십시오."라는 추가 텍스트를 포함합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailText "Do not forward voice messages to users outside this organization."

