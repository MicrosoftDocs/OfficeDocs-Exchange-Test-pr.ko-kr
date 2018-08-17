---
title: 'SIP URI 다이얼 플랜에 사서함 및 클라이언트 액세스 서버를 추가 합니다.: Exchange 2013 Help'
TOCTitle: SIP URI 다이얼 플랜에 사서함 및 클라이언트 액세스 서버를 추가 합니다.
ms:assetid: 17fed308-ff0d-4e61-b9f9-e6680b6eccaa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996399(v=EXCHG.150)
ms:contentKeyID: 52058055
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# SIP URI 다이얼 플랜에 사서함 및 클라이언트 액세스 서버를 추가 합니다.

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-04-16_

클라이언트 액세스 서버와 사서함 서버를 SIP 다이얼 플랜에 추가할 수 있습니다. 클라이언트 액세스 서버와 사서함 서버를 내선 전화 또는 E.164 다이얼 플랜에 연결할 수는 없지만 이러한 서버는 모든 수신 전화에 응답합니다.

Microsoft Lync Server를 배포하는 경우 아웃바운드 통화가 정상적으로 작동하도록 설정하려면 Lync Server용으로 만든 모든 SIP URI 다이얼 플랜에 모든 클라이언트 액세스 서버와 사서함 서버를 수동으로 추가해야 합니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 SIP URI 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 서버를 SIP URI 다이얼 플랜에 추가

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  목록 보기에서 수정하려는 사서함 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **Exchange Server** 페이지에서 **통합 메시징**을 클릭합니다.

4.  **UM 서비스 설정** \> **연결된 다이얼 플랜**에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

5.  **UM 다이얼 플랜 선택** 창에서 SIP URI 다이얼 플랜을 선택한 다음 **추가**, **확인**, **저장**을 차례로 클릭합니다.

## 셸을 사용하여 사서함 서버를 SIP URI 다이얼 플랜에 추가

이 예에서는 `MyMailboxServer`라는 사서함 서버를 `MySIPDialPlan`이라는 SIP URI 다이얼 플랜에 추가하고 해당 사서함 서버가 새 통화를 수락하지 못하도록 차단합니다. 또한 시작 모드를 이중 모드로 설정하여 사서함 서버가 TCP 및 TLS 요청을 수락할 수 있도록 합니다.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan -Status Disabled -UMStartupMode Dual

이 예에서는 `MyMailboxServer`라는 사서함 서버를 `MySIPDialPlan` 및 `MySIPDialPlan2`라는 두 SIP 다이얼 플랜에 추가하고 다음 항목을 설정합니다.

  - IPv4 및 IPv6 주소를 모두 허용합니다.

  - 최대 수신 전화 수를 50으로 설정합니다.

  - Lync Server용 SIP 액세스 서비스를 구성합니다.

<!-- end list -->

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -MaxCallsAllowed 50 -SipAccessService northamerica.lyncpoolna.contoso.com

## EAC를 사용하여 클라이언트 액세스 서버를 SIP URI 다이얼 플랜에 추가

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  목록 보기에서 수정하려는 클라이언트 액세스 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **Exchange Server** 페이지에서 **통합 메시징**을 클릭합니다.

4.  **UM 통화 라우터 설정** \> **연결된 다이얼 플랜**에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

5.  **UM 다이얼 플랜 선택** 창에서 SIP URI 다이얼 플랜을 선택한 다음 **추가**, **확인**, **저장**을 차례로 클릭합니다.

## 셸을 사용하여 클라이언트 액세스 서버를 SIP URI 다이얼 플랜에 추가

이 예에서는 `MyClientAccessServer`라는 클라이언트 액세스 서버를 `MySIPDialPlan`이라는 SIP URI 다이얼 플랜에 추가합니다. 또한 시작 모드를 이중 모드로 설정하여 클라이언트 액세스 서버가 TCP 및 TLS 요청을 수락할 수 있도록 합니다.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan -Server MyClientAccessServer -UMStartupMode Dual

이 예에서는 `MyClientAccessServer`라는 클라이언트 액세스 서버를 `MySIPDialPlan` 및 `MySIPDialPlan2`라는 두 SIP 다이얼 플랜에 추가하고 서버가 IPv4 및 IPv6 주소를 모두 사용하도록 허용합니다.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -Server MyClientAccessServer

