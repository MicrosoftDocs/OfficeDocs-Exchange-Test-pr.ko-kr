---
title: '메일 라우팅에 대 한 Active Directory 사이트를 사용 하 여 계획: Exchange 2013 Help'
TOCTitle: 메일 라우팅에 대 한 Active Directory 사이트를 사용 하 여 계획
ms:assetid: 0f697cee-bcaa-4c69-b80c-7a2afd1817d2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996299(v=EXCHG.150)
ms:contentKeyID: 52058052
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 라우팅에 대 한 Active Directory 사이트를 사용 하 여 계획

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-05-21_

Microsoft Exchange Server 2013에서는 Active Directory 사이트 및 DAG(데이터베이스 사용 가능 그룹)를 라우팅 경계로 인식합니다. 그러나 Exchange 2013은 계속 Active Directory 사이트 토폴로지를 사용하여 조직 내의 개별 DAG 또는 사이트에서 Exchange 서버 간에 메시지가 전송되는 방법을 결정합니다. 자세한 내용은 [메일 라우팅](mail-routing-exchange-2013-help.md)을 참조하십시오.

사서함 서버의 전송 서비스는 Exchange 조직 내의 메시지 전송 기능을 제공합니다. Exchange 2013만으로 이루어진 조직을 배포하거나 Exchange Server 2010 조직만으로 이루어진 조직에 Exchange 2013을 도입하는 경우 포리스트에 라우팅을 설정하기 위해 추가 구성이 필요하지 않습니다.

**목차**

How Exchange 2013 uses Active Directory site membership

Determine Active Directory site membership

Overview of IP site links

Exchange 2013 server placement in Active Directory sites

## Exchange 2013에서 Active Directory 사이트 구성원을 사용하는 방법

Exchange 2013은 사이트 인식 응용 프로그램입니다. 사이트 인식 응용 프로그램은 Active Directory를 쿼리하여 자체의 Active Directory 사이트 구성원과 다른 서버의 사이트 구성원을 확인할 수 있습니다. Exchange 2013에서는 사이트 구성원을 사용하여 Active Directory 쿼리 처리에 사용할 도메인 컨트롤러와 글로벌 카탈로그 서버를 확인합니다. 또한 Exchange를 실행하는 서버가 다른 Exchange 서버의 Active Directory 사이트 구성원을 확인해야 하는 경우 Active Directory를 쿼리하여 사이트 이름을 검색할 수 있습니다.

Exchange 2013에서 Microsoft Exchange Active Directory 토폴로지 서비스는 Exchange 서버 개체의 사이트 특성을 업데이트합니다. Active Directory 사이트 구성원은 서버 개체 특성이므로 Exchange에서는 서버 주소가 Active Directory 사이트와 연결된 서브넷인지 확인하기 위해 DNS를 쿼리할 필요가 없습니다. Exchange 서버 개체의 Active Directory 사이트 특성을 스탬프 처리하면 구독된 Edge 전송 서버와 같이 도메인 구성원이 아닌 서버에 Active Directory 사이트 구성원을 할당할 수도 있습니다.

