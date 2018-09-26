---
title: '데이터베이스 가용성 그룹 관리: Exchange 2013 Help'
TOCTitle: 데이터베이스 가용성 그룹 관리
ms:assetid: 74be3f97-ec0f-4d2a-b5d8-7770cc489919
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298065(v=EXCHG.150)
ms:contentKeyID: 50483432
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 가용성 그룹 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-10-04_

DAG(데이터베이스 가용성 그룹)는 데이터베이스, 서버 또는 네트워크 오류에 대한 데이터베이스 수준의 자동 복구 기능을 제공하는 최대 16개의 Microsoft Exchange Server 2013 사서함 서버로 이루어진 집합입니다. DAG는 연속 복제 및 Windows 장애 조치(failover) 클러스터링 기술의 하위 집합을 사용하여 고가용성 및 사이트 복구를 제공합니다. DAG의 사서함 서버는 오류가 있는지 상호 모니터링합니다. 사서함 서버를 DAG에 추가하면 DAG의 다른 서버와 함께 작동하여 데이터베이스 오류로부터 데이터베이스 수준의 자동 복구 기능을 제공합니다.

DAG를 만든 경우 초기에는 비어 있습니다. DAG에 첫 번째 서버를 추가하는 경우 해당 DAG에 대한 장애 조치(failover) 클러스터가 자동으로 만들어집니다. 또한 서버에서 네트워크 또는 서버 오류를 모니터링하는 인프라가 시작됩니다. 그러면 장애 조치(failover) 클러스터 하트비트 메커니즘 및 클러스터 데이터베이스를 사용하여 데이터베이스 탑재 상태, 복제 상태, 마지막으로 탑재된 위치 등 신속하게 변경할 수 있는 DAG 관련 정보를 추적하고 관리합니다.

**목차**

Creating DAGs

DAG membership

Configuring DAG properties

DAG networks

Configuring DAG members

Performing maintenance on DAG members

Shutting down DAG members

Installing updates on DAG members

## DAG 만들기

EAC(Exchange 관리 센터)에서 새 데이터베이스 사용 가능 그룹 마법사를 사용하거나, Exchange 관리 셸에서 **New-DatabaseAvailabilityGroup** cmdlet을 실행하여 DAG를 만들 수 있습니다. DAG를 만들 경우 DAG에 이름을 지정하고, 선택적으로 미러링 모니터 서버 및 감시 디렉터리 설정을 지정합니다. 또한 고정 IP 주소를 사용하거나, DAG에서 DHCP(Dynamic Host Configuration Protocol)를 통해 필요한 IP 주소를 자동으로 할당하도록 하여 DAG에 IP 주소를 하나 이상 할당할 수 있습니다. *DatabaseAvailabilityGroupIpAddresses* 매개 변수를 사용하여 DAG에 IP 주소를 수동으로 할당할 수 있습니다. 이 매개 변수를 생략하면 DAG는 네트워크에서 DHCP 서버를 사용하여 IP 주소를 가져옵니다.

Windows Server 2012 R2를 실행하는 사서함 서버가 포함된 DAG를 만드는 경우 관리 액세스 포인트가 없는 DAG를 만들 수 있는 옵션도 제공됩니다. 이 경우 Active Directory에서 클러스터에는 CNO(클러스터 이름 개체)가 없으며 클러스터 핵심 리소스 그룹에는 네트워크 이름 리소스 또는 IP 주소 리소스가 포함되지 않습니다.

DAG를 만드는 방법에 대한 자세한 단계는 [데이터베이스 가용성 그룹 만들기](create-a-database-availability-group-exchange-2013-help.md)를 참조하십시오.

DAG를 만드는 경우 Active Directory에 지정된 이름으로 DAG를 나타내는 빈 개체와 **msExchMDBAvailabilityGroup**의 개체 클래스가 만들어집니다.

DAG는 데이터베이스가 활성 상태와 수동 상태 간에 변경되거나 탑재 상태와 분리 상태 간에 변경되는 경우와 같이 빠르게 변경될 수 있는 데이터를 저장하기 위해 클러스터 하트비트, 클러스터 네트워크 및 클러스터 데이터베이스와 같은 Windows 장애 조치(failover) 클러스터링의 일부 기술을 사용합니다. DAG는 Windows 장애 조치(failover) 클러스터링을 사용하므로 Exchange 2013 R2 Enterprise 또는 Datacenter 운영 체제, Windows Server 2012 Standard 또는 Datacenter 운영 체제 또는 Windows Server 2012 R2 Standard 또는 Datacenter 운영 체제를 실행하는 Windows Server 2008 사서함 서버에서만 DAG를 만들 수 있습니다.


> [!NOTE]  
> DAG에서 만들어 사용하는 장애 조치(failover) 클러스터는 해당 DAG 전용으로 사용해야 합니다. 해당 클러스터를 기타 고가용성 솔루션이나 다른 용도로 사용할 수 없습니다. 예를 들어, 장애 조치(failover) 클러스터를 다른 응용 프로그램이나 서비스를 클러스터링하는 데 사용할 수 없습니다. DAG 이외의 목적으로 DAG의 기본 장애 조치(failover) 클러스터를 사용하는 것은 지원되지 않습니다.



## DAG 미러링 모니터 서버 및 감시 디렉터리

DAG를 만들 경우 Active Directory 포리스트 내에서 고유한 DAG 이름을 최대 15자로 지정해야 합니다. 또한 각 DAG는 미러링 모니터 서버 및 감시 디렉터리로 구성됩니다. 미러링 모니터 서버와 해당 디렉터리는 DAG의 구성원 수가 짝수이고 쿼럼의 경우에만 사용됩니다. 감시 디렉터리를 미리 만들 필요는 없습니다. Exchange는 미러링 모니터 서버에서 사용자에게 필요한 디렉터리를 자동으로 만들고 보안합니다. DAG 미러링 모니터 서버를 제외한 다른 목적으로 디렉터리를 사용하면 안 됩니다.

미러링 모니터 서버에 대한 요구 사항은 다음과 같습니다.

  - 미러링 모니터 서버는 DAG의 구성원일 수 없습니다.

  - 미러링 모니터 서버는 DAG와 동일한 Active Directory 포리스트에 있어야 합니다.

  - 미러링 모니터 서버는 지원 되는 버전의 Windows Server를 실행 합니다. 자세한 내용은 [Exchange 2013 시스템 요구 사항](exchange-2013-system-requirements-exchange-2013-help.md)을 참조 하십시오.

  - 서버 하나가 여러 DAG에 대한 미러링 모니터 서버로 작동할 수 있지만 각 DAG에 해당 감시 디렉터리가 필요합니다.

미러링 모니터 서버로 사용되는 서버가 무엇인지에 상관없이, 의도한 미러링 모니터 서버에서 Windows 방화벽이 활성화된 경우 파일 및 프린터 공유에 대해 Windows 방화벽 예외를 활성화해야 합니다.


> [!IMPORTANT]   
> 지정한 미러링 모니터 서버는 Exchange 2013 또는 Exchange 2010 서버 없으면 Exchange 신뢰할 수 있는 하위 시스템 유니버설 보안 그룹 (USG) DAG를 만들기 전에 미러링 모니터 서버에서 로컬 Administrators 그룹에 추가 해야 합니다. 이러한 보안 권한을 해당 Exchange 수 있는 디렉터리를 만들고 필요에 따라 미러링 모니터 서버에서 공유할 수 있도록 필요 합니다.<BR>미러링 모니터 서버는 SMB 포트 445를 사용합니다.



