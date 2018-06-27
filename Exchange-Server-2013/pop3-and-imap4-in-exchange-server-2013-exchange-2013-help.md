---
title: 'Exchange Server 2013의 POP3 및 IMAP4: Exchange 2013 Help'
TOCTitle: POP3 및 IMAP4
ms:assetid: a7dc91ee-2919-4db3-ae9c-cd665d2e09ea
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657728(v=EXCHG.150)
ms:contentKeyID: 50483896
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013의 POP3 및 IMAP4

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-08-16_

Exchange Server 2013의 POP3 및 IMAP4 프로토콜 간 차이점과 다양한 전자 메일 프로그램에서 Exchange 2013 사서함에 액세스하도록 옵션을 구성하는 방법에 대해 자세히 알아보세요.

기본적으로 POP3 및 IMAP4는 Exchange Server 2013에서 사용하지 않도록 설정되어 있습니다. 이러한 프로토콜을 계속 사용하는 POP3 클라이언트를 지원하려면 Microsoft Exchange POP3 서비스와 Microsoft Exchange POP3 Backend 서비스라는 두 가지 POP3 서비스를 시작해야 합니다. 이러한 프로토콜을 계속 사용하는 IMAP4 클라이언트를 지원하려면 Microsoft Exchange IMAP4 서비스와 Microsoft Exchange IMAP4 Backend 서비스라는 두 가지 IMAP4 서비스를 시작해야 합니다.

POP3 및 IMAP4 서비스를 사용하도록 설정하는 자세한 단계는 [Exchange 2013에서 POP3 사용](enable-pop3-in-exchange-2013-exchange-2013-help.md) 및 [Exchange 2016에서 IMAP4를 사용 하도록 설정](enable-imap4-in-exchange-2013-exchange-2013-help.md)을 참조하십시오.

기본적으로 Exchange 2013이 실행되는 컴퓨터에 사서함이 있는 사용자는 Outlook이나 Outlook Web App, Exchange ActiveSync 또는 Outlook 음성 액세스를 사용하여 사서함에 액세스할 수 있습니다. Outlook, Outlook Web App 및 Outlook 음성 액세스를 사용하여 전자 메일 사용자는 Exchange 2016 서버에 사서함이 있는 사용자가 사용할 수 있는 포괄적인 기능 모음을 사용할 수 있습니다.

**목차**

POP3 및 IMAP4 기능 개요

POP3 및 IMAP4 사이트 간 연결

POP3 및 IMAP4에 비표준 계정 사용

POP3와 IMAP4 차이점 이해

POP3 및 IMAP4 전자 메일 응용 프로그램에 대한 보내기 및 받기 옵션

POP3 및 IMAP4 응용 프로그램

Exchange 2013사서함에 대한 POP3 또는 IMAP4 액세스를 구성하기 위한 사용자 설정

## POP3 및 IMAP4 기능 개요

이 섹션에서는 Exchange 2013의 POP3 및 IMAP4 기능에 대해 설명합니다.

POP3 및 IMAP4 프로토콜은 다음과 같은 이점과 제한 사항이 있습니다.

  - **POP3**   POP3는 오프라인 메일 처리를 지원하도록 설계되어 있습니다. POP3를 사용하면 클라이언트가 메일을 서버에 저장하도록 설정되지 않은 경우 서버에서 전자 메일 메시지가 제거되어 로컬 POP3 클라이언트에 저장됩니다. 이로써 사용자가 데이터 관리 및 보안 책임을 가지게 됩니다. POP3는 일정, 연락처 및 작업 같은 고급 공동 작업 기능을 제공하지 않습니다.

  - **IMAP4**   IMAP4는 오프라인 및 온라인 액세스를 제공하지만 POP3와 마찬가지로 일정, 연락처, 작업 등 고급 공동 작업 기능을 제공하지 않습니다.

POP3 및 IMAP4 전자 메일 응용 프로그램은 전자 메일 서버에 메시지를 보내는 데 POP3 및 IMAP4를 사용하지 않습니다. 이러한 프로그램은 SMTP 프로토콜을 통해 메시지를 보냅니다. POP3 또는 IMAP4를 사용하는 클라이언트 응용 프로그램으로부터 전자 메일 전송을 수신하는 커넥터는 Exchange 설치 시 자동으로 만들어집니다. 커넥터에 대한 자세한 내용은 [수신 커넥터](receive-connectors-exchange-2013-help.md)를 참조하세요.


> [!NOTE]
> 사용자가 POP 또는 IMAP 기반 전자 메일 프로그램을 사용하여 Office 365 전자 메일을 열 때마다 몇 초의 지연이 발생합니다. 이 지연은 인증을 위한 추가 홉을 제공하는 프록시 서버 사용으로 인한 것입니다. 프록시 서버는 먼저 할당된 팟 서버(클라이언트 액세스 서버)를 조회한 다음 해당 서버에 대해 인증을 합니다.



