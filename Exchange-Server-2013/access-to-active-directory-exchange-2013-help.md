---
title: 'Active Directory에 대 한 액세스: Exchange 2013 Help'
TOCTitle: Active Directory에 대 한 액세스
ms:assetid: 61080b45-8bce-4c23-b744-ed264d5f0b7d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998561(v=EXCHG.150)
ms:contentKeyID: 50483230
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory에 대 한 액세스

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013에서는 Active Directory 디렉터리 서비스 데이터베이스에 모든 구성 및 받는 사람 정보를 저장합니다. Exchange 2013을 실행하는 컴퓨터에서 Exchange 조직의 구성 정보 및 받는 사람 정보가 필요한 경우 Active Directory에 쿼리하여 해당 정보에 액세스해야 합니다. Active Directory이 제대로 작동하기 위해서는 Exchange 2013 서버가 사용 가능해야 합니다.

이 항목에서는 Exchange 2013에 액세스할 수 있도록 Active Directory이 Active Directory에 정보를 저장하고 검색하는 방법에 대해 설명합니다. 또한 삭제된 Exchange 2013 Active Directory 개체를 복구하려는 경우 알아야 할 문제에 대해서도 설명합니다.

## Active Directory에 저장된 Exchange 정보

Active Directory 데이터베이스는 다음 섹션에서 설명하는 세 가지 유형의 논리 파티션에 정보를 저장합니다.

  - 스키마 파티션

  - 구성 파티션

  - 도메인 파티션

## 스키마 파티션

스키마 파티션에는 다음 두 가지 유형의 정보가 저장됩니다.

  - **스키마 클래스**는 Active Directory에 만들어지고 저장될 수 있는 모든 유형의 개체를 정의합니다.

  - **스키마 특성**은 Active Directory에 저장되는 개체를 설명하는 데 사용될 수 있는 모든 속성을 정의합니다.

첫 번째 Exchange 2013 서버 역할을 포리스트에 설치하거나 Active Directory 준비 과정을 실행하는 경우 Active Directory 준비 과정에서는 여러 클래스와 특성을 Active Directory 스키마에 추가합니다. 스키마에 추가된 클래스는 에이전트 및 커넥터와 같은 Exchange 관련 개체를 만드는 데 사용됩니다. 스키마에 추가된 특성은 Exchange 관련 개체와 메일 사용 가능 사용자 및 그룹을 구성하는 데 사용됩니다. 이러한 특성은 Microsoft Office Outlook Web Access 설정 및 Microsoft Exchange UM(통합 메시징) 설정과 같은 속성을 포함합니다. 포리스트의 모든 도메인 컨트롤러와 글로벌 카탈로그 서버에는 스키마 파티션의 완전한 복제본이 있습니다.

Exchange 2013의 스키마 수정 사항에 대한 자세한 내용은 [Exchange 2013 Active Directory 스키마 변경 사항](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)을 참조하십시오.

## 구성 파티션

구성 파티션은 포리스트 전반의 구성 정보를 저장합니다. 이 구성 정보에는 Active Directory 사이트, Exchange 전역 설정, 전송 설정 및 사서함 정책의 구성이 포함됩니다. 각 유형의 구성 정보는 구성 파티션의 컨테이너에 저장되고, Exchange 구성 정보는 구성 파티션의 서비스 컨테이너 아래 하위 폴더에 저장됩니다. 이 컨테이너에 저장된 정보는 다음을 포함합니다.

  - 주소 목록

  - 주소록 사서함 정책

  - 관리 그룹

  - 클라이언트 액세스 설정

  - 연결

  - 모바일 사서함 설정

  - 전역 설정

  - 모니터링 설정

  - 시스템 정책

  - 보존 정책 컨테이너

  - 전송 설정

포리스트의 모든 도메인 컨트롤러와 글로벌 카탈로그 서버에는 구성 파티션의 완전한 복제본이 있습니다.

## 도메인 파티션

