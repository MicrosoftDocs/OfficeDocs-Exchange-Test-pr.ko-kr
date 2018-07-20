---
title: '사용 권한 를 분할 하는 Active Directory 도메인 컨트롤러에 설치 지원 되지 않습니다.: Exchange 2013 Help'
TOCTitle: 사용 권한 를 분할 하는 Active Directory 도메인 컨트롤러에 설치 지원 되지 않습니다.
ms:assetid: 977e3758-5e09-40a2-80c1-fe344b1d8a2a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.installondcinadsplitpermissionmode(v=EXCHG.150)
ms:contentKeyID: 50483723
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 권한 [InstallOnDCInADSplitPermissionMode]를 분할 하는 Active Directory 도메인 컨트롤러에 설치 지원 되지 않습니다.

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2012-11-12_

Microsoft Exchange Server 2013 설치 프로그램이 사용자가 Active Directory 도메인 컨트롤러에서 설치를 실행하려고 하며, 다음 중 하나가 참인 것을 감지했습니다.

  - Exchange 조직이 이미 Active Directory 사용 권한 분할로 구성되어 있습니다.

  - Exchange 2013 설치 프로그램에서 Active Directory 사용 권한 분할 옵션을 선택했습니다.

Exchange 조직이 Active Directory 사용 권한 분할로 구성되어 있는 경우 Exchange 2013을 도메인 컨트롤러에 설치하는 것은 지원되지 않습니다.

Exchange 2013을 도메인 컨트롤러에 설치하려면 Exchange 조직을 RBAC(역할 기반 액세스 제어) 사용 권한 분할 또는 사용 권한 공유로 구성해야 합니다shared permissions.


> [!IMPORTANT]
> Exchange 2013은 Active Directory 도메인 컨트롤러에 설치하지 않는 것이 좋습니다. 자세한 내용은 <A href="installing-exchange-on-a-domain-controller-is-not-recommended-exchange-2013-help.md">도메인 컨트롤러에서 Exchange 설치 [WarningInstallExchangeRolesOnDomainController] 하지 않기</A>를 참조하십시오.



Active Directory 사용 권한 분할을 계속 사용하려면 Exchange 2013을 구성원 서버에 설치해야 합니다.

Exchange 2013에서의 사용 권한 분할 및 공유에 대한 자세한 내용은 다음 항목을 참조하십시오.

[분할 권한 이해](understanding-split-permissions-exchange-2013-help.md)

[Exchange 2013 분할 된 사용 권한 구성](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)

[Exchange 2013 공유 사용 권한 구성](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