미러링 모니터 서버 또는 감시 디렉터리는 모두 내결함성을 갖출 필요가 없으며 중복성 또는 고가용성 형식을 사용하지 않아도 됩니다. 미러링 모니터 서버의 경우 클러스터된 파일 서버와 기타 복구 양식을 사용하지 않아도 됩니다. 여기에는 다양한 원인이 있습니다. DAG 규모가 큰 경우(예: 6명 이상) 오류가 여러 개 있어야 미러링 모니터 서버가 필요합니다. 구성원이 6명인 DAG는 쿼럼을 손실하지 않고 최대 2개의 Voter 오류를 감당할 수 있으므로 3 Voter가 실패하면 미러링 모니터 서버가 쿼럼을 유지 관리해야 합니다. 또한 현재 미러링 모니터 서버에 영향을 미치는 오류가 발생하는 경우(예: 하드웨어 오류로 인해 미러링 모니터 서버 손실) [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ko-kr/library/dd297934\(v=exchg.150\)) cmdlet을 사용하여 쿼럼이 있는 경우 새 미러링 모니터 서버와 감시 디렉터리를 구성합니다.


> [!NOTE]   
> 미러링 모니터 서버에서 저장소가 손실되었거나 사용자가 감시 디렉터리 또는 공유 권한을 변경한 경우 <STRONG>Set-DatabaseAvailabilityGroup</STRONG> cmdlet을 사용하여 원래 위치에 미러링 모니터 서버와 감시 디렉터리를 구성할 수도 있습니다.



## 미러링 모니터 서버 배치 고려 사항

DAG의 미러링 모니터 서버 배치 비즈니스 요구 사항을 파악 하 고 조직에 사용할 수 있는 옵션에 따라 달라 집니다. Exchange 2013 권장 또는 Exchange 의 이전 버전에서 지원 하지 않는 되지 않은 새 DAG 구성 옵션에 대 한 지원을 포함 됩니다. 이러한 옵션 세번째 데이터 센터, 지사, 또는 Microsoft Azure 가상 네트워크와 같은 세 위치를 사용 하 여 포함 됩니다.

다음 표에는 다양한 배포 시나리오에 대한 일반적인 미러링 모니터 서버 배치 권장 사항이 나열되어 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>배포 시나리오</th>
<th>권장 사항</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>단일 데이터 센터에 배포된 단일 DAG</p></td>
<td><p>DAG 구성원과 동일한 데이터 센터에 미러링 모니터 서버 찾기</p></td>
</tr>
<tr class="even">
<td><p>두 데이터 센터에 배포된 단일 DAG(추가 위치 사용 불가능)</p></td>
<td><p>자동 데이터 센터 장애 조치를 사용 하도록 설정 하려면 Microsoft Azure 가상 네트워크에서 미러링 모니터 서버 찾기 또는</p>
<p>기본 데이터 센터에 미러링 모니터 서버 찾기</p></td>
</tr>
<tr class="odd">
<td><p>단일 데이터 센터에 배포된 여러 DAG</p></td>
<td><p>DAG 구성원과 동일한 데이터 센터에서 미러링 모니터 서버 찾기. 추가 옵션:</p>
<ul>
<li><p>여러 DAG에 동일한 미러링 모니터 서버 사용</p></li>
<li><p>다른 DAG에 하나의 미러링 모니터 서버 역할을 하는 한 개의 DAG 구성원 사용</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>두 데이터 센터에 배포된 여러 DAG</p></td>
<td><p>자동 데이터 센터 장애 조치를 사용 하도록 설정 하려면 Microsoft Azure 가상 네트워크에서 미러링 모니터 서버 찾기 또는</p>
<p>각 DAG에 대해 기본으로 간주되는 데이터 센터에서 미러링 모니터 서버 찾기. 추가 옵션:</p>
<ul>
<li><p>여러 DAG에 동일한 미러링 모니터 서버 사용</p></li>
<li><p>다른 DAG에 하나의 미러링 모니터 서버 역할을 하는 한 개의 DAG 구성원 사용</p>
<p></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>셋 이상의 데이터 센터에 배포된 단일 또는 여러 DAG</p></td>
<td><p>이 구성에서 미러링 모니터 서버는 쿼럼 응답의 대부분이 있기를 원하는 데이터 센터에 배치해야 함</p></td>
</tr>
</tbody>
</table>


두 데이터 센터 DAG를 배포 하는 경우 미러링 모니터 서버를 호스트 하는 것에 대 한 세번째 위치를 사용 하 Exchange 2013 에서 새로운 구성 옵션이입니다. 조직에 DAG 배포 된 두 데이터 센터에는 영향을 주는 네트워크 오류 로부터 격리 된 네트워크 인프라 세번째 위치 경우 구성 함으로써 DAG의 미러링 모니터 서버, 세번째 해당 위치에 배포할 수 프로그램 자동 장애 조치는 기능 DAG 데이터 센터 수준 오류 이벤트에 대 한 응답으로 다른 데이터 센터에 데이터베이스. 조직에는 두 실제 위치에 있는 경우에 미러링 모니터 서버를 배치 하려면 세번째 위치로 Microsoft Azure 가상 네트워크를 사용할 수 있습니다.

## DAG를 만드는 동안 미러링 모니터 서버 및 감시 디렉터리 지정

DAG를 만들 경우 DAG의 이름을 지정해야 합니다. 선택적으로 미러링 모니터 서버와 디렉터리를 지정할 수도 있습니다.

DAG를 만들 경우 다음과 같은 옵션 및 동작의 조합을 사용할 수 있습니다.

  - DAG의 이름만 지정하고 **미러링 모니터 서버**와 **감시 디렉터리** 필드를 비워 둡니다. 이 시나리오에서 마법사는 로컬 Active Directory 사이트에서 사서함 서버가 설치되어 있지 않은 클라이언트 액세스 서버를 검색하고, 해당 서버에 기본 디렉터리(%SystemDrive%:\\DAGFileShareWitnesses\\\<*DAGFQDN*\>) 및 기본 공유(\<*DAGFQDN*\>)를 자동으로 만들며, 이 클라이언트 액세스 서버를 미러링 모니터 서버로 사용합니다. 예를 들면 C 드라이브에 운영 체제가 설치되어 있는 미러링 모니터 서버 CAS3이 있다고 가정합니다. contoso.com 도메인의 DAG1이라는 DAG는 \\\\CAS3\\DAG1.contoso.com으로 공유되는 C:\\DAGFileShareWitnesses\\DAG1.contoso.com의 기본 감시 디렉터리를 사용하게 됩니다.

  - 미러링 모니터 서버에 만들고 공유할 디렉터리, 사용할 미러링 모니터 서버 및 DAG의 이름을 지정할 수 있습니다.

  - DAG의 이름을 지정하고 사용할 미러링 모니터 서버를 지정하고 **감시 디렉터리** 필드를 비워 둡니다. 이 시나리오에서 마법사는 지정된 미러링 모니터 서버에 기본 디렉터리를 만듭니다.

  - DAG의 이름을 지정하고, **미러링 모니터 서버** 필드를 비워 두고, 미러링 모니터 서버에서 만들고 공유할 디렉터리를 지정할 수 있습니다. 이 시나리오에서 마법사는 사서함 서버 역할이 설치되지 않은 클라이언트 액세스 서버를 검색하고, 해당 서버에 지정된 DAG를 자동으로 만들고 해당 디렉터리를 공유하며, 이 클라이언트 액세스 서버를 미러링 모니터 서버로 사용합니다.

