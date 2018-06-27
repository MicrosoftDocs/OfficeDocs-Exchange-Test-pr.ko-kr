---
title: 'DAG 미러링 모니터 서버와 Microsoft Azure VM을 사용 하 여: Exchange 2013 Help'
TOCTitle: DAG 미러링 모니터 서버와 Microsoft Azure VM을 사용 하 여
ms:assetid: 03d1e215-518b-4b48-bfcd-8d187ff8f5ef
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn903504(v=EXCHG.150)
ms:contentKeyID: 63892236
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DAG 미러링 모니터 서버와 Microsoft Azure VM을 사용 하 여

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Exchange Server 2013 를 사용 하면 자동 데이터 센터 장애 조치에 대 한 데이터베이스 가용성 그룹 (DAG)에서 사서함 데이터베이스를 구성할 수 있습니다. 이 구성은 필요 세 별도 실제 위치: 사서함 서버 및 미러링 모니터 서버는 DAG에 대해 시키려면 세번째 위치 두 데이터 센터입니다. 이제 조직만 두 실제 위치와도 활용할 수 자동 데이터 센터 장애 조치 DAG의 미러링 모니터 서버 역할을 Microsoft Azure 파일 서버 가상 컴퓨터를 사용 하 여 합니다.

이 문서는 Microsoft Azure에서 DAG 미러링 모니터 서버 배치에 중점적으로 설명 하 고는 사이트 복구 계획 개념을 숙지 하 고 두 데이터 센터에 걸쳐 모든 기능을 갖춘 DAG 인프라를 이미 있다고 가정 합니다. 사용 하도록 구성 된 DAG 인프라를 이미 설치 하지 않은 경우 먼저 다음 문서를 검토 하는 것이 좋습니다.

[고가용성 및 사이트 복구](high-availability-and-site-resilience-exchange-2013-help.md)

[DAG(데이터베이스 가용성 그룹)](database-availability-groups-dags-exchange-2013-help.md)

[고가용성 및 사이트 복원 계획](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)

## Microsoft Azure 변경

이 구성에 대 한 다중 사이트 VPN 필요합니다. 항상 되었을 Microsoft Azure 사이트 마다 VPN 연결을 사용 하 여 조직의 네트워크에 연결할 수 있습니다. 그러나 과거에 Azure만 단일 사이트 마다 VPN을 지원 합니다. 여러 사이트 간 Vpn을 필요한 세 데이터 센터 DAG 및 해당 미러링 모니터 서버를 구성, 이후 Azure VM에서 DAG 미러링 모니터 서버 배치 가능한 처음 되지 않았습니다.

