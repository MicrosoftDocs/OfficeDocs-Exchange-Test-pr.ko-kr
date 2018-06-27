---
title: '역할 그룹 변경 내용을 검색 또는 관리자 감사 로그: Exchange 2013 Help'
TOCTitle: 역할 그룹 변경 내용을 검색 또는 관리자 감사 로그
ms:assetid: c7188d53-e672-492b-b57d-cd711379ddb3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff459262(v=EXCHG.150)
ms:contentKeyID: 50553912
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 그룹 변경 내용을 검색 또는 관리자 감사 로그

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2013-12-02_

관리자 감사 로그를 검색하여 누가 조직, 서버, 받는 사람 구성을 변경했는지 알아낼 수 있습니다. 이 기능은 예기치 않은 동작의 원인을 추적하거나, 악의적인 관리자를 식별하거나, 규정 준수 요구 사항이 충족되었는지 확인할 경우에 유용합니다. 관리자 감사 로깅에 대한 자세한 내용은 [관리자 감사 로깅](administrator-audit-logging-exchange-2013-help.md)을 참조하십시오.

사서함 감사 로그를 검색하려면 [사서함 감사 로깅](mailbox-audit-logging-exchange-2013-help.md)를 참조하십시오.


> [!TIP]
> Exchange Online에서 EAC를 사용하여 관리자 감사 로그 항목을 볼 수 있습니다. 자세한 내용은 <A href="view-the-administrator-audit-log-exchange-2013-help.md">관리자 감사 로그 보기</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "관리자 감사 로깅만 보기" 항목

  - 관리자 감사 로깅은 기본적으로 사용하도록 설정됩니다. 관리자 감사 로깅이 사용하도록 설정되어 있는지 확인하려면 다음 명령을 실행합니다.
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    `True` 값은 관리자 감사 로깅이 사용하도록 설정되어 있음을 나타냅니다. `False` 값은 관리자 감사 로깅이 사용하지 않도록 설정되어 있음을 나타냅니다. 온-프레미스 Exchange 조직에서 관리자 감사 로깅을 사용할 수 있도록 설정해야 하는 경우 다음 명령을 실행합니다.
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $true
    

    > [!NOTE]
    > Exchange Online에서는 <STRONG>Set-AdminAuditLogConfig</STRONG> cmdlet을 사용할 수 없습니다.

    
    자세한 내용은 [관리자가 관리 감사 로깅](manage-administrator-audit-logging-exchange-2013-help.md)를 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 관리 역할 그룹 변경 보고서 실행

조직의 역할 그룹에서 관리 역할 그룹 구성원에 대한 변경 내용을 확인하려면 EAC(Exchange 관리 센터)의 관리자 역할 변경 보고서를 사용할 수 있습니다. 관리자 역할 그룹 보고서를 사용하여 지정된 날짜 범위 동안 변경된 역할 그룹의 목록을 볼 수 있습니다. 또한 변경 내용을 볼 특정 역할 그룹을 선택할 수 있습니다.

1.  EAC에서 **준수 관리** \> **감사**를 선택한 후 **관리자 역할 그룹 보고서 실행**을 클릭합니다.

2.  **시작 날짜**와 **끝 날짜** 필드를 사용하여 날짜 범위를 선택합니다.

3.  **역할 그룹 선택**을 클릭한 후 변경 내용을 표시할 역할 그룹을 선택합니다. 모든 역할 그룹에 대한 변경 내용을 검색하려면 이 필드를 비워둡니다.

4.  **검색**을 클릭합니다.

지정한 기준을 사용하여 변경 내용을 찾은 경우 변경 내용 목록이 결과 창에 표시됩니다. 역할 그룹을 클릭하면 세부 정보 창에 해당 역할 그룹에 대한 변경 내용이 표시됩니다.

## EAC를 사용하여 관리자 감사 로그 내보내기

조직에 대한 변경 내용을 포함하는 XML 파일을 만들려면 EAC의 관리자 감사 로그 내보내기 보고서를 사용할 수 있습니다. 관리자 감사 로그 내보내기 보고서를 사용하면 지정한 사용자가 변경한 내용이 포함된 감사 로그 항목의 검색 날짜 범위를 지정할 수 있습니다. 그러면 XML 파일이 받는 사람에게 전자 메일 첨부 파일로 전송됩니다. XML 파일의 최대 크기는 10MB(메가바이트)입니다.


