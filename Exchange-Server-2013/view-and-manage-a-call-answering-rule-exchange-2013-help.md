---
title: '보기 및 전화 응답 규칙 관리: Exchange 2013 Help'
TOCTitle: 보기 및 전화 응답 규칙 관리
ms:assetid: de6d9fa1-7878-49a9-bddb-e3317d94f4d8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn140251(v=EXCHG.150)
ms:contentKeyID: 54651803
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보기 및 전화 응답 규칙 관리

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2015-04-08_

셸을 사용 하 여를 보거나 구성 하나 또는 사용자에 대 한 자세한 전화 응답 규칙. 확인 하거나 전화 응답 규칙을 여러 사용자에 대 한 관리 하려면 Exchange 관리 셸 스크립트에서 **Get-UMCallAnsweringRule** 또는 **Set-UMCallAnsweringRule** cmdlet를 사용할 수 있습니다.

전화 응답 규칙은 받은 편지함 규칙을 받는 전자 메일 메시지에 적용 되는 방식과 비슷합니다 수신 통화에 적용 됩니다. 사용자에 대 한 UM (통합 메시징)을 사용 하는 경우에 기본적으로 전화 응답 규칙의 없이 구성 됩니다. 그럼에도 수신 전화는 메일 시스템에 의해 응답이 제공 되 고 발신자는 음성 메시지를 남길 하 라는 메시지가 표시 됩니다.


> [!IMPORTANT]
> UM 사용이 가능한 사용자 만들기, 관리 및 전화 응답 규칙을 제거 하도록 Outlook Web App에 로그인 할 수 있습니다.



전화 응답 규칙에 관련 된 추가 관리 작업을 [프로시저를 호출 하는 착신 전환](forwarding-calls-procedures-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 항목의 "UM 전화 응답 규칙" 항목.

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 절차를 수행하기 전에 사용자 사서함에서 UM을 사용하도록 설정했는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요. Windows PowerShell을 사용하여 Exchange Online에 연결하는 방법을 알아보려면 [Exchange Online PowerShell에 연결](https://go.microsoft.com/fwlink/p/?linkid=396554)을 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용 하 여 전화 응답 규칙을 보려면

단일 전화 응답 규칙에 대 한 속성을 검색할 수 또는 UM 사용이 가능한 사용자의 사서함에서 전화 응답 규칙의 목록입니다.

이 예에서는 사용자의 UM 사용이 가능한 사서함에서 전화 응답 규칙의 서식 있는 목록을 반환합니다.

    Get-UMCallAnsweringRule-Mailbox tonysmith | Format-List

전화 응답 규칙 `MyUMCallAnsweringRule`의 속성을 표시 하는이 예제입니다.

    Get-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

## 셸을 사용 하 여 전화 응답 규칙을 구성 하려면

구성 하거나 사용자의 사서함에 저장 된 전화 응답 규칙을 변경할 수 있습니다. 다음 조건을 지정할 수 있습니다.

  - 수신 전화를 건 사람

  - 시간

  - 약속 있음/없음 상태

  - 전자 메일에 대해 자동 회신 기능이 켜져 있는지 여부

다음과 같은 작업도 지정할 수 있습니다.

  - 내게 연결

  - 발신자를 다른 사람에게 전환

  - 음성 메시지 남기기

이 예제에서는 순위를 설정 2에는 전화 응답 규칙 `MyCallAnsweringRule` 존재 하는 사서함에 Tony Smith에 대 한 합니다.

    Set-UMCallAnsweringRule -Mailbox tonysmith -Name MyCallAnsweringRule -Priority 2

이 예에서는 Tony Smith에 대 한는 전화 응답 규칙 `MyCallAnsweringRule` 사서함에 대 다음 작업을 수행 합니다.

  - 두 호출자 ID에 대한 전화 응답 규칙을 설정합니다.

  - 전화 응답 규칙의 우선 순위를 2로 설정합니다.

  - 호출자가 인사말을 중단할 수 있는 전화 응답 규칙을 설정합니다.

<!-- end list -->

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

이 예에서는 Tony Smith에 대 한에는 전화 응답 규칙 `MyCallAnsweringRule` 의 사서함에서 약속 있음/없음 상태를 자리 비움으로 변경 하 고 우선순위를 2로 설정 합니다.

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith@contoso.com -ScheduleStatus 0x8

