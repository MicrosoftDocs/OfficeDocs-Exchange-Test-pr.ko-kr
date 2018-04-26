---
title: 문제 해결을 위해 Exchange Server 2013 관리 팩 사용
TOCTitle: 문제 해결을 위해 Exchange Server 2013 관리 팩 사용
ms:assetid: c9672dad-1e67-4f07-bad9-539a67f2ac70
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn195913(v=EXCHG.150)
ms:contentKeyID: 53275606
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 문제 해결을 위해 Exchange Server 2013 관리 팩 사용

 

_**마지막으로 수정된 항목:** 2013-04-09_

[Exchange Server 2013 관리 팩 시작](getting-started-with-exchange-server-2013-management-pack.md)에서는 관리 팩 대시보드에 대해 간략하게 설명하고, 관리 팩 대시보드를 통해 문제를 해결하는 과정을 안내합니다. 예를 통해 이 프로세스를 적절하게 설명합니다. 즉, 다음과 같은 상황에서 오류가 발생할 수 있습니다.

Contoso의 Exchange 관리자인 Rob Fielder가 SCOM 콘솔을 열고 Exchange Server 2013 대시보드에서 **서버 상태**를 클릭하여 Exchange 서버의 상태를 확인합니다. 이 과정에서 CAS 서버 중 하나의 **서비스 구성 요소**가 위험 상태임이 확인됩니다.

![실패한 CAS 서버](images/Dn195913.32a265d9-68e0-4d8c-9f83-1d10cdda1f84(EXCHG.150).png "실패한 CAS 서버")

Rob은 서버를 두 번 클릭하여 **상태 탐색기** 창을 엽니다. 이 창에서 비정상 상태인 서비스 구성 요소가 OWA.Proxy 상태 설정임을 확인하여 해당 상태 설정을 클릭하여 관련 정보를 확인합니다.

![실패한 CAS 서버 상태 설정 정보](images/Dn195913.8e4d05a6-9128-40d8-b262-e60e9affc973(EXCHG.150).png "실패한 CAS 서버 상태 설정 정보")

외부 기술 자료 아래의 링크를 클릭하여 [OWA.Proxy 상태 설정 문제 해결](https://technet.microsoft.com/ko-kr/library/jj737712\(v=exchg.150\)) 항목으로 이동합니다. 이 문서에는 우선 문제가 아직 존재하는지를 확인하라는 지침이 나와 있습니다. 이 지침에 따라 Rob은 다음 명령을 실행하여 셸에서 OWA.Proxy 상태 설정의 현재 상태를 확인합니다.

    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}

이 명령을 실행하면 다음 출력이 표시됩니다.

    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Unhealthy  OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy

이 출력을 통해 OWA 응용 프로그램에 문제가 있음을 확인할 수 있습니다. 다음 단계로 비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. Rob은 "OWA.Proxy 상태 설정 문제 해결" 항목의 표를 참조하여 다시 실행해야 하는 프로브가 OWAProxyTestProbe임을 확인하고 다음 명령을 실행합니다.

    Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server Server1.contoso.com | Format-List

Rob은 출력을 검사해 ResultType 값을 찾아서 프로브에 오류가 발생했음을 확인합니다.

    ResultType : Failed

Rob은 해당 문서의 "OWAProxyTestMonitor 복구 작업"을 계속 진행합니다. 이를 위해 IIS 관리자를 사용해 서버1에 연결하여 IIS 서버에서 MSExchangeOWAAppPool이 실행되고 있는지를 확인합니다. 실행되고 있음을 확인하면, 다음 단계 지침에 따라 MSExchangeOWAAppPool을 재순환합니다.

    C:\Windows\System32\Inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool

MSExchangeOWAAppPool이 재순환되었음을 확인한 후 Rob은 Invoke-MonitoringProbe cmdlet을 사용해 프로브를 다시 실행하여 문제가 계속 존재하는지를 다시 확인합니다. 이번에는 결과가 성공으로 확인됩니다. 다음으로 Rob은 다음 명령을 실행하여 상태 설정이 **정상** 상태를 보고하는지 다시 확인합니다.

    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}

이제 문제가 해결되었음을 확인할 수 있습니다.

    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Healthy    OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy

Rob은 SCOM 콘솔로 돌아가 문제가 해결되었음을 확인합니다.

![서버 상태](images/Dn195908.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "서버 상태")

위에서 다룬 시나리오는 SCOM 콘솔에서 경고가 표시될 때의 문제 해결 워크플로를 간략하게 보여줍니다. 실제 작업 시 세부 사항은 달라지지만, 콘솔에서 보고되는 각 문제에 대해 일반적으로는 이와 비슷한 문제 해결 워크플로를 따릅니다.

