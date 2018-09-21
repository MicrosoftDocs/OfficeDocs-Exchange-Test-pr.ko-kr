---
title: '고가용성 및 사이트 복구 배포: Exchange 2013 Help'
TOCTitle: 고가용성 및 사이트 복구 배포
ms:assetid: 4c4e00a4-1f57-4fdb-b9b2-2779abf381a9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638129(v=EXCHG.150)
ms:contentKeyID: 50483060
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 고가용성 및 사이트 복구 배포

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange Server 2013에서는 *증분 배포*로 알려진 개념을 사용하여 고가용성과 사이트 복구를 실현합니다. 두 개 이상의 Exchange 2013 사서함 서버를 독립 실행형 서버로 간단히 설치한 다음 고가용성 및 사이트 복구 기능을 제공하기 위해 필요에 따라 사서함 서버와 사서함 데이터베이스를 추가로 구성합니다.

## 배포 프로세스 개요

각 조직에서 사용하는 실제 단계는 약간씩 다를 수 있지만 고가용 또는 사이트 복구 구성의 Exchange 2013을 배포하는 전체 프로세스는 일반적으로 동일합니다. DAG(데이터베이스 가용성 그룹)를 구성 및 배포하고 사서함 데이터베이스 복사본을 만들기 위해 필요한 계획 및 디자인 작업을 수행한 후 다음과 같이 합니다.

1.  DAG를 만듭니다. 자세한 단계는 [데이터베이스 가용성 그룹 만들기](create-a-database-availability-group-exchange-2013-help.md)를 참조하십시오.

2.  필요한 경우 CNO(클러스터 이름 개체)를 사전 준비합니다. Windows Server 2012를 실행하는 사서함 서버를 사용하여 DAG를 배포할 때는 DNO를 사전 준비해야 합니다. Windows Server 2012 R2를 실행하는 사서함 서버를 사용하여 관리 액세스 포인트가 없는 DAG를 배포하는 경우에는 CNO를 사전 준비할 필요가 없습니다. 컴퓨터 계정 생성이 제한되거나 컴퓨터 계정이 기본 컴퓨터 컨테이너가 아닌 다른 컨테이너에 생성되는 환경에서도 사전 준비 작업이 필요합니다. 자세한 단계는 [데이터베이스 가용성 그룹에 대한 클러스터 이름 개체 미리 준비](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)를 참조하십시오.

3.  둘 이상의 사서함 서버를 DAG에 추가합니다. 자세한 단계는 [데이터베이스 가용성 그룹 구성원 관리](manage-database-availability-group-membership-exchange-2013-help.md)를 참조하십시오.

4.  필요에 맞게 DAG 속성을 구성합니다.
    
    1.  필요에 따라 DAG 암호화 및 압축, 복제 포트, DAG IP 주소 및 기타 DAG 속성을 구성합니다. 자세한 단계는 [데이터베이스 가용성 그룹 속성 구성](configure-database-availability-group-properties-exchange-2013-help.md)을 참조하십시오.
    
    2.  DAG에 대해 DAC(데이터 센터 활성화 조정) 모드를 사용하도록 설정합니다. 이렇게 하면 데이터 센터 전환이 수행된 후 기본 데이터 센터로 다시 전환하는 동안 데이터베이스 수준의 분할 브레인 상태에서 DAG를 보호하고 기본 제공 DAG 복구 cmdlet을 사용할 수 있습니다. 자세한 내용은 [데이터 센터 활성화 조정 모드](datacenter-activation-coordination-mode-exchange-2013-help.md)를 참조하십시오.

5.  사서함 서버의 사서함 데이터베이스 복사본을 DAG에 추가합니다. 자세한 단계는 [사서함 데이터베이스 복사본을 추가 합니다.](add-a-mailbox-database-copy-exchange-2013-help.md)를 참조하십시오.

## 배포 예: 두 데이터 센터의 네 구성원 DAG

이 예에서는 Contoso, Ltd.라는 조직이 두 물리적 위치에 확장될 네 구성원 DAG를 구성 및 배포하는 방법을 자세히 설명합니다. 두 물리적 위치: 레드몬드(워싱턴 주), 포틀랜드(오리건 주)

## 기본 인프라

각 위치에는 Exchange 2013을 기반으로 메시징 인프라를 운영하는 데 필요한 다음과 같은 인프라 요소가 포함되어 있습니다.

  - 디렉터리 서비스(Active Directory 또는 AD DS(Active Directory))

  - DNS(Domain Name System) 이름 확인

  - 여러 Exchange 2013 클라이언트 액세스 서버

  - 여러 Exchange 2013 사서함 서버