DAG가 구성되면 처음에는 노드 과반수 쿼럼 모델이 사용됩니다. 두 번째 사서함 서버가 DAG에 추가되면 쿼럼은 자동으로 노드 및 파일 공유 과반수 쿼럼 모델로 변경됩니다. 이러한 변경이 발생하면 DAG의 클러스터는 쿼럼을 유지 관리하기 위해 미러링 모니터 서버를 사용하기 시작합니다. 감시 디렉터리가 없는 경우 Exchange에서 자동으로 감시 디렉터리를 만들고, 공유하고, 이 공유에 DAG CNO 컴퓨터 계정에 대한 모든 권한을 프로비전합니다.


> [!NOTE]  
> DFS(분산 파일 시스템) 네임스페이스의 일부인 파일 공유는 사용할 수 없습니다.

DAG가 만들어지기 전에 Windows 방화벽이 미러링 모니터 서버에서 활성화되면 DAG의 생성을 방해할 수 있습니다. Exchange는 Windows WMI(Windows Management Instrumentation)를 사용하여 미러링 모니터 서버에 디렉터리 및 파일 공유를 만듭니다. Windows 방화벽이 미러링 모니터 서버에서 활성화되고 WMI에 방화벽 예외가 구성되어 있지 않으면 **New-DatabaseAvailabilityGroup** cmdlet은 오류로 인해 실패합니다. 미러링 모니터 서버를 지정할 때 감시 디렉터리를 지정하지 않을 경우 다음 오류 메시지를 수신합니다.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>서버 &lt;<em>Server Name</em>&gt;에 기본 감시 디렉터리를 만들지 못했습니다. 감시 디렉터리를 수동으로 지정하십시오.</p></td>
</tr>
</tbody>
</table>


미러링 모니터 서버와 감시 디렉터리를 지정할 경우 다음 경고 메시지가 표시됩니다.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>미러링 모니터 서버 '<em>ServerName</em>'의 파일 공유에 액세스할 수 없습니다. 이 문제가 해결될 때까지 데이터베이스 가용성 그룹에서 오류 발생이 증가할 수 있습니다. DatabaseAvailabilityGroup cmdlet을 사용하여 작업을 다시 시도할 수 있습니다. 오류: 네트워크 경로를 찾지 못했습니다.</p></td>
</tr>
</tbody>
</table>


DAG가 만들어진 후 서버가 추가되기 전에 미러링 모니터 서버에서 Windows 방화벽이 활성화되면 DAG 구성원의 추가나 제거를 방해할 수 있습니다. Windows 방화벽이 미러링 모니터 서버에서 활성화되고 WMI에 방화벽 예외가 구성되어 있지 않으면 **Add-DatabaseAvailabilityGroupServer** cmdlet은 다음 경고 메시지를 표시합니다.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>미러링 모니터 서버 '<em>'ServerName'</em>에 파일 공유 감시 디렉터리 'C:\DAGFileShareWitnesses\DAG_FQDN'을 만들지 못했습니다. 이 문제가 해결될 때까지 데이터베이스 가용성 그룹에서 오류 발생이 증가할 수 있습니다. DatabaseAvailabilityGroup cmdlet을 사용하여 작업을 다시 시도할 수 있습니다. 오류: 서버 <em>'ServerName'</em>에서 WMI 예외가 발생했습니다. RPC 서버를 사용할 수 없습니다. (HRESULT: 0x800706BA의 예외).</p></td>
</tr>
</tbody>
</table>


위 오류와 경고를 해결하려면 다음 중 하나를 수행합니다.

  - 미러링 모니터 서버에 감시 디렉터리를 수동으로 생성하여 공유하고 해당 디렉터리 및 공유의 DAG 모든 권한에 대해 CNO를 지정합니다.

  - Windows 방화벽에서 WMI 예외를 허용하도록 설정합니다.

  - Windows 방화벽을 사용하지 않도록 설정합니다.

맨 위로 이동

## DAG 구성원

DAG를 만들고 난 후 EAC에서 데이터베이스 가용성 그룹 관리 마법사를 사용하거나, 셸에서 **Add-DatabaseAvailabilityGroupServer** 또는 **Remove-DatabaseAvailabilityGroupServer** cmdlet을 사용하여 서버를 DAG 서버에 추가하거나 DAG 서버에서 제거할 수 있습니다. DAG 구성원을 관리하는 방법에 대한 자세한 단계는 [데이터베이스 가용성 그룹 구성원 관리](manage-database-availability-group-membership-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]  
> DAG의 구성원인 각 사서함 서버는 DAG에 사용되는 기본 클러스터의 노드이기도 합니다. 그 결과로 사서함 서버는 한 번에 한 개의 DAG 구성원일 수 있습니다.



DAG에 추가할 사서함 서버에 장애 조치(failover) 클러스터링 구성 요소가 설치되어 있지 않은 경우 서버를 추가하기 위해 사용되는 방법(예: **Add-DatabaseAvailabilityGroupServer** cmdlet 또는 데이터베이스 가용성 그룹 관리 마법사)을 통해 장애 조치(failover) 클러스터링 기능이 설치됩니다.

첫 번째 사서함 서버가 DAG에 추가되면 다음이 발생합니다.

  - Windows 장애 조치(failover) 클러스터링 구성 요소가 아직 설치되지 않았으면 설치됩니다.

  - 장애 조치(failover) 클러스터가 DAG 이름을 사용하여 만들어집니다. 이 장애 조치(failover)는 DAG에서 단독으로 사용되며 해당 클러스터는 DAG에 전용으로 사용되어야 합니다. 기타 다른 목적을 위해 클러스터를 사용하는 것은 지원되지 않습니다.

  - CNO는 기본 컴퓨터 컨테이너에서 만들어집니다.

  - DAG의 이름 및 IP 주소가 DNS(Domain Name System)의 호스트 (A) 레코드로 등록됩니다.

  - Active Directory에서 서버가 DAG 개체에 추가됩니다.

  - 클러스터 데이터베이스가 추가된 서버에 탑재된 데이터베이스의 정보로 업데이트됩니다.

대규모 또는 다중 사이트 환경에서, 특히 DAG가 다중 Active Directory 사이트로 확장된 경우, 첫 번째 DAG 구성원을 포함하는 DAG 개체의 Active Directory 복제가 완료될 때까지 기다려야 합니다. 이 Active Directory 개체가 환경 전체에 복제되지 않은 채로 두 번째 서버를 추가하면 DAG에 대한 새 클러스터(및 새 CNO)가 만들어집니다. 이는 두 번째 구성원이 추가되는 관점에서 DAG 개체가 비어 있는 것으로 인식하기 때문에 결국 이들 개체가 이미 있다고 하더라도 **Add-DatabaseAvailabilityGroupServer** cmdlet에 의해 DAG에 대한 새 클러스터와 CNO가 만들어지는 것입니다. 첫 번째 DAG 서버를 포함하는 DAG 개체가 복제되었는지 알아보려면 추가되는 두 번째 서버에서 **Get-DatabaseAvailabilityGroup** cmdlet을 사용하여, 추가한 첫 번째 서버가 DAG의 구성원으로 표시되는지를 확인합니다.

