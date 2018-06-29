---
title: '기본 오프 라인 주소록을 변경 합니다.: Exchange 2013 Help'
TOCTitle: 기본 오프 라인 주소록을 변경 합니다.
ms:assetid: 61abf78e-2543-4431-acc8-839e3c7a4548
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998569(v=EXCHG.150)
ms:contentKeyID: 50483250
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 기본 오프 라인 주소록을 변경 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-12-16_

기본적으로 사서함 서버 역할을 설치하면 기본 오프라인 주소록이라는 웹 기반 기본 OAB(오프라인 주소록)가 만들어집니다. Exchange 조직에 있는 OAB 중 원하는 항목을 기본 OAB로 설정할 수 있습니다. 이렇게 새로 설정한 기본 OAB는 새로 작성되는 모든 사서함 데이터베이스와 연결됩니다. 조직에는 기본 OAB가 하나만 있을 수 있습니다. 기본 OAB를 삭제할 경우 MicrosoftExchange에서 다른 OAB를 기본값으로 자동 지정하지 않습니다. 수동으로 다른 OAB를 기본값으로 지정해야 합니다.

OAB와 관련된 추가 관리 작업에 대한 자세한 내용은 [오프 라인 주소록 절차](offline-address-book-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "오프라인 주소록" 항목

  - Exchange Online에서는 기본적으로 주소 목록 역할이 어떤 역할 그룹에도 할당되지 않습니다. 주소 목록 역할이 필요한 cmdlet을 사용하려면 역할 그룹에 이 역할을 추가해야 합니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 항목의 "역할 그룹에 역할 추가" 섹션을 참조하세요.

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 기본 OAB 변경

이 예에서는 이름이 My OAB인 OAB를 기본 OAB로 설정합니다.

    Set-OfflineAddressBook -Identity "My OAB" -IsDefault $true

구문과 매개 변수에 대한 자세한 내용은 [Set-OfflineAddressBook](https://technet.microsoft.com/ko-kr/library/aa996330\(v=exchg.150\))를 참조하십시오.

