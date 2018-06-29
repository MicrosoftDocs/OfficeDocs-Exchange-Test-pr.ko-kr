---
title: '클라이언트 액세스 서버에서 TCP 수신 대기 포트를 설정 합니다.: Exchange 2013 Help'
TOCTitle: 클라이언트 액세스 서버에서 TCP 수신 대기 포트를 설정 합니다.
ms:assetid: 5f48f21a-d8d4-48b2-868f-9a3647693841
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673530(v=EXCHG.150)
ms:contentKeyID: 50556005
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 클라이언트 액세스 서버에서 TCP 수신 대기 포트를 설정 합니다.

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-04-09_

Microsoft Exchange 통합 메시징 통화 라우터 서비스를 실행 중인 클라이언트 액세스 서버에서 SIP 요청을 수신 대기하는 데 사용되는 TCP 포트를 구성할 수 있습니다. 기본적으로 클라이언트 액세스 서버를 설치할 때 SIP TCP 수신 대기 포트 번호는 5060으로 설정되고 클라이언트 액세스 서버는 TCP 모드로 시작합니다. SIP TCP 포트는 EAC를 사용하여 구성할 수 없습니다. SIP TCP 수신 대기 포트 번호는 **Set-UMCallRouterSettings** cmdlet을 사용하여 구성해야 합니다.

VoIP 게이트웨이, IP PBX 또는 SBC(Session Borders Controller)가 SIP 표준 5060이 아닌 TCP 포트를 사용하도록 구성되어 있으면 TCP 수신 대기 포트를 5061로 구성해야 합니다.

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

## EAC를 사용하여 클라이언트 액세스 서버에 대해 TCP 수신 대기 포트 구성

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  목록 보기에서 수정하려는 Exchange 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **Exchange Server** 페이지에서 **통합 메시징**을 클릭합니다.

4.  **UM 통화 라우터 설정**의 **TCP 수신 대기 포트**에 TCP 포트의 번호를 입력한 후 **저장**을 클릭합니다.

## 셸을 사용하여 클라이언트 액세스 서버에 대해 TCP 수신 대기 포트 구성

이 예에서는 `MyClientAccessServer`라는 클라이언트 액세스 서버에 대해 TCP 수신 대기 포트를 5566으로 설정합니다.

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTCPListeningPort 5566

