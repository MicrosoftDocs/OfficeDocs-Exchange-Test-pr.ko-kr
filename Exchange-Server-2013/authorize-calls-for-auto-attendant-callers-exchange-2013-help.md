---
title: '자동 전화 교환 발신자에 대 한 통화 권한 부여: Exchange 2013 Help'
TOCTitle: 자동 전화 교환 발신자에 대 한 통화 권한 부여
ms:assetid: c6c94fad-64df-44aa-a198-980f017ef716
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb691238(v=EXCHG.150)
ms:contentKeyID: 51407738
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 자동 전화 교환 발신자에 대 한 통화 권한 부여

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-21_

UM(통합 메시징) 자동 전화 교환에서 전화 걸기 권한 부여를 사용하도록 설정할 수 있습니다. 자동 전화 교환의 전화 걸기 권한 부여는 자동 전화 교환으로 전화를 거는 사용자가 국내 또는 국제 전화나 *외부로 전화 걸기*를 수행하지 못하도록 차단하는 데 사용됩니다. 외부로 전화 걸기는 사용자가 UM 자동 전화 교환에 구성된 전화 번호로 전화를 건 후 통합 메시징에서 사용자에 대해 발신 전화를 걸 때 수행됩니다.

외부로 전화 걸기와 관련된 추가 관리 작업에 대한 자세한 내용은 [사용자가 통화 절차를 수행 하도록 허용](allowing-users-to-make-calls-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 절차를 수행하기 전에 UM 다이얼 플랜에 대해 국내 및 국제 전화 걸기 규칙이 만들어졌는지 확인하십시오. 자세한 단계는 [사용자에 대 한 전화걸기 규칙 만들기](create-dialing-rules-for-users-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 국내 규칙 그룹에 대해 UM 자동 전화 교환에서 전화 걸기 권한 부여를 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 전화 걸기 권한 부여를 만들 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지 \> **전화 걸기 권한 부여**에서**권한이 부여된 국내 전화 걸기 규칙 그룹** 아래에 있는 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **허용할 전화 걸기 규칙 그룹 선택** 페이지에서 전화 걸기 규칙 그룹을 선택하고 **확인**, **저장**을 차례로 클릭합니다.

## EAC를 사용하여 국제 규칙 그룹에 대해 UM 자동 전화 교환에서 전화 걸기 권한 부여를 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 전화 걸기 권한 부여를 만들 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지 \> **전화 걸기 권한 부여**에서**권한이 부여된 국제 전화 걸기 규칙 그룹** 아래에 있는 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **허용할 전화 걸기 규칙 그룹 선택** 페이지에서 전화 걸기 규칙 그룹을 선택하고 **확인**, **저장**을 차례로 클릭합니다.

## 셸을 사용하여 UM 자동 전화 교환에서 국내 및 국제 전화 걸기 권한 부여를 사용하도록 설정

이 예에서는 `MyUMAutoAttendant`라는 UM 자동 전화 교환에서 InCountry/RegionGroup1, InCountry/RegionGroup2, InternationalGroup1 및 InternationalGroup2 전화 걸기 권한 부여를 사용하도록 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

