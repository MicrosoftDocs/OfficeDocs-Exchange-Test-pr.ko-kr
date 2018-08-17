---
title: '실패 한 이동에서 공용 폴더 및 공용 폴더 사서함 복원: Exchange 2013 Help'
TOCTitle: 실패 한 이동에서 공용 폴더 및 공용 폴더 사서함 복원
ms:assetid: 2ade83c9-5f9b-4945-bf32-48fa8185b515
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ983802(v=EXCHG.150)
ms:contentKeyID: 52058064
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 실패 한 이동에서 공용 폴더 및 공용 폴더 사서함 복원

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-13_

공용 폴더 또는 공용 폴더 사서함에 대한 이동 요청이 실패하는 경우 다음 조건이 적용되면 폴더 또는 사서함을 복원할 수 있습니다.

  - **실패한 공용 폴더 이동**   일시 삭제된 공용 폴더의 복사본이 원본 공용 폴더 사서함에 아직 있으며 보존 기간이 아직 남아 있습니다.

  - **실패한 공용 폴더 사서함 이동**   일시 삭제된 공용 폴더 사서함의 복사본이 원본 사서함 데이터베이스에 아직 있으며 사서함 보존 기간이 아직 남아 있습니다.

사서함 보존 기간이 경과된 경우에는 백업에서 개별 공용 폴더 사서함을 복구할 수 있습니다. 그런 다음 복원된 사서함에서 데이터를 추출하여 대상 폴더에 복사하거나 다른 사서함과 병합합니다. 자세한 내용은 [복구 데이터베이스를 사용하여 데이터 복원](restore-data-using-a-recovery-database-exchange-2013-help.md)을 참조하십시오.

공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 복원 요청" 항목

  - EAC를 사용하여 이 절차를 수행할 수는 없으며, 셸을 사용해야 합니다.

  - 복원 요청을 만들려면 일시 삭제된 공용 폴더 사서함에 대해 *DisplayName*, *LegacyDN* 또는 *MailboxGUID* 매개 변수의 값을 제공해야 합니다.

  - 기본적으로 휴지통 폴더가 일반 폴더와 함께 복원됩니다. 휴지통 폴더를 복원하지 않으려면 *ExcludeDumpster* 매개 변수를 사용하면 됩니다.

  - 공용 폴더 사서함 복원의 경우 폴더가 대상 사서함에 없으면 만들어지지 않는다는 점에서 일반 사서함 복원과 다릅니다. 누락된 폴더는 복원 요청 종료 시 경고 메시지에 표시됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 일시 삭제된 공용 폴더 복원

이 예에서는 공용 폴더 \\Dev\\CustomerEnagagements를 대상 공용 폴더 사서함 Development01에 복원합니다.

    New-MailboxRestoreRequest -SourceStoreMailbox Development -SourceDatabase MBX_DB01 -TargetMailbox Development01 -AllowLegacyDNMismatch -IncludeFolders \Dev\CustomerEngagements

구문과 매개 변수에 대한 자세한 내용은 [New-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829875\(v=exchg.150\))를 참조하십시오.

## 일시 삭제된 공용 폴더 사서함 복원

이 예에서는 공용 폴더 사서함 PF\_Singapore을 새 공용 폴더 사서함 PF\_Singapore\_Restore에 복원합니다.

    New-MailboxRestoreRequest -SourceStoreMailbox PF_Singapore -SourceDatabase MBX_DB01 -TargetMailbox PF_Singapore_Restore -AllowLegacyDNMismatch

구문과 매개 변수에 대한 자세한 내용은 [New-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829875\(v=exchg.150\))를 참조하십시오.

