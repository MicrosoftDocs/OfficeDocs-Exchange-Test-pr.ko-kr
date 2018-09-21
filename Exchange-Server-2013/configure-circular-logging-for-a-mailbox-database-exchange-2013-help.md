---
title: '사서함 데이터베이스에 대한 순환 로깅 구성: Exchange 2013 Help'
TOCTitle: 사서함 데이터베이스에 대한 순환 로깅 구성
ms:assetid: 29cbd7cd-382b-4e0d-8368-2e49e75df2fc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn756374(v=EXCHG.150)
ms:contentKeyID: 62524840
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 데이터베이스에 대한 순환 로깅 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-06-24_

사서함 데이터베이스에 대해 순환 로깅을 사용하도록 설정할 경우 제공되는 순환 로깅 유형은 사서함 데이터베이스가 연속 복제를 사용하여 복제되는지 여부에 따라 다릅니다.

  - 사서함 데이터베이스가 복제되지 않으면 JET 순환 로깅이 사용됩니다. 이 경우 JET 순환 로깅을 사용하거나 사용하지 않도록 설정하려면 데이터베이스를 분리했다가 탑재해야 합니다.

  - 사서함 데이터베이스가 복제되면 CRCL(연속 복제 순환 로깅)이 사용됩니다. 이 경우 CRCL을 사용하거나 사용하지 않도록 설정하면 동적으로 적용되므로 데이터베이스를 분리했다가 다시 탑재할 필요가 없습니다.

순환 로깅 및 CRCL에 대한 자세한 내용은 [Exchange Native Data Protection](backup-restore-and-disaster-recovery-exchange-2013-help.md)를 참조하세요.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 권한" 항목

## EAC를 사용하여 데이터베이스의 순환 로깅 구성

1.  EAC에서 **서버** \> **데이터베이스**로 이동합니다.

2.  구성할 사서함 데이터베이스를 선택하고 ![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **순환 로깅 사용** 확인란을 선택하거나 선택 취소하고 **저장**을 클릭합니다.

4.  분리 및 탑재 작업이 필요하면 경고 메시지가 표시됩니다. **확인**을 클릭하여 경고 메시지를 닫습니다.
    
    1.  데이터베이스를 분리하려면 **자세히**![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘")를 클릭하고 **분리**를 클릭합니다. 경고 메시지가 표시되면 **예**를 클릭합니다.
    
    2.  데이터베이스를 탑재하려면 **자세히**![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘")를 클릭하고 **탑재**를 클릭합니다. 경고 메시지가 표시되면 **예**를 클릭합니다.

## 셸을 사용하여 데이터베이스의 순환 로깅 구성

이 예제에서는 데이터베이스 DB1에 대한 순환 로깅을 사용하도록 설정합니다.

```powershell
Set-MailboxDatabase DB1 -CircularLoggingEnabled $True
```

이 예제에서는 데이터베이스 DB1에 대한 순환 로깅을 사용하지 않도록 설정합니다.

```powershell
Set-MailboxDatabase DB1 -CircularLoggingEnabled $False
```

구성할 수 있는 사서함 데이터베이스 매개 변수에 대한 자세한 내용은 [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\))를 참조하세요.

