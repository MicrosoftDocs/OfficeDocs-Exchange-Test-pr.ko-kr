---
title: '시작 하거나 원본 위치 eDiscovery 검색을 중지 합니다.: Exchange 2013 Help'
TOCTitle: 시작 하거나 원본 위치 eDiscovery 검색을 중지 합니다.
ms:assetid: 0d546763-4bf5-4523-91f4-d181b7ee4ac2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335090(v=EXCHG.150)
ms:contentKeyID: 50482495
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 시작 하거나 원본 위치 eDiscovery 검색을 중지 합니다.

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-07-14_

언제 든 지 원본 위치 eDiscovery 검색을 다시 시작 하거나 중지 수 있습니다. 예: 검색 속성을 수정 하려는 경우 검색 키워드 또는 사서함 검색을 같은 먼저 중지 해야 합니다. 그런 다음 필요한 변경 작업을 수행 하는 후 검색을 다시 시작할 수 있습니다.


> [!WARNING]
> 원본 위치 eDiscovery 검색을 다시 시작 하는 경우에 검색에 지정 된 검색 사서함에 복사 하는 검색 결과 제거 됩니다.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "원본 위치 eDiscovery" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 시작 하거나 원본 위치 eDiscovery 검색을 중지 하려면

1.  **규정 준수 관리** 로 이동 \> **원본 위치 eDiscovery 및 유지** 합니다.

2.  진행 중인 검색을 중지 하려면 검색을 선택한 다음 **검색을 중지** 를 클릭 합니다.

3.  중단 된 검색을 시작 하려면 검색을 선택한 다음 **다시 시작 설정 검색** 을 클릭 합니다.

## 셸을 사용 하 여 시작 하거나 원본 위치 eDiscovery 검색을 중지 하려면

원본 위치 eDiscovery 검색을 시작 하는 방법의 예를 참조 하십시오. "1" [Start-MailboxSearch](https://technet.microsoft.com/ko-kr/library/dd351245\(v=exchg.150\))의 예제입니다.

원본 위치 eDiscovery 검색을 중지 하는 방법의 예를 참조 하십시오. "1" [Stop-MailboxSearch](https://technet.microsoft.com/ko-kr/library/dd351075\(v=exchg.150\))의 예제입니다.

