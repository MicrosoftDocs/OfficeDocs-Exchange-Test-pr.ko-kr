---
title: '일반 또는 배타적 범위 만들기: Exchange 2013 Help'
TOCTitle: 일반 또는 배타적 범위 만들기
ms:assetid: b97a5be3-15cc-4954-ba30-a824a95e21be
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351083(v=EXCHG.150)
ms:contentKeyID: 50483995
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 일반 또는 배타적 범위 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

관리 역할 범위에서는 개체에 할당된 cmdlet과 매개 변수를 사용하여 개체를 변경할 수 있도록 사용자가 사용할 수 있는 개체를 결정합니다. 관리 범위를 추가하면 관리 역할 할당을 구성하여 사용자가 조직의 특정 서버, 데이터베이스, 받는 사람 및 다른 개체를 관리할 수 있도록 허용하면서도 다른 개체가 변경되는 것은 제한할 수 있습니다.


> [!IMPORTANT]
> 일반 또는 단독 범위를 만들면 사용자가 할당하는 관리 역할에 정의되어 있는 쓰기 범위가 다시 정의됩니다. 관리 역할에 구성된 읽기 범위는 다시 정의할 수 없습니다.



사용자 지정 관리 범위를 만들고 관리 역할 할당을 추가 또는 변경할 수 있습니다. 미리 작성된 관리 범위 또는 OU(조직 단위) 관리 범위로 관리 역할 할당을 만들려면 [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)를 참조하십시오.

Microsoft Exchange Server 2013의 관리 역할 범위 및 할당에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

범위와 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 범위" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 사용자 지정 범위 만들기

사용자 지정 범위를 만들려면 다음의 범위 유형 중 하나를 선택합니다.

## 받는 사람 필터 범위

받는 사람 필터 기반 범위는 **New-ManagementScope** cmdlet의 *RecipientRestrictionFilter* 매개 변수를 사용하여 만듭니다. 받는 사람 필터를 만들 때는 필터링할 받는 사람 속성 외에도 필터 쿼리가 실행될 OU를 지정할 수 있습니다. 기본 OU를 지정하면 해당 역할의 쓰기 범위를 더욱 제한할 수 있습니다.

관리 범위 필터에 대한 자세한 내용은 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.

기본 OU가 있는 도메인 제한 필터 범위를 만들려면 다음 구문을 사용합니다.

    New-ManagementScope -Name <scope name> -RecipientRestrictionFilter <filter query> [-RecipientRoot <OU>]

이 예에서는 contoso.com/Sales OU 내의 모든 사서함을 포함하는 범위를 만듭니다.

    New-ManagementScope -Name "Mailboxes in Sales OU" -RecipientRestrictionFilter { RecipientType -eq 'UserMailbox' } -RecipientRoot "contoso.com/Sales OU"


> [!NOTE]
> 특정 OU 내에서만 아니라 관리 역할의 암시적 읽기 범위 전체에 필터를 적용하려면 <EM>RecipientRoot</EM> 매개 변수를 생략할 수 있습니다.



구문과 매개 변수에 대한 자세한 내용은 [New-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd335137\(v=exchg.150\))를 참조하십시오.

## 서버 필터 구성 범위

서버 필터 기반 구성 범위는 **New-ManagementScope** cmdlet의 *ServerRestrictionFilter* 매개 변수를 사용하여 만듭니다. 서버 필터를 사용하면 지정한 필터와 일치하는 서버에만 적용되는 범위를 만들 수 있습니다.

관리 범위 필터와 필터링할 수 있는 서버 속성 목록에 대한 자세한 내용은 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.

서버 필터 범위를 만들려면 다음 구문을 사용합니다.

```powershell
New-ManagementScope -Name <scope name> -ServerRestrictionFilter <filter query>
```

이 예에서는 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' AD(Active Directory) 사이트 내의 모든 서버를 포함하는 범위를 만듭니다.

    New-ManagementScope -Name "Servers in Seattle AD site" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd335137\(v=exchg.150\))를 참조하십시오.

## 서버 목록 구성 범위

서버 목록 기반 구성 범위는 **New-ManagementScope** cmdlet의 *ServerList* 매개 변수를 사용하여 만듭니다. 서버 목록 범위를 사용하면 목록에 지정한 서버에만 적용되는 범위를 만들 수 있습니다.

서버 목록 범위를 만들려면 다음 구문을 사용합니다.

```powershell
New-ManagementScope -Name <scope name> -ServerList <server 1>, <server 2...>
```

이 예에서는 MBX1, MBX3 및 MBX5에만 적용되는 범위를 만듭니다.

```powershell
New-ManagementScope -Name "Mailbox servers" -ServerList MBX1,MBX3,MBX5
```

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd335137\(v=exchg.150\))를 참조하십시오.

## 데이터베이스 필터 구성 범위

