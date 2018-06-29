---
title: 'ExecutionPolicy GPO가 정의됨: Exchange 2013 Help'
TOCTitle: ExecutionPolicy GPO가 정의됨
ms:assetid: 63de83e2-9a6b-4f57-85b9-df445bea18dd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.powershellexecutionpolicycheckset(v=EXCHG.150)
ms:contentKeyID: 61203320
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ExecutionPolicy GPO가 정의됨

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2016-12-15_

**ExecutionPolicy** GPO(그룹 정책 개체)가 다음 정책 중 하나 또는 둘 다를 정의하므로 Microsoft Exchange Server 2013 설치를 계속할 수 없습니다.

  - **MachinePolicy**

  - **UserPolicy**

정책을 정의한 방법은 관계가 없으며 정책이 정의되었다는 사실 자체가 중요합니다.

Exchange 2013 설치 프로그램을 실행하면 WMI(Windows Management Instrumentation) 서비스가 중지되고 사용하지 않도록 설정됩니다. 이러한 정책 중 하나가 정의되어 있는 경우 Windows PowerShell 스크립트를 실행하려면 WMI 서비스를 사용하도록 설정해야 합니다. 정책이 정의된 상태에서 WMI 서비스가 중지되면 설치가 실패하며 서버가 일치하지 않는 상태로 남아 있게 됩니다.

설치를 계속하려면 **ExecutionPolicy** GPO에서 **MachinePolicy** 또는 **UserPolicy** 정의를 일시적으로 제거해야 합니다.

**ExecutionPolicy** GPO **MachinePolicy** 또는 **UserPolicy** 정의 제거 하는 방법에는 내용은 [기술 자료 문서 KB981474](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=981474)를 참조 하십시오.


> [!NOTE]
> 이 기술 자료 문서는 Exchange 2010용으로 작성되었지만 Exchange 2013 누적 업데이트 및 서비스 팩에도 적용됩니다.



문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

