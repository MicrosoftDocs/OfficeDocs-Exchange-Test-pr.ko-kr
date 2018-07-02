---
title: '주소 목록에 추가 하거나 오프 라인 주소록에서 주소 목록을 제거합니다: Exchange 2013 Help'
TOCTitle: 주소 목록에 추가 하거나 오프 라인 주소록에서 주소 목록을 제거합니다
ms:assetid: 86bd5651-ad41-4516-bf23-6579f4e4da03
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123563(v=EXCHG.150)
ms:contentKeyID: 50483592
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주소 목록에 추가 하거나 오프 라인 주소록에서 주소 목록을 제거합니다

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-12-16_

셸을 사용하여 OAB(오프라인 주소록)에서 주소 목록을 추가 또는 제거할 수 있습니다. 기본적으로 GAL(전체 주소 목록)이 포함된 기본 오프라인 주소록이라는 이름의 OAB가 있습니다. OAB는 자신이 포함하는 주소 목록을 기반으로 생성됩니다. 사용자가 다운로드할 수 있는 사용자 지정 OAB를 만들려면 OAB에서 주소 목록을 추가하거나 제거할 수 있습니다.

OAB와 관련된 추가 관리 작업에 대한 자세한 내용은 [오프 라인 주소록 절차](offline-address-book-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "오프라인 주소록" 항목

  - Exchange Online에서는 기본적으로 주소 목록 역할이 어떤 역할 그룹에도 할당되지 않습니다. 주소 목록 역할이 필요한 cmdlet을 사용하려면 역할 그룹에 이 역할을 추가해야 합니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 항목의 "역할 그룹에 역할 추가" 섹션을 참조하세요.

  - 주소 목록의 변경 내용은 해당 주소 목록이 포함된 OAB가 생성될 때까지 클라이언트에서 다운로드할 수 없습니다. 자세한 내용은 [오프 라인 주소록 업데이트](update-an-offline-address-book-exchange-2013-help.md)을 참조하십시오.

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 OAB에 주소 목록 추가

*AddressLists* 매개 변수를 사용하면 현재 존재하는 모든 주소 목록을 덮어씁니다. *AddressLists* 매개 변수를 사용할 때 기존 주소 목록을 포함해야만 OAB에서 해당 주소 목록을 계속 생성할 수 있습니다. 이 예에서는 AddressList1 및 AddressList2가 있는 상황에서 AddressList3을 추가합니다.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2,AddressList3

구문과 매개 변수에 대한 자세한 내용은 [Set-OfflineAddressBook](https://technet.microsoft.com/ko-kr/library/aa996330\(v=exchg.150\))을 참조하십시오.

## 셸을 사용하여 OAB에서 주소 목록 제거

OAB에서 주소 목록을 제거하려면 주소 목록에서 해당 주소 목록을 생략하면 됩니다. 이 예에서는 AddressList1, AddressList2, AddressList3이 있는 상황에서 AddressList3을 제거합니다.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2

구문과 매개 변수에 대한 자세한 내용은 [Set-OfflineAddressBook](https://technet.microsoft.com/ko-kr/library/aa996330\(v=exchg.150\))를 참조하십시오.