## POP3 및 IMAP4 사이트 간 연결

이전 버전의 Exchange에서는 조직의 다른 사이트에 사서함이 있는 경우 POP3 및 IMAP4 클라이언트가 조직의 한 사이트에서 메일에 연결할 수 있도록 수동 구성 단계를 수행해야 했습니다. 기본적으로 Exchange 2013은 한 사이트의 클라이언트 액세스 서버에서 올바른 서버로 자동으로 프록시 처리됩니다.

## POP3 및 IMAP4에 비표준 계정 사용

POP3 및 IMAP4를 통해 Exchange 2016 사서함에 로그온하는 데 익명 계정이나 Guest 계정을 사용할 수 없습니다. POP3 및 IMAP4를 사용하여 액세스하기 위해 비표준 계정을 사용하는 경우에는 보안 취약점으로 인해 익명 계정이 차단됩니다. 또한 POP3 또는 IMAP4를 통해 관리자 사서함에 연결할 수 없습니다. 이 제한 사항은 관리자 사서함 보안을 향상시키기 위한 Exchange 2013의 의도적인 동작입니다. 관리자 사서함에 액세스하려면 Outlook 또는 Outlook Web App을 사용해야 합니다.

## POP3와 IMAP4 차이점 이해

**POP3** POP3는 흔히 사용되는 전자 메일 인터넷 프로토콜입니다. 기본적으로 POP3 전자 메일 응용 프로그램이 전자 메일 메시지를 클라이언트 컴퓨터에 다운로드하면 다운로드된 메시지는 서버에서 제거됩니다. 사용자의 전자 메일 복사본이 전자 메일 서버에 보관되지 않으면 사용자는 여러 컴퓨터에서 동일한 전자 메일 메시지에 액세스할 수 없습니다. 그러나 일부 POP3 전자 메일 응용 프로그램의 경우 서버에 메시지 복사본을 보관하도록 구성할 수 있기 때문에 다른 컴퓨터에서 동일한 전자 메일 메시지에 액세스할 수 있습니다. POP3 클라이언트 응용 프로그램은 전자 메일 서버에서 클라이언트 컴퓨터의 단일 폴더(일반적으로 받은 편지함)에 메시지를 다운로드하는 경우에만 사용할 수 있습니다. POP3 프로토콜은 전자 메일 서버의 여러 폴더를 클라이언트 컴퓨터의 여러 폴더와 동기화할 수 없습니다.

**IMAP4** IMAP4를 사용하는 전자 메일 클라이언트 응용 프로그램은 POP3를 사용하는 전자 메일 클라이언트 응용 프로그램보다 유연하며 일반적으로 더 많은 기능을 제공합니다. 기본적으로 IMAP4 전자 메일 응용 프로그램이 전자 메일 메시지를 클라이언트 컴퓨터에 다운로드하면 다운로드된 메시지의 복사본이 전자 메일 서버에 남습니다. 사용자의 전자 메일 메시지 복사본이 전자 메일 서버에 보관되기 때문에 사용자는 여러 컴퓨터에서 동일한 전자 메일 메시지에 액세스할 수 있습니다. IMAP4 전자 메일을 사용하는 경우 사용자는 전자 메일 서버에 여러 개의 전자 메일 폴더를 만들고 이러한 폴더에 액세스할 수 있습니다. 그런 다음 여러 위치의 컴퓨터에서 서버의 모든 메시지에 액세스할 수 있습니다. 예를 들어, 대부분의 IMAP4 응용 프로그램은 사용자의 보낸 항목 복사본을 서버에 보관하도록 구성할 수 있기 때문에 사용자는 다른 모든 컴퓨터에서 해당 보낸 항목을 볼 수 있습니다. IMAP4는 대부분의 IMAP4 응용 프로그램에서 지원하는 추가 기능을 지원합니다. 예를 들어, 일부 IMAP4 응용 프로그램에는 사용자가 서버에서 전자 메일 메시지 헤더(메시지를 보낸 사람과 제목)만 확인한 다음 읽고 싶은 메시지만 다운로드할 수 있는 기능이 포함되어 있습니다. 또한 IMAP4는 공용 폴더 액세스를 지원하지 않습니다.


> [!NOTE]
> IMAP4 및 POP3 클라이언트는 Exchange에 대한 일정 정보에 제한적으로 액세스할 수 있습니다. 자세한 내용은 <A href="configure-calendar-options-for-pop3-exchange-2013-help.md">P o p 3에 대 한 일정 옵션 구성</A> 및 <A href="configure-calendar-options-for-imap4-exchange-2013-help.md">IMAP4에 대 한 일정 옵션 구성</A>을 참조하십시오.



