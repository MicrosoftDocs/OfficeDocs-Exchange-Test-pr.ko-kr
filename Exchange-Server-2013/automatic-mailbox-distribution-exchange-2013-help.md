---
title: '자동 사서함 배포: Exchange 2013 Help'
TOCTitle: 자동 사서함 배포
ms:assetid: f4db4636-948c-466b-839c-300c1a3a9544
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff477621(v=EXCHG.150)
ms:contentKeyID: 59635553
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 자동 사서함 배포

 

_**적용 대상:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**마지막으로 수정된 항목:**2013-08-13_

사서함을 만들거나 이동할 때 또는 기존 사용자가 메일을 사용할 수 있도록 설정할 때 해당 사서함을 사서함 데이터베이스에 저장해야 합니다. Microsoft Exchange Server 2013에서는 Exchange가 자동 사서함 배포를 사용하여 데이터베이스를 선택하게 하는 옵션을 제공합니다.

자동 사서함 배포를 사용하여 Exchange는 조직의 사서함 데이터베이스를 보고 나중에 이 항목에서 설명되는 기준을 사용하여 적합하지 않은 데이터베이스를 제외한 후 사서함이 있어야 할 데이터베이스를 임의로 선택합니다. 이 프로세스는 사용자 조직에서 적합한 모든 사서함 데이터베이스에 사서함을 임의로 배포합니다.

**New-Mailbox** 및 **Enable-Mailbox** cmdlet에서 *Database* 매개 변수를 지정하지 않거나 **New-MoveRequest** cmdlet에서 *TargetDatabase* 매개 변수를 지정하지 않은 경우 자동 배포가 사용됩니다.


> [!NOTE]
> 사서함이 Exchange 2013 서버에 생성되어 Exchange 2013 서버로 이동되거나 사용자가 메일 사용이 가능할 때만 자동 사서함 배포가 수행됩니다. <STRONG>New-Mailbox</STRONG>, <STRONG>New-MoveRequest</STRONG> 및 <STRONG>Enable-Mailbox</STRONG> cmdlet은 Exchange 2013을 실행하는 서버에서 실행해야 합니다. Exchange는 서버 부하를 기반으로 자동으로 데이터베이스 간에 로드를 분산하기 위해 사서함을 재배포하지 않습니다.



다음 프로세스는 새로운 사서함이나 이동한 사서함이 있어야 하는 적합한 사서함 데이터베이스를 찾는 데 사용됩니다.

1.  Exchange는 Exchange 2013 조직의 모든 사서함 데이터베이스 목록을 검색합니다.

2.  배포 프로세스에서 제외하는 것으로 표시된 사서함 데이터베이스는 사용 가능한 데이터베이스 목록에서 제거됩니다. 사용자는 어떤 데이터베이스를 제외할 것인지 제어할 수 있습니다. 자세한 내용은 이 항목 뒷부분의 Exclude Databases from Automatic Distribution를 참조하십시오.

3.  작업을 수행하는 관리자에게 적용된 데이터베이스 관리 범위 밖에 있는 모든 사서함 데이터베이스는 사용 가능한 데이터베이스 목록에서 제거됩니다. 자세한 내용은 이 항목 뒷부분의 Database Scopes를 참조하십시오.

4.  작업이 수행 중인 로컬 Active Directory 사이트 밖에 있는 모든 사서함 데이터베이스는 사용 가능한 데이터베이스 목록에서 제거됩니다.

5.  사서함 데이터베이스의 나머지 목록에서 Exchange는 데이터베이스를 임의로 선택합니다. 데이터베이스가 온라인이고 양호한 경우 Exchange에서 데이터베이스를 사용합니다. 오프라인 또는 양호하지 않은 경우에는 다른 데이터베이스에서 임의로 선택됩니다. 온라인이거나 양호한 데이터베이스가 없으면 오류로 인해 작업이 실패합니다.

사서함 데이터베이스 선택 프로세스는 Mailbox Resources Management Agent cmdlet 확장 에이전트에서 수행합니다. `Mailbox Resources Management Agent`는 실행 중인 cmdlet의 기능을 확장하는 몇몇 cmdlet 확장 에이전트 중 하나입니다. cmdlet 확장 에이전트에 대한 자세한 내용은 [cmdlet 확장 에이전트](cmdlet-extension-agents-exchange-2013-help.md)를 참조하세요.

사서함을 자동으로 배포하지 않으려면 `Mailbox Resources Management Agent`를 사용하지 않도록 설정할 수 있습니다. 에이전트를 사용하지 않도록 설정한 경우 해당 변경 내용은 전체 Exchange 조직에 적용됩니다. cmdlet 확장 에이전트를 사용하지 않도록 설정하는 방법에 대한 자세한 내용은 [Cmdlet 확장 에이전트를 관리 합니다.](manage-cmdlet-extension-agents-exchange-2013-help.md)를 참조하세요.

## 자동 배포에서 데이터베이스 제외

기본적으로 로컬 Exchange 2013 사이트의 Active Directory 서버에 있는 온라인 및 정상 상태의 모든 사서함 데이터베이스를 자동 사서함 배포에서 선택하여 새 사서함 또는 이동된 사서함을 저장할 수 있습니다. 그러나 여러 이유로 배포 프로세스에서 일부 데이터베이스를 제외할 수 있습니다. 예를 들어 사서함 데이터베이스를 저널링 데이터베이스로 지정할 수 있으며 저널링 데이터베이스에는 수동으로 지정한 사서함만이 있어야 합니다. 또는 교대에서 데이터베이스를 일시적으로 제거하여 예약된 유지 관리를 수행할 수 있습니다. Exchange 2013에서는 **Set-MailboxDatabase** cmdlet을 사용하여 설정할 수 있는 *IsExcludedFromProvisioning* 매개 변수를 사용하여 제외 프로세스에서 데이터베이스를 영구적으로 또는 일시적으로 제외하는 옵션을 제공합니다.


