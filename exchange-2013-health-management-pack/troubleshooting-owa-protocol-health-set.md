---
title: OWA 문제를 해결 합니다. 프로토콜 상태 설정
TOCTitle: OWA 문제를 해결 합니다. 프로토콜 상태 설정
ms:assetid: fe172da8-65d3-43e0-ba62-d36a1b05fc11
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.owa.protocol(v=EXCHG.150)
ms:contentKeyID: 53275598
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# OWA 문제를 해결 합니다. 프로토콜 상태 설정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

OWA 합니다. 사서함 서버에서 Outlook Web App 프로토콜을 모니터링 하는 프로토콜 상태 설정 합니다.

알림이 표시 되도록 지정 하는 경우 OWA 합니다. 프로토콜은 정상 임을 사용자가 Outlook Web App 를 사용 하 여 자신의 사서함에 액세스 하지 못하게 할 수 있는 문제가 없습니다.

## 설명

OWA 서비스는 다음 프로브 및 모니터를 사용 하 여 모니터링 됩니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>프로브</th>
<th>상태 설정</th>
<th>종속성</th>
<th>연결된 모니터</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OwaSelfTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>None</p></td>
<td><p>OwaSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OwaDeepTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Active Directory</p>
<p>정보 저장소</p></td>
<td><p>OwaDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


**OwaSelfTestProbe** 프로브 다음 주소에 단일 HTTP 요청을 보냅니다: https://localhost:444/owa/exhealth.check 합니다. 응용 프로그램 풀을 반환 하 여 응답 하는지 확인 하는 프로브를 **200 확인** 상태 코드입니다. 이 프로브 Exchange 구성 요소에 없는 종속성을 갖습니다.

**OwaDeepTestProbe** 프로브 현재 서버의 복사본을 사용 하 여 각 사서함 데이터베이스에 대해 실행 됩니다. 프로브 해당 서버에 대해 전자 메일을 설정할 수 있는지를 결정 합니다. 이 작업을 수행 하는 특정 서버에 대해 클라이언트 액세스 서버 (CA)에 의해 생성 되는 트래픽 유형을 시뮬레이션 합니다. 프로브는 Active Directory 인증의 경우 도메인 서비스 (AD DS) 및 사서함 액세스에 대 한 사서함 저장소에 따라 다릅니다. 프로브 및 모니터 하는 방법에 대 한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조 하십시오.

## 일반적인 문제

다음과 같은 일반적인 이유로 인해 이 프로브에 오류가 발생할 수 있습니다.

  - 모니터링 되는 CA에서 호스트 되는 OWA 응용 프로그램 풀이 응답 하지 않습니다, 또는 사서함 서버에서 호스팅하는 응용 프로그램 풀이 응답 하지 않습니다.

  - 네트워킹 문제를 발생 하는 CA 또는 사서함 서버는 하 고 다른 서버 또는 도메인 컨트롤러에 연결할 수 없습니다.

  - 모니터링 계정 자격 증명이 잘못되었습니다.

  - 사용자의 데이터베이스가 탑재 되지 되었거나 정보 저장소 해당 사서함에 액세스할 수 없습니다.

  - 정보 저장소 응답 하지 않습니다.

  - 도메인 컨트롤러가 응답하지 않습니다.

## 사용자 작업

서비스가 경고를 보낸 후 복구되었을 수도 있습니다. 따라서 상태 설정이 비정상임을 지정하는 경고가 표시되면 해당 문제가 여전히 존재하는지를 먼저 확인하십시오. 문제가 있는 경우 다음 섹션에 설명된 적절한 복구 작업을 수행합니다.

## 문제가 여전히 존재하는지 확인

1.  경고의 서버 이름 및 상태 설정 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우에는 메시지 세부 정보에서 근본 원인을 파악하는 데 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보낸 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        예: OWA를 검색할 수 있습니다. 프로토콜 상태 server1. contoso.com, 다음 명령을 실행 하는 방법에 대 한 세부 정보를 설정 합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Protocol"}
    
    2.  명령 출력의 오류를 보고 하는 모니터를 결정을 검토 합니다. 경고를 모니터에 대 한 **AlertValue**`Unhealthy`됩니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        예, 오류가 발생 한 모니터 **OwaSelfTestMonitor** 했음을 것으로 가정 합니다. 모니터에 연결 된 프로브 **OwaSelfTestProbe** 됩니다. Server1. contoso.com에 해당 프로브를 실행 하려면 다음 명령을 실행 합니다.
        
            Invoke-MonitoringProbe OWA.Protocol\OwaSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  명령 출력에서 프로브의 **Result** 값을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

