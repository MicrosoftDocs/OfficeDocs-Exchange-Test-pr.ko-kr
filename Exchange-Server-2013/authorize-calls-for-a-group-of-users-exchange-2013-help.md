---
title: '사용자 그룹에 대 한 통화 권한 부여: Exchange 2013 Help'
TOCTitle: 사용자 그룹에 대 한 통화 권한 부여
ms:assetid: 7fc36757-868c-4bde-b793-6ae630da155c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232099(v=EXCHG.150)
ms:contentKeyID: 51407716
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자 그룹에 대 한 통화 권한 부여

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-21_

UM(통합 메시징) 사서함 정책에서 전화 걸기 권한 부여를 사용하도록 설정할 수 있습니다. 사서함 정책에서 전화 걸기 권한 부여를 사용하여 UM 사서함 정책에 연결된, 인증된 Outlook Voice Access 사용자가 국내나 국제 전화 또는 *외부로 전화 걸기*를 수행하지 못하도록 차단할 수 있습니다. 외부로 전화 걸기는 통합 메시징에서 UM 다이얼 플랜에 대해 구성된 Outlook Voice Access 전화 번호로 전화를 건 후 통합 메시징에서 사용자에 대해 발신 전화를 걸 경우 일어나는 과정입니다. UM 사서함 정책에 대한 설정을 구성하는 경우 해당 설정이 UM 사서함 정책과 연결된 모든 UM 사용 가능 사용자에게 적용됩니다.

외부로 전화 걸기와 관련된 추가 관리 작업에 대한 자세한 내용은 [사용자가 통화 절차를 수행 하도록 허용](allowing-users-to-make-calls-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 절차를 수행하기 전에 UM 다이얼 플랜에 대해 국내 및 국제 전화 걸기 규칙이 만들어졌는지 확인하십시오. 자세한 단계는 [사용자에 대 한 전화걸기 규칙 만들기](create-dialing-rules-for-users-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 국내 전화 걸기 규칙 그룹에 대해 UM 사서함 정책에서 전화 걸기 권한 부여를 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 전화 걸기 권한 부여를 만들 UM 사서함 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지 \> **전화 걸기 권한 부여**에서**권한이 부여된 국내 전화 걸기 규칙 그룹** 아래에 있는 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **허용할 전화 걸기 규칙 그룹 선택** 페이지에서 전화 걸기 규칙 그룹을 선택하고 **확인**, **저장**을 차례로 클릭합니다.

## EAC를 사용하여 국제 전화 걸기 규칙 그룹에 대해 UM 사서함 정책에서 전화 걸기 권한 부여를 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 전화 걸기 권한 부여를 만들 UM 사서함 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지 \> **전화 걸기 권한 부여**에서**권한 있는 국제 전화 걸기 규칙 그룹** 아래에 있는 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **허용할 전화 걸기 규칙 그룹 선택** 페이지에서 전화 걸기 규칙 그룹을 선택하고 **확인**, **저장**을 차례로 클릭합니다.

## 셸을 사용하여 UM 사서함 정책에서 국내 및 국제 전화 걸기 권한 부여를 사용하도록 설정

이 예에서는 이름이 `MyUMMailboxPolicy`인 UM 사서함 정책에서 InCountry/RegionGroup1, InCountry/RegionGroup2, InternationalGroup1 및 InternationalGroup2 전화 걸기 권한 부여를 사용하도록 설정합니다.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

