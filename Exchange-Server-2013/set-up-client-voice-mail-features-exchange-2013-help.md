---
title: '클라이언트 음성 메일 기능 설정: Exchange 2013 Help'
TOCTitle: 클라이언트 음성 메일 기능 설정
ms:assetid: 5e661cfd-d34e-4caa-91a5-967bbecb75eb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673529(v=EXCHG.150)
ms:contentKeyID: 50556004
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 클라이언트 음성 메일 기능 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-20_

이 항목에서는 Exchange UM(통합 메시징) 사용 가능 사용자가 자신의 사서함에 있는 전자 메일과 음성 메일 메시지에 액세스할 수 있도록 하는 클라이언트 기능을 설명합니다. 이러한 기능을 사용하면 사용자가 간편하게 음성 메일에 액세스할 수 있고 전반적인 사용자 환경이 향상됩니다.

**목차**

Voice mail client support

Outlook Voice Access

Forwarding calls

Voice Mail Preview

Receiving faxes

## 음성 메일 클라이언트 지원

**Exchange ActiveSync 클라이언트**   Microsoft Exchange ActiveSync 프로토콜은 인터넷 사용이 가능한 모바일 장치에 있는 클라이언트 등 모바일 클라이언트를 Exchange 사서함에 연결하는 데 사용됩니다. 사용자는 모바일 장치로 사서함에 액세스하여 전자 메일 메시지를 보고, 일정 및 연락처 정보를 보거나 변경하며, 음성 메일 메시지를 청취할 수 있습니다. 또한 전자 메일, 음성 메일, 일정 항목 및 연락처 정보를 다른 장치와 동기화할 수도 있습니다.

**Outlook과 통합**   Microsoft Outlook에서는 사용자가 Exchange 사서함에 액세스한 다음 사서함의 전자 메일 메시지를 보고, 일정 정보를 보거나 변경하며, 전자 메일 메시지 내부에 포함된 Microsoft Windows Media Player를 사용하여 음성 메시지를 청취할 수 있습니다. 지원되는 전자 메일 클라이언트를 통해 사용자는 전화에서 재생 기능과 같은 추가 기능을 사용할 수 있습니다.

**Outlook Web App과 통합**   Microsoft Outlook Web App은 사용자에게 Outlook처럼 완전한 기능을 갖춘 전자 메일 클라이언트와 유사한 UM 인터페이스 및 도구를 제공합니다. 사용자는 Outlook Web App을 통해 호환되는 웹 브라우저를 사용하여 자신의 Exchange 사서함에 액세스할 수 있습니다. Outlook Web App은 Outlook처럼 사용자가 음성 메시지를 청취하고 전화에서 재생 같은 다른 기능에 액세스할 수 있도록 전자 메일에 Windows Media Player를 포함하여 제공합니다.

## Outlook Voice Access

Exchange UM에서 UM 사용 가능 사용자는 UM 다이얼 플랜에 구성된 내부 또는 외부 전화 번호로 전화를 걸어 사서함에 액세스하고 Outlook Voice Access 메뉴 시스템을 사용할 수 있습니다. UM 사용 가능 사용자는 이 메뉴를 사용하여 전자 메일 읽기, 음성 메시지 듣기, Outlook 일정 조작, 개인 연락처에 대한 액세스뿐 아니라 Outlook Voice Access PIN 구성 또는 음성 메일 인사말 녹음 등의 작업을 수행할 수 있습니다. 자세한 내용은 [Outlook Voice Access 설정](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/set-up-outlook-voice-access)을 참조하십시오.

## 착신 전환

UM 사용 가능 사용자는 Outlook 또는 Outlook Web App를 사용하여 전화 응답 규칙을 만들고 구성할 수 있습니다. 전화 응답 규칙을 사용하면 사용자가 수신 전화 처리 방법을 제어할 수 있습니다. 규칙은 받은 편지함 규칙이 받는 전자 메일 메시지에 적용되는 것과 유사하게 수신 전화에 적용되며, 다른 음성 설정과 함께 사용자의 사서함에 저장됩니다. UM 사용 가능한 각각의 사서함에 최대 9개의 전화 응답 규칙을 설정할 수 있습니다. 이러한 규칙은 사서함 규칙과는 별개이며 사용자의 받은 편지함 규칙 저장소 할당량 일부를 차지하지 않습니다. 자세한 내용은 [음성 통화를 착신 전환 하려면 메일 사용자를 허용](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-voice-mail-users-to-forward-calls)을 참조하십시오.

## 음성 사서함 미리 보기

음성 메일 미리 보기는 UM 음성 메일 시스템에서 음성 메일 메시지를 받는 사용자가 사용할 수 있는 기능입니다. 음성 메일 미리 보기는 오디오 녹음을 텍스트 버전으로 제공하여 음성 메일 환경을 향상합니다. 자세한 내용은 [사용자가 음성 메일 대화 내용이 표시 될 수 있도록 허용](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md)을 참조하십시오.

## 팩스 수신

UM에서 UM 사용 가능 사용자에 대한 수신 팩스 호출을 전용 팩스 파트너 솔루션으로 전달하면 팩스 호출과 팩스를 보낸 사람이 연결되고 사용자를 대신하여 팩스를 수신합니다. UM 사용 가능 사용자가 사서함에 팩스 메시지를 수신할 수 있으려면 다음을 수행해야 합니다.

  - *FaxEnabled* 매개 변수를 `$true`로 설정하여 사용자에게 연결된 UM 다이얼 플랜에서 수신 팩스를 허용하도록 설정합니다.

  - *Allowfax* 매개 변수를 `$true`로 설정하여 사용자에게 연결된 UM 다이얼 플랜에서 수신 팩스를 허용하도록 설정합니다.

  - *FaxEnabled* 매개 변수를 `$true`로 설정하여 사용자에 대한 수신 팩스를 허용하도록 설정합니다.

  - 파트너 팩스 서버 URI가 수신 팩스를 허용하도록 설정합니다.

  - 사서함 서버와 팩스 파트너 서버 간에 인증을 구성합니다.

