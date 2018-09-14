---
title: '가져오기 및 사용자 지정 인사말, 알림, 메뉴 및 음성 안내 내보내기: Exchange 2013 Help'
TOCTitle: 가져오기 및 사용자 지정 인사말, 알림, 메뉴 및 음성 안내 내보내기
ms:assetid: e82da5d5-625f-4d8b-8d31-ac45513aacfd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee681667(v=EXCHG.150)
ms:contentKeyID: 54651842
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 가져오기 및 사용자 지정 인사말, 알림, 메뉴 및 음성 안내 내보내기

 

_**적용 대상:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-04-08_

가져오기 및 UM (통합 메시징) 다이얼 플랜 및 자동 전화 교환에 사용 하 여 기록한 했을 때 오디오 파일을 내보낼 수 있습니다. 예, 다음 내보내기 및 Exchange의 이전 버전에서 업그레이드 하는 경우 오디오 파일의 복사본을 저장 하는 것이 좋습니다. 또는 파악 해야 다이얼 플랜을 구성 하기 전에 기록 된 오디오 음성 안내의 복사본을 가져오거나 자동 전화 교환 합니다.

오디오 파일은 다음과 같은 용도로 사용됩니다.

  - UM 다이얼 플랜에서는 오디오 파일이 사용자 지정 환영 인사말 및 정보 알림에 사용됩니다. Outlook Voice Access 사용자가 Outlook Voice Access 번호로 전화를 걸면 해당 오디오 파일이 재생됩니다.

  - UM 자동 전화 교환에서 오디오 파일은 사용자 지정된 업무 시간 및 업무 시간 외 환영 인사말, 정보 알림, 메뉴 음성 안내 및 탐색 메뉴에 사용되며, 발신자가 UM 자동 전화 교환으로 전화를 걸면 해당 오디오 파일이 재생됩니다.

사용자 지정 인사말, 알림, 메뉴 및 음성 안내에 지원되는 오디오 파일 형식은 다음과 같습니다.

  - Windows Media 오디오 9.2로 인코딩된 .wma 파일 - 96kbps/44kHz/스테레오 1패스 CBR(Windows 녹음기)

  - Windows Media 오디오 음성 9 - 8kbps/8kHz/모노 및 선형 PCM(16비트/샘플), 8kHz 오디오 코덱을 사용하여 인코딩된 .wav 파일

UM 다이얼 플랜에서 사용 되 고 {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 라는 시스템 사서함에 자동 전화 교환 및이 시스템 사서함에서 오디오 파일을 내보낼 하는 오디오 파일을 가져옵니다. 오디오 파일 가져오고 **Import-UMPrompt** 및 **Export-UMPrompt** cmdlet을 사용 하 여 내보낼 수 있습니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "UM 다이얼 플랜" 및 "UM 자동 전화 교환? [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 의 항목입니다.

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant)을 참조하십시오.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 UM 다이얼 플랜 및 자동 전화 교환에 사용할 사용자 지정 인사말, 알림, 메뉴 및 음성 안내 가져오기

이 예에서는 d:\\UMPrompts의 환영 인사말 파일 welcomegreeting.wav를 UM 다이얼 플랜 `MyUMDialPlan`으로 가져옵니다.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

이 예에서는 d:\\UMPrompts의 환영 인사말 파일 welcomegreeting.wav를 UM 자동 전화 교환 `MyUMAutoAttendant`로 가져옵니다.

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

## 셸을 사용하여 UM 다이얼 플랜 및 자동 전화 교환에서 사용자 지정 인사말, 알림, 메뉴 및 음성 안내 내보내기

이 예에서는 UM 다이얼 플랜 `MyUMDialPlan`의 환영 인사말을 내보내고 welcomegreeting.wav 파일로 저장합니다.

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav�? -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

이 예에서는 UM 자동 전화 교환 `MYUMAutoAttendant`의 업무 시간 환영 인사말을 내보내고 BusinessHoursWelcomeGreeting.wav 파일로 저장합니다.

    $prompt = Export-UMPrompt -BusinessHoursWelcomeGreeting -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "d:\UMPrompts\BusinessHoursWelcomeGreeting.wav" -Value $prompt.AudioData -Encoding Byte

