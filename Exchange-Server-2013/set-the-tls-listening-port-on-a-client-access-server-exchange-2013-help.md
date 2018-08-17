---
title: '클라이언트 액세스 서버에서 TLS 수신 대기 포트를 설정 합니다.: Exchange 2013 Help'
TOCTitle: 클라이언트 액세스 서버에서 TLS 수신 대기 포트를 설정 합니다.
ms:assetid: f4401923-61fa-4dc5-95f8-c0d2f515b2ea
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673576(v=EXCHG.150)
ms:contentKeyID: 50556113
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 클라이언트 액세스 서버에서 TLS 수신 대기 포트를 설정 합니다.

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-17_

Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행 하는 클라이언트 액세스 서버에 대 한 SIP 요청에 대 한 수신 대기 하는데 사용 되는 전송 계층 보안 (TLS) 포트를 구성할 수 있습니다. 기본적으로 클라이언트 액세스 서버를 설치할 때 TLS SIP 수신 대기 포트 번호는 5061로 설정 합니다.

하려는 경우에 TLS 수신 대기 포트 5061 구성 해야할 수 있습니다.

  - UM 다이얼 플랜에서 VoIP를 SIP 보안으로 설정

  - UM 다이얼 플랜에서 VoIP를 보안으로 설정

  - Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server와 통합

  - 상호 전송 계층 보안을 사용 하 여 (mutual TLS) 클라이언트 액세스 서버, Microsoft Exchange 통합 메시징 서비스를 실행 하는 사서함 서버와 VoIP 게이트웨이, SIP Session Initiation Protocol (), IP Pbx 또는 세션 테두리 컨트롤러 (반자)를 사용 하도록 설정 (Pbx) Private Branch Exchange 간에 네트워크 데이터를 암호화 합니다.

UM IP 게이트웨이 및 UM IP 게이트웨이 만들 때 SIP 보안 또는 보안 모드에서 작동 하는 다이얼 플랜 간의 mutual TLS를 사용 하려는 경우에 정규화 된 도메인 이름 (FQDN)으로 구성 하 고 TLS 포트 5061에서 수신 대기 하도록 UM IP 게이트웨이 구성 해야 합니다. 또한 모든 VoIP 게이트웨이, Pbx SIP, IP Pbx를 사용 하도록 설정 또는 Sbc 포트 5061에서 mutual TLS 요청을 수신 대기 하도록 구성 된도 확인 해야 합니다.

클라이언트 액세스 서버 TCP 및 TLS 포트만 구성할 수 있고, Exchange 2013 사서함 서버에 대한 포트는 구성할 수 없습니다. 그러나, **Set-UMService** cmdlet을 사용하여 2010 UM 서버에 대한 TCP 및 TLS 수신 대기 포트를 구성할 수는 있습니다.

통합 메시징 및 클라이언트 액세스 서버와 관련된 추가 작업에 대한 자세한 내용은 [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "클라이언트 액세스 서버(UM 통화 라우터 서비스)" 항목

  - 클라이언트 액세스 서버 및 사서함 서버가 올바르게 설치되었는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 클라이언트 액세스 서버에서 TLS 수신 대기 포트를 구성 하려면

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  목록 보기에서 수정하려는 Exchange 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **Exchange Server** 페이지에서 **통합 메시징**을 클릭합니다.

4.  **UM 서비스 설정** 아래에서 **TLS 수신 대기 포트** 를 TLS 포트 번호를 입력 한 다음 **저장** 을 클릭 합니다.

## 셸을 사용 하 여 클라이언트 액세스 서버에서 TLS 수신 대기 포트를 구성 하려면

5561를 `MyClientAccessServer` 이라는 클라이언트 액세스 서버에서 TLS 수신 대기 포트를 설정 하는이 예제입니다.

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTlsListeningPort 5561

