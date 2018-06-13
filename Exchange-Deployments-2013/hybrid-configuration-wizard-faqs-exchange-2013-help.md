---
title: '하이브리드 구성 마법사 FAQ: Exchange 2013 Help'
TOCTitle: 하이브리드 구성 마법사 FAQ
ms:assetid: e911e6e0-e36e-4430-ac36-c745a10d6c26
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt488940(v=EXCHG.150)
ms:contentKeyID: 72045785
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 하이브리드 구성 마법사 FAQ

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft는 하이브리드 배포의 구성을 단순화하고, 하이브리드 구성의 유연성을 높이고, 항상 최신 버전의 환경을 실행할 수 있도록 하는 새로운 하이브리드 구성 마법사를 배포했습니다. 이 버전의 하이브리드 마법사는 Exchange 2016 및 Exchange 2013 릴리스(누적 업데이트 10부터)에 기본적으로 제공되어 있지만 이전 Exchange 2013 CU(누적 업데이트) 또는 Exchange 2010 SP3(서비스 팩 3)를 실행하는 경우에도 새 마법사를 다운로드할 수 있습니다.

Office 365 하이브리드 구성 마법사에 대한 자세한 내용은 Exchange 팀 블로그의 [Introducing the Microsoft Office 365 Hybrid Configuration Wizard(Microsoft Office 365 하이브리드 구성 마법사 소개)](http://go.microsoft.com/fwlink/?linkid=717122) 및 [Office 365 Hybrid Configuration Wizard for Exchange 2010(Exchange 2010용 Office 365 하이브리드 구성 마법사)](http://go.microsoft.com/fwlink/?linkid=730687)을 참조하세요.

Office 365 하이브리드 구성 마법사를 다운로드하려면 [http://aka.ms/HybridWizard](http://aka.ms/hybridwizard)로 이동합니다.

## 고객이 자주 묻는 질문

  - Q: 어떤 버전의 Exchange새 하이브리드 구성 마법사를 지원하나요?  
    A: 다음 요구 사항을 충족하는 하나 이상의 서버가 있어야 합니다.
    
      - **Exchange 2010**Exchange 2010 SP3를 사서함, 허브 전송 및 클라이언트 액세스 서버 역할을 실행하는 하나 이상의 서버에 설치해야 합니다. 또한 Exchange 2010 SP3에 대해 사용할 수 있는 사용 가능한 최신 업데이트 롤업을 설치하는 것이 좋습니다.
    
      - **Exchange 2013** 최신 Exchange 2013 CU를 사서함 및 클라이언트 액세스 서버 역할을 실행하는 하나 이상의 서버에 설치해야 합니다. 최신 CU를 설치할 수 없으면 바로 이전 릴리스도 지원됩니다. 이전 CU는 지원되지 않습니다.
    
      - **Exchange 2016**Exchange 2016 릴리스를 사서함 서버 역할을 실행하는 하나 이상의 서버에 설치해야 합니다.
    
    예를 들어 온-프레미스 조직에 Exchange 2013 CU8을 설치했다고 가정하면, 사용할 수 있는 가장 최근 Exchange 2013 릴리스는 CU10입니다. 지원되는 하이브리드 구성에 남아 있으려면, Exchange 2013 서버를 적어도 CU9로 업그레이드해야 합니다. 하지만 CU10으로 업그레이드하는 것이 가장 좋습니다.
    
    누적 업데이트는 분기별로 릴리스됩니다. 따라서 서버에 최신 누적 업데이트를 적용하면 업그레이드를 완료해야 할 추가 시간이 주기적으로 필요한 경우 유연성을 추가로 확보할 수 있습니다.

<!-- end list -->

  - Q: 이 하이브리드 구성 마법사가 Exchange 2007?  
    A: 조직에서 Exchange 2007을 사용하여 하이브리드 배포를 구성할 수 있습니다. 그러나 이렇게 하려면 위의 요구 사항을 충족하는 Exchange 2013 실행 서버를 하나 이상 배포해야 합니다.

<!-- end list -->

  - Q: 새 하이브리드 구성 마법사에서 거부할 수 있나요?  
    A: 아니요. 새 하이브리드 구성 마법사는 현재 Exchange 2010, Exchange 2013 및 Exchange 2016에서 지원되는 유일한 마법사입니다.

<!-- end list -->

  - Q: 새 하이브리드 구성 마법사를 사용하여 현재 Exchange 2010 하이브리드 구성을 Exchange 2013 또는 Exchange 2016으로 업그레이드할 수 있나요?  
    A: 예. 현재 하이브리드 구성 마법사 요구 사항을 충족하는 서버가 하나 이상 있는지 확인하고 실행합니다. 이 마법사는 하이브리드 구성의 현재 상태를 파악하고 업그레이드 프로세스를 원활하게 진행합니다.

