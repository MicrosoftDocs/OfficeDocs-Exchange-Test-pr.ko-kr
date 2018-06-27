---
title: 'Edge 전송 서버 복제 된 구성: Exchange 2013 Help'
TOCTitle: Edge 전송 서버 복제 된 구성
ms:assetid: 683a6b8a-59bf-43ed-96c8-504945c2f665
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998622(v=EXCHG.150)
ms:contentKeyID: 61183423
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 전송 서버 복제 된 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

Edge 전송 서버의 구성 정보는 AD LDS(Active Directory Lightweight Directory Services)에 저장됩니다. 경계 네트워크에 Edge 전송 서버를 두 대 이상 설치하고 DNS 라운드 로빈을 사용하여 Edge 전송 서버 간의 네트워크 트래픽을 균형 있게 조정할 수 있습니다. 라운드 로빈은 네트워크 리소스에 대한 로드를 공유 및 배포하기 위해 DNS 서버에서 사용하는 간단한 메커니즘입니다.

모든 Edge 전송 서버가 같은 구성 정보를 사용하도록 하려면 제공되는 복제된 구성 스크립트를 사용하여 원본 서버의 구성을 대상 서버에 복제합니다.

*복제된 구성*은 구성된 원본 서버를 기반으로 새 Edge 전송 서버를 배포하는 데 사용됩니다. 이 경우 원본 서버 구성 정보를 복제하여 XML 파일로 내보냅니다. 그리고 대상 서버에서 해당 XML 파일을 가져옵니다.

이 항목에서는 복제된 구성 프로세스에 대해 간략하게 설명합니다. 복제된 구성을 사용하여 Edge 전송 서버를 구성하는 자세한 단계는 [복제 된 구성을 사용 하 여 Edge 전송 서버 구성](configure-edge-transport-server-using-cloned-configuration-exchange-2013-help.md)을 참조하십시오.

**목차**

Cloned configuration and EdgeSync

Cloned configuration process

Transport configuration information

## 복제된 구성 및 EdgeSync

복제된 구성을 가져온 후에는 EdgeSync 프로세스를 실행합니다. 받는 사람 조회 및 메시지 보안 작업을 수행하려면 Edge 전송 서버에는 Active Directory에 있는 데이터가 필요합니다. *EdgeSync*는 Active Directory에서 Edge 전송 서버의 AD LDS 인스턴스로 받는 사람 및 구성 정보를 복제하는 단방향 복제를 설정하기 위해 Exchange 2013 사서함 서버에서 실행되는 프로세스의 모음입니다. EdgeSync는 Edge 전송 서버에서 스팸 방지 작업을 수행하는 데 필요한 정보와 종단 간 메일 흐름을 사용하는 데 필요한 커넥터 구성 관련 정보만 복사합니다. EdgeSync는 AD LDS의 정보를 최신 상태로 유지하도록 예약된 업데이트를 수행합니다.

복제된 구성에서는 서버의 Edge 구독 설정을 복제하지 않습니다. EdgeSync에서 사용되는 인증서도 복제되지 않습니다. 각 Edge 전송 서버에 대해 EdgeSync 프로세스를 별도로 실행해야 합니다. EdgeSync에서는 복제된 구성 정보와 EdgeSync 복제 정보에 포함된 모든 설정을 덮어씁니다. 이러한 설정에는 송신 커넥터, 수신 커넥터, 허용 도메인, 원격 도메인 등이 있습니다.

## 복제된 구성 프로세스

복제된 구성 프로세스는 다음 세 단계로 이루어집니다.

1.  원본 서버에서 구성을 내보냅니다.
    
    %ExchangeInstallPath%Scripts에 있는 ExportEdgeConfig.ps1 스크립트를 실행하여 원본 서버의 구성 정보를 중간 XML 파일로 내보냅니다.

2.  대상 서버의 구성 유효성을 검사합니다.
    
    %ExchangeInstallPath%Scripts에 있는 ImportEdgeConfig.ps1 스크립트를 실행합니다. 이 스크립트는 중간 XML 파일의 기존 정보를 검사하여 내보낸 설정이 대상 서버에 유효한지 확인한 다음 응답 파일을 만듭니다. 응답 파일은 구성을 대상 서버로 가져올 때 사용되는 서버별 정보를 지정합니다. 대상 서버에 사용할 수 없는 각 원본 서버 설정에 해당하는 항목이 들어 있습니다. 이러한 설정은 대상 서버에 맞게 수정할 수 있습니다. 모든 설정이 유효하게 되면 응답 파일에 항목이 없게 됩니다.

