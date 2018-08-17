---
title: '전자 메일 주소 정책 제거: Exchange 2013 Help'
TOCTitle: 전자 메일 주소 정책 제거
ms:assetid: f1d05223-7d41-406d-8fae-f4227be1c1c2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125181(v=EXCHG.150)
ms:contentKeyID: 50484509
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전자 메일 주소 정책 제거

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-13_

기본적으로 Exchange 전자 메일 주소의 로컬 일부로 받는 사람의 별칭을 지정 하 고 기본 허용 도메인을 사용 하 여 전자 메일 주소 정책을 포함 합니다. 전자 메일 주소의 로컬 부분은 "at" 기호 앞에 나타나는 이름 (@). 조직에서 모든 사용자에 게이 전자 메일 주소 정책을 적용 됩니다. 이 전자 메일 주소 정책을 제거할 수 없습니다.

전자 메일 주소 정책에 관련 된 추가 관리 작업을 [전자 메일 주소 정책 절차](email-address-policy-procedures-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 사항은 무엇입니까?

  - 예상 완료 시간: 5분

  - 기본 정책으로 받는 사람에 사용 되는 전자 메일 주소 정책을 제거 하는 경우 받는 사람에 대해 구성 된 다른 정책이 기본 정책 사용 됩니다.

  - 기본 정책을 삭제할 수 없습니다. 기본 정책을 삭제 하려는 경우 기본적으로 다른 정책의 먼저 할당 해야 합니다.

  - 삭제 하려는 전자 메일 주소 정책을 3, 000 개 이상의 받는 사람을 포함 하는 경우에이 절차를 수행 하려면 셸을 사용 해야 합니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [전자 메일 주소 및 주소록](email-addresses-and-address-books-exchange-2013-help.md)의 "전자 메일 주소 정책" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

> [!CAUTION]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, 또는 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>


## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 전자 메일 주소 정책을 제거 하려면

1.  **메일 흐름** \> **전자 메일 주소 정책**으로 이동합니다.

2.  목록 보기에서 삭제 하 고 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭 한 다음 원하는 전자 메일 주소 정책을 선택 합니다.

3.  경고에서 **예** 를 정책을 제거를 클릭 합니다.

## 셸을 사용 하 여 전자 메일 주소 정책 제거

이 예제에서는 South East Offices 전자 메일 주소 정책에서 제거 합니다.

    Remove-EmailAddressPolicy -Identity "South East Offices"

정책을 제거 하 고 enter 키를 누른 다음을 확인 하려면 **Y** 입력 합니다.

자세한 구문 및 매개 변수 정보에 대 한 [Remove-EmailAddressPolicy](https://technet.microsoft.com/ko-kr/library/bb124504\(v=exchg.150\))를 참조 하십시오.

