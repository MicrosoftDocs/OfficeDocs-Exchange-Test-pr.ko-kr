---
title: '역할 범위를 변경 합니다.: Exchange 2013 Help'
TOCTitle: 역할 범위를 변경 합니다.
ms:assetid: 9180e1e0-c352-4ccd-8da6-885a2e309867
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298145(v=EXCHG.150)
ms:contentKeyID: 50483671
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 범위를 변경 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

관리 역할 범위에서는 개체에 할당된 cmdlet과 매개 변수를 사용하여 개체를 변경할 수 있도록 사용자가 사용할 수 있는 개체를 결정합니다. 범위를 변경하면 사용자가 만들거나 변경하거나 제거할 수 있는 개체를 변경할 수 있습니다.

사용자 지정 관리 범위를 변경할 수 있습니다. 배타적 범위 또는 일반 범위를 변경할 수 있습니다. 배타적 범위를 변경하면 새 범위가 즉시 적용됩니다. 미리 정의된 관리 범위 또는 OU(조직 구성 단위) 관리 범위에서 관리 역할 할당을 변경하려면 [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md)을 참조하십시오.

Microsoft Exchange Server 2013의 관리 역할 범위 및 할당에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

역할 범위와 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 범위" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 범위의 이름 변경

범위의 이름을 변경하려면 다음 구문을 사용합니다.

```powershell
Set-ManagementScope <current scope name> -Name <new scope name>
```

이 예에서는 Seattle Servers 범위를 Seattle Exchange Servers로 변경합니다.

```powershell
Set-ManagementScope "Seattle Servers" -Name "Seattle Exchange Servers"
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd297996\(v=exchg.150\))를 참조하십시오.

## 범위에서 받는 사람 필터 변경

범위에서 받는 사람 필터를 변경하려면 다음 구문을 사용합니다.

```powershell
Set-ManagementScope <scope name> -RecipientRestrictionFilter { <new recipient filter> }
```

이 예에서는 **Company** 속성이 contoso로 설정된 모든 받는 사람 개체가 일치하도록 받는 사람 필터를 변경합니다.

```powershell
Set-ManagementScope "Company Scope" -RecipientRestrictionFilter { Company -eq 'contoso' }
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd297996\(v=exchg.150\))를 참조하십시오.

받는 사람 필터에 대한 자세한 내용과 필터링 가능한 받는 사람 속성의 목록을 보려면 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.

## 범위에서 조직 구성 단위 루트 변경

범위에서 OU 루트를 변경하려면 다음 구문을 사용합니다.

```powershell
Set-ManagementScope <scope name> -RecipientRoot <OU>
```

이 예에서는 OU 루트를 contoso.com 도메인 아래의 North America/Sales Sales Users OU로 변경합니다.

```powershell
Set-ManagementScope "Sales Users" -RecipientRoot "contoso.com/North America/Sales"
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd297996\(v=exchg.150\))를 참조하십시오.

## 범위에서 서버 필터 변경

범위의 서버 필터를 변경하려면 다음 구문을 사용합니다.

```powershell
Set-ManagementScope <scope name> -ServerRestrictionFilter { <new server filter> }
```
이 예에서는 **ServerSite** 속성이 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com'으로 설정된 모든 서버 개체와 일치하도록 서버 필터를 변경합니다.

```powershell
Set-ManagementScope "Company Scope" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd297996\(v=exchg.150\))를 참조하십시오.

서버 필터에 대한 자세한 내용과 필터링 가능한 서버 속성의 목록을 보려면 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.

## 범위에서 서버 목록 변경

범위에서 서버 목록을 변경할 수는 없습니다. 서버 목록을 변경해야 하는 경우에는 다음을 수행해야 합니다.

1.  필요한 경우 [역할 범위 보기](view-role-scopes-exchange-2013-help.md) 항목의 "특정 범위 보기" 절차를 사용하여 바꿀 범위에서 현재 서버 목록을 검색합니다.

2.  [일반 또는 배타적 범위 만들기](create-a-regular-or-exclusive-scope-exchange-2013-help.md) 항목의 "1단계: 사용자 지정 범위 만들기" 절차를 사용하여 새 서버 목록으로 새 범위를 만듭니다.

3.  [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md) 항목의 "셸을 사용하여 역할 할당의 서버 필터 또는 목록 기반 범위 변경" 절차를 사용하여 이전 범위를 사용하는 모든 관리 역할 할당이 새 범위를 사용하도록 변경합니다.

4.  [역할 범위를 제거 합니다.](remove-a-role-scope-exchange-2013-help.md) 항목의 절차를 사용하여 이전 범위를 제거합니다.

## 범위에서 데이터베이스 필터 변경

범위에서 데이터베이스 필터를 변경하려면 다음 구문을 사용합니다.

```powershell
Set-ManagementScope <scope name> -DatabaseRestrictionFilter { <new database filter> }
```
이 예에서는 **Name** 속성에 "Executive" 문자열이 포함된 모든 데이터베이스 개체와 일치하도록 데이터베이스 필터를 변경합니다.

```powershell
Set-ManagementScope "Database Executive Scope" -DatabaseRestrictionFilter { Name -Like "*Executive*" }
```
구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd297996\(v=exchg.150\))를 참조하십시오.

데이터베이스 필터에 대한 자세한 내용과 필터링 가능한 데이터베이스 속성의 목록을 보려면 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.

## 범위에서 데이터베이스 목록 변경

범위에서 데이터베이스 목록을 변경할 수는 없습니다. 데이터베이스 목록을 변경해야 하는 경우에는 다음을 수행해야 합니다.

1.  필요한 경우 [역할 범위 보기](view-role-scopes-exchange-2013-help.md) 항목의 "특정 범위 보기" 절차를 사용하여 바꿀 범위에서 현재 데이터베이스 목록을 검색합니다.

2.  [일반 또는 배타적 범위 만들기](create-a-regular-or-exclusive-scope-exchange-2013-help.md) 항목의 "1단계: 사용자 지정 범위 만들기" 절차를 사용하여 새 데이터베이스 목록으로 새 범위를 만듭니다.

3.  [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md) 항목의 "셸을 사용하여 역할 할당의 데이터베이스 필터 또는 목록 기반 범위 변경" 절차를 사용하여 이전 범위를 사용하는 모든 관리 역할 할당이 새 범위를 사용하도록 변경합니다.

4.  [역할 범위를 제거 합니다.](remove-a-role-scope-exchange-2013-help.md) 항목의 절차를 사용하여 이전 범위를 제거합니다.

