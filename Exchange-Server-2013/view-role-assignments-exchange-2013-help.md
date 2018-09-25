---
title: '역할 할당을 보기: Exchange 2013 Help'
TOCTitle: 역할 할당을 보기
ms:assetid: 0be4def9-af6d-476a-9c97-7155ae11b587
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335086(v=EXCHG.150)
ms:contentKeyID: 50482452
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 할당을 보기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

관리 역할 할당에서는 역할 담당자에 관리 역할을 할당합니다. Microsoft Exchange Server 2013의 관리 역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참조하십시오.

역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "역할 할당" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목에서는 파이프라이닝과 **Format-List** cmdlet을 사용합니다. 이 개념에 대한 자세한 내용은 다음 항목을 참조하십시오.
    
      - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))
    
      - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 모든 역할 할당 목록 보기

**Get-ManagementRoleAssignment** cmdlet을 실행하여 조직에 구성된 모든 역할 할당 목록을 볼 수 있습니다. 지정한 부분 문자열과 일치하는 역할 할당 목록을 검색하려면 와일드카드 문자(\*)를 사용합니다. 이 예에서는 "Tier 1" 문자열로 시작하는 모든 역할 할당 목록을 검색합니다.

```powershell
Get-ManagementRoleAssignment "Tier 1*"
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 특정 역할 할당의 세부 정보 보기

**Get-ManagementRoleAssignment** cmdlet의 결과를 **Format-List** cmdlet으로 파이프하여 역할 할당의 세부 정보를 볼 수 있습니다. 다음 구문을 사용합니다.

```powershell
Get-ManagementRoleAssignment <assignment name> | Format-List
```

이 예에서는 Help Desk Assignment 역할 할당의 세부 정보를 검색합니다.

```powershell
Get-ManagementRoleAssignment "Help Desk Assignment" | Format-List
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 특정 역할 담당자에 할당된 역할 할당 목록 보기

관리 역할 그룹, 역할 또는 역할 할당 정책이나 사용자 또는 USG(유니버설 보안 그룹)에 연결된 역할 할당 목록을 보려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRoleAssignment -RoleAssignee <role assignee name>
```

이 예에서는 Server Management 역할 그룹에 연결된 역할 할당을 모두 검색합니다.

```powershell
Get-ManagementRoleAssignment -RoleAssignee "Server Management"
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 특정 역할에 연결된 역할 할당 보기

각 역할에 여러 역할 할당이 있을 수 있습니다. **Get-ManagementRoleAssigment** cmdlet을 사용하여 특정 역할에 연결된 역할 할당 목록을 볼 수 있습니다.

지정한 역할에 연결된 역할 할당 목록을 보려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRoleAssignment -Role <role name>
```

이 예에서는 Mail Recipients 역할에 연결된 역할 할당을 모두 검색합니다.

```powershell
Get-ManagementRoleAssignment -Role "Mail Recipients"
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 미리 정의된 특정 범위를 사용하는 역할 할당 목록 보기

미리 정의된 특정 범위를 사용하는 역할 할당 목록을 보려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRoleAssignment -RecipientWriteScope < MyGAL | MyDistributionGroups | Organization | Self | CustomRecipientScope | ExecutiveRecipientScope >
```

이 예에서는 미리 정의된 Organization 범위를 사용하는 역할 할당을 모두 검색합니다.

```powershell
Get-ManagementRoleAssignment -RecipientWriteScope Organization
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 범위가 특정 OU로 지정된 역할 할당 목록 보기

범위가 특정 OU(조직 구성 단위)로 지정된 역할 할당 목록을 보려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope <OU>
```

이 예에서는 범위가 contoso.com 도메인의 North America\\Engineering\\Users OU로 지정된 역할 할당을 모두 검색합니다.

```powershell
Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope "contoso.com/North America/Engineering/Users"
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 특정 사용자 지정 범위를 사용하는 할당 목록 보기

