---
title: '내선 번호를 제거 합니다.: Exchange 2013 Help'
TOCTitle: 내선 번호를 제거 합니다.
ms:assetid: c2b896cf-21f7-4453-a4e6-b23d236a6dd3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351124(v=EXCHG.150)
ms:contentKeyID: 50556078
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 내선 번호를 제거 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-07-21_

UM에 대 한 사용자를 사용 하도록 설정 하 고 전화 내선 번호 다이얼 플랜에 연결할 때 사용자의 내선 번호를 포함 하는 사용자에 대 한 EUM 프록시 주소가 만들어집니다. 사용자의 사서함에 음성 메일을 보낼 수 있도록를 사용 하 여 UM에 대 한 하나 이상의 내선 번호를 정의 해야 합니다. 내선 번호는 Outlook Voice Access 번호의 사용자를 호출 하는 경우에 사용 됩니다.

사용자가 UM을 사용 하는 경우 추가 된 기본 내선 번호 또는 사용자에 대해 관련된 EUM 프록시 주소와 함께 나중에 추가 된 보조 내선 번호를 제거할 수 있습니다. 사용자가 UM을 사용 하는 경우 추가한 기본 내선 번호에 기본 EUM 프록시 주소로 표시 됩니다. 추가한 모든 추가 내선 번호에 보조 EUM 프록시 주소도 표시 됩니다. 내선 번호를 제거 되 면 발신자에 게는 제거 된 내선 번호에 사용자에 대 한 음성 메일 더이상 남길 수 없습니다.

기본 내선 번호를 제거 하면 UM 사용자의 사서함 및 전화 응답 규칙을 처리할 수 없습니다 음성 메일을 보낼 수 없습니다. 기본 내선 번호를 제거한 후에 사용자에 대 한 EUM 프록시 주소로 **Null** EAC에서 및 셸에서 **Get-Mailbox** cmdlet을 실행 하는 경우 사용자의 사서함에 표시 됩니다. 또한, **Get-UMMailbox** cmdlet을 실행 하는 경우에 null 또는 빈 *Extensions*, *PhoneNumber*및 *CallAnsweringRulesExtensions* 매개 변수 수 있습니다.

기본 또는 보조 내선 번호를 제거 하려면 EAC 또는 셸을 사용할 수 있습니다. 기본 또는 보조 내선 번호를 제거 하려면 EAC에서 사용자의 사서함에서 **전자 메일 주소** 페이지를 사용할 수 있습니다. 기본 내선 번호를 제거 하려면 EAC에서 **UM 사서함** 페이지를 사용할 수 없습니다 하지만 보조 내선 번호를 제거 하려면 사용할 수 있습니다.

셸에서 **Get-UMMailbox** cmdlet 또는 **Get-Mailbox** cmdlet을 사용 하 여 사용자에 대 한 기본 및 보조 내선 번호를 볼 수 있습니다.

음성 메일을 사용하도록 설정된 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행 하기 전에 사용자의 사서함 UM을 사용할 수 및 전화 내선 번호 다이얼 플랜에 연결 된 있는지를 확인 합니다. 자세한 단계 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)를 참조 하십시오.

  - 이러한 절차를 수행 하기 전에 사용자에 대 한 기본 및 보조 내선 번호 구성 되었는지 확인 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 기본 또는 보조 내선 번호를 제거 하려면

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 내선 번호를 제거 하려는 사서함 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

3.  **사용자 사서함** 페이지의 **전자 메일 주소** 목록에서 제거할 내선 번호를 선택 하 고![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")**삭제** 를 클릭 합니다. 기본 EUM 프록시 주소 또는 내선 번호에 굵은 문자와 숫자가 표시 됩니다.

4.  **저장**을 클릭합니다.

## EAC를 사용 하 여 보조 내선 번호를 제거 하려면

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 사용자의 내선 번호를 제거 하려는 사서함을 선택 합니다.

3.  세부 정보 창의 **전화 및 음성 기능** \> **통합 메시징**에서 **세부 정보 보기**를 클릭합니다.

4.  **다른 확장** 페이지의 **내선 번호** 상자에서 제거할 내선 번호를 선택 하 고![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")**삭제** 를 클릭 합니다.

5.  **저장**을 클릭합니다.

## 셸을 사용 하 여 내선 번호를 제거 하려면

이 예에서는 Tony Smith, UM 사용이 가능한 사용자의 사서함에서 내선 번호 12345를 제거합니다.


> [!NOTE]
> 셸을 사용 하는 내선 번호를 제거 하기 전에 EUM 프록시 주소를 수정 하려는의 위치를 결정 해야 합니다. 위치를 확인 하려면 <STRONG>$mbx.EmailAddresses</STRONG> 명령을 사용 합니다. 목록에서 첫번째 EUM 프록시 주소는 0이 됩니다.



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.remove("eum:22222;phone-context=MyDialPlan.contoso.com") 
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

