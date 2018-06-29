---
title: '보낸사람 신뢰도 관리 합니다.: Exchange 2013 Help'
TOCTitle: 보낸사람 신뢰도 관리 합니다.
ms:assetid: f2716bd9-e3ac-46d9-9264-4e3dabfa0f38
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125186(v=EXCHG.150)
ms:contentKeyID: 50484521
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보낸사람 신뢰도 관리 합니다.

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-08_

보낸사람 신뢰도 프로토콜 분석 에이전트에 의해 제공 됩니다. 보낸사람 신뢰도 보낸의 다양 한 특성에 따라 메시지를 차단합니다. 보낸사람 신뢰도 인바운드 메시지에 대해 수행할 작업을 확인 하려면 보낸사람에 대 한 영구 데이터에 의존 합니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)의 "스팸 방지 기능" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 기본적으로 스팸 방지 기능은 사서함 서버의 전송 서비스에서 사용되지 않도록 설정되어 있습니다. 일반적으로 Exchange 조직에서 들어오는 메시지를 수락하기 전에 스팸 방지 필터링을 미리 수행하지 않은 경우에만 사서함 서버에서 스팸 방지 기능을 사용하도록 설정할 수 있습니다. 자세한 내용은 [사서함 서버에서 스팸 방지 기능을 사용 하도록 설정](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)을 참조하세요.

  - 프로토콜 분석 에이전트는 보낸사람 신뢰도 기능에 대 한 원본으로 사용 하는 에이전트입니다. 보낸사람 신뢰도 사용 하지 않는 경우 프로토콜 분석 에이전트는 계속 사용할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용 하 여 하거나 보낸사람 신뢰도 사용 하지 않도록 설정

이 예에서는 보낸사람 신뢰도 비활성화합니다.

    Set-SenderReputationConfig -Enabled $false

보낸사람 신뢰도 설정 하는이 예제입니다.

    Set-SenderReputationConfig -Enabled $true

## 작동 여부는 어떻게 확인합니까?

성공적으로 사용 하도록 설정 하거나 했는지 보낸사람 신뢰도 사용 하지 않도록 설정을 확인 하려면 다음을 수행 합니다.

1.  프로토콜 분석 에이전트를 설치 하 고 다음 명령을 실행 하 여 활성화를 확인 합니다.
    
        Get-TransportAgent

2.  다음 명령을 실행 하 여 구성한 보낸사람 신뢰도 값을 확인 합니다.
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

## 셸을 사용 하 여 하거나 내부 또는 외부 메시지에 대 한 보낸사람 신뢰도 사용 하지 않도록 설정

기본적으로 보낸사람 신뢰도 외부 메시지에 사용 되며 내부 메시지에 사용할 수 없습니다. 메시지를 외부 Exchange 조직에 대 한 인증 되지 않은 연결에서 제공 하는 경우 외부 것으로 간주 됩니다. 인증 된 연결에서 제공 하 고 보낸 사람의 도메인이 Exchange 조직에서 신뢰할 수 있는 도메인으로 구성 하는 경우 메시지 내부 것으로 간주 됩니다.

외부 메시지에 대 한 보낸사람 신뢰도 사용 하지 않으려면 다음 명령을 실행 합니다.

    Set-SenderReputationConfig -ExternalMailEnabled $false

외부 메시지에 대 한 보낸사람 신뢰도 사용 하도록 설정 하려면 다음 명령을 실행 합니다.

    Set-SenderReputationConfig -ExternalMailEnabled $true

내부 메시지에 대 한 보낸사람 신뢰도 사용 하지 않으려면 다음 명령을 실행 합니다.

    Set-SenderReputationConfig -InternalMailEnabled $false

내부 메시지에 대 한 보낸사람 신뢰도 사용 하도록 설정 하려면 다음 명령을 실행 합니다.

    Set-SenderReputationConfig -InternalMailEnabled $true

## 작동 여부는 어떻게 확인합니까?

성공적으로 사용 하도록 설정 하거나 했는지 내부 및 외부 메시지에 대 한 보낸사람 신뢰도 사용 하지 않도록 설정을 확인 하려면 다음을 수행 합니다.

1.  다음 명령을 실행합니다.
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

2.  표시된 값이 구성한 값과 일치하는지 확인합니다.

## 셸을 사용 하 여 보낸사람 신뢰도 속성을 구성 하려면

보낸사람 신뢰도 속성을 구성 하려면 다음 명령을 실행 합니다.

    Set-SenderReputationConfig -SrlBlockThreshold <Value> -SenderBlockingPeriod <Hours>

이 예에서는 보낸사람 신뢰도 수준 (SRL) 차단 임계값을 6으로 설정 하는 및 36 시간에 대 한 확인 된 유해한 보낸사람 IP 차단 목록에 추가 하려면 보낸사람 신뢰도 구성 합니다.

    Set-SenderReputationConfig -SrlBlockThreshold 6 -SenderBlockingPeriod 36

## 작동 여부는 어떻게 확인합니까?

보낸사람 신뢰도 속성을 성공적으로 구성 했는지를 확인 하려면 다음을 수행 합니다.

1.  다음 명령을 실행합니다.
    
        Get-SenderReputationConfig

2.  표시된 값이 구성한 값과 일치하는지 확인합니다.

## 셸을 사용 하 여 개방형 프록시 서버의 검색에 대 한 아웃 바운드 액세스를 구성 하려면

인터넷 및 프로토콜 분석 에이전트를 실행 하는 Exchange 서버 사이 있는 모든 방화벽을 통과를 보낸사람 신뢰도 허용 하기 위한 추가 단계를 수행 해야 합니다. 다음 표에서 보낸사람 신뢰도에 필요한 아웃 바운드 포트를 보여줍니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>프로토콜</th>
<th>포트</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SOCKS4, SOCKS5</p></td>
<td><p>1081, 1080</p></td>
</tr>
<tr class="even">
<td><p>Wingate, 텔넷, Cisco</p></td>
<td><p>23</p></td>
</tr>
<tr class="odd">
<td><p>HTTP CONNECT, HTTP POST</p></td>
<td><p>6588, 3128, 80</p></td>
</tr>
</tbody>
</table>


개방형 프록시 서버를 감지에 대 한 아웃 바운드 액세스를 구성 하려면 다음 명령을 실행 합니다.

    Set-SenderReputationConfig -ProxyServerName <String> -ProxyServerPort <Port> -ProxyServerType <String>

이 예에서는 server01 포트 80에서 HTTP 연결 프로토콜을 사용 하는 개방형 프록시 서버를 사용 하도록 보낸사람 신뢰도 구성 합니다.

    Set-SenderReputationConfig - ProxyServerName SERVER01 -ProxyServerPort 80 -ProxyServerType HttpConnect

## 작동 여부는 어떻게 확인합니까?

개방형 프록시 서버는 검색에 대 한 아웃 바운드 액세스 성공적으로 구성 했는지를 확인 하려면 다음을 수행 합니다.

1.  다음 명령을 실행합니다.
    
        Get-SenderReputationConfig | Format-List ProxyServer*

2.  표시된 값이 구성한 값인지 확인합니다.

