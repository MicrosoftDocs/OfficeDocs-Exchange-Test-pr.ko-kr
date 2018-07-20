---
title: '주소록 정책 설정 변경: Exchange 2013 Help'
TOCTitle: 주소록 정책 설정 변경
ms:assetid: ba1ca350-71c2-4c60-a612-33bfa9320b5e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh529941(v=EXCHG.150)
ms:contentKeyID: 50484005
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주소록 정책 설정 변경

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-03-30_

ABP(주소록 정책)를 만들면 이름 및 할당된 GAL(전체 주소 목록), OAB(오프라인 주소록), 방 목록 및 주소 목록을 보거나 수정할 수 있습니다.

ABP와 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 주소록 정책 절차](address-book-policy-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md) 항목의 "주소록 정책" 항목

  - 조직의 ABP를 만드는 과정은 여러 단계로 이루어지며 계획이 필요합니다. 자세한 내용은 [시나리오: 주소록 정책 배포](scenario-deploying-address-book-policies-exchange-2013-help.md)을 참조하십시오.

  - ABP를 구성하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

  - 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

## 무슨 작업을 하고 싶으십니까?

## ABP의 OAB, 방 목록 및 GAL 변경

이 예에서는 All Fabrikam ABP라는 이름의 ABP가 할당된 사서함 사용자가 사용할 OAB, 대화방 목록 및 GAL을 변경합니다.

    Set-AddressBookPolicy -Identity "All Fabrikam ABP" -OfflineAddressBook \Fabrikam-OAB-2 -GlobalAddressList "\All Fabrikam GAL" -RoomList "\All Fabrikam Rooms"

## 주소 목록에 ABP 바꾸기

기존 ABP에 대 한 지정 하는 주소 목록에는 ABP.에서 모든 주소 목록 바꾸기

이 예제에서는 한 정부 기관 A. 라는 ABP에 대 한 GovernmentAgencyA Atlanta 및 GovernmentAgencyA 모스크바 이라는 주소 목록을 사용 하 여 기존 주소 목록을 대체합니다

    Set-AddressBookPolicy -Identity "Government Agency A" -AddressLists "GovernmentAgencyA-Atlanta","GovernmentAgencyA-Moscow"

## ABP에 주소 목록을 추가합니다

ABP.에 새 값을 추가 하는 경우 이러한 주소 목록을 지정 해야하는 유지 하기 위해 ABP에 이미 정의 된 주소 목록

ABP에 Contoso 시카고 라는 주소 목록 이라는 Contoso Seattle 이라는 주소 목록을 사용 하도록 이미 구성 되어있는 ABP Contoso, 추가 하는이 예제입니다.

    Set-AddressBookPolicy -Identity "ABP Contoso" -AddressLists "Contoso-Chicago","Contoso-Seattle"

## ABP에서 주소 목록을 제거합니다

ABP에 이미 정의 된 기존 주소 목록을 제거 하려면 유지 하려는 주소 목록을 지정 해야 합니다.

예, 라는 ABP Fabrikam ABP Fabrikam HR 및 재무 Fabrikam 이라는 주소 목록을 사용 합니다. Fabrikam HR 주소 목록에서의 ABP를 제거 하려면 유지 하려는 Fabrikam 재무 주소 목록을 지정 합니다.

    Set-AddressBookPolicy -Identity "ABP Fabrikam" -AddressLists Fabrikam-Finance

## 자세한 내용

구문과 매개 변수에 대한 자세한 내용은 [Set-AddressBookPolicy](https://technet.microsoft.com/ko-kr/library/hh529945\(v=exchg.150\))를 참조하십시오.

