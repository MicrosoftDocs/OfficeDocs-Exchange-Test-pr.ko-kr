---
title: OWA 문제를 해결 합니다. Protocol.Dep 상태 설정
TOCTitle: OWA 문제를 해결 합니다. Protocol.Dep 상태 설정
ms:assetid: f39c63d5-f161-4eee-9415-05f3355e7cc7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.owa.protocol.dep(v=EXCHG.150)
ms:contentKeyID: 54651896
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# OWA 문제를 해결 합니다. Protocol.Dep 상태 설정

 

_**적용 대상:** Exchange Server 2013, Project Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

IM (인스턴트 메시징) 서비스에 Outlook Web AppLync 2013 및 Exchange 2013 간의 통합 된의 전반적인 상태를 모니터링 하는 **OWA.Protocol.DEP** 상태 설정 합니다. Outlook Web App 에서 인스턴트 메시징을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [Microsoft Lync Server 2013 통합 (영문) 및 Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418)을 참조 하십시오.

**OWA.Protocol.DEP** 상태 설정 상태가 정상 인지 여부를 나타내는 알림이 표시 하는 경우이 Outlook Web App 에서 정상적으로 작동에서 인스턴트 메시징를 방해할 수 있는 문제를 나타냅니다.

## 설명

**OWA.Protocol.DEP** 서비스는 다음 프로브 및 모니터를 사용 하 여 모니터링 됩니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>프로브</th>
<th>상태 설정</th>
<th>연결된 모니터</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>OwaIMInitializationFailedMonitor</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>WacDiscoveryFailureEventMonitor</p></td>
</tr>
</tbody>
</table>


프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 사용자 작업

경고를 발급 한 후 서비스 복구는 불가능 합니다. 따라서 **OWA.Protocol.DEP** 상태 설정 상태가 정상 인지를 지정 하는 알림을 받으면 먼저 문제가 여전히 있는지 확인 합니다. 이 문제는 존재 하는 경우 다음 섹션에 설명 된 적절 한 복구 작업을 수행 합니다.

## 오류에 대 한 복구 작업: "InstantMessageOCSProvider.InitializeEndpointManager 합니다. 레지스트리 설정이 없습니다 IM 공급자에 대 한. "

이 오류는 사서함 서버에 필요한 레지스트리 키를 없는 나타냅니다. 이 레지스트리 키는 서버에는 Microsoft 통합 통신 관리 되는 API (UCMA) 4.0 설치 시에 구성 된 해야 합니다. 누락 된 레지스트리 키는 다음과 같습니다.

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\MSExchange OWA\InstantMessaging

이 키는 `Microsoft.Rtc.Internal.Ucweb` DLL 가리키는 **ImplementationDLLPath** 문자열을 포함 해야 합니다. 기본 위치는 `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP\Microsoft.Rtc.Internal.Ucweb.dll`합니다.

