---
title: '사서함 감사 로그 검색 만들기: Exchange 2013 Help'
TOCTitle: 사서함 감사 로그 검색 만들기
ms:assetid: 48ba22cf-b1f2-4dbc-98fc-fed22d97db14
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff461929(v=EXCHG.150)
ms:contentKeyID: 50483021
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 감사 로그 검색 만들기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-11_

사서함 감사 로그 검색을 만들어 사서함 한 개 이상을 비동기적으로 검색하고 검색 결과를 지정된 주소에 XML 파일의 전자 메일로 전송할 수 있습니다.

단일 사서함에 대해 사서함 감사 로그를 검색하고 셸 창에 결과를 표시하려면 [사서함에 대 한 사서함 감사 로그를 검색 합니다.](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md)을 사용합니다.

사서함 감사 로깅과 관련된 추가 관리 작업에 대한 자세한 내용은 [사서함 감사 로깅 절차](mailbox-audit-logging-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "사서함 감사 로깅" 항목

  - 기본적으로 사서함 감사 로깅은 모든 사서함에 대해 사용하지 않도록 설정되어 있습니다. 감사할 각 사서함에 대해, 감사 로깅을 사용하도록 설정하고 감사할 사서함 소유자, 대리인 또는 관리자 작업을 지정해야 합니다. 자세한 내용은 [사서함 감사 사서함에 대해 로깅을 사용 하지 않도록 설정 하거나 사용](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)을 참조하십시오.

  - EAC를 사용하여 사서함 감사 로그에서 소유자 액세스를 검색할 수는 없습니다. EAC의 감사 섹션에는 비소유자 사서함 액세스에 대한 보고서가 포함되어 있으며 이 섹션에서 비소유자 액세스 이벤트를 검색하고 내보낼 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 감사 로그 검색 만들기

1.  **규정 준수 관리** \> **감사**로 이동합니다.

2.  목록 보기에서 **사서함 감사 로그 내보내기**를 선택합니다.

3.  **사서함 감사 로그 내보내기**에서 다음 필드에 값을 입력하고 **내보내기**를 클릭합니다.
    
      - **시작 날짜**
    
      - **끝 날짜**
    
      - **다음 사서함을 검색하거나 공백을 유지하여 비소유자가 액세스한 모든 사서함 찾기**
        

        > [!WARNING]
        > 조직의 사서함 수와 각 사서함의 사서함 감사 로그 데이터 양에 따라 모든 사서함을 검색하는 데 오랜 시간이 걸릴 수 있습니다.

    
      - **검색에 액세스한 사용자**
        
        다음 중 검색할 액세스 이벤트 유형을 선택합니다.
        
          - **모든 비소유자**
        
          - **외부 사용자**
        
          - **관리자 및 위임된 사용자**
        
          - **관리자**
    
      - **다음 사람에게 감사 보고서 보내기**

## 셸을 사용하여 사서함 감사 로그 검색 만들기

셸을 사용하여 사서함 감사 로그 검색을 만드는 방법의 예제를 보려면 **New-MailboxAuditLogSearch**의 [Example 1](https://technet.microsoft.com/ko-kr/95365cab-bbb2-4a64-8e8f-1c89fa9e0352\(exchg.150\)#example1) 항목을 참조하십시오.