3.  대상 서버에 구성을 가져옵니다.
    
    ImportEdgeConfig.ps1 스크립트는 중간 XML 파일과 응답 파일을 사용하여 기존 구성을 복제하거나 서버를 특정 구성으로 복원합니다.

## 1단계: 원본 서버에서 구성 내보내기

Edge 전송 서버 역할을 설치 및 구성한 후 %ExchangeInsallPath%Scripts에 있는 ExportEdgeConfig.ps1 스크립트를 실행합니다. 이 스크립트는 원본 서버의 구성 정보를 검색하여 중간 XML 파일에 저장합니다.

원본 서버에서 내보내서 중간 XML 파일에 저장되는 정보는 다음과 같습니다.

  - 전송 서비스 관련 정보 및 로그 파일 경로 정보:
    
      - *ReceiveProtocolLogPath*
    
      - *SendProtocolLogPath*
    
      - *MessageTrackingLogPath*
    
      - *PickupDirectoryPath*
    
      - *RoutingTableLogPath*

  - 각 전송 에이전트의 상태 및 우선 순위 설정이 포함된 전송 에이전트 관련 정보

  - 모든 송신 커넥터 관련 정보. 자격 증명을 사용하도록 구성된 송신 커넥터가 있는 경우 암호는 중간 XML 파일에 암호화된 문자열로 기록됩니다. ImportEdgeConfig.ps1 및 ExportEdgeConfig.ps1 스크립트에 *-key* 매개 변수를 사용하여 암호화 및 암호 해독에 사용할 32바이트 문자열을 지정할 수 있습니다. *-key* 매개 변수를 사용하지 않으면 기본 암호화 키가 사용됩니다.

  - 수신 커넥터 관련 정보. 로컬 네트워크 바인딩 및 포트 속성을 수정하려면 구성 유효성 검사 단계에서 만들어진 응답 파일에서 구성 정보를 수정해야 합니다.

  - 허용 도메인 구성

  - 원격 도메인 구성

  - 스팸 방지 기능 구성 설정:
    
      - IP 허용 목록 정보. 관리자가 수동으로 구성한 IP 허용 목록 항목만 내보냅니다.
    
      - IP 차단 목록 정보
    
      - 콘텐츠 필터 구성
    
      - 받는 사람 필터 구성
    
      - 주소 다시 쓰기 항목
    
      - 첨부 파일 필터 항목

맨 위로 이동

## 2단계: 대상 서버의 구성 유효성 검사

대상 서버는 Edge 전송 서버 역할이 새로 설치된 Exchange 2013 서버를 말합니다. 먼저 대상 서버에서 %ExchangeInsallPath%Scripts에 있는 ImportEdgeConfig.ps1 스크립트를 실행하여 중간 XML 파일의 기존 정보 유효성을 검사하고 응답 파일을 만듭니다. 응답 파일은 구성을 대상 서버로 가져올 때 사용되는 서버별 정보를 지정합니다. 대상 서버에 사용할 수 없는 각 원본 서버 설정에 해당하는 항목이 들어 있습니다. 대상 서버에 사용할 수 있도록 이러한 설정을 수정해야 합니다. 모든 설정이 유효하게 되면 응답 파일에 항목이 없게 됩니다. 중간 XML 파일은 여러 대상 서버에 사용할 수 있지만 응답 파일은 대상 서버별로 고유합니다.

%ExchangeInsallPath%Scripts에 있는 ImportEdgeConfig.ps1 스크립트를 실행하면 다음 작업이 수행됩니다.

  - 대상 서버에 데이터 경로와 로그 경로를 만들 수 있는지 확인합니다. 경로를 만들 수 없는 경우 응답 파일에 빈 경로를 삽입합니다.

  - XML 파일의 각 송신 커넥터에 대해 응답 파일에 원본 IP 주소에 해당하는 빈 항목을 추가합니다.

  - XML 파일의 각 수신 커넥터에 대해 응답 파일에 로컬 네트워크 바인딩에 해당하는 빈 항목을 추가합니다.

