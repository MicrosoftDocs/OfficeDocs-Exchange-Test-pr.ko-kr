---
title: '공용 폴더 사서함을 다른 사서함 데이터베이스로 이동: Exchange 2013 Help'
TOCTitle: 공용 폴더 사서함을 다른 사서함 데이터베이스로 이동
ms:assetid: 67601d45-4824-4ae6-9a7e-b645ec3af4d3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ906434(v=EXCHG.150)
ms:contentKeyID: 51407708
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공용 폴더 사서함을 다른 사서함 데이터베이스로 이동

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-07-21_

부하 분산을 목적으로 또는 리소스를 보다 가까운 지리적 위치로 이동할 목적으로 공용 폴더 사서함을 다른 사서함 데이터베이스로 이동해야 할 수 있습니다. 일반적인 사서함 이동과 마찬가지로 **MoveRequest** cmdlet을 사용하여 공용 폴더 사서함을 이동할 수 있습니다. 사서함 이동에 대한 자세한 내용은 [Exchange 2013 사서함 이동](mailbox-moves-in-exchange-2013-exchange-2013-help.md)을 참조하십시오.

공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간은 공용 폴더 사서함의 크기에 따라 다릅니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 이동 및 마이그레이션 권한" 섹션

  - EAC에서는 이 절차를 수행할 수 없으며, 셸에서만 이 절차를 수행할 수 있습니다.

  - 공용 폴더 사서함 크기에 따라 이동 작업에 몇 시간이 소요될 수 있습니다. 이 시간 동안 사용자는 공용 폴더에 액세스할 수 없습니다. 또한 공용 폴더가 "완료 진행 중" 상태일 때 잠시 동안 공용 폴더에 액세스할 수 없습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 이동 요청 만들기

**New-MoveRequest** cmdlet은 공용 폴더 사서함을 Microsoft Exchange 사서함 복제 서비스 큐에 대기시킵니다. Microsoft Exchange 사서함 복제 서비스를 사용할 수 있게 되면 이 서비스에서 이동 요청을 선택하고 공용 폴더 사서함 이동을 시작하며, 전체 요청을 처음부터 끝까지 완료합니다.

이 예에서는 공용 폴더 사서함 PF\_SanFrancisco를 사서함 데이터베이스 MBX\_DB01로 이동시키는 이동 요청을 시작합니다.

```powershell
New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01
```

구문과 매개 변수에 대한 자세한 내용은 [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))를 참조하십시오.

## 나중에 완료할 이동 요청 만들기

이동 요청 최종 단계에서 `CompletionInProgress` 단계에 있을 때 사용자가 잠길 수 있다 일시적으로 공용 폴더 사서함입니다. 필요한 경우에 해당 단계에 도달 하기 전에 이동 요청을 일시 중단 수 있으며 사용자가 영향을 받을 수 없습니다는 한번에 다시 시작할 수 있습니다.

이 예에서는 공용 폴더 사서함 PF\_SanFrancisco를 사서함 데이터베이스 MBX\_DB01로 이동하는 이동 요청을 시작하고 이동 요청이 완료될 준비가 되면 이 요청을 일시 중단합니다.

```powershell
New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01 -SuspendWhenReadyToComplete
```

구문과 매개 변수에 대한 자세한 내용은 [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))를 참조하십시오.

이 예에서는 공용 폴더 사서함 PF\_SanFrancisco에 대해 진행 중인 사서함 이동의 상태를 검색합니다.

```powershell
Get-MoveRequest -Identity "PF_SanFrancisco"
```

구문과 매개 변수에 대한 자세한 내용은 [Get-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd335227\(v=exchg.150\))를 참조하십시오.

이동 요청 상태가 \[Suspended\]로 설정되면 요청을 다시 시작할 수 있습니다. 이 예에서는 공용 폴더 사서함 PF\_SanFrancisco에 대한 이동 요청을 다시 시작합니다.

```powershell
Resume-MoveRequest -Identity "PF_SanFrancisco"
```

구문과 매개 변수에 대한 자세한 내용은 [Resume-MoveRequest](https://technet.microsoft.com/ko-kr/library/ee332320\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

이동 요청이 만들어졌는지 확인하려면 다음 명령을 실행합니다.

```powershell
Get-MoveRequestStatistics -Identity PF_SanFrancisco | Format-List Status
```

상태가 `Completed`이면 이동 요청이 정상적으로 수행된 것입니다.

이동 요청이 실패한 경우 공용 폴더를 복원해야 할 수 있습니다. 자세한 내용은 [실패 한 이동에서 공용 폴더 및 공용 폴더 사서함 복원](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)을 참조하십시오.

