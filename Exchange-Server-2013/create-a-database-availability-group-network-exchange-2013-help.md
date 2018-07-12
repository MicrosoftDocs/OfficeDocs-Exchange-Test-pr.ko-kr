---
title: '데이터베이스 가용성 그룹 네트워크를 만들기: Exchange 2013 Help'
TOCTitle: 데이터베이스 가용성 그룹 네트워크를 만들기
ms:assetid: 6caec7be-788a-4058-87a7-f31c575b870c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298051(v=EXCHG.150)
ms:contentKeyID: 50483328
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 가용성 그룹 네트워크를 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-02_

필요한 경우 DAG(데이터베이스 사용 가능 그룹)에 추가 네트워크를 만들 수 있습니다. DAG 네트워크를 만들려면 EAC 또는 셸을 사용합니다.

DAG와 관련된 다른 관리 작업에 대한 자세한 내용은 [데이터베이스 가용성 그룹 관리](managing-database-availability-groups-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "데이터베이스 가용성 그룹" 항목

  - DAG에 대해 자동 네트워크 구성이 사용하지 않도록 설정된 경우에만 DAG 네트워크를 만들 수 있습니다. DAG에 대해 자동 네트워크 구성을 사용하지 않도록 설정하는 방법에 대한 자세한 단계는 [데이터베이스 가용성 그룹 속성 구성](configure-database-availability-group-properties-exchange-2013-help.md)을 참조하십시오.

  - DAG 네트워크를 만드는 경우에는 다른 DAG 네트워크에서 사용하지 않는 고유한 서브넷을 할당해야 합니다. 기존 DAG 네트워크에 할당된 서브넷을 사용할 경우 해당 DAG 네트워크에서 서브넷이 제거되고 새로 만든 DAG 네트워크에 추가됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 데이터베이스 가용성 그룹 네트워크 만들기

1.  EAC에서 **서버** \> **데이터베이스 사용 가능 그룹**으로 이동합니다.

2.  구성할 DAG를 선택하고 ![DAG 네트워크 추가](images/Dd298051.befcdc4e-7f7a-451d-a0a8-608c79f5d186(EXCHG.150).gif "DAG 네트워크 추가")을 클릭합니다.

3.  **새 데이터베이스 가용성 그룹 네트워크** 페이지에서 다음과 같은 정보를 입력합니다.
    
      - **데이터베이스 사용 가능 그룹 네트워크 이름**   이 필드에 DAG에서 고유한 네트워크 이름을 입력합니다.
    
      - **설명**   이 필드를 사용하여 DAG 네트워크에 대한 텍스트 설명을 입력합니다.
    
      - **서브넷**   이 필드를 사용하여 하나 이상의 서브넷을 DAG 네트워크에 연결합니다. 서브넷을 추가하려면 ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 항목을 클릭하고, 서브넷을 편집하려면 ![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘") 항목을 클릭하고, 서브넷을 제거하려면 빼기(-)를 클릭합니다.

4.  **저장**을 클릭하여 DAG 네트워크를 만듭니다.

## 셸을 사용하여 데이터베이스 가용성 그룹 네트워크 만들기

이 예에서는 DAG1이라는 DAG에 서브넷이 10.0.0.0이고 비트마스크가 8인 ReplicationDagNetwork02 네트워크를 만듭니다. 네트워크에서 복제를 사용할 수 있으며 네트워크에 대한 선택적 설명도 추가됩니다.

    New-DatabaseAvailabilityGroupNetwork -DatabaseAvailabilityGroup DAG1 -Name ReplicationDagNetwork02 -Description "Replication network 2" -Subnets 10.0.0.0/8 -ReplicationEnabled:$True

## 작동 여부는 어떻게 확인합니까?

DAG 네트워크가 성공적으로 만들어졌는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 **서버** \> **데이터베이스 사용 가능 그룹**으로 이동합니다. 적절한 DAG를 선택하면 새로 만든 DAG 네트워크가 세부 정보 창에 표시됩니다.

  - 셸에서 다음 명령을 실행하여 DAG 네트워크가 만들어졌는지 확인하고 DAG 네트워크 구성 정보를 표시합니다.
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## 자세한 내용

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd298131\(v=exchg.150\))

