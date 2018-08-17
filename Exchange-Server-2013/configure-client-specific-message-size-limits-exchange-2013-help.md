---
title: '클라이언트별 메시지 크기 제한 구성: Exchange 2013 Help'
TOCTitle: 클라이언트별 메시지 크기 제한 구성
ms:assetid: fef9ca78-b68f-4342-ada0-881ab985ce3c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh529949(v=EXCHG.150)
ms:contentKeyID: 52058133
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 클라이언트별 메시지 크기 제한 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-01-26_

Microsoft Exchange Server 2013에는 Exchange 조직을 통과하는 메시지에 적용되는 여러 다양한 메시지 크기 제한이 있습니다. 자세한 내용은 [메시지 크기 제한](message-size-limits-exchange-2013-help.md)을 참조하십시오.

그러나 클라이언트별 메시지 크기 제한 ActiveSync 또는 Exchange Web Services (EWS)를 사용 하는 Outlook Web App 및 전자 메일 클라이언트에 대해 구성할 수 있습니다. Exchange 조직 차원 메시지 크기 제한을 변경 되는 경우 Outlook Web App, ActiveSync 대 한 메시지 크기를 제한 하 고 그에 따라 Exchange 웹 서비스 설정 확인 해야 합니다. 클라이언트 액세스 서버 및 사서함 서버에 있는 web.config 파일에서 이러한 값을 구성합니다. 이러한 제한은 다음 표에 설명 되어있습니다.

### ActiveSync

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>서버 역할</th>
<th>구성 파일</th>
<th>키 및 기본값</th>
<th>크기</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>클라이언트 액세스</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   기본적으로 없음 (메모 참조).</p></td>
<td><p>바이트</p></td>
</tr>
<tr class="even">
<td><p>클라이언트 액세스</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>(킬로바이트)</p></td>
</tr>
<tr class="odd">
<td><p>사서함</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   기본적으로 없음 (메모 참조).</p></td>
<td><p>바이트</p></td>
</tr>
<tr class="even">
<td><p>사서함</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>(킬로바이트)</p></td>
</tr>
<tr class="odd">
<td><p>사서함</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>&lt;add key=&quot;MaxDocumentDataSize&quot; value=&quot;10240000&quot;&gt;</code></p></td>
<td><p>바이트</p></td>
</tr>
</tbody>
</table>


**ActiveSync 제한에 대 한 의견**

기본적으로 ActiveSync 의 `web.config` 파일에 없는 *maxAllowedContentLength* 키가 합니다. 그러나 ActiveSync 에 대 한 최대 메시지 크기는 서버에서 모든 웹 사이트에 적용 되는 **maxAllowedContentLength** 값에 의해 영향을 받습니다. 기본값은 30000000 바이트 (30 MB)입니다. 클라이언트 액세스 서버 및 사서함 서버에서 IIS 관리자에서 ActiveSync 에 대해 이러한 값을 보려면 다음 단계를 수행 합니다.

1.  다음 단계 중 하나를 수행 합니다.
    
      - 클라이언트 액세스 서버에서 **IIS 관리자** 를 열고, **사이트로** 이동 \> **기본 웹사이트** 및 **Microsoft-서버-ActiveSync** 선택 합니다.
    
      - 사서함 서버에서 **IIS 관리자** 를 열고, **사이트로** 이동 \> **Exchange 백엔드** 및 **Microsoft-서버-ActiveSync** 선택 합니다.

2.  **기능 보기**, 선택한 **관리** 섹션에서 **구성 편집기** 두번클릭를 확인 합니다.

3.  **섹션** 필드의 드롭다운 화살표를 클릭, **system.webServer** 로 이동 \> **보안** 및 **requestFiltering** 선택 합니다.

4.  결과에서 **requestLimits** 확장 하 고 **maxAllowedContentLength** 및 기본값 (바이트) 30000000 표시 됩니다.

**maxAllowedContentLength** 값을 변경 하려면 바이트에 새 값을 입력 하 고 **적용** 을 클릭 합니다. 클라이언트 액세스 서버 및 사서함 서버에 값을 변경 해야 합니다. IIS 관리자에서 값을 변경한 후 새로운 *maxAllowedContentLength* 키 (클라이언트 액세스 서버에서`%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config` ) 및 사서함 서버에서 `%ExchangeInstallPath%ClientAccess\Sync\web.config` 해당 `web.config` 파일에 기록 됩니다.

