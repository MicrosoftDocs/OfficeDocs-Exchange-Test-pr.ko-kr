---
title: '받는 사람 필터를 사용 하 여 주소 목록 만들기: Exchange 2013 Help'
TOCTitle: 받는 사람 필터를 사용 하 여 주소 목록 만들기
ms:assetid: 8eabea64-97c6-40af-b61c-9b6a125cbdf1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123718(v=EXCHG.150)
ms:contentKeyID: 50483654
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 받는 사람 필터를 사용 하 여 주소 목록 만들기

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-12-16_

이 항목에서는 받는 사람 필터를 사용하여 주소 목록을 만드는 방법에 대해 설명합니다. 주소 목록에 대한 자세한 내용은 [주소 목록](address-lists-exchange-2013-help.md)를 참조하십시오.

주소 목록과 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 목록 절차](address-list-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "주소 목록" 항목

  - Exchange Online에서는 기본적으로 주소 목록 역할이 어떤 역할 그룹에도 할당되지 않습니다. 주소 목록 역할이 필요한 cmdlet을 사용하려면 역할 그룹에 이 역할을 추가해야 합니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 항목의 "역할 그룹에 역할 추가" 섹션을 참조하세요.

  - *RecipientFilter* 매개 변수를 사용하여 사용자 지정 필터를 만들려면 필터의 문자열을 지정해야 합니다. 셸에서는 필터링 구문으로 OPATH를 사용합니다. OPATH는 개체 데이터 원본을 쿼리하기 위한 쿼리 언어입니다.

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸에서 받는 사람 필터를 사용하여 주소 목록 만들기

이 예에서는 워싱턴이나 오리건에 거주하며 Exchange 사서함이 있는 모든 사용자의 주소 목록을 만듭니다.

    New-AddressList -Name "Pacific Northwest Mailboxes" -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

이 예에서는 *CustomAttribute15* 매개 변수 값으로 `AgencyB`를 갖고 있고 Exchange 사서함이 있는 모든 사용자의 주소 목록을 만듭니다.

    New-AddressList -Name "AgencyB" -RecipientFilter {(RecipientType -eq 'UserMailbox') -and (CustomAttribute15 -like *AgencyB*)}

구문과 매개 변수에 대한 자세한 내용은 [New-AddressList](https://technet.microsoft.com/ko-kr/library/aa996912\(v=exchg.150\))를 참조하십시오.

