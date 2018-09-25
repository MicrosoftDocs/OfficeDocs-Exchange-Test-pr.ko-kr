---
title: 'Exchange UM 문제해결 도구에 대 한 설명: Exchange 2013 Help'
TOCTitle: Exchange UM 문제해결 도구에 대 한 설명
ms:assetid: cc11bf5e-2c87-4495-b2ad-3e9a6bc81dbc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg584301(v=EXCHG.150)
ms:contentKeyID: 56270333
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange UM 문제해결 도구에 대 한 설명

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange 2010 통합 메시징 문제해결 도구는 **Test-ExchangeUMCallFlow**라는 Exchange 관리 셸 cmdlet은입니다. 이 도구를 사용 하 여 조직에서 일련의 진단 테스트에 대 한 UM (통합 메시징)을 수행할 수 있습니다. 테스트 중 하나라도 실패 문제를 해결 하려면 오류 및 가능한 솔루션에 대 한 이유를 보고 하는 도구입니다. 만 Exchange 2010 또는 이후 서버에서 UM 문제해결 도구를 사용할 수 있습니다.

UM 문제 해결 도구를 사용하여 온-프레미스 배포와 크로스-프레미스 배포 둘 다에서 음성 메일이 올바르게 작동하는지 여부를 테스트할 수 있습니다. Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server 2010 이상이 포함된 UM 배포 또는 VoIP 게이트웨이, IP PBX(IP Private Branch eXchange) 또는 SBC(Session Border Controller)가 포함된 UM 배포에서 이 도구를 사용할 수 있습니다.


> [!NOTE]
> UM 문제 해결 도구는 테스트 및 문제 해결에 사용됩니다. 반면 <STRONG>Test-UMConnectivity</STRONG> cmdlet은 모니터링에 사용해야 합니다. <STRONG>Test-UMConnectivity</STRONG> cmdlet은 Exchange 2010 UM 서버 또는 Exchange 2013 클라이언트 액세스, 사서함 서버 및 전화 통신 구성 요소를 모니터링하는 데 사용되는 SCOM(System Center Operations Manager) 관리 팩과 함께 사용됩니다. <STRONG>Test-UMConnectivity</STRONG> cmdlet은 사서함에 대해 로컬 SIP 테스트 및 로컬 로그온 테스트를 수행하며 SCOM 작업으로 실행될 수 있습니다.



