---
title: '사서함 데이터베이스 복사본 업데이트: Exchange 2013 Help'
TOCTitle: 사서함 데이터베이스 복사본 업데이트
ms:assetid: bead3cc5-7d50-446f-95b7-e432bcb7968e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351100(v=EXCHG.150)
ms:contentKeyID: 50484034
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 데이터베이스 복사본 업데이트

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2012-11-02_

*시드*라고도 하는 업데이트는 사서함 데이터베이스의 복사본을 DAG(데이터베이스 사용 가능 그룹)의 다른 사서함 서버에 추가하는 프로세스를 말합니다. 새로 추가된 복사본은 활성 복사본에서 복사된 로그 파일이 재생되는 수동 복사본에 대한 기본 데이터베이스가 됩니다. 시드가 필요한 경우는 다음과 같습니다.

  - 데이터베이스의 새 수동 복사본이 만들어지는 경우 시드는 새 사서함 데이터베이스 복사본에 대해 연기될 수 있지만 결국 중복 데이터베이스 복사본으로 기능을 하려면 각 수동 데이터베이스 복사본을 시드해야 합니다.

  - 수동 데이터베이스 복사본이 현저하게 차이가 나거나 복구할 수 없게 되면서 데이터가 손실되어 장애 조치가 발생한 후

  - 시스템에서 데이터베이스의 수동 복사본으로 재생될 수 없는 손상된 로그 파일이 검색되는 경우

  - 데이터베이스 복사본의 오프라인 조각 모음이 발생한 후

  - 데이터베이스의 로그 생성 시퀀스가 1로 다시 설정된 후

시드 작업을 수행할 때 사용할 수 있는 방법은 다음과 같습니다.

  - <strong>자동 시드</strong>   자동 시드는 대상 사서함 서버에 활성 데이터베이스의 수동 복사본을 만듭니다. 자동 시드는 데이터베이스를 만드는 동안 발생합니다.

  - <strong>Update-MailboxDatabaseCopy cmdlet을 사용한 시드</strong>   셸에서 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd335201\(v=exchg.150\)) cmdlet을 사용하여 언제든지 데이터베이스 복사본을 시드할 수 있습니다.

  - <strong>사서함 데이터베이스 복사본 업데이트 마법사를 사용한 시드</strong>   EAC에서 사서함 데이터베이스 복사본 업데이트 마법사를 사용하여 언제든지 데이터베이스 복사본을 시드할 수 있습니다.

  - <strong>오프라인 데이터베이스의 수동 복사</strong>   데이터베이스의 활성 복사본을 분리하고 데이터베이스 파일을 같은 DAG에 있는 다른 사서함 서버의 동일한 위치로 복사할 수 있습니다. 이 방법에서는 데이터베이스를 분리하는 프로세스가 필요하므로 서비스가 중단됩니다.

데이터베이스 복사본을 업데이트하는 데는 시간이 오래 걸릴 수 있으며, 특히 복사하는 데이터베이스의 용량이 크거나 네트워크 대기 시간이 길거나 네트워크 대역폭이 낮은 경우 오래 걸릴 수 있습니다. 시드 프로세스가 시작된 후에는 프로세스가 완료될 때까지 EAC 또는 셸을 닫지 마십시오. 닫을 경우 시드 작업이 종료됩니다.

활성 복사본 또는 최신 수동 복사본을 시드를 위한 원본으로 사용하여 데이터베이스 복사본을 시드할 수 있습니다. 수동 복사본에서 시드할 때 다음과 같은 상황에서는 네트워크 통신 오류와 함께 시드 작업이 종료됩니다.

  - 시드 원본 복사본의 상태가 실패 또는 FailedAndSuspended로 변경된 경우

  - 데이터베이스가 다른 복사본으로 장애 조치된 경우

여러 데이터베이스 복사본을 동시에 시드할 수 있습니다. 그러나 여러 복사본을 동시에 시드할 때는 데이터베이스 파일만 시드해야 하며 콘텐츠 인덱스 카탈로그에서 생략해야 합니다. [Update-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd335201\(v=exchg.150\)) cmdlet이 있는 *DatabaseOnly* 매개 변수를 사용하여 이 작업을 수행할 수 있습니다.


> [!NOTE]
> 같은 원본에서 여러 대상을 시드할 때 <EM>DatabaseOnly</EM> 매개 변수를 사용하지 않을 경우 SeedInProgressException 오류 FE1C6491이 나타나면서 작업이 실패합니다.