Exchange 2013 서버는 Active Directory 사이트 구성원 정보를 다음과 같이 사용합니다.

  - **메일 전송**   Exchange 2013 사서함 서버의 사서함 전송 제출 서비스는 Active Directory 사이트 구성원 정보를 사용하여 같은 Active Directory 사이트에 있는 다른 Exchange 2013 사서함 서버를 확인합니다. 원본 사서함 서버가 DAG에 속하지 않거나 DAG에 여러 Active Directory 사이트가 포함되지 않는 경우에는 원본 사서함 서버의 사서함 전송 제출 서비스에서 같은 Active Directory 사이트에 있는 Exchange 2013 사서함 서버의 전송 서비스로 라우팅 및 전송할 메시지를 전송합니다.

  - **메일 배달**   Exchange 2013 사서함 서버의 전송 서비스는 받는 사람 확인을 수행하고 Active Directory를 쿼리하여 전자 메일 주소가 받는 사람 계정과 일치하게 합니다. 받는 사람 계정 정보에는 사용자 사서함 데이터베이스의 FQDN(정규화된 도메인 이름)이 포함됩니다. 전송 서비스는 Active Directory를 쿼리해 사용자 사서함 데이터베이스의 Active Directory 사이트를 확인합니다. 사서함 데이터베이스가 DAG에 속하지 않으면 해당 사서함 서버로 메시지를 배달합니다. 그렇지 않으면 배달을 위해 대상 사서함 서버와 동일한 사이트에 있는 다른 사서함 서버로 메시지를 릴레이합니다.

  - **메시지 라우팅**   Exchange 2013 사서함 서버의 전송 서비스는 Active Directory에서 정보를 검색하여 조직 내에서 메일을 라우팅할 방식을 결정합니다. Exchange 2013에서는 *배달 그룹* 개념을 사용하여 메시지를 라우팅할 위치와 방법을 결정합니다. 대상에 따라 메시지를 Exchange 2013 사서함 서버의 사서함 전송 배달 서비스 또는 전송 서비스나, 이전 Exchange 버전을 실행 중인 허브 전송 서버로 라우팅할 수 있습니다. 자세한 내용은 [메일 라우팅](mail-routing-exchange-2013-help.md)을 참조하십시오.

  - **통합 메시징 메시지 전송**   Exchange 2013 사서함 서버의 통합 메시징 서비스는 Active Directory 사이트 구성원 정보를 사용하여 같은 Active Directory 사이트에 있는 다른 사서함 서버를 찾습니다. 통합 메시징 서비스는 같은 Active Directory 사이트 내 사서함 서버의 전송 서비스로 라우팅할 메시지를 전송합니다. 전송 서비스 서버는 받는 사람 확인을 수행하고 Active Directory를 쿼리하여 전화 번호, E.164 번호 또는 SIP 주소를 받는 사람 계정에 일치시킵니다. 받는 사람 확인이 완료되면 전송 서비스는 일반적인 전자 메일 메시지와 같은 방식으로 대상 사서함에 메시지를 배달합니다.

  - **클라이언트 액세스 서버에 대한 클라이언트 연결**   클라이언트 액세스 서버는 사용자 연결 요청을 받으면 Active Directory를 쿼리하여 사용자 사서함을 호스트하는 사서함 서버를 확인합니다. 그리고 나서 해당 사서함 서버의 Active Directory 사이트 구성원을 검색하고 연결을 사서함 서버에 프록시합니다.

## Active Directory 사이트 구성원 확인

Active Directory 클라이언트는 할당된 IP 주소를 Active Directory 사이트 및 서비스에 정의되어 있으며 Active Directory 사이트에 연결된 서브넷에 일치시켜 사이트 구성원을 추정합니다. 그런 다음 이 정보를 사용하여 해당 사이트에 있는 도메인 컨트롤러 및 글로벌 카탈로그 서버를 확인하고, 인증 및 권한 부여를 위해 이러한 디렉터리 서버와 통신합니다. Exchange 2013에서는 우선적으로 Exchange 2013 서버와 같은 사이트에 있는 디렉터리 서버에서 받는 사람에 대한 정보를 검색하면서 이 관계를 활용합니다.

동일한 Active Directory 사이트에 속하는 모든 컴퓨터는 믿을 수 있는 고속 네트워크 연결을 통해 정상적으로 연결되어 있다고 간주됩니다. 기본적으로 Active Directory 포리스트가 처음 배포될 때는 `Default-First-Site-Name`이라는 단일 사이트가 있습니다. 관리자가 다른 사이트를 수동으로 구성하지 않으면 포리스트의 모든 서버 및 클라이언트 컴퓨터가 `Default-First-Site-Name`의 구성원으로 간주됩니다.

둘 이상의 사이트가 정의되면 Active Directory 관리자는 조직에 있는 서브넷을 정의한 후 해당 서브넷을 Active Directory 사이트에 연결해야 합니다.

Microsoft Exchange Active Directory 토폴로지 서비스는 서버가 시작될 때 Exchange 서버 개체의 사이트 구성원 특성을 확인합니다. 사이트 특성을 업데이트해야 할 경우 Microsoft Exchange Active Directory 토폴로지 서비스는 해당 특성을 새 값으로 스탬프 처리합니다. Microsoft Exchange Active Directory 토폴로지 서비스는 사이트 특성 값을 15분 간격으로 확인하고 사이트 구성원이 변경되었으면 해당 값을 업데이트합니다. Microsoft Exchange Active Directory 토폴로지 서비스는 네트워크 로그온 서비스를 사용하여 현재 사이트 구성원을 확인합니다. 네트워크 로그온 서비스는 사이트 구성원을 5분 간격으로 업데이트합니다. 즉, 사이트 구성원이 변경되는 시점과 사이트 특성이 새 값으로 스탬프 처리되는 시점은 최고 20분의 차이가 있을 수 있습니다.