다음 그림에서는 Contoso 구성을 보여 줍니다.

**두 사이트 간에 확장된 데이터베이스 사용 가능 그룹**

![두 사이트에 확장된 데이터베이스 사용 가능 그룹](images/Dd638129.1c326fd4-3c7b-4416-a63d-fbfdd0cc6b18(EXCHG.150).gif "두 사이트에 확장된 데이터베이스 사용 가능 그룹")

## 네트워크 구성

이전 그림에서 설명한 대로 솔루션은 여러 서브넷과 여러 네트워크의 사용을 포함합니다. DAG의 각 사서함 서버는 개별 서브넷에 두 개의 네트워크 어댑터를 갖습니다. 각 사서함 서버에서 네트워크 어댑터 하나는 MAPI 네트워크(192.168.*x*.*x*)에 사용되고 하나는 복제 네트워크(10.0.*x*.*x*)에 사용됩니다. MAPI 네트워크만 Active Directory, DNS 서비스, 다른 Exchange 서버와 클라이언트에 대한 연결을 제공합니다. 각 구성원의 복제 네트워크에 사용되는 어댑터는 DAG의 다른 구성원의 복제 네트워크 어댑터에만 연결을 제공합니다.

각 노드의 각 네트워크 어댑터에 대한 설정은 다음 표에 자세히 나와 있습니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>이름</th>
<th>IPv4 주소</th>
<th>서브넷 마스크</th>
<th>기본 게이트웨이</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MBX1(MAPI)</p></td>
<td><p>192.168.1.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>MBX2(MAPI)</p></td>
<td><p>192.168.1.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX3(MAPI)</p></td>
<td><p>192.168.2.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="even">
<td><p>MBX4(MAPI)</p></td>
<td><p>192.168.2.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX1(복제)</p></td>
<td><p>10.0.1.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>MBX2(복제)</p></td>
<td><p>10.0.1.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>없음</p></td>
</tr>
<tr class="odd">
<td><p>MBX3(복제)</p></td>
<td><p>10.0.2.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>MBX4(복제)</p></td>
<td><p>10.0.2.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>없음</p></td>
</tr>
</tbody>
</table>


이 표에 나와 있는 대로, 복제 네트워크에 사용되는 어댑터는 기본 게이트웨이를 사용하지 않습니다. 각 복제 네트워크 어댑터 간에 네트워크 연결을 제공하기 위해 Contoso에서는 Netsh.exe 도구를 사용해 구성하는 영구 고정 경로를 사용합니다.

MBX1과 MBX2의 복제 네트워크 어댑터에 대한 라우팅을 구성하기 위해 각 서버에서 다음 명령을 실행했습니다.

```powershell
netsh interface ipv4 add route 10.0.2.0/24 <NetworkName> 10.0.1.254
```

MBX3과 MBX4의 복제 네트워크 어댑터에 대한 라우팅을 구성하기 위해 각 서버에서 다음 명령을 실행했습니다.

```powershell
netsh interface ipv4 add route 10.0.1.0/24 <NetworkName> 10.0.2.254
```

다음 추가 네트워크 설정도 구성했습니다.

  - 각 DAG 구성원의 MAPI 네트워크 어댑터에 대해서는 **DNS에 이 연결의 주소를 등록** 확인란이 선택되고, 각 복제 네트워크 어댑터에서는 이 확인란의 선택이 취소됩니다.

  - 각 DAG 구성원의 MAPI 네트워크 어댑터에 대해서는 적어도 하나의 DNS 서버 주소가 구성되고, 복제 네트워크 어댑터에 대해서는 아무것도 구성되지 않습니다. 중복을 위해, Contoso는 MAPI 네트워크 어댑터에 여러 DNS 서버 주소를 사용하고 있습니다.

  - Contoso는 Windows 방화벽을 사용하지 않으며, 서버에서 이 기능을 해제했습니다.

네트워크 어댑터를 구성한 후 Contoso는 DAG를 만들고 DAG에 사서함 서버를 추가할 준비를 완료했습니다.

## 데이터베이스 가용성 그룹 만들기 및 구성

