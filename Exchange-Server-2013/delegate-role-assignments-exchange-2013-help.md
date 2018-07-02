---
title: '대리인 역할 할당: Exchange 2013 Help'
TOCTitle: 대리인 역할 할당
ms:assetid: ed2d00d9-90c9-49dc-ab8a-cd791569aeed
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351237(v=EXCHG.150)
ms:contentKeyID: 50484480
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 대리인 역할 할당

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-02_

관리 역할 위임 역할 책임자를 다른 관리 역할 그룹, 관리 역할 할당 정책, 사용자 또는 (USG) 유니버설 보안 그룹에 지정 된 관리 역할을 할당할 수 있습니다. 기본적으로 조직 관리 관리 역할 그룹의 구성원만 역할 할당을 위임할 수 있습니다. Microsoft Exchange Server 2013 의 새 설치를 배포 하는 경우 Exchange 2013 를 설치 하는 사용자 계정이 조직 관리 역할 그룹의 구성원입니다.

역할 그룹에는 위임 역할 할당을 할당 하는 경우 역할 그룹의 모든 구성원은 관련 된 관리 역할을 다른 역할 임무 책임자에 게 위임할 수 있습니다.


> [!IMPORTANT]
> 위임 역할 할당 하지 역할 담당자 사용 권한 부여 부여 된 다른 사용자에 게 역할을 할당 하는 기능에만 역할별 합니다. 또한 역할 담당자에 게 역할에 따라 부여 된 권한을 부여 하려면 일반 역할 할당을 만들어야 합니다. 일반 역할 할당을 만들려면 다음 항목을 참조 합니다.<BR><A href="manage-role-groups-exchange-2013-help.md">역할 그룹 관리</A><BR><A href="manage-role-assignment-policies-exchange-2013-help.md">역할 할당 정책 관리</A><BR><A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">사용자 또는 USG에는 역할을 추가 합니다.</A>




> [!NOTE]
> 이 항목에서는 관리 역할 할당 위임에 설명 합니다. 위임 하려는 구성원을 추가 하거나 제거할 수 있는 경우를 위임의 권장된 메서드를 사용 하는 역할 그룹에서 구성원 <A href="manage-role-groups-exchange-2013-help.md">역할 그룹 관리</A>를 참조 합니다.



일반 역할 할당 및 관리 역할 할당을 위임 하는 방법에 대 한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)을 참조 하십시오.

사용 권한 관리와 관련 된 다른 관리 작업을 찾고 있습니까? [고급 사용 권한](advanced-permissions-exchange-2013-help.md)확인할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상이 절차를 완료 시간: 5 분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "역할 할당" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용 하 여 관리 역할 위임

같은 미리 정의 된 범위, 받는 사람 필터 또는 서버 필터 기반 범위, 서버 목록에 기반한 범위 및 일반 또는 배타적 범위를 만들를 사용할 수 있는 조직 구성 단위 (OU) 범위를 사용 하 여 위임 역할 할당을 만들 수 있습니다. 일반 역할 할당 및 위임 역할 할당 만들기에 대 한 유일한 차이점은 *Delegating* 스위치는 명령에 추가 합니다. 역할 할당을 만드는 방법에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)


> [!NOTE]
> 관리 역할 할당 정책에는 위임 역할 할당을 만들 수 없습니다.



이 예제에서는 선임 관리자 역할 그룹의 구성원이 Exchange 조직에서 모든 역할 담당자에 게는 편지 병합 받는 사람 역할을 할당할 수 있도록 하는 위임 역할 할당을 만듭니다.

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admin - Delegate" -Delegating

이 예에서는 contoso.com 도메인의 판매/사용자 OU에 대 한 사용자 에게만 편지 병합 받는 사람 역할을 할당할 선임 관리자 역할 그룹의 구성원을 사용 하도록 설정 하려면 위임 역할 할당을 만듭니다.

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admins - Delegate" -RecipientOrganizationalUnitScope contoso.com/sales/users -Delegating

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

