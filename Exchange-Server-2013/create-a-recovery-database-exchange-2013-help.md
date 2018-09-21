---
title: '복구 데이터베이스 만들기: Exchange 2013 Help'
TOCTitle: 복구 데이터베이스 만들기
ms:assetid: 34d87491-b7b7-44a9-8d69-e1a9c1fe5852
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee332321(v=EXCHG.150)
ms:contentKeyID: 50482829
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 복구 데이터베이스 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-01-21_

셸을 사용하여 복구 작업의 일환으로 복원된 데이터베이스를 탑재하고 데이터를 추출하는 데 사용되는 특수한 종류의 사서함 데이터베이스인 복구 데이터베이스를 만들 수 있습니다. 복구 데이터베이스를 만든 후 복구 또는 복원된 사서함 데이터베이스를 복구 데이터베이스로 이동한 다음 [New-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829875\(v=exchg.150\)) cmdlet을 사용하여 복구된 데이터베이스에서 데이터를 추출할 수 있습니다. 추출이 끝나면 데이터를 폴더로 내보내거나 기존 사서함에 병합할 수 있습니다. 복구 데이터베이스를 사용하면 현재 데이터에 대한 사용자 액세스를 방해하지 않고 데이터베이스의 백업 또는 복사본에서 데이터를 복구할 수 있습니다.

복구 데이터베이스와 관련된 다른 관리 작업에 대한 자세한 내용은 [복구 데이터베이스](recovery-databases-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "사서함 복구" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 복구 데이터베이스 만들기

다음은 사서함 서버 MBX2에 복구 데이터베이스를 RDB1을 만드는 예입니다.

```powershell
New-MailboxDatabase -Recovery -Name RDB1 -Server MBX2
```

다음은 데이터베이스 파일 및 로그 폴더에 대한 사용자 지정 경로를 사용하여 사서함 서버 MBX1에 복구 데이터베이스 RDB2를 만드는 예입니다.

    New-MailboxDatabase -Recovery -Name RDB2 -Server MBX1 -EdbFilePath "C:\Recovery\RDB2\RDB2.EDB" -LogFolderPath "C:\Recovery\RDB2"

구문과 매개 변수에 대한 자세한 내용은 [New-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/aa997976\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

복구 데이터베이스가 성공적으로 만들어졌는지 확인하려면 다음을 수행하십시오.

  - 셸에서 다음 명령을 실행하여 복구 데이터베이스에 대한 구성 정보를 표시합니다.
    
    ```powershell
Get-MailboxDatabase <RecoveryDatabaseName> | Format-List
```

## 다른 작업

복구 데이터베이스를 만든 후에는 복구 데이터베이스를 사용하여 데이터를 복원할 수도 있습니다. 자세한 단계는 [복구 데이터베이스를 사용하여 데이터 복원](restore-data-using-a-recovery-database-exchange-2013-help.md)을 참조하십시오.

