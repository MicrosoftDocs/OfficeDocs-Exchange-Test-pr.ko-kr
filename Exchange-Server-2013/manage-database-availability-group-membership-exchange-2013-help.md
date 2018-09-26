---
title: '데이터베이스 가용성 그룹 구성원 관리: Exchange 2013 Help'
TOCTitle: 데이터베이스 가용성 그룹 구성원 관리
ms:assetid: fb2ea15e-96d5-4045-b75b-b0aa5fc60479
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351278(v=EXCHG.150)
ms:contentKeyID: 50484578
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 가용성 그룹 구성원 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-08-13_

서버를 DAG(데이터베이스 사용 가능 그룹)에 추가하면 DAG의 다른 서버와 함께 작동하여 데이터베이스, 서버 또는 네트워크 오류로부터 데이터베이스 수준의 자동 복구 기능을 제공합니다. DAG에서 서버를 제거하면 더 이상 오류로부터 보호되지 않습니다.

DAG와 관련된 다른 관리 작업에 대한 자세한 내용은 [데이터베이스 가용성 그룹 관리](managing-database-availability-groups-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 서버당 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "데이터베이스 가용성 그룹" 항목

  - DAG는 WFC(Windows 장애 조치(failover) 클러스터링) 기술을 사용합니다. DAG의 구성원인 각 사서함 서버는 DAG에 사용되는 기본 클러스터의 노드이기도 합니다. 따라서 언제나 사서함 서버는 하나의 DAG 구성원만 될 수 있습니다. DAG는 WFC 기술을 사용하므로 DAG에 추가된 모든 서버에서는 동일한 운영 체제인 Windows Server 2008 R2 Enterprise 또는 Datacenter Edition이나 Windows Server 2012 또는 Windows Server 2012 R2의 Standard 또는 Datacenter Edition이 실행되어야 합니다.

  - Windows Server 2012가 실행 중인 사서함 서버를 추가할 때는 DAG를 위해 CNO(클러스터 이름 개체)를 사전 준비해야 합니다. Windows Server 2012 R2를 실행하는 사서함 서버를 추가하는 경우 DAG에 관리 액세스 포인트가 없으면 CNO를 미리 준비할 필요가 없습니다. 관리 액세스 포인트가 없는 DAG에는 CNO가 없기 때문입니다. 자세한 단계는 [데이터베이스 가용성 그룹에 대한 클러스터 이름 개체 미리 준비](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)를 참조하십시오.

  - DAG에 구성원을 추가하려면 먼저 DAG를 만들어야 합니다. 자세한 단계는 [데이터베이스 가용성 그룹 만들기](create-a-database-availability-group-exchange-2013-help.md)를 참조하십시오.

  - DAG에서 서버를 제거하려면 먼저 서버의 모든 복제된 데이터베이스 복사본을 제거해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 데이터베이스 사용 가능 그룹 구성원 관리

1.  EAC에서 **서버** \> **데이터베이스 사용 가능 그룹**으로 이동합니다.

2.  구성할 DAG를 선택하고 ![DAG 구성원 관리](images/Dd351278.d567ae56-d6cd-4edb-ab67-ad8f7c58f337(EXCHG.150).gif "DAG 구성원 관리")을 클릭합니다.
    
      - DAG에 하나 이상의 사서함 서버를 추가하려면 ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭하고 목록에서 서버를 선택한 다음 **추가**를 클릭하고 **확인**을 클릭합니다.
    
      - DAG에서 하나 이상의 사서함 서버를 제거하려면 해당 서버를 선택하고 빼기(-) 아이콘을 클릭합니다.

3.  **저장**을 클릭하여 변경 내용을 저장합니다.

4.  작업이 성공적으로 완료되었으면 **닫기**를 클릭합니다.

## 셸을 사용하여 데이터베이스 사용 가능 그룹 구성원 관리

이 예에서는 MBX1이라는 사서함 서버를 DAG1라는 DAG에 추가합니다.

```powershell
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
```

이 예에서는 DAG DAG1에서 사서함 서버 MBX1을 제거합니다. 이 명령을 실행하기 전에 사서함 서버에 복제된 데이터베이스가 없는지 확인합니다.

```powershell
Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
```

이 예에서는 DAG DAG2에서 사서함 서버 MBX4의 구성 설정을 제거합니다. MBX4는 장기 오프라인 상태가 예상되므로 나머지 온라인 DAG 구성원과의 쿼럼을 설정하기 위해 오프라인 상태에 있는 동안 DAG에서 구성이 제거되고 있습니다.

```powershell
Remove-DatabaseAvailabilityGroupServer -Identity DAG2 -MailboxServer MBX4 -ConfigurationOnly
```

## 작동 여부는 어떻게 확인합니까?

DAG 구성원 자격을 성공적으로 관리했는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 **서버** \> **데이터베이스 사용 가능 그룹**으로 이동합니다. 현재 DAG 구성원이 **구성원 서버** 열에 표시됩니다.

  - 셸에서 다음 명령을 실행하여 DAG 구성원 정보를 표시합니다.
    
    ```powershell
    Get-DatabaseAvailabilityGroup <DAGName> | Format-List Servers
    ```

## 자세한 내용

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ko-kr/library/dd298049\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/ko-kr/library/dd297956\(v=exchg.150\))

