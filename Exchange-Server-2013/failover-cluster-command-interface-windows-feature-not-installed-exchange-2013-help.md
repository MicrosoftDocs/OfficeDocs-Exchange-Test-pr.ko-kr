---
title: '장애 조치 클러스터 명령 인터페이스 Windows 기능이 설치 되지 않았습니다: Exchange 2013 Help'
TOCTitle: 장애 조치 클러스터 명령 인터페이스 Windows 기능이 설치 되지 않았습니다
ms:assetid: 0d839514-5ab7-497d-8945-41392b4c3980
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.rsatclusteringcmdinterfaceinstalled(v=EXCHG.150)
ms:contentKeyID: 51407665
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 장애 조치 클러스터 명령 인터페이스 Windows 기능이 설치 되지 않았습니다

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2014-12-03_

로컬 컴퓨터에 필요한 Windows 기능이 없으므로 Microsoft Exchange Server 2013 설치 프로그램이 설치를 계속할 수 없습니다. 이 Windows 기능을 설치해야 Exchange 2013이 설치를 계속할 수 있습니다.

Exchange 2013 설치 컴퓨터에 설치를 계속 하기 전에 **장애 조치 클러스터 명령 인터페이스** Windows 기능을 설치 해야 합니다.

이 컴퓨터에 Windows 기능을 설치하려면 다음을 수행합니다. 이 업데이트의 설치 완료를 위해 다시 부팅을 해야 하는 경우 Exchange 2013 설치 프로그램을 종료하고 다시 부팅한 다음 설치 프로그램을 다시 시작해야 합니다.


> [!NOTE]
> 추가 Windows 기능이나 업데이트를 설치해야 Exchange 2013 설치 프로그램이 설치를 계속할 수 있습니다. 필요한 Windows 기능 및 업데이트의 전체 목록을 보려면 <A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 필수 구성 요소</A>를 확인하세요.



1.  로컬 컴퓨터에서 Windows PowerShell을 엽니다.

2.  필요한 Windows 기능을 설치 하려면 다음 명령을 실행 합니다.
    
        Install-WindowsFeature RSAT-Clustering-CmdInterface

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

