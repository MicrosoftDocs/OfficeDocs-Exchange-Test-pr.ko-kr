---
title: '허용 또는 사서함 서버에서 전화 응답을 금지.: Exchange 2013 Help'
TOCTitle: 허용 또는 사서함 서버에서 전화 응답을 금지.
ms:assetid: 4b860c09-6669-4e3d-b3dc-17b8018b3860
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997908(v=EXCHG.150)
ms:contentKeyID: 50555987
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 허용 또는 사서함 서버에서 전화 응답을 금지.

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-11-18_

새 호출에 응답 하거나 그 이렇게 하지 못하도록 하려면 사서함 서버에서 Microsoft Exchange 통합 메시징 서비스를 허용할 수 있습니다. 기본적으로 사서함 서버가 설치 된 후 활성된 상태로 설정입니다. 들어오는 음성, 팩스, 자동 전화 교환 및 Outlook Voice Access 호출을 수락 하도록 사서함 서버를 설정 하는 경우 **Set-ServerComponentState** cmdlet을 사용 합니다.

사서함 서버에 대 한 유지 관리 모드를 구성 서비스가 중단 서버 걸릴 수 있습니다. 사서함 서버에 대 한 서비스의 아웃 바운드 있음을 나타내고 모든 활성 데이터베이스를 호스트할 되지 않음, 모든 전송 큐는 비어 서버 클라이언트 액세스 서버, VoIP 게이트웨이, IP Pbx, SIP 사용 가능 Pbx 또는 세션 테두리 컨트롤러 (Sbc)에서 들어오는 호출을 수락 하지 않습니다.

Exchange 2007 및 Exchange 2010 에서 통합 메시징 서버의 작동 상태를 제어 하는데 사용할 수 있는 상태 매개 변수를 사용 했습니다. Exchange 2013 사서함 서버에 대 한 **Set-UMService** cmdlet에서 해당 목적을 위해 없음 status 매개 변수를 사용 하 여 제공 됩니다.


> [!IMPORTANT]
> UM과 Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server를 통합할 경우를 제외하고는 통합 메시징에 대한 통화를 처리하기 위해 클라이언트 액세스 및 사서함 서버를 UM 다이얼 플랜에 추가할 필요가 없습니다. 기본적으로 조직의 모든 클라이언트 액세스 및 사서함 서버에서 들어오는 수신 전화에 응답할 수 있습니다.



사서함 서버와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "Exchange Server 구성 설정" 항목

  - 클라이언트 액세스 서버와 동일한 컴퓨터나 별도의 컴퓨터에 사서함 서버가 설치되어 있는지 확인합니다.

  - 사서함 서버를 유지 관리 모드로 올리는 경우 서버에서 서비스 벗어나 사용할 수 있도록 하려면 모든 데이터베이스 복사본의 충분 한 중복 인지 확인 합니다.

  - 서버를 유지 관리 모드에서 해제하려면 먼저 서버의 상태를 확인하고 서버가 서비스를 다시 시작할 준비가 되었는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용 하 여 허용 하거나 금지 사서함 서버에서 전화 응답

들어오는 음성, 팩스, 자동 전화 교환에 응답 하는 사서함 서버 `UMMBXr-05x.contoso.com` 를 사용 하는이 예제 및 Outlook Voice Access에서 VoIP 게이트웨이, IP Pbx, SIP 사용 가능 Pbx 및 Sbc를 호출 하 고 UMMBX 05 레지스트리 하 여 변경 내용을 기록 x 서버입니다.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

이 예제에서는 응답 들어오는 음성, 팩스, 자동 전화 교환 및 Outlook Voice Access 통화에서 VoIP 게이트웨이, IP Pbx, SIP 사용 가능 Pbx 및 Sbc에서 사서함 서버 `UMMBX-05x.contoso.com` 수 없도록 하 고 Active Directory에만 변경 합니다.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

