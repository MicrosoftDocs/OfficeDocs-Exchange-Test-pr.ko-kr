---
title: '전체 주소 목록 만들기: Exchange 2013 Help'
TOCTitle: 전체 주소 목록 만들기
ms:assetid: 59e4955a-8999-4d17-be9f-23a41a23b929
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232063(v=EXCHG.150)
ms:contentKeyID: 50483180
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전체 주소 목록 만들기

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-12-16_

GAL(전체 주소 목록)은 조직에서 구현된 MicrosoftExchange 내의 모든 그룹, 사용자 및 연락처에 대한 항목이 포함된 디렉터리입니다. 조직에서 주소록 정책을 사용하는 경우 추가 GAL을 만들 수 있습니다. 자세한 내용은 [주소록 정책](address-book-policies-exchange-2013-help.md)를 참조하십시오.

주소 목록과 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 목록 절차](address-list-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "주소 목록" 항목

  - Exchange Online에서는 기본적으로 주소 목록 역할이 어떤 역할 그룹에도 할당되지 않습니다. 주소 목록 역할이 필요한 cmdlet을 사용하려면 역할 그룹에 이 역할을 추가해야 합니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 항목의 "역할 그룹에 역할 추가" 섹션을 참조하세요.

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 조건부 필터 속성을 사용하는 GAL 만들기

이 예에서는 사서함 사용자이고 회사가 Contoso로 표시되는 받는 사람이 포함된 GAL\_Contoso라는 GAL을 만듭니다.

    New-GlobalAddressList -Name "GAL_Contoso" -IncludedRecipients MailboxUsers -ConditionalCompany Contoso


> [!NOTE]
> 미리 만든 조건부 필터 속성을 사용할 경우에는 <EM>IncludedRecipients</EM> 매개 변수를 비워 둘 수 없습니다.



구문과 매개 변수에 대한 자세한 내용은 [New-GlobalAddressList](https://technet.microsoft.com/ko-kr/library/bb123785\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 받는 사람 필터를 사용하는 GAL 만들기

이 예에서는 *CustomAttribute15* 매개 변수에 `AgencyA` 값이 있는 받는 사람이 포함된 GAL\_AgencyA라는 GAL을 만듭니다.

    New-GlobalAddressList -Name "GAL_AgencyA" -RecipientFilter {CustomAttribute15 -like "AgencyA"}

구문과 매개 변수에 대한 자세한 내용은 [New-GlobalAddressList](https://technet.microsoft.com/ko-kr/library/bb123785\(v=exchg.150\))를 참조하십시오.

