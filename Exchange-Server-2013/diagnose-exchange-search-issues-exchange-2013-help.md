---
title: 'Exchange 검색 문제 진단: Exchange 2013 Help'
TOCTitle: Exchange 검색 문제 진단
ms:assetid: 8cfa26f4-ccf0-42dd-8570-67018188b4e8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123701(v=EXCHG.150)
ms:contentKeyID: 52058112
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 검색 문제 진단

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Exchange 검색은 사서함을 인덱싱하여 및 Exchange 사서함에서 첨부 파일을 지원 합니다. 전자 메일의 양이 증가, 사서함 크기 및 저장소 할당량을 사용자에 대 한 보관 사서함 및 원본 위치 eDiscovery 검색 검색을 수행 하기 위한 프로 비전을 늘리면 Exchange 검색은 Microsoft Exchange Server 2013 조직에 있는 사서함 서버의 중요 한 구성 요소를 사용 합니다. Exchange 검색 관련 문제는 사용자의 생산성에 영향을 줄 수 있으며 원본 위치 eDiscovery 기능에 영향을 줄 수 있습니다.

Exchange Search에 대한 자세한 내용은 [Exchange 검색](exchange-search-exchange-2013-help.md)를 참조하세요.

Exchange Search 관리와 관련된 관리 작업에 대한 자세한 내용은 [Exchange 검색 절차](exchange-search-procedures-exchange-2013-help.md)를 참조하십시오.

## Test-ExchangeSearch cmdlet 사용

이 항목에 나오는 절차 5단계에서는 **Test-ExchangeSearch** cmdlet을 실행하여 Exchange Search 문제를 진단하는 데 도움을 주는 방법을 설명합니다. **Test-ExchangeSearch** cmdlet을 사용하여 사서함 서버, 사서함 데이터베이스 또는 특정 사서함에 대한 Exchange Search 기능을 테스트할 수 있습니다. 이 cmdlet은 지정된 사서함(또는 사서함을 지정하지 않은 경우 데이터베이스의 시스템 사서함)으로 테스트 메시지를 전달한 다음 검색을 수행하여 메시지가 인덱싱되었는지 여부와 인덱싱하는 데 소요된 시간을 확인합니다. 정상 상태에서 Exchange Search는 만들어지거나 사서함으로 전달되는 메시지를 약 10초 이내에 인덱싱합니다. 테스트 메시지는 테스트 후에 자동으로 삭제됩니다.

