---
title: '허용 하거나 금지 하는 클라이언트 액세스 서버에서 전화 응답: Exchange 2013 Help'
TOCTitle: 허용 하거나 금지 하는 클라이언트 액세스 서버에서 전화 응답
ms:assetid: 8287bb78-2621-4b80-a128-8f2ccd67923a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123529(v=EXCHG.150)
ms:contentKeyID: 50556023
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 허용 하거나 금지 하는 클라이언트 액세스 서버에서 전화 응답

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-11-18_

클라이언트 액세스 서버의 Microsoft Exchange 통합 메시징 통화 라우터 서비스가 새로 걸려온 전화에 응답하는 것을 허용하거나 금지할 수 있습니다. 기본적으로 클라이언트 액세스 서버는 설치 후 사용 가능한 상태로 있습니다. 클라이언트 액세스 서버가 들어오는 음성, 팩스, 자동 전화 교환 및 Outlook Voice Access 통화를 수락하도록 설정하려면 **Set-ServerComponentState** cmdlet을 사용합니다.

클라이언트 액세스 서버에 대해 유지 관리 모드를 구성하면 서버의 서비스를 중단시킬 수 있습니다. 클라이언트 액세스 서버의 경우 서비스 중단은 더 이상 서버가 VoIP 게이트웨이, IP PBX, SIP 사용 가능 PBX 또는 SBC(Session Border Controller)의 수신 전화를 수락하지 않음을 의미합니다.

Exchange 2007 및 Exchange 2010에는 통합 메시징 서버의 작동 상태를 제어하는 데 사용할 수 있는 상태 매개 변수가 있었습니다. Exchange 2013의 경우 클라이언트 액세스 서버의 **Set-UMCallRouterSettings** cmdlet에서 같은 목적으로 사용할 수 있는 상태 매개 변수가 없습니다.


> [!IMPORTANT]
> UM과 Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server를 통합할 경우를 제외하고는 통합 메시징에 대한 통화를 처리하기 위해 클라이언트 액세스 및 사서함 서버를 UM 다이얼 플랜에 추가할 필요가 없습니다. 기본적으로 조직의 모든 클라이언트 액세스 및 사서함 서버에서 들어오는 수신 전화에 응답할 수 있습니다.



클라이언트 액세스 서버와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "Exchange Server 구성 설정" 항목

  - 사서함 서버와 동일한 컴퓨터나 별도의 컴퓨터에 클라이언트 액세스 서버가 설치되어 있는지 확인합니다.

  - 클라이언트 액세스 서버를 유지 관리 모드로 전환하려면 클라이언트 액세스 배열에 서버의 서비스를 중단시킬 수 있을 만큼 충분한 정상 용량이 있는지 확인합니다.

  - 서버를 유지 관리 모드에서 해제하려면 먼저 서버의 상태를 확인하고 서버가 서비스를 다시 시작할 준비가 되었는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 클라이언트 액세스 서버에서의 전화 응답 허용 또는 금지

이 예에서는 클라이언트 액세스 서버 `UMCallRouter-05x.contoso.com`이 VoIP 게이트웨이, IP PBX, SIP 사용 가능 PBX 및 SBC에서 들어오는 음성, 팩스, 자동 전화 교환 및 Outlook Voice Access 통화에 응답할 수 있도록 설정하고 변경 내용을 UMCallRouter-05x 서버의 레지스트리에 씁니다.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

이 예에서는 클라이언트 액세스 서버 `UMCallRouter-05x.contoso.com`이 VoIP 게이트웨이, IP PBX, SIP 사용 가능 PBX 및 SBC에서 들어오는 음성, 팩스, 자동 전화 교환 및 Outlook Voice Access 통화에 응답하지 못하도록 설정하고 변경 내용을 Active Directory에만 씁니다.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

