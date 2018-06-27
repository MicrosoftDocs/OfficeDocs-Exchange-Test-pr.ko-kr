---
title: '현재 계정 Active Directory 도메인에 로그인 하지 않습니다.: Exchange 2013 Help'
TOCTitle: 현재 계정 Active Directory 도메인에 로그인 하지 않습니다.
ms:assetid: 0e229d10-605a-420f-bf8b-58a7fcb5b259
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.loggedontodomain(v=EXCHG.150)
ms:contentKeyID: 50482505
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 현재 계정 Active Directory 도메인에 로그인 하지 않습니다.

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2014-12-02_

현재 계정 Active Directory 도메인에 로그온 하지 않기 때문에 Microsoft Exchange Server 2013 설치를 계속할 수 없습니다. Exchange Server 2013을 설치 하는 데 필요한 사용 권한이 있는 Active Directory 계정을 사용 하 여 로그인 해야 합니다.

설치를 위해서는 Exchange 2013을 설치할 때 로그인한 사용자에게 Active Directory의 개체를 만들고 수정할 수 있는 권한이 있어야 합니다. 사용자의 조직에서 Exchange 2013 설치 프로그램을 처음으로 실행하는 경우 사용하는 계정은 Schema Admins 및 Enterprise Admins 그룹의 구성원이어야 합니다. Exchange 2013 최초 설치 프로그램 실행을 위해 Active Directory가 준비되었기 때문에 이러한 권한이 필요합니다. Active Directory가 준비된 후 추가 Exchange 2013 서버 설치를 위해 사용하는 계정은 Organization Management 역할 그룹의 구성원이어야 합니다.

이 문제를 해결하려면 로그온한 사용자에게 적절한 권한을 부여하거나 해당 권한을 가진 계정으로 로그온한 다음 Exchange 2013 설치 프로그램을 다시 실행하십시오.


> [!IMPORTANT]
> Exchange 2013의 포리스트 간 설치는 지원되지 않습니다. Exchange 2013을 설치할 때는 Active Directory 포리스트의 구성원인 계정을 사용하십시오.



문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