## IP 사이트 링크의 개요

Active Directory 사이트 간 관계는 IP 사이트 링크에 의해 정의됩니다. IP 사이트 링크는 두 개 이상의 Active Directory 사이트로 구성됩니다. 링크에 속하는 모든 Active Directory 사이트는 동일한 비용으로 통신합니다. IP 사이트 링크 속성에는 순위 할당, 일정 및 간격이 포함됩니다. 일정 및 간격 속성은 Active Directory 복제 빈도를 결정하는 데만 사용됩니다. Exchange 2013에서는 비용 할당을 사용하여 대상에 대한 경로가 여러 개 있을 때 트래픽이 이동되는 최저 비용 경로를 결정합니다. 경로 순위는 전송 경로에 포함된 모든 사이트 링크의 순위를 집계하여 결정합니다. Active Directory 관리자는 사용 가능한 다른 연결과 비교한 상대 네트워크 속도와 사용 가능한 대역폭을 기반으로 링크에 비용을 할당합니다.

기본적으로 사서함 서버의 전송 서비스는 항상 다른 Active Directory 사이트의 사서함 서버에 있는 메일 전송 배달 서비스 또는 전송 서비스에 직접 연결하려고 합니다. 전송되는 메시지는 사이트 링크 경로에 포함된 각 사서함 서버의 전송 서비스를 통해 릴레이되지 않습니다. 그러나 라우팅 경로의 중간 Active Directory 사이트에 있는 사서함 서버는 다음 시나리오에서 메시지 릴레이를 수행할 수 있습니다.

  - 허브 사이트가 최저 비용의 라우팅 경로에 존재할 경우 사서함 서버 간의 직접 릴레이는 수행되지 않습니다. Active Directory 사이트를 허브 사이트로 구성하여 메시지가 대상 서버로 릴레이되기 전에 허브 사이트로 라우팅되도록 할 수 있습니다. 허브 사이트는 이 항목 뒷부분에서 설명합니다.

  - Exchange 2013에서는 대상 Active Directory 사이트에 대한 통신이 실패할 때 IP 사이트 링크 정보에서 파생된 라우팅 경로를 사용합니다. 대상 Active Directory 사이트의 사서함 서버가 응답하지 않으면 라우팅 경로에 따라 Active Directory 사이트의 사서함 서버와 연결될 때까지 최저 비용 라우팅 경로를 따라 메시지가 배달되지 않습니다. 메시지는 해당 Active Directory 사이트에 대기되며 큐는 다시 시도 상태가 됩니다. 이 작업을 *실패 시점의 큐*라고 합니다.

  - DAG가 없는 Exchange 2013 조직에서는 사서함 서버의 전송 서비스가 IP 사이트 링크 정보를 사용하여 여러 명의 받는 사람에게 보내진 메시지의 라우팅을 최적화할 수도 있습니다. 사서함 서버는 받는 사람에 대한 라우팅 경로에서 포크에 도달할 때까지 메시지의 분기를 지연시킵니다. 분기된 메시지는 개별 라우팅 경로의 포크를 나타내는 Active Directory 사이트의 사서함 서버에 의해 각 받는 사람 대상으로 릴레이됩니다. 이 기능을 *지연된 팬아웃*이라고 합니다.

## 허브 사이트 지정

**Set-AdSite** cmdlet을 사용하여 Active Directory 사이트를 허브 사이트로 구성할 수 있습니다. 두 대의 전송 서버 간 최저 비용 라우팅 경로에 허브 사이트가 있을 경우 메시지는 대상 서버로 릴레이되기 전에 처리를 위해 허브 사이트로 라우팅됩니다. 이러한 라우팅 동작을 수행하려면 두 전송 서버 사이의 최저 비용 라우팅 경로에 허브 사이트가 있어야 합니다. 이 구성은 Active Directory 사이트 간에 방화벽이 존재하여 SMTP 통신의 직접 릴레이를 차단하는 경우처럼 네트워크 토폴로지에 의해 요구될 때만 사용해야 합니다. 자세한 내용은 [Active Directory의 Exchange 메일 라우팅 설정 구성](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md)을 참조하십시오.

## IP 사이트 링크에 Exchange 관련 비용 설정

