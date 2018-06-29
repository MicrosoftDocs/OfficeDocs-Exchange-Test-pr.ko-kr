---
title: '클라이언트 액세스 역할 로컬 site_ClientAccessRoleNotPresentInSite에서 검색 되지 않음: Exchange 2013 Help'
TOCTitle: 클라이언트 액세스 역할 로컬 site_ClientAccessRoleNotPresentInSite에서 검색 되지 않음
ms:assetid: b5bfc6af-9c55-46c0-a293-6078b64e87dd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.clientaccessrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 50483952
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 클라이언트 액세스 역할 로컬 site\_ClientAccessRoleNotPresentInSite에서 검색 되지 않음

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

기존 클라이언트 액세스 역할 로컬 Active Directory® 디렉터리 서비스 사이트에서 검색 하지 않아서이 경고를 표시 하는 Microsoft® Exchange Server 2007 설치 합니다.

클라이언트 액세스 역할의 인스턴스로 하기 전에 역할은 Active Directory 사이트에 설치 된 사서함 서버를 설치 하기로 선택 했습니다.

클라이언트 액세스 서버 역할은 다양 한 다양 한 클라이언트에서에서 하 여 Exchange 2007 서버에 연결을 허용 합니다. 예: Microsoft Outlook Express 및 Eudora 소프트웨어 클라이언트는 Exchange 서버와 통신 하도록 POP3 또는 IMAP4 연결을 사용 합니다. 모바일 장치 등의 하드웨어 클라이언트 ActiveSync, POP3 또는 IMAP4를 사용 하 여 Exchange 서버와 통신할 수 있습니다.

사용자가 자신의 받은 편지함 Microsoft Office Outlook® 이외의 모든 클라이언트를 사용 하 여에 액세스 하는 경우에 Exchange 조직에서 클라이언트 액세스 서버 역할을 설치 해야 합니다.

사용자는 Outlook과 함께 자신의 사서함에 로그온 할 수 있지만 로컬 Active Directory 사이트에 대 한 클라이언트 액세스 역할은 전에 동일한 사서함에 대해 Outlook Web Access 또는 모바일 장치를 사용할 수 없습니다.