상태 설정에서 경고가 표시될 때는 다음 정보가 포함된 전자 메일 메시지를 받게 됩니다.

  - 경고를 보낸 서버의 이름

  - (자가 테스트 또는 DeepTest)에 실패 한 프로브 유형

  - 경고가 발생한 날짜와 시간

  - 프로브에 대 한 전체 HTTP 요청 추적을 찾을 수 있는 폴더에 대 한 경로
    
      
    기본적으로 추적 파일은 다음 폴더에 있습니다.
    
      - SelfTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\ProtocolProbe
    
      - DeepTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\MailboxProbe

  - 마지막 오류의 전체 예외 추적(진단 데이터 및 특정 HTTP 헤더 정보 포함)  
    
    **참고 사항**   이 문제를 해결 하기 위해 전체 예외 추적에 정보를 사용할 수 있습니다. 프로브에서 생성 된 예외는 프로브 실패 이유를 설명 하는 실패 이유를 포함 합니다. 실패 이유는 다음 중 하나가 될 수 있습니다.
    
      - **MissingKeyword**   서버 응답에서 예상 되는 키워드를 찾지 못했습니다. 이 경우 예외가 예상 되는 키워드를 포함합니다.
    
      - **NameResolution**   지정 된 서버 이름을 확인 하기 위해 DNS 확인 실패 합니다.
    
      - **NetworkConnection**   프로브 카페에서 OWA 응용 프로그램 풀에 연결 하려고 하면 네트워크 연결 오류를 수신 합니다.
    
      - **UnexpectedHttpResponseCode**   응답에 예기치 않은 HTTP 코드를 포함 합니다. 등 서버는 HTTP **503** 코드를 반환 합니다.
    
      - **RequestTimeout**   서버 시간 초과로 클라이언트 요청에 응답 합니다.
    
      - **UnexpectedHttpResponseCode**   에 대 한 응답 예기치 않은 HTTP 코드를 반환 했습니다. 등 서버는 HTTP **503** 코드를 반환 합니다.
    
      - **ScenarioTimeout**   프로브는 성공적으로 마쳤으나 그렇게 1 분 이상 소요 합니다. 이것은 보통 오버 로드 되는 시스템을 나타냅니다.
    
      - **OwaErrorPage**   OWA 오류 페이지를 반환 합니다. 오류를 발생 시킨 오류의 이름은 예외 메시지에서 일반적으로 사용할 수 있습니다.
    
      - **OwaMailboxErrorPage**   OWA는 사서함 저장소와 관련 된 오류를 포함 하는 오류 페이지를 반환 합니다. 이 일반적으로 이러한 문제를 다운 되 고 사서함 저장소 또는 분리 되는 사서함으로 나타냅니다.
    
    예외 추적 필드가 들어 있는 중요 한 라는 **FailingComponent**, 프로브를 확인 하 고 오류를 범주별로 분류 하려고 하는 수단을 만듭니다. 예는 프로브는 다음 값 중 하나를 반환할 수 있습니다.
    
      - **사서함**   프로브 OWA에 도달할 수 있지만 사서함 저장소에 연결할 수 없습니다. 이 경우에 프로브 실패 했거나 실패 하 고 **ScenarioTimeout** 오류를 생성 하는 프로브를 발생 시킨 사서함 액세스 대기 시간입니다. 이러한 유형의 오류가 발생 했을 때 사서함 서버의 상태를 확인 해야 합니다.
    
      - **Active Directory**   프로브 OWA에 도달할 수 있지만 AD DS에 연결할 수 없습니다. 이 경우에 프로브 실패 또는 AD DS 통화 대기 시간이 초과 프로브 않을 수 있습니다. 이러한 종류의 오류가 발생 했을 때에 도메인 컨트롤러의 상태를 확인 하 고도 CA 및 사서함 서버와 도메인 컨트롤러 간의 네트워크 연결을 확인 해야 합니다.
    
      - **OWA**   이 일반적으로 OWA 레이어 내부 오류가 발생 했음을 의미 합니다. 이러한 종류의 오류가 발생 했을 때 CA 및 사서함 서버에서 OWA 프로세스의 상태를 확인 하 고도 네트워크 연결을 확인 해야 합니다.
    
    예외에는 가장 최근의 HTTP 요청을 받고 응답 정보를 프로브 실패 하기 전에 받은 들어 있습니다.  
      
    에스컬레이션 본문 전체 HTTP 웹 요청 및 프로브 실패 했을 때 전송 된 응답을 확인 하기 위해 사용할 수 있는 프로브 로그에 대 한 경로 포함 합니다. 이 파일만 로그온 시도 실패 기록 하기 때문에 실패 한 프로브에 대해서만 데이터를 포함 합니다. 이 정보를 가져올 테스트에 실패 한 이유의 완벽 하 게 보기를 사용할 수 있습니다.

