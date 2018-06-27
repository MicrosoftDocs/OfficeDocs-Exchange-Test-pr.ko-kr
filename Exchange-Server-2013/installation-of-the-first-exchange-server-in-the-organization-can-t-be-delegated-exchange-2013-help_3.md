---
title: '서버는 조직에서이 아니어야 첫번째 Exchange 설치 위임: Exchange 2013 Help'
TOCTitle: 서버는 조직에서이 아니어야 첫번째 Exchange 설치 위임
ms:assetid: d451581b-6161-4e95-99f1-03dac8313fae
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.delegatedmailboxfirstinstall(v=EXCHG.150)
ms:contentKeyID: 50484225
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 서버는 조직에서이 아니어야 첫번째 Exchange 설치 위임

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2014-11-05_

로그온한 사용자의 계정에는 조직에 첫 번째 Exchange 2013 서버를 설치하는 데 필요한 권한이 없기 때문에 Microsoft Exchange Server 2013 설치를 계속할 수 없습니다.

Exchange 2013 설치 시 위임을 사용하여 후속 서버 역할을 설치할 수 있지만 로그온한 사용자가 조직의 첫 번째 Exchange 2013 서버를 설치할 때 엔터프라이즈 관리자 Windows 보안 그룹의 구성원이어야 합니다. 이는 Exchange 2013 설치 시 Active Directory의 Exchange 조직 컨테이너에 개체가 생성되고 구성되기 때문에 필요합니다.


> [!NOTE]
> Exchange 2013에 대한 Active Directory 스키마를 준비하지 않은 경우에는 로그온한 사용자가 스키마 관리자 Windows 보안 그룹에도 속해 있어야 합니다. 또한 스키마 관리자 Windows 그룹의 구성원인 다른 사용자가 Exchange 2013을 설치하기 전에 Active Directory 스키마를 준비할 수 있습니다.



이 문제를 해결하려면 로그온한 사용자를 엔터프라이즈 관리자 보안 그룹의 구성원으로 추가합니다. 또는 엔터프라이즈 관리자 보안 그룹의 구성원인 계정에 로그인합니다. 그런 다음 Exchange 2013 설치 프로그램을 다시 실행합니다.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