## POP3 및 IMAP4 전자 메일 응용 프로그램에 대한 보내기 및 받기 옵션

POP3 및 IMAP4 전자 메일 응용 프로그램을 사용하면 사용자가 서버에 연결하여 전자 메일을 보내고 받을 시점을 선택할 수 있습니다. 이 섹션에서는 가장 일반적인 연결 옵션 중 몇 가지를 검토하고, 사용자가 POP3 및 IMAP4 전자 메일 응용 프로그램에서 사용할 수 있는 연결 옵션을 선택할 때 고려해야 할 몇 가지 요소에 대해서도 설명합니다.

## 일반 구성 설정

POP3 또는 IMAP4 클라이언트 응용 프로그램에 설정할 수 있는 가장 일반적인 연결 설정은 다음과 같이 세 가지가 있습니다.

  - 전자 메일 응용 프로그램이 시작될 때마다 메시지 주고받기. 이 옵션을 사용하면 전자 메일 응용 프로그램을 시작할 때만 메일을 보내고 받습니다.

  - 수동으로 메시지 주고받기. 이 옵션을 사용하면 사용자가 클라이언트 사용자 인터페이스에서 "보내기 및 받기" 옵션을 클릭하는 경우에만 메시지를 보내고 받습니다.

  - 설정된 시간(분)마다 메시지 주고받기. 이 옵션을 사용하면 클라이언트 응용 프로그램이 설정된 시간(분)마다 서버에 연결하여 메시지를 보내고 새로운 모든 메시지를 다운로드합니다.

사용하는 전자 메일 응용 프로그램에 대해 이러한 설정을 구성하는 방법에 대한 자세한 내용은 각 전자 메일 응용 프로그램에서 제공하는 도움말 설명서를 참조하십시오.

## 보내기/받기 옵션을 선택할 때 고려할 사항

POP3 또는 IMAP4 전자 메일 응용 프로그램을 실행 중인 장치나 컴퓨터가 항상 인터넷에 연결되어 있으면 사용자는 설정된 시간(분)마다 메시지를 보내고 받도록 전자 메일 응용 프로그램을 구성할 수 있습니다. 서버에 자주 연결하면 사용자는 서버의 최신 정보를 사용하여 전자 메일 응용 프로그램을 최신 상태로 유지할 수 있습니다. 그러나 POP3 또는 IMAP4 전자 메일 응용 프로그램을 실행 중인 장치나 컴퓨터가 항상 인터넷에 연결되어 있지 않으면 사용자는 수동으로 메시지를 보내고 받도록 전자 메일 응용 프로그램을 구성할 수 있습니다.


> [!NOTE]
> 사용자가 IMAP4 IDLE 명령이 지원되는 IMAP4 호환 전자 메일 응용 프로그램을 사용하는 경우 거의 실시간으로 Exchange 사서함으로 전자 메일을 보내고 이 사서함에서 전자 메일을 받을 수 있습니다. 전자 메일 서버 응용 프로그램과 클라이언트 응용 프로그램이 모두 IMAP4 IDLE 명령을 지원해야만 이 연결 방법이 제대로 작동합니다. 대부분의 경우 이 연결 방법을 사용하기 위해 사용자가 IMAP4 응용 프로그램에서 어떤 설정을 구성할 필요는 없습니다.



## POP3 및 IMAP4 응용 프로그램

Exchange 2013은 POP3 및 IMAP4를 지원하기 때문에 사용자는 POP3 및 IMAP4 클라이언트 응용 프로그램을 지원하는 모든 응용 프로그램을 사용하여 Exchange 2013에 연결할 수 있습니다. 이러한 응용 프로그램에는 Outlook, Windows Live 메일, Outlook Web App Outlook Express, Entourage 및 여러 타사 응용 프로그램(예: Gmail, Mozilla Thunderbird 및 Eudora 등)이 있습니다. 각 전자 메일 클라이언트 응용 프로그램에서 지원하는 기능은 다양합니다. 특정 POP3 및 IMAP4 클라이언트 응용 프로그램에서 제공하는 특정 기능에 대한 자세한 내용은 각 응용 프로그램에 포함되어 있는 설명서를 참조하세요.

## Exchange 2013사서함에 대한 POP3 또는 IMAP4 액세스를 구성하기 위한 사용자 설정

POP3 및 IMAP4 클라이언트 액세스를 사용하도록 설정할 경우 전자 메일 프로그램을 해당 Exchange 2016 사서함에 연결하는 데 필요한 정보를 사용자에게 제공해야 합니다.

