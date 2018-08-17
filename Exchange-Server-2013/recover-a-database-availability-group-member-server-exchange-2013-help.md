---
title: '데이터베이스 가용성 그룹의 구성원 서버를 복구 합니다.: Exchange 2013 Help'
TOCTitle: 데이터베이스 가용성 그룹의 구성원 서버를 복구 합니다.
ms:assetid: eccd8f61-9706-4bb7-a62a-ec7c166f8019
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638206(v=EXCHG.150)
ms:contentKeyID: 50484440
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 가용성 그룹의 구성원 서버를 복구 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

(DAG) 데이터베이스 가용성 그룹의 구성원 인 사서함 서버 손실 또는 그렇지 않은 경우 실패 하 고 복구할 수 없는 하 고을 교체 해야, 하는 경우에 서버 복구 작업을 수행할 수 있습니다. Microsoft Exchange Server 2013 설치 프로그램을 사용 하 여 서버 복구 작업을 수행할 수 있는 스위치 */m:RecoverServer* 를 포함 합니다. */m:RecoverServer* 스위치를 사용 하면 설치 프로그램을 실행 하는 서버와 이름이 같은 서버에 대 한 Active Directory 에서 서버의 구성 정보를 읽을 수는 설치 된 설치 프로그램을 실행 합니다. 서버의 구성 후 Active Directory, 원래 Exchange 파일에서에서 정보를 수집 하 고 서비스는 다음의 서버에 설치 됩니다 역할 및 Active Directory 에 저장 된 설정 그러면 서버에 적용 됩니다.

DAG와 관련된 다른 관리 작업에 대한 자세한 내용은 [데이터베이스 가용성 그룹 관리](managing-database-availability-groups-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 30분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

  - 기본 위치가 아닌 다른 위치에 Exchange를 설치 하는 경우에 Exchange 프로그램 파일의 위치를 지정 하려면 */TargetDir* 설치 스위치를 사용 해야 합니다. */TargetDir* 스위치를 사용 하지 않으면 하는 경우 Exchange 프로그램 파일의 기본 위치 (%programfiles%\\Microsoft\\Exchange Server\\V15)에 설치 됩니다.
    
    설치 위치를 확인하려면 다음 단계를 따르십시오.
    
    1.  ADSIEDIT.MSC 또는 LDP.EXE를 엽니다.
    
    2.  다음 위치로 이동합니다. **CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com**
    
    3.  Exchange 서버 개체를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.
    
    4.  **msExchInstallPath** 특성을 찾습니다. 이 특성은 현재 설치 경로를 저장합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 설치 프로그램의 /m:RecoverServer를 사용하여 서버 복구

1.  [Get-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb124924\(v=exchg.150\)) cmdlet을 사용하여 복구하려는 서버에 있는 모든 사서함 데이터베이스 복사본의 재생 지연 또는 자르기 지연 설정을 검색합니다.
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd335119\(v=exchg.150\)) cmdlet을 사용하여 복구하려는 서버에 있는 모든 사서함 데이터베이스 복사본을 제거합니다.
    
        Remove-MailboxDatabaseCopy DB1\MBX1

3.  [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ko-kr/library/dd297956\(v=exchg.150\)) cmdlet을 사용하여 DAG에서 실패한 서버의 구성을 제거합니다.
    
        Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    

    > [!NOTE]
    > 제거 되는 DAG 구성원 오프 라인 및 온라인 상태로 만들 수 없습니다, 경우에 위 명령에 <EM>ConfigurationOnly</EM> 매개 변수를 추가 해야 합니다. <EM>ConfigurationOnly</EM> 스위치를 사용 하는 경우 수동으로 클러스터에서 노드를 제거 해야 합니다.



4.  Active Directory 에서 서버의 컴퓨터 계정을 다시 설정 합니다. 자세한 단계 [컴퓨터 계정 재설정](http://go.microsoft.com/fwlink/p/?linkid=167188)를 참조 합니다.

5.  명령 프롬프트 창을 엽니다. 원본 설치 미디어를 사용하여 다음 명령을 실행합니다.
    
        Setup /m:RecoverServer

6.  설치 프로그램의 복구 프로세스가 완료되면 [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ko-kr/library/dd298049\(v=exchg.150\)) cmdlet을 사용하여 복구된 서버를 DAG에 추가합니다.
    
        Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

7.  서버가 다시 DAG에 추가된 후 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd298105\(v=exchg.150\)) cmdlet을 사용하여 사서함 데이터베이스 복사본을 다시 구성할 수 있습니다. 추가하려는 데이터베이스 복사본의 재생 지연 또는 자르기 지연 시간이 이전에 0을 넘긴 적이 있는 경우 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd298105\(v=exchg.150\)) cmdlet의 *ReplayLagTime* 및 *TruncationLagTime* 매개 변수를 사용하여 이러한 설정을 다시 구성할 수 있습니다.
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX1
        Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00
        Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -TruncationLagTime 3.00:00:00

## 작동 여부는 어떻게 확인합니까?

DAG 구성원을 성공적으로 복구 했는지를 확인 하려면 다음을 수행 합니다.

  - 셸에서 복구 된 DAG 구성원의 상태를 확인 하려면 다음 명령을 실행 합니다.
    
    ```
    Test-ReplicationHealth <ServerName>
    ```
    
    ```
    Get-MailboxDatabaseCopyStatus -Server <ServerName>
    ```
    
    복제 상태 테스트를 모두 성공적으로 전달 해야 하 고 데이터베이스 및 해당 콘텐츠 인덱스의 상태가 정상 이어야 합니다.

