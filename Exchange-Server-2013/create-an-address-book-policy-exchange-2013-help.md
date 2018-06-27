---
title: '주소록 정책 만들기: Exchange 2013 Help'
TOCTitle: 주소록 정책 만들기
ms:assetid: 6359abaf-e6f6-4667-8c2b-3860728b39a9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh529931(v=EXCHG.150)
ms:contentKeyID: 50483265
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주소록 정책 만들기

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-12-16_

ABP(주소록 정책)를 사용하면 사용자를 특정 그룹으로 분할하여 조직의 GAL(전체 주소 목록)에 대한 사용자 지정 보기를 제공할 수 있습니다. ABP를 만들 때 GAL, OAB(오프라인 주소록), 방 목록 및 하나 이상의 주소 목록을 정책에 할당합니다. 그런 다음 ABP를 사서함 사용자에게 할당하여 사서함 사용자에게 Outlook과 Outlook Web App에서 사용자 지정된 GAL에 액세스할 수 있는 권한을 제공할 수 있습니다. 여러 개의 GAL이 필요한 온-프레미스 조직에서 보다 간단하게 GAL 조각화를 수행할 수 있는 메커니즘을 제공하는 것이 목표입니다. ABP에 대한 자세한 내용은 [주소록 정책](address-book-policies-exchange-2013-help.md)를 참조하십시오.

ABP와 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 주소록 정책 절차](address-book-policy-procedures-exchange-2013-help.md) 항목을 참조하십시오.

이 절차를 사용하는 경우는 [시나리오: 주소록 정책 배포](scenario-deploying-address-book-policies-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md) 항목의 "주소록 정책" 항목

  - Exchange Online에서는 기본적으로 주소 목록 역할이 어떤 역할 그룹에도 할당되지 않습니다. 주소 목록 역할이 필요한 cmdlet을 사용하려면 역할 그룹에 이 역할을 추가해야 합니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 항목의 "역할 그룹에 역할 추가" 섹션을 참조하세요.

  - 조직의 ABP를 만드는 과정은 여러 단계로 이루어지며 계획이 필요합니다. 자세한 내용은 [시나리오: 주소록 정책 배포](scenario-deploying-address-book-policies-exchange-2013-help.md)를 참조하십시오.

  - ABP를 만드는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

  - 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

## 셸을 사용하여 ABP 만들기

이 예제에서는 다음과 같은 설정으로 ABP를 만듭니다.

  - **이름:** 모든 Fabrikam ABP

  - **GAL:** 모든 Fabrikam

  - **OAB:** Fabrikam-All-OAB

  - **대화방 목록:** All Fabrikam Rooms

  - **주소 목록:** All Fabrikam, All Fabrikam Mailboxes, All Fabrikam DLs 및 All Fabrikam Contacts

<!-- end list -->

    New-AddressBookPolicy -Name "All Fabrikam ABP" -AddressLists "\All Fabrikam","\All Fabrikam Mailboxes","\All Fabrikam DLs","\All Fabrikam Contacts" -OfflineAddressBook \Fabrikam-All-OAB -GlobalAddressList "\All Fabrikam" -RoomList "\All Fabrikam Rooms"

구문과 매개 변수에 대한 자세한 내용은 [New-AddressBookPolicy](https://technet.microsoft.com/ko-kr/library/hh529913\(v=exchg.150\))를 참조하십시오.

## 자세한 내용

[메일 사용자에 게 주소록 정책 할당](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)

