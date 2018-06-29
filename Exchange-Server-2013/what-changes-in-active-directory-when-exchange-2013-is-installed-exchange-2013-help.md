---
title: 'Exchange 2013이 설치될 때 Active Directory에서 변경되는 내용: Exchange 2013 Help'
TOCTitle: Exchange 2013이 설치될 때 Active Directory에서 변경되는 내용
ms:assetid: 07386078-6103-49a2-8698-2d41db9cec95
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn750898(v=EXCHG.150)
ms:contentKeyID: 62371362
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013이 설치될 때 Active Directory에서 변경되는 내용

 

_**적용 대상:**Exchange Server, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-05-26_

Exchange 2013을 설치할 경우 Active Directory 포리스트 및 도메인이 변경됩니다. Exchange는 Exchange 서버, 사서함 및 조직의 Exchange와 관련된 기타 개체에 대한 정보를 저장할 수 있도록 이 작업을 수행합니다. 이러한 변경은 Exchange 2013 명령줄 설정 중에 Exchange 2013 설치 마법사를 실행하거나 *PrepareSchema*, *PrepareAD* 및 *PrepareDomains* 명령([Active Directory 및 도메인 준비](prepare-active-directory-and-domains-exchange-2013-help.md) 에서 이러한 명령 사용 방법 참조)을 실행할 때 수행됩니다. Exchange에서 Active Directory에 대해 변경한 내용이 알고 싶은 경우 이 항목이 도움이 될 것입니다. 여기서는 Exchange가 각 Active Directory 준비 단계에서 수행하는 작업에 대해 설명합니다.

Exchange에 대해 Active Directory를 준비하기 위해 수행해야 하는 작업에는 세 단계가 있습니다.

  - Extend the Active Directory schema

  - Prepare Active Directory containers, objects, and other items

  - Prepare Active Directory domains

이러한 세 단계를 모두 수행하면 Active Directory 포리스트는 Exchange 2013에 맞게 준비됩니다. [설치 마법사를 사용하여 Exchange 2013 설치](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)를 읽어 Exchange 2013 설치 방법에 대해 자세히 알아볼 수 있습니다.

## Active Directory 스키마 확장

Active Directory 스키마를 확장하면 클래스, 특성 및 기타 항목이 추가되고 업데이트됩니다. 이러한 변경 내용은 Exchange에서 Exchange 조직에 대한 정보를 저장하기 위한 컨테이너 및 개체를 만들기 위해 필요합니다. Exchange에서는 Active Directory 스키마를 많이 변경하므로 이 단계와 주로 관련된 항목이 제공됩니다. 스키마에 대해 수행된 모든 변경 내용을 확인하려면 [Exchange 2013 Active Directory 스키마 변경 사항](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)을 참조하세요.

이 단계는 Active Directory 포리스트의 첫 번째 Exchange 2013 서버에서 Exchange 2013 설치 마법사를 실행할 때 자동으로 수행됩니다. 또한 포리스트의 첫 번째 Exchange 2013 서버에서 *PrepareSchema* 명령(또는 선택적으로 *PrepareAD* 명령)을 사용하여 Exchange 2013 명령줄 설치를 실행할 때도 수행됩니다. 스키마를 확장하는 방법에 대한 자세한 내용은 [Active Directory 및 도메인 준비](prepare-active-directory-and-domains-exchange-2013-help.md)에서 [Extend the Active Directory schema](prepare-active-directory-and-domains-exchange-2013-help.md)을 참조하세요.

Exchange에서 스키마 확장을 마치면 **ms-Exch-Schema-Version-Pt** 특성에 저장된 스키마 버전을 설정합니다. Active Directory 스키마가 성공적으로 확장되었는지 확인하려면 이 특성에 저장된 값을 확인할 수 있습니다. 이 특성의 값이 설치한 Exchange 2013 릴리스에 대해 나열된 스키마 버전과 일치하면 스키마가 성공적으로 확장된 것입니다. Exchange 릴리스 목록 및 이 특성 값을 확인하는 방법은 [Active Directory 및 도메인 준비](prepare-active-directory-and-domains-exchange-2013-help.md)의 [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) 섹션을 참조하세요.

## Active Directory 컨테이너, 개체 및 기타 항목 준비

스키마가 확장되면 다음 단계는 Exchange가 Active Directory에 정보를 저장하는 데 사용하는 컨테이너, 특성 및 기타 항목을 모두 추가하는 것입니다. 이 단계에서 변경한 대부분의 내용은 전체 Active Directory 포리스트에 적용됩니다. 설치 중에 *PrepareAD* 명령이 실행된 로컬 Active Directory 도메인은 비교적 적게 변경됩니다.