도메인 파티션에서는 정보를 Active Directory 관리자가 만든 조직 구성 단위 및 기본 컨테이너에 저장합니다. 이러한 컨테이너에는 도메인별 개체가 포함되어 있습니다. 이 데이터에는 해당 도메인의 컴퓨터, 사용자 및 그룹에 대한 정보 및 Exchange 시스템 개체가 포함됩니다. Exchange 2013을 설치할 때 Exchange는 Exchange 기능을 지원하기 위해 이 파티션의 개체를 업데이트합니다. 이 기능은 받는 사람 정보를 저장하는 방법 및 해당 정보에 액세스하는 방법에 영향을 줍니다.

각 도메인 컨트롤러에는 신뢰할 수 있는 도메인에 대한 도메인 파티션의 완전한 복제본이 있습니다. 포리스트의 모든 글로벌 카탈로그 서버에는 해당 포리스트의 모든 도메인 파티션에 있는 정보의 하위 집합이 포함되어 있습니다.

## Exchange 2013에서 Active Directory의 정보에 액세스하는 방법

Exchange 2013에서는 Active Directory API를 사용하여 Active Directory에 저장된 정보에 액세스합니다. Microsoft ExchangeActive Directory 토폴로지 서비스는 모든 Exchange 2013 서버 역할에서 실행됩니다. 이 서비스는 모든 Active Directory 파티션에서 정보를 읽습니다. Exchange 2013 서버에서 검색되는 데이터를 캐시하고 사용하여 조직 내 모든 Active Directory 서비스의 Exchange 사이트 위치를 찾습니다.

토폴로지 및 서비스 검색에 대한 자세한 내용은 [메일 라우팅에 대 한 Active Directory 사이트를 사용 하 여 계획](planning-to-use-active-directory-sites-for-routing-mail-exchange-2013-help.md)을 참조하십시오.

Exchange 2013은 Active Directory 사이트 인식 응용 프로그램으로, 네트워크 트래픽을 최적화하기 위해 Exchange 서버와 동일한 사이트에 위치한 디렉터리 서버와 통신합니다. 다른 Exchange 2013 서버 역할에 대한 정보 및 받는 사람 정보를 검색하려면 각각의 Active Directory 조직 서버 역할이 Exchange 2013와 통신해야 합니다. 다음 섹션에서는 각 서버 역할이 수집한 데이터에 대해 설명합니다.

기본적으로 Exchange 2013 서버는 시작될 때마다 자체 사이트 안에서 임의로 선택된 도메인 컨트롤러와 글로벌 카탈로그 서버에 바인딩됩니다. Exchange 관리 셸에서 **Get-ExchangeServer** cmdlet을 사용하여 선택한 디렉터리 서버를 볼 수 있습니다. 또한 **Set-ExchangeServer** cmdlet을 사용하여 Exchange 2013 서버에서 바인딩해야 할 도메인 컨트롤러의 정적 목록 또는 제외해야 할 도메인 컨트롤러 목록을 구성할 수도 있습니다.


> [!IMPORTANT]
> Windows Server 2008 도메인 컨트롤러는 읽기 전용 디렉터리 서버로 구성할 수 있습니다. 이러한 구성은 인증 및 권한 부여를 위해 도메인 컨트롤러나 글로벌 카탈로그 서버를 원격 사이트에 배포하되 해당 사이트의 관리자가 Active Directory에 대한 변경 내용을 기록하지 못하게 하려는 경우에 유용합니다. 하지만 읽기 전용 디렉터리 서버만 있는 사이트에는 Exchange 2013 서버를 배포할 수 없습니다.



## 사서함 서버 역할

사서함 서버 역할은 사서함 사용자에 대한 구성 정보를 Active Directory에 저장합니다. 또한 Exchange 2013에서는 사서함 서버에 Exchange 2010의 모든 기존 서버 구성 요소가 포함됩니다. 클라이언트 액세스 프로토콜, 전송 서비스, 사서함 데이터베이스 및 통합 메시징이 이에 해당합니다. 사서함 서버는 해당 서버에서 활성 사서함에 대한 모든 작업을 처리합니다.

## 클라이언트 액세스 서버 역할