## OwaSelfTestProbe 복구 작업

이 프로브에 거의 종속성, 있기 때문에 실패 OWA 응용 프로그램 풀 프로세스 응답 하지 않을 경우 일반적으로 발생 합니다.

이 문제를 해결하려면 다음 단계를 수행합니다.

1.  새 오류는 발생 하 고 있음을 확인 하려면 경고 전자 메일 메시지 본문에 프로브 추적 로그 URL을 클릭 합니다.

2.  사서함 탑재 되는 동일한 서버에 테스트 사용자 계정을 만듭니다. 이 문제를 재현할 수 있는지 여부를 확인 하려면 로그온을 시도 합니다.

3.  특정 사서함 서버에 영향을 주는 문제를 나타낼 수 있는 OWA 상태 집합에 대 한 경고를 확인 합니다. 자세한 내용은 [OWA 상태 설정 문제해결](troubleshooting-owa-health-set.md)을 참조 하십시오.

4.  IIS 관리자를 시작 하 고 **MSExchangeOwaAppPool** 응용 프로그램 풀이 CA에서 실행 되 고 있는지 여부를 확인 하려면 문제를 보고 하는 서버에 연결 합니다.

5.  IIS 관리자에서 기본 웹사이트 실행 되 고 있는지 확인 합니다.

6.  IIS 관리자에서 **응용 프로그램 풀** 을 클릭 한 후 Exchange 관리 셸 에서 다음 명령을 실행 하 여 **MSExchangeOWAAppPool** 응용 프로그램 풀을 재순환 합니다.
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

7.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

8.  문제가 여전히 존재하는 경우 IISReset 유틸리티를 사용하거나 다음 명령을 실행하여 IIS 서비스를 재순환합니다.
    
        Iisreset /noforce

9.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

10. 그래도 문제가 계속 발생하면 서버를 다시 시작하십시오.

11. 서버가 다시 시작되면 Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

12. 그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## OwaDeepTestProbe 복구 작업

1.  문제가 여전히 존재 하는지 여부를 확인 하려면 탑재 되는 사서함에는 동일한 서버에 테스트 사용자 계정 및 OWA에 로그온 하려고 하면를 만듭니다. 예를 사용 하 여 로그온 하려고: https:// *\<servername\>*/owa 합니다.

2.  특정 사서함 서버에 영향을 주는 문제를 나타낼 수 있는 OWA 상태 집합에 대 한 경고를 확인 합니다. 자세한 내용은 [OWA 상태 설정 문제해결](troubleshooting-owa-health-set.md)을 참조 하십시오.

3.  IIS 관리자를 시작 하 고 **MSExchangeOwaAppPool** 응용 프로그램 풀이 CA에서 실행 되 고 있는지 여부를 확인 하려면 문제를 보고 하는 서버에 연결 합니다.

4.  IIS 관리자에서 기본 웹사이트 실행 되 고 있는지 확인 합니다.

5.  실패 한 프로브에 대 한 사서함 데이터베이스를 찾아 사서함 데이터베이스 사서함 서버에서 활성 상태 이며 사서함 저장소의 상태가 정상 인지 확인 합니다. 실패 한 데이터베이스 GUID 정보를 찾으려면 전체 예외 추적 정보를 엽니다. 각 오류는 다음과 같이 표시 하는 항목을 포함 해야 합니다.
    
    `Starting Owa probe with Target: https://localhost/owa/, Username:  HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com`

6.  HealthMailbox GUID를 복사 하 고 셸에서 다음 명령을 실행 합니다.
    
        Get-Mailbox -Monitoring -Identity <username>
    
    예, 다음 명령을 실행 합니다.
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    반환 된 개체는 사용자의 데이터베이스 이름을 찾아 현재 활성 상태인 데이터베이스가 있는 확인할 수 있습니다.

7.  IIS 관리자에서 **응용 프로그램 풀** 을 클릭 한 후 셸에서 다음 명령을 실행 하 여 **MSExchangeOWAAppPool** 응용 프로그램 풀을 재순환 합니다.
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

8.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

9.  문제가 여전히 존재하는 경우 IISReset 유틸리티를 사용하거나 다음 명령을 실행하여 IIS 서비스를 재순환합니다.
    
        Iisreset /noforce

10. Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

11. 그래도 문제가 계속 발생하면 서버를 다시 시작하십시오.

12. 서버가 다시 시작되면 Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

13. 그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## 자세한 내용

[Exchange 2013의 새로운 기능](https://technet.microsoft.com/ko-kr/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\))