데이터베이스 필터 기반 구성 범위는 **New-ManagementScope** cmdlet의 *DatabaseRestrictionFilter* 매개 변수를 사용하여 만듭니다. 데이터베이스 필터를 사용하면 지정한 필터와 일치하는 데이터베이스에만 적용되는 범위를 만들 수 있습니다.


> [!IMPORTANT]
> 데이터베이스 범위와 관련 된 역할 할당 Microsoft Exchange Server 2010 서비스 팩 1 (SP1)을 실행 하는 서버에 연결 하는 사용자 에게만 적용 됩니다 이상 또는 Exchange 2013 합니다. 데이터베이스 범위와 관련 된 역할 할당을 할당 된 사용자가 사전Exchange 2010 SP1 서버에 연결 하는 경우에 역할 할당 사용자에 게 적용 되지 않습니다 및 사용자 역할 할당에서 제공 하는 모든 권한을 부여 되지 않습니다.



관리 범위 필터와 필터링할 수 있는 데이터베이스 속성 목록에 대한 자세한 내용은 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.

데이터베이스 제한 필터를 만들려면 다음 구문을 사용합니다.

```powershell
New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>
```

이 예에서는 데이터베이스의 **Name** 속성에 "경영진"이라는 문자열이 있는 모든 데이터베이스를 포함하는 범위를 만듭니다.

    New-ManagementScope -Name "Executive Databases" -DatabaseRestrictionFilter { Name -Like '*Executive*' }

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd335137\(v=exchg.150\))를 참조하십시오.

## 데이터베이스 목록 구성 범위

데이터베이스 목록 기반 구성 범위는 **New-ManagementScope** cmdlet의 *DatabaseList* 매개 변수를 사용하여 만듭니다. 데이터베이스 목록 범위를 사용하면 목록에 지정한 데이터베이스에만 적용되는 범위를 만들 수 있습니다.


> [!IMPORTANT]
> 데이터베이스 범위와 관련 된 역할 할당 Microsoft Exchange Server 2010 서비스 팩 1 (SP1)을 실행 하는 서버에 연결 하는 사용자 에게만 적용 됩니다 이상 또는 Exchange 2013 합니다. 데이터베이스 범위와 관련 된 역할 할당을 할당 된 사용자가 사전Exchange 2010 SP1 서버에 연결 하는 경우에 역할 할당 사용자에 게 적용 되지 않습니다 및 사용자 역할 할당에서 제공 하는 모든 권한을 부여 되지 않습니다.



데이터베이스 목록 범위를 만들려면 다음 구문을 사용합니다.

```powershell
New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>
```

이 예에서는 데이터베이스 Database 1, Database 2 및 Database 3에만 적용되는 범위를 만듭니다.

```powershell
New-ManagementScope -Name "Primary databases" -DatabaseList "Database 1", "Database 2", "Database 3"
```

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd335137\(v=exchg.150\))를 참조하십시오.

## 단독 범위

**New-ManagementScope** cmdlet으로 만드는 모든 범위는 단독 범위로 지정할 수 있습니다. 단독 범위를 만들려면 이전 섹션 중 하나에 나오는 것과 같은 명령을 사용하여 받는 사람 필터 기반 범위, 서버 필터 기반 범위, 서버 목록 기반 범위, 데이터베이스 필터 기반 범위 또는 데이터베이스 목록 기반 범위를 만든 다음 명령에 *Exclusive* 스위치를 추가하면 됩니다.


> [!WARNING]
> 단독 관리 범위를 만들면 수정할 개체가 포함된 단독 범위가 할당된 역할 담당자만 이러한 개체에 액세스할 수 있습니다. 즉, 단독 범위가 있는 역할이 할당된 관리자만 이러한 단독 또는 보호 개체에 액세스할 수 있습니다.



이 예에서는 Executives 부서에 있는 모든 사용자와 일치하는 단독 받는 사람 필터 기반 범위를 만듭니다.

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive

기본적으로 단독 범위가 생성되면 사용자가 단독 범위를 만들었으며 단독이 아닌 기존 역할 할당에 대한 단독 범위의 영향을 인식하고 있음을 확인해야 합니다. 경고를 표시하지 않으려면 *Force* 스위치를 사용할 수 있습니다. 이 예에서는 앞의 예와 같은 범위를 만들지만 경고를 표시하지 않습니다.

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive -Force

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd335137\(v=exchg.150\))를 참조하십시오.

## 2단계: 관리 역할 할당 추가 또는 변경

범위를 만든 후에는 이를 새로운 또는 기존 관리 역할 할당에 추가해야 합니다.

관리 범위를 만들고 이를 만들려는 새 관리 역할 할당에 추가하려는 경우 다음 항목을 참조하십시오.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

관리 역할 범위를 만들고 이를 기존 관리 역할 할당에 추가하려는 경우 다음 항목을 참조하십시오.

  - [역할 할당 정책 관리](manage-role-assignment-policies-exchange-2013-help.md)

  - [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md)