특정 사용자 지정 범위를 사용하는 역할 할당 목록을 보려면 먼저 범위가 받는 사람 범위, 구성 범위, 배타적 받는 사람 범위 또는 배타적 구성 범위인지를 확인해야 합니다. 각 범위 유형은 **Get-ManagementRoleAssignment** cmdlet의 다른 매개 변수를 사용합니다. 다음 목록에서는 각 범위 및 범위에 연결된 매개 변수를 보여 줍니다.

  - **받는 사람 범위**   *CustomRecipientWriteScope*

  - **구성 범위**   *CustomConfigWriteScope*

  - **배타적 받는 사람 범위**   *ExclusiveRecipientWriteScope*

  - **배타적 구성 범위**   *ExclusiveConfigWriteScope*

각 매개 변수에 대한 구문은 같습니다. 범위 유형과 일치하는 매개 변수를 사용하여 범위 이름을 지정합니다.

이 예에서는 Vancouver Recipients 받는 사람 범위를 사용하는 역할 할당을 모두 검색합니다.

```powershell
Get-ManagementRoleAssignment -CustomRecipientWriteScope "Vancouver Recipients"
```

이 예에서는 Seattle AD Site 배타적 구성 범위를 사용하는 역할 할당을 모두 검색합니다.

```powershell
Get-ManagementRoleAssignment -ExclusiveConfigWriteScope "Seattle AD Site"
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 배타적 범위 또는 일반 범위 목록 보기

배타적 또는 일반 역할 할당 목록을 보려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRoleAssignment -Exclusive < $True | $False >
```

예를 들어 배타적 범위 목록을 보려면 다음 명령을 실행합니다.

```powershell
Get-ManagementRoleAssignment -Exclusive $True
```

이 예에서는 배타적 범위 없이 일반 범위 목록을 검색합니다.

```powershell
Get-ManagementRoleAssignment -Exclusive $False
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 특정 받는 사람 또는 서버를 수정할 수 있는 사람 보기

특정 받는 사람 또는 서버를 수정할 수 있는 역할 할당 목록을 보려면 *WritableRecipient* 및 *WritableServer* 매개 변수를 사용합니다. *WritableRecipient* 매개 변수를 사용하여 받는 사람 이름을 지정하고 *WritableServer* 매개 변수를 사용하여 서버 이름을 지정합니다.

이 예에서는 받는 사람 Brian을 수정할 수 있는 역할 할당 목록을 검색합니다.

```powershell
Get-ManagementRoleAssignment -WritableRecipient "Brian"
```

*WritableRecipient* 및 *WritableServer* 매개 변수를 *RoleAssignee* 매개 변수, *GetEffectiveUsers* 스위치 등의 다른 매개 변수와 함께 사용하여 쿼리를 구체화하고 역할 그룹이나 USG를 확장할 수 있습니다. 이 예에서는 EX02 서버를 수정할 수 있고 Server Management 역할 그룹이 할당된 사용자를 모두 검색합니다.

```powershell
Get-ManagementRoleAssignment -WritableServer EX02 -RoleAssignee "Server Management" -GetEffectiveUsers
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 역할 그룹 또는 USG를 통해 할당에서 사용 권한을 받는 사용자 보기

역할 할당에서 사용 권한을 받는 사용자 목록을 보려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRoleAssignment <assignment name> -GetEffectiveUsers
```

이 예에서는 Help Desk Assignment 역할 할당의 사용자 목록을 검색합니다.

```powershell
Get-ManagementRoleAssignment "Help Desk Assignment" -GetEffectiveUsers
```

**Get-ManagementRoleAssignment** cmdlet에 *GetEffectiveUsers* 스위치와 여러 다른 매개 변수를 함께 사용하여 역할 할당이 할당된 역할 그룹과 USG를 확장할 수도 있습니다. *GetEffectiveUsers* 스위치를 다른 매개 변수와 함께 사용하는 방법의 예는 이 항목의 앞부분에 있는 "특정 받는 사람 또는 서버를 수정할 수 있는 사람 보기"를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 사용하거나 사용하지 않도록 설정된 역할 할당 목록 보기

사용하거나 사용하지 않도록 설정된 역할 할당 목록을 보려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRoleAssignment -Enabled < $True | $False >
```

이 예에서는 사용하지 않도록 설정된 역할 할당 목록을 검색합니다.

```powershell
Get-ManagementRoleAssignment -Enabled $False
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