Exchange 2013에서 클라이언트 액세스 서버는 인증, 제한된 리디렉션 및 프록시 서비스를 제공합니다. 클라이언트 액세스 서버 자체는 데이터 렌더링을 수행하지 않습니다. 클라이언트 액세스 서버는 상태 비저장 씬 서버입니다. 클라이언트 액세스 서버에서는 어떠한 항목도 큐에 추가되거나 저장되지 않습니다. 클라이언트 액세스 서버는 일반적인 클라이언트 액세스 프로토콜을 모두 제공합니다. HTTP, POP, IMAP 및 SMTP가 이에 해당합니다.

## 삭제된 Exchange 개체 복구

Active Directory 휴지통은 백업에서 Active Directory 데이터를 복원하거나, AD DS(Active Directory 도메인 서비스)를 다시 시작하거나, 도메인 컨트롤러를 다시 부팅하지 않고도 실수로 삭제한 Active Directory 개체를 보존 및 복구하는 기능을 향상시켜 디렉터리 서비스 가동 중지 시간을 최소화하는 데 도움이 됩니다.

삭제된 Exchange와 관련된 Active Directory 개체의 복구에 대해 이해해야 할 가장 중요한 점은 Exchange 개체가 격리 상태에 있지 않다는 것입니다. 예를 들어 사용자의 메일을 사용하도록 설정하면 현재 Exchange 구성을 기반으로 하여 사용자에 대해 여러 가지 다양한 정책과 링크가 계산됩니다. 삭제된 Exchange 구성 또는 받는 사람 개체를 복원할 때 발생할 수 있는 두 가지 문제는 다음과 같습니다.

  - **충돌**   일부 Exchange 특성은 포리스트에서 고유해야 합니다. 예를 들어 프록시(전자 메일) 주소는 두 명의 다른 사용자에 대해 동일해서는 안 됩니다. Active Directory는 프록시 주소의 고유성을 적용하지 않습니다. 고유성은 Exchange 관리 도구에서 검사합니다. 또한 Exchange 전자 메일 주소 정책은 결정적 규칙을 기반으로 하여 프록시 주소 할당 시 가능한 충돌 문제를 자동으로 해결합니다. 따라서 Exchange 사용자 개체를 복원하고 그에 따라 프록시 주소 또는 고유해야 하는 기타 특성과의 충돌이 발생할 수 있습니다.

  - **잘못된 구성**   Exchange에는 다양한 정책 또는 설정을 할당하는 자동화된 규칙이 있습니다. 받는 사람을 삭제한 다음 규칙 또는 정책을 변경할 경우 Exchange 사용자 개체를 복원하면 사용자가 잘못된 정책 또는 더 이상 존재하지 않는 정책에 할당될 수 있습니다.

다음 지침은 삭제된 Exchange 관련 개체를 복구할 때 문제를 최소화하는 데 도움이 됩니다.

  - Exchange 관리 도구를 사용하여 Exchange 구성 개체를 삭제한 경우에는 개체를 복원하지 마십시오. 대신 Exchange 관리 도구(Exchange 관리 센터 또는 Exchange 관리 셸)를 사용하여 개체를 다시 만듭니다.

  - Exchange 관리 도구를 사용하지 않고 Exchange 구성 개체를 삭제한 경우에는 가능한 한 빨리 개체를 복구하십시오. 삭제 후 시스템에서 수행된 관리 및 구성 변경 사항이 많을수록 개체를 복원할 때 구성이 잘못될 가능성이 높습니다.

  - 삭제된 Exchange 받는 사람(연락처, 사용자 또는 메일 그룹)을 복구하는 경우에는 복구된 개체와 관련된 충돌과 오류를 자세히 모니터링하십시오. Exchange 정책 또는 받는 사람과 관련된 다른 정책이 삭제된 후 모니터링할 경우에는 제대로 구성되도록 복원된 받는 사람에게 현재 정책을 다시 적용해야 합니다.

## 자세한 내용

[Active Directory Recycle Bin 단계별 가이드](https://go.microsoft.com/fwlink/p/?linkid=178720)

[Active Directory 관리 센터 향상 된 기능 (수준 100) 소개](https://go.microsoft.com/fwlink/p/?linkid=267641)

[고급 Active Directory 관리 센터 (레벨 200)를 사용 하 여 AD DS 관리](https://go.microsoft.com/fwlink/p/?linkid=267642)

