---
title: '사서함 서버에서 UM 설정 관리: Exchange 2013 Help'
TOCTitle: 사서함 서버에서 UM 설정 관리
ms:assetid: 6df4853d-21d2-473f-b0ca-ebc996d8794a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998815(v=EXCHG.150)
ms:contentKeyID: 50556013
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMServerPropertiesPropertyPage
ms.translationtype: MT
---

# 사서함 서버에서 UM 설정 관리

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-11_

Microsoft Exchange 통합 메시징 서비스를 실행 중인 사서함 서버를 설치하면 동시 통화 수, TCP 및 TLS(전송 계층 보안) 수신 대기 포트, 상태, UM 시작 모드 등 여러 옵션을 구성할 수 있습니다.


> [!IMPORTANT]
> 사서함 서버가 UM(통합 메시징)에 대한 통화를 처리할 수 있기 전에는 이들 서버를 UM 다이얼 플랜에 추가하지 않아도 됩니다. 단, UM과 Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server를 통합하는 경우는 예외입니다. 기본적으로 조직의 모든 사서함 서버는 수신 전화에 응답할 수 있습니다.



통합 메시징 및 사서함 서버와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 항목의 "사서함 서버(UM 서비스)" 항목을 참조하십시오.

  - 클라이언트 액세스 서버와 동일한 컴퓨터나 별도의 컴퓨터에 사서함 서버가 설치되어 있는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 사서함 서버에서 통합 메시징 속성 구성

이 예에서는 모든 SIP(Session Initiation Protocol) 다이얼 플랜에서 `MyMailboxServer`라는 사서함 서버를 제거합니다.

    Set-UMService -Identity MyMailboxServer -DialPlans $null

이 예에서는 `MyMailboxServer`라는 사서함 서버를 UM SIP 다이얼 플랜 `MySIPDialPlanName`에 추가하고 수신 음성 통화의 최대 개수를 설정합니다.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -MaxCalls 150 

이 예에서는 `MyUMServer`라는 사서함 서버에서 시작 모드를 이중 모드로 설정합니다.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -UMStartUpMode -Dual 

## 셸을 사용하여 사서함 서버 속성 보기

다음 예에서는 모든 사서함 서버의 목록을 표시합니다.

    Get-UMService

이 예에서는 `MyMailboxServer`라는 사서함 서버의 속성을 서식 있는 목록으로 표시합니다.

    Get-UMService -Identity MyMailboxServer | Format-List

