---
title: '원본 위치 eDiscovery 검색 제거: Exchange 2013 Help'
TOCTitle: 원본 위치 eDiscovery 검색 제거
ms:assetid: 78461a78-1255-4a26-9d36-c6b8eb82a4f9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298078(v=EXCHG.150)
ms:contentKeyID: 50483455
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원본 위치 eDiscovery 검색 제거

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-07-14_

Microsoft Exchange Server 2013 를 사서함 콘텐츠를 검색 하려면 원본 위치 eDiscovery를 사용할 수 있습니다. 언제 든 지 원본 위치 eDiscovery 검색을 제거할 수 있습니다. 원본 위치 eDiscovery 검색을 제거 하면 검색 결과 검색 사서함에서 제거 됩니다.


> [!WARNING]
> 원본 위치 eDiscovery 검색을 삭제 하면 검색 사서함에 복사 하는 모든 검색 결과 제거 됩니다.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2 ~ 5분.

  - 원본 위치 유지를 사용 하도록 설정 된 원본 위치 eDiscovery 검색을 제거 하려면 먼저 제거 해야 원본 위치 유지에서 검색 합니다. 자세한 내용은 [만들기 또는 In-place Hold 제거](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/create-or-remove-in-place-holds)를 참조 합니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "원본 위치 eDiscovery" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 원본 위치 eDiscovery 검색을 제거 하려면

1.  **준수 관리** \> **원본 위치 eDiscovery 및 유지**로 이동합니다.

2.  목록 보기에서 제거 하려는 원본 위치 eDiscovery 검색을 선택 하 고![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")**삭제** 를 클릭 합니다.

## 셸을 사용 하 여 원본 위치 eDiscovery 검색을 제거 하려면

원본 위치 eDiscovery 검색을 제거 하는 방법의 예를 [Remove-MailboxSearch](https://technet.microsoft.com/ko-kr/library/dd298130\(v=exchg.150\))에서 "예제" 섹션을 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

원본 위치 eDiscovery 검색을 성공적으로 제거 했는지를 확인 하려면 다음 중 하나를 수행 합니다.

  - EAC를 사용 하 여 검색 더이상 **원본 위치 eDiscovery 및 유지** 탭의 목록 보기에 표시 되는지 확인 합니다.

  - 원본 위치 eDiscovery 검색을 검색 하려면 **Get-MailboxSearch** cmdlet을 사용 합니다. 원본 위치 eDiscovery 검색을 검색 하는 방법의 예를 [Get-MailboxSearch](https://technet.microsoft.com/ko-kr/library/dd351021\(v=exchg.150\))에서 "예제" 섹션을 참조 하십시오.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