사서함 데이터베이스 복사본과 관련된 다른 관리 작업에 대한 자세한 내용은 [사서함 데이터베이스 복사본 관리](managing-mailbox-database-copies-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 2분 + 데이터베이스 복사본을 시드하는 시간. 이 시간은 데이터베이스 크기, 속도, 사용 가능한 대역폭, 네트워크의 대기 시간, 저장소 속도 등과 같은 다양한 요소에 따라 달라집니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

  - 사서함 데이터베이스 복사본을 일시 중단해야 합니다. 자세한 단계는 [사서함 데이터베이스 복사본을 다시 시작 또는 일시 중단](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md)을 참조하십시오.

  - 업데이트할 수동 데이터베이스 복사본을 호스트하는 서버에서 원격 레지스트리 서비스가 실행되고 있어야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 데이터베이스 복사본 업데이트

1.  EAC에서 <strong>서버</strong> \> <strong>데이터베이스</strong>로 이동합니다.

2.  업데이트할 수동 복사본의 사서함 데이터베이스를 선택합니다.

3.  세부 정보 창의 <strong>데이터베이스 복사본</strong>에서 시드할 수동 데이터베이스 복사본 아래에 있는 <strong>일시 중단</strong>을 클릭합니다. 설명을 입력하고(선택 사항) <strong>저장</strong>을 클릭합니다.

4.  세부 정보 창의 <strong>데이터베이스 복사본</strong>에서 시드할 수동 데이터베이스 복사본 아래에 있는 <strong>업데이트</strong>를 클릭합니다.

5.  
    
    기본적으로 데이터베이스의 활성 복사본은 시드를 위한 원본 데이터베이스로 사용됩니다. 데이터베이스의 수동 복사본을 시드에 사용하려면 <strong>찾아보기…</strong>를 클릭하여 원본으로 사용할 수동 데이터베이스 복사본이 있는 서버를 선택합니다.

6.  <strong>저장</strong>을 클릭하여 수동 데이터베이스 복사본을 업데이트합니다.

## 셸을 사용하여 사서함 데이터베이스 복사본 업데이트

이 예에서는 MBX1에 있는 데이터베이스 DB1의 복사본을 시드하는 방법을 보여줍니다.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1
```

이 예에서는 MBX2를 시드의 원본 사서함 서버로 사용하여 MBX1에 있는 데이터베이스 DB1의 복사본을 시드하는 방법을 보여줍니다.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2
```

이 예에서는 콘텐츠 인덱스 카탈로그를 시드하지 않고 MBX1에 있는 데이터베이스 DB1의 복사본을 시드하는 방법을 보여줍니다.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -DatabaseOnly
```

이 예에서는 데이터베이스 파일을 시드하지 않고 MBX1에 있는 데이터베이스 DB1 복사본의 콘텐츠 인덱스 카탈로그를 시드하는 방법을 보여줍니다.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly
```

## 수동으로 오프라인 데이터베이스 복사

1.  데이터베이스에서 순환 로깅을 사용하도록 설정되어 있을 경우 단계를 진행하기 전에 이 설정을 사용하지 않도록 변경합니다. 다음 예에 나오는 대로, [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\)) cmdlet을 사용하여 사서함 데이터베이스에 대한 순환 로깅을 사용하지 않도록 설정할 수 있습니다.
    
    ```powershell
    Set-MailboxDatabase DB1 -CircularLoggingEnabled $false
    ```

2.  데이터베이스를 분리합니다. 다음 예에 나오는 대로, [Dismount-Database](https://technet.microsoft.com/ko-kr/library/bb124936\(v=exchg.150\)) cmdlet을 사용할 수 있습니다.
    
    ```powershell
    Dismount-Database DB1 -Confirm $false
    ```

3.  데이터베이스 파일(데이터베이스 파일 및 모든 로그 파일)을 외부 디스크 드라이브 또는 네트워크 공유와 같은 다른 위치에 수동으로 복사합니다.

4.  데이터베이스를 탑재합니다. 다음 예에 나오는 대로, [Mount-Database](https://technet.microsoft.com/ko-kr/library/aa998871\(v=exchg.150\)) cmdlet을 사용할 수 있습니다.
    
    ```powershell
    Mount-Database DB1
    ```

5.  복사본을 호스트할 서버에서 외부 드라이브 또는 네트워크 공유의 데이터베이스 파일을 활성 데이터베이스 복사본과 동일한 경로에 복사합니다. 예를 들어 활성 복사본 데이터베이스 경로가 D:\\DB1\\DB1.edb이고 로그 파일 경로가 D:\\DB1인 경우, 복사본을 호스트하는 서버의 D:\\DB1에 데이터베이스 파일을 복사합니다.

6.  다음 예에 나오는 대로, [Add-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd298105\(v=exchg.150\)) cmdlet을 *SeedingPostponed* 매개 변수와 함께 사용하여 사서함 데이터베이스 복사본을 추가합니다.
    
    ```powershell
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -SeedingPostponed
    ```

7.  데이터베이스에 순환 로깅이 사용하도록 설정된 경우 다음 예에 나오는 대로, [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\)) cmdlet을 사용하여 다시 사용하도록 설정합니다.
    
    ```powershell
    Set-MailboxDatabase DB1 -CircularLoggingEnabled $true
    ```

## 작동 여부는 어떻게 확인합니까?

사서함 데이터베이스 복사본이 성공적으로 시드되었는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 <strong>서버</strong> \> <strong>데이터베이스</strong>로 이동합니다. 시드된 데이터베이스를 선택합니다. 세부 정보 창에 데이터베이스 복사본의 상태 및 해당 콘텐츠 인덱스와 함께 현재 복사 큐 길이가 표시됩니다.

  - 셸에서 다음 명령을 실행하여 사서함 데이터베이스 복사본이 성공적으로 시드되어 있고 정상 상태인지 확인합니다.
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    ```
    
    상태 및 콘텐츠 인덱스 상태가 모두 정상이어야 합니다.

