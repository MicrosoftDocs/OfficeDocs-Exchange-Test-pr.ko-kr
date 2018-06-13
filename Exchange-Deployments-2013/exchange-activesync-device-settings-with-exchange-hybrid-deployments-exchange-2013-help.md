---
title: 'Exchange 하이브리드 배포를 사용한 Exchange ActiveSync 장치 설정: Exchange 2013 Help'
TOCTitle: Exchange 하이브리드 배포를 사용한 Exchange ActiveSync 장치 설정
ms:assetid: 77f7cd72-2a8a-467e-9ffd-b93f5eeb2f69
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn931281(v=EXCHG.150)
ms:contentKeyID: 64365530
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 하이브리드 배포를 사용한 Exchange ActiveSync 장치 설정

 

_**적용 대상:**Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-01-27_

사서함이 Exchange 온-프레미스 조직에서 Office 365로 이동한 경우 Exchange ActiveSync 장치가 자동으로 다시 구성됩니다. Exchange ActiveSync가 Office 365에서 새 사서함 위치를 찾아 Office 365에 직접 전달하도록 해당 구성을 업데이트합니다. Exchange ActiveSync 장치는 Office 365로 리디렉션된 후 온-프레미스 Exchange 서버에 연결을 시도하지 않습니다. 아래를 비롯한 몇 가지 예외적인 경우 외에는 사용자가 해당 장치를 수동으로 설정하지 않아도 메일이 정상적으로 작동합니다.

Office 365로 사서함을 이동하려면 [하이브리드 배포에서 온-프레미스 및 Exchange Online 조직 간의 사서함 이동](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md)을 참조하세요.

하이브리드 배포에 대한 자세한 내용은 [Exchange Server 하이브리드 배포](exchange-server-hybrid-deployments-exchange-2013-help.md)를 참조하세요.

자동 전환을 사용하려면 온-프레미스 서버에서 Exchange 2010, Exchange 2013 Exchange 2016 이상의 최신 릴리스가 실행되고 있어야 합니다. 하이브리드 배포를 설정하려면 [하이브리드 구성 마법사](hybrid-configuration-wizard-exchange-2013-help.md)도 사용해야 합니다. Exchange ActiveSync 리디렉션 기능은 조직 관계 개체에 설정된 웹에서 Outlook 대상 URL을 사용합니다. 이 개체는 하이브리드 구성 마법사를 실행할 때 구성됩니다.

조직이 위에 나열된 요구 사항을 충족하는 경우에는 사용자의 사서함이 이동되면 추가 구성 없이 모바일 장치가 Office 365로 자동으로 리디렉션됩니다. 최상의 환경을 위해 사용자의 모바일 장치에서 최신 버전의 운영 체제 및 전자 메일 클라이언트를 실행하는지 확인합니다. Android 운영 체제를 실행하는 것과 같은 일부 모바일 장치는 리디렉션하는 데 예상보다 오래 걸릴 수 있습니다. 또한 일부 장치는 Exchange에서 전송된 Exchange ActiveSync 451 리디렉션 명령을 제대로 해석하지 못할 수 있습니다. 이러한 장치에서는 여전히 사용자가 해당 전자 메일 계정을 수동으로 다시 구성하거나 다시 만들어야 합니다. 장치에서 Exchange ActiveSync 451 리디렉션을 지원하는지 여부에 대한 질문이 있는 경우 장치 제조업체에 문의하세요.

Exchange ActiveSync 자동 리디렉션은 다음 시나리오에서 지원되지 않습니다.

  - Office 365에서 온-프레미스 Exchange 조직으로 사서함을 이동하는 경우

  - 온-프레미스 Exchange 조직 간에 사서함을 이동하는 경우

  - Exchange 2007 서버에서 Office 365로 사서함을 이동하는 경우

