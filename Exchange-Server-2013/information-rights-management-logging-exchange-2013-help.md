---
title: '정보 권한 관리 로깅: Exchange 2013 Help'
TOCTitle: 정보 권한 관리 로깅
ms:assetid: e06f57f9-a9e2-43a2-b88c-288b324d71f0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff461940(v=EXCHG.150)
ms:contentKeyID: 50484324
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 정보 권한 관리 로깅

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange Server 2013, 정보 권한 관리 (IRM) 작업 IRM 로그에 기록 됩니다. IRM 로그를 모니터링 하 고 Exchange 2013 서버에서 서비스 RMS (권한 관리) 클라이언트와 조직에서 Active Directory 권한 관리 서비스 (AD RMS) 클러스터 간의 상호작용 문제를 해결 하는데 도움이 됩니다.

IRM에 대한 자세한 내용은 [정보 권한 관리](information-rights-management-exchange-2013-help.md)를 참조하십시오.

**목차**

IRM 로그의 구조

로깅 프로세스

IRM 로그에 기록 되는 정보

로그 IRM 관리

IRM과 관련된 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md)를 참조하십시오.

## IRM 로그의 구조

기본적으로 IRM 로그는 C:\\Program Files\\Microsoft\\Exchange Server\\V14\\Logging\\IRMLogs에 있습니다.

IRM 로그 파일의 명명 규칙은 \<*프로세스*\>\_\<*프로세스 식별자* 또는 *IIS AppPool 식별자*\>\_IRMLOG*yyyymmdd*-*nnnn*.log입니다. 여기서 각 항목은 다음을 나타냅니다.

  - \<*Process*\>= 로그 파일을 만드는 프로세스입니다. 예, 전송 서비스에서이 속성은 EdgeTransport 합니다.

  - \<*프로세스 식별자* 또는 *IIS AppPool 식별자\>* =프로세스의 숫자 ID입니다.

  - *yyyymmdd* = 로그 파일이 생성된 UTC(협정 세계시) 날짜입니다.

  - *nnnn* = 매일 1부터 시작하는 인스턴스 번호입니다.

IRM 로그 파일 이름의 예는 EdgeTransport\_1056\_IRMLOG20101201-1.log입니다.

다음 표는 각 서버 역할에 대해 생성되는 로그를 보여 줍니다.

### 서버 역할에 대한 로그

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>서버 역할</th>
<th>IRM 로그 파일 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>전송 서비스</p></td>
<td><p>EdgeTransport_&lt;<em>프로세스 식별자</em>&gt;_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>이 로그를 사용 하 여 전송 파이프라인 (예: 전송 보호 규칙 및 저널 보고서 암호 해독) 전송 서비스에 수행한 모든 RMS 트랜잭션을 기록 합니다. Edgetransport.exe 프로세스의 프로세스 id (PID) 로그 파일 이름을 생성 하는데 사용 됩니다.</p></td>
</tr>
<tr class="even">
<td><p>사서함</p></td>
<td><p>msftefd_&lt;<em>프로세스 식별자</em>&gt;_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>이 로그를 사용 하 여 검색 및 인덱스 요청 하는 동안 발생 하는 모든 RMS 거래를 기록 합니다. Exchange 2013 사서함 서버 콘텐츠 인덱싱에 대 한 msftefd.exe 프로세스를 사용합니다. Msftefd.exe 프로세스의 PID 로그 파일 이름을 생성 하는데 사용 됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>클라이언트 액세스</p></td>
<td><p>w3wp_MSExchangeOWAAppOol_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>이 로그는 Microsoft OfficeOutlook Web App에서 IRM에 대한 모든 트랜잭션을 기록하는 데 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p>모든 Exchange 2013 서버 역할</p></td>
<td><p>w3wp_MSExchangePowerShellAppPool_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>이 로그는 예를 들어 <strong>Test-IRMConfiguration</strong> cmdlet을 실행할 때 Windows PowerShell에서 실행되는 모든 IRM RMS 트랜잭션을 기록하는 데 사용됩니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 로깅 프로세스

파일 크기가 지정한 최대값에 도달할 때까지 로그 파일에 정보가 기록됩니다. 최대 크기에 도달하면 증가하는 인스턴스 번호가 있는 로그 파일이 생성됩니다. 이 프로세스는 하루 종일 반복됩니다. IRM 로그 디렉터리가 지정된 최대 크기에 도달하거나 로그 파일이 각 서버의 IRM 로깅 구성에 지정된 최대 보존 기간에 도달하면 순환 로깅은 가장 오래된 로그 파일을 삭제합니다.

맨 위로 이동

## IRM 로그에 기록 되는 정보