회사 네트워크 내부에서 연결하려면 사용자에게 다음 정보가 있어야 합니다.

  - 내부 POP3 또는 IMAP4 서버 이름

  - 내부 POP3 또는 IMAP4 포트 번호

  - 내부 POP3 또는 IMAP4 암호화 방법

  - 내부 SMTP(보내는 서버) 이름

  - 내부 SMTP(보내는 서버) 포트 번호

  - 내부 SMTP(보내는 서버) 암호화 방법

인터넷에서 연결하려면 사용자에게 다음 정보가 있어야 합니다.

  - 외부 POP3 또는 IMAP4 서버 이름

  - 외부 POP3 또는 IMAP4 포트 번호

  - 외부 POP3 또는 IMAP4 암호화 방법

  - 외부 SMTP(보내는 서버) 이름

  - 외부 SMTP(보내는 서버) 포트 번호

  - 외부 SMTP(보내는 서버) 암호화 방법

전자 메일이나 다른 수동 통신 방법으로 사용자에게 이러한 설정을 제공할 수 있습니다. 사용자가 Outlook Web App를 사용하여 고유한 설정을 조회할 수 있도록 Exchange를 구성할 수도 있습니다.

**사용자가 POP3, IMAP4 및 SMTP 서버 설정을 조회할 수 있도록 Exchange 구성**

기본적으로 사용자는 Outlook Web App통해 POP3, IMAP4 및 SMTP 서버 설정을 조회할 수 없습니다. 이를 허용하려면 **Set-PopSettings** 및 **Set-ImapSettings** cmdlet을 사용해야 합니다. 사용자가 SMTP(보내는) 서버 설정을 조회할 수 있도록 하려면 **Set-ReceiveConnector** cmdlet을 사용해야 합니다.

사용자가 자신의 POP3, IMAP4 및 SMTP 설정을 조회할 수 있게 하려면 다음을 수행합니다.

  - **POP3 설정** *ExternalConnectionSettings* 매개 변수를 사용하여 **Set-POPSettings** cmdlet을 실행합니다. `Set-POPSettings -ExternalConnectionSetting {<FQDN>:995:SSL}` 형식을 사용합니다. 예를 들어, FQDN이 Dublin01.Contoso.com인 서버를 통해 연결하는 클라이언트가 자신의 POP 설정을 조회할 수 있게 하려면 `Set-PopSettings -ExternalConnectionSetting {Dublin01.Contoso.com:995:SSL}`을 실행합니다.
    
    이 설정을 적용한 후 IIS를 다시 시작해야 합니다.

  - **IMAP4 설정** *ExternalConnectionSettings* 매개 변수를 사용하여 **Set-IMAPSettings** cmdlet을 실행합니다. `Set-ImapSettings -ExternalConnectionSetting {<FQDN>:993:SSL}` 형식을 사용합니다. 예를 들어, FQDN이 Dublin01.Contoso.com인 서버를 통해 연결하는 클라이언트가 자신의 IMAP 설정을 조회할 수 있게 하려면 `Set-IMAPSettings -ExternalConnectionSetting {Dublin01.Contoso.com:993:SSL}`을 실행합니다.
    
    이 설정을 적용한 후 IIS를 다시 시작해야 합니다.

  - **SMTP 설정** *AdvertiseClientSettings* 매개 변수를 사용하여 **Set-ReceiveConnector** cmdlet을 실행합니다. `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN <FQDN>` 형식을 사용합니다. 예를 들어, FQDN이 Dublin01.Contoso.com인 서버를 통해 연결하는 클라이언트가 자신의 SMTP 설정을 조회할 수 있게 하려면 `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN Dublin01.Contoso.com`을 실행합니다.
    
    이 설정을 적용한 후 IIS를 다시 시작해야 합니다.

**Set-POPSettings**, **Set-IMAPSettings**, 및 **Set-ReceiveConnector** cmdlet을 실행하여 기본 설정을 변경하고 나면 사용자는 **설정** \> **옵션** \> **계정** \> **내 계정** \> **POP 또는 IMAP 액세스 설정**을 클릭하여 Outlook Web App의 외부 POP, IMAP, SMTP 서버 설정을 조회할 수 있습니다.

**메시지 복사본을 서버에 유지**

일부 전자 메일 프로그램의 기본 설정에서는 메시지가 검색된 후 서버에서 메시지를 제거하는 것입니다. 사용자가 클라이언트에서 검색하는 모든 메시지의 복사본을 서버에 유지하도록 전자 메일 프로그램을 설정하게 하는 것이 좋습니다. 메시지 복사본을 서버에 유지하면 사용자는 다른 전자 메일 프로그램에서 메시지에 액세스할 수 있습니다.

