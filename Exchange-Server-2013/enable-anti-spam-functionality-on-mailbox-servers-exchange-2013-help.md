---
title: '사서함 서버에서 스팸 방지 기능을 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 사서함 서버에서 스팸 방지 기능을 사용 하도록 설정
ms:assetid: 59d22c5e-64bc-4879-8ad1-364862b6ba11
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201691(v=EXCHG.150)
ms:contentKeyID: 50483178
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 서버에서 스팸 방지 기능을 사용 하도록 설정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-01-23_

Microsoft Exchange Server 2013에서는 사서함 서버의 전송 서비스에서 다음 스팸 방지 에이전트를 사용할 수 있지만 기본적으로 설치되지는 않습니다.

  - 콘텐츠 필터 에이전트

  - 보낸 사람 ID 에이전트

  - 보낸 사람 필터 에이전트

  - 보낸 사람 신뢰도 대한 프로토콜 분석 에이전트

Exchange 관리 셸의 스크립트를 사용하여 사서함 서버에 이러한 스팸 방지 에이전트를 설치할 수 있습니다. 일반적으로 조직에서 사전 스팸 방지 필터링 없이 들어오는 모든 메일을 수락하는 경우에만 사서함 서버에 스팸 방지 에이전트를 설치합니다.


> [!NOTE]
> 받는 사람 필터 에이전트 사서함 서버에서 사용할 수는 있지만에 구성 하면 안됩니다. 다른 유효한 받는 사람이 포함 된 메시지에 유효 하지 않거나 차단 된 받는 사람을 하나를 검색 하는 사서함 서버에서 받는 사람 필터링을 하는 경우에 메시지가 거부 됩니다. 기본적으로 받는 사람 필터 에이전트를 사용 하지만 모든 받는 사람을 차단 하도록 구성 되지 않았습니다. 자세한 내용은 <A href="manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md">Edge 전송 서버의 받는 사람 필터링 관리</A>을 참조 하십시오.



사서함 서버의 전송 서비스에서 사용 가능한 스팸 방지 에이전트를 설치 하지만 메시지에서 작동 하는 사서함 서버에 도달 하기 전에 다른 Exchange 스팸 방지 에이전트가 있는 경우 어떻게 됩니까? 예, 경우에 어떻게 해야 Edge 전송 서버를 경계 네트워크에 있습니까? 사서함 서버에서 스팸 방지 에이전트 다른 Exchange 스팸 방지 에이전트에 의해 메시지에 추가 되는 스팸 방지 X-헤더 값을 인식 하 고 이러한 X-헤더를 포함 하는 메시지를 다시 검사 하지 않고 통과 키를 누릅니다. 그러나 받는 사람 필터 에이전트에 의해 수행 되는 받는 사람 조회 사서함 서버에서 다시 발생 합니다.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 구성" 항목

  - 연결 필터 에이전트와 첨부 파일 필터 에이전트는 사서함 서버에서는 사용할 수 없고 Edge 전송 서버에서만 사용할 수 있지만, 맬웨어 에이전트는 기본적으로 사서함 서버에 설치되고 사용됩니다. 자세한 내용은 [맬웨어 방지 보호](anti-malware-protection-exchange-2013-help.md) 항목을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 셸을 사용하여 Install-AntispamAgents.ps1 스크립트 실행

다음 명령을 실행합니다.

    & $env:ExchangeInstallPath\Scripts\Install-AntiSpamAgents.ps1

## 이 단계의 작동 여부는 어떻게 확인합니까?

스크립트가 오류 없이 실행되고 Microsoft Exchange Transport Service를 다시 시작하라는 메시지가 나타나면 이 단계가 제대로 작동한 것입니다.

## 2단계: 셸을 사용하여 Microsoft Exchange Transport Service 다시 시작

다음 명령을 실행합니다.

    Restart-Service MSExchangeTransport

## 이 단계의 작동 여부는 어떻게 확인합니까?

Microsoft Exchange Transport Service가 오류 없이 다시 시작되면 이 단계가 제대로 작동한 것입니다.

## 3단계: 셸을 사용하여 조직에 내부 SMTP 서버 지정

보낸 사람 ID 에이전트가 무시하도록 할 내부 SMTP 서버의 IP 주소를 지정해야 합니다. 적어도 하나의 내부 SMTP 서버 IP 주소를 지정해야 합니다. 스팸 방지 에이전트를 실행하는 사서함 서버가 조직의 유일한 SMTP 서버일 경우 해당 컴퓨터의 IP 주소를 지정하십시오.

기존 값에 영향을 주지 않고 내부 SMTP 서버의 IP 주소를 추가하려면 다음 명령을 실행합니다.

    Set-TransportConfig -InternalSMTPServers @{Add="<ip address1>","<ip address2>"...}

이 예에서는 조직의 전송 구성에 내부 SMTP 서버 주소 10.0.1.10 및 10.0.1.11을 추가합니다.

    Set-TransportConfig -InternalSMTPServers @{Add="10.0.1.10","10.0.1.11"}

## 이 단계의 작동 여부는 어떻게 확인합니까?

적어도 하나의 내부 SMTP 서버 IP 주소가 지정되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-TransportConfig | Format-List InternalSMTPServers

2.  적어도 하나의 유효한 내부 SMTP 서버 IP 주소가 표시되는지 확인합니다.

