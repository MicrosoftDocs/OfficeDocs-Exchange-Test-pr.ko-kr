---
title: '엔진 및 정의 업데이트 다운로드: Exchange 2013 Help'
TOCTitle: 엔진 및 정의 업데이트 다운로드
ms:assetid: 8f2ca383-e463-4df0-aa5d-29afe2f81aaf
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657471(v=EXCHG.150)
ms:contentKeyID: 50483655
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 엔진 및 정의 업데이트 다운로드

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

Microsoft 맬웨어 방지 엔진 및 정의 (서명) 업데이트에 수동으로 Exchange Server 2013 관리자 다운로드할 수 있습니다. 프로덕션에 배치 하기 전에 Exchange 서버에 엔진 및 정의 업데이트를 다운로드 하는 것이 좋습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이 절차는 셸을 사용해야 수행할 수 있습니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요.

  - 업데이트를 다운로드 하려면 사용자의 컴퓨터에서 인터넷에 액세스 하 여 TCP 포트 80 (HTTP)에 대 한 연결을 설정할 수 있어야 합니다. 인터넷 액세스를 위한 프록시 서버를 사용 하는 조직, 하는 경우이 항목의 맬웨어 방지 업데이트에 대 한 프록시 서버 설정을 구성 하려면 셸 사용 하 여 섹션을 참조 하십시오.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "맬웨어 방지? [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) 의 항목입니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 수동으로 엔진 및 정의 업데이트 다운로드

엔진 및 정의 업데이트를 다운로드하려면 다음 명령을 실행합니다.

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity <FQDN of server>

이 예제에서는 mailbox01.contoso.com 라는 Exchange 서버에 엔진 및 정의 업데이트를 수동으로 다운로드 합니다.

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com

필요에 따라 `http://forefrontdl.microsoft.com/server/scanengineupdate`의 기본 위치가 아닌 다른 곳에서 업데이트를 다운로드 하려면 *EngineUpdatePath* 매개 변수를 사용할 수 있습니다. 대체 HTTP 주소 또는 UNC 경로 지정 하려면이 매개 변수를 사용할 수 있습니다. UNC 경로 지정 하는 경우 네트워크 서비스에는 경로에 대 한 액세스를 권한이 있어야 합니다.

이 예제에서는 `\\FileServer01\Data\MalwareUpdates`의 UNC 경로 mailbox01.contoso.com 라는 Exchange 서버에 엔진 및 정의 업데이트를 수동으로 다운로드 합니다.

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com -EngineUpdatePath \\FileServer01\Data\MalwareUpdates

## 작동 여부는 어떻게 확인합니까?

업데이트가 성공적으로 다운로드되었는지 확인하려면 이벤트 뷰어에 액세스하여 이벤트 로그를 확인해야 합니다. 다음 절차에 설명된 대로 FIPFS 이벤트만 필터링하는 것이 좋습니다.

1.  **시작** 메뉴에서 **모든 프로그램** \> **관리 도구** \> **이벤트 뷰어**를 클릭합니다.

2.  이벤트 뷰어에서 **Windows 로그** 폴더를 확장하고 **응용 프로그램**을 클릭합니다.

3.  **작업** 메뉴에서 **현재 로그 필터링**을 클릭합니다.

4.  **현재 로그 필터링** 대화 상자의 **이벤트 원본** 드롭다운 목록에서 **FIPFS** 확인란을 선택하고 **확인**을 클릭합니다.

엔진 업데이트가 성공적으로 다운로드된 경우 다음과 유사한 이벤트 ID 6033이 나타납니다.

`MS Filtering Engine Update process performed a successful scan engine update.`

`Scan Engine: Microsoft`

`Update Path: http://forefrontdl.microsoft.com/server/scanengineupdate`

`Last Update time: ‎2012‎-‎08‎-‎16T13:22:17.000Z`

`Engine Version: 1.1.8601.0`

`Signature Version: 1.131.2169.0`

## 셸을 사용 하 여 맬웨어 방지 업데이트에 대 한 프록시 서버 설정을 구성 하려면

프록시 서버를 사용 하 여 인터넷에 대 한 액세스를 제어 하는 조직, 맬웨어 방지 엔진 및 정의 업데이트를 성공적으로 다운로드할 수 있도록 프록시 서버를 식별 해야 합니다. **Netsh.exe** 도구, Internet Explorer 연결 설정과 *InternetWebProxy* 매개 변수를 사용 하 여 **Set-ExchangeServer** cmdlet에서 사용할 수 있는 프록시 서버 설정을 맬웨어 방지 업데이트를 다운로드 하는 방법에 영향을 하지 않습니다.

맬웨어 방지 업데이트에 대 한 프록시 서버 설정을 구성 하려면 다음 단계를 수행 합니다.

1.  다음 명령을 실행합니다.
    
    ```powershell
Add-PsSnapin Microsoft.Forefront.Filtering.Management.Powershell
```

2.  **Get-ProxySettings** 및 **Set-ProxySettings** cmdlet을 사용 하 여 보기 및 맬웨어 방지 업데이트를 다운로드 하는데 사용 되는 프록시 서버 설정을 구성 합니다. **Set-ProxySettings** cmdlet에는 다음 구문을 사용합니다.
    
        Set-ProxySettings -Enabled <$true | $false> -Server <Name or IP address of proxy server> -Port <TCP port of proxy server>
    
    예, TCP 포트 80에서 172.17.17.10 주소에 프록시 서버를 사용 하 여 맬웨어 방지 업데이트를 구성 하려면 다음 명령을 실행 합니다.
    
    ```powershell
Set-ProxySettings -Enabled $true -Server 172.17.17.10 -Port 80
```
    
    프록시 서버 설정을 확인 하려면 **Get-ProxySettings** cmdlet을 실행 합니다.

## 자세한 내용

[맬웨어 방지 정책 구성](configure-anti-malware-policies-exchange-2013-help.md)

