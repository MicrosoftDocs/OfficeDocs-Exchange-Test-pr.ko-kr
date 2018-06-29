---
title: '음성 메일 미리 보기 advisor: Exchange 2013 Help'
TOCTitle: 음성 메일 미리 보기 advisor
ms:assetid: 0957dd54-df6d-4b50-9db5-4757f548b899
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee364730(v=EXCHG.150)
ms:contentKeyID: 51407663
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메일 미리 보기 advisor

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange UM(통합 메시징)에는 ASR(자동 음성 인식)을 사용하여 음성 메일 메시지에 음성 메일 오디오 파일의 텍스트 버전을 추가하는 음성 메일 미리 보기라는 기능이 포함되어 있습니다. ASR은 특히 알 수 없는 음성과 잡음이 섞인 전화 오디오를 녹음할 때는 정확하지 않을 수 있습니다. 일부 조직에는 일관되게 오류가 없거나 오류가 거의 없는 음성 메시지의 기록이 필요합니다. 이러한 조직은 음성 메일 미리 보기 파트너 프로그램을 통해 요구 사항을 충족할 수 있습니다.

음성 메일 미리 보기에서는 [Microsoft 음성 기술](http://go.microsoft.com/fwlink/p/?linkid=187348)을 사용하여 녹음된 오디오의 텍스트 버전을 제공합니다. 음성 메일 텍스트는 MicrosoftOutlook Web App, Outlook 2010 이상 버전 및 기타 전자 메일 프로그램 내의 전자 메일 메시지에 표시됩니다.

기본적으로 온-프레미스 또는 하이브리드 배포에서 사용자가 UM을 사용하도록 설정하면 지원되는 UM 언어 팩이 설치되어 있는 경우 음성 메일 미리 보기가 전송됩니다. Exchange Online에서 사용자가 UM을 사용하도록 설정하면 모든 UM 언어 팩이 설치됩니다. 그러나 설치되는 모든 언어에서 음성 메일 미리 보기가 지원되는 것은 아닙니다.

음성 메일 미리 보기 기능을 위한 향상된 기록 서비스 및 지원을 제공하는 음성 메일 미리 보기 파트너가 있습니다. 이러한 파트너는 ASR을 사용하여 만들어진 음성 메일 기록을 수정할 인력을 고용하며, 요구 사항을 준수하여 Exchange UM과의 상호 운용을 인증 받아야 합니다.

음성 메일 미리 보기를 보내지는지 확인 하는 경우에 사용자에 게 충분히 정확 하지에 나열 된 [Microsoft 적절치](https://go.microsoft.com/fwlink/p/?linkid=281966) 및 기호를 이러한는 추가 비용 인증 된 음성 메일 미리 보기 파트너 중 하나에 문의할 수 있습니다.

**목차**

개요

Exchange Unified Messaging Voice Mail Partner program

Voice Mail Preview partners certified for Exchange Unified Messaging

Configuring Voice Mail Preview partners

VoIP or media gateways and IP PBX support

## 개요

통합 메시징에서는 음성 메시지의 오디오를 녹음할 때 ASR을 사용하여 오디오 파일에서 음성 메일 미리 보기 텍스트를 만든 다음 사용자에게 배달할 전체 음성 메시지를 전송합니다. 생성된 각 음성 메시지에 대해 통합 메시징은 메시지에 포함된 음성 메일 미리 보기의 신뢰 수준을 결정합니다. 이때 녹음된 소리가 메시지의 단어, 숫자 및 구문과 얼마나 잘 일치하는지 측정합니다. 시스템이 일치하는 항목을 쉽게 찾으면 신뢰 수준이 높아집니다. 일반적으로 신뢰 수준이 높을수록 정확도도 높습니다.

음성 메일 미리 보기 텍스트의 정확도는 다양한 요소에 따라 달라지며 경우에 따라 이러한 요소를 제어하지 못할 수도 있습니다. 그러나 다음과 같은 경우에는 텍스트가 더욱 정확해집니다.

  - 발신자가 비속어, 기술적 은어 또는 이상한 단어나 구를 사용하지 않고 간단한 음성 메시지를 남긴 경우

  - 발신자가 음성 메일 시스템에서 쉽게 인식하고 번역하는 언어를 사용합니다. 일반적으로 너무 빠르거나 너무 조용히 말하지 않는 발신자와 어조가 강하지 않은 발신자가 남긴 음성 메시지가 더 정확한 문장과 구문을 생성합니다.

  - 음성 메시지에 주위 소음, 울림이 없으며, 오디오가 끊기지 않는 경우

통합 메시징을 사용하는 대부분의 고객은 음성 메일 미리 보기가 사용자에게 충분히 정확하다고 여깁니다. 그러나 알 수 없는 음성과 주위 소음이 전화를 통해 녹음된 경우 ASR이 적용되면 음성 메일 미리 보기 텍스트가 대개 완전히 정확하지는 않습니다. 신뢰 수준이 일관되게 낮거나 받은 음성 메일 미리 보기가 그다지 정확하지 않은 경우 사용자가 받는 음성 메일 미리 보기의 정확도를 다음과 같이 높일 수 있습니다.

  - 음성 메일 미리 보기 파트너의 음성 녹음 서비스에 등록합니다.

  - 음성 메일 미리 보기 파트너에 등록한 후 파트너가 UM을 사용할 수 있도록 설정합니다. 음성 메일 미리 보기 파트너에 대해 UM을 구성하는 방법에 대한 자세한 내용은 [사용자에 대 한 음성 메일 미리 보기 파트너 서비스를 구성 합니다.](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md)을 참조하십시오.

음성 메일 미리 보기 파트너에 등록하면 조직의 Exchange 서버에서는 음성 메시지에 대해 음성 메일 미리 보기 텍스트를 생성하고 사용자 사서함으로 음성 메시지를 전송하는 대신, 오디오 파일이 첨부된 음성 메시지를 음성 메일 미리 보기 파트너에 리디렉션합니다. 그런 다음 음성 메일 미리 보기 파트너가 생성한 음성 메일 미리 보기 텍스트가 포함된 전자 메일 메시지는 받는 사람의 사서함으로 배달되기 위해 조직의 Exchange 서버로 전송됩니다.


> [!IMPORTANT]
> 통합 메시징 배포를 계획 하는 모든 고객은 UM 전문가의 도움을 얻을 것이 좋습니다. UM 전문가 레거시 음성 메일 시스템에서 UM을 원활 하 게 전환 있는지 확인 하는데 도움이 됩니다. 새 배포를 수행 하거나 레거시 음성 메일 시스템을 업그레이드 필요 VoIP 게이트웨이, IP Pbx, Pbx, 세션 테두리 컨트롤러 (Sbc)에 대 한 중요 한 기술 및 메시징 통합 합니다. UM 전문가 게 문의 하는 방법에 대 한 자세한 내용은 <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 통합 메시징 (UM) 전문가</A> 나 <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">통합 메시징에 대 한 Microsoft 적절치</A>를 참조 하십시오.



맨 위로 이동

## Exchange 통합 메시징 음성 메일 파트너 프로그램

Exchange UM과 상호 운용되는 음성 메일 미리 보기 파트너로 인증을 받으려면 파트너는 음성 메일 미리 보기 상호 운용성 사양에 포함된 요구 사항을 구현해야 하며 파트너 솔루션은 독립적인 인증 공급업체의 인증을 받아야 합니다. 기록 서비스가 Exchange UM과 연동됨을 인증 받으려면 [Exchange 통합 메시징의 음성 메일 미리 보기 파트너](mailto:vmppp@microsoft.com)에 요청을 제출하십시오.

## Exchange 통합 메시징에 대해 인증된 음성 메일 미리 보기 파트너

이미 배포한 통합 메시징 조직에서 할 필요가 없고 지원 서비스를 제공 하는 인증 된 음성 메일 미리 보기 파트너에 대 한 찾는 [Microsoft 적절치](https://go.microsoft.com/fwlink/p/?linkid=281966)를 참조 하십시오. 이러한 소프트웨어 공급 업체 Exchange UM와 상호 운용으로 인증 합니다.

## 음성 메일 미리 보기 파트너 구성

구성된 UM은 오디오가 포함된 음성 메시지를 전용 음성 메일 미리 보기 파트너로 전달합니다. 그러면 파트너는 오디오 파일을 받아 음성 메일 미리 보기 텍스트를 만듭니다. 그러나 사용자가 사서함에 음성 메시지와 함께 음성 메일 미리 보기를 받도록 허용하려면 UM 사서함 정책을 구성하고 사용자를 UM 사서함 정책과 연결한 다음 사용자가 Outlook 2010 이상 버전이나 Outlook Web App의 음성 메시지에서 음성 메일 미리 보기를 받을 수 있는지 확인하도록 해야 합니다. 음성 메일 미리 보기 파트너에 대해 UM을 구성하는 방법에 대한 자세한 내용은 [사용자에 대 한 음성 메일 미리 보기 파트너 서비스를 구성 합니다.](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md)을 참조하십시오.

## VoIP 또는 미디어 게이트웨이 및 IP PBX 지원

조직에 대해 VoIP 게이트웨이 및 IP PBX를 구성하는 것은 음성 메일 미리 보기 파트너로 통합 메시징을 성공적으로 배포하기 위해 완료해야 하는 어려운 배포 작업입니다. VoIP 게이트웨이 및 IP PBX를 구성하는 데 도움이 될 수 있는 정보 및 구성 방법에 대한 최신 정보는 [Exchange 2013에 대 한 전화 통신 관리자](telephony-advisor-for-exchange-2013-exchange-2013-help.md) 또는 [지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)를 참조하십시오.

테스트와 상호 운용성 Exchange UM의 VoIP 게이트웨이 Microsoft Unified Communications 개방형 상호 운용성 프로그램 통합 되었습니다. 자세한 내용은 [Microsoft 통합 커뮤니케이션의 개방형 상호 운용성 프로그램](https://go.microsoft.com/fwlink/p/?linkid=132071)을 참조 하십시오.

맨 위로 이동

