---
title: '원본 위치 eDiscovery 검색 만들기: Exchange 2013 Help'
TOCTitle: 원본 위치 eDiscovery 검색 만들기
ms:assetid: feedc0c9-4a44-4bb2-8520-cc29d66d4fc3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd353189(v=EXCHG.150)
ms:contentKeyID: 50484611
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원본 위치 eDiscovery 검색 만들기

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-01-17_


> [!NOTE]
> Exchange Online(Office 365 및 Exchange Online 독립 실행형 계획)에 새 원본 위치 eDiscovery 검색 만들기에 대한 마감 날짜인 2017년 7월 1일을 연기했습니다. 하지만 올해 말 또는 내년 초에는 Exchange Online에 새 검색을 만들 수 없습니다. eDiscovery 검색을 만들려면 Office 365 보안 및 준수 센터의 <A href="https://go.microsoft.com/fwlink/?linkid=847843">콘텐츠 검색</A>을 사용하시기 바랍니다. 새 원본 위치 eDiscovery를 해제한 후에도 기존 원본 위치 eDiscovery 검색을 계속 수정할 수 있으며 Exchange Server 2013 및 Exchange 하이브리드 배포에서 새 원본 위치 eDiscovery 검색을 계속 만들 수 있습니다.



[원본 위치 eDiscovery](in-place-ediscovery-exchange-2013-help.md)를 사용하면 [원본 위치 유지 및 소송 보존](in-place-hold-and-litigation-hold-exchange-2013-help.md) 상태인 사용자의 수정된 항목 원본 버전과 지운 편지함을 비롯한 모든 사서함 콘텐츠를 검색할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "원본 위치 eDiscovery" 항목.

  - EDiscovery 검색을 만들려면에서 검색을 만들려는 조직에 SMTP 주소가 해야 합니다. 따라서 Exchange Online 하면 사서함이 있어야 사용이 허가 된 Exchange Online (계획 2) eDiscovery 검색을 만들 수 있습니다. Exchange 하이브리드 조직에서 온-프레미스 Exchange 사서함 있어야 해당 메일 사용자 계정을 Office 365 조직에서 Exchange Online 사서함을 검색할 수 있도록 합니다. 또는 Office 365, 테 넌 트 관리자 계정 같은에 존재 하는 계정을 사용 하 여 로그인 하면 해당 계정에 Exchange Online (계획 2) 라이선스를 할당 해야 합니다.

  - Exchange 2013 설치 프로그램은 **사서함 검색**이라는 검색 사서함을 만들어 검색 결과를 복사합니다. 사서함 검색도 Exchange Online에서 기본적으로 만들어집니다. 검색 사서함을 추가로 만들 수 있습니다. 자세한 내용은 [검색 사서함 만들기](create-a-discovery-mailbox-exchange-2013-help.md)를 참조하십시오.

  - 원본 위치 eDiscovery 검색을 만들 때 검색 결과에 반환된 메시지는 검색 사서함에 자동으로 복사되지 않습니다. 검색을 만든 후에 EAC(Exchange 관리 센터)를 사용하여 검색 결과를 예상하고 미리 보거나 검색 사서함으로 복사할 수 있습니다. 자세한 내용은
    
      - 이 항목의 뒷부분에 나오는 Estimate or preview search results를 참조하세요.
    
      - [EDiscovery 검색 결과 검색 사서함으로 복사](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 원본 위치 eDiscovery 검색 만들기

앞에서 설명한 것처럼 eDiscovery 검색을 만들려면 조직에 SMTP 주소가 있는 사용자 계정으로 로그인해야 합니다.

1.  **규정 준수 관리** \> **원본 위치 eDiscovery & 유지**로 이동합니다.

2.  **새로 만들기** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭합니다.

3.  **원본 위치 eDiscovery 및 유지**의 **이름 및 설명** 페이지에서 검색의 이름을 입력하고 선택적 설명을 추가한 후 **다음**을 클릭합니다.

4.  **사서함** 페이지에서 검색 사서함을 선택 합니다. 모든 사서함에서 검색 하거나 검색 하는 특정 이벤트를 선택 수 있습니다. 또한 Exchange Online 검색에 대 한 콘텐츠 원본으로 Office 365 그룹을 선택할 수 있습니다.
    

    > [!IMPORTANT]
    > <STRONG>모든 사서함 검색</STRONG> 옵션을 사용하여 모든 사서함을 보류 상태로 설정할 수는 없습니다. 원본 위치 유지를 만들려면 <STRONG>검색할 사서함 지정</STRONG>을 선택해야 합니다. 자세한 내용은 <A href="create-or-remove-an-in-place-hold-exchange-2013-help.md">만들기 또는 In-place Hold 제거</A>를 참조하십시오.



5.  **검색 쿼리** 페이지에서 다음 필드를 작성합니다.
    
      - **모든 사용자 사서함 콘텐츠 포함**   선택한 사서함의 모든 콘텐츠를 보류 상태로 설정하려면 이 옵션을 선택합니다. 이 옵션을 선택하면 추가 검색 조건을 지정할 수 없습니다.
    
      - **조건 기반의 필터**   키워드, 시작 및 종료 날짜, 보낸 사람 및 받는 사람 주소, 메시지 유형을 포함한 검색 조건을 지정하려면 이 옵션을 선택합니다.
        
        ![eDiscovery 검색 쿼리 구성](images/Dd353189.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "eDiscovery 검색 쿼리 구성")  
    

    > [!NOTE]
    > <STRONG>에서:</STRONG> 및 <STRONG>에/참조/숨은 참조:</STRONG> 검색을 실행할 때 생성 되는 검색 쿼리에 <STRONG>또는</STRONG> 연산자가 연결 된 필드입니다. 즉, 지정 된 사용자 (및 다른 검색 조건과 일치 하는 결과) 중 하나에서 주고받은 모든 메시지는 검색 결과에 포함 됩니다.<BR>날짜는 <STRONG>AND</STRONG> 연산자로 연결 되어있습니다.



6.  **원본 위치 유지 설정** 페이지에서 **선택한 사서함의 검색 쿼리와 일치하는 내용을 보류 중으로 표시** 확인란을 선택하고 다음 옵션 중 하나를 선택하여 항목을 원본 위치 유지 상태로 설정합니다.
    
      - **무기한 보류**   반환된 항목을 무기한 보류 상태로 설정하려면 이 옵션을 선택합니다. 보류 중인 항목은 검색에서 사서함을 제거하거나 검색을 제거할 때까지 유지됩니다.
    
      - **수신 날짜를 기준으로 항목을 보관할 날짜 수 지정** 특정 기간 동안 항목을 보관하려면 이 옵션을 사용합니다. 예를 들어 조직에서 모든 메시지를 7년 이상 유지해야 할 경우에 이 옵션을 사용할 수 있습니다. 보존 정책과 *시간 기반* 원본 위치 유지를 사용하여 7년 후에 항목이 삭제되도록 할 수 있습니다.
        

        > [!IMPORTANT]
        > 법적 목적을 위해 사서함이나 항목을 원본 위치 유지 상태로 설정하는 경우 일반적으로 항목을 무기한 보류했다가 사례나 조사가 완료될 때 보류 상태를 해제하는 것이 좋습니다.



7.  검색을 저장하고 지정한 조건에 따라 검색에 의해 반환될 항목의 예상 전체 크기 및 개수를 반환하려면 **마침**을 클릭합니다. 예상 값은 세부 정보 창에 표시됩니다. 세부 정보 창에 표시된 정보를 업데이트하려면 **새로 고침**![새로 고침 아이콘](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "새로 고침 아이콘")을 클릭합니다.

맨위로 돌아가기

## 셸을 사용하여 원본 위치 eDiscovery 검색 만들기

이 예에서는 012 키워드 Contoso 및 ProjectA를 포함 하는 항목에 대 한 검색 하는 하 고 다음 조건을 충족 하는 명명 된 원본 위치 eDiscovery 검색을 만듭니다.

  - 시작 날짜: 1/1/2009

  - 종료 날짜: 12/31/2011

  - 원본 사서함: DG-Finance

  - 대상 사서함: 사서함 검색

  - 메시지 유형: Email

  - 검색 통계에 검색할 수 없는 항목 포함

  - 로그 수준: 전체


> [!IMPORTANT]
> 원본 위치 eDiscovery 검색을 실행할 때 추가 검색 매개 변수를 지정하지 않으면 지정된 원본 사서함의 모든 항목이 결과에 반환됩니다. 검색할 사서함을 지정하지 않으면 Exchange 또는 Exchange Online 조직의 모든 사서함이 검색됩니다.



    New-MailboxSearch "Discovery-CaseId012" -StartDate "01/01/2009" -EndDate "12/31/2011" -SourceMailboxes "DG-Finance" -TargetMailbox "Discovery Search Mailbox" -SearchQuery '"Contoso" AND "Project A"' -MessageTypes Email -IncludeUnsearchableItems -LogLevel Full


> [!NOTE]
> <EM>StartDate</EM> 및 <EM>EndDate</EM> 매개 변수 사용 시에는 로컬 컴퓨터 설정이 dd/mm/yyyy 등의 다른 형식을 사용하도록 구성되어 있어도 mm/dd/yyyy 날짜 형식을 사용해야 합니다. 예를 들어 2013년 4월 1일과 2013년 7월 1일 사이에 전송된 메시지를 검색하려면 시작 날짜와 종료 날짜로 <STRONG>04/01/2013</STRONG> 및 <STRONG>07/01/2013</STRONG>을 사용합니다.



이 예제에서는 Sara Davis Alex Darrow 하 여 2015에서 보내는 전자 메일 메시지에 대 한 검색 하는 HRCase090116 라는 원본 위치 eDiscovery 검색을 만듭니다.

    New-MailboxSearch "HRCase090116" -StartDate "01/01/2015" -EndDate "12/31/2015" -SourceMailboxes  alexd,sarad -SearchQuery 'From:alexd@contoso.com AND To:sarad@contoso.com' -MessageTypes Email -TargetMailbox "Discovery Search Mailbox" -IncludeUnsearchableItems -LogLevel Full

셸을 사용하여 원본 위치 eDiscovery 검색을 만든 후에는 **Start-MailboxSearch** cmdlet을 사용하여 검색을 시작해 *TargetMailbox* 매개 변수에 지정한 검색 사서함으로 메시지를 복사해야 합니다. 자세한 내용은 [EDiscovery 검색 결과 검색 사서함으로 복사](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)를 참조하세요.

구문과 매개 변수에 대한 자세한 내용은 [New-MailboxSearch](https://technet.microsoft.com/ko-kr/library/dd298064\(v=exchg.150\))를 참조하십시오.

맨위로 돌아가기

## EAC를 사용하여 검색 결과 예상 또는 미리 보기

원본 위치 eDiscovery 검색을 만든 후에는 EAC를 사용하여 검색 결과를 예상하고 미리 볼 수 있습니다. **New-MailboxSearch** cmdlet을 사용하여 새 검색을 만든 경우에는 셸을 사용하여 검색을 시작해 예상 검색 결과를 확인할 수 있습니다. 셸을 사용해서는 검색 결과에 반환된 메시지를 미리 볼 수 없습니다.

1.  **준수 관리** \> **원본 위치 eDiscovery 및 유지**로 이동합니다.

2.  목록 보기에서 원본 위치 eDiscovery 검색을 선택한 후 다음 중 하나를 수행 합니다.
    
      - **검색** ![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘") 클릭 \> **예상 검색 결과** 의 예상 전체 크기 및 검색에 의해 반환 되는 항목 수를 반환 하려면 지정 된 조건에 따라. 이 옵션을 선택 하면 검색을 다시 시작 하 고 예상을 수행 합니다.
        
        예상 검색 결과는 세부 정보 창에 표시됩니다. 세부 정보 창에 표시된 정보를 업데이트하려면 **새로 고침**![새로 고침 아이콘](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "새로 고침 아이콘")을 클릭합니다.
    
      - 검색 estimate 완료 되 면 결과 미리보려면 세부 정보 창에서 **검색 결과 미리 보기를** 클릭 합니다. 이 옵션을 선택 하면 **eDiscovery 검색 미리 보기** 창에서 열립니다. 검색 된 사서함에서 반환 된 모든 메시지가 표시 됩니다.
        

        > [!NOTE]
        > 검색된 사서함은 <STRONG>eDiscovery 검색 미리 보기</STRONG> 창의 오른쪽 창에 나열됩니다. 각 사서함에 대해 반환된 항목 수와 이러한 항목의 총 크기도 표시됩니다. 검색에서 반환된 모든 항목은 오른쪽 창에 나열되며 최신 항목 또는 오래된 항목순으로 정렬할 수 있습니다. 왼쪽 창에서 사서함을 클릭하여 각 사서함의 항목을 오른쪽 창에 표시할 수는 없습니다. 특정 사서함에서 반환된 항목을 보려면 검색 결과를 복사하고 검색 사서함에서 항목을 확인할 수 있습니다.

    
    ![검색 결과 예상 또는 미리 보기](images/Dd353189.57e0fc2d-71bf-42aa-aa4b-4a77148f2b43(EXCHG.150).gif "검색 결과 예상 또는 미리 보기")  

맨위로 돌아가기

## 셸을 사용하여 예상 검색 결과 예상

*EstimateOnly* 스위치를 사용하면 결과를 검색 사서함에 복사하지는 않고 예상 검색 결과만 반환할 수 있습니다. 이렇게 하려면 **Start-MailboxSearch** cmdlet을 사용하여 예상만 수행하는 검색을 시작해야 합니다. 그런 후에 **Get-MailboxSearch** cmdlet을 사용하여 예상 검색 결과를 검색할 수 있습니다.

예를 들어 새 eDiscovery 검색을 만든 다음 예상 검색 결과를 표시하려면 다음 명령을 실행합니다.

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeKeywordStatistics

    Start-MailboxSearch "FY13 Q2 Financial Results"

    Get-MailboxSearch "FY13 Q2 Financial Results"

위 예제에서 예상 검색 결과에 대한 특정 정보를 표시하려면 다음 명령을 실행하면 됩니다.

    Get-MailboxSearch "FY13 Q2 Financial Results" | FL Name,Status,LastRunBy,LastStartTime,LastEndTime,Sources,SearchQuery,ResultSizeEstimate,ResultNumberEstimate,Errors,KeywordHits

맨위로 돌아가기

## eDiscovery 검색에 대한 추가 정보

  - 새 eDiscovery 검색을 만든 후에는 검색 결과를 검색 사서함에 복사한 다음 PST 파일로 내보낼 수 있습니다. 자세한 내용은 다음을 참조하세요.
    
      - [EDiscovery 검색 결과 검색 사서함으로 복사](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)
    
      - [PST 파일로 eDiscovery 검색 결과 내보내기](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)

  - EDiscovery 검색 예상 (하는 검색 조건에 키워드 포함)를 실행 한 후에 선택한 검색에 대 한 세부 정보 창에서 **키워드 통계 보기를** 클릭 하 여 키워드 통계를 볼 수 있습니다. 이러한 통계 검색 쿼리에 사용 되는 각 키워드에 대해 반환 되는 항목 수에 대 한 세부 정보를 표시 합니다. 그러나 100 개가 넘는 원본 사서함의 검색에 포함 된, 하는 경우 키워드 통계를 확인 하려고 하면 오류가 반환 됩니다. 키워드 통계를 보려면 100 개 이하의 원본 사서함 검색에 포함할 수 있습니다.

  - 검색 속성;의 전체 목록을 반환 하는 검색의 이름을 지정 해야하는 eDiscovery 검색에 대 한 정보를 검색할 수 있는 Exchange Online 에서 **Get-MailboxSearch** 을 사용 하는 경우 예: `Get-MailboxSearch "Contoso Legal Case"`. 매개 변수를 사용 하지 않고 **Get-MailboxSearch** cmdlet을 실행 하는 경우 다음과 같은 속성 반환 되지 않습니다.
    
      - SourceMailboxes
    
      - Sources
    
      - SearchQuery
    
      - ResultsLink
    
      - PreviewResultsLink
    
      - Errors
    
    조직에서 모든 eDiscovery 검색에 대 한 이러한 속성을 반환 하는 리소스를 많이 필요 하다는 메시지가 나타나는 이유는.

맨위로 돌아가기