UM 문제해결 도구를 다운로드 하려면 [통합 메시징 문제해결 도구](https://go.microsoft.com/fwlink/p/?linkid=182625)를 참조 하십시오.

**목차**

개요

UM troubleshooting architecture

VoIP gateway and IP PBX deployments

Office Communications Server R2 and Microsoft Lync Server deployments

Installing the UM Troubleshooting Tool

Cmdlet parameters

## 개요

UM 문제 해결 도구는 UM 배포의 테스트 및 문제 해결을 간소화합니다. UM 문제 해결 도구를 실행하면 일련의 추적 파일이 자동으로 생성되어 C:\\Users\\%UserProfile%\\AppData\\Roaming\\Microsoft Exchange 2010 UM Troubleshooting 폴더에 저장됩니다. 도구에서 생성하는 추적 파일은 다음과 같습니다.

  - **UMTool\_Collaboration**   RTC 스택 추적을 포함합니다.

  - **UMTool\_DiagnosticLog**   실행된 모든 테스트와 해당 결과를 표시합니다.

  - **UMTool\_S4**   S4: 신호 스택 추적을 포함합니다.

  - **UMTool\_SIPMessageLogs**   수행된 테스트 전화에 대한 전체 SIP 추적을 포함합니다.

UM 문제 해결 도구는 해당하는 경우 온-프레미스 SBC(Session Border Controller)에 직접 연결하거나 데이터 센터의 SBC에 연결하고, VoIP 게이트웨이 또는 IP PBX를 통해 PBX에서 전화가 걸려온 것처럼 수신 전화를 에뮬레이트합니다. UM 문제 해결 도구를 사용하여 다음을 진단할 수 있습니다.

  - Office Communications Server 2007 R2 또는 Microsoft Lync Server가 배포되어 있는 온-프레미스/크로스-프레미스 UM 배포에 잘못된 설정

  - VoIP 게이트웨이와 PBX 또는 IP PBX가 포함된 온-프레미스/크로스-프레미스 전화 통신 장비에 잘못된 설정

  - DNS(Domain Name System) 관련 문제

  - SIP 보안 또는 보안 UM 다이얼 플랜을 사용하는 경우 인증서 문제

  - DTMF(터치톤이라고도 함) 및 오디오에 대한 신호 및 미디어 문제

UM 문제 해결 도구가 구성 오류를 검색하면 오류가 발생한 이유와 검색된 문제의 가능한 해결 방법을 보고합니다. 온-프레미스 배포에서 UM 문제 해결 도구를 사용할 때 보고될 수 있는 오류는 다음과 같습니다.

  - 최대 호출 제한에 도달했습니다.

  - 사용자가 통합 메시징을 사용할 수 있도록 설정되어 있지 않습니다.

  - UM IP 게이트웨이, 다이얼 플랜 또는 헌트 그룹 정보를 찾을 수 없습니다.

  - 보안 유형이 UM 다이얼 플랜과 일치하지 않습니다.

  - 호출을 처리하기 위해 사용할 수 있는 작업자 프로세스가 없습니다.

  - UM 서비스 또는 UM 통화 라우터 서비스가 중지됩니다.

  - Active Directory 포리스트를 찾을 수 없습니다.

  - 사용할 수 있는 디스크 공간이 없습니다.

  - 요청에 사용된 SIP 헤더가 잘못되었습니다.

  - Office Communications Server 2007 R2 서버 또는 Lync Server 서버가 호출되었습니다.

  - UM IP 게이트웨이를 사용할 수 없음.

  - 호출되는 사용자의 URI가 잘못되었습니다.

크로스-프레미스 배포에서 UM 문제 해결 도구를 사용할 때 보고될 수 있는 오류는 다음과 같습니다.

  - 사용자가 통합 메시징을 사용할 수 있도록 설정되어 있지 않습니다.

  - UM IP 게이트웨이를 사용할 수 없음.

  - 사용자의 URI가 잘못되었습니다.

  - 보안 유형이 UM 다이얼 플랜과 일치하지 않습니다.

  - 요청에 사용된 SIP 헤더가 잘못되었습니다.

  - UM IP 게이트웨이, 다이얼 플랜 또는 헌트 그룹 정보를 찾을 수 없습니다.

UM 문제 해결 도구는 15초 동안 샘플 wav 파일을 보냅니다. 오디오 파일 및 RTP 오디오 스트림이 전송 및 재생되면 이 도구에서 일반 오디오 품질 메트릭을 보고하여 지터나 평균 패킷 손실 같이 네트워크 연결과 관련된 오디오 품질 문제를 진단합니다. 이러한 보고서에는 다음을 비롯하여 UM 서버에서 받고 보내는 미디어 스트림 품질이 포함됩니다.

  - NMOS(Network Mean Opinion Score)

  - 코덱

  - 대기 시간(ms)

  - 지터(ms)

  - 패킷 손실률(%)

  - 오디오 품질을 확인하는 데 사용할 NMOS 분류 및 등급:
    
      - NMOS가 2보다 작음 = 나쁨
    
      - NMOS가 2보다 크고 3보다 작음 = 평균
    
      - NMOS가 3보다 크고 4보다 작음 = 좋음
    
      - NMOS가 4보다 크고 5보다 작음 = 우수

UM 문제 해결 도구는 보안, SIP 보안 및 보안되지 않는 호출을 사용하는 UM 다이얼 플랜의 테스트를 지원합니다. 보안 또는 SIP 보안을 선택하면 사용된 인증서의 지문을 검사하여 인증서가 만료되었는지 여부 및 TLS(전송 계층 보안) 통신에 사용되는 인증서 유형이 확인됩니다. 인증서는 원격 컴퓨터의 ID를 올바르게 식별하고 확인하는 데 사용됩니다. 보안 또는 SIP 보안 모드가 선택된 경우 UM 문제 해결 도구는 다음이 true인지 여부를 확인합니다.

  - 로컬 컴퓨터 저장소에 로컬 인증서가 있습니다.

  - 사용 중인 인증서를 신뢰할 수 있습니다.

  - 인증서에 지정된 대상 이름이 유효합니다.

  - 인증서가 만료되었습니다.

  - 원격 컴퓨터가 인증서를 신뢰합니다.

  - 인증서가 해지되었습니다.

  - 인증서에 필요한 확장된 키 사용이 없습니다.

Office Communications Server 2007 R2 또는 Lync Server가 배포되어 있는지, VoIP 게이트웨이와 PBX 또는 IP PBX가 통합 메시징 서버와 함께 사용되는지 여부에 따라 게이트웨이나 SIPClient 모드에서 UM 문제 해결 도구를 실행할 수 있습니다. 게이트웨이 또는 SIPClient 모드를 사용하는 경우 UM 문제 해결 도구는 다음 형식의 호출을 지원합니다. 사용되는 형식은 UM 다이얼 플랜의 URI 유형에 따라 달라집니다.

  - 전화 내선 번호   425-555-1010

  - E.164 전화 번호   +1 (425) 555-1010

  - SIP 주소   tonysmith@contoso.com

SIPClient 모드를 사용하는 경우 UM 문제 해결 도구에서 음성 메모 호출을 수행합니다. 이 호출은 전화나 UC(통합 통신) 끝점을 울리지 않는 호출입니다. 대신 호출을 음성 메일로 직접 보냅니다. UM 문제 해결 도구는 SIPClient 모드로 실행되는 경우 다음을 확인합니다.

  - 호출되는 대상 사용자

  - SIP 호출이 설정되었는지 여부

  - Exchange 2010 통합 메시징 서버 또는 Exchange 2013 사서함 서버에서 호출을 수락했는지 여부

  - 올바른 DTMF 시퀀스가 수신되었는지 여부

  - Exchange 2010 UM 서버 또는 Exchange 2013 사서함 서버에서 .diagnostic .wav 파일을 주고받았는지 여부

  - 미디어 또는 오디오 품질 스트림을 받을 때 사용된 메트릭

UM 문제 해결 도구는 수신 전화를 에뮬레이트하고 온-프레미스 관리자와 테넌트 관리자가 전화 응답에 대한 통화 흐름을 테스트하고 구성 오류를 식별할 수 있도록 일련의 진단 테스트를 실행합니다. 전화 응답 시나리오에서 UM 문제 해결 도구를 사용할 수 있지만 다음과 같은 호출 유형의 테스트에는 사용할 수 없습니다.

  - 음성 사서함, 전자 메일, 일정, 디렉터리, 개인 연락처 또는 개인 옵션에 액세스하는 호출을 비롯한 Outlook Voice Access 호출

  - UM 자동 전화 교환

  - 전화에서 재생

  - 전화 응답 규칙

  - 팩스

  - 프롬프트 프로비전

맨 위로 이동

## UM 문제 해결 아키텍처

UM 문제 해결 도구는 크로스-프레미스 배포의 구성 문제를 해결하고 진단 및 복구하는 데 유용하며, 온-프레미스 통합 메시징 배포에서도 사용할 수 있습니다. 크로스-프레미스 배포에서는 현장 SBC 구성의 유효성도 검사됩니다. 관리자는 SBC를 비롯하여 통합 메시징에 사용되는 통합 메시징 구성 요소를 모두 테스트할 수 있습니다.

## VoIP 게이트웨이 및 IP PBX 배포

다음 예에서는 게이트웨이 모드를 사용하여 Office Communications Server 2007 R2 또는 Lync Server가 포함되지 않은 환경의 통화 흐름을 테스트합니다. 이 예에서는 VoIP 게이트웨이, PBX 및 IP PBX, 통합 메시징 구성 요소 등의 전화 통신 장비를 테스트합니다. 또한 VoIP(Voice over IP) 보안 모드를 보안되지 않음으로 설정하고, IP 주소 10.1.1.1을 다음 홉으로 사용하며, 전환 정보에 내선 번호를 포함합니다.

```powershell
Test-ExchangeUMCallFlow -Mode Gateway -VoIPSecurity Unsecured -NextHop 10.1.1.1 -Diversion 12345
```

맨 위로 이동

## Office Communications Server 2007 R2 및 Microsoft Lync Server 배포

SIPClient 모드가 설정된 경우 Office Communications Server 2007 R2 또는 Microsoft Lync Server가 포함된 온-프레미스 또는 크로스-프레미스 배포에서 UM 문제 해결 도구를 사용할 수 있습니다. 다음 예에서는 SIPClient 모드를 사용하며, Office Communications Server 2007 R2 또는 Lync Server 서버가 포함된 환경에서 보안 UM 다이얼 플랜으로 호출 흐름을 테스트합니다. 기본적으로 UM 문제 해결 도구를 실행할 때 이 도구는 컴퓨터에 현재 로그온한 사용자의 자격 증명을 사용합니다. 다음 예를 실행하는 경우 UM 문제 해결 도구를 실행할 때 사용할 자격 증명을 묻는 메시지가 표시됩니다. 자세한 내용은 [Exchange UM 문제해결 도구를 사용 하 여 자격 증명 설정](set-the-credentials-to-use-with-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)를 참조하십시오.

```powershell
Test-ExchangeUMCallFlow -Mode SIPClient -VoIPSecurity Secured -CallingParty tony@contoso.com -CalledParty david@contoso.com -Credential $get
```
## UM 문제 해결 도구 설치

UM 문제 해결 도구는 로컬 통합 메시징 서버나 다음 중 하나를 실행하는 다른 64비트 컴퓨터에 설치할 수 있습니다.

  - Windows 7 또는 Windows 8 운영 체제

  - Windows Server 2008 또는 Windows Server 2008 R2 운영 체제

  - Windows Server 2012 또는 Windows Server 2012 R2 운영 체제

64비트 버전의 Windows 7, Windows 8 또는 64비트 버전의 Windows Server 2008에서 UM 문제 해결 도구를 사용하는 경우 UM 문제 해결 도구를 설치하기 전에 먼저 다음 구성 요소를 설치해야 합니다.

  - Microsoft .NET Framework 3.5 서비스 팩 1 (SP1) [Microsoft.NET Framework 3.5 서비스 팩 1](https://go.microsoft.com/fwlink/p/?linkid=152380)를 참조 하십시오.
    

    > [!NOTE]
    > Windows Vista 또는 Windows Server 2008 컴퓨터에서 도구를 실행 하는 경우 <A href="https://go.microsoft.com/fwlink/p/?linkid=178998">Windows Server 2008 x64 및 Windows Vista x64, 용 Microsoft.NET Framework 3.5 제품군 업데이트</A>를 참조 하십시오.



  - WinRM(Windows 원격 관리) 2.0 및 Windows PowerShell V2(Windows6.0-KB968930.msu)   Microsoft 기술 자료 문서 968930, [Windows 관리 프레임워크 핵심 패키지(Windows PowerShell 2.0 및 WinRM 2.0)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=968930)를 참조하세요.

  - Microsoft Unified Communications Managed API 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi) [Unified Communications Managed API 2.0, Core Runtime (64 비트)](https://go.microsoft.com/fwlink/p/?linkid=198175)를 참조 하십시오.

UM 문제해결 도구 (**Test-ExchangeUMCallFlow** cmdlet) Exchange 2010 SP1 DVD만 Exchange 2010 또는 Exchange 2013 설치 미디어를 포함 하는 다운로드 포함 되지 않습니다. 그러나 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?linkid=182625)에서 UM 문제해결 도구를 다운로드할 수 있습니다.

자세한 내용은 [Exchange UM 문제 해결 도구 설치](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## Cmdlet 매개 변수

다음 표에는 **Test-ExchangeUMCallFlow** cmdlet과 함께 사용할 수 있는 매개 변수 및 이러한 매개 변수에 대한 설명이 나와 있습니다. 셸 명령 `Get-help Test-ExchangeUMCallFlow -detailed`를 사용하여 **Test-ExchangeUMCallFlow** cmdlet과 함께 사용할 수 있는 각 매개 변수에 대한 자세한 설명 및 사용 예를 확인할 수도 있습니다.

### 매개 변수

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>CalledParty</em></p></td>
<td><p><em>CalledParty</em> 매개 변수는 Enterprise Voice를 사용하도록 설정된 Office Communications Server 2007 R2 또는 Lync Server 사용자의 SIP URI를 지정합니다. 이 사용자는 <strong>Test-ExchangeUMCallFlow</strong> cmdlet이 음성 통화를 수행할 사용자입니다. <code>-CalledParty tonysmith@contoso.com</code>을 예로 들 수 있습니다. SIPClient 모드에서 도구를 실행하는 경우 이 매개 변수를 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>CallingParty</em></p></td>
<td><p><em>CallingParty</em> 매개 변수는 Enterprise Voice를 사용하도록 설정된 Office Communications Server 2007 R2 또는 Lync Server 사용자의 SIP URI를 지정합니다. 이 사용자는 수신 전화를 수행하는 사용자입니다. <code>-CallingParty tonysmith@contoso.com</code>을 예로 들 수 있습니다. SIPClient 모드에서 도구를 실행하는 경우 이 매개 변수를 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>Diversion</em></p></td>
<td><p><em>Diversion</em> 매개 변수는 들어오는 호출에 대한 전환 정보로 전송되어야 할 문자열을 지정합니다. 이것은 전환 또는 기록 정보 헤더 형태가 될 수 있습니다. 수신 전화에 포함된 전환 정보는 내선 번호일 수도 있고 추가 전환 정보를 포함할 수도 있습니다.</p>
<p>기록 정보 헤더로 전환 정보를 제공하는 경우 다음을 확인하십시오.</p>
<ul>
<li><p>다른 사용자 부분이 포함된 두 개 이상의 다른 항목이 있습니다.</p></li>
<li><p>마지막 항목에는 사용자의 연결된 UM 다이얼 플랜에 해당하는 파일럿 번호가 포함되어 있습니다.</p></li>
<li><p>마지막 항목에서 두 번째 항목에는 UM 사용이 가능한 사용자의 내선 번호가 포함됩니다. 또한 이 항목은 적절한 이유 텍스트를 포함해야 합니다. 이 텍스트는 표준 URL 매개 변수 이스케이프 규칙에 따라 적절하게 이스케이프되어야 합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p><em>Mode</em> 매개 변수는 VoIP 게이트웨이, IP PBX 또는 Office Communications Server 2007 R2 또는 Lync Server 모드 중에서 사용할 모드를 지정합니다. UM 배포에 VoIP 게이트웨이나 IP PBX가 포함된 경우에는 게이트웨이 모드를, UM 배포에 Office Communications Server 2007 R2 또는 Lync Server가 포함된 경우에는 SIPClient 모드를 지정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>NextHop</em></p></td>
<td><p><em>NextHop</em> 매개 변수는 다음 홉의 IP 주소 또는 FQDN(정규화된 도메인 이름)을 지정하며, <strong>Test-ExchangeUMCallFlow</strong> cmdlet이 VoIP 게이트웨이 또는 IP PBX를 에뮬레이트하는 동안 연결해야 하는 다음 홉의 TCP 포트도 포함할 수 있습니다. TCP 포트를 포함할 때 보안되지 않음 모드의 경우 포트 5060, 보안 또는 SIP 보안 모드의 경우 포트 5061을 지정해야 합니다. 예를 들면 다음과 같습니다. <code>gateway.contoso.com:5061</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>CertificateThumbprint</em></p></td>
<td><p><em>CertificateThumbprint</em> 매개 변수는 TLS에 사용되는 인증서의 지문을 지정합니다. 이 매개 변수는 UM 다이얼 플랜에서 SIP 보안 또는 보안 모드가 구성되어 있는 경우에 필요합니다. 이 인증서 지문은 VoIP 게이트웨이, IP PBX 또는 SBC에서 내보낸 인증서입니다. 또한 UM 문제 해결 도구가 설치되어 있고 통화 흐름을 테스트하는 데 사용되는 컴퓨터가 다음 홉의 인증서를 신뢰해야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>Credential</em></p></td>
<td><p><em>Credential</em> 매개 변수는 cmdlet을 실행하는 데 사용되는 자격 증명을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>HuntGroup</em></p></td>
<td><p><em>HuntGroup</em> 매개 변수는 에뮬레이트되는 VoIP 게이트웨이와 연결된 UM 헌트 그룹을 지정합니다. 일반적으로 이것은 내선 번호입니다. 게이트웨이 모드에서 도구를 실행하는 경우 이 매개 변수를 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoIPSecurity</em></p></td>
<td><p><em>VoIPSecurity</em> 매개 변수는 게이트웨이 모드에서 cmdlet을 사용할 때 보안 모드를 지정합니다. 다음과 같은 VoIP 보안 모드 중 하나를 사용할 수 있습니다.</p>
<ul>
<li><p>보안(TLS/SRTP)</p></li>
<li><p>보안되지 않음(TCP/RTP)(기본값)</p></li>
<li><p>SIP 보안(TLS/RTP)</p></li>
</ul></td>
</tr>
</tbody>
</table>


맨 위로 이동

