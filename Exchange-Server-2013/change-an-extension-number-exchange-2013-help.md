---
title: '내선 번호를 변경 합니다.: Exchange 2013 Help'
TOCTitle: 내선 번호를 변경 합니다.
ms:assetid: ff22b366-3bfb-4bf7-9f11-62fba48f1caf
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232208(v=EXCHG.150)
ms:contentKeyID: 50556115
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 내선 번호를 변경 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-11-14_

UM에 대 한 사용자를 사용 하도록 설정 하 고 전화 내선 번호 다이얼 플랜에 연결할 때 사용자의 내선 번호를 포함 하는 사용자에 대 한 EUM 프록시 주소가 만들어집니다. 사용자의 사서함에 음성 메일을 보낼 수 있도록를 사용 하 여 UM에 대 한 하나 이상의 내선 번호를 정의 해야 합니다. 내선 번호는 Outlook Voice Access 번호의 사용자를 호출 하는 경우에 사용 됩니다.

사용자가 UM을 사용 하는 경우 추가 된 기본 내선 번호 또는 사용자에 대 한 관련된 EUM 프록시 주소와 함께 나중에 추가 된 보조 내선 번호를 변경할 수 있습니다. 사용자가 UM을 사용 하는 경우 추가한 기본 내선 번호에 기본 EUM 프록시 주소로 표시 됩니다. 추가한 모든 추가 보조 내선 번호에 보조 EUM 프록시 주소도 표시 됩니다. 내선 번호, 변경 된 경우 발신자를 남길 수는 사용자에 대 한 음성 메일 전혀 설정 된 새 내선 번호입니다. 음성 메시지를 모두 동일한 사용자의 사서함으로 배달 됩니다.

기본 키 열 이나 사용자에 대 한 보조 내선 번호를 변경 하려면 EAC 또는 셸을 사용할 수 있습니다. 기본 또는 보조 내선 번호를 변경 하려면 EAC에서 사용자의 사서함에서 **전자 메일 주소** 페이지를 사용할 수 있습니다. 기본 내선 번호를 변경 하려면 EAC에서 **UM 사서함** 페이지를 사용할 수 없습니다 하지만 보조 내선 번호를 변경 하려면 사용할 수 있습니다. 보조 내선 번호를 변경 하려면 먼저 기존 보조 내선 번호를 제거 하 고 사용자에 대 한 올바른 보조 내선 번호를 추가 해야 합니다.

셸에서 **Get-UMMailbox** cmdlet 또는 **Get-Mailbox** cmdlet을 사용 하 여 사용자에 대 한 기본 및 보조 내선 번호를 볼 수 있습니다.

음성 메일을 사용하도록 설정된 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이러한 절차를 수행 하기 전에 전화 내선 번호 UM 다이얼 플랜을 만들었는지 확인 합니다. 자세한 단계 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조 하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행 하기 전에 사용자의 사서함 UM을 사용할 수 및 전화 내선 번호 다이얼 플랜에 연결 된 있는지 확인 합니다. 자세한 단계 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조 하십시오.

  - 이러한 절차를 수행 하기 전에 사용자에 게 할당 되는 내선 번호 UM 다이얼 플랜에 설정 하는 올바른 자릿수 포함 되어있는지 확인 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 기본 또는 보조 내선 번호를 변경 하려면

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 내선 번호를 변경 하려는 사서함을 선택 하 고![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")**편집** 을 클릭 합니다.

3.  **사용자 사서함** 페이지의 **전자 메일 주소** 변경할 내선 번호를 선택 하 고![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")**편집** 을 클릭 합니다. 기본 내선 번호에 굵은 문자와 숫자가 표시 됩니다.

4.  **전자 메일 주소** 페이지에서 **주소/확장명** 상자에 사용자에 대 한 새 내선 번호를 입력 합니다. 새 UM 다이얼 플랜을 선택 해야 하는 경우 **찾아보기** 를 클릭 수 있습니다.

5.  **저장**을 클릭합니다.

## 셸을 사용 하 여 기본 또는 보조 내선 번호를 변경 하려면

이 예에서는 Tony Smith, UM 사용이 가능한 사용자에 대 한 22222에 내선 번호를 변경합니다.


> [!NOTE]
> 셸을 사용 하는 내선 번호를 변경 하기 전에 EUM 프록시 주소를 변경 하려면의 위치를 결정 해야 합니다. 위치를 확인 하려면 <STRONG>$mbx.EmailAddresses</STRONG> 명령을 사용 합니다. 첫번째 EUM 프록시 주소는 기본 (기본) 내선 번호 및 목록에서 0 됩니다.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(0)="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