두 번째 및 그 이후 서버가 DAG에 추가되면 다음이 발생합니다.

  - 서버가 DAG용 Windows 장애 조치(failover) 클러스터에 가입됩니다.

  - 쿼럼 모델이 자동으로 조정됩니다.
    
      - 구성원이 홀수인 DAG에 노드 과반수 쿼럼 모델이 사용됩니다.
    
      - 구성원이 짝수인 DAG에 노드 및 파일 공유 과반수 쿼럼 모델이 사용됩니다.

  - 감시 디렉터리 및 공유가 필요한 경우 Exchange에 의해 자동으로 만들어집니다.

  - Active Directory에서 서버가 DAG 개체에 추가됩니다.

  - 클러스터 데이터베이스가 탑재된 데이터베이스에 대한 정보로 업데이트됩니다.


> [!NOTE]
> 쿼럼 모델 변경은 자동으로 수행되어야 합니다. 하지만 쿼럼 모델이 적절한 모델로 자동 변경되지 않는 경우에는 <STRONG>Set-DatabaseAvailabilityGroup</STRONG> cmdlet에 <EM>Identity</EM> 매개 변수만 사용하여 DAG에 대한 쿼럼 설정을 수정하십시오.



## DAG에 대한 클러스터 이름 개체 미리 준비

CNO는 Active Directory에 만들어지고 클러스터의 이름 리소스와 연결되는 컴퓨터 계정입니다. 클러스터의 이름 리소스는 CNO에 연결되며, 클러스터의 ID로 동작하고 클러스터의 보안 컨텍스트를 제공하는 Kerberos 사용 가능 개체입니다. 첫 번째 구성원이 DAG에 추가될 때 DAG의 기본 클러스터 및 해당 클러스터에 대한 CNO 형성이 수행됩니다. 첫 번째 서버가 DAG에 추가되면 원격 Powershell은 추가 작업이 진행 중인 사서함 서버의 Microsoft Exchange 복제 서비스를 실행합니다. Microsoft Exchange 복제 서비스는 장애 조치(failover) 클러스터링 기능을 설치하고(아직 설치되지 않은 경우) 클러스터 생성 프로세스를 시작합니다. Microsoft Exchange 복제 서비스는 LOCAL SYSTEM 보안 컨텍스트에서 실행되며 이는 클러스터 생성이 수행되는 컨텍스트입니다.

> [!CAUTION]
> DAG 구성원이 Windows Server 2012를 실행 중인 경우에는 첫 번째 서버를 DAG에 추가하기 전에 CNO를 미리 준비해야 합니다. DAG 구성원이 Windows Server 2012 R2를 실행하는 경우 클러스터 관리 액세스 포인트가 없는 DAG를 만들면 CNO가 생성되지 않으며 DAG용 CNO를 만들 필요가 없습니다.


컴퓨터 계정 생성이 제한되는 환경이나 컴퓨터 계정이 기본 컴퓨터 컨테이너가 아닌 컨테이너에 만들어지는 환경에서는 CNO를 미리 준비하고 프로비전할 수 있습니다. CNO에 대한 컴퓨터 계정을 만들거나 사용하지 않도록 설정한 후 다음을 수행합니다.

  - DAG에 추가하려는 첫 번째 사서함 서버의 컴퓨터 계정에 대한 컴퓨터 계정의 모든 권한 할당

  - Exchange Trusted Subsystem USG에 대한 컴퓨터 계정의 모든 권한 할당

DAG에 추가 중인 첫 번째 사서함 서버의 컴퓨터 계정에 컴퓨터 계정에 대한 모든 권한을 할당하면 LOCAL SYSTEM 보안 컨텍스트가 미리 준비된 컴퓨터 계정을 관리할 수 있습니다. Exchange Trusted Subsystem USG에는 도메인에 있는 모든 Exchange 서버의 컴퓨터 계정을 포함하므로 Exchange Trusted Subsystem USG에 컴퓨터 계정에 대한 모든 권한을 할당하는 것으로 대신할 수 있습니다.

DAG에 대해 CNO를 미리 준비하고 프로비전하는 방법에 대한 자세한 내용은 [데이터베이스 가용성 그룹에 대한 클러스터 이름 개체 미리 준비](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)를 참조하십시오.

## DAG에서 서버 제거

EAC에서 데이터베이스 가용성 그룹 관리 마법사를 사용하거나, 셸에서 **Remove-DatabaseAvailabilityGroupServer** cmdlet을 사용하여 DAG에서 사서함 서버를 제거할 수 있습니다. DAG에서 사서함 서버를 제거하려면 먼저 복제된 모든 사서함 데이터베이스를 서버에서 제거해야 합니다. 복제된 사서함 데이터베이스가 포함된 사서함 서버를 DAG에서 제거하려면 작업이 실패합니다.

특정 작업을 수행하기 전에는 사서함 서버를 DAG에서 제거해야 한다는 시나리오가 있습니다. 이러한 시나리오는 다음과 같습니다.

  - **서버 복구 작업 수행**   DAG의 구성원인 사서함 서버가 손실되었거나, 그렇지 않고 오류가 발생하고 복구할 수 없어 교체가 필요한 경우 **Setup /m:RecoverServer** 스위치를 사용하여 서버 복구 작업을 수행할 수 있습니다. 하지만 복구 작업을 수행하려면 먼저 [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ko-kr/library/dd297956\(v=exchg.150\)) cmdlet을 *ConfigurationOnly* 매개 변수와 함께 사용하여 DAG에서 서버를 제거해야 합니다.

  - **데이터베이스 가용성 그룹 제거**   DAG를 제거해야 할 상황(예: 타사 복제 모드를 사용하지 않도록 설정하는 경우)이 발생할 수도 있습니다. DAG를 제거해야 하는 경우 먼저 DAG에서 모든 서버를 제거해야 합니다. 구성원이 포함된 DAG를 제거하면 작업이 실패합니다.

맨 위로 이동

## DAG 속성 구성

DAG에 서버를 추가한 후 EAC 또는 셸을 사용하여 DAG에서 사용하는 미러링 모니터 서버와 감시 디렉터리 및 DAG에 할당되는 IP주소를 비롯한 DAG의 속성을 구성할 수 있습니다.

구성 가능한 속성은 다음과 같습니다.

  - **미러링 모니터 서버**   파일 공유 감시를 위해 파일 공유를 호스트할 서버 이름입니다. 미러링 모니터 서버로 클라이언트 액세스 서버를 지정하는 것이 좋습니다. 이렇게 하면 시스템이 필요에 따라 자동으로 공유를 구성, 보안 및 사용할 수 있으며 메시징 관리자가 미러링 모니터 서버의 가용성을 알 수 있습니다.

  - **감시 디렉터리**   파일 공유 감시 데이터를 저장하는 데 사용되는 디렉터리의 이름입니다. 이 디렉터리는 지정된 미러링 모니터 서버에서 시스템에 의해 자동으로 만들어집니다.

  - **데이터베이스 가용성 그룹 IP 주소**   DAG 구성원이 Windows Server 2012 R2를 실행할 때 IP 주소 없는 DAG를 만드는 경우를 제외하고는 DAG에 하나 이상의 IP 주소를 할당해야 합니다. 그렇지 않으면 DAG의 IP 주소는 수동으로 할당된 고정 IP 주소를 사용하여 구성되거나, 조직의 DHCP 서버를 사용하여 DAG에 자동으로 할당될 수 있습니다.

