---
title: '레거시 전송 에이전트에 대 한 지원을 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 레거시 전송 에이전트에 대 한 지원을 사용 하도록 설정
ms:assetid: 00617e87-7199-406e-b4a3-94378f657f1f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ591524(v=EXCHG.150)
ms:contentKeyID: 50482369
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 레거시 전송 에이전트에 대 한 지원을 사용 하도록 설정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

Microsoft Exchange Server 2013에서는 Microsoft .NET Framework 버전 4.0을 사용하여 만든 전송 에이전트가 기본적으로 지원됩니다. Exchange 2013에서 이전 버전의 .NET Framework를 사용하여 만든 전송 에이전트를 지원하지만 이러한 레거시 전송 에이전트에 대한 지원은 기본적으로 사용되지 않습니다. 레거시 전송 에이전트에 대한 지원을 사용하도록 설정하려면 해당 XML 응용 프로그램 구성 파일을 수정해야 합니다. 수정해야 하는 파일은 전송 에이전트가 설치된 위치에 따라 다릅니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>서버</th>
<th>응용 프로그램 구성 파일</th>
<th>Microsoft Windows 서비스</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>클라이언트 액세스 서버</p></td>
<td><p>%ExchangeInstallPath%Bin\MSExchangeFrontendTransport.exe.config</p></td>
<td><p>Microsoft Exchange 프런트 엔드 전송(MSExchangeFrontendTransport)</p></td>
</tr>
<tr class="even">
<td><p>사서함 서버</p></td>
<td><ul>
<li><p>%ExchangeInstallPath%Bin\EdgeTransport.exe.config</p></li>
<li><p>%ExchangeInstallPath%Bin\MSExchangeTransport.exe.config</p></li>
</ul></td>
<td><p>Microsoft Exchange Transport(MSExchangeTransport)</p></td>
</tr>
</tbody>
</table>


레거시 전송 에이전트에 대한 지원은 응용 프로그램 구성 파일에 있는 키로 제어됩니다. 기본적으로 응용 프로그램 구성 파일에는 필요한 키가 아무것도 없습니다. 따라서 키를 수동으로 추가해야 합니다. 다음 표에서는 각 키에 대해 더 자세히 설명합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>키</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>useLegacyV2RuntimeActivationPolicy</em></p></td>
<td><p>이 키는 레거시 전송 에이전트에 대한 지원을 사용하거나 사용하지 않도록 설정합니다. 이 키의 유효한 값은 <code>true</code> 또는 <code>false</code>입니다. 이 키를 지정하지 않은 경우 기본값은 <code>false</code>입니다.</p></td>
</tr>
<tr class="even">
<td><p><em>supportedRuntime version</em></p></td>
<td><p>이 키는 에이전트에 필요한 Microsoft .NET Framework 버전을 지정합니다. 이 키의 유효한 값은 다음과 같습니다.</p>
<ul>
<li><p><code>v4.0</code> 또는 <code>v4.0.30319</code></p></li>
<li><p><code>v3.5</code> 또는 <code>v3.5.21022</code></p></li>
<li><p><code>v3.0</code> 또는 <code>v3.0.4506</code></p></li>
<li><p><code>v2.0</code> 또는 <code>v2.0.50727</code></p></li>
</ul>
<p>여러 <em>supportedRuntime version</em> 키 인스턴스를 사용하여 여러 값을 지정합니다.</p>
<p><em>useLegacyV2RuntimeActivationPolicy</em> 키를 사용하여 레거시 전송 에이전트 지원을 사용하도록 설정하는 경우 레거시 전송 에이전트에 필요한 값 외에도 <code>v4.0</code> 값을 항상 지정해야 합니다.</p></td>
</tr>
</tbody>
</table>


## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이 항목의 절차에는 Exchange 권한이 적용되지 않습니다. 이 절차는 Exchange Server의 운영 체제에서 수행됩니다.

  - 응용 프로그램 구성 파일에 저장하는 변경 내용은 해당 서비스를 다시 시작한 후에 적용됩니다.

  - 응용 프로그램 구성 파일과 연결된 서비스 중 하나를 다시 시작하면 서버의 메일 흐름이 일시적으로 중단됩니다.

  - Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 파일 또는 사서함 서버의 EdgeTransport.exe.config 파일)에 설정하는 사용자 지정된 모든 서버 단위 설정은 Exchange CU(누적 업데이트)를 설치하면 덮어쓰게 됩니다. 설치 후 서버를 쉽게 다시 구성할 수 있도록 이 정보를 저장했는지 확인하세요. 이러한 설정은 Exchange CU를 설치한 후에 다시 구성해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 명령 프롬프트를 사용하여 레거시 전송 에이전트에 대한 지원 구성

레거시 전송 에이전트에 대한 지원을 사용하도록 설정하려면 다음 절차를 따르십시오.

1.  명령 프롬프트 창을 열고 레거시 전송 에이전트 지원을 구성하려는 Exchange 2013 서버에서 다음 명령을 실행하여 메모장으로 해당 응용 프로그램 구성 파일을 엽니다.
    
        Notepad %ExchangeInstallPath%Bin\<AppConfigFile>
    
    예를 들어 사서함 서버의 EdgeTransport.exe.config 파일을 열려면 다음 명령을 실행합니다.
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  파일 끝에서 *\</configuration\>* 키를 찾고 다음 키를 *\</configuration\>* 키 앞에 붙여 넣습니다.
    
        <startup useLegacyV2RuntimeActivationPolicy="true">
           <supportedRuntime version="v4.0" />
           <supportedRuntime version="v3.5" />
           <supportedRuntime version="v3.0" />
           <supportedRuntime version="v2.0" />
        </startup>

3.  작업을 마치면 응용 프로그램 구성 파일을 저장하고 닫습니다.

4.  다른 응용 프로그램 구성 파일을 수정하려면 1~3단계를 반복합니다.

5.  다음 명령을 실행하여 연결된 Windows 서비스를 다시 시작합니다.
    
        net stop <service> && net start <service>
    
    예를 들어 EdgeTransport.exe.config 파일을 수정한 경우 다음 명령을 실행하여 Microsoft Exchange Transport Service를 다시 시작해야 합니다.
    
        net stop MSExchangeTransport && net start MSExchangeTransport

6.  다른 수정된 응용 프로그램 구성 파일과 연결된 서비스를 다시 시작하려면 5단계를 반복합니다.

## 작동 여부는 어떻게 확인합니까?

이 절차는 레거시 전송 에이전트가 성공적으로 설치된 경우에 효과가 있습니다. 이 항목의 절차를 수행하지 않고 레거시 전송 에이전트를 설치하려고 하면 다음과 유사한 오류가 수신됩니다.

    Mixed mode assembly is built against version '<version>' of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.

