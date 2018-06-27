---
title: '조직 관계 만들기: Exchange 2013 Help'
TOCTitle: 조직 관계 만들기
ms:assetid: 5ea61b96-c8ca-44fc-b8b5-ca4341af36a6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657451(v=EXCHG.150)
ms:contentKeyID: 50483228
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 조직 관계 만들기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-07_

외부 비즈니스 파트너와 일정 정보를 공유 하는 조직 관계를 설정 합니다. 두 페더레이션된 Exchange 2013 조직 간에 또는 페더레이션된 Exchange 2013 조직 및 페더레이션된 Exchange 2010 조직 간에 조직 관계를 구성할 수 있습니다. 온-프레미스 Exchange 조직과 Office 365 조직 간에 조직 관계를 설정할 수도 있습니다.


> [!IMPORTANT]
> 조직 관계를 만드는 작업은 Exchange 조직에 페더레이션된 공유를 설정하기 위한 여러 개의 단계 중 하나로서 온-프레미스 Exchange 조직에 대해 페더레이션 트러스트를 구성하는 작업을 수행해야 합니다.



페더레이션 공유에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "일정 및 공유 권한? [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 섹션입니다.

  - 온-프레미스 Exchange 조직에 대한 활성 페더레이션 트러스트를 구성해야 합니다. 자세한 내용은 [페더레이션 트러스트를 구성 합니다.](configure-a-federation-trust-exchange-2013-help.md) 항목을 참조하십시오.

  - 조직 관계에서 구성 하려는 외부 조직은 Azure AD 인증 시스템을 통해 설정 된 페더레이션 트러스트를 권한도 부여 받아야 합니다. 조직 관계를 구성 하는 경우 외부 Exchange 조직에 대 한 기본 페더레이션된 도메인을 사용 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 조직 관계 만들기

1.  온-프레미스 조직의 Exchange 2013 서버에서 **조직** \> **공유**로 이동합니다.

2.  **조직 공유**에서 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

3.  **새 조직 관계**의 **관계 이름** 상자에 조직 관계의 이름을 입력합니다.

4.  **공유할 도메인** 상자에 일정을 보도록 허용할 Office 365 또는 Exchange 온-프레미스 조직의 페더레이션 도메인 또는 페더레이션 하위 도메인을 입력합니다. 외부 조직에 대해 여러 도메인을 입력해야 하는 경우 각 도메인을 쉼표로 구분합니다. 구분하십시오(예: **contoso.com, service.contoso.com**).

5.  **약속 있음/없음 일정 정보 공유 사용** 확인란을 선택하여 목록에 포함한 도메인에 대해 일정 공유를 설정합니다. 약속 있음/없음 일정 정보의 공유 수준과 약속 있음/없음 일정 정보를 공유할 수 있는 사용자를 설정합니다.
    
    약속 있음/없음 액세스 수준을 설정하려면 다음 중 하나를 선택합니다.
    
      - **약속 있음/없음 일정 정보(시간만 포함)**
    
      - **약속 있음/없음 일정 정보(시간, 제목 및 위치 포함)**
    
    약속 있음/없음 일정 정보를 공유할 사용자를 설정하려면 다음 중 하나를 선택합니다.
    
      - **조직의 모든 사람**
    
      - **지정된 보안 그룹**
        
        보안 그룹을 지정하려면 **찾아보기**를 클릭합니다.

6.  **저장**을 클릭하여 조직 관계를 만듭니다.

## 셸을 사용하여 조직 관계 만들기

이 예에서는 다음 조건을 사용하여 Contoso, Ltd와의 조직 관계를 만듭니다.

  - 조직 관계는 contoso.com, northamerica.contoso.com 및 europe.contoso.com에 대해 사용할 수 있습니다.

  - 약속 있음/없음 액세스를 사용할 수 있습니다.

  - 요청하는 조직은 대상 조직으로부터 약속 있음/없음 시간, 주제 및 위치 정보를 받습니다.

<!-- end list -->

    New-OrganizationRelationship -Name "Contoso" -DomainNames "contoso.com","northamerica.contoso.com","europe.contoso.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails

이 예에서는 **Get-FederationInformation** cmdlet에 제공된 도메인 이름을 사용하여 외부 Exchange 조직 Contoso.com의 구성 정보를 자동으로 검색합니다. 이 방법을 사용하여 조직 관계를 만드는 경우 먼저 **Set-FederatedOrganizationIdentifier** cmdlet을 사용하여 조직 식별자를 만들었는지 확인해야 합니다.

    Get-FederationInformation -DomainName Contoso.com | New-OrganizationRelationship -Name "Contoso" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -LimitedDetails

구문과 매개 변수에 대한 자세한 내용은 [Get-FederationInformation](https://technet.microsoft.com/ko-kr/library/dd351221\(v=exchg.150\)) 및 [New-OrganizationRelationship](https://technet.microsoft.com/ko-kr/library/ee332357\(v=exchg.150\))을 참조하십시오.

이 예에서는 Fourth Coffee와의 조직 관계를 만듭니다. 외부 Exchange 조직과의 연결 설정이 제공됩니다. 다음과 같은 조건이 적용됩니다.

  - Fourth Coffee의 페더레이션 도메인인 fourthcoffee.com 도메인과의 조직 관계가 설정됩니다.

  - Exchange 웹 서비스 응용 프로그램 URL은 mail.fourthcoffee.com입니다.

  - 자동 검색 URL은 https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity입니다.

  - 약속 있음/없음 액세스를 사용할 수 있습니다.

  - 요청하는 조직은 시간만 포함된 약속 있음/없음 정보를 받습니다.

<!-- end list -->

    New-OrganizationRelationship -Name "Fourth Coffee" -DomainNames "fourthcoffee.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -AvailabilityOnly -TargetAutodiscoverEpr "https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity" -TargetApplicationUri "mail.fourthcoffee.com"

구문과 매개 변수에 대한 자세한 내용은 [New-OrganizationRelationship](https://technet.microsoft.com/ko-kr/library/ee332357\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

**새 조직 관계** 마법사가 성공적으로 완료되면 조직 관계 만들기가 예상대로 작동한 것입니다.

조직 관계가 만들어졌는지 추가로 확인하려면 다음 셸 명령을 실행하여 조직 관계 정보를 검토합니다.

    Get-OrganizationRelationship | format-list


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


