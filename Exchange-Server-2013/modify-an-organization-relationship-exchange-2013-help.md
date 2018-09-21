---
title: '조직 관계 수정: Exchange 2013 Help'
TOCTitle: 조직 관계 수정
ms:assetid: 3713ef83-f01a-41bb-b127-62ca242dd7a4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673055(v=EXCHG.150)
ms:contentKeyID: 50482849
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 조직 관계 수정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-01_

조직 관계는 Exchange 조직의 사용자가 일정 약속 있음/없음 정보를 Office 365 조직 또는 다른 Exchange 온-프레미스 조직과 공유할 수 있도록 하는 기능입니다. 이름을 변경하거나, 일정 공유를 일시적으로 사용하지 않도록 설정하거나, 액세스 수준을 변경하거나, 일정을 공유할 보안 그룹을 변경하는 등 조직 관계의 설정을 변경할 수 있습니다.

다른 조직과 일정을 공유하려면 클라우드와의 인증 관계("페더레이션"이라고도 함)를 설정해야 하며 최소 소프트웨어 요구 사항을 충족해야 합니다. 페더레이션 공유에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md)를 참조하십시오.

페더레이션과 관련된 추가 관리 작업에 대한 자세한 내용은 [페더레이션 프로시저](federation-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 *Calendar and Sharing Permissions* 항목을 참조하십시오.

  - 온-프레미스 Exchange 조직에 대한 활성 페더레이션 트러스트를 구성해야 합니다.

  - 조직 관계에서 구성 하려는 외부 조직은 Azure AD 인증 시스템을 통해 설정 된 페더레이션 트러스트를 권한도 부여 받아야 합니다.

  - 이 항목의 절차에서는 Contoso 조직 관계를 변경합니다. 이 예에서는 다음 작업을 수행하는 방법을 설명합니다.
    
      - 외부 조직에 service.contoso.com 도메인 추가
    
      - 조직 관계에 대해 약속 있음/없음 정보 공유를 사용하지 않도록 설정
    
      - 약속 있음/없음 정보 액세스 수준을 *Calendar free/busy information with time, subject, and location*에서 *Calendar free/busy information with time only*로 변경

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 조직 관계에 도메인 추가

1.  온-프레미스 조직의 Exchange 2013 서버에서 **조직** \> **공유**로 이동합니다.

2.  목록 보기의 **조직 공유**에서 조직 관계 Contoso를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **조직 관계** \> **일반**에서 조직 관계의 **이름**은 변경하지 않습니다.

4.  **공유할 도메인** 상자에 **service.contoso.com** 도메인을 입력하고 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

5.  **저장**을 클릭하여 조직 관계를 업데이트합니다.

## EAC를 사용하여 조직 관계에 대한 약속 있음/없음 공유를 사용하지 않도록 설정

1.  **조직** \> **공유**로 이동합니다.

2.  목록 보기의 **조직 공유**에서 조직 관계 Contoso를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **조직 관계**에서 **공유**를 클릭합니다.

4.  **시간만 있는 약속 있음/없음 일정 정보**를 선택합니다.

5.  **저장**을 클릭하여 조직 관계를 업데이트합니다.

## EAC를 사용하여 조직 관계에 대한 약속 있음/없음 액세스 수준 변경

1.  **조직** \> **공유**로 이동합니다.

2.  목록 보기의 **조직 공유**에서 조직 관계 Contoso를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **조직 관계**에서 **공유**를 클릭합니다.

4.  **시간만 있는 약속 있음/없음 일정 정보**를 선택합니다.

5.  **저장**을 클릭하여 조직 관계를 업데이트합니다.

## 셸을 사용하여 조직 관계 수정

  - 이 예에서는 Contoso 조직 관계에 도메인 이름 service.contoso.com을 추가합니다.
    
        $domains = (Get-OrganizationRelationship Contoso).DomainNames
        $domains += 'service.contoso.com'
        Set-OrganizationRelationship -Identity Contoso -DomainNames $domains

  - 이 예에서는 조직 관계 Contoso를 사용하지 않도록 설정합니다.
    
    ```powershell
Set-OrganizationRelationship -Identity Contoso -Enabled $false
```

  - 이 예에서는 조직 관계 WoodgroveBank에 대해 일정 약속 있음/없음 정보 액세스를 허용하고 액세스 수준을 `AvailabilityOnly`(약속 있음/없음 일정 정보(시간만))로 설정합니다.
    
        Set-OrganizationRelationship -Identity Contoso -FreeBusyAccessEnabled $true -FreeBusyAccessLevel AvailabilityOnly

구문과 매개 변수에 대한 자세한 내용은 [Get-OrganizationRelationship](https://technet.microsoft.com/ko-kr/library/ee332343\(v=exchg.150\)) 및 [Set-OrganizationRelationship](https://technet.microsoft.com/ko-kr/library/ee332326\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

조직 관계가 성공적으로 업데이트되었는지 확인하려면 다음 셸 명령을 실행하여 조직 관계 정보를 확인합니다.

```powershell
Get-OrganizationRelationship | format-list
```


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


