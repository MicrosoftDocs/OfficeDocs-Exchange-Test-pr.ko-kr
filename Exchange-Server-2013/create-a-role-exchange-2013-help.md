---
title: '역할 만들기: Exchange 2013 Help'
TOCTitle: 역할 만들기
ms:assetid: e614ad8f-5946-4135-b130-89ea626afcd4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351214(v=EXCHG.150)
ms:contentKeyID: 50484413
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 만들기

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2012-10-17_

관리 역할을 만들 지정, 관리 역할 항목 변경, 필요에 따라 하 고 역할 담당자에 게 역할을 할당 하는 경우 범위를 추가 합니다. 이 절차를 수행 해야 거의 해야 합니다. 기본 제공 관리 역할을 관리 역할을 만드는 대신 사용할 수 있는지 여부를 확인 하는 것이 좋습니다. 기본 제공 관리 역할 목록은 [기본 제공 관리 역할](built-in-management-roles-exchange-2013-help.md)를 참조 합니다.

Microsoft Exchange Server 2013 의 관리 역할에 대 한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)을 참조 하십시오.


> [!NOTE]
> 이 항목에서는 범위가 지정 되지 않은 관리 역할을 만드는 방법에 설명 하지 않습니다. 범위가 지정 되지 않은 관리 역할을 만드는 방법에 대 한 정보를 <A href="create-an-unscoped-role-exchange-2013-help.md">범위가 지정되지 않은 역할 만들기</A>을 참조 하십시오.



역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 역할" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1 단계: 관리 역할 만들기

새 관리 역할은 기존 역할을 기반으로 합니다. 역할을 만들 때 기존 역할 및 해당 관리 역할 항목을 새 역할에 복사 됩니다. 기존 역할에는 새 하위 역할을 부모 됩니다. 항상 모든 cmdlet 및 매개 변수를 사용 하 여 필요한 포함 된 역할을 선택 하 고 하지 않을 주소를 제거 해야 합니다. 하위 역할 상위 역할에 존재 하지 않는 관리 역할 항목을 가질 수 없습니다.

다음 구문을 사용하여 새 역할을 만듭니다.

```powershell
New-ManagementRole -Parent <existing role to copy> -Name <name of new role>
```

시애틀 편지 병합 받는 사람 역할에 편지 병합 받는 사람 역할 및 해당 관리 역할 항목을 복사 하는이 예제입니다.

```powershell
New-ManagementRole -Parent "Mail Recipients" -Name "Seattle Mail Recipients"
```

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd298073\(v=exchg.150\))를 참조하십시오.

## 2 단계: 새 역할의 관리 역할 항목 변경

사용자의 역할을 만든 후에 역할의 항목을 변경 해야 합니다. 연결 된 cmdlet에 대 한 액세스를 완전히 제거 하는 전체 역할 항목을 제거할 수 있습니다. 또는 관련된 cmdlet에서 해당 특정 매개 변수에 대 한 액세스를 제거 하는 역할 항목에서 매개 변수를 제거할 수 있습니다.

상위 역할에 존재 하지 않으면 새 역할 항목 또는 매개 변수가 역할 항목에 추가할 수 없습니다. 1 단계에서에서 상위 역할에서 역할을 방금 만든 때문에 추가할 수 없습니다 모든 추가 역할 항목 또는 매개 변수 역할 항목에서 상위 역할에 없는 때문입니다.

역할에서 역할 항목을 변경할 때 다음 중 하나를 수행할 수 있습니다.

  - 한 개의 전체 역할 항목을 제거합니다.

  - 여러 개의 전체 역할 항목을 제거합니다.

  - 역할 항목에서 매개 변수를 제거합니다.

새 역할에서 역할 항목을 제거하려면 [역할에서 역할 항목을 제거 합니다.](remove-a-role-entry-from-a-role-exchange-2013-help.md)를 참조하십시오.

## 3 단계: 필요한 경우 사용자 지정 관리 역할 범위 만들기

관리 역할 범위를 보거나 변경 2 단계에서에서 구성 된 역할 항목을 사용 하 여 사용자에 게 사용할 수 있는 개체를 결정 합니다. 새 관리 역할 상속 하는 읽기 및 쓰기 관리 해당 상위 역할의 역할 범위입니다. 이러한 *암시적 범위*라고 합니다. 그러나 비즈니스 요구에 맞게 새 역할의 쓰기 범위를 변경 하는 경우도 있을 수 있습니다. 사용자 지정 범위를 만들 때 역할의 암시적 쓰기 범위를 재정의 합니다. 역할의 암시적 읽기 범위 변경 되지 않습니다. 관리 역할 범위에 대 한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)을 참조 하십시오.

사용자 지정 범위를 만들 배타적 범위 만들기 또는 미리 정의 된 범위를 사용 하 여 조직 구성 단위 (OU)에 대 한 할당의 범위 수 있습니다. 새 범위 역할의 암시적 읽기 범위 내에 있어야 합니다. 미리 정의 된 범위를 사용 하 여 또는 조직 구성 단위를 지정 하려면 4 단계로 건너뜁니다.

새 역할에 사용자 지정 범위를 추가할 [일반 또는 배타적 범위 만들기](create-a-regular-or-exclusive-scope-exchange-2013-help.md)를 참조 하십시오.

## 4 단계: 새 관리 역할 할당

역할을 만들고 구성할 때 가장 마지막 단계는 역할을 역할 담당자에게 할당하는 것입니다.

역할 할당을 만들 때에 다음 중 하나를 수행 하도록 선택할 수 있습니다.

  - 없는 범위를 가진 역할 할당을 만듭니다.

  - 미리 정의 된 범위를 가진 역할 할당을 만듭니다.

  - 도메인 제한 필터 없이 OU와 역할 할당을 만듭니다.

  - 3 단계에서에서 만든 사용자 지정 또는 배타적 범위를 가진 역할 할당을 만듭니다.
    

    > [!NOTE]
    > 역할 및 관리 역할 할당 정책을 사이 할당을 만들 때 범위를 지정할 수 없습니다.



역할 그룹, 역할 할당 정책, 사용자, 또는 유니버설 보안 그룹 (USG)에 새 역할을 할당할 수 있습니다. 자세한 내용은 다음 항목을 참조 하십시오.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [역할 할당 정책 관리](manage-role-assignment-policies-exchange-2013-help.md)

  - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

