---
title: '새로운 소식 통합 메시징에 대 한 Exchange 2013: Exchange 2013 Help'
TOCTitle: 새로운 소식 통합 메시징에 대 한 Exchange 2013
ms:assetid: a444ef2d-d893-408e-adf9-c9d8a8b07593
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150545(v=EXCHG.150)
ms:contentKeyID: 50483814
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 새로운 소식 통합 메시징에 대 한 Exchange 2013

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013에서는 새로운 기능의 추가와 아키텍처의 변경을 통해 이전 릴리스의 Exchange가 향상되었습니다. Exchange 2013의 UM(통합 메시징)에는 Exchange 2010 및 Exchange 2007과 동일한 기능 집합이 포함되어 있지만 통합 메시징은 더 이상 별도의 서버 역할이 아닙니다. 이것은 이제 Exchange 2013에서 제공되는 음성 관련 기능의 구성 요소입니다.

## 음성 아키텍처의 변경 사항

Exchange 2013의 아키텍처는 Exchange 2010 및 Exchange 2007의 아키텍처와 달라졌습니다. 이전 버전의 Exchange UM에서는 통합 메시징의 모든 구성 요소가 UM 서버 역할이 설치된 서버에 포함되어 있었습니다. Exchange 2013에서는 모든 통합 메시징 구성 요소가 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행하는 클라이언트 액세스 서버 및 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버 간에 분할됩니다. 들어오는 호출을 사서함 서버로 프록시하는 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행하는 클라이언트 액세스 서버를 제외하고 통합 메시징에 대한 서비스 및 작업자 프로세스를 포함한 모든 기능은 각 사서함 서버에 있습니다. 자세한 내용은 [아키텍처 변경 사항](voice-architecture-changes-exchange-2013-help.md) 항목을 참조하십시오.

## IPv6 지원

IPv6(인터넷 프로토콜 버전 6)은 가장 최근 버전의 IP(인터넷 프로토콜)입니다. IPv6에서는 이전 버전의 IP인 IPv4의 많은 결점이 수정되었습니다. Exchange 2010에서와 마찬가지로 Exchange 2013 클라이언트 액세스 및 사서함 서버는 IPv6 네트워크를 완전히 지원합니다. 자세한 내용은 [통합 메시징의 IPv6 지원](ipv6-support-in-unified-messaging-exchange-2013-help.md) 항목을 참조하십시오.

## UCMA 4.0 API에 대한 지원

Exchange 2010 서비스 팩 1부터 통합 메시징 역할은 UCMA(Unified Communications Managed API) v2.0을 통해 신호 및 미디어를 처리합니다. 따라서 UCMA 2.0은 Exchange 2010 UM 설치의 필수 조건입니다. UCMA 2.0은 관리자가 별도로 다운로드하여 Exchange 2010 SP1 이상 버전이 실행되는 통합 메시징 서버에 수동으로 설치합니다. Exchange 2013의 경우에는 UCMA 4.0이 필요합니다. 하지만 UM 서버가 더 이상 Exchange 2013의 별도 서버 역할이 아니기 때문에 이제 클라이언트 액세스 및 사서함 서버에 UCMA 4.0이 필요합니다.

UCMA 4.0에서는 TTS(텍스트 음성 변환) 및 ASR(자동 음성 인식) 모두에 대해 동일한 버전의 음성 엔진을 사용하는 것과 같은 통합 메시징의 새로운 기능을 지원합니다. Exchange 2013에 사용되는 플랫폼인 .NET 4.0은 단일 설치 관리자 파일을 포함하며 Exchange 2010 및 Exchange 2007 UM 서버의 이전 버전과의 호환성을 지원합니다.

Exchange 2010 SP2 및 SP1에서는 통합 메시징 서버에 서비스 팩을 설치하기 전에 UCMA 2.0을 설치해야 합니다. 그러나 UCMA 2.0에는 몇 가지 제한이 있었습니다. UCMA 4.0에서는 이러한 결점이 많이 수정되었습니다. Exchange Server 2013에서 UM은 계속 UCMA를 사용합니다. 하지만 최신 버전의 UCMA로 전환하면 다음과 같은 이점이 있습니다.

  - UCMA의 최신 빌드에는 핫픽스와 패치가 통합되어 있습니다.

  - UCMA에는 Exchange Server 2013에서 사용하는 플랫폼인 .NET 4.0이 필요합니다. 하지만 UCMA 2.0은.NET 4.0을 지원하지 않습니다.

  - UCMA 4.0은 IPv6을 지원합니다.

  - UCMA 4.0의 배포가 단순화되고 자동화되었습니다. Exchange 2013 설치 프로그램은 UCMA 4.0에 대한 단일 검사를 수행합니다.

  - UCMA 4.0 설치에는 Exchange 2013에 대한 모든 필수 구성 요소가 포합됩니다.


> [!NOTE]
> UCMA 4.0은 Exchange 2013을 설치할 때 설치됩니다. UCMA 4.0 및 설치 요구 사항에 대한 자세한 내용은 <A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 필수 구성 요소</A> 항목을 참조하십시오. 최신 버전의 UCMA로 업그레이드하려면 먼저 프로그램 추가/제거를 사용하여 설치된 UCMA의 이전 버전을 제거해야 합니다.



