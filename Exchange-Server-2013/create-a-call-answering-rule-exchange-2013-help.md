---
title: '전화 응답 규칙 만들기: Exchange 2013 Help'
TOCTitle: 전화 응답 규칙 만들기
ms:assetid: 0976f8f2-3449-44f1-b0d1-20c91622e827
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ898495(v=EXCHG.150)
ms:contentKeyID: 51407664
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전화 응답 규칙 만들기

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-04-08_

셸을 사용 하 여 하나 이상의 전화 사용자에 대 한 응답 규칙을 만들 수 있습니다. 여러 사용자에 대 한 전화 응답 규칙을 만들 수는 Exchange 관리 셸 스크립트에서 **New-UMCallAnsweringRule** cmdlet를 사용할 수 있습니다.

전화 응답 규칙은 받은 편지함 규칙을 받는 전자 메일 메시지에 적용 되는 방식과 비슷합니다 수신 통화에 적용 됩니다. 사용자에 대 한 UM (통합 메시징)을 사용 하는 경우에 기본적으로 전화 응답 규칙의 없이 구성 됩니다. 그럼에도 수신 전화는 메일 시스템에 의해 응답이 제공 되 고 발신자는 음성 메시지를 남길 하 라는 메시지가 표시 됩니다.


> [!NOTE]  
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



## 셸을 사용 하 여 전화 응답 규칙을 만들려면

2의 우선순위가 가장 Tony Smith에 대 한 사서함에서 전화 응답 규칙 `MyCallAnsweringRule` 를 만드는 하는이 예제입니다.

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith

이 예제에서는 전화 응답 규칙 `MyCallAnsweringRule` 의 사서함에서 Tony Smith에 대 한 만들고 다음 작업을 수행 합니다.

  - 두 호출자 ID에 대한 전화 응답 규칙을 설정합니다.

  - 전화 응답 규칙의 우선 순위를 2로 설정합니다.

  - 호출자가 인사말을 중단할 수 있는 전화 응답 규칙을 설정합니다.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

이 예제에서는 전화 응답 규칙 `MyCallAnsweringRule` 의 사서함에서 Tony Smith에 대 한 만들고 다음 작업을 수행 합니다.

  -  전화 응답 규칙의 우선 순위를 2로 설정합니다.

  -  전화 응답 규칙에 대한 키 매핑을 만듭니다.

  -  발신자가 사용자의 음성 메일에 연결할 때 사용자 상태가 "약속 있음"인 경우 발신자는 다음을 수행할 수 있습니다.
    
      - 1 키를 누르면 내선 번호 45678의 교환원으로 전환됩니다.
    
      - 내게 연결 기능이 긴급 한 문제에 대해 사용할 첫째, 내선 번호 23456에 연결 하 고 확장 45671 연결 된 다음 연결 있도록 2 키를 누릅니다.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith -ScheduleStatus 0x4 - -KeyMappings "1,1,Receptionist,,,,,45678,","5,2,Urgent Issues,23456,23,45671,50,,"