> [!NOTE]
> Outlook Web App은 기본적으로 XML 첨부 파일을 열지 못하도록 되어 있습니다. Exchange을 사용하여 XML 첨부 파일을 볼 수 있도록 Outlook Web App을 구성하거나 Microsoft Outlook과 같은 다른 전자 메일 클라이언트를 사용하여 첨부 파일을 볼 수 있습니다. Outlook Web App에서 XML 첨부 파일을 볼 수 있도록 구성하는 방법에 대한 자세한 내용은 <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Outlook Web App 가상 디렉터리 보기 또는 구성</A>을 참조하세요.



1.  EAC에서 **준수 관리** \> **감사**를 선택한 후 **관리자 감사 로그 내보내기**를 클릭합니다.

2.  **시작 날짜**와 **끝 날짜** 필드를 사용하여 날짜 범위를 선택합니다.

3.  **다음 사람에게 감사 보고서 보내기** 필드에서 **사용자 선택**을 클릭한 후 보고서를 받을 사람을 선택합니다.

4.  **내보내기**를 클릭합니다.

지정한 기준을 사용하여 로그 항목을 찾은 경우 XML 파일이 생성되어 지정한 받는 사람에게 전자 메일 첨부 파일로 전송됩니다.

## 셸을 사용하여 감사 로그 항목 검색

셸을 사용하여 지정한 기준을 충족하는 감사 로그 항목을 검색할 수 있습니다. 검색 기준 목록은 [관리자 감사 로깅](administrator-audit-logging-exchange-2013-help.md)를 참조하십시오. 이 절차에서는 **Search-AdminAuditLog** cmdlet을 사용하고 셸에 검색 결과를 표시합니다. 이 cmdlet은 **New-AdminAuditLogSearch** cmdlet 또는 EAC 감사 보고 보고서에 정의된 제한을 초과하는 결과를 반환해야 할 경우에 사용할 수 있습니다.

감사 로그 검색 결과를 받는 사람에게 전자 메일 첨부 파일로 전송하려면 이 항목의 뒷부분에 나오는 Use the Shell to search for audit log entries and send results to a recipient을 참조하십시오.

지정한 기준을 충족하는 감사 로그를 검색하려면 다음 구문을 사용합니다.

    Search-AdminAuditLog - Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False >


> [!NOTE]
> <STRONG>Search-AdminAuditLog</STRONG> cmdlet은 기본적으로 최대 1,000개의 로그 항목을 반환합니다. <EM>ResultSize</EM> 매개 변수를 사용하여 최대 250,000개의 로그 항목을 지정할 수 있습니다. 또는 <CODE>Unlimited</CODE> 값을 사용하여 모든 항목을 반환할 수 있습니다.



이 예에서는 다음 기준을 사용하여 모든 감사 로그 항목을 검색합니다.

  - **시작 날짜**   04.08.12

  - **끝 날짜**   03.10.12

  - **사용자 ID**   davids, chrisd, kima

  - **Cmdlet**   **Set-Mailbox**

  - **매개 변수**   *ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

<!-- end list -->

    Search-AdminAuditLog -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima

이 예에서는 특정 사서함에 대한 변경 내용을 검색합니다. 문제를 해결하거나 조사에 필요한 정보를 제공해야 할 경우에 유용합니다. 다음과 같은 기준이 사용됩니다.

  - **시작 날짜**   01.05.12

  - **끝 날짜**   03.10.12

  - **개체 ID**   contoso.com/Users/DavidS

<!-- end list -->

    Search-AdminAuditLog -StartDate 05/01/2012 -EndDate 10/03/2012 -ObjectID contoso.com/Users/DavidS

검색 결과 여러 로그 항목이 반환될 경우 이 항목의 뒷부분에 있는 Use the Shell to search for audit log entries and send results to a recipient에서 제공하는 절차를 사용하는 것이 좋습니다. 해당 섹션의 절차는 지정한 받는 사람에게 XML 파일을 전자 메일 첨부 파일로 전송하므로 관심 있는 데이터를 더 쉽게 추출할 수 있습니다.