## 음성 메일 미리 보기의 향상된 기능

Speech Engine 11.0 및 UCMA 4.0을 통해 Exchange Server 2013 UM에 대한 음성 관련 서비스가 일부 향상되었습니다. 문법 생성 및 언어 개선이 포함되어 있습니다. 또한 Exchange Server 2013에서 UM에는 UI에 대한 몇 가지 향상과 음성 메일 미리 보기의 신뢰성과 정확성을 위한 향상이 포함되어 있습니다. 자세한 내용은 [음성 메일 미리 보기 향상 기능](voice-mail-preview-enhancements-exchange-2013-help.md) 항목을 참조하십시오.

## 향상된 발신자 번호 지원

이전 릴리스의 Exchange 통합 메시징에서 호출을 수행하는 UM 서버는 발신자 번호를 사용하여 발신자의 신원 조회를 시도했습니다. 이 검색이 Active Directory 및 사서함에 저장된 UM 사용자의 개인 연락처까지 확장되었습니다.

Exchange 사용자는 발신자 번호로 Exchange 또는 개인 연락처를 식별할 수 없는 문제점을 겪는 경우가 있습니다. 지금까지는 Exchange UM의 기본 연락처 폴더만이 이 검색에 사용되었습니다. 하지만 Exchange Server 2013 사용자에게는 외부 소셜 네트워크에서 수집한 연락처나 사용자가 직접 만든 고유 폴더의 연락처가 있을 수 있습니다. Exchange 2013에서는 외부 소셜 네트워크로부터의 연락처 수집을 지원하고, 같은 사람을 참조하는 여러 연락처를 지능적으로 연결하며, 이 데이터를 사용하여 사람 중심(연락처 중심이 아니라) 보기를 제공합니다. 외부 네트워크에서 수집된 연락처는 사용자가 만든 추가 연락처 폴더와 함께 연락처 폴더에 저장됩니다. Exchange 2013 UM의 기능에서는 검색 범위가 확장되어 사용자의 다른 Exchange 및 직접 만든 개인 연락처 폴더까지 포함됩니다.

발신자 번호 조회는 연락처 집계와 통합되어 있으므로 외부 연락처를 검색합니다. Null이 아닌 값을 표시하고 이를 사용하는 PersonID 속성은 같은 사람과 연결된 연락처에 대한 중복 일치를 방지함으로써 발신자 번호 확인에 대한 사용자 환경을 향상시킵니다. 두 결과의 PersonID 속성이 동일하므로 UM은 단일 연락처와 일치하는 것으로 간주합니다.

## 음성 플랫폼 및 음성 인식 향상의 향상된 기능

Exchange Server 2013 UM에서는 다음을 비롯하여 음성 플랫폼 및 음성 인식에 대한 기능이 향상되었습니다.

  - 음성 메일 미리 보기의 향상된 기능 및 정확성 개선

  - [Microsoft 음성 플랫폼 – 런타임 (버전 11.0)](https://go.microsoft.com/fwlink/p/?linkid=253196)을 지원 합니다.

  - 조직의 시스템 사서함을 사용하여 음성 문법 생성

Exchange 통합 메시징은 정적 및 동적 음성 문법을 사용하여 명령, 전체 주소 목록의 연락처 이름 및 사용자 사서함에 있는 개인 연락처의 이름을 인식합니다. 현재 Exchange Server 2013에서 Microsoft Exchange 통합 메시징 서비스를 실행하는 모든 사서함 서버는 서버에 설치된 모든 UM 언어에 대한 문법을 생성하여 디렉터리에 저장합니다. 모든 사서함 서버는 가능한 모든 문법을 저장합니다. 이러한 문법은 설치된 다이얼 플랜, 자동 전화 교환 및 UM 언어의 수를 기준으로 생성됩니다.

문법 파일은 음성 인식 프로세스에 대한 입력으로 사용되며 주기적으로 생성됩니다. Exchange 2007 및 Exchange 2010의 GGG.exe 명령을 사용하면 예약 업데이트를 기다리지 않고 문법 파일을 직접 업데이트할 수 있습니다. Exchange Server 2013에서는 UM에 대한 ASR 문법 생성 확장성 문제를 해결하기 위해 통합 메시징 서버 역할이 설치된 서버에서 음성 GAL 문법 생성이 더 이상 수행되지 않습니다. 대신 조직의 중재 사서함을 호스트하는 Microsoft Exchange 통합 메시징 서비스를 실행 중인 사서함 서버에서 사서함 도우미를 사용하여 정기적으로 수행됩니다. GAL 음성 문법 파일은 조직의 중재 사서함에 저장되었다가 나중에 해당 Exchange 조직의 모든 사서함 서버로 다운로드됩니다. 기본적으로 사서함 도우미는 24시간마다 실행됩니다. **Set-MailboxServer** cmdlet을 사용하여 빈도를 조정할 수 있습니다.

## Cmdlet 업데이트

Exchange 2013의 경우 많은 UM cmdlet을 Exchange 2010에서 가져왔지만 일부 cmdlet은 변경되었으며 새 기능을 위한 새로운 cmdlet이 추가되었습니다. 자세한 내용은 [통합된 메시징 cmdlet 업데이트](unified-messaging-cmdlet-updates-exchange-2013-help.md) 항목을 참조하십시오.