관리자는 여러 작업을 수행하는 Windows PowerShell 명령줄 인터페이스 스크립트를 사용하기로 결정했습니다.

  - 이 스크립트는 [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/ko-kr/library/dd351107\(v=exchg.150\)) cmdlet을 사용하여 DAG를 만듭니다. REDMOND는 기본 데이터 센터로 간주되므로 Contoso는 같은 데이터 센터에 CAS1이라는 미러링 모니터 서버를 사용하기로 결정했습니다.

  - 데이터 센터 전환이 필요한 경우 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ko-kr/library/dd297934\(v=exchg.150\)) cmdlet을 사용하여 대체 미러링 모니터 서버와 대체 미러링 모니터 디렉터리를 사전 구성합니다.

  - [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ko-kr/library/dd298049\(v=exchg.150\)) cmdlet을 사용하여 네 개의 각 사서함 서버를 DAG에 추가합니다.

  - [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ko-kr/library/dd297934\(v=exchg.150\)) cmdlet을 사용하여 DAG를 DAC 모드로 구성합니다. DAC 모드에 대한 자세한 내용은 [데이터 센터 활성화 조정 모드](datacenter-activation-coordination-mode-exchange-2013-help.md)를 참조하십시오.

다음은 스크립트에 사용된 명령입니다.

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer CAS1 -WitnessDirectory C:\DAGWitness\DAG1.contoso.com -DatabaseAvailabilityGroupIPAddresses 192.168.1.8,192.168.2.8

이 명령은 DAG1이라는 DAG를 만들고, CAS1을 미러링 모니터 서버로 구성하고, 특정 감시 디렉터리(C:\\DAGWitness\\DAG1.contoso.com)를 구성하고, DAG에 두 개의 IP 주소(MAPI 네트워크의 각 서브넷에 하나씩)를 구성합니다.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGWitness\DAG1.contoso.com -AlternateWitnessServer CAS4

이 명령은 DAG1이 CAS4의 대체 미러링 모니터 서버와 CAS1에 구성된 것과 동일한 경로를 사용하는 CAS4의 대체 감시 디렉터리를 사용하도록 구성합니다.


> [!NOTE]
> 동일한 경로를 필수적으로 사용해야 하는 것은 아닙니다. Contoso는 구성을 표준화하기 위해 동일한 경로를 사용하도록 선택했습니다.



    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX3
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX4

