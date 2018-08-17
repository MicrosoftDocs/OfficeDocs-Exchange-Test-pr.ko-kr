---
title: 'EDiscovery 검색 결과 검색 사서함으로 복사: Exchange 2013 Help'
TOCTitle: EDiscovery 검색 결과 검색 사서함으로 복사
ms:assetid: bff2ce89-9e6f-494a-bd6a-2f2011507845
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn624163(v=EXCHG.150)
ms:contentKeyID: 61183427
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# EDiscovery 검색 결과 검색 사서함으로 복사

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-02-24_

원본 위치 eDiscovery 검색을 만든 후에 결과 검색 사서함으로 복사 하려면 EAC를 사용할 수 있습니다. 검색을 만들 때 지정 된 검색 사서함으로 결과 복사할는 **New-MailboxSearch** cmdlet을 사용 하 여 만든 eDiscovery 검색을 시작 하려면 셸을 사용할 수도 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5 분 또는 사서함 항목 수에 따라 검색 결과에 반환

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "원본 위치 eDiscovery" 항목.

  - EDiscovery 검색에 검색 결과 복사할 수는 있지만 전에 EAC 또는 셸을 사용 하 여 만들어야 합니다. 자세한 내용은 [원본 위치 eDiscovery 검색 만들기](create-an-in-place-ediscovery-search-exchange-2013-help.md)를 참조 합니다.

  - Exchange 2013 설치 프로그램 **사서함 검색** 검색 결과 복사 하려면 이라는 검색 사서함을 만듭니다. 사서함에 대 한 검색 검색 Exchange Online 에서 기본적으로도 생성 됩니다. 추가 검색 사서함을 만들 수 있습니다. 자세한 내용은 [검색 사서함 만들기](create-a-discovery-mailbox-exchange-2013-help.md)를 참조 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 검색 결과 복사 하려면

1.  EAC에서 **규정 준수 관리** 로 이동 \> **원본 위치 eDiscovery 및 유지** 합니다.

2.  목록 보기에서 eDiscovery 검색을 선택 합니다.

