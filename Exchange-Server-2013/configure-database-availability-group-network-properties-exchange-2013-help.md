---
title: '데이터베이스 가용성 그룹 네트워크 속성 구성: Exchange 2013 Help'
TOCTitle: 데이터베이스 가용성 그룹 네트워크 속성 구성
ms:assetid: 41197639-988f-476c-9788-51d5191a7dce
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd297927(v=EXCHG.150)
ms:contentKeyID: 50482960
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 가용성 그룹 네트워크 속성 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-31_

각 DAG(데이터베이스 사용 가능 그룹) 네트워크에서는 DAG 네트워크 이름, DAG 네트워크의 설명 필드, DAG 네트워크에 사용되는 서브넷 목록 및 DAG 네트워크를 복제에 사용할 수 있는지 여부를 비롯한 여러 가지 속성을 구성할 수 있습니다.

DAG와 관련된 다른 관리 작업에 대한 자세한 내용은 [데이터베이스 가용성 그룹 관리](managing-database-availability-groups-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "데이터베이스 가용성 그룹" 항목

  - DAG에 대한 자동 네트워크 구성을 사용하지 않도록 설정한 경우에만 DAG 네트워크를 구성할 수 있습니다. DAG에 대해 자동 네트워크 구성을 사용하지 않도록 설정하는 방법에 대한 자세한 단계는 [데이터베이스 가용성 그룹 속성 구성](configure-database-availability-group-properties-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 데이터베이스 가용성 그룹 네트워크 속성 구성

1.  EAC에서 **서버** \> **데이터베이스 사용 가능 그룹**으로 이동합니다.

2.  구성하려는 DAG를 선택하고 세부 정보 창의 구성할 DAG 네트워크 아래에서 다음을 선택합니다.
    
      - **복제 사용 안 함** 또는 **복제 사용**   DAG 네트워크에 대한 복제 설정을 구성합니다.
    
      - **제거**   DAG 네트워크를 제거합니다. DAG 네트워크를 제거하려면 먼저 DAG 네트워크에서 연결된 모든 서브넷을 제거해야 합니다.
    
      - **세부 정보 보기**   DAG의 이름, 설명 및 연결된 서브넷 등 DAG 네트워크 속성을 구성합니다. 또한 해당 서브넷과 관련된 네트워크 인터페이스를 보고, DAG 네트워크에 대해 복제를 사용하거나 사용하지 않도록 설정할 수 있습니다.

## 셸을 사용하여 데이터베이스 가용성 그룹 네트워크 속성 구성

이 예에서는 서브넷 10.0.0.0 및 서브넷 마스크 255.0.0.0을 DAG1이라는 DAG의 MapiDagNetwork 네트워크에 추가합니다.

```powershell
Set-DatabaseAvailabilityGroupNetwork -Subnets 10.0.0.0/8 -Identity DAG1\MapiDagNetwork
```

## 작동 여부는 어떻게 확인합니까?

DAG 네트워크가 성공적으로 구성되었는지 확인하려면 다음을 수행하십시오.

  - 셸에서 다음 명령을 실행하여 DAG 네트워크 구성 설정을 표시하고 DAG 네트워크가 성공적으로 구성되었는지 확인합니다.
    
    ```powershell
Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List
```

## 자세한 내용

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/ko-kr/library/dd298131\(v=exchg.150\))

