---
title: '오디오 코덱 변경: Exchange 2013 Help'
TOCTitle: 오디오 코덱 변경
ms:assetid: 139b2ccd-28c5-46c0-9050-777f4f59aade
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996342(v=EXCHG.150)
ms:contentKeyID: 50482553
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 오디오 코덱 변경

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

통합 메시징에서는 음성 메일 메시지를 만드는 데 MP3, WMA(Windows Media Audio), GSM(Group System Mobile) 06.10 및 G.711 PCM(Pulse Code Modulation) Linear의 네 가지 코덱 중 하나를 사용할 수 있습니다. 기본적으로 UM(통합 메시징) 다이얼 플랜을 만들 때 UM 다이얼 플랜에서는 MP3 오디오 코덱을 사용하여 음성 메시지를 녹음합니다. MP3 오디오 형식은 여러 운영 체제, 전자 메일 클라이언트 및 MP3 플레이어에서 사용되는 잘 알려진 오디오 형식입니다. UM 다이얼 플랜을 만든 후 WMA, GSM 06.10 또는 G.711 PCM Linear 오디오 코덱을 비롯한 다른 오디오 형식 중 하나를 사용하도록 UM 다이얼 플랜을 구성할 수 있습니다. 음성 메시지를 들으려면 휴대폰이나 컴퓨터에 호환되는 오디오 소프트웨어 응용 프로그램이 설치되어 있어야 합니다.

UM 다이얼 플랜과 관련된 추가 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 통합 메시징 다이얼 플랜의 오디오 코덱 변경

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **설정**의 **오디오 코덱** 아래에서 드롭다운 목록을 사용하여 다음 중 하나를 선택합니다.
    
      - MP3
    
      - WMA
    
      - GSM
    
      - G711

5.  **저장**을 클릭합니다.

## 셸을 사용하여 통합 메시징 다이얼 플랜의 오디오 코덱 변경

이 예에서는 `MyUMDialPlan`이라는 UM 다이얼 플랜의 오디오 코덱을 G.711로 설정합니다.

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec G711

이 예에서는 `MyUMDialPlan`이라는 UM 다이얼 플랜의 오디오 코덱을 WMA로 설정합니다.

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec Wma