다음은 Active Directory 포리스트에서 변경된 내용입니다.

  - Microsoft Exchange 컨테이너는 아직 없는 경우 CN=Services,CN=Configuration,DC=\<*root domain*\> 아래에 만들어집니다.

  - 다음 컨테이너 및 개체는 아직 없는 경우 CN=\<*organization name*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> 아래에 만들어집니다.
    
      - CN=Address Lists Container
    
      - CN=AddressBook Mailbox Policies
    
      - CN=Addressing
    
      - CN=Administrative Groups
    
      - CN=Approval Applications
    
      - CN=Auth Configuration
    
      - CN=Availability Configuration
    
      - CN=Client Access
    
      - CN=Connections
    
      - CN=ELC Folders Container
    
      - CN=ELC Mailbox Policies
    
      - CN=ExchangeAssistance
    
      - CN=Federation
    
      - CN=Federation Trusts
    
      - CN=Global Settings
    
      - CN=Hybrid Configuration
    
      - CN=Mobile Mailbox Policies
    
      - CN=Mobile Mailbox Settings
    
      - CN=Monitoring Settings
    
      - CN=OWA Mailbox Policies
    
      - CN=Provisioning Policy Container
    
      - CN=Push Notification Settings
    
      - CN=RBAC
    
      - CN=Recipient Policies
    
      - CN=Remote Accounts Policies Container
    
      - CN=Retention Policies Container
    
      - CN=Retention Policy Tag Container
    
      - CN=ServiceEndpoints
    
      - CN=System Policies
    
      - CN=Team Mailbox Provisioning Policies
    
      - CN=Transport Settings
    
      - CN=UM AutoAttendant Container
    
      - CN=UM DialPlan Container
    
      - CN=UM IPGateway Container
    
      - CN=UM Mailbox Policies
    
      - CN=Workload Management Settings

  - 다음 컨테이너 및 개체는 아직 없는 경우 CN=Transport Settings,CN=\<*Organization Name*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> 아래에 만들어집니다.
    
      - CN=Accepted Domains
    
      - CN=ControlPoint Config
    
      - CN=DNS Customization
    
      - CN=Interceptor Rules
    
      - CN=Malware Filter
    
      - CN=Message Classifications
    
      - CN=Message Hygiene
    
      - CN=Rules
    
      - CN=MicrosoftExchange329e71ec88ae4615bbc36ab6ce41109e

  - 사용 권한은 Active Directory의 구성 파티션 전체에 대해 설정됩니다.

  - Rights.ldf 파일을 가져옵니다. 이 파일은 Exchange를 설치하고 Active Directory를 구성하는 데 필요한 사용 권한을 추가합니다.

  - Microsoft Exchange Security Groups OU(조직 구성 단위)가 포리스트의 루트 도메인에 만들어지고 사용 권한이 할당됩니다.

  - 다음 관리 역할 그룹이 아직 없는 경우 Microsoft Exchange Security Groups OU 내에 만들어집니다.
    
      - Compliance Management
    
      - Delegated Setup
    
      - Discovery Management
    
      - Help Desk
    
      - Hygiene Management
    
      - Organization Management
    
      - Public Folder Management
    
      - Recipient Management
    
      - Records Management
    
      - Server Management
    
      - UM Management
    
      - 보기 전용 Organization Management

  - Microsoft Exchange Security Groups OU에서 만들어진 새 관리 역할 그룹(Active Directory에 USG(유니버설 보안 그룹)으로 표시)이 CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> 컨테이너에 저장된 **otherWellKnownObjects** 특성에 추가됩니다.

  - 통합 메시징 음성 보낸 사람 연락처가 루트 도메인의 Microsoft Exchange System Objects 컨테이너에 만들어집니다.

  - *PrepareAD* 명령이 실행된 도메인이 Exchange 2013에 대해 준비됩니다. Exchange에 대해 Active Directory 도메인을 준비하기 위해 수행된 작업에 대한 자세한 내용은 Preparing Active Directory domains를 참조하세요.

  - Exchange 조직 개체의 **msExchProductId** 속성이 설정됩니다. Active Directory 스키마가 성공적으로 확장되었는지 확인하려면 이 속성에 저장된 값을 확인할 수 있습니다. 이 속성의 값이 설치한 Exchange 2013 릴리스에 대해 나열된 스키마 버전과 일치하면 스키마가 성공적으로 확장된 것입니다. Exchange 릴리스 목록 및 이 속성 값을 확인하는 방법은 [Active Directory 및 도메인 준비](prepare-active-directory-and-domains-exchange-2013-help.md)의 [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) 섹션을 참조하세요.

## Active Directory 도메인 준비

Exchange에 대해 Active Directory를 준비하는 최종 단계는 Exchange 서버가 설치되거나 사서함 사용 사용자가 위치할 모든 Active Directory 도메인을 준비하는 것입니다. 이 단계는 *PrepareAD* 명령이 실행된 도메인에서 자동으로 수행됩니다.

다음은 Active Directory 도메인에서 변경된 내용입니다.

  - Microsoft Exchange System Objects 컨테이너가 아직 없는 경우 Active Directory의 루트 도메인 파티션에 만들어집니다.

  - Exchange Servers, Organization Management 및 Authenticated Users 보안 그룹에 대한 Microsoft Exchange System Objects 컨테이너에 대해 사용 권한이 설정됩니다.

  - Exchange Install Domain Servers 도메인 글로벌 그룹이 현재 도메인에 만들어지고 Microsoft Exchange System Objects 컨테이너에 추가됩니다.

  - Exchange Install Domain Servers 그룹이 루트 도메인의 Exchange Servers USG에 추가됩니다.

  - Exchange Servers USG 및 Organization Management USG에 대한 도메인 수준에서 사용 권한이 할당됩니다.

  - DC=\<*root domain*\> 아래의 Microsoft Exchange System Objects 컨테이너에서 **objectVersion** 속성이 설정됩니다. Active Directory 스키마가 성공적으로 확장되었는지 확인하려면 이 속성에 저장된 값을 확인할 수 있습니다. 이 속성의 값이 설치한 Exchange 2013 릴리스에 대해 나열된 스키마 버전과 일치하면 스키마가 성공적으로 확장된 것입니다. Exchange 릴리스 목록 및 이 속성 값을 확인하는 방법은 [Active Directory 및 도메인 준비](prepare-active-directory-and-domains-exchange-2013-help.md)의 [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) 섹션을 참조하세요.

