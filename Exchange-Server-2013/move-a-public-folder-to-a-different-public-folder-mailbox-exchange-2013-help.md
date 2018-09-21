---
title: '다른 공용 폴더 사서함에 공용 폴더 이동: Exchange 2013 Help'
TOCTitle: 다른 공용 폴더 사서함에 공용 폴더 이동
ms:assetid: b8744934-a3cb-443e-acce-a9a6ca5d88f6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ906435(v=EXCHG.150)
ms:contentKeyID: 51407740
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 다른 공용 폴더 사서함에 공용 폴더 이동

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-11-16_

공용 폴더 사서함의 콘텐츠가 사서함 할당량을 초과하기 시작하면 공용 폴더를 다른 공용 폴더 사서함으로 이동해야 할 수 있습니다. 몇 가지 방법을 통해 이 작업을 수행할 수 있습니다. 하위 폴더가 없는 공용 폴더를 하나 이상 이동하려는 경우 **PublicFolderMoveRequest** cmdlet을 사용할 수 있습니다. 상위 공용 폴더와 모든 하위 폴더가 포함되는 전체 공용 폴더 분기를 이동해야 하는 경우에는 Exchange 2013을 설치하면 제공되는 `Move-PublicFolderBranch.ps1` 스크립트를 사용하면 됩니다.

공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업을 완료하기 위한 예상 시간은 공용 폴더의 크기에 따라 다릅니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md)의 "공용 폴더" 항목

  - EAC를 사용하여 이 절차를 수행할 수는 없으며, 셸을 사용해야 합니다.

  - 이동하려는 폴더에 포함된 하위 폴더는 기본적으로 이동되지 않습니다. 공용 폴더와 모든 하위 폴더를 함께 이동하려면 **Move-PublicFolderBranch.ps1** 스크립트를 사용합니다.

  - 공용 폴더를 이동하면 해당 공용 폴더의 실제 콘텐츠만 이동되며 논리적 계층 구조는 변경되지 않습니다.

  - 공용 폴더의 크기와 공용 폴더에 포함된 콘텐츠의 양에 따라 이동을 완료하려면 몇 시간이 걸릴 수 있습니다. 이 시간 동안에도 사용자는 공용 폴더에 액세스할 수 있습니다. 그러나 폴더가 "완료 중" 상태일 때는 잠시 동안 공용 폴더에 액세스할 수 없습니다.

  - 공용 폴더 이동 요청은 한 번에 하나씩만 수행할 수 있습니다. 완료된 요청을 제거하려면 **Remove-PublicFolderMoveRequest** cmdlet을 사용해야 합니다.

  - 진행 중인 공용 폴더 이동 요청의 상태를 확인하려면 [Get-PublicFolderMoveRequest](https://technet.microsoft.com/ko-kr/library/jj878076\(v=exchg.150\)) cmdlet을 사용합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 공용 폴더 하나 이동

이 예에서는 공용 폴더 \\CustomerEnagagements에 대해 공용 폴더 사서함 DeveloperReports에서 DeveloperReports01로의 이동 요청을 시작합니다.

    New-PublicFolderMoveRequest -Folders \DeveloperReports\CustomerEngagements -TargetMailbox DeveloperReports01


> [!NOTE]
> 대상 공용 폴더 사서함의 이동 요청이 활성화 된 동안 잠깁니다.



구문과 매개 변수에 대한 자세한 내용은 [New-PublicFolderMoveRequest](https://technet.microsoft.com/ko-kr/library/jj878081\(v=exchg.150\))를 참조하십시오.

## 여러 공용 폴더 이동

이 예에서는 \\Dev 공용 폴더 분기 아래 공용 폴더에 대해 대상 공용 폴더 사서함 DeveloperReports01로의 이동 요청을 시작합니다. 공용 폴더 \\Dev는 이동하지 않습니다.

    New-PublicFolderMoveRequest -Folders \Dev\CustomerEngagements,\Dev\RequestsforChange,\Dev\Usability -TargetMailbox DeveloperReports01


> [!NOTE]
> 대상 공용 폴더 사서함의 이동 요청이 활성화 된 동안 잠깁니다.



구문과 매개 변수에 대한 자세한 내용은 [New-PublicFolderMoveRequest](https://technet.microsoft.com/ko-kr/library/jj878081\(v=exchg.150\))를 참조하십시오.

## 공용 폴더 분기 이동

이 예에서는 `Move-PublicFolderBranch.ps1` 스크립트를 사용하여 공용 폴더 분기를 이동합니다. 이 스크립트는 공용 폴더 \\Dev 및 모든 하위 폴더에 대한 공용 폴더 사서함 DeveloperReports01로의 이동 요청을 시작합니다. 이 스크립트는 스크립트 폴더에 있으며 해당 위치에서 실행해야 합니다.

    CD $env:ExchangeInstallPath\scripts
    
    .\Move-PublicFolderBranch.ps1 -FolderRoot \Dev -TargetPublicFolderMailbox DeveloperReports01

## 작동 여부는 어떻게 확인합니까?

공용 폴더 이동 요청이 정상적으로 수행되었는지 확인하려면 다음 명령을 실행합니다.

```powershell
Get-PublicFolderMoveRequest | Format-List Status
```

상태가 `Completed`이면 이동 요청이 정상적으로 수행된 것입니다.

이동 요청이 실패한 경우에는 공용 폴더 또는 해당 콘텐츠를 복원해야 합니다. 자세한 내용은 [실패 한 이동에서 공용 폴더 및 공용 폴더 사서함 복원](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)을 참조하십시오.