이 명령은 각 사서함 서버를 한 번에 하나씩 DAG에 추가합니다. 또한 각 사서함 서버에 Windows 장애 조치(failover) 클러스터링 구성 요소도 설치하고(아직 설치하지 않은 경우), 장애 조치(failover) 클러스터를 만들고, 새로 만든 클러스터에 각 사서함 서버를 가입시킵니다.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly
```

이 명령은 DAG에 대해 DAC 모드를 사용하도록 설정합니다.

## 사서함 데이터베이스 및 사서함 데이터베이스 복사본

DAG를 만들고 DAG에 사서함 서버를 추가한 후 Contoso는 사서함 데이터베이스와 사서함 데이터베이스 복사본을 만들 준비를 합니다. 오류를 견디기 위한 조건을 충족하기 위해, Contoso는 지연되지 않은 데이터 베이스 복사본 세 개와 지연된 데이터베이스 복사본 하나로 각 사서함 데이터베이스를 구성할 계획을 세웁니다. 지연된 복사본은 3일의 구성된 로그 재생 지연을 갖게 됩니다.

이 구성으로 각 데이터베이스에 대한 총 4개(활성 1개, 지연되지 않은 수동 2개, 지연된 수동 1개)의 복사본이 제공됩니다. Contoso는 서버당 네 개의 활성 데이터베이스를 갖는 계획을 세웁니다. 서버당 활성 데이터베이스 4개와 각 데이터베이스의 수동 복사본 3개를 비롯하여, Contoso 솔루션은 총 16개의 데이터베이스 복사본을 포함합니다.

다음 그림에 나와 있는 대로, Contoso는 데이터베이스 레이아웃에 균형 잡힌 접근 방식을 취하고 있습니다.

**Contoso, Ltd의 데이터베이스 복사본 레이아웃**

![Contoso, Ltd의 데이터베이스 복사본 레이아웃](images/Dd638129.41d0c78e-ccaf-4b67-8bab-6fb344668ead(EXCHG.150).gif "Contoso, Ltd의 데이터베이스 복사본 레이아웃")

각 사서함 서버는 한 개의 활성 사서함 데이터베이스 복사본, 두 개의 지연되지 않은 수동 데이터베이스 복사본 및 한 개의 지연된 수동 데이터베이스 복사본을 호스트합니다. 각 활성 사서함 데이터베이스의 지연된 복사본은 다른 사이트의 사서함 서버에서 호스트됩니다.

이 구성을 만들기 위해 관리자는 여러 명령을 실행합니다.

MBX1에 대해 다음 명령을 실행합니다.

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -SuspendComment "Seed from MBX4" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB1\MBX3 -SourceServer MBX4
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -ActivationOnly

MBX2에 대해 다음 명령을 실행합니다.

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -SuspendComment "Seed from MBX3" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB2\MBX4 -SourceServer MBX3
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -ActivationOnly

MBX3에 대해 다음 명령을 실행합니다.

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -SuspendComment "Seed from MBX2" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB3\MBX1 -SourceServer MBX2
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -ActivationOnly

MBX4에 대해 다음 명령을 실행합니다.

    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX2 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -SuspendComment "Seed from MBX1" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB4\MBX2 -SourceServer MBX1
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -ActivationOnly

**Add-MailboxDatabaseCopy** cmdlet에 대한 위 예에서 *ActivationPreference* 매개 변수는 지정되지 않았습니다. 추가된 각 복사본을 사용하여 활성화 기본 설정 번호가 자동으로 증가합니다. 원본 데이터베이스는 항상 우선 설정 번호 1을 갖고, **Add-MailboxDatabaseCopy** cmdlet을 사용하여 추가된 첫 복사본에 우선 설정 번호 2가 자동으로 할당되며, 제거되는 복사본이 없다는 가정 하에 그 다음 추가된 복사본에 우선 설정 번호 3이 할당됩니다. 따라서, 위 예에서는 활성 복사본과 같은 데이터 센터의 수동 복사본이 활성화 우선 설정 번호 2를 갖고, 원격 데이터 센터의 지연되지 않은 수동 복사본이 활성화 우선 설정 번호 3을 가지며, 원격 데이터 센터의 지연된 수동 복사본이 활성화 우선 설정 번호 4를 갖습니다.

다른 위치의 WAN에 걸쳐 있는 각 활성 데이터베이스의 복사본은 두 개지만 WAN을 통한 시드는 한 번만 수행되었습니다. 이는 Contoso가 Exchange 2013의 기능을 활용하여 데이터베이스의 수동 복사본을 시드의 원본으로 사용하고 있기 때문입니다. [Add-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd298105\(v=exchg.150\)) cmdlet에 *SeedingPostponed* 매개 변수를 함께 사용하면 만들어지는 새 데이터베이스 복사본이 자동으로 시드되는 일이 방지됩니다. 그러면 관리자는 시드되지 않은 복사본을 일시 중단하고, [Update-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd335201\(v=exchg.150\)) cmdlet에 *SourceServer* 매개 변수를 사용하여 데이터베이스의 로컬 복사본을 시드 작업의 원본으로 지정할 수 있습니다. 따라서, 각 위치로 추가되는 보조 데이터베이스 복사본의 시드는 WAN을 통하지 않고 로컬로 수행됩니다.


> [!NOTE]
> 위 예에서 지연되지 않은 데이터베이스 복사본은 WAN을 통해 시드되고, 이 복사본은 지연되지 않은 복사본과 같은 데이터 센터에 있는 데이터베이스의 지연된 복사본을 시드하는 데 사용됩니다.



Contoso는 거의 발생하지는 않지만 치명적인 데이터베이스 논리적 손상에 대한 보호를 제공하기 위해 각 사서함 데이터베이스의 수동 복사본 중 하나를 지연된 데이터베이스 복사본으로 구성했습니다. 그 결과로, 관리자는 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd351074\(v=exchg.150\)) cmdlet에 *ActivationOnly* 매개 변수를 사용하여 지연된 복사본이 활성화에 대해 차단되도록 구성하고 있습니다. 이렇게 하면 데이터베이스 또는 서버 장애 조치(failover)가 수행되는 경우 지연된 데이터베이스 복사본이 활성화되지 않습니다.

## 솔루션 유효성 검사

솔루션을 배포하고 구성한 후, 관리자는 DAG에서 프로덕션 사서함을 데이터베이스로 이동하기에 앞서 솔루션의 준비 상태를 검사하는 작업을 수행합니다. 솔루션을 테스트할 때는 오류 시뮬레이션을 포함한 몇 가지 방법을 사용해야 합니다. 솔루션의 유효성을 확인하기 위해 관리자는 다음과 같은 몇 가지 작업을 수행합니다.

DAG의 전반적인 상태를 확인하기 위해 [Test-ReplicationHealth](https://technet.microsoft.com/ko-kr/library/bb691314\(v=exchg.150\)) cmdlet을 실행합니다. 이 cmdlet은 복제 및 재생 상태를 검사하여 DAG의 각 사서함 서버와 데이터베이스 복사본에 대한 정보를 제공합니다.

복제 및 재생 작업을 확인하기 위해 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ko-kr/library/dd298044\(v=exchg.150\)) cmdlet을 실행합니다. 이 cmdlet은 특정 서버의 모든 사서함 데이터베이스 복사본 또는 특정 사서함 데이터베이스 복사본에 대한 실시간 상태 정보를 제공할 수 있습니다. DAG의 복제된 데이터베이스 상태 모니터링에 대한 자세한 내용은 [데이터베이스 사용 가능 그룹 모니터링](monitoring-database-availability-groups-exchange-2013-help.md)을 참조하십시오.

전환 작업이 예상대로 작동하는지 확인하려면 관리자가 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/ko-kr/library/dd298068\(v=exchg.150\)) cmdlet을 사용하여 일련의 데이터베이스/서버 전환을 수행합니다. 이 작업들이 성공적으로 완료되면 관리자는 같은 cmdlet을 사용하여 활성 데이터베이스 복사본을 원래 위치로 이동합니다.

다양한 오류 시나리오에서 예상되는 동작을 확인하기 위해 오류를 시뮬레이션하거나 실제로 오류가 발생하도록 하는 여러 가지 작업을 수행합니다. 예를 들면 관리자는 다음과 같이 할 수 있습니다.

  - MBX1에서 전원 코드를 분리하여 서버 장애 조치(failover)가 수행되도록 합니다. 그런 다음 관리자가 DB1이 다른 서버(가급적 MBX2, 활성화 기본 설정 값 기준)에서 활성 상태가 되는지 확인합니다.

  - MBX2에서 MAPI 네트워크 어댑터의 네트워크 케이블을 분리하여 서버 장애 조치(failover)가 수행되도록 합니다. 그런 다음 관리자가 DB2이 다른 서버(가급적 MBX1, 활성화 기본 설정 값 기준)에서 활성 상태가 되는지 확인합니다.

  - DB3의 활성 복사본에 사용되는 디스크를 오프라인으로 만들어 서버 장애 조치(failover)가 수행되도록 합니다. 그런 다음 관리자가 DB3이 다른 서버(가급적 MBX4, 활성화 기본 설정 값 기준)에서 활성 상태가 되는지 확인합니다.

비즈니스 요구 사항에 따라 조직에서 테스트할 다른 오류 시나리오가 있을 수 있습니다. 전원 플러그를 뽑는 것 같은 단일 오류를 시뮬레이션하고 솔루션의 복구 동작을 확인한 후, 관리자는 솔루션을 원래 구성으로 되돌려야 합니다. 경우에 따라서는 여러 동시 오류에 대해 솔루션을 테스트할 수 있습니다. 궁극적으로, 솔루션 테스트 계획은 각 오류 시뮬레이션이 완료된 후 솔루션이 원래 구성으로 돌아가는지 여부를 알려줍니다.

또한, 관리자는 두 데이터 센터 간 네트워크 연결을 끊어 사이트 오류가 시뮬레이션되도록 합니다. 데이터 센터 전환 수행은 한층 더 복잡하고 조화가 필요하지만, 배포하는 솔루션이 메시징 서비스와 데이터에 대한 사이트 복구를 제공할 목적을 가진 경우 권장되는 프로세스입니다.

## 작업 전환

솔루션을 배포한 후 증분 배포를 통해 더욱 확장할 수 있습니다. 이러한 점에서 솔루션 관리는 다음 작업이 수행되는 작업 프로세스로의 전환이기도 합니다.

  - DAG 및 사서함 데이터베이스 복사본의 상태를 모니터링합니다. 자세한 내용은 [데이터베이스 사용 가능 그룹 모니터링](monitoring-database-availability-groups-exchange-2013-help.md)를 참조하십시오.

  - 필요에 따라 데이터베이스 전환을 수행합니다. 데이터베이스 전환을 수행하는 방법에 대한 자세한 단계는 [사서함 데이터베이스 복사본 활성화](activate-a-mailbox-database-copy-exchange-2013-help.md)를 참조하세요.

솔루션 관리에 대한 자세한 내용은 [고가용성 및 사이트 복구를 관리합니다.](managing-high-availability-and-site-resilience-exchange-2013-help.md)를 참조하십시오.