구문과 매개 변수에 대한 자세한 내용은 [Test-ExchangeSearch](https://technet.microsoft.com/ko-kr/library/bb124733\(v=exchg.150\))를 참조하십시오.

## 검색할 수 없는 항목 가져오기 (영문)

Exchange 검색 하 여 성공적으로 인덱싱할 수 없는 사서함을 검색할 수 없는 항목 목록을 검색 하려면 [Get-FailedContentIndexDocuments](https://technet.microsoft.com/ko-kr/library/dd351154\(v=exchg.150\)) cmdlet을 사용할 수 있습니다. 사서함 서버, 사서함 데이터베이스 또는 특정 사서함에 대해 cmdlet을 실행할 수 있습니다. Cmdlet은 검색할 수 없으며 각 항목에 대 한 세부 정보를 반환 합니다. 다음과 같이 몇 가지 이유 사서함 항목을 검색할 수 없습니다. 전자 메일 메시지 검색으로 인덱싱할 수 없는 하는 첨부 파일 형식에 포함 될 수 있습니다 예 검색 필터가 설치 되지 않았거나 사용 하지 않으면 때문에 또는 합니다. 해당 파일 형식에 대 한 검색 필터를 사용할 수 있는 경우에 Exchange 서버에 설치할 수 있습니다.


> [!IMPORTANT]
> Microsoft에서 제공하는 검색 필터는 Microsoft에서 테스트 및 지원합니다. 타사 검색 필터는 프로덕션 환경의 Exchange 서버에 설치하기 전에 먼저 테스트 환경에서 테스트하는 것이 좋습니다.



검색할 수 없는 항목에 대 한 자세한 내용은 다음을 참조 합니다.

  - [Exchange 검색에서 인덱싱하는 파일 형식](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Exchange eDiscovery의 검색할 수 없는 항목](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

## Exchange 검색 문제 진단

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "Exchange 검색" 항목

1.  **서비스 상태 확인**   Microsoft Exchange Search(MSExchangeFastSearch) 서비스가 사서함 서버에서 시작되었습니까? 예인 경우 2단계로 이동하고, 아니요인 경우 서비스 MMC 스냅인을 사용하여 MSExchangeFastSearch 서비스가 실행되고 있는지 확인합니다.
    
    1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **서비스**를 클릭합니다.
    
    2.  **서비스**에서 **Microsoft Exchange Search** 서비스의 **상태**가 **시작됨**으로 표시되는지 확인합니다.

2.  **사서함 데이터베이스 구성 확인**   사용자의 사서함 데이터베이스에 대한 *IndexEnabled* 매개 변수가 true로 설정되어 있습니까? 예인 경우 3단계로 이동하고, 아니요인 경우 셸에서 다음 명령을 실행하여 *IndexEnabled* 플래그가 true로 설정되어 있는지 확인합니다.
    
        Get-MailboxDatabase | Format-Table Name,IndexEnabled
    
    구문과 매개 변수에 대한 자세한 내용은 [Get-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb124924\(v=exchg.150\))를 참조하십시오.

3.  **사서함 데이터베이스 크롤링 상태 확인**      Exchange 데이터베이스가 크롤링되었습니까? 예인 경우 4단계로 이동하고, 아니요인 경우 안정성 및 성능 모니터를 사용하여 **MSExchange Search Indexes** 성능 개체의 **Crawler: Mailboxes Remaining** 카운터를 확인합니다. 다음 단계를 수행합니다.
    
    1.  **성능 모니터** (perfmon.exe)를 엽니다.
    
    2.  콘솔 트리의 **모니터링 도구**에서 **성능 모니터**를 클릭합니다.
    
    3.  성능 모니터 창에서 **추가**(녹색 더하기 기호)를 클릭합니다.
    
    4.  **카운터 추가**의 **다음 컴퓨터에서 카운터 선택:** 목록에서 모니터링할 사서함 데이터베이스가 있는 서버를 선택합니다.
    
    5.  **컴퓨터에서 카운터 선택** 목록 아래에서 레이블이 표시되지 않은 상자에 있는 **MSExchange Search Indexes** 성능 개체를 선택합니다.
    
    6.  **선택한 개체의 인스턴스** 상자에서 사용자의 사서함 데이터베이스에 대한 인스턴스를 선택합니다.
    
    7.  **추가**를 클릭한 다음 **확인**을 클릭합니다.
        
        성능 모니터 창에서 **개체** 열에 **MSExchange Search Indexes** 성능 개체가 표시되며 해당하는 여러 카운터가 **카운터** 열에 표시됩니다.
    
    8.  **Crawler 보기: Mailboxes Remaining** 카운터를 확인합니다. 1보다 큰 값을 지정하면 데이터베이스의 사서함이 여전히 크롤링될 것임을 나타냅니다. 크롤링이 완료된 경우 값은 **0**입니다.
    
    성능 모니터를 사용 하는 방법에 대 한 정보, 성능 및 안정성 모니터링 하기 시작 가이드에 대 한 Windows Server 2008[](https://go.microsoft.com/fwlink/p/?linkid=178005)

4.  **데이터베이스 복사본 인덱싱 상태 확인**   콘텐츠 인덱스 상태가 정상입니까? **Get-MailboxDatabaseCopyStatus** cmdlet을 사용하여 데이터베이스 복사본의 콘텐츠 인덱싱 상태를 확인합니다.
    
        Get-MailboxDatabaseCopyStatus -Server $env:ComputerName | Format-Table Name,Status,ContentIndex* -Auto
    
    구문과 매개 변수에 대한 자세한 내용은 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ko-kr/library/dd298044\(v=exchg.150\))를 참조하십시오.

5.  **Test-ExchangeSearch cmdlet 실행**   사서함 데이터베이스를 이미 크롤링한 경우에는 사서함 데이터베이스 또는 특정 사서함에 대해 **Test-ExchangeSearch** cmdlet을 실행할 수 있습니다.
    
        Test-ExchangeSearch -Identity AlanBrewer@contoso.com
    
    구문과 매개 변수에 대한 자세한 내용은 [Test-ExchangeSearch](https://technet.microsoft.com/ko-kr/library/bb124733\(v=exchg.150\))를 참조하십시오.

6.  **응용 프로그램 이벤트 로그를 확인 합니다.**   이벤트 뷰어 또는 셸을 using, 검색 관련 오류 메시지에 대 한 응용 프로그램 이벤트 로그를 확인 합니다. 다음과 같은 이벤트 소스를 확인 합니다.
    
      - **MSExchangeFastSearch**
    
      - **MSExchangeIS**
    
    자세한 내용은 이벤트 로그 항목의 링크를 수행 합니다.

7.  **Microsoft Exchange Search 서비스 다시 시작**   서비스 MMC 스냅인 또는 셸을 사용하여 MicrosoftExchange Search(MSExchangeFastSearch) 서비스를 중지했다가 다시 시작합니다.
    
    1.  **시작**을 클릭하고 **관리 도구**를 가리킨 다음 **서비스**를 클릭합니다.
    
    2.  **서비스**에서 **Microsoft Exchange Search**를 마우스 오른쪽 단추로 클릭하고 **중지**를 클릭합니다. 서비스가 중지되면 다시 마우스 오른쪽 단추로 서비스를 클릭하고 **시작**을 클릭합니다.

8.  **검색 카탈로그 다시 시드**   검색 카탈로그가 손상된 경우 등 필요한 경우에는 카탈로그를 다시 시드해야 할 수 있습니다. 검색 카탈로그를 다시 시드해야 하는 경우 Exchange Search는 응용 프로그램 이벤트 로그에 항목을 로깅하여 사용자에게 알립니다. 검색 카탈로그 다시 시드에 대한 자세한 내용은 [검색 카탈로그 다시 시드](reseed-the-search-catalog-exchange-2013-help.md)를 참조하십시오.