서버별 설정에 대한 다음 정보를 제공하려면 응답 파일을 수동으로 수정해야 합니다.

  - 데이터 경로와 로그 경로를 입력합니다. 응답 파일에서 해당 경로를 비워 두면 다음 단계에서 대상 서버로 구성을 가져올 때 중간 XML 파일에 구성되는 경로가 사용됩니다.

  - 각 송신 커넥터 항목에 대해 원본 IP 주소를 입력합니다. 이 필드를 비워 두면 구성 가져오기 단계에서 오류가 발생합니다.

  - 각 수신 커넥터 항목에 대해 로컬 네트워크 바인딩을 입력합니다. 로컬 네트워크 바인딩을 비워 두면 대상 서버로 구성을 가져올 때 오류가 발생합니다.

맨 위로 이동

## 3단계: 대상 서버로 구성 가져오기

기존 Edge 전송 서버의 구성을 복제하거나 특정 구성으로 복원하려는 모든 대상 서버에 대해 이 단계를 수행할 수 있습니다. %ExchangeInsallPath%Scripts에 있는 ImportEdgeConfig.ps1 스크립트를 실행하여 새 구성의 유효성을 검사하고 구성을 가져옵니다. 이 스크립트를 실행한 후에는 대상 서버의 구성이 중간 XML 파일 및 응답 파일의 설정과 일치하게 됩니다.


> [!IMPORTANT]
> 복제 작업이 실패하는 경우 서버를 이전의 안정된 상태로 복원할 수 있도록 구성 가져오기 프로세스를 실행하기 전에 기존 서버 구성을 백업해 두는 것이 좋습니다.



이 단계에서는 응답 파일에서 제공되는 서버별 정보가 사용됩니다. 응답 파일에 설정이 지정되지 않은 경우 중간 XML 파일의 데이터가 사용됩니다. 이 단계에서 스크립트는 구성을 수정하기 전에 중간 XML 파일 및 응답 파일에 있는 데이터의 유효성을 검사합니다.

구성 가져오기를 수행하면 다음의 대상 서버 구성 설정이 수정됩니다.

  - 전송 에이전트 구성 수정

  - 대상 서버의 기존 커넥터 제거 및 중간 XML 파일에 있는 커넥터 추가

  - 기존 허용 도메인 제거 및 중간 XML 파일에 있는 허용 도메인 항목 추가

  - 기존 원격 도메인 제거 및 중간 XML 파일에 있는 원격 도메인 항목 추가

  - 기존 IP 허용 목록 항목 제거 및 중간 원격 도메인 파일에 있는 IP 허용 목록 항목 추가

  - 기존 IP 차단 목록 항목 제거 및 중간 원격 도메인 파일에 있는 IP 차단 목록 항목 추가

  - 대상 서버로 복제되는 스팸 방지 구성은 다음과 같습니다.
    
      - 콘텐츠 필터 구성
    
      - 받는 사람 필터 구성
    
      - 주소 다시 쓰기 항목
    
      - 첨부 파일 필터 항목

맨 위로 이동

## 전송 구성 정보

전송 구성 개체의 설정을 통해 Edge 전송 서버의 서버 전체 전자 메일 전송 설정이 정의됩니다. 대상 서버로 중간 XML을 가져오면 다음을 제외한 모든 전송 구성 개체 설정을 가져옵니다.

  - 내보낸 XML 파일의 일반 이름 및 생성 일자

  - 송신 커넥터 정보

  - 수신 커넥터 정보

  - 첨부 파일 필터 항목

  - **MaxDumpsterSizePerStorageGroup** 특성 항목

