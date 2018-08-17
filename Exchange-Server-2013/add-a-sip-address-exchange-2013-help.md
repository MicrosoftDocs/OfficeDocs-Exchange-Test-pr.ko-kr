---
title: 'SIP 주소를 추가 합니다.: Exchange 2013 Help'
TOCTitle: SIP 주소를 추가 합니다.
ms:assetid: 40295bcf-c62b-4f26-95ca-a8c4bd210fb3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ662760(v=EXCHG.150)
ms:contentKeyID: 50555972
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# SIP 주소를 추가 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-14_

UM에 대 한 사용자를 사용 하도록 설정 하 고 SIP URI 다이얼 플랜에 연결할 때 두 EUM 프록시 주소 만들어집니다. 사용자의 내선 번호를 포함 하 고 다른 사용자에 대 한 SIP 주소를 포함 합니다. 내선 번호는 Outlook Voice Access 번호의 사용자를 호출 하는 경우에 사용 됩니다.

SIP URI 다이얼 플랜 및 SIP 주소는 UM 및 Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server를 통합 하는 경우 사용 됩니다. SIP 주소는 들어오는 호출을 라우팅할 및 사용자에 게 음성 메일을 보낼 Communications Server 또는 Lync Server에서 사용 됩니다. 기본적으로 UM에서 사용 되는 SIP 주소는 Communications Server 또는 Lync Server에 사용 되는 SIP 주소가 됩니다.

사용자가 UM을 사용 하는 경우 추가한 기본 SIP 주소에 기본 EUM 프록시 주소로 표시 됩니다. 기본 SIP 주소를 제거한 경우에 사용자의 SIP 주소를 포함 하는 추가 첫번째 EUM 프록시 주소 기본 EUM 프록시 주소로 표시 됩니다. 보조 EUM 프록시 주소 추가 하면 추가 SIP 주소에 표시 됩니다. 보조 SIP 주소는 추가 되 면 발신자에 게 SIP 주소를 사용 하는 사용자가 로그인 하는 SIP 끝점에서 사용자에 대 한 음성 메일을 남길 수 있습니다. 음성 메시지를 모두 동일한 사용자의 사서함으로 배달 됩니다.

기본 키 열 이나 사용자에 대 한 보조 SIP 주소를 추가 하려면 EAC 또는 셸을 사용할 수 있습니다. 기본 또는 보조 SIP 주소를 추가 하려면 EAC에서 사용자의 사서함에서 **전자 메일 주소** 페이지를 사용할 수 있습니다. 기본 또는 보조 SIP 주소를 추가 하려면 EAC에서 **UM 사서함** 페이지를 사용할 수 없습니다.

셸에서 **Get-UMMailbox** cmdlet 또는 **Get-Mailbox** cmdlet을 사용 하 여 사용자에 대 한 기본 및 보조 SIP 주소를 볼 수 있습니다.

음성 메일을 사용하도록 설정된 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이러한 절차를 수행 하기 전에 SIP URI UM 다이얼 플랜을 만들었는지 확인 합니다. 자세한 단계 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조 하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행 하기 전에 기존 사용자의 SIP URI 다이얼 플랜에 연결 된 UM을 사용할 수를 확인 합니다. 자세한 단계 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조 하십시오.

  - 이러한 절차를 수행 하기 전에 사용자에 게 할당할 SIP 주소 인지 확인 유효 하 고 서식이 지정 된 올바르게 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 기본 또는 보조 SIP 주소를 추가 하려면

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 SIP 주소를 추가 하려는 사서함을 선택 하 고![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")**편집** 을 클릭 합니다.

3.  **사용자 사서함** 페이지에서 **전자 메일 주소** 를![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**추가** 클릭 합니다.

4.  **새 전자 메일 주소** 페이지에서 **EUM** 를 선택 하 고 **주소/확장명** 상자에 사용자에 대 한 새 SIP 주소를 입력 합니다.

5.  **새 전자 메일 주소** 페이지에서 **다이얼 플랜** 을 SIP URI 다이얼 플랜을 선택 하려면 **찾아보기** 를 클릭 하 고 **확인** 을 클릭 합니다.

6.  **저장**을 클릭합니다.

## 셸을 사용 하 여 SIP 주소를 추가 하려면

이 예에서는 Tony Smith, UM 사용이 가능한 사용자에 대 한 SIP 주소를 추가합니다.


> [!NOTE]
> 셸을 사용 하 여 SIP 주소를 추가 하기 전에 EUM 프록시 주소를 추가 하려는 위치를 결정 해야 합니다. 위치를 확인 하려면 <STRONG>$mbx.EmailAddresses</STRONG> 명령을 사용 합니다. 목록에서 첫번째 프록시 주소는 0이 됩니다.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:tsmit@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

