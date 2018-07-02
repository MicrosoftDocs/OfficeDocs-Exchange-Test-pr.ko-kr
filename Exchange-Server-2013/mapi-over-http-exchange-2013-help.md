---
title: 'MAPI over HTTP: Exchange 2013 Help'
TOCTitle: MAPI over HTTP
ms:assetid: 4663b5db-5b30-4a5a-a302-be6fef7fe5da
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn635177(v=EXCHG.150)
ms:contentKeyID: 61203319
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# MAPI over HTTP

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-05-10_

HTTP를 통한 응용 프로그래밍 인터페이스 (MAPI) 메시징는 MicrosoftExchange Server 2013 서비스 팩 1 (SP1)에서 구현 하는 새 전송 프로토콜. HTTP 통한 MAPI 업계 표준의 HTTP 모델에 전송 계층을 이동 하 여 안정성과 Outlook 및 Exchange 연결의 안정성을 향상 시킵니다. 이렇게 하면 더 높은 수준의 전송 오류 및 향상 된 복구 기능에 대 한 가시성 있습니다. 추가 기능에는 명시적 일시 중지 및 다시 시작 함수에 대 한 지원을 포함 됩니다. 이렇게 하면 지원 되는 클라이언트가 네트워크를 변경 하거나 동일한 서버 컨텍스트를 유지 관리 하는 동안 최대 절전 모드에서 다시 시작할 수 있습니다.

HTTP를 통한 MAPI를 구현 Exchange 에 액세스 하려면 Outlook 에 대해 사용할 수 있는 유일한 프로토콜 임을 의미 하지 않습니다. 여전히 Outlook 클라이언트는 MAPI HTTP를 통한 Outlook Anywhere (RPC over HTTP)를 사용 하 여 MAPI 사용이 가능한 클라이언트 액세스 서버를 통해 Exchange에 액세스할 수 있습니다.

## MAPI over HTTP의 이점

HTTP 통한 MAPI를 지 원하는 클라이언트는 다음과 같은 이점을 제공 합니다.

  - HTTP 기반 프로토콜을 사용함으로써 향후 제공되는 혁신적 인증 기능을 사용할 수 있습니다.

  - 통신이 중단된 이후 RCP 연결이 아닌 TCP 연결만 다시 구축하면 되므로 보다 빠르게 다시 연결할 수 있습니다. 통신 중단의 예는 다음과 같습니다.
    
      - 장치 최대 절전 모드
    
      - 유선 네트워크에서 무선 또는 셀룰러 네트워크로 변경

  - 연결에 의존하지 않는 세션 컨텍스트가 제공됩니다. 즉, 사용자가 네트워크를 변경해도 서버는 구성 가능한 기간 동안 세션 컨텍스트를 유지합니다.

## MAPI over HTTP 배포

MAPI over HTTP를 사용하려는 경우 다음 요구 사항을 고려하세요.

  - **지원 가능성**   원하는 구성 버전이 지원되는지 확인합니다.

  - **필수 구성 요소**   환경이 업그레이드되었으며 MAPI over HTTP를 사용할 준비가 되었는지 확인합니다.

  - **구성**   가상 디렉터리를 구성하고 조직에 대해 MAPI를 사용하도록 설정합니다.

## 지원 가능성

다음 표를 참조하여 클라이언트와 서버가 MAPI over HTTP를 지원하는지 확인합니다.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>제품</th>
<th>Exchange 2013 SP1</th>
<th>Exchange 2013 RTM</th>
<th>Exchange 2010 SP3</th>
<th>Exchange 2007 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 SP1</p></td>
<td><ul>
<li><p>MAPI over HTTP</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2013 RTM</p></td>
<td><p>Outlook Anywhere</p></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2010 S p 2와 업데이트 KB2956191 및 KB2965295 (2015 년 4 월 14)</p></td>
<td><ul>
<li><p>HTTP 통한 MAPI<span></span></p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2010 S p 2와 이전 버전</p></td>
<td><p>Outlook Anywhere</p></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Outlook Anywhere</p></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 선행 조건

클라이언트와 서버가 MAPI over HTTP를 지원하도록 준비하려면 다음 단계를 수행합니다.

1.  Outlook 2013 SP1 또는 s p 2 Outlook 2010 및 업데이트 KB2956191 및 KB2965295 (2015 년 4 월 14,)로 Outlook 클라이언트를 업그레이드 합니다.

2.  클라이언트 액세스 서버와 사서함 서버를 Exchange 2013 SP1로 업그레이드합니다. 업그레이드 방법은 [최신 누적 업데이트 또는 서비스 팩으로 Exchange 2013 업그레이드](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)를 참조하세요.
    

    > [!NOTE]
    > MAPI over HTTP를 사용하도록 설정하기 전에 모든 클라이언트 액세스 서버를 Exchange 2013 SP1로 업그레이드해야 합니다. 그렇지 않으면 Outlook에서 사서함에 연결하지 못할 수 있습니다.<BR>DAG(데이터베이스 사용 가능 그룹)의 모든 사서함 서버를 업그레이드하지 않으면 전자 메일이 지연되고 데이터베이스 장애 조치(failover) 시에 클라이언트가 Outlook을 다시 시작해야 할 수 있습니다.



