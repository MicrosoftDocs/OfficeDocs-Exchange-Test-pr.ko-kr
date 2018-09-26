---
title: '데이터베이스 가용성 그룹 만들기: Exchange 2013 Help'
TOCTitle: 데이터베이스 가용성 그룹 만들기
ms:assetid: d6b98299-e203-488b-af73-50753fe152c8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351172(v=EXCHG.150)
ms:contentKeyID: 50484310
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 가용성 그룹 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

DAG(데이터베이스 사용 가능 그룹)는 데이터베이스, 서버 또는 네트워크 오류에 대한 데이터베이스 수준의 자동 복구 기능을 제공하는 최대 16개의 Microsoft Exchange Server 2013 사서함 서버로 이루어진 집합입니다. 사서함 서버를 DAG에 추가하면 이 서버가 DAG의 다른 서버와 함께 작동하여 데이터베이스, 서버 및 네트워크 오류에 대한 데이터베이스 수준의 자동 복구 기능을 제공합니다.

DAG와 관련된 다른 관리 작업에 대한 자세한 내용은 [데이터베이스 가용성 그룹 관리](managing-database-availability-groups-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "데이터베이스 가용성 그룹" 항목

  - Windows Server 2012가 실행 중인 사서함 서버에서 DAG를 생성할 때는 DAG에 구성원을 추가하기 전에 CNO(클러스터 이름 개체)를 사전 준비해야 합니다. Windows Server 2012 R2를 실행 중인 사서함 서버를 사용하여 관리 액세스 포인트가 없는 DAG를 만들 때는 DAG에 대한 CNO를 사전 준비할 필요가 없습니다. 자세한 단계는 [데이터베이스 가용성 그룹에 대한 클러스터 이름 개체 미리 준비](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)를 참조하십시오.

  - DAG를 만들 때는 DAG에 고유한 이름을 지정합니다(최대 15자). 관리 액세스 포인트가 없는 Windows Server 2012 R2 DAG를 만들고 DAG에 IP를 할당하지 않으려는 경우를 제외하면 DAG의 이름을 제공하는 것 외에 IP 주소(IPv4 또는 IPv4와 IPv6 둘 다)도 하나 이상 DAG에 할당해야 합니다. 그렇지 않으면 할당하려는 IP 주소가 MAPI 네트워크에 사용되는 각 서브넷에 있어야 하며 사용 가능한 상태여야 합니다. 사용자가 하나 이상의 IPv4 주소를 지정하고 시스템이 IPv6을 사용하도록 구성되어 있는 경우 이 작업을 수행하면 DAG에 하나 이상의 IPv6 주소가 자동으로 할당됩니다.

  - DAG를 만들 때는 미러링 모니터 서버와 감시 디렉터리를 선택적으로 지정할 수 있습니다. 미러링 모니터 서버를 지정하는 경우 사서함 역할이 설치되지 않은 클라이언트 액세스 서버를 사용하는 것이 좋습니다. 이렇게 하면 Exchange 관리자가 감시 가능성을 인식할 수 있고, 미러링 모니터 서버를 사용하는 데 필요한 모든 필수 보안 권한이 준비될 수 있습니다.
    
    다음과 같은 옵션 및 동작의 조합을 사용할 수 있습니다.
    
      - DAG의 이름만 지정하고 **미러링 모니터 서버**와 **감시 디렉터리** 필드를 비워 둡니다. 이 시나리오에서는 사서함 서버 역할이 설치되지 않은 클라이언트 액세스 서버가 검색됩니다. 그런 다음 자동으로 기본 감시 디렉터리를 만들고 해당 클라이언트 액세스 서버에서 공유하며 DAG를 구성하여 해당 서버를 미러링 모니터 서버로 사용합니다.
    
      - 미러링 모니터 서버에 만들고 공유할 디렉터리, 사용할 미러링 모니터 서버 및 DAG의 이름을 지정할 수 있습니다.
    
      - DAG의 이름을 지정하고 사용할 미러링 모니터 서버를 지정하고 **감시 디렉터리** 필드를 비워 둡니다. 이 시나리오에서는 지정된 미러링 모니터 서버에 기본 감시 디렉터리가 만들어집니다.
    
      - 사용자는 DAG의 이름을 지정하고, **미러링 모니터 서버** 필드를 비워 두고, 미러링 모니터 서버에서 만들고 공유할 디렉터리를 지정할 수 있습니다. 이 시나리오에서 마법사는 사서함 서버 역할이 설치되어 있지 않은 클라이언트 액세스 서버를 검색하고, 해당 서버에 지정된 감시 디렉터리를 자동으로 만들고 공유하며, 해당 클라이언트 액세스 서버를 미러링 모니터 서버로 사용하도록 DAG를 구성합니다.
    

    > [!IMPORTANT]    
    > 지정한 미러링 모니터 서버는 Exchange 2013 또는 Exchange 2010 서버 없으면 미러링 모니터 서버에서 로컬 Administrators 그룹에 Exchange 신뢰할 수 있는 하위 시스템 유니버설 보안 그룹을 추가 해야 합니다. 이러한 보안 권한을 해당 Exchange 수 있는 디렉터리를 만들고 필요에 따라 미러링 모니터 서버에서 공유할 수 있도록 필요 합니다. 적절 한 사용 권한이 구성 되지 않은 경우 다음과 같은 오류가 반환 됩니다.<BR><CODE>Error: An error occurred during discovery of the database availability group topology. Error: An error occurred while attempting a cluster operation. Error: Cluster API "AddClusterNode() (MaxPercentage=12) failed with 0x80070005. Error: Access is denied."</CODE>



  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 데이터베이스 사용 가능 그룹 만들기

1.  EAC에서 **서버** \> **데이터베이스 사용 가능 그룹**으로 이동합니다.

2.  ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭하여 DAG를 만듭니다.

3.  **새 데이터베이스 사용 가능 그룹** 페이지에서 DAG에 대한 다음 정보를 입력합니다.
    
      - **데이터베이스 사용 가능 그룹 이름**   이 필드에 유효하고 고유한 DAG 이름을 입력합니다(최대 15자). 이 이름은 컴퓨터 이름과 동일하며 해당하는 CNO가 이 이름으로 Active Directory에 만들어집니다. 이 이름은 DAG의 이름과 기본 클러스터 모두의 이름이 됩니다.
    
      - **미러링 모니터 서버**   이 필드에 DAG의 미러링 모니터 서버를 지정합니다. 이 필드를 비워 둘 경우 시스템은 미러링 모니터 서버로 사용할 사서함 서버와 함께 컴퓨터에 설치되지 않은 로컬 Active Directory 사이트의 클라이언트 액세스 서버를 자동으로 선택하려고 시도합니다.
        

        > [!NOTE]  
        > 미러링 모니터 서버를 지정하는 경우 호스트 이름이나 FQDN(정규화된 도메인 이름)을 사용해야 합니다. IP 주소 또는 와일드카드 이름은 지원되지 않습니다. 또한 미러링 모니터 서버는 DAG의 구성원일 수 없습니다.

    
      - **감시 디렉터리**   이 필드에 감시 데이터를 저장하는 데 사용할 미러링 모니터 서버의 디렉터리 경로를 입력합니다. 이 디렉터리가 없으면 시스템이 자동으로 미러링 모니터 서버에 디렉터리를 만듭니다. 이 필드를 비워 둘 경우 기본 디렉터리(%SystemDrive%\\DAGFileShareWitnesses\\\<DAG FQDN\>)가 미러링 모니터 서버에 만들어집니다.
    
      - **데이터베이스 사용 가능 그룹 IP 주소**   이 필드에 하나 이상의 고정 IPv4 주소를 DAG에 할당합니다. IPv4 주소를 입력하고 ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭하여 이 주소를 추가합니다. DAG에서 DHCP(Dynamic Host Configuration Protocol)를 사용하여 필요한 IPv4 주소를 가져오게 하려면 이 필드를 비워 두십시오. 필요한 경우 255.255.255.255를 입력하여 IP 주소 또는 클러스터 관리 액세스 포인트가 없는 DAG를 만듭니다. 이 방법은 Windows Server 2012 R2를 실행 중인 사서함 서버를 포함할 DAG에만 적용됩니다.

4.  **저장**을 클릭하여 DAG를 만듭니다.

## 셸을 사용하여 데이터베이스 사용 가능 그룹 만들기

이 예에서는 미러링 모니터 서버 FILESRV1과 로컬 디렉터리 C:\\DAG1을 사용하도록 구성된 DAG인 DAG1을 만듭니다. 또한 DAG1은 DAG의 IP 주소에 DHCP를 사용하도록 구성됩니다.

```powershell
New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer FILESRV1 -WitnessDirectory C:\DAG1
```

이 예에서는 DAG2라는 DAG를 만듭니다. 시스템은 사서함 서버 역할을 DAG의 미러링 모니터 서버로 포함되지 않는 로컬 Active Directory 사이트의 클라이언트 액세스 서버를 자동으로 선택합니다. 이 예에서는 모든 DAG 구성원에 동일한 서브넷의 MAPI 네트워크가 포함되므로 DAG2에는 고정 IP 주소 하나가 할당됩니다.

```powershell
New-DatabaseAvailabilityGroup -Name DAG2 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8
```

이 예에서는 DAG3이라는 DAG를 만듭니다. DAG3은 미러링 모니터 서버 MBX2와 로컬 디렉터리 C:\\DAG3을 사용하도록 구성됩니다. DAG 구성원이 MAPI 네트워크에서 서로 다른 서브넷에 있으므로 DAG3에는 여러 개의 고정 IP 주소가 할당됩니다.

```powershell
New-DatabaseAvailabilityGroup -Name DAG3 -WitnessServer MBX2 -WitnessDirectory C:\DAG3 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,192.168.0.8
```
이 예에서는 DHCP를 사용하도록 구성된 DAG DAG4를 만듭니다. 또한 시스템에서 미러링 모니터 서버를 자동으로 선택하며 기본 감시 디렉터리가 만들어집니다.

```powershell
New-DatabaseAvailabilityGroup -Name DAG4
```

이 예에서는 관리 액세스 포인트가 포함되지 않은 DAG인 DAG5를 만듭니다. 이 방법은 Windows Server 2012 R2 DAG의 경우에만 유효합니다. 또한 MBX4를 DAG의 미러링 모니터 서버로 사용하고 기본 감시 디렉터리를 만듭니다.

```powershell
New-DatabaseAvailabilityGroup -Name DAG5 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress]::None) -WitnessServer MBX4
```

## 작동 여부는 어떻게 확인합니까?

DAG가 성공적으로 만들어졌는지 확인하려면 다음 중 하나를 수행하세요.

  - EAC에서 **서버** \> **데이터베이스 사용 가능 그룹**으로 이동합니다. 새로 만든 DAG가 표시됩니다.

  - 셸에서 다음 명령을 실행하여 DAG가 만들어졌는지, DAG 속성 정보가 표시되는지 확인합니다.
    
    ```powershell
    Get-DatabaseAvailabilityGroup <DAGName> | Format-List
    ```

## 자세한 내용

[DAG(데이터베이스 가용성 그룹)](database-availability-groups-dags-exchange-2013-help.md)

[데이터베이스 가용성 그룹 속성 구성](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ko-kr/library/dd297934\(v=exchg.150\))

[New-DatabaseAvailabilityGroup](https://technet.microsoft.com/ko-kr/library/dd351107\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd335225\(v=exchg.150\))

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ko-kr/library/dd298049\(v=exchg.150\))