이 문제를 해결 하려면 UCMA 4.0을 다시 설치 하거나 수동으로 레지스트리 키를 만듭니다. 여기에 UCMA 4.0를 다운로드할 수 있습니다: [Unified Communications Managed API 4.0 Runtime](https://go.microsoft.com/fwlink/p/?linkid=260990)합니다.

## 오류에 대 한 복구 작업: "InstantMessageOCSProvider.InitializeEndpointManager 합니다. IM 공급자 찾을 수 없습니다. "

이 오류는 `Microsoft.Rtc.Internal.Ucweb` DLL 파일은 사서함 서버에서 누락 된를 나타냅니다. UCMA 4.0 서버에 설치 된 경우이 파일이 설치 된 해야 합니다. 기본 위치는 `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP`합니다.

이 문제를 해결 하려면 UCMA 4.0을 다시 설치 합니다. 자세한 내용은 [Unified Communications Managed API 4.0 Runtime](https://go.microsoft.com/fwlink/p/?linkid=260990)을 참조 하십시오.

## 오류에 대 한 복구 작업: "인스턴트 메시징 서버 이름은 설정"을 null 또는 빈 web.config에서 합니다.

이 오류는 Lync 2013 서버 사서함 서버에서 Outlook Web App 응용 프로그램 구성 파일 (web.config) 파일에서 정의 되어있지 나타냅니다. 이 `web.config` 파일은 `%ExchangeInstallPath%ClientAccess\Owa`있으며 Lync 2013 서버의 FQDN을 지정 하는 **IMServerName** 라는 키를 포함 해야 합니다. 이 문제를 해결 하려면 다음이 단계를 따릅니다.

1.  명령 프롬프트 창에서 다음 명령을 실행 하 여 Outlook Web App web.config 파일을 메모장에서에서 엽니다.
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  **IMServerName**라는 키를 검색 합니다. 발견 되는 경우 Lync 2013 서버의 FQDN을 확인 합니다. 키가 없는 경우 다음 단계를 수행 하 여 추가 합니다.
    
    1.  **\<appSettings\>**라는 태그를 소개 합니다.
    
    2.  **\<appSettings\>** 노드에 다음 줄을 추가 합니다.
        
            <add key="IMServerName" value="Lync Server FQDN" />
        
        예를 들면 다음과 같습니다.
        
            <add key="IMServerName" value="lync01.contoso.com" />
    
    3.  Outlook Web App 변경 된 내용을 적용 하려면 다음 명령을 실행 합니다.
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## 오류에 대 한 복구 작업: "인스턴트 메시징 인증서 지문을 null 또는 빈 web.config에서 되었습니다."

이 오류는 사서함 서버에서 Outlook Web App 응용 프로그램 구성 파일 (web.config) 파일에 정의 되어있지 Lync 2013 및 Outlook Web App 통합 하는데 사용 되는 인증서를 나타냅니다. 이 `web.config` 파일은 `%ExchangeInstallPath%ClientAccess\Owa`있으며 인증서의 지문 (해시)를 지정 하는 **IMCertificateThumbprint** 라는 키를 포함 해야 합니다.

**Get-ExchangeCertificate** cmdlet을 사용 하 여 또는 **서버** 에 Exchange 관리 센터 (EAC)에서 인증서의 지문 값을 가져올 수 있습니다 \> **인증서** 입니다.

이 문제를 해결 하려면 다음이 단계를 따릅니다.

1.  명령 프롬프트 창에서 다음 명령을 실행 하 여 Outlook Web App web.config 파일을 메모장에서에서 엽니다.
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  **IMCertificateThumbprint**라는 키를 검색 합니다. 발견 되는 경우 지문 값이 올바른지 확인 합니다. 키가 없는 경우 다음 단계를 수행 하 여 추가 합니다.
    
    1.  **\<appSection\>**라는 태그를 소개 합니다.
    
    2.  **\<appSection\>** 노드에 다음 줄을 추가 합니다.
        
            <add key="IMCertificateThumbprint" value="thumbprint"/>
        
        예를 들면 다음과 같습니다.
        
            <add key="IMCertificateThumbprint" value="35CB4C441D55506C88E59B7946B567A4F45B3B5C" />
    
    3.  Outlook Web App 변경 된 내용을 적용 하려면 다음 명령을 실행 합니다.
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## 오류에 대 한 복구 작업: "\< 값 \> 지문이 있는 IM 인증서를 찾을 수 없습니다."

이 오류는 사서함 서버에서 Lync 2013 및 Outlook Web App 통합 하는데 사용 되는 인증서를 찾을 수 없는 나타냅니다. 이 인증서는 사서함 서버와 Lync 2013 서버에 설치 되어 있어야 하며 두 서버를 신뢰 해야 합니다. 인증서 요구 사항에 대 한 자세한 내용은 [Microsoft Lync Server 2013 통합 (영문) 및 Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418)에서 Outlook Web App 섹션에서 사용 하도록 설정 인스턴트 메시징을 참조 하십시오.

일치 시킬 수 있습니다가 인증서에 대 한 오류에 지문 값 **Get-ExchangeCertificate** cmdlet을 사용 하 여 또는 **서버** 에 Exchange 관리 센터 (EAC)에서 \> **인증서** 입니다.

## 오류에 대 한 복구 작업: "IM 인증서가 만료 되었습니다."

이 오류는 Lync 2013 및 Outlook Web App 통합 하는데 사용 되는 인증서가 만료를 나타냅니다. 이 오류를 해결 하려면 인증서를 갱신 해야 합니다.

일치 시킬 수 있습니다가 인증서에 대 한 오류에 지문 값 **Get-ExchangeCertificate** cmdlet을 사용 하 여 또는 **서버** 에 Exchange 관리 센터 (EAC)에서 \> **인증서** 입니다.

## 오류에 대 한 복구 작업: "IM 인증서가 유효 하 게 아직."

이 오류 Lync 2013 통합 하는데 사용 되는 인증서를 나타내고 Outlook Web App 에 잘못 된 날짜를 적용 합니다. 이 오류를 해결 하려면 새 인증서를 구성 해야 하 고 `%ExchangeInstallPath%ClientAccess\Owa\web.config` 에서 **IMCertificateThumbprint** 키의 새 지문 값을 추가 해야 합니다. 인증서 요구 사항에 대 한 자세한 내용은 [Microsoft Lync Server 2013 통합 (영문) 및 Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418)에서 Outlook Web App 섹션에서 사용 하도록 설정 인스턴트 메시징을 참조 하십시오.

## 오류에 대 한 복구 작업: "IM 인증서 개인 키가 하지 않습니다."

이 오류는 Lync 2013 및 Outlook Web App 통합 하는데 사용 되는 인증서에 개인 키 없는 나타냅니다. 이 오류를 해결 하려면 개인 키가 있는 새 인증서를 구성 해야 하 고 `%ExchangeInstallPath%ClientAccess\Owa\web.config` 에서 **IMCertificateThumbprint** 키의 새 지문 값을 추가 해야 합니다. 인증서 요구 사항에 대 한 자세한 내용은 [Microsoft Lync Server 2013 통합 (영문) 및 Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418)에서 Outlook Web App 섹션에서 사용 하도록 설정 인스턴트 메시징을 참조 하십시오.