구문과 매개 변수에 대한 자세한 내용은 [Search-AdminAuditLog](https://technet.microsoft.com/ko-kr/library/ff459250\(v=exchg.150\))를 참조하십시오.

## 감사 로그 항목의 상세 정보 보기

**Search-AdminAuditLog** cmdlet은 [관리자 감사 로깅](administrator-audit-logging-exchange-2013-help.md)의 "감사 로그 콘텐츠" 섹션에 설명된 필드를 반환합니다. cmdlet에 의해 반환된 필드 중에서 **CmdletParameters** 및 **ModifiedProperties**의 두 필드에는 기본적으로 볼 수 없는 추가 정보가 포함됩니다.

**CmdletParameters** 및 **ModifiedProperties** 필드의 콘텐츠를 보려면 다음 단계를 수행합니다. 또는 이 항목의 뒷부분에 있는 Use the Shell to search for audit log entries and send results to a recipient의 절차를 사용하여 XML 파일을 만들 수 있습니다.

이 절차에서는 다음 개념을 사용합니다.

  - [배열](https://technet.microsoft.com/ko-kr/library/aa998267\(v=exchg.150\))

  - [사용자 정의 변수](https://technet.microsoft.com/ko-kr/library/bb123690\(v=exchg.150\))

<!-- end list -->

1.  검색할 기준을 정하고 **Search-AdminAuditLog** cmdlet을 실행한 후 다음 명령을 사용하여 변수에 결과를 저장합니다.
    
        $Results = Search-AdminAuditLog <search criteria>

2.  각 감사 로그 항목은 `$Results` 변수에 배열 요소로 저장됩니다. 배열 요소 인덱스를 지정하여 배열 요소를 선택할 수 있습니다. 배열 요소 인덱스는 첫 번째 배열 요소에 대해 0에서 시작합니다. 예를 들어, 인덱스가 4인 5번째 배열 요소를 검색하려면 다음 명령을 사용합니다.
    
        $Results[4]

3.  이전 명령이 배열 요소 4에 저장된 로그 항목을 반환합니다. 이 로그 항목의 **CmdletParameters** 및 **ModifiedProperties** 필드의 콘텐츠를 보려면 다음 명령을 사용합니다.
    
        $Results[4].CmdletParameters
        $Results[4].ModifiedProperties

4.  다른 로그 항목의 **CmdletParameters** 또는 **ModifiedParameters** 필드의 콘텐츠를 보려면 배열 요소 인덱스를 변경합니다.

## 셸을 사용하여 감사 로그 항목을 검색하고 받는 사람에게 결과 전송

셸을 사용하여 지정한 기준을 충족하는 감사 로그 항목을 검색한 다음 지정한 받는 사람에게 해당 결과를 XML 첨부 파일로 전송할 수 있습니다. 결과가 15분 내에 받는 사람에게 전송됩니다. 검색 기준 목록은 [관리자 감사 로깅](administrator-audit-logging-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> Outlook Web App은 기본적으로 XML 첨부 파일을 열지 못하도록 되어 있습니다. Exchange을 사용하여 XML 첨부 파일을 볼 수 있도록 Outlook Web App을 구성하거나 Microsoft Outlook과 같은 다른 전자 메일 클라이언트를 사용하여 첨부 파일을 볼 수 있습니다. Outlook Web App에서 XML 첨부 파일을 볼 수 있도록 구성하는 방법에 대한 자세한 내용은 <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Outlook Web App 가상 디렉터리 보기 또는 구성</A>을 참조하세요.



지정한 기준을 충족하는 감사 로그를 검색하려면 다음 구문을 사용합니다.

    New-AdminAuditLogSearch -Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False > -StatusMailRecipients <recipient 1, recipient 2, ...> -Name <string to include in subject>

이 예에서는 다음 기준을 사용하여 모든 감사 로그 항목을 검색합니다.

  - **시작 날짜**   04.08.12

  - **끝 날짜**   03.10.12

  - **사용자 ID**   davids, chrisd, kima

  - **Cmdlet**   **Set-Mailbox**

  - **매개 변수**   *ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

이 명령을 실행하면 제목 줄에 "사서함 제한 변경 내용"이라고 표시된 메시지가 결과와 함께 davids@contoso.com SMTP 주소에 전송됩니다.

    New-AdminAuditLogSearch -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima -StatusMailRecipients davids@contoso.com -Name "Mailbox limit changes"


> [!NOTE]
> <STRONG>New-AdminAuditLogSearch</STRONG> cmdlet이 생성할 수 있는 보고서의 최대 크기는 10MB입니다. 검색 결과에 10MB보다 큰 보고서가 반환될 경우 지정한 검색 기준을 변경합니다. 예를 들어, 데이터 범위의 크기를 줄이고 원래 날짜 범위에 포함된 여러 보고서를 실행합니다.



XML 파일의 형식에 대한 자세한 내용은 [관리자 감사 로그 구조](administrator-audit-log-structure-exchange-2013-help.md)를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [New-AdminAuditLogSearch](https://technet.microsoft.com/ko-kr/library/ff459243\(v=exchg.150\))를 참조하십시오.

