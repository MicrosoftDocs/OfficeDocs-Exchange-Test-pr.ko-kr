---
title: '사서함에 대 한 사서함 감사 로그를 검색 합니다.: Exchange 2013 Help'
TOCTitle: 사서함에 대 한 사서함 감사 로그를 검색 합니다.
ms:assetid: 5b518a08-3b51-4ba3-bfbd-0e35cc5ff374
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff461930(v=EXCHG.150)
ms:contentKeyID: 50483202
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 대 한 사서함 감사 로그를 검색 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

사서함 감사 로그 항목을 동시에 검색하고 검색 결과를 셸에 표시할 수 있습니다.

여러 사서함의 사서함 감사 로그를 검색하고 전자 메일을 통해 지정된 주소로 결과를 보내려면 대신 사서함 감사 로그 검색을 만들어야 합니다. 자세한 내용은 [사서함 감사 로그 검색 만들기](create-a-mailbox-audit-log-search-exchange-2013-help.md) 항목을 참조하십시오.

사서함 감사 로깅과 관련된 추가 관리 작업에 대한 자세한 내용은 [사서함 감사 로깅 절차](mailbox-audit-logging-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "사서함 감사 로깅" 항목

  - 기본적으로 사서함 감사 로깅은 모든 사서함에 대해 사용하지 않도록 설정되어 있습니다. 감사할 각 사서함에 대해, 감사 로깅을 사용하도록 설정하고 감사할 사서함 소유자, 대리인 또는 관리자 작업을 지정해야 합니다. 자세한 내용은 [사서함 감사 사서함에 대해 로깅을 사용 하지 않도록 설정 하거나 사용](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md) 항목을 참조하십시오.

  - 사서함의 사서함 감사 로그를 검색하는 데에는 EAC를 사용할 수 없습니다. 하지만 EAC를 사용하여 비소유자 사서함 액세스 보고서를 검색하고 내보낼 수는 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 사서함에 대한 사서함 감사 로그를 검색합니다.

셸을 사용하여 사서함의 사서함 감사 로그를 검색하는 방법의 예를 보려면 [Search-MailboxAuditLog](https://technet.microsoft.com/ko-kr/library/ff522360\(v=exchg.150\))의 [Examples](https://technet.microsoft.com/ko-kr/ff522360\(exchg.150\)#examples) 항목을 참조하십시오.

