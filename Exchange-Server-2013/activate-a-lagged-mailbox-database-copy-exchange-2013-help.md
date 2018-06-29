---
title: '지연 된 사서함 데이터베이스 복사본 활성화: Exchange 2013 Help'
TOCTitle: 지연 된 사서함 데이터베이스 복사본 활성화
ms:assetid: 493d9c40-644d-49d6-9291-949acbcfdcb6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd979786(v=EXCHG.150)
ms:contentKeyID: 50483030
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 지연 된 사서함 데이터베이스 복사본 활성화

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-01-28_

지연된 사서함 데이터베이스 복사본은 0보다 큰 재생 지연 시간 값을 사용하여 구성된 사서함 데이터베이스 복사본입니다. 데이터베이스에서 모든 로그 파일을 재생하고 데이터베이스 복사본을 최신 상태로 만들려는 경우 지연된 사서함 데이터베이스 복사본을 활성화하고 복구하는 프로세스가 간단합니다. 로그 파일을 지정 시간까지 재생하려는 경우 수동으로 로그 파일을 조작하고 Eseutil을 실행해야 하기 때문에 작업이 더 복잡해집니다.

지연된 사서함 데이터베이스 복사본에 대한 자세한 내용은 [사서함 데이터베이스 복사본 관리](managing-mailbox-database-copies-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> 지연된 사서함 데이터베이스 복사본을 직접 활성화하는 데 걸리는 시간은 재생해야 하는 로그 파일 수와 로그 파일을 재생할 수 있는 하드웨어 속도에 따라 달라집니다. 최소한 로그 재생 속도가 각 데이터베이스마다 초당 로그 두 개 이상이어야 합니다.



## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 1분 지연된 복사본을 복제하고, 필요한 로그 파일을 재생하고, 데이터를 추출하거나 클라이언트 작업을 위해 데이터베이스를 탑재하는 데 걸리는 시간 추가

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

  - 0보다 큰 재생 지연 시간을 사용하여 활성화되는 사서함 데이터베이스 복사본을 구성해야 합니다.

  - 활성화되는 사서함 데이터베이스 복사본에 복구하려는 지정 시간까지의 로그 파일이 모두 있어야 합니다. 복구할 지정 시간을 결정할 때 데이터베이스 트랜잭션이 여러 로그 파일에 걸쳐 있을 수 있다는 것에 주의해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 지연된 사서함 데이터베이스 복사본을 지정 시간까지 활성화


> [!NOTE]
> EAC를 사용하여 지연된 사서함 데이터베이스 복사본을 특정 시점에 활성화할 수는 없습니다. 대신 셸과 명령줄을 사용하여 일련의 단계를 수행합니다.



1.  이 예에서는 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd351074\(v=exchg.150\)) cmdlet을 사용하여 활성화되어 있는 지연된 복사본의 복제를 일시 중단합니다.
    
        Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false

2.  원하는 경우 지연된 복사본을 유지하려면 데이터베이스 복사본 및 해당 로그 파일을 복사합니다.
    

    > [!NOTE]
    > 이때 기존 볼륨에서 계속 이 절차를 수행하면 복사본 쓰기 성능이 저하됩니다. 이 문제를 방지하려면 복구를 수행할 다른 볼륨으로 데이터베이스 및 로그 파일을 복사할 수 있습니다.



3.  Windows 탐색기에 표시된 로그 파일 날짜와 시간에 따라 이 복구에 대한 지정 시간 요구 사항을 충족하기 위해 데이터베이스에 재생해야 하는 로그 파일을 확인합니다. 이 시간 후에 만들어진 모든 로그는 복구 프로세스가 완료되고 더 이상 로그가 필요하지 않을 때까지 다른 디렉터리로 이동되어야 합니다.

4.  데이터베이스에 대한 검사점 파일(.chk)을 삭제합니다.

5.  이 예에서는 Eseutil을 사용하여 복구 작업을 수행합니다.
    
        Eseutil.exe /r eXX /a
    

    > [!NOTE]
    > 앞의 예에서 e<EM>XX</EM>는 데이터베이스의 로그 생성 접두사(예: E00, E01, E02 등)입니다.

    

    > [!IMPORTANT]
    > 재생 지연 시간, 이 기간 동안 생성된 로그 파일 수, 복구되는 데이터베이스에 이러한 로그를 재생할 수 있는 하드웨어 속도 등의 여러 요소에 따라 이 작업에 오랜 시간이 걸릴 수 있습니다.



6.  로그 재생을 마치면 데이터베이스가 완전한 종료 상태가 되며 복사하여 복구 작업에 사용할 수 있습니다.

