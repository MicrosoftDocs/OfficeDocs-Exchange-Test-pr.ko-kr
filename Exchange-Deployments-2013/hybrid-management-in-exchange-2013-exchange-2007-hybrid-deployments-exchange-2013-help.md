---
title: 'Exchange 2013/Exchange 2007 하이브리드 배포에서 하이브리드 관리: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2007 하이브리드 배포에서 하이브리드 관리
ms:assetid: 4b4370d5-1645-4b44-b4e0-c585fcaf970f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn151299(v=EXCHG.150)
ms:contentKeyID: 54651850
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2007 하이브리드 배포에서 하이브리드 관리

이 항목은 진행 중입니다.  

_**적용 대상:**Exchange Online, Exchange Server, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Exchange 2007 온-프레미스 조직에서 Microsoft Exchange Server 2013을 실행하는 서버를 설치할 경우 Exchange 2013 관리 도구가 서버에 자동으로 설치됩니다. 다음 도구를 사용하여 온-프레미스 Exchange 및 Exchange Online 조직 둘 다에 대해 하이브리드 기능을 구성 및 관리할 수 있습니다.

  - **Exchange 관리 센터**   EAC는 사용하기 쉬운, Exchange 2013에 포함된 웹 기반 관리 콘솔로서 온-프레미스, 온라인 또는 하이브리드 Exchange 배포에 최적화되어 있습니다. EAC는 Exchange Server 2007 관리에 사용한 인터페이스인 EMC(Exchange 관리 콘솔) 및 ECP(Exchange 제어판)를 보완합니다.

  - **Exchange 관리 셸**Exchange 관리 셸은 Windows PowerShell 기반 명령줄 인터페이스입니다.

## Exchange 관리 센터

EAC를 사용하여 온-프레미스 Exchange 서버와 Exchange Online 조직 모두에서 여러 배포 작업 및 가장 일반적인 일상 관리 작업을 수행할 수 있습니다. EAC는 모든 Exchange 2013 서버에 기본적으로 설치됩니다. 또한 EAC는 웹 기반 관리 콘솔이므로, 네트워크의 다른 컴퓨터에서 웹 브라우저를 사용하여 액세스하거나 ECP 가상 디렉터리 URL을 사용하여 인터넷을 통해 액세스할 수도 있습니다.


> [!IMPORTANT]
> Exchange 2007 사서함 서버에 있는 사서함이 있는 계정(예: 도메인 관리자 계정)을 사용하여 EAC에 액세스할 경우 EAC에 액세스하려면 브라우저에서 다음 주소를 사용해야 합니다.<BR>https://<EM>&lt;FQDN of Exchange 2013 Client Access server&gt;</EM>/ECP? ExchClientVer=15



Office 365 프레미스 간 탐색 탭을 선택하여 EAC에서 Exchange Online 조직에 액세스합니다. 프레미스 간 탐색 기능을 사용하면 Exchange Online 조직과 온-프레미스 Exchange 조직 간에 쉽게 전환할 수 있습니다. 하이브리드 배포를 구성한 경우 Office 365 탭을 선택하면 Exchange Online 조직 및 받는 사람 개체를 관리할 수 있습니다. Exchange Online 조직이 없는 경우 Office 365 링크를 선택하면 Office 365 등록 페이지가 표시됩니다.

EAC에 대한 자세한 내용은 [Exchange 2013의 Exchange 관리 센터](https://technet.microsoft.com/ko-kr/library/jj150562\(v=exchg.150\))를 참조하십시오.

## Exchange 관리 셸

Exchange 관리 셸을 사용하면 EAC에서 수행하는 모든 작업과 Exchange 관리 셸에서만 수행 가능한 일부 추가 작업을 수행할 수 있습니다. Exchange 관리 셸은 Exchange 2013 관리 도구가 설치될 때 컴퓨터에 설치되는 Windows PowerShell 스크립트 및 cmdlet 모음입니다. 이 스크립트와 cmdlet은 Exchange 관리 셸 아이콘을 사용하여 Exchange 관리 셸을 열 경우에만 로드됩니다. Windows PowerShell을 직접 여는 경우 Exchange 스크립트 및 cmdlet이 로드되지 않으며 온-프레미스 조직을 관리할 수 없게 됩니다.


> [!NOTE]
> 아래 Exchange Online 조직에 수동으로 연결하는 방식과 비슷하게 로컬 온-프레미스 조직에 수동으로 Windows&nbsp;PowerShell을 연결할 수도 있습니다. 하지만 온-프레미스 Exchange 서버를 관리하기 위해 Exchange 관리 셸을 열려면 Exchange 관리 셸 아이콘을 사용하는 것이 좋습니다.



관리 도구가 설치된 컴퓨터에서 Exchange 관리 셸 아이콘을 사용하여 Exchange 관리 셸을 열 경우 온-프레미스 조직을 관리할 수 있습니다. 그러나 이 아이콘을 사용하여 Exchange 관리 셸을 여는 경우 Exchange Online 조직을 관리할 수 없습니다. 이는 Exchange 관리 셸 아이콘을 사용하여 Exchange 관리 셸을 열면 로컬 Exchange 서버에 자동으로 연결되기 때문입니다.

Windows PowerShell을 이용하여 Exchange Online 조직을 관리하고자 하는 경우, Exchange 관리 셸 아이콘을 경유하지 않고 Windows PowerShell을 직접 열어야 합니다. Windows PowerShell을 열 때에는 연결하고자 하는 장소를 수동으로 지정할 수 있습니다. 수동으로 연결하는 경우, Office 365 테넌트 조직에 관리자 계정을 지정한 후 명령을 실행하여 연결을 생성할 수 있습니다. 연결이 구축되면 실행 권한을 가진 Exchange cmdlet을 사용할 수 있게 됩니다. 자세한 내용은 [Windows PowerShell 사용](http://go.microsoft.com/fwlink/p/?linkid=209660)을 참조하세요.

Exchange 관리 셸이 처음인 경우 Exchange 관리 셸 작업 방식, 명령 구문 등에 대한 기본적인 사항에 대해 알아보려면 [PowerShell을 사용 하 여 Exchange 2013 (Exchange 관리 셸)](https://technet.microsoft.com/ko-kr/library/bb123778\(v=exchg.150\))을 참조하세요.