ActiveSync 클라이언트에 대 한 최대 메시지 크기를 변경 하려면 클라이언트 액세스 서버 및 사서함 서버에서 `web.config` 파일에서 *maxRequestLength* , 사서함 서버에서 `web.config` 파일에서 *MaxDocumentDataSize* 및 *maxAllowedContentLength* IIS 관리자에서 클라이언트 액세스 서버 및 사서함 서버에서의 값을 변경 해야 합니다.

### Exchange Web Services

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>역할을 역합니다</th>
<th>구성 파일</th>
<th>키 및 기본값</th>
<th>크기</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>클라이언트 액세스</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>바이트</p></td>
</tr>
<tr class="even">
<td><p>사서함</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>바이트</p></td>
</tr>
<tr class="odd">
<td><p>사서함</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxReceivedMessageSize=&quot;67108864&quot;</code> 의 14 인스턴스</p></td>
<td><p>바이트</p></td>
</tr>
</tbody>
</table>


**Exchange 웹 서비스 제한에 대 한 의견**

  - (Http 및 https) 바인딩 및 인증 방법의 다양 한 조합을에 해당 하는 값 `maxReceivedMessageSize="67108864"` 의 14 별도 인스턴스가 있습니다.

  - Exchange 웹 서비스 클라이언트에 대 한 최대 메시지 크기를 변경 하려면 *maxAllowedContentLength*`web.config` 파일 및 모든 14 인스턴스의 `maxReceivedMessageSize="67108864"` 사서함 서버에서 `web.config` 파일에 모두의 값을 변경 해야 합니다.

  - 사서함 서버에서 `web.config` 파일에서 수정할 필요가 없는 **UMLegacyMessageEncoderSoap11Element** 바인딩의 값 `maxReceivedMessageSize="1048576"` 의 두 인스턴스도 있습니다.

  - *maxRequestLength* 는 두 web.config 파일에는 있지만 수정 하지 않아도 Exchange 웹 서비스에서 사용 되지 않은 ASP.NET 설정 합니다.

### Outlook Web App

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>서버 역할</th>
<th>구성 파일</th>
<th>키 및 기본값</th>
<th>크기</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>클라이언트 액세스</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>바이트</p></td>
</tr>
<tr class="even">
<td><p>클라이언트 액세스</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>(킬로바이트)</p></td>
</tr>
<tr class="odd">
<td><p>사서함</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>바이트</p></td>
</tr>
<tr class="even">
<td><p>사서함</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>(킬로바이트)</p></td>
</tr>
<tr class="odd">
<td><p>사서함</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxReceivedMessageSize=&quot;35000000&quot;</code> 의 2 인스턴스</p></td>
<td><p>바이트</p></td>
</tr>
<tr class="even">
<td><p>사서함</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxStringContentLength=&quot;35000000&quot;</code> 의 2 인스턴스</p></td>
<td><p>바이트</p></td>
</tr>
</tbody>
</table>


**Outlook Web App 제한에 대 한 의견**

  - 사서함 서버에서 `web.config` 파일에서 http 및 https 바인딩을에 해당 하는 값 `maxReceivedMessageSize="35000000"` 및 `maxStringContentLength="35000000"` 별도 두 인스턴스가 있습니다.

  - Outlook Web App 클라이언트에 대 한 최대 메시지 크기를 변경 하려면 모든 사서함 서버에서 `web.config` 파일에서 *maxReceivedMessageSize* 및 *maxStringContentLength* 의 두 인스턴스를 포함 하 여 두 파일에 이러한 값을 변경 해야 합니다.

  - 사서함 서버에서 `web.config` 파일에서 수정할 필요가 없는 **MsOnlineShellService** 바인딩에 대 한 값 `maxStringContentLength="102400"` 의 인스턴스도 됩니다.