> [!NOTE]
> 다른 두 매개 변수 <EM>IsSuspendedFromProvisioning</EM>과 <EM>IsExcludedFromInitialProvisioning</EM>은 <STRONG>Set-MailboxDatabase</STRONG> cmdlet에서도 사용할 수 있습니다. 이러한 매개 변수는 Exchange의 향후 릴리스에서 제거될 예정이며, 해당 매개 변수의 사용은 지원되지 않습니다.



*IsExcludedFromProvisioning* 매개 변수의 유효한 두 값은 `$True` 및 `$False`입니다. 이 속성을 `$True`로 설정하면 사서함 데이터베이스가 자동 배포 프로세스에서 제외됩니다. 이 속성을 `$False`로 설정하면 사서함 데이터베이스가 자동 배포 프로세스에 포함됩니다. 기본값은 `$False`입니다.

자동 배포에서 사서함 데이터베이스를 제외하려면 다음 명령을 사용합니다.

    Set-MailboxDatabase <database name> -IsExcludedFromProvisioning $True

사서함 데이터베이스가 자동 배포에서 제외된 경우, 데이터베이스에 사서함을 만들거나 데이터베이스로 사서함을 이동하는 유일한 방법은 **New-Mailbox** 및 **Enable-Mailbox** cmdlet에서 *Database* 매개 변수를 사용하거나 **New-MoveRequest** cmdlet에서 *TargetDatabase* 매개 변수를 사용하는 것입니다.

## 데이터베이스 범위

데이터베이스 관리 범위는 Exchange 2013에서 사용 가능한 자동 사서함 배포 프로세스에 대한 추가 제어 수준입니다. 사서함 데이터베이스가 온라인 및 정상 상태이며 로컬 Active Directory 사이트에 있으면서 자동 배포 프로세스에서 제외되지 않은 경우, Exchange 2013은 사서함 데이터베이스가 cmdlet을 실행하는 관리자에 적용된 데이터베이스 범위에 포함되어 있는지를 확인합니다. 데이터베이스 범위에 포함된 경우 해당 관리자가 사용할 수 있는 데이터베이스 목록에 포함됩니다.

데이터베이스 범위는 RBAC(역할 기반 액세스 제어) 권한 모델에 속합니다. RBAC 및 데이터베이스 범위에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

자동 배포에 사용할 수 있는 여러 사서함 데이터베이스가 로컬 Active Directory 사이트에 있지만 특정 관리자 집합이 사용할 수 있는 데이터베이스를 제한하려는 경우 데이터베이스 범위가 유용할 수 있습니다. Exchange 2013 서버가 몇몇 기관에 제공되지만 각 기관에서 사서함을 할당한 사서함 데이터베이스에 사서함을 만들거나 해당 사서함 데이터베이스로 사서함을 이동하려는 경우를 예로 들 수 있습니다.

기본적으로 Exchange 2013 조직의 모든 관리자는 해당 조직의 사서함 데이터베이스를 모두 볼 수 있습니다. 관리자가 볼 수 있는 데이터베이스를 제한하여 잠재적으로 사서함을 만들거나 사서함을 이동할 수 있는 데이터베이스를 제한하려면 다음을 수행해야 합니다.

1.  관리자가 사용할 사서함 데이터베이스만이 포함된 **New-ManagementScope** cmdlet을 사용하여 사용자 지정 데이터베이스 관리 범위를 만듭니다.

2.  다음 방법 중 하나로 새 데이터베이스 범위를 관리 역할 할당에 연결합니다.
    
      - **Set-ManagementRoleAssignment** cmdlet에서 *CustomConfigWriteScope* 매개 변수를 사용하여 새 데이터베이스 범위를 기존 관리 역할 할당에 추가합니다. 이제 데이터베이스 범위는 관리 역할 그룹, USG(유니버설 보안 그룹) 또는 사용자가 할당한 역할 할당에 적용됩니다.
    
      - **New-ManagementRoleAssignment** cmdlet을 사용하여 관리 역할 할당을 만들고 *CustomConfigWriteScope* 매개 변수를 사용하여 새 데이터베이스 범위를 지정합니다. 관리 역할과 역할 그룹, USG 또는 사용자 간의 역할 할당을 만들 수 있습니다.

3.  역할 그룹이나 USG에 역할 할당을 만든 경우 역할 할당과 데이터베이스 범위가 해당 사용자에게 적용되도록 사용자를 역할 그룹이나 USG에 추가합니다.

4.  해당하는 경우 액세스하지 않으려는 데이터베이스를 포함한 데이터베이스 범위를 할당할 수 있는 USG 또는 기타 역할 그룹에서 새 역할 할당을 할당한 사용자(또는 이전 단계에서 만든 USG 또는 역할 그룹의 구성원인 사용자)를 제거합니다.

5.  액세스해야 하는 데이터베이스에 대해서만 액세스 권한이 관리자에게 있는지 확인합니다.

이러한 단계를 완료하면 생성한 데이터베이스 범위가 있는 역할 할당을 할당한 관리자만이 지정한 데이터베이스에 사서함을 만들거나 지정한 데이터베이스로 사서함을 이동할 수 있습니다.

데이터베이스 범위를 사용하여 관리자가 사용할 수 있는 사서함 데이터베이스를 제한하는 방법에 대한 자세한 내용은 [데이터베이스 범위를 사용 하 여 자동 사서함 배포 제어](control-automatic-mailbox-distribution-using-database-scopes-exchange-2013-help.md)를 참조하십시오.

