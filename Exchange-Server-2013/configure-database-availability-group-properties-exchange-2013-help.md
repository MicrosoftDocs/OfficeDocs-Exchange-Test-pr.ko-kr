---
title: '데이터베이스 가용성 그룹 속성 구성: Exchange 2013 Help'
TOCTitle: 데이터베이스 가용성 그룹 속성 구성
ms:assetid: 50daeac5-a16f-4362-a325-19e0fe25d59d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd297985(v=EXCHG.150)
ms:contentKeyID: 50483114
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 가용성 그룹 속성 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-06-24_

EAC 또는 셸을 사용하여 DAG에 사용되는 DAG IP 주소 구성, 미러링 모니터 서버 및 감시 디렉터리를 비롯한 DAG(데이터베이스 사용 가능 그룹)의 속성을 구성할 수 있습니다. 셸을 사용하면 대체 미러링 모니터 서버 및 대체 감시 디렉터리 정보, 복제에 사용되는 TCP 포트, DAC(데이터 센터 활성화 조정) 모드 등 EAC에서 사용할 수 없는 DAG 속성을 구성할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "데이터베이스 가용성 그룹" 항목

  - DAG 속성 값은 Active Directory와 클러스터 데이터베이스에 모두 저장됩니다. 그러나 일부 속성은 클러스터 데이터베이스에만 저장됩니다. 따라서 다음에 대한 속성을 설정하려면 DAG의 기본 클러스터가 실행되고 있고 쿼럼이 있어야 합니다.
    
      - ReplicationPort
    
      - NetworkCompression
    
      - NetworkEncryption
    
      - DiscoverNetworks

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 데이터베이스 가용성 그룹 속성 구성

1.  EAC에서 **서버** \> **데이터베이스 사용 가능 그룹**으로 이동합니다.

2.  구성할 DAG를 선택하고 ![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **일반** 페이지에서 DAG 구성원 자격 및 작동 상태를 확인하고 DAG 미러링 모니터 서버, 감시 디렉터리 및 자동 네트워크 구성을 지정합니다.
    
      - **미러링 모니터 서버**   DAG에 대한 미러링 모니터 서버의 호스트 이름 또는 FQDN(정규화된 도메인 이름)입니다. 이 속성은 모든 DAG의 필수 속성이지만, DAG 구성원의 수가 짝수이고 클러스터에 사용되는 쿼럼 모델이 노드 및 파일 공유 과반수 쿼럼일 때 미러링 모니터 서버가 사용됩니다.
    
      - **감시 디렉터리**   미러링 모니터 서버에서 witness.log 파일을 저장하는 데 사용되는 디렉터리의 전체 경로입니다. 이 속성은 모든 DAG의 필수 속성이지만, DAG의 미러링 모니터 서버가 사용 중일 때만 감시 디렉터리가 사용됩니다.
    
      - **작동 서버**   DAG 구성원 목록 및 각 구성원의 현재 작동 상태가 표시되는 읽기 전용 필드입니다.
    
      - **데이터베이스 그룹 네트워크 수동 구성**   모든 DAG 네트워크를 수동으로 구성하려고 할 때 선택하는 확인란입니다. 이 확인란이 비어 있는 상태로 두면 시스템에서 네트워크 인터페이스 구성을 기반으로 DAG 네트워크를 자동으로 구성합니다. 이 확인란의 선택을 취소하면 DAG에 대한 관리 용도로 **Set-DatabaseAvailabilityGroupNetwork** 및 **New-DatabaseAvailabilityGroupNetwork** cmdlet이 사용되지 않습니다.

4.  **IP 주소** 페이지에서 DAG에 할당된 IP 주소를 보고 수정합니다.
    
      - 기존 IP 주소를 수정하려면 주소를 선택하고 ![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하여 수정합니다.
    
      - 기존 IP 주소를 제거하려면 주소를 선택하고 빼기 아이콘(삭제)을 클릭합니다.
    
      - IP 주소를 DAG에 추가하려면 주소를 입력하고 ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭합니다.

5.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용하여 데이터베이스 가용성 그룹 속성 구성

이 예에서는 DAG DAG1에 대한 감시 디렉터리를 C:\\DAG1DIR로 설정합니다.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessDirectory C:\DAG1DIR

이 예에서는 DAG DAG1에 대해 CAS3의 대체 미러링 모니터 서버와 C:\\DAGFileShareWitnesses\\DAG1.contoso.com의 대체 감시 디렉터리를 미리 구성합니다.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGFileShareWitnesses\DAG1.contoso.com -AlternateWitnessServer CAS3

이 예에서는 DAG1이라는 DAG에서 DHCP(Dynamic Host Configuration Protocol)를 사용하여 IP 주소를 가져오도록 구성합니다.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 0.0.0.0

이 예에서는 DAG DAG1에서 고정 IP 주소 10.0.0.8을 사용하도록 구성합니다.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

이 예에서는 여러 개의 고정 IP 주소를 사용하여 다중 서브넷 DAG DAG1을 구성합니다.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,10.0.1.8

이 예에서는 DAC 모드에 대해 DAG DAG1을 구성합니다.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

이 예에서는 DAG1이라는 DAG의 복제 포트를 63132로 구성합니다.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -ReplicationPort 63132


> [!NOTE]
> DAG의 기본 복제 포트를 변경한 후 지정된 포트를 통해 통신할 수 있도록 하려면 DAG의 각 구성원에 대해 Windows 방화벽 예외를 수동으로 수정해야 합니다.



## 작동 여부는 어떻게 확인합니까?

DAG가 성공적으로 구성되었는지 확인하려면 다음을 수행하십시오.

  - 셸에서 다음 명령을 실행하여 DAG 구성 설정을 표시하고 DAG가 구성되었는지 확인합니다.
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## 자세한 내용

[데이터베이스 가용성 그룹 만들기](create-a-database-availability-group-exchange-2013-help.md)

[데이터베이스 가용성 그룹을 제거 합니다.](remove-a-database-availability-group-exchange-2013-help.md)

[데이터베이스 가용성 그룹 네트워크를 만들기](create-a-database-availability-group-network-exchange-2013-help.md)

[데이터베이스 가용성 그룹 구성원 관리](manage-database-availability-group-membership-exchange-2013-help.md)

[Get-DatabaseAvailabilityGroup](https://technet.microsoft.com/ko-kr/library/dd351226\(v=exchg.150\))

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/ko-kr/library/dd297934\(v=exchg.150\))

