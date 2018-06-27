---
title: 'VoIP 보안 설정 구성: Exchange 2013 Help'
TOCTitle: VoIP 보안 설정 구성
ms:assetid: b5335654-c766-4f3f-883c-f31263e1d9c1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201721(v=EXCHG.150)
ms:contentKeyID: 50483951
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# VoIP 보안 설정 구성

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2014-10-16_

UM (통합 메시징) 다이얼 플랜에 대 한 IP (VoIP) 보안을 통해 음성을 설정할 수 있습니다. 기본적으로 UM 다이얼 플랜을 만들 때 보안 되지 않은 모드 또는 암호화 사용 합니다. Exchange 서버 단일 또는 여러 UM 다이얼 플랜에 대 한 호출에 응답할 수 및 다른 VoIP 보안 설정을 포함 하는 다이얼 플랜에 대 한 통화에 응답할 수 있습니다. Office 365 및 Exchange Online 보안 모드 필요 하 고 사용 하지 않도록 설정할 수 없습니다.

사용 하 여 UM 다이얼 플랜을 구성 하는 경우 프로토콜 SIP (Session Initiation) 보안 또는 보안 모드를 UM 다이얼 플랜에 대 한 호출에 응답 하는 Exchange 서버는 암호화 (SIP 보안된 모드)에 대 한 트래픽을 또는 모두 실시간 전송 프로토콜 (RTP) 미디어 채널 및 신호 트래픽 (보안 모드)에 대 한 SIP 신호 SIP 합니다.


> [!IMPORTANT]
> 온-프레미스 및 하이브리드 배포의 경우는 SipTCPListeningPort, SipTLSListeningPort, 또는 Microsoft Exchange 통합 메시징 호출 라우터 서비스 또는 Microsoft Exchange 통합 메시징 서비스를 실행 하는 사서함 서버를 실행 하는 클라이언트 액세스 서버에서 UMStartUpMode를 구성할 때 해야 SIP 및 RTP 네트워크 트래픽을 허용 하도록 Windows 방화벽 규칙을 올바르게 구성 해야 합니다.



다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 UM 다이얼 플랜에서 VoIP 보안 설정 구성

1.  EAC에서 **통합** 메시징으로 이동 \> VoIP 보안을 변경 하려는 UM 다이얼 플랜 **UM 다이얼 플랜** 을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

2.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

3.  **일반**, **VoIP 보안 모드** 아래에서 다음 옵션 중 하나를 선택 합니다.
    
      - **SIP 보안**
    
      - **보안 되지 않음** (기본값)
    
      - **보안**

4.  **저장**을 클릭합니다.

## 셸을 사용 하 여 UM 다이얼 플랜에서 VoIP 보안 구성

이 예에서는 `MySecureDialPlan` 라는 SIP 및 RTP 트래픽 모두를 암호화 하는데 UM 다이얼 플랜을 구성 합니다.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Secured

이 예제에서는 SIP 암호화 하지만 암호화 하지는 RTP 트래픽을 `MySecureDialPlan` 이라는 UM 다이얼 플랜을 구성 합니다.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity SIPsecured

이 예에서는 `MySecureDialPlan` 라는 SIP 및 RTP 트래픽 암호화 하지를 UM 다이얼 플랜을 구성 합니다.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Unsecured