Exchange 관리 셸에서 **Set-AdSiteLink** cmdlet을 사용하여 Active Directory IP 사이트 링크에 대한 Exchange 관련 비용을 구성할 수 있습니다. Exchange 관련 비용은 Active Directory 할당 비용 대신 사용되어 Exchange 라우팅 경로를 결정하는 별도의 특성입니다. 이 구성은 Active Directory IP 사이트 링크 비용으로 최적의 Exchange 메시지 라우팅 토폴로지를 얻지 못할 때 유용합니다. 자세한 내용은 [Active Directory의 Exchange 메일 라우팅 설정 구성](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md)을 참조하십시오.

## IP 사이트 링크에 메시지 크기 제한 설정

기본적으로 Exchange 2013에서는 다른 Active Directory 사이트에 있는 사서함 서버 간에 릴레이되는 메시지에 최대 메시지 크기 제한을 적용하지 않습니다. **Set-AdSiteLink** cmdlet을 사용하여 Active Directory IP 사이트 링크에 최대 메시지 크기를 구성할 경우 최저 비용 라우팅 경로의 Active Directory 사이트 링크에 구성되어 있는 최대 메시지 크기 제한보다 큰 메시지에 대해 라우팅 시 배달 못 함 보고서(NDR)가 생성됩니다. 이러한 구성은 대역폭이 낮은 연결을 통해 통신해야 하는 원격 Active Directory 사이트로 보내는 메시지의 크기를 제한하는 데 유용합니다.

## Active Directory 사이트에 Exchange 2013 서버 배치

Exchange 2013 서버 간 메시지 라우팅이 올바르게 수행되려면 포리스트에 배포된 모든 Exchange 서버가 한 Active Directory 사이트에 속해야 합니다. 할당한 IP 주소가 Active Directory 사이트와 올바르게 연결된 서브넷에 있는지 확인하십시오.

Active Directory 사이트 토폴로지의 Exchange 2013 서버 배치를 계획하는 첫 번째 단계는 현재 토폴로지를 문서화하는 것입니다. 문서화에는 다음이 포함되어야 합니다.

  - 사이트

  - 서브넷 및 해당 사이트 연결

  - IP 사이트 링크 및 해당 구성원 사이트

  - IP 사이트 링크 순위

  - 각 사이트의 디렉터리 서버

  - 실제 네트워크 연결

  - 방화벽 위치

이러한 개체를 다이어그램으로 나타낸 후에 Exchange 서버의 배치를 계획합니다. 서버 위치를 결정할 때는 다음 정보를 고려합니다.

  - 사서함 서버는 Active Directory 조회를 위해 글로벌 카탈로그 서버와 직접 통신해야 합니다.

  - 부하 분산 및 내결함성을 제공하기 위해 각 Active Directory 사이트에 둘 이상의 사서함 서버를 배포하는 것이 좋습니다.

  - DAG 및 사이트 복구

  - 사서함 서버의 통합 메시징 서비스는 사서함으로 배달하기 위해 사서함 서버의 전송 서비스로 음성 메일 메시지를 전송합니다. 통합 메시징 통화 라우터 서비스를 실행 중인 클라이언트 액세스 서버는 허브 사이트에 위치하거나 IP 또는 VoIP(Voice over IP) 게이트웨이, IP PBX(Private Branch Exchange), SIP 사용 가능 PBX 또는 SBC(Session Border Controller) 가까이에 위치할 수 있습니다. 클라이언트 액세스 서버와 동일한 사이트 구성원을 포함하는 사서함 서버의 전송 서비스는 전송할 음성 메일 메시지를 받은 다음 조직의 다른 사서함 서버에 있는 전송 서비스로 메시지를 라우팅합니다.

  - 클라이언트 액세스 서버는 Exchange에 원격으로 액세스하는 사용자에게 Exchange 조직에 대한 연결 지점을 제공합니다. 클라이언트 액세스 서버는 사서함 서버가 있는 각 Active Directory 사이트에 배포되어야 합니다.

Exchange 2013 서버 배치를 계획한 후에는 통신 흐름의 향상을 위해 Active Directory 사이트 토폴로지를 수정할 수 있는 영역을 식별할 수 있습니다. IP 사이트 링크 및 사이트 링크 비용을 조정하여 메일 배달을 최적화할 수 있습니다. Active Directory 토폴로지가 효율적이면 Exchange 2013을 지원하기 위해 변경하지 않아도 됩니다.