셸을 사용하면 DAG IP 주소, 네트워크 암호화 및 압축 설정, 네트워크 검색, 복제에 사용되는 TCP 포트, 대체 미러링 모니터 서버 및 감시 디렉터리 설정 등 EAC에서 사용할 수 없는 DAG 속성을 구성하고 데이터 센터 활성화 조정 모드를 사용하도록 설정할 수 있습니다.

DAG 속성을 구성하는 방법에 대한 자세한 단계는 [데이터베이스 가용성 그룹 속성 구성](configure-database-availability-group-properties-exchange-2013-help.md)을 참조하십시오.

## DAG 네트워크 암호화

Dag은 Windows Server 운영 체제의 암호화 기능을 활용 하 여 암호화 사용을 지원 합니다. Dag은 Exchange 서버 간에 Kerberos 인증을 사용 합니다. Microsoft Kerberos 보안 지원 공급자 (SSP) EncryptMessage 및 DecryptMessage Api에 대 한 핸들 암호화 DAG 네트워크 트래픽입니다. Microsoft Kerberos SSP 여러 암호화 알고리즘을 지원 합니다. (전체 목록은 "암호화 유형의" [Kerberos 프로토콜 확장](https://go.microsoft.com/fwlink/p/?linkid=179131)3.1.5.2, 섹션을 참조). 목록에서 지원 되는 가장 강력한 암호화 프로토콜을 선택 하는 Kerberos 인증 핸드셰이크: 일반적으로 암호화 표준 AES (고급) 256 비트 잠재적으로와 s h A 해시 기반 메시지 인증 코드 HMAC ()의 무결성을 유지 하는 데이터입니다. 자세한 내용은 [HMAC](https://en.wikipedia.org/wiki/hmac)를 참조 하십시오.

네트워크 암호화는 DAG 네트워크가 아닌 DAG의 속성입니다. DAG 네트워크 암호화는 셸에서 **Set-DatabaseAvailabilityGroup** cmdlet을 사용하여 구성할 수 있습니다. 다음 표에서는 DAG 네트워크 통신용으로 가능한 암호화 설정을 보여 줍니다.

### DAG 네트워크 통신 암호화 설정

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>설정</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>사용 안 함</p></td>
<td><p>네트워크 암호화가 사용되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>사용</p></td>
<td><p>모든 DAG 네트워크에서 네트워크 암호화가 복제 및 시드용으로 사용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>여러 서브넷에서 복제 시 DAG 네트워크에서 네트워크 암호화가 사용됩니다. 기본 설정입니다.</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>모든 DAG 네트워크에서 네트워크 암호화가 시드용으로만 사용됩니다.</p></td>
</tr>
</tbody>
</table>


## DAG 네트워크 압축

Dag 기본 제공 압축을 지원 합니다. 압축을 사용 하는 경우 Microsoft를 구현 하는 LZ77 알고리즘은, XPRESS DAG 네트워크 통신에 사용 합니다. 자세한 내용은 [설명은 줄이기 알고리즘](http://www.zlib.net/feldspar.html) 및 섹션을 참조 3.1.4.11.1.2.1 [와이어 형식 프로토콜 사양](https://go.microsoft.com/fwlink/p/?linkid=179133)의 "압축 알고리즘 LZ77" 합니다. 이 특히 대부분의 Microsoft 프로토콜에 사용 되는 압축, Microsoft Outlook 와 Exchange 사이의 MAPI RPC 압축의 동일한 형식입니다.

네트워크 암호화와 마찬가지로 네트워크 압축은 DAG 네트워크가 아닌 DAG의 속성입니다. DAG 네트워크 압축은 셸에서 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ko-kr/library/dd297934\(v=exchg.150\)) cmdlet을 사용하여 구성합니다. 다음 표에서는 DAG 네트워크 통신용으로 가능한 압축 설정을 보여 줍니다.

### DAG 네트워크 통신 압축 설정

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>설정</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>사용 안 함</p></td>
<td><p>네트워크 압축이 사용되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>사용</p></td>
<td><p>모든 DAG 네트워크에서 네트워크 압축이 복제 및 시드용으로 사용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>여러 서브넷에서 복제 시 DAG 네트워크에서 네트워크 압축이 사용됩니다. 기본 설정입니다.</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>모든 DAG 네트워크에서 네트워크 압축이 시드용으로만 사용됩니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## DAG 네트워크

DAG 네트워크에 복제 트래픽을 또는 MAPI 트래픽에 사용 되는 하나 이상의 서브넷의 컬렉션입니다. 각 DAG MAPI 네트워크의 최대 숫자와 0 개 이상의 복제 네트워크를 포함 합니다.

## 단일 네트워크 어댑터 구성

단일 네트워크 어댑터 구성에서 동일한 네트워크는 MAPI 및 복제 트래픽 모두에 사용 됩니다. 복잡성을 줄이기위해 단일 네트워크 어댑터 이므로 Exchange 서버에 대 한 권장 되는 구성 MAPI 및 복제 트래픽 모두 동일한 네트워크에 있는 하 게 확인 하는 것입니다.

## 이중 네트워크 어댑터 구성

일반적으로 증가 네트워크 트래픽을 단일 네트워크 어댑터를 완전히 포화 가능성이 갖는 이중 네트워크 어댑터를 사용 하기만 하면 됩니다.

이중 네트워크 어댑터 구성에서는 하나의 네트워크는 일반적으로 전용 복제 트래픽을입니다 하 고 다른 네트워크 MAPI 트래픽에 대 한 주로 사용 됩니다. 각 DAG 구성원에 게 네트워크 어댑터를 추가 하 고 복제 네트워크로 추가 DAG 네트워크를 구성할 수도 있습니다.


> [!NOTE]
> 복제 네트워크를 여러 개 사용할 때 우선 사용되도록 네트워크 순위를 지정할 수 있는 방법은 없습니다. Exchange는 복제 네트워크 그룹에서 로그를 전달하는 데 사용할 복제 네트워크를 임의로 선택합니다.



Exchange 2010에서는 많은 시나리오에서 DAG 네트워크를 수동으로 구성해야 했습니다. Exchange 2013에서는 기본적으로 DAG 네트워크가 시스템에 의해 자동으로 구성됩니다. DAG 네트워크를 만들거나 수정하려면 먼저 다음 명령을 실행하여 수동 DAG 네트워크 제어를 사용하도록 설정해야 합니다.

```powershell
Set-DatabaseAvailabilityGroup <DAGName> -ManualDagNetworkConfiguration $true
```

수동 DAG 네트워크 구성을 설정한 후 셸에서 **New-DatabaseAvailabilityGroupNetwork** cmdlet을 사용하여 DAG 네트워크를 만들 수 있습니다. DAG 네트워크를 만드는 방법에 대한 자세한 단계는 [데이터베이스 가용성 그룹 네트워크를 만들기](create-a-database-availability-group-network-exchange-2013-help.md)를 참조하십시오.

셸에서 **Set-DatabaseAvailabilityGroupNetwork** cmdlet을 사용하여 DAG 네트워크 속성을 구성할 수 있습니다. DAG 네트워크 속성을 구성하는 방법에 대한 자세한 단계는 [데이터베이스 가용성 그룹 네트워크 속성 구성](configure-database-availability-group-network-properties-exchange-2013-help.md)을 참조하십시오. 각 DAG 네트워크에서는 다음 필수 매개 변수 및 선택적 매개 변수를 구성해야 합니다.

  - **네트워크 이름**   DAG 네트워크의 고유한 이름으로 최대 128자입니다.

  - **네트워크 설명**   DAG 네트워크 선택적 설명으로 최대 256자입니다.

  - **네트워크 서브넷**   *IPAddress/Bitmask* 형식을 사용하여 입력하는 하나 이상의 서브넷입니다(예: IPv4(Internet Protocol version 4) 서브넷의 경우 192.168.1.0/24, IPv6(Internet Protocol version 6) 서브넷의 경우 2001:DB8:0:C000::/64).

  - **복제 사용**   EAC에서 DAG 네트워크를 복제 트래픽 전용으로 사용하고 MAPI 트래픽을 차단하려면 이 확인란을 선택합니다. 복제에 DAG 네트워크를 사용할 수 없도록 하고 MAPI 트래픽을 사용하도록 설정하려면 이 확인란의 선택을 취소합니다. 셸에서 복제 사용 여부를 설정하려면 [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd298008\(v=exchg.150\)) cmdlet의 *ReplicationEnabled* 매개 변수를 사용합니다.


> [!NOTE]
> MAPI 네트워크에서 복제를 사용하지 않도록 설정하더라도 시스템이 복제를 위해 MAPI 네트워크를 사용하지 않음을 보장하지 않습니다. 구성된 모든 복제 네트워크가 오프라인 또는 장애가 있거나 그렇지 않다면 이용할 수 없어서 MAPI 네트워크만이 존재하는 경우(복제에 대해 사용 안 함으로 구성됨), 해당 시스템은 복제를 위해 MAPI 네트워크를 사용합니다.



시스템이 만든 초기 DAG 네트워크(예: MapiDagNetwork 및 ReplicationDagNetwork01)는 클러스터 서비스에서 열거한 서브넷을 기반으로 합니다. 각 DAG 구성원의 네트워크 어댑터 수는 동일해야 하며 각 네트워크 어댑터는 고유한 서브넷에서 IPv4 주소(IPv6 주소는 선택적임)를 가져야만 합니다. 여러 DAG 구성원이 동일한 서브넷에서 IPv4 주소를 가질 수 있지만 특정 DAG 구성원의 각 네트워크 어댑터와 IP 주소 쌍은 고유한 서브넷상에 존재해야 합니다. 또한 MAPI 네트워크를 위해서 사용하는 어댑터만 기본 게이트웨이를 사용하여 구성해야 합니다. 복제 네트워크는 기본 게이트웨이를 사용하여 구성하면 안 됩니다.

예를 들어, 두 명의 구성원이 있고 각 구성원은 두 개의 네트워크 어댑터(하나는 MAPI 네트워크 전용, 다른 하나는 복제 네트워크 전용)를 가지는 DAG인 DAG1이 있다고 간주합니다. 다음 표는 IP 주소 구성 설정 예입니다.

### 네트워크 어댑터 설정 예

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>서버-네트워크 어댑터</th>
<th>IP 주소/서브넷 마스크</th>
<th>기본 게이트웨이</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.1.15/24</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX1-복제</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.16</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2-복제</p></td>
<td><p>10.0.0.16</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


다음 구성에는 두 개의 서브넷, 192.168.1.0 및 10.0.0.0이 DAG에 구성되어 있습니다. EX1 및 EX2가 DAG에 추가되는 경우 두 개의 서브넷이 열거되고 두 개의 DAG 네트워크, MapiDagNetwork(192.168.1.0) 및 ReplicationDagNetwork01(10.0.0.0)이 만들어집니다. 이러한 네트워크는 다음 표에 표시된 대로 구성됩니다.

### 단일-서브넷 DAG에 대해 열거되는 DAG 네트워크 설정

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>이름</th>
<th>서브넷</th>
<th>인터페이스</th>
<th>MAPI 액세스 사용</th>
<th>복제 사용</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.1.0/24</p></td>
<td><p>EX1(192.168.1.15)</p>
<p>EX2(192.168.1.16)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p></td>
<td><p>EX1(10.0.0.15)</p>
<p>EX2(10.0.0.16)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


ReplicationDagNetwork01을 전용 복제 네트워크로 구성을 완료하려면 다음 명령을 실행하여 MapiDagNetwork에 대한 복제를 사용하지 않도록 설정합니다.

```powershell
Set-DatabaseAvailabilityGroupNetwork -Identity DAG1\MapiDagNetwork -ReplicationEnabled:$false
```

MapiDagNetwork에 대해 복제를 사용하지 않도록 설정하면 Microsoft Exchange 복제 서비스는 연속 복제를 위해 ReplicationDagNetwork01을 사용합니다. ReplicationDagNetwork01에 장애가 발생하는 경우 Microsoft Exchange 복제 서비스는 연속 복제를 위해 MapiDagNetwork를 다시 사용합니다. 시스템은 고가용성을 유지하기 위해 의도적으로 이를 수행합니다.

## DAG 네트워크 및 다중 서브넷 배포

이전 예제에서는 DAG가 사용하는 두 개의 다른 서브넷(192.168.1.0 및 10.0.0.0)이 존재해도 각 구성원이 MAPI 네트워크를 형성하기 위해 동일한 서브넷을 사용하므로 DAG는 단일-서브넷 DAG로 간주됩니다. DAG 구성원이 MAPI 네트워크를 위해 다른 서브넷을 사용하는 경우 DAG는 *다중-서브넷 DAG*로 간주됩니다. 다중 서브넷 DAG에서는 적절한 서브넷이 각 DAG 네트워크에 자동으로 연결됩니다.

예를 들어, 두 개의 구성원이 있고 각 구성원은 두 개의 네트워크 어댑터(하나는 MAPI 네트워크 전용, 다른 하나는 복제 네트워크 전용)를 갖고 있으며, 각 DAG 구성원이 별도의 Active Directory 사이트에 위치해 있고 다른 서브넷상에 해당 MAPI 네트워크가 있는 DAG2가 있다고 간주합니다. 다음 표는 IP 주소 구성 설정 예입니다.

### 다중-서브넷 DAG에 대한 네트워크 어댑터 설정 예

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>서버-네트워크 어댑터</th>
<th>IP 주소/서브넷 마스크</th>
<th>기본 게이트웨이</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.0.15/24</p></td>
<td><p>192.168.0.1</p></td>
</tr>
<tr class="even">
<td><p>EX1-복제</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.15</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2-복제</p></td>
<td><p>10.0.1.15</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


다음 구성에는 네 개의 서브넷, 192.168.0.0, 192.168.1.0, 10.0.0.0 및 10.0.1.0이 DAG에 구성되어 있습니다. DAG에 EX1 및 EX2가 추가되는 경우 네 개의 서브넷이 열거되지만 두 개의 DAG 네트워크인 MapiDagNetwork(192.168.0.0, 192.168.1.0) 및 ReplicationDagNetwork01(10.0.0.0, 10.0.1.0)만 만들어집니다. 이러한 네트워크는 다음 표에 표시된 대로 구성됩니다.

### 다중-서브넷 DAG에 대해 열거되는 DAG 네트워크 설정

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>이름</th>
<th>서브넷</th>
<th>인터페이스</th>
<th>MAPI 액세스 사용</th>
<th>복제 사용</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.0.0/24</p>
<p>192.168.1.0/24</p></td>
<td><p>EX1(192.168.0.15)</p>
<p>EX2(192.168.1.15)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p>
<p>10.0.1.0/24</p></td>
<td><p>EX1(10.0.0.15)</p>
<p>EX2(10.0.1.15)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


## DAG 네트워크 및 iSCSI 네트워크

기본적으로 DAG는 기본 클러스터에서 사용하기 위해 감지되고 구성된 모든 네트워크의 검색을 수행합니다. 이 네트워크에는 하나 이상의 DAG 구성원에 대한 iSCSI(인터넷 SCSI) 저장소 사용의 결과로 사용 중인 iSCSI 네트워크가 포함되어 있습니다. 최적의 방법으로 iSCSI 저장소는 전용 네트워크 및 네트워크 어댑터를 사용해야 합니다. 이러한 네트워크는 DAG 또는 클러스터에서 관리되지 않고 DAG 네트워크(MAPI 또는 복제)로 사용되지 않아야 합니다. 대신 이러한 네트워크를 DAG에서 사용하지 않도록 수동으로 설정하여 iSCSI 저장소 트래픽 전용으로 설정할 수 있습니다. iSCSI 네트워크가 DAG 네트워크로 감지되고 사용되지 않도록 설정하려면 다음 예외 같이 [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd298008\(v=exchg.150\)) cmdlet을 사용하여 DAG가 현재 감지되는 iSCSI 네트워크를 무시하도록 구성합니다.

```powershell
Set-DatabaseAvailabilityGroupNetwork -Identity DAG2\DAGNetwork02 -ReplicationEnabled:$false -IgnoreNetwork:$true
```

또한 이 명령은 클러스터에서 네트워크를 사용하지 않도록 설정합니다. iSCSI 네트워크가 계속해서 DAG 네트워크로 나타나지만 위의 명령을 실행한 후에는 MAPI 또는 복제 트래픽에 iSCSI 네트워크가 사용되지 않습니다.

맨 위로 이동

## DAG 구성원 구성

DAG의 구성원인 사서함 서버는 다음 섹션의 설명과 같이 구성해야 하는 고가용성에 특정한 일부 속성을 갖고 있습니다.

  - Automatic database mount dial

  - Database copy automatic activation policy

  - Maximum active databases

## 자동 데이터베이스 탑재 다이얼

*AutoDatabaseMountDial* 매개 변수는 데이터베이스 장애 조치(failover) 후 자동 데이터베이스 탑재 행동을 지정합니다. [Set-MailboxServer](https://technet.microsoft.com/ko-kr/library/aa998651\(v=exchg.150\)) cmdlet을 사용하여 다음 값을 가진 *AutoDatabaseMountDial* 매개 변수를 구성할 수 있습니다.

  - `BestAvailability`   이 값을 지정하면 복사 큐 길이가 12 이하인 경우 장애 조치(failover) 후 즉시 데이터베이스가 자동으로 탑재됩니다. 복사 큐 길이는 복제해야 하는 수동 복사본에서 인식되는 로그 개수입니다. 복사 큐 길이가 12보다 크면 데이터베이스가 자동으로 탑재되지 않습니다. 복사 큐 길이가 12 이하이면 Exchange에서는 나머지 로그를 수동 복사본에 복제하려고 시도하며 데이터베이스를 탑재합니다.

  - `GoodAvailability`   이 값을 지정하면 복사 큐 길이가 6 이하인 경우 장애 조치(failover) 후 즉시 데이터베이스가 자동으로 탑재됩니다. 복사 큐 길이는 복제해야 하는 수동 복사본에서 인식되는 로그 개수입니다. 복사 큐 길이가 6보다 크면 데이터베이스가 자동으로 탑재되지 않습니다. 복사 큐 길이가 6 이하이면 Exchange에서는 나머지 로그를 수동 복사본에 복제하려고 시도하며 데이터베이스를 탑재합니다.

  - `Lossless`   이 값을 지정하면 활성 복사본에 생성된 모든 로그가 수동 복사본에 복사될 때까지 데이터베이스가 자동으로 탑재되지 않습니다. 또한 이 설정은 Active Manager의 최상의 복사본 선택 알고리즘이 데이터베이스 복제의 복제 큐 길이가 아닌 활성화 선호값을 기반으로 활성화할 잠재적인 후보들을 정렬하도록 합니다.

기본값은 `GoodAvailability`입니다. `BestAvailability` 또는 `GoodAvailability`를 지정하면 활성 복사본의 모든 로그를 활성화되어 있는 수동 복사본에 복제할 수 없는 경우 사서함 데이터가 일부 손실될 수도 있습니다. 그러나 기본적으로 사용하도록 설정되는 보안 네트워크 기능을 통해 보안 네트워크 큐에 있는 메시지를 다시 전송하여 대부분의 데이터 손실을 방지할 수 있습니다.

## 예: 자동 데이터베이스 탑재 다이얼 구성

`GoodAvailability`의 *AutoDatabaseMountDial* 설정을 갖는 사서함 서버 구성 예는 다음과 같습니다.

```powershell
Set-MailboxServer -Identity EX1 -AutoDatabaseMountDial GoodAvailability
```

## 데이터베이스 복사본 자동 활성화 정책

*DatabaseCopyAutoActivationPolicy* 매개 변수는 선택한 사서함 서버의 사서함 데이터베이스 복사본에 사용할 수 있는 자동 활성화 형식을 지정합니다. [Set-MailboxServer](https://technet.microsoft.com/ko-kr/library/aa998651\(v=exchg.150\)) cmdlet을 사용하여 다음 값을 가진 *DatabaseCopyAutoActivationPolicy* 매개 변수를 구성할 수 있습니다.

  - `Blocked`   이 값을 지정하면 선택한 사서함 서버에서 데이터베이스를 자동으로 활성화할 수 없습니다.

  - `IntrasiteOnly`  동일한 Active Directory 사이트의 서버에서 데이터베이스 복사본을 활성화할 수 있습니다. 이 값을 설정하면 사이트 간 장애 조치(failover) 또는 활성화를 사용할 수 없습니다. 이 속성은 들어오는 사서함 데이터베이스 복사본(예: 활성 복사본으로 설정되는 수동 복사본)에 사용됩니다. 다른 Active Directory 사이트에서 활성화된 데이터베이스 복사본에 대해 이 사서함 서버의 데이터베이스를 활성화할 수 없습니다.

  - `Unrestricted` 이 값을 지정하면 선택한 사서함 서버에서 사서함 데이터베이스 복사본을 활성화하는 기능에 대한 특별한 제한은 없습니다.

## 예: 데이터베이스 복사본 자동 활성화 정책 구성

`Blocked`의 *DatabaseCopyAutoActivationPolicy* 설정을 갖는 사서함 서버 구성 예는 다음과 같습니다.

```powershell
Set-MailboxServer -Identity EX1 -DatabaseCopyAutoActivationPolicy Blocked
```

## 최대 활성 데이터베이스

*MaximumActiveDatabases* 매개 변수([Set-MailboxServer](https://technet.microsoft.com/ko-kr/library/aa998651\(v=exchg.150\)) cmdlet과 함께 사용되기도 함)는 사서함 메일 서버에 탑재될 수 있는 데이터베이스 수를 지정합니다. 개인 사서함 서버가 오버로드되지 않도록 하여 배포 요구사항을 충족하도록 사서함 서버를 구성할 수 있습니다.

*MaximumActiveDatabases* 매개 변수는 숫자 값(정수)으로 설정됩니다. 최대 개수에 도달하면 장애 조치(failover) 또는 전환이 발생해도 서버의 데이터베이스 복사본이 활성화되지 않습니다. 서버에서 복사본이 이미 활성화되어 있으면 데이터베이스를 탑재할 수 없습니다.

## 예: 최대 활성 데이터베이스 구성

다음은 최대 20개의 활성 데이터베이스를 지원하는 사서함 서버 구성 예입니다.

```powershell
Set-MailboxServer -Identity EX1 -MaximumActiveDatabases 20
```

맨 위로 이동

## DAG 구성원에서 유지 관리 수행

DAG 구성원에서 모든 유형의 소프트웨어 또는 하드웨어 유지 관리를 수행하기 전에 먼저 DAG 구성원을 유지 관리 모드로 설정해야 합니다. 여기에는 모든 활성 데이터베이스를 서버에서 제거하고 활성 데이터베이스가 서버로 이동하지 못하게 차단하는 작업이 포함됩니다. 또한 서버(예: PAM(Primary Active Manager) 역할)에서 수행할 수 있는 중요한 모든 DAG 지원 기능이 다른 서버로 이동하며 서버로 다시 이동하는 것이 차단됩니다. 특히 다음 작업을 수행해야 합니다.

1.  전송 큐 드레이닝 프로세스를 시작하려면 `Set-ServerComponentState <ServerName> -Component HubTransport -State Draining -Requester Maintenance`를 실행합니다.

2.  전송 큐 드레이닝을 시작하려면 `Restart-Service MSExchangeTransport`를 실행합니다.

3.  모든 통합 메시징 호출 드레이닝 프로세스를 시작하려면 `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Draining -Requester Maintenance`를 실행합니다.

4.  로컬 큐에서 전달 보류 중인 메시지를 Target 매개 변수에 의해 지정된 사서함 서버로 리디렉션하려면 `Redirect-Message -Server <ServerName> -Target <MailboxServerFQDN>`을 실행합니다.

5.  클러스터 노드를 일시 중지하여 노드가 PAM이 되지 않도록 하려면 `Suspend-ClusterNode <ServerName>`를 실행합니다.

6.  DAG 구성원에 현재 호스팅된 모든 활성 데이터베이스를 다른 DAG 구성원으로 이동하려면 `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $True`를 실행합니다.

7.  서버가 활성 데이터베이스 복사본을 호스팅하지 않도록 하려면 `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Blocked`을 실행합니다.

8.  서버를 유지 관리 모드로 설정하려면 `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Inactive -Requester Maintenance`를 실행합니다.

서버가 유지 관리에 대한 준비가 되었는지 확인하려면 다음 작업을 수행합니다.

1.  서버가 유지 관리 모드로 설정되었는지 확인하려면 `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`를 실행합니다.

2.  서버가 어떠한 활성 데이터베이스 복사본도 호스팅하고 있지 않는지 확인하려면 `Get-MailboxServer <ServerName> | ft DatabaseCopy* -Autosize`를 실행합니다.

3.  노드가 일시 중지되었는지 확인하려면 `Get-ClusterNode <ServerName> | fl`을 실행합니다.

4.  모든 전송 큐가 없어졌는지 확인하려면 `Get-Queue`를 실행합니다.

유지 관리가 완료되고 DAG 구성원이 서비스할 준비가 된 후에는 다음 작업을 수행하여 DAG 구성원을 유지 관리 모드에서 해제하고 다시 프로덕션 모드로 설정할 수 있습니다.

  - 서버가 유지 관리 모드에서 해제되도록 지정하려면 `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Maintenance`를 실행합니다.

  - 서버가 통합 메시징 호출을 수락하도록 하려면 `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Active -Requester Maintenance`를 실행합니다.

  - 클러스터의 노드를 다시 시작하고 서버에 대한 전체 클러스터 기능을 사용하려면 `Resume-ClusterNode <ServerName>`을 실행합니다.

  - 데이터베이스가 서버에서 활성 상태가 되도록 하려면 `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $False`를 실행합니다.

  - 자동 활성화 블록을 제거하려면 `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Unrestricted`를 실행합니다.

  - 전송 큐를 사용하도록 설정하고 서버가 메시지를 수락 및 처리하도록 하려면 `Set-ServerComponentState <ServerName> -Component HubTransport -State Active -Requester Maintenance`를 실행합니다.

  - 전송 작업을 다시 시작하려면 `Restart-Service MSExchangeTransport`를 실행합니다.

서버가 프로덕션용으로 준비되었는지 확인하려면 다음 작업을 수행합니다.

1.  서버가 유지 관리 모드에 있지 않은지 확인하려면 `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`를 실행합니다.

Exchange 업데이트를 설치할 때 업데이트 프로세스에 실패한 경우 일부 서버 구성 요소가 비활성 상태로 남아 있을 수 있으며, 이러한 구성 요소가 위 Get-ServerComponentState cmdlet의 출력에 표시됩니다. 이를 해결하려면 다음 명령을 실행합니다.

  - `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component Monitoring -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component RecoveryActionsEnabled -State Active -Requester Functional`

맨 위로 이동

## DAG 구성원 종료

Exchange 2013 고가용성 솔루션은 Windows 종료 프로세스와 통합되었습니다. 관리자 또는 응용 프로그램이 DAG에서 하나 이상의 DAG 구성원에 복제되어 탑재된 데이터베이스를 보유한 Windows 서버 종료를 시작하는 경우 시스템은 종료 프로세스가 완료되기 전에 탑재된 데이터베이스의 다른 복사본을 활성화합니다.

하지만 이 새로운 동작은 서버에서 종료되는 데이터베이스가 모두 `lossless` 활성화되는지 보장하지 않습니다. 따라서 DAG의 구성원인 서버를 종료하기 전에 서버 전환을 수행하는 것이 좋은 방법입니다.

맨 위로 이동

## DAG 구성원에 업데이트 설치

DAG 구성원인 서버에 Microsoft Exchange Server 2013 업데이트를 설치하는 작업은 비교적 간단한 프로세스입니다. DAG 구성원인 서버에 업데이트를 설치할 때 모든 Exchange 서비스와 클러스터 서비스를 비롯하여 여러 서비스가 설치하는 동안 중지됩니다. DAG 구성원에 업데이트를 적용하는 일반적인 프로세스는 다음과 같습니다.

1.  위에 설명한 단계를 사용하여 DAG 구성원을 유지 관리 모드로 설정합니다.

2.  업데이트를 설치합니다.

3.  위에 설명한 단계를 사용하여 DAG 구성원을 유지 관리 모드에서 해제하고 다시 프로덕션 모드로 설정합니다.

4.  필요시 RedistributeActiveDatabases.ps1 스크립트를 사용하여 DAG의 활성 데이터베이스 복사본의 균형을 다시 맞춥니다.

Exchange 2013에 대한 최신 업데이트는 [Microsoft 다운로드 센터](http://www.microsoft.com/downloads/ko-kr/)에서 다운로드할 수 있습니다.

맨 위로 이동