7.  복구 프로세스가 완료되면 이 예에서는 복구 프로세스의 일부로 사용된 데이터베이스에 대해 복제를 다시 시작합니다.
    
        Resume-MailboxDatabaseCopy DB1\EX3

구문과 매개 변수에 대한 자세한 내용은 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd351074\(v=exchg.150\)) 또는 [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd335220\(v=exchg.150\))를 참조하십시오.

## 셸을 통해 커밋되지 않은 모든 로그 파일을 재생하여 지연된 사서함 데이터 베이스 복사본 활성화

1.  원하는 경우 지연된 복사본을 유지하려면 데이터베이스 복사본 및 해당 로그 파일을 복사합니다.
    
    1.  이 예에서는 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd351074\(v=exchg.150\)) cmdlet을 사용하여 활성화되어 있는 지연된 복사본의 복제를 일시 중단합니다.
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  원하는 경우 지연된 복사본을 유지하려면 데이터베이스 복사본 및 해당 로그 파일을 복사합니다.
        

        > [!NOTE]
        > 이때 기존 볼륨에서 계속 이 절차를 수행하면 복사본 쓰기 성능이 저하됩니다. 이 문제를 방지하려면 복구를 수행할 다른 볼륨으로 데이터베이스 및 로그 파일을 복사할 수 있습니다.



2.  이 예에서는 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/ko-kr/library/dd298068\(v=exchg.150\)) cmdlet과 *SkipLagChecks* 매개 변수를 사용하여 지연된 사서함 데이터베이스 복사본을 활성화합니다.
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -SkipLagChecks

## 셸에서 SafetyNet 복구를 사용하여 지연된 사서함 데이터베이스 복사본 활성화

1.  원하는 경우 지연된 복사본을 유지하려면 데이터베이스 복사본 및 해당 로그 파일이 포함된 볼륨에 대해 파일 시스템 기반(비 Exchange 인식) VSS(볼륨 섀도 복사본 서비스) 스냅숏을 만듭니다.
    
    1.  이 예에서는 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd351074\(v=exchg.150\)) cmdlet을 사용하여 활성화되어 있는 지연된 복사본의 복제를 일시 중단합니다.
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  원하는 경우 지연된 복사본을 유지하려면 데이터베이스 복사본 및 해당 로그 파일을 복사합니다.
        

        > [!NOTE]
        > 이때 기존 볼륨에서 계속 이 절차를 수행하면 복사본 쓰기 성능이 저하됩니다. 이 문제를 방지하려면 복구를 수행할 다른 볼륨으로 데이터베이스 및 로그 파일을 복사할 수 있습니다.



2.  ESEUTIL 데이터베이스 헤더 출력애서 "로그 필요:" 값을 찾아 지연된 데이터베이스 복사본에 필요한 로그를 확인합니다.
    
        Eseutil /mh <DBPath> | findstr /c:"Log Required"
    
    괄호로 묶인 16진수 값을 적어둡니다. 첫 번째 번호는 생성 번호가 가장 낮은 필수 번호이며(LowGeneration이라고 함) 두 번째 번호는 생성 번호가 가장 높은 필수 번호입니다(HighGeneration이라고 함). HighGeneration보다 높은 생성 시퀀스를 가진 모든 로그 생성 파일을 다른 위치로 이동하여 이 파일이 데이터베이스에 재생되지 않도록 합니다.

3.  데이터베이스의 활성 복사본을 호스트하는 서버의 경우 활성 복사본에서 활성화 중인 지연된 복사본의 로그 파일을 삭제하거나 Microsoft Exchange 복제 서비스를 중지합니다.

4.  데이터베이스를 전환하고 지연된 복사본을 활성화합니다. 이 예에서는 여러 매개 변수와 함께 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/ko-kr/library/dd298068\(v=exchg.150\)) cmdlet을 사용하여 데이터베이스를 활성화합니다.
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -MountDialOverride BestEffort -SkipActiveCopyChecks -SkipClientExperienceChecks -SkipHealthChecks -SkipLagChecks

5.  그러면 데이터베이스는 자동으로 탑재되며 SafetyNet으로부터 누락된 메시지의 다시 배달을 요청합니다.

## 작동 여부는 어떻게 확인합니까?

지연된 사서함 데이터베이스 복사본이 활성화되었는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 **서버** \> **데이터베이스**로 이동합니다. 적절한 데이터베이스를 선택하고 세부 정보 창에서 **세부 정보 보기**를 클릭하여 데이터베이스 복사 속성을 봅니다.

  - 셸에서 다음 명령을 실행하여 데이터베이스 복사본에 대한 상태 정보를 표시합니다.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