가져오는 과정이 완료된 후에는 **Set-TransportConfig** cmdlet을 사용하여 설정을 구성할 수도 있습니다. 자세한 내용은 [Set-TransportConfig](https://technet.microsoft.com/ko-kr/library/bb124151\(v=exchg.150\))를 참조하십시오.

다음 표에는 전송 구성 개체에 연관된 특성 및 기본값이 나와 있습니다. 사서함 서버와 Edge 전송 서버 둘 다에서 이 개체를 구성할 수 있습니다. 그러나 대부분의 특성은 Exchange 2013 사서함 서버의 전송 서비스에만 적용됩니다. Edge 전송 서버에서는 이러한 특성을 구성해도 아무런 영향을 주지 않습니다.

### 전송 구성 특성 및 기본값

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>특성</th>
<th>설명</th>
<th>기본값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ClearCategories</strong></p></td>
<td><p>이 특성은 콘텐츠를 변환하는 동안 Microsoft Outlook 범주를 지울지 여부를 지정합니다.</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><strong>GenerateCopyOfDSNFor</strong></p></td>
<td><p>이 특성은 DSN(배달 상태 알림) 메시지가 전자 메일 관리자 전자 메일 주소로 복사되도록 하는 DSN 코드를 지정합니다. DSN 코드는 <em>x.y.z</em> 형식으로 입력되며 쉼표로 구분됩니다.</p></td>
<td><p>5.4.8, 5.4.6, 5.4.4, 5.2.4, 5.2.0, 5.1.4</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalSMTPServers</strong></p></td>
<td><p>이 특성은 보낸 사람 ID 및 연결 필터링에서 무시할 내부 SMTP 서버 IP 주소 또는 IP 주소 범위의 목록을 지정합니다.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>JournalingReportNdrTo</strong></p></td>
<td><p>이 특성은 저널링 사서함을 사용할 수 없는 경우 저널 보고서를 보낼 전자 메일 주소를 지정합니다. Edge 전송 서버의 구성에서는 이 특성이 적용되지 않습니다.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxDumpsterSizePerStorageGroup</strong></p></td>
<td><p>이 특성은 사서함 서버에 있는 전송 휴지통의 최대 크기를 지정합니다. Edge 전송 서버의 구성에서는 이 특성이 적용되지 않습니다.</p></td>
<td><p>18MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxDumpsterTime</strong></p></td>
<td><p>이 특성은 사서함 서버의 전송 휴지통에 전자 메일 메시지가 보존되는 기간을 지정합니다. Edge 전송 서버의 구성에서는 이 특성이 적용되지 않습니다.</p></td>
<td><p>7.00:00:00</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxReceiveSize</strong></p></td>
<td><p>이 특성은 조직의 받는 사람이 받을 수 있는 최대 메시지 크기를 지정합니다. Edge 전송 서버의 구성에서는 이 특성이 적용되지 않습니다.</p></td>
<td><p>10MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxRecipientEnvelopeLimit</strong></p></td>
<td><p>이 특성은 단일 전자 메일 메시지에 허용되는 최대 받는 사람 수를 지정합니다. Edge 전송 서버의 구성에서는 이 특성이 적용되지 않습니다.</p></td>
<td><p>5,000</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxSendSize</strong></p></td>
<td><p>이 특성은 조직의 보내는 사람이 보낼 수 있는 최대 메시지 크기를 지정합니다. Edge 전송 서버의 구성에서는 이 특성이 적용되지 않습니다.</p></td>
<td><p>10MB</p></td>
</tr>
<tr class="even">
<td><p><strong>TLSReceiveDomainSecureList</strong></p></td>
<td><p>이 특성은 도메인 보안을 지원하도록 구성된 수신 커넥터를 통해 상호 TLS(전송 계층 보안) 인증을 사용하는 원격 도메인을 지정합니다. 도메인이 여러 개이면 쉼표로 구분할 수 있습니다. 이 특성에 나열된 도메인에는 와일드카드 문자(*)를 사용할 수 없습니다.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>TLSSendDomainSecureList</strong></p></td>
<td><p>이 특성은 대상 도메인의 주소 공간 및 도메인 보안을 지원하도록 구성된 송신 커넥터를 통해 전자 메일이 전송될 때 상호 TLS 인증을 사용할 원격 도메인을 지정합니다. 도메인이 여러 개이면 쉼표로 구분할 수 있습니다. 이 특성에 나열된 도메인에는 와일드카드 문자(*)를 사용할 수 없습니다.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>VerifySecureSubmitEnabled</strong></p></td>
<td><p>이 특성은 사서함 서버의 사서함으로부터 메시지를 전송 중인 전자 메일 클라이언트에서 암호화된 MAPI 전송을 사용하는지 확인합니다. Edge 전송 서버의 구성에서는 이 특성이 적용되지 않습니다. 이 특성에 사용할 수 있는 유효한 값은 <code>$true</code> 또는 <code>$false</code>입니다.</p></td>
<td><p>False</p></td>
</tr>
<tr class="odd">
<td><p><strong>VoicemailJournalingEnabled</strong></p></td>
<td><p>이 특성은 저널링 에이전트에서 통합 메시징 음성 메시지를 저널링할지 여부를 지정합니다. Edge 전송 서버의 구성에서는 이 특성이 적용되지 않습니다.</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Edge 전송 서버가 이후에 Exchange 조직에 구독되면 EdgeSync 프로세스 중에 <STRONG>InternalSMTPServers</STRONG> 특성의 값을 덮어씁니다. 자세한 내용은 <A href="edge-subscriptions-exchange-2013-help.md">Edge 구독</A>를 참조하십시오.



맨 위로 이동

