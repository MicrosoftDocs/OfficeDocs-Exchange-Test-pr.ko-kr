---
title: 'PBX와 통신 하도록 VoIP 게이트웨이 연결 합니다.: Exchange 2013 Help'
TOCTitle: PBX와 통신 하도록 VoIP 게이트웨이 연결 합니다.
ms:assetid: 76bcdc54-3ec2-408a-bdbe-37826580dd62
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998872(v=EXCHG.150)
ms:contentKeyID: 50556019
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# PBX와 통신 하도록 VoIP 게이트웨이 연결 합니다.

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-15_

Microsoft Exchange Server 2013에서 UM(통합 메시징)을 위한 전화 통신 및 데이터 네트워크를 구성할 경우 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행하는 클라이언트 액세스 서버 및 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버와 통신하도록 VoIP 게이트웨이를 구성해야 합니다. 또한 조직의 PBX(Private Branch eXchanges)와 통신하도록 VoIP 게이트웨이를 구성해야 합니다. 이 항목의 정보와 링크를 사용하여 PBX와 통신하도록 VoIP 게이트웨이를 구성할 수 있습니다.

## VoIP 게이트웨이 구성

VoIP 게이트웨이를 구성할 때는 VoIP 게이트웨이 장치가 아날로그인지 아니면 디지털인지 또는 아날로그/디지털 혼용인지 고려해야 합니다. PBX에 연결된 VoIP 게이트웨이 인터페이스가 아날로그이면 VoIP 게이트웨이가 PBX와 통신할 수 있도록 해당 설정을 올바르게 구성해야 합니다. PBX에 연결된 VoIP 게이트웨이 인터페이스가 디지털이면 디지털 인터페이스가 PBX와 통신할 수 있도록 추가 구성을 하지 않아도 됩니다.

Exchange TechCenter의 다음 제안 리소스에서는 VoIP 게이트웨이와 PBX를 올바르게 구성하는 데 유용한 정보를 제공합니다.

  - **지원되는 VoIP 게이트웨이, IP PBX 및 PBX 문서**   [Exchange 2013에 대 한 전화 통신 관리자](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013)에는 VoIP 게이트웨이 및 PBX를 구성할 때 사용할 수 있는 구성 파일과 설정 정보가 있습니다.

  - **구성 및 기술 참고 사항**   [지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)에는 VoIP 게이트웨이 및 PBX를 구성할 때 사용할 수 있는 구성 파일과 설정 정보가 있습니다.

  - **AudioCodes 기반 VoIP 게이트웨이 구성**  [Microsoft Exchange Server 리소스 페이지](https://www.audiocodes.com/solutions/microsoft/exchange-server) 통합 메시징과 함께 사용 하기 위해 AudioCodes 기반 VoIP 게이트웨이 구성 하는데 도움이 되는 최신 지원 및 구성 정보를 제공 합니다.

  - **Dialogic 기반 VoIP 게이트웨이 구성**   [Dialogic 웹사이트](https://www.dialogic.com/) Dialogic 기반 VoIP 게이트웨이 대 한 최신 지원 및 구성 정보를 제공합니다.

통합 메시징 배포를 계획 하는 모든 고객은 통합 메시징 전문가의 도움을 얻을 것이 좋습니다. Exchange 통합 메시징 전문가 레거시에서 통합 메시징에 원활 하 게 업그레이드 하는 방법이 나 타사 음성 메일 시스템 고 계획 하 고 Exchange 통합 메시징이 있는 새 음성 메일 시스템을 배포 하는 데 도움이 있는지 확인 하는 데 도움이 됩니다. 새 음성 메일 시스템을 배포 하거나 하나 레거시 음성 업그레이드에 VoIP 게이트웨이, Pbx 및 통합 메시징에 대 한 중요 한 지식이 필요 합니다. 통합 메시징 전문가 게 문의 하는 방법에 대 한 자세한 내용은 [Microsoft Exchange Server 2013 통합 메시징 (UM) 전문가](http://go.microsoft.com/fwlink/p/?linkid=262708) 또는 [Microsoft 적절치](https://go.microsoft.com/fwlink/p/?linkid=261951)에 인증 된 UM 파트너를 참조 하십시오.

## 자세한 내용

[지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)

[지원 되는 VoIP 게이트웨이를 UM에 연결](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md)