3.  모든 Exchange 2013 서버의 Microsoft.NET Framework 4.5.2를 설치 해야 합니다. 자세한 내용은 [.NET Framework를 설치](https://go.microsoft.com/fwlink/p/?linkid=518380)를 참조 하십시오.

4.  모든 Exchange 2013 SP1 클라이언트 액세스 서버에서 다음 단계를 수행하여 **COMPLUS\_DisableRetStructPinning** Windows 환경 변수를 추가합니다.
    
    1.  명령 프롬프트 창에서 `systempropertiesadvanced`를 실행하고 **환경 변수**를 클릭합니다.
    
    2.  **시스템 변수** 섹션에서 **새로 만들기**를 클릭하고 다음 정보를 입력합니다.
        
          - **변수 이름**   `COMPLUS_DisableRetStructPinning`
        
          - **변수 값**   1
    
    3.  작업을 마치면 **확인**을 클릭합니다.

## 구성

조직에 대해 MAPI over HTTP를 구성하려면 다음 단계를 수행합니다.

1.  **가상 디렉터리 구성**   기본적으로 Exchange 2013 SP1은 MAPI over HTTP용 가상 디렉터리를 만듭니다. **Set-MapiVirtualDirectory** cmdlet을 사용하여 가상 디렉터리를 구성합니다. 내부 URL이나 외부 URL 중 하나 또는 둘 다를 구성해야 합니다. 자세한 내용은 [Set-MapiVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dn595082\(v=exchg.150\))를 참조하세요.
    
    예를 들어 내부 URL 값을 https://contoso.com/mapi로 설정하고 인증 방법을 `Negotiate`로 설정하여 로컬 Exchange 서버에서 기본 MAPI 가상 디렉터리를 구성하려면 다음 명령을 실행합니다.
    
        Set-MapiVirtualDirectory -Identity "Contoso\mapi (Default Web Site)" -InternalUrl https://Contoso.com/mapi -IISAuthenticationMethods Negotiate

2.  **인증서 구성**   Exchange 환경에서 사용하는 디지털 인증서는 MAPI 가상 디렉터리에 구성된 것과 같은 *InternalURL* 및 *ExternalURL* 값을 포함해야 합니다. Exchange 2013 인증서 관리에 대한 자세한 내용은 [디지털 인증서 및 SSL](digital-certificates-and-ssl-exchange-2013-help.md)을 참조하세요. Exchange 인증서를 Outlook 클라이언트 워크스테이션에서 신뢰하는지 확인하고, 특히 MAPI 가상 디렉터리에 구성된 URL에 액세스하는 경우에는 인증서 오류가 없는지 확인합니다.

3.  **서버 규칙 업데이트**   부하 분산 장치, 역방향 프록시 및 방화벽이 MAPI over HTTP 가상 디렉터리 액세스를 허용하도록 구성되어 있는지 확인합니다.

4.  **Exchange 조직에서 MAPI over HTTP 사용**
    
    다음 명령을 실행합니다.
    
        Set-OrganizationConfig -MapiHttpEnabled $true

## MAPI over HTTP 연결 테스트

**Test-OutlookConnectivity** cmdlet을 사용하여 종단 간 MAPI over HTTP 연결을 테스트할 수 있습니다. **Test-OutlookConnectivity** cmdlet을 사용하려면 Microsoft Exchange Health Manager(MSExchangeHM) 서비스를 시작해야 합니다.

다음 예에서는 Exchange 서버 ContosoMail에서 MAPI over HTTP 연결을 테스트합니다.

    Test-OutlookConnectivity -RunFromServerId ContosoMail -ProbeIdentity OutlookMapiHttpSelfTestProbe

테스트가 정상적으로 완료되면 다음 예와 같은 출력이 반환됩니다.

    MonitorIdentity                                          StartTime              EndTime                Result      Error     Exception
    ---------------                                          ---------              -------                ------      -----     ---------
    OutlookMapiHttp.Protocol\OutlookMapiHttpSelfTestProbe    2/14/2014 7:15:00 AM   2/14/2014 7:15:10 AM   Succeeded

자세한 내용은 [Test-OutlookConnectivity](https://technet.microsoft.com/ko-kr/library/dd638082\(v=exchg.150\))를 참조하세요.

MAPI over HTTP 작업의 로그는 다음 위치에 있습니다.

  - %Exchange 설치 경로%Logging\\MAPI Address Book Service\\

  - %Exchange 설치 경로%Logging\\MAPI Client Access\\

  - %ExchangeInstallPath%Logging\\HttpProxy\\Mapi\\

## MAPI over HTTP 관리

다음 cmdlet을 사용하여 MAPI over HTTP의 구성을 관리할 수 있습니다.

  - [Set-MapiVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dn595082\(v=exchg.150\))

  - [Get-MapiVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dn595080\(v=exchg.150\))

  - [New-MapiVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dn595081\(v=exchg.150\))

  - [Remove-MapiVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dn595083\(v=exchg.150\))

