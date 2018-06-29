---
title: 'Outlook Web App: Exchange 2013 Help'
TOCTitle: Outlook Web App
ms:assetid: 3814b665-01e8-4881-9a44-163f14789ee4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657718(v=EXCHG.150)
ms:contentKeyID: 50482868
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Outlook Web Access 2010 보다 이전 버전의 Microsoft Exchange에서 걸려온는 Outlook Web App에 대해 설명 합니다. 이 문서에 도움이 되는 정보에 아웃 링크와 함께 간략 한 개요를 제공합니다.

기본적으로 MicrosoftExchange 2013을 설치할 때 Outlook Web App를 사용하도록 설정하며 MicrosoftOutlook Web App는 사용자가 거의 모든 웹 브라우저에서 자신의 Exchange 사서함에 액세스할 수 있도록 합니다.

클라이언트 액세스 서버 역할은 Outlook Web App에 대한 프록시 및 리디렉션 서비스를 제공합니다.


> [!NOTE]
> Outlook Web App는 Exchange 2010 이전의 Microsoft Exchange 버전에서 Outlook Web Access라고 불렸습니다.



새로운 기능에 대한 자세한 내용은 [Exchange 2013의 새로운 기능](what-s-new-in-exchange-2013-exchange-2013-help.md) 항목을 참조하십시오. Exchange 2013의 클라이언트 액세스 서버 역할에 대한 자세한 내용은 [클라이언트 액세스 서버](client-access-server-exchange-2013-help.md) 항목을 참조하십시오.

## Outlook Web App 개요

완전히 지원되는 웹 브라우저에서 사용자는 대화 뷰, 받은 편지함 규칙, 읽기 창 및 일정 도우미와 같은 기능에 액세스할 수 있습니다. 완전히 지원되지 않는 브라우저도 사용할 수 있지만 사용자는 기능이 더 적은 Outlook Web App의 라이트 버전을 보게 됩니다. Outlook Web App의 새로운 기능에 대한 자세한 내용은 [Exchange 2013에서 Outlook Web App의 새 기능](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md) 항목을 참조하십시오.

## Outlook Web App 관리

Exchange 2013에서 가장 일반적인 Outlook Web App 관리 작업은 EAC(Exchange 관리 센터)에서 수행할 수 있습니다. 이러한 모든 작업 및 대부분의 기타 작업은 Exchange 관리 셸을 사용하여 수행할 수 있습니다. 하지만 SSL(Secure Sockets Layer) 구성 또는 사용자를 위한 단순 URL 설정과 같은 일부 작업에서 아직도 IIS(인터넷 정보 서비스) 관리자와 같은 도구를 사용합니다.

## Outlook Web App 액세스 (영문)

사용자와 함께에 로그인 할 수 Outlook Web App이 같은 URL을 사용 하 여: **https://\<domain 이름 \> / OWA** 또는 **https://mail.\<domain 이름 \> / OWA**

예, 조직의 도메인 contoso.com 인 경우에 https://contoso.com/OWA 또는 https://mail.contoso.com/OWA 사용 합니다. Outlook Web App [여기](https://support.microsoft.com/en-us/kb/2897680)에 액세스 하는 방법에 대 한 자세한 내용은. 다른 것에 로그인 URL을 변경 하려면 또는 SSL에 대 한 리디렉션을 강제 실행 하려면 [Outlook Web App URL 단순화](simplify-the-outlook-web-app-url-exchange-2013-help.md)를 참조 하십시오.

전자 메일에 대 한 Exchange Online 또는 Office 365를 사용 중인를 경우 사용자와 함께 **outlook.office365.com/owa** 또는 [여기를 클릭](http://go.microsoft.com/fwlink/p/?linkid=402333)에서 Outlook Web App 액세스 합니다. 자세한 내용은 [Outlook Web app 로그인](http://go.microsoft.com/fwlink/p/?linkid=511341) 하 고 [Office 365로 로그인 할 위치](http://go.microsoft.com/fwlink/p/?linkid=522691).

