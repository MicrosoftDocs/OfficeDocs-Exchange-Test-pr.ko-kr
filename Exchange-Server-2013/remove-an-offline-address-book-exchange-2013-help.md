---
title: '오프 라인 주소록을 제거 합니다.: Exchange 2013 Help'
TOCTitle: 오프 라인 주소록을 제거 합니다.
ms:assetid: d69f1e8a-b3cb-4739-90cd-85ea450d06f3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124744(v=EXCHG.150)
ms:contentKeyID: 50484243
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 오프 라인 주소록을 제거 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-12-16_

이 항목에서는 오프 라인 주소록 (OAB)를 제거 하는 방법에 설명 합니다.

OAB와 관련된 추가 관리 작업에 대한 자세한 내용은 [오프 라인 주소록 절차](offline-address-book-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "오프라인 주소록" 항목

  - Exchange Online에서는 기본적으로 주소 목록 역할이 어떤 역할 그룹에도 할당되지 않습니다. 주소 목록 역할이 필요한 cmdlet을 사용하려면 역할 그룹에 이 역할을 추가해야 합니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 항목의 "역할 그룹에 역할 추가" 섹션을 참조하세요.

  - 사용자에 게 또는 사서함 데이터베이스에 연결 된 OAB를 제거한 후 해당 사용자에 대 한 새 OAB를 할당할 때까지 받는 기본 OAB를 다운로드 합니다. 기본 OAB를 제거 하는 경우에 기본 OAB로 다른 OAB를 할당 해야 합니다. 기본 OAB를 변경 하는 방법에 대 한 자세한 내용은 [기본 오프 라인 주소록을 변경 합니다.](change-the-default-offline-address-book-exchange-2013-help.md)합니다.

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용 하 여 OAB를 제거 하려면

이 예에서는 My OAB 라는 OAB를 제거 합니다.

    Remove-OfflineAddressBook -Identity "My OAB"

OAB를 제거 하 고 enter 키를 누른 다음을 확인 하려면 **Y** 입력 합니다.

자세한 구문 및 매개 변수 정보에 대 한 [Remove-OfflineAddressBook](https://technet.microsoft.com/ko-kr/library/bb123594\(v=exchg.150\))를 참조 하십시오.