모든 메시지 크기 제한에 대해 적용하려는 실제 크기보다 큰 값을 설정해야 합니다. 이처럼 값을 더 크게 설정해야 하는 이유는, 메시지 첨부 파일 및 기타 이진 데이터가 Base64로 인코딩되고 나면 메시지 크기가 항상 증가하기 때문입니다. Base64 인코딩 시에는 메시지 크기가 약 33% 증가하기 때문에 메시지 크기 제한에 대해 지정하는 값은 실제 사용 가능한 메시지 크기보다 약 33% 더 커야 합니다. 예를 들어 최대 메시지 크기 값을 64MB로 지정하는 경우 실제 최대 메시지 크기 값은 약 48MB가 됩니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이 항목의 절차에는 Exchange 권한이 적용되지 않습니다. 이 절차는 Exchange Server의 운영 체제에서 수행됩니다.

  - Web.config 구성 파일에 저장하는 변경 내용은 IIS를 다시 시작하고 나면 적용됩니다.

  - Base64 인코딩으로 인한 33% 크기 증가를 허용하려면 메가바이트 단위의 원하는 새 최대 크기 값에 4/3을 곱합니다. 이 값을 킬로바이트 단위로 변환하려면 1024를 곱하고, 바이트 단위로 변환하려면 1048756(1024\*1024)을 곱합니다. Base64 인코딩 시에는 크기가 33%보다 더 증가할 수 있으며 크기 증가율은 첨부 파일 크기, 형식, 압축, 메시지 작성/보내기에 사용한 전자 메일 클라이언트 등의 여러 요소에 따라 달라집니다.

  - Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 파일 또는 사서함 서버의 EdgeTransport.exe.config 파일)에 설정하는 사용자 지정된 모든 서버 단위 설정은 Exchange CU(누적 업데이트)를 설치하면 덮어쓰게 됩니다. 설치 후 서버를 쉽게 다시 구성할 수 있도록 이 정보를 저장했는지 확인하세요. 이러한 설정은 Exchange CU를 설치한 후에 다시 구성해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 메모장을 사용 하 여 클라이언트별 메시지 크기 제한을 구성 하려면

1.  메모장에서 적절 한 web.config 파일을 엽니다. 예, Exchange Web Services 클라이언트에 대 한 web.config 파일을 열려면 다음 명령을 실행 합니다.
    
        Notepad %ExchangeInstallPath%ClientAccess\exchweb\ews\web.config
        Notepad %ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config

2.  항목의 앞부분에서 테이블의 설명에 따라 적절 한 web.config 파일에서 관련 키를 찾습니다. 예 Exchange Web Services 클라이언트에 대 한 키를 찾을 *maxAllowedContentLength* 파일 및 모든 14 인스턴스의 값 `maxReceivedMessageSize="67108864"` 모두에서 사서함 서버에서 `web.config` 파일에 있습니다.
    
        <requestLimits maxAllowedContentLength="67108864" />
        ...maxReceivedMessageSize="67108864"...
    
    예를 들어 Base64로 인코딩된 최대 메시지 크기를 약 64MB로 허용하려면 모든 `67108864` 인스턴스를 `89478486`(64\*4/3\*1048756)으로 변경합니다.
    
        <requestLimits maxAllowedContentLength="89478486" />
        ...maxReceivedMessageSize="89478486"...

3.  작업이 끝나면 저장 하 고 web.config 파일을 닫습니다.

4.  다음 명령을 실행하여 IIS를 다시 시작합니다.
    
        IISReset /noforce

## 명령줄에서 클라이언트별 메시지 크기 제한 구성

메모장을 사용 하는 대신 명령줄에서 클라이언트별 메시지 크기 제한을 구성할 수도 있습니다. (명령 프롬프트 창 **관리자 권한으로 실행** 을 선택 하 여 열면) Exchange 서버에서 관리자 권한으로 명령 프롬프트를 열고 하 고 구성할 수는 제한에 대 한 적절 한 명령을 실행 합니다.

**참고**:

  - 명령에서 크기 값에서 기본값을 되므로으로 변경 해야 합니다.

  - 바이트 또는 킬로바이트에 값이 있는지 여부에 주의 해야 합니다.

**ActiveSync**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:appSettings /[key='MaxDocumentDataSize'].value:10240000

**Exchange Web Services**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpsBinding'].maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpBinding'].maxReceivedMessageSize:67108864

**Outlook Web App**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].readerQuotas.maxStringContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].readerQuotas.maxStringContentLength:35000000

## 작동 여부는 어떻게 확인합니까?

클라이언트별 메시지 크기 제한 구성 되었는지 확인 하려면, 하 고 영향을 받는 클라이언트에 의해 액세스 되는 사서함에서 테스트 메시지를 보내려고 해야 합니다. 테스트 메시지는 약 33% 미만으로 구성한 하므로 몇가지 더 작은 첨부 파일 또는 큰 첨부 파일이 하나 시도할 수 있습니다. 예, 구성 된 값이 85 MB 사실적인 최대 메시지 크기를 약 64MB의 만들어집니다.

