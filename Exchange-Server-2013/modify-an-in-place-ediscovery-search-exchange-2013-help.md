---
title: '원본 위치 eDiscovery 검색 수정: Exchange 2013 Help'
TOCTitle: 원본 위치 eDiscovery 검색 수정
ms:assetid: 3162743c-cc12-4997-91e0-bcbfea8bcb17
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335182(v=EXCHG.150)
ms:contentKeyID: 50482817
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원본 위치 eDiscovery 검색 수정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-08-27_

원본 위치 eDiscovery 검색을 만든 후에 검색 매개 변수를 변경 하도록 수정할 수 있습니다. 예: 검색할 사서함을 변경할 수 있습니다, 날짜 범위, 키워드, 로깅 옵션 또는 하면 검색 결과 저장 하는 다른 검색 사서함을 지정할 수 있습니다. 검색 속성을 변경 사항을 검색을 다시 시작 하는 경우 사용 됩니다.


> [!WARNING]
> 원본 위치 eDiscovery 검색을 실행 하는 경우이 수정 하기 전에 중지 해야 합니다. 검색을 다시 시작 하면 마지막으로 실행 된 검색 결과 검색 사서함에서 제거 됩니다. 그러나 이전 검색 결과에서 로그를 저장 됩니다.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2 ~ 5 분입니다.

  - 원본 위치 eDiscovery 검색 만들어진 및 실행 되지 않습니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "원본 위치 eDiscovery" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 원본 위치 eDiscovery 검색을 수정 하려면

1.  **준수 관리** \> **원본 위치 eDiscovery 및 유지**로 이동합니다.

2.  목록 보기에서 수정 하려는 원본 위치 eDiscovery 검색을 선택 하 고![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")**편집** 을 클릭 합니다.

3.  **원본 위치 eDiscovery 및 유지** 에서 다음 설정을 수정할 수 있습니다.
    
      - **이름** 페이지에서 검색 및 선택적 설명에 대 한 이름을 수정 합니다.
    
      - **사서함** 페이지에서 사서함 검색을 수정 합니다. 모든 사서함에서 검색 합니다. 수도 있고 검색 하는 특정 이벤트를 선택할 수 있습니다.
        

        > [!IMPORTANT]
        > 대기 Exchange 2013 사서함 서버의 모든 사서함을 보류 <STRONG>모든 사서함을 검색</STRONG> 옵션을 사용할 수 없습니다. In-place Hold를 만들려면 <STRONG>지정 사서함 검색을</STRONG> 선택 해야 합니다. 자세한 내용은 <A href="create-or-remove-an-in-place-hold-exchange-2013-help.md">만들기 또는 In-place Hold 제거</A>을 참조 하십시오.

    
      - **검색 쿼리** 페이지에서 다음 필드를 수정 합니다.
        
          - **모든 사용자 사서함 콘텐츠를 포함 합니다.**    보류에서 선택한 사서함에 모든 콘텐츠를 배치 하려면이 옵션을 선택 합니다.
        
          - **조건 기반의 필터**   키워드, 시작 및 종료 날짜, 보낸 사람 및 받는 사람 주소, 메시지 유형을 포함한 검색 조건을 지정하려면 이 옵션을 선택합니다.
    
      - **원본 위치 유지** 페이지에서 **선택한 사서함에서 검색 쿼리 일치에 전체 콘텐츠 유지** 확인란을 선택 하 고 원본 위치 유지에 항목을 배치 하려면 다음 옵션 중 하나를 선택 합니다.
        
          - **무기한 보류**   반환된 항목을 무기한 보류 상태로 설정하려면 이 옵션을 선택합니다. 보류 중인 항목은 검색에서 사서함을 제거하거나 검색을 제거할 때까지 유지됩니다.
        
          - **수신 날짜를 기준으로 항목을 보관할 날짜 수 지정** 특정 기간 동안 항목을 보관하려면 이 옵션을 사용합니다. 예를 들어 조직에서 모든 메시지를 7년 이상 유지해야 할 경우에 이 옵션을 사용할 수 있습니다. 보존 정책과 *시간 기반* 원본 위치 유지를 사용하여 7년 후에 항목이 삭제되도록 할 수 있습니다.
            

            > [!IMPORTANT]
            > 법적 목적을 위해 사서함이나 항목을 원본 위치 유지 상태로 설정하는 경우 일반적으로 항목을 무기한 보류했다가 사례나 조사가 완료될 때 보류 상태를 해제하는 것이 좋습니다.



4.  **저장**을 클릭합니다.

## 셸을 사용 하 여 원본 위치 eDiscovery 검색을 수정 하려면

원본 위치 eDiscovery 검색 DG ProjectManagers 메일 그룹의 구성원에 게 속한 사서함을 검색 하려면 검색 Project Contoso를 수정 하는이 예제입니다.

    Set-MailboxSearch -Identity "Search-Project Contoso" -SourceMailboxes "DG-ProjectManagers"

## 작동 여부는 어떻게 확인합니까?

을 원본 위치 eDiscovery 검색 수정 되었는지 확인 하려면 다음 중 하나를 수행 합니다.

  - EAC를 사용 하 여 검색의 속성을 확인 합니다.

  - 검색의 속성을 확인 하려면 셸에서 **Get-MailboxSearch** cmdlet을 사용 합니다. 사서함 검색의 속성을 확인 하는 방법의 예를 [Get-MailboxSearch](https://technet.microsoft.com/ko-kr/library/dd351021\(v=exchg.150\))에서 "예제" 섹션을 참조 하십시오.


> [!NOTE]
> 검색 속성;의 전체 목록을 반환 하는 검색의 이름을 지정 해야하는 eDiscovery 검색에 대 한 정보를 검색 하려면 Exchange Online 에서 <STRONG>Get-MailboxSearch</STRONG> 를 사용 하는 경우 예: <CODE>Get-MailboxSearch "Contoso Legal Case"</CODE>합니다. 매개 변수를 사용 하지 않고 <STRONG>Get-MailboxSearch</STRONG> cmdlet을 실행 하는 경우 다음과 같은 속성 반환 되지 않습니다. 
> <UL>
> <LI>
> <P>SourceMailboxes</P>
> <LI>
> <P>Sources</P>
> <LI>
> <P>SearchQuery</P>
> <LI>
> <P>ResultsLink</P>
> <LI>
> <P>PreviewResultsLink</P>
> <LI>
> <P>Errors</P></LI></UL>조직에서 모든 eDiscovery 검색에 대 한 이러한 속성을 반환 하는 리소스를 많이 필요 하다는 메시지가 나타나는 이유는 합니다.