3.  **검색** ![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘")을 클릭하고 드롭다운 목록에서 **검색 결과 복사**를 클릭합니다.

4.  **검색 결과 복사**의 다음 옵션 중에서 선택합니다.
    
      - **검색할 수 없는 항목 포함**    사서함 항목 (예: Exchange 검색으로 인덱싱할 수 없는 파일 형식 첨부 파일이 있는 메시지) 검색할 수 없으며을 포함 하려면이 확인란을 선택 합니다. 자세한 내용은 [Exchange eDiscovery의 검색할 수 없는 항목](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)을 참조 하십시오.
    
      - **중복 제거 사용**   중복 메시지를 제외하려면 이 확인란을 선택합니다. 단일 메시지 인스턴스만 검색 사서함으로 복사됩니다.
    
      - **전체 로깅 사용**   검색 결과에 전체 로그를 포함하려면 이 확인란을 선택합니다.
    
      - **복사가 완료되면 메일 받기**   검색이 완료될 때 전자 메일 알림을 받으려면 이 확인란을 선택합니다.
    
      - **결과를 이 검색 사서함에 복사** **찾아보기**를 클릭하여 검색 결과를 복사할 검색 사서함을 선택합니다.
        
        ![검색 결과 복사](images/Dn624163.875e25ed-8308-408c-92c4-8c76fc9d9bfc(EXCHG.150).gif "검색 결과 복사")  

5.  **복사**를 클릭하여 검색 결과를 지정된 검색 사서함에 복사하는 프로세스를 시작합니다.

6.  세부 정보 창에 표시된 복사 상태에 대한 정보를 업데이트하려면 **새로 고침**![새로 고침 아이콘](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "새로 고침 아이콘")을 클릭합니다.

7.  복사가 완료되면 **열기**를 클릭하여 검색 사서함을 열고 검색 결과를 확인합니다.

## 셸을 사용 하 여 검색 결과 복사 하려면

**New-MailboxSearch** cmdlet을 사용 하 여 원본 위치 eDiscovery 검색 만들기, 후 *TargetMailbox* 매개 변수에서 지정한 검색 사서함으로 메시지를 복사 하는 검색을 시작 해야 합니다. 셸을 사용 하 여 eDiscovery 검색 만들기 (영문) 하는 방법에 대 한 정보를 참조 하십시오.

  - [셸을 사용하여 원본 위치 eDiscovery 검색 만들기](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [New-MailboxSearch](https://technet.microsoft.com/ko-kr/library/dd298064\(v=exchg.150\))

예는 지정 된 검색 사서함으로 검색 결과 복사 하려면 *Fabrikam 조사* 라는 eDiscovery 검색을 시작 하려면 다음 명령을 실행 하는 것입니다.

    Start-MailboxSearch "Fabrikam Investigation"

검색 결과 예상 하려면 *EstimateOnly* 스위치를 사용 하는 경우 검색 결과 복사 하기 전에 스위치를 제거 해야 합니다. 검색 결과를 복사할 대상 검색 사서함을 지정 해야 합니다. 예는 예측 전용 검색 다음 명령을 사용 하 여 만든 가정해보십시오.

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeUnsearchableItems

이 검색의 결과 검색 사서함으로 복사 하려면 다음 명령을 실행 하는:

  ```
  Set-MailboxSearch "FY13 Q2 Financial Results" -EstimateOnly $false -TargetMailbox "Discovery Search Mailbox"
  ```  
  
  ```
  Start-MailboxSearch "FY13 Q2 Financial Results"
  ```
## 검색 결과 복사 하는 방법에 대 한 자세한 내용

  - 검색 사서함으로 검색 결과 복사한 후에 PST 파일에 해당 검색 결과 내보낼 수 있습니다. 자세한 내용은 [PST 파일로 eDiscovery 검색 결과 내보내기](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)을 참조 하십시오.

  - 검색할 수 없는 항목에 대 한 자세한 내용은 [Exchange eDiscovery의 검색할 수 없는 항목](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)을 참조 하십시오.

  - (검색 조건에서 모든 키워드를 지정 하지 않으면) 하 여 특정 날짜 범위 내에서 모든 사서함 콘텐츠를 복사 하는 경우 자동으로 해당 날짜 범위 내에서 검색할 수 없는 항목을 모든 검색 결과에 포함 됩니다. 따라서 하지 검색 결과 복사할 때 **검색할 수 없는 항목 포함** 확인란을 선택 합니다. 그렇지 않은 경우 모든 검색할 수 없는 항목의 중복 복사본 검색 사서함으로 복사 됩니다.

  - 검색 결과 검색 사서함으로 복사, 외에도 예측 하거나 선택한 검색에 대 한 검색 결과 미리 볼 수도 있습니다.
    
      - **예상 검색 결과**   이 옵션의 예상 전체 크기 및 지정한 조건에 따라 검색에 의해 반환 되는 항목 수를 반환 합니다. 예상은 EAC에서 세부 정보 창에 표시 됩니다.
    
      - **검색 결과 미리 보기**   이 옵션을 통해를 보려면 검색 사서함에 복사 하는 대신 검색에서 반환 된 검색 결과 미리 볼 수 있습니다. 이 통해 신속 하 게 검색 결과 관련 된 있는지 여부를 결정할 수 있습니다. 결과 미리 보고 한 후에 검색 결과 범위를 좁힐 하 고 검색을 다시 실행 하 여 검색 쿼리를 수정할 수 있습니다. 항목 미리 보기 페이지에서 실제 검색 결과의 버전을 읽기 전용으로 설정 되므로 수 없는 이동, 편집, 삭제 또는 미리 보기 페이지에서 음성 메일로 착신 전환.
    
    자세한 내용은 [Estimate 또는 검색 결과 미리 보기를](create-an-in-place-ediscovery-search-exchange-2013-help.md)참조 하십시오.

