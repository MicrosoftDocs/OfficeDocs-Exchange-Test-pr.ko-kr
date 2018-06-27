---
title: '조직 관계에 대 한 메일 설명 관리: Exchange 2013 Help'
TOCTitle: 조직 관계에 대 한 메일 설명 관리
ms:assetid: 6e6b48ef-c41c-47ad-8063-66901765c2a5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ649324(v=EXCHG.150)
ms:contentKeyID: 50483334
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 조직 관계에 대 한 메일 설명 관리

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-08_

Exchange 관리 셸을 사용하여 여러 조직 간의 메일 설명에 대한 사용자 지정 설정을 구성할 수 있습니다.

조직 관계를 설정하면 약속 있음/없음 데이터를 공유하고, 보안 메시지 흐름을 구성하고, 메시지 추적을 사용하도록 설정하여 두 조직의 사용자 환경을 모두 개선할 수 있습니다. 조직 관계에 대한 자세한 내용은 [조직 관계를 통해 메일 설명](mailtips-over-organization-relationships-exchange-2013-help.md)를 참조하십시오.

다양한 설정을 사용하여 조직 관계를 설정한 두 조직 간에 메일 설명이 사용되는 방법을 제어할 수 있습니다. 이 섹션의 절차에서는 이러한 다양한 제어 방법을 보여 줍니다. 모든 예에서 온-프레미스 조직은 contoso.com이고, 원격 조직은 online.contoso.com이며, 조직 관계의 이름은 Contoso Online입니다.

**Set-OrganizationRelationship** cmdlet을 사용하여 이러한 설정을 구성합니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "메일 설명" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 두 조직 간에 메일 설명을 사용하거나 사용하지 않도록 설정

이 예에서는 조직의 받는 사람에게 보내는 메시지를 작성할 때 메일 설명이 원격 조직의 보낸 사람에게 반환되도록 조직 관계를 구성합니다.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $true

이 예에서는 조직의 받는 사람에게 보내는 메시지를 작성할 때 메일 설명이 원격 조직의 보낸 사람에게 반환되지 않도록 조직 관계를 구성합니다.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $false

구문과 매개 변수에 대한 자세한 내용은 [Set-OrganizationRelationship](https://technet.microsoft.com/ko-kr/library/ee332326\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 원격 조직으로 반환되는 메일 설명 구성

각 조직 관계에 대해 다른 조직의 보낸 사람에게 반환되는 메일 설명 집합을 결정할 수 있습니다. 이 예에서는 모든 메일 설명이 반환되도록 조직 관계를 구성합니다.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel All

이 예에서는 자동 회신, 대용량 메시지, 제한된 받는 사람 및 사서함 가득 참 메일 설명만 반환되도록 조직 관계를 구성합니다.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel Limited

이 예에서는 메일 설명이 반환되지 않도록 조직 관계를 구성합니다.


> [!NOTE]
> 이 관계에 대해 메일 설명을 사용하지 않도록 설정하려면 이 방법을 사용하지 마십시오. 메일 설명을 사용하지 않도록 설정하려면 <EM>MailTipsAccessEnabled</EM> 매개 변수를 <CODE>$false</CODE>로 설정합니다.



    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel None

구문과 매개 변수에 대한 자세한 내용은 [Set-OrganizationRelationship](https://technet.microsoft.com/ko-kr/library/ee332326\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 받는 사람별 메일 설명을 반환할 특정 사용자 그룹 구성

받는 사람별 메일 설명의 반환을 특정 사용자 그룹으로 제한할 수 있습니다. 기본적으로 조직 관계에 대해 메일 설명을 사용하도록 설정하면 모든 사용자에 대해 다음과 같은 받는 사람별 메일 설명이 반환됩니다.

  - 자동 회신

  - 사서함 꽉 참

  - 사용자 지정 메일 설명

조직 관계에 대한 메일 설명 액세스 그룹을 지정할 수 있습니다. 그룹을 지정하면 사서함, 메일 연락처 및 해당 그룹의 구성원인 메일 사용자에 대해서만 받는 사람별 메일 설명이 반환됩니다. 이 예에서는 ShareMailTips@contoso.com 그룹의 구성원에 대해서만 받는 사람별 메일 설명을 반환하도록 조직 관계를 구성합니다.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessScope ShareMailTips@contoso.com

구문과 매개 변수에 대한 자세한 내용은 [Set-OrganizationRelationship](https://technet.microsoft.com/ko-kr/library/ee332326\(v=exchg.150\))를 참조하십시오.

