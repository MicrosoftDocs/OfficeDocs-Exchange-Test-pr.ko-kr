---
title: 'UM에 대 한 인증서를 배포합니다.: Exchange 2013 Help'
TOCTitle: UM에 대 한 인증서를 배포합니다.
ms:assetid: 95658f6f-eac2-4674-90e7-f2d3f25c5242
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee681661(v=EXCHG.150)
ms:contentKeyID: 52058117
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM에 대 한 인증서를 배포합니다.

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-04-29_

상호 TLS(상호 전송 계층 보안)를 사용하여 Microsoft Exchange 2013 서버와 VoIP 게이트웨이, IP PBX, SBC(Session Border Controller) 및 Microsoft Lync Server 간 전송되는 데이터를 암호화할 수 있습니다. 인증서는 정보를 디지털 방식으로 암호화하고 서명하는 데 사용되는 전자 키(공개 및 개인) 쌍에 인증서 소유자의 ID를 바인딩합니다.

Exchange 2010 조직에서 SIP 보안이나 보안된 다이얼 플랜을 사용하는 경우 사용된 인증서를 Microsoft Exchange UM 통화 라우터 서비스를 실행하는 Exchange 2013 클라이언트 액세스 서버 및 Microsoft Exchange UM 서비스를 실행하는 사서함 서버로 가져와야 합니다. UM 및 UM 통화 라우터 서비스에는 다음 인증서 중 하나를 사용할 수 있습니다.

  - 자체 서명된(Exchange) 인증서

  - 내부 PKI(공개 키 인프라) 인증서

  - 타사 상업용 인증서

기본적으로 통합 메시지를 설치하면 자체 서명된 인증서가 만들어지고 사용되며, 이 자체 서명된 인증서를 VoIP 게이트웨이, IP PBX 및 SBC에서 사용할 수 있습니다. 단, UM과 Lync Server를 통합한 경우에는 사용할 수 없습니다. Lync Server에서 사용할 인증서를 배포할 경우 Exchange 인증서 마법사나 **New-ExchangeCertificate** cmdlet을 사용하여 내부 또는 PKI CA(인증 기관)에서 발급한 인증서를 가져오거나 통합 메시징 및 Lync Server에서 상호 신뢰할 수 있는 상업용 또는 타사 인증서를 구입해야 합니다.

## VoIP 게이트웨이, IP PBX 및 SBC용 인증서 배포

UM에서 VoIP 게이트웨이, IP PBX 및 SBC 간 전송되는 데이터를 암호화할 수 있도록 하려면 다음을 수행해야 합니다.

  - 자체 서명 UM 인증서를 사용하고 새 Exchange 인증서 요청을 만들고 내부 PKI 인증서를 가져오거나 UM, VoIP 게이트웨이, IP PBX 및 SBC 간 상호 TLS에 사용할 수 있는 타사 상업용 인증서를 구입합니다.

  - 조직의 모든 클라이언트 액세스 및 사서함 서버에서 사용할 인증서를 가져옵니다.

  - 인증서를 UM 서비스에서 사용하도록 설정합니다.

  - VoIP 게이트웨이, IP PBX 및 SBC에서 인증서를 가져옵니다.

  - UM 다이얼 플랜을 SIP 보안 또는 보안으로 구성합니다.

  - 조직의 클라이언트 액세스 및 사서함 서버에서 UM 시작 모드를 구성합니다.

  - FQDN(정규화된 도메인 이름)으로 필요한 UM IP 게이트웨이를 만듭니다.

  - TLS 포트 5061을 사용하도록 UM IP 게이트웨이의 수신 대기 포트를 구성합니다.

  - 모든 클라이언트 액세스 서버에서 통합 메시징 통화 라우터 서비스를 다시 시작하고 모든 사서함 서버에서 Microsoft Exchange 통합 메시징 서비스를 다시 시작합니다.

## Lync Server용 인증서 배포

UM 및 Lync Server 간 전송되는 데이터를 암호화하려면 다음을 수행해야 합니다.

  - 새 Exchange 인증서 요청을 만들고 내부 PKI 인증서를 가져오거나 타사 상업용 인증서를 구입합니다. 이 인증서는 UM 및 Lync Server에서 상호 신뢰해야 합니다.

  - 조직의 모든 클라이언트 액세스 및 사서함 서버에서 사용할 인증서를 가져옵니다.

  - 인증서를 UM 서비스에서 사용하도록 설정합니다.

  - Lync Server를 실행하는 컴퓨터에서 인증서를 가져옵니다.

  - SIP URI UM 다이얼 플랜을 SIP 보안 또는 보안으로 구성합니다.

  - 조직의 클라이언트 액세스 및 사서함 서버에서 UM 시작 모드를 구성합니다.

  - Lync Server 컴퓨터에서 OcsUmUtil.exe를 실행합니다.

  - 조직의 모든 클라이언트 액세스 서버에서 통합 메시징 통화 라우터 서비스를 다시 시작하고 조직의 모든 사서함 서버에서 Microsoft Exchange 통합 메시징 서비스를 다시 시작합니다. 자세한 내용은 [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조하십시오.

  - 모든 Lync Server 서버에서 Enterprise Edition 프런트 엔드 풀의 일부인 Lync Server 프런트 엔드 서비스를 다시 시작하거나 Standard Edition 프런트 엔드 서버를 다시 시작합니다. **Stop-CsWindowsService** cmdlet을 사용하여 Lync Server 서비스를 중지하고 **Start-CsWindowsService** cmdlet을 사용하여 Lync Server 서비스를 시작할 수 있습니다.
    
    **Start-CsWindowsService** 및 **Stop-CsWindowsService** cmdlet은 일반 Windows PowerShell cmdlet인 **Start-Service** 및 **Stop-Service**와 비슷합니다. 원하는 경우 **Start-Service** 또는 **Stop-Service** cmdlet을 사용하여 Lync Server 서비스를 시작하고 중지할 수 있습니다. 단, **Start-CsWindowsServiceStop-CsWindowsService** cmdlet에는 원격 컴퓨터에서 Lync Server 서비스를 보다 쉽게 중지하고 시작할 수 있도록 해주는 *ComputerName* 매개 변수가 포함됩니다. 원격 컴퓨터에서 Lync Server 서비스를 보다 쉽게 중지하고 시작하려면 *ComputerName* 매개 변수 뒤에 원격 컴퓨터의 FQDN(정규화된 도메인 이름)을 포함합니다. **Start-Service** 및 **Stop-Service** cmdlet에는 비슷한 매개 변수가 없습니다.
    

    > [!NOTE]
    > 따라서 UM 및 Lync Server를 완전히 통합하려면 조직의 모든 클라이언트 액세스 또는 사서함 서버에서 ExchUcUtil.ps1 스크립트도 실행해야 합니다.