6 월 2014 년에 Microsoft Azure에는 조직에서 동일한 Azure 가상 네트워크를 여러 데이터 센터에 연결 수를 사용 하도록 설정 하는 다중 사이트 VPN 지원을 도입 되었습니다. 이 변경도 가능해졌습니다 조직 두 데이터 센터에 대 한 Microsoft Azure 세번째를 삽입할 위치를 자신의 DAG 미러링 모니터 서버도 활용할 수 있도록 합니다. Azure의 다중 사이트 VPN 기능에 대 한 자세한 내용은 하십시오 [구성 다중 사이트 VPN](http://go.microsoft.com/fwlink/?linkid=522621)를 참조 합니다.


> [!NOTE]
> 이 구성 미러링 모니터 서버를 배포 하기 위한 Azure 가상 컴퓨터 및 다중 사이트 VPN 기술을 활용 하 고 Azure 클라우드 미러링 모니터 서버를 사용 하지 않습니다.



## Microsoft Azure 파일 서버 미러링 모니터 서버

다음 다이어그램은 VM에는 Microsoft Azure 파일 서버를 사용 하 여 DAG 미러링 모니터 서버로 대 한 개요입니다. Azure 가상 네트워크 Azure 가상 네트워크 및 도메인 컨트롤러 및 Azure 가상 컴퓨터에 배포 되는 파일 서버에 데이터 센터를 연결 하는 다중 사이트 VPN 해야 합니다.


> [!NOTE]
> 기술적으로이 목적을 위해 단일 Azure VM을 사용 하 고 도메인 컨트롤러에서 파일 공유를 미러링 모니터 서버를 배치 하는 것이 불가능 합니다. 그러나 이렇게 하면 불필요 한 권한 상승 합니다. 따라서 구성 방법은 바람직하지 않습니다.



**Microsoft Azure에서 DAG 미러링 모니터 서버**

![Azure의 Exchange DAG 감시 개요](images/Dn903504.7cbda882-bbae-4be7-b0ea-60947b8aa4ef(EXCHG.150).png "Azure의 Exchange DAG 감시 개요")

가장 먼저 여 DAG 미러링 모니터 서버는 구독을 얻는 것에 대 한 Microsoft Azure VM을 사용 하기 위해 수행 해야 합니다. Azure에 구독 구입 하는 최상의 방법에 대해 [Azure를 구입 하는 방법](http://go.microsoft.com/fwlink/?linkid=398989) 참조 합니다.

Azure 구독을 설치한 후 순서에 따라 다음을 수행 해야 합니다.

1.  Microsoft Azure 가상 네트워크를 준비 합니다.

2.  다중 사이트 VPN을 구성 합니다.

3.  가상 컴퓨터를 구성 합니다.

4.  DAG 미러링 모니터 서버를 구성 합니다.


> [!NOTE]
> 이 문서의 지침의 중요 한 부분 Microsoft Azure 구성을 수행 해야 합니다. 따라서 Azure 설명서에 대 한 링크는 해당 때마다 사용 됩니다.



## 필수 구성 요소

  - Exchange 높은 가용성 및 사이트 복원 력 배포를 지원할 수 있는 두 데이터 센터입니다. 자세한 내용은 [고가용성 및 사이트 복원 계획](planning-for-high-availability-and-site-resilience-exchange-2013-help.md) 참조

  - 각 사이트에 VPN 게이트웨이에 대 한 NAT 뒤에 없는 공용 IP 주소를

  - Microsoft Azure과 호환 되는 각 사이트에 사용 되는 VPN 장치입니다. 호환 가능한 장치에 대 한 자세한 내용은 [가상 네트워크에 대 한 VPN 장치에 대 한](http://go.microsoft.com/fwlink/?linkid=522619) 을 참조 하십시오.

  - DAG 개념 및 관리에 능숙 해야함

  - Windows PowerShell에 대 한 지식

## 1 단계: Microsoft Azure 가상 네트워크를 준비 합니다.

Microsoft Azure 네트워크 구성은 배포 프로세스의 가장 중요 한 부분입니다. 이 단계 끝 다중 사이트 VPN 통해 두 데이터 센터에 연결 된 모든 기능을 갖춘 Azure 가상 네트워크를 해야 합니다.

## DNS 서버를 등록 합니다.

이 구성에 온-프레미스 서버와 Azure Vm 간의 이름 확인 필요 하기 때문에 고유한 DNS 서버를 사용 하 여 Azure를 구성 해야 합니다. [이름 확인 (DNS)](http://msdn.microsoft.com/en-us/library/azure/jj156088.aspx) 항목 이름 확인 Azure에 대 한 개요를 제공합니다.

DNS 서버를 등록 하려면 다음을 수행 합니다.

1.  Azure 포털에서 **네트워크** 이동 하 고 **새로 만들기** 를 클릭 합니다.

2.  **네트워크 서비스** 를 클릭 \> **가상 네트워크** \> **DNS 서버를 등록** 합니다.

3.  이름 및 DNS 서버에 대 한 IP 주소를 입력 합니다. 여기에 지정 된 이름 관리 포털에 사용 되는 논리 이름을 이며 경우 DNS 서버의 실제 이름과 일치 필요가 없습니다.

4.  추가 하려는 다른 DNS 서버에 대해 1-3 단계를 반복 합니다.
    

    > [!NOTE]
    > 등록 하는 DNS 서버에 라운드 로빈 방식으로 사용 되지 않습니다. Azure Vm 나열 된 첫번째 DNS 서버를 사용 하 고 첫번째 계정을 사용할 수 없는 경우에 다른 서버를 사용 합니다.



5.  1-Microsoft Azure에 배포 하는 도메인 컨트롤러에 사용할 IP 주소를 추가 하려면 3 단계를 반복 합니다.

## 로컬 만들기 Azure의 네트워크 개체 (온-프레미스)

다음을 in Microsoft Azure 데이터 센터를 표시 하는 논리 네트워크 개체를 만들려면 다음을를 수행 합니다.

1.  Azure 포털에서 다음 **네트워크** 이동 하 고 **새로 만들기** 를 클릭 하 고 있습니다.

2.  **네트워크 서비스** 를 클릭 \> **가상 네트워크** \> **로컬 네트워크를 추가** 합니다.

3.  해당 사이트에서 첫번째 데이터 센터 사이트와 VPN 장치의 IP 주소에 이름을 입력 합니다. 이 IP 주소 NAT. 뒤에 없는 정적 공용 IP 주소 여야 합니다.

4.  다음 화면에서 첫번째 사이트에 대 한 IP 서브넷을 지정 합니다.

5.  단계 1-반복 하 여 두번째 사이트에 대 한 4입니다.

## Azure 가상 네트워크 만들기

이제, Vm에서 사용 되는 Azure 가상 네트워크를 만들려면 다음을 수행 합니다.

1.  Azure 포털에서 **네트워크** 이동 하 고 **새로 만들기** 를 클릭 합니다.

2.  **네트워크 서비스** 를 클릭 \> **가상 네트워크** \> **사용자 지정 만들기**.

3.  **가상 네트워크 세부 정보** 페이지에서 가상 네트워크에 대 한 이름을 지정 하 고 네트워크에 대 한 지리적 위치를 선택 합니다.

4.  **DNS 서버 및 VPN 연결** 페이지에서 이전에 등록 된 DNS 서버가 DNS 서버에 나타나는지 확인 합니다.

5.  **사이트 간 연결** 에서 **사이트 간 VPN 구성** 확인란을 선택 합니다.
    

    > [!IMPORTANT]
    > 그러면 다중 사이트 VPN을 설정 하는 데 필요한 필요한 구성 변경을 방지할 수 있으므로 <STRONG>사용 ExpressRoute</STRONG> 를 선택 하지 마십시오.



6.  **로컬 네트워크** 구성한 두 온-프레미스 네트워크 중 하나를 선택 합니다.

7.  **가상 네트워크 주소 공간** 페이지에서 Azure 가상 네트워크에 사용할 IP 주소 범위를 지정 합니다.

## 검사점: 검토 네트워크 구성

이 시점 **네트워크** 로 이동할 때의 **가상 네트워크,로컬 네트워크** 및 **DNS 서버** 에서 서버의 등록 된 DNS 서버에서 로컬 사이트에서 구성 하는 가상 네트워크를 표시 됩니다.

## 다중 사이트 VPN을 구성 하는 2 단계:

다음 단계에서는 온-프레미스 사이트에 VPN 게이트웨이 설정 하는 것입니다. 이 작업을 수행 해야 합니다.

1.  Azure 포털을 사용 하 여 VPN 게이트웨이 사이트 중 하나를 설정 합니다.

2.  가상 네트워크 구성 설정을 내보냅니다.

3.  다중 사이트 VPN을 구성 파일을 수정 합니다.

4.  업데이트 된 Azure 네트워크 구성을 가져옵니다.

5.  Azure 게이트웨이 IP 주소 및 미리 공유한 키를 기록 합니다.

6.  온-프레미스 VPN 장치를 구성 합니다.

다중 사이트 VPN을 구성 하는 방법에 대 한 자세한 내용은 [Configure 다중 사이트 VPN](http://go.microsoft.com/fwlink/?linkid=522621)를 참조 합니다.

## 첫번째 사이트에 대 한 VPN 게이트웨이가 설정

해당 가상 게이트웨이 만들 때 note 이미 지정한 첫번째 온-프레미스 사이트에 연결 될 됩니다. 가상 네트워크 대시보드, 들어갈 때 게이트웨이 만들어지지 않은 표시 메시지가 표시 됩니다.

Azure 측에서 VPN 게이트웨이 설정 하기 위해 [구성 관리 포털에서 가상 네트워크 게이트웨이](http://msdn.microsoft.com/en-us/library/azure/jj156210.aspx)의 [가상 네트워크 게이트웨이 시작](http://msdn.microsoft.com/en-us/library/azure/jj156210.aspx#bkmk_startgateway) 섹션의 지침을 따릅니다.


> [!IMPORTANT]
> 만 문서의 "시작 가상 네트워크 게이트웨이" 섹션의 단계를 수행 하 고 섹션을 계속 하지 마십시오.



## 가상 네트워크 구성 설정 내보내기

현재 Azure 관리 포털 다중 사이트 VPN을 구성할 수 있습니다를 허용 하지 않습니다. 이 구성에 대 한 가상 네트워크 구성 설정을 XML 파일로 내보내고 다음 해당 파일을 수정 해야 합니다. 설정을 내보내려면[네트워크 구성 파일을 가상 네트워크 설정 내보내기](http://msdn.microsoft.com/en-us/library/azure/dn133804.aspx) 에서 지침을 따릅니다.

## 다중 사이트 VPN에 대 한 네트워크 구성 설정 수정

모든 XML 편집기에 내보낸 파일을 엽니다. 온-프레미스 사이트에 대 한 게이트웨이 연결 "ConnectionsToLocalNetwork" 섹션에 나열 됩니다. 섹션을 찾습니다 XML 파일에서 해당 용어를 검색 합니다. 구성 파일의이 섹션은 다음과 같이 표시 됩니다 (로컬 사이트 사이트인 "A"에 대해 만든 사이트 이름 가정함).

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

두번째 사이트를 구성 하려면 "ConnectionsToLocalNetwork" 섹션에서 다른 "LocalNetworkSiteRef" 섹션을 추가 합니다. 업데이트 된 구성 파일에 섹션은 다음과 같이 표시 됩니다 (둘째 로컬 사이트에는 "사이트 B"에 대 한 사이트 이름 가정함).

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
        <LocalNetworkSiteRef name="Site B">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

업데이트 된 구성 설정 파일을 저장 합니다.

## 가상 네트워크 구성 설정 가져오기

두번째으로 사이트 참조 (영문)가 구성 파일에 추가한 새 터널을 만들려면 Microsoft Azure 트리거합니다. [네트워크 구성 파일 가져오기](http://msdn.microsoft.com/en-us/library/azure/jj156213.aspx)의 지침을 사용 하 여 업데이트 된 파일을 가져옵니다. 가져오기가 완료 가상 네트워크 대시보드 모두 로컬 사이트에 대 한 게이트웨이 연결 표시 됩니다.

## Azure 게이트웨이 IP 주소 및 미리 공유 된 키를 기록 합니다.

새 네트워크 구성 설정을 가져온 후 가상 네트워크 대시보드 Azure 게이트웨이에 대 한 IP 주소가 표시 됩니다. 두 사이트 모두에서 VPN 장치에 연결 하는 IP 주소입니다. 참조 (영문)에 대 한이 IP 주소를 적어둡니다.

또한 해야하는 만들어진 각 터널에 대 한 사전 공유 IPsec/IKE 키를 가져옵니다. Azure 게이트웨이 IP 주소와 함께 이러한 키를 사용 하 여 온-프레미스 VPN 장치를 구성 합니다.

PowerShell을 사용 하 여 미리 공유한 키 해야 합니다. PowerShell을 사용 하 여 Azure 관리에 생소 하는 경우 [Azure PowerShell](http://msdn.microsoft.com/en-us/library/azure/jj156055.aspx)을 참조 하십시오.

사전 공유 키를 추출 하는 [Get AzureVNetGatewayKey](http://msdn.microsoft.com/en-us/library/azure/dn495198.aspx) cmdlet을 사용 합니다. 각 터널에 대해 한번씩이 cmdlet을 실행 합니다. 다음 예제에서는 가상 네트워크 "Azure 사이트" 및 "사이트 A"와 "사이트 B" 사이트 간의 터널에 대 한 키를 추출 하 실행 해야하는 명령 이 예제에서는 출력을 별도 파일로 저장 됩니다. 또는 이러한 키를 다른 PowerShell cmdlet 파이프라인 하거나 스크립트에 사용할 수 있습니다.

    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site A" > C:\Keys\KeysForTunnelToSiteA.txt 
    
    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site B" > C:\Keys\KeysForTunnelToSiteB.txt

## 온-프레미스 VPN 장치를 구성 합니다.

Microsoft Azure 지원 되는 VPN 장치에 대 한 VPN 장치 구성 스크립트를 제공합니다. VPN 장치에 대 한 적절 한 스크립트에 대 한 가상 네트워크 대시보드에서 **VPN 장치 스크립트 다운로드** 링크를 클릭 합니다.

다운로드 하면 스크립트를 가상 네트워크를 설정 하 고 해당 사이트에 대 한 VPN 장치를 구성할 수 있는 그대로 사용할 수를 구성 하는 첫번째 사이트에 대 한 구성 설정을 갖습니다. 예를 지정한 경우 사이트 A **로컬 네트워크** 로 가상 네트워크를 만들 때 VPN 장치 스크립트 수 있는 사이트에 사용 A. 그러나 해야하는 수정 하 여 사이트 b VPN 장치를 구성 합니다. 특히, 두번째 사이트에 대 한 키와 일치 하는 미리 공유한 키를 업데이트 해야 합니다.

등 사이트에 대해 라우팅 및 원격 액세스 서비스 (RRAS) VPN 장치를 사용 하는 경우를 해야 합니다.

1.  모든 텍스트 편집기에서 구성 스크립트를 엽니다.

2.  `#Add S2S VPN interface` 섹션을 찾습니다.

3.  이 섹션의 **Add-VpnS2SInterface** 명령을 찾아보십시오. *SharedSecret* 매개 변수 값 VPN 장치를 구성 하는 사이트에 대 한 사전 공유 키와 일치 하는지 확인 합니다.

다른 장치에는 추가 확인 해야할 수 있습니다. 예, Cisco 장치에 대 한 구성 스크립트는 로컬 IP 주소 범위를 사용 하 여 ACL 규칙을 설정 합니다. 검토 하 고 사용 하기 전에 구성 스크립트에서 로컬 사이트에 대 한 모든 참조를 확인 해야 합니다. 자세한 내용은 다음 항목을 참조 하십시오.

[라우팅 및 원격 액세스 서비스 (RRAS) 서식 파일](http://msdn.microsoft.com/en-us/library/azure/dn133801.aspx)

[Cisco ASR 서식 파일](http://msdn.microsoft.com/en-us/library/azure/dn133802.aspx)

[Cisco ISR 서식 파일](http://msdn.microsoft.com/en-us/library/azure/dn133800.aspx)

[Juniper SRX 서식 파일](http://msdn.microsoft.com/en-us/library/azure/dn133794.aspx)

[Juniper J 계열 서식 파일](http://msdn.microsoft.com/en-us/library/azure/dn133799.aspx)

[Juniper ISG 서식 파일](http://msdn.microsoft.com/en-us/library/azure/dn133797.aspx)

[Juniper SSG 서식 파일](http://msdn.microsoft.com/en-us/library/azure/dn133796.aspx)

## 검사점: VPN 상태를 검토 합니다.

이 시점 VPN 게이트웨이 통해 Azure 가상 네트워크에 연결 된 두 사이트 모두 합니다. PowerShell에서 다음 명령을 실행 하 여 다중 사이트 VPN의 상태를 확인할 수 있습니다.

    Get-AzureVnetConnection -VNetName "Azure Site" | Format-Table LocalNetworkSiteName, ConnectivityState

두 터널을 실행 하 고는,이 명령의 출력은 다음과 같은 찾습니다.

    LocalNetworkSiteName    ConnectivityState
    
    --------------------    -----------------
    
    Site A                  Connected
    
    Site B                  Connected

Azure 관리 포털에서 가상 네트워크 대시보드를 확인 하 여 연결을 확인할 수도 있습니다. 두 사이트에 대 한 **상태** 열 **연결** 로 표시 됩니다.


> [!NOTE]
> Azure 관리 포털에 표시 되는 상태 변경에 대 한 연결이 성공적으로 설정 하 고 나면 몇 분정도 걸릴 수 있습니다.



## 3 단계: 가상 컴퓨터 구성

이 배포에 대 한 Microsoft Azure의 두 가상 컴퓨터의 최소를 만들어야 할: 도메인 컨트롤러 및 DAG 미러링 모니터 서버로 사용 될 파일 서버.

1.  도메인 컨트롤러 및 [만들기는 가상 컴퓨터를 실행 하는 Windows](http://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-tutorial/)의 지침을 사용 하 여 파일 서버에 대 한 가상 컴퓨터를 만듭니다. 가상 컴퓨터의 설정을 지정 하는 경우 **지역/선호도 그룹/가상 네트워크** 를 위해 만든 가상 네트워크를 선택 하 고 있는지 확인 하십시오.

2.  도메인 컨트롤러와 Azure PowerShell을 사용 하 여 파일 서버에 대 한 기본 IP 주소를 지정 합니다. VM에 대 한 기본 IP 주소를 지정 하면 VM를 다시 시작 해야 합니다 하는 업데이트 되도록 해야 합니다. 다음 예에서는 IP 주소 Azure DC 및 Azure FSW 10.0.0.10 및 10.0.0.11 각각 설정 합니다.
    
        Get-AzureVM Azure-DC | Set-AzureStaticVNetIP -IPAddress 10.0.0.10 | Update-AzureVM
        
        Get-AzureVM Azure-FSW | Set-AzureStaticVNetIP -IPAddress 10.0.0.11 | Update-AzureVM
    

    > [!NOTE]
    > 기본 IP 주소와 VM 해당 주소를 사용 하 여 시도 합니다. 그러나 다른 VM에는 주소가 할당 하는 경우에 기본 IP 주소 구성 사용 하 여 VM 시작 되지 않습니다. 이 문제를 방지 하려면 IP 주소를 사용 하면 다른 VM에 할당 되지 되어있는지 확인 합니다. 자세한 내용은 <A href="http://msdn.microsoft.com/library/azure/dn630228.aspx">Configure VM에 대 한 고정 내부 IP 주소를</A> 을 참조 하십시오.



3.  도메인 컨트롤러 조직에서 사용 하는 표준을 사용 하 여 Azure에서 VM을 프로 비전 합니다.

4.  Exchange DAG 미러링 모니터 서버에 대 한 필수 구성 요소를 사용 하 여 파일 서버를 준비 합니다.
    
    1.  역할 추가 및 기능 마법사 또는 [Add-windowsfeature](http://technet.microsoft.com/en-us/library/ee662309.aspx) cmdlet을 사용 하 여 파일 서버 역할을 추가 합니다.
    
    2.  로컬 Administrators 그룹에 Exchange 신뢰할 수 있는 하위 시스템 유니버설 보안 그룹을 추가 합니다.

## 검사점: 가상 컴퓨터 상태를 검토 합니다.

이 시점 가상 컴퓨터를 실행 하 고 있어야 및 모두 프로그램 온-프레미스 데이터 센터의 서버와 통신할 수 있어야 합니다.

  - 온-프레미스 도메인 컨트롤러와 Azure에서 도메인 컨트롤러 복제 복제 하 고 있는지 확인 합니다.

  - Azure에서 이름으로 파일 서버에 연결 하 고 Exchange 서버에서 SMB 연결을 설정할 수 있는지 확인 합니다.

  - Azure에서 파일 서버에서 이름으로 Exchange 서버에 도달할 수 있는지 확인 합니다.

## 4 단계: DAG 미러링 모니터 서버를 구성 합니다.

마지막으로, 새 미러링 모니터 서버를 사용 하 여 DAG를 구성 해야 합니다. 기본적으로 Exchange는 C:\\DAGFileShareWitnesses을 사용 하 여 미러링 모니터 서버에서 파일 공유 감시 경로로 합니다. 사용자 지정 파일 경로 사용 하는 경우에 특정 공유에 대 한 감시 디렉터리 계획도 업데이트 해야 합니다.

1.  Exchange 관리 셸 에 연결 합니다.

2.  대화 dag 미러링 모니터 서버를 구성 하려면 다음 명령을 실행 합니다.
    
        Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessServer Azure-FSW

자세한 내용은 다음 항목을 참조 하십시오.

[데이터베이스 가용성 그룹 속성 구성](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-databaseavailabilitygroup](http://technet.microsoft.com/en-us/library/dd297934\(v=exchg.150\).aspx)

## 검사점: 파일 공유 DAG 미러링 모니터의 유효성을 검사합니다

이 시점에 DAG 미러링 모니터 서버로 azure 파일 서버를 사용 하 여 DAG를 구성 했습니다. 구성을 확인 하려면 다음을 수행 합니다.

1.  다음 명령을 실행 하 여 DAG 구성의 유효성을 검사 합니다.
    
        Get-DatabaseAvailabilityGroup -Identity DAG1 -Status | Format-List Name, WitnessServer, WitnessDirectory, WitnessShareInUse
    
    있는지 *WitnessServer* 매개 변수는 Azure에서 파일 서버에 설정, *WitnessDirectory* 매개 변수는 올바른 경로를 설정 하 고 **Primary**를 표시 하는 *WitnessShareInUse* 매개 변수를 확인 합니다.

2.  DAG 노드 수가 짝수인 경우 파일 공유 미러링 모니터 서버가 구성 됩니다. 다음 명령을 실행 하 여 클러스터 속성에서 설정 파일 공유 감시의 유효성을 검사 합니다. *SharePath* 매개 변수 값은 파일 서버를 가리키도록 하 고 올바른 경로 표시 해야 합니다.
    
        Get-ClusterResource -Cluster MBX1 | Get-ClusterParameter | Format-List

3.  다음으로, 다음 명령을 실행 하 여 "파일 공유 감시" 클러스터 리소스의 상태를 확인 합니다. 클러스터 리소스의 *State***Online**를표시 되어야 합니다.
    
        Get-ClusterResource -Cluster MBX1

4.  마지막으로, 공유 성공적으로 만들어졌는지 파일 서버에서 파일 탐색기의 폴더와 서버 관리자에서 공유를 검토 하 여 확인 합니다.

## 참고 항목


[고가용성 및 사이트 복원 계획](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
[전환 및 장애 조치](switchovers-and-failovers-exchange-2013-help.md)  
[데이터베이스 가용성 그룹 관리](managing-database-availability-groups-exchange-2013-help.md)