IRM 로그 파일은 CSV(쉼표로 분리된 값) 형식으로 데이터를 포함하는 텍스트 파일입니다. 각 IRM 로그에는 다음과 같은 정보가 포함된 헤더가 있습니다.

  - **\#Software:**    IRM 로그 파일을 만든 소프트웨어의 이름입니다. 일반적으로 값은 `Microsoft Exchange Server`입니다.

  - **\#Version:**    IRM 로그 파일을 만든 소프트웨어의 버전 번호입니다.

  - **\#Log-type**   로그 유형 값으로, `Rms Client Manager Log`입니다.

  - **\#Date:**    로그 파일이 만들어진 UTC 날짜 및 시간입니다. UTC 날짜 및 시간은 다음과 같은 ISO 8601 날짜-시간 형식으로 표시됩니다. *yyyy*-*mm*-*dd*T*hh*:*mm*:*ss.fff*Z. 여기서 각 항목은 다음을 나타냅니다.
    
      - yyyy = 년
    
      - *mm* = 월
    
      - *dd* = 일
    
      - T = 시간 구성 요소의 시작을 표시하는 데 사용되는 시간 지정자
    
      - *hh* = 시간
    
      - *mm* = 분
    
      - *ss* = 초
    
      - *fff* = 1초의 분수
    
      - Z = Zulu(UTC를 표시하는 또 다른 방법)

  - **\#Fields:**    IRM 로그 파일에서 사용되는 쉼표로 구분된 필드 이름입니다.
    
    IRM 로그에는 각 RMS 트랜잭션 이벤트가 단일 줄에 저장되며 쉼표로 구분된 필드로 구성됩니다. 다음 표는 IRM 기능이 사용되는 모든 서버 역할에 대한 IRM 로그의 필드를 보여 줍니다.
    
    ### IRM 로그에 사용되는 필드
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>필드</th>
    <th>설명</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Date-time</strong></p></td>
    <td><p>UTC 타임스탬프를 나열합니다.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Feature</strong></p></td>
    <td><p>사용된 RMS 클라이언트 기능을 나열합니다. 사용할 수 있는 값은 다음과 같습니다.</p>
    <ul>
    <li><p><code>RacClc</code></p></li>
    <li><p><code>Template</code></p></li>
    <li><p><code>Prelicense</code></p></li>
    <li><p><code>UseLicense</code></p></li>
    <li><p>서명 확인</p></li>
    <li><p><code>ServerInfo</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Event-Type</strong></p></td>
    <td><p>이벤트 유형을 나열합니다. 사용할 수 있는 값은 다음과 같습니다.</p>
    <ul>
    <li><p><code>Acquire</code>   RMS 라이선스 또는 템플릿이 요청되었습니다.</p></li>
    <li><p><code>Success</code>   RMS 라이선스 또는 템플릿을 구했습니다.</p></li>
    <li><p><code>Exception</code>   오류가 발생했습니다.</p></li>
    <li><p><code>Queued</code>   요청이 보류 중입니다.</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><p><strong>Tenant-Id</strong></p></td>
    <td><p>Microsoft 내부용으로 예약되어 있습니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Server-url</strong></p></td>
    <td><p>작업 중에 액세스한 RMS 서버 URL을 나열합니다.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Context</strong></p></td>
    <td><p>호출 프로세스에서 여러 RMS 트랜잭션을 함께 결합하는 데 사용합니다. 사용할 수 있는 값은 다음과 같습니다.</p>
    <ul>
    <li><p><code>MessageID: &lt;Actual message ID&gt;</code></p></li>
    <li><p><code>MailboxGuid: &lt;Mailbox GUID&gt;</code></p></li>
    <li><p><code>AttachmentFileName: &lt;File name&gt;</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Transaction-id</strong></p></td>
    <td><p>고유 트랜잭션을 식별합니다. 한 트랜잭션 중에 발생하는 모든 이벤트는 동일한 트랜잭션 ID를 갖습니다.</p></td>
    </tr>
    </tbody>
    </table>


맨 위로 이동

## 로그 IRM 관리

IRM 기능을 사용할 수 있는 각 서버 역할에서 IRM 로깅이 기본적으로 사용됩니다. 각 서버 역할에 대해 서버 역할의 해당 **Set** cmdlet을 사용하여 다음과 같은 IRM 로그 구성을 수정할 수 있습니다. 예를 들어, 사서함 서버에서 IRM 로깅을 구성하려면 **Set-MailboxServer** cmdlet을 사용합니다.

### IRM 로그에 대한 구성 매개 변수

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
<td><p><em>IrmLogEnabled</em></p></td>
<td><p>IRM 트랜잭션의 로깅을 사용하도록 설정합니다. IRM 로깅은 기본적으로 사용하도록 설정되어 있습니다. 서버 역할에 대해 IRM 로깅을 사용하지 않도록 설정하려면 매개 변수를 <code>$false</code>로 설정합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxAge</em></p></td>
<td><p>IRM 로그 파일의 최대 보존 기간을 지정합니다. 지정된 보존 기간보다 오래된 파일은 삭제됩니다. 기본값은 <code>30.00:00:00</code>(30일)입니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogMaxDirectorySize</em></p></td>
<td><p>연결 로그 디렉터리에 있는 모든 IRM 로그의 최대 크기를 지정합니다. 디렉터리가 최대 파일 크기에 도달하면 서버에서 가장 오래된 파일을 먼저 삭제합니다. 기본값은 <code>250 MB</code>입니다.</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxFileSize</em></p></td>
<td><p>단일 로그 파일의 최대 파일 크기를 지정합니다. 파일이 지정된 크기에 도달하면 로그 파일이 생성되고 인스턴스 번호가 증가합니다. 기본값은 <code>10 MB</code>입니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogPath</em></p></td>
<td><p>IRM 로그 위치를 지정합니다. 기본 경로 %ExchangeInstallPath%Logging\IRMLogs 합니다.</p></td>
</tr>
</tbody>
</table>


구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Set-MailboxServer](https://technet.microsoft.com/ko-kr/library/aa998651\(v=exchg.150\))

  - [Set-ClientAccessServer](https://technet.microsoft.com/ko-kr/library/bb125157\(v=exchg.150\))

  - [Set-TransportService](https://technet.microsoft.com/ko-kr/library/jj215682\(v=exchg.150\))

맨 위로 이동

