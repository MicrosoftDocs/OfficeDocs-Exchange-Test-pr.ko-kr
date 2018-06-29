---
title: '모바일 장치: Exchange 2013 Help'
TOCTitle: 모바일 장치
ms:assetid: 93a949e7-b3ef-43ea-ae0c-6698826fc8d2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232129(v=EXCHG.150)
ms:contentKeyID: 50483705
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 모바일 장치

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-09-24_

Microsoft Exchange ActiveSync와 호환되는 모바일 장치를 사용하는 사용자는 언제 어디서나 대부분의 Microsoft Exchange 사서함 데이터에 액세스할 수 있습니다. Exchange ActiveSync에서 사용할 수 있는 휴대폰 및 장치에는 여러 가지가 있습니다. 예를 들면 Windows Phone, Nokia 휴대폰, Android 휴대폰 및 태블릿, Apple iPhone, iPod 및 iPad 등이 있습니다.

휴대폰 및 휴대폰 외의 모바일 장치가 모두 Exchange ActiveSync를 지원하지만 대부분의 Exchange ActiveSync 설명서에서는 *모바일 장치*라는 용어를 사용합니다. 설명하고 있는 기능이 SMS 메시지 알림 같은 휴대폰 신호를 필요로 하는 경우를 제외하고 모바일 장치라는 용어는 휴대폰뿐 아니라 태블릿 같은 다른 모바일 장치에도 적용됩니다.

## Exchange ActiveSync

Exchange ActiveSync는 무선으로 전자 메일 메시지, 일정 데이터, 연락처 및 작업에 대한 모바일 액세스를 지원하는 통신 프로토콜입니다. Exchange ActiveSync는 Windows Phone 및 Exchange ActiveSync와 호환되는 타사 휴대폰에서 사용할 수 있습니다.

Exchange ActiveSync는 직접 올리기 기술을 제공합니다. 직접 올리기는 새 전자 메일 메시지와 기타 Exchange 데이터를 휴대폰에 올리기 위해 모바일 장치와 서버 간에 구성되어 유지 관리되는 암호화된 HTTPS 연결을 사용합니다.

Microsoft Exchange Server 2013에서 직접 올리기를 사용하려면 사용자에게 직접 올리기를 지원하도록 설계된 모바일 장치가 있어야 합니다.

## Exchange ActiveSync 기능

Exchange ActiveSync에서는 모바일 장치에 보안 정책을 적용할 수 있는 여러 기능에 액세스할 수 있습니다. Exchange 2013을 사용하면 여러 모바일 장치 사서함 정책을 구성하고 Exchange 서버와 동기화할 모바일 장치를 제어할 수 있습니다. 모바일 장치를 분실하거나 도난 당했을 경우 Exchange ActiveSync를 통해 모바일 장치에서 모든 데이터를 지우는 원격 장치 데이터 지움 명령을 보낼 수 있습니다. Outlook Web App에서도 원격 장치 데이터 지움을 시작할 수 있습니다.

Exchange ActiveSync에서는 사용자가 복구 암호를 생성할 수 있습니다. 이 복구 암호는 모바일 장치에 저장되며 사용자가 암호를 잊었을 경우 사용됩니다. 사용자는 장치 암호 또는 PIN을 생성하면서 동시에 복구 암호를 생성합니다. 이 복구 암호는 모바일 장치의 잠금을 해제하는 데 사용할 수 있습니다. 복구 암호가 사용되면 그 즉시 사용자는 새로운 PIN을 만들어야 합니다.

## POP3 및 IMAP4

모바일 장치에서 Exchange ActiveSync를 지원하지 않거나 Exchange ActiveSync에서 제공하는 다양한 기능 집합이 필요하지 않은 경우에는 모바일 장치에서 POP3 또는 IMAP4를 사용하여 전자 메일에 액세스할 수 있습니다. 사서함에 대한 POP3 및 IMAP4 액세스에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md) 항목을 참조하십시오.

