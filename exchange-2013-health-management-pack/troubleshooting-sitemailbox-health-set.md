---
title: 설정 SiteMailbox 상태 문제를 해결
TOCTitle: 설정 SiteMailbox 상태 문제를 해결
ms:assetid: ac00985c-c9a5-44bf-b152-4b99d8ae24ed
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.sitemailbox(v=EXCHG.150)
ms:contentKeyID: 53275594
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 설정 SiteMailbox 상태 문제를 해결

 

_**적용 대상:**Exchange Server 2013, Project Server 2013_

_**마지막으로 수정된 항목:**2013-02-11_

SiteMailbox 상태 설정은 조직 사이트 사서함의 전체 상태 및 접근성을 모니터링합니다.

SiteMailbox의 상태가 비정상임을 지정하는 경고가 표시되면 사용자 사서함의 콘텐츠가 동기화된 상태가 아닌 것입니다.

## 설명

SiteMailbox 모니터링 시스템은 백그라운드 동기화 서비스에서 수동 동기화 결과를 받습니다. 이 시스템은 프로브를 사용하지 않습니다. 수동 동기화 결과는 각 동기화 시도 후 SiteMailbox 모니터링 시스템에 기록됩니다. 다음 이벤트가 발생할 때도 동기화가 트리거됩니다.

  - 사용자가 Outlook 또는 Outlook Web App을 사용하여 사이트 사서함에 액세스할 때

  - **Update-SiteMailbox** 명령을 실행할 때

  - Outlook Web App 옵션 창을 열고 선택한 사이트 사서함에 대해 **동기화 상태** 페이지에서 **동기화 시작** 단추를 클릭할 때

Update-SiteMailbox cmdlet에 대한 자세한 내용은 다음 항목을 참조하십시오. [Update-SiteMailbox](https://technet.microsoft.com/ko-kr/library/jj218690\(v=exchg.150\))

프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 일반적인 문제

동기화 모니터링 서비스에서는 보통 사이트 전체에 걸친 동기화 문제가 발생하면 경고를 트리거합니다. 사이트 사서함 하나를 동기화하지 못한 경우에는 경고가 전송되지 않습니다. 단일 사이트 사서함에 대한 임계값 초과 경고의 원인을 확인하려면 사이트 사서함 동기화 로그 파일을 검토하는 것이 좋습니다.

## 사용자 작업

서비스가 경고를 보낸 후 복구되었을 수도 있습니다. 따라서 상태 설정이 비정상임을 지정하는 경고가 표시되면 해당 문제가 여전히 존재하는지를 먼저 확인하십시오. 문제가 있는 경우 다음 섹션에 설명된 적절한 복구 작업을 수행합니다.

## 문제가 여전히 존재하는지 확인

1.  경고의 서버 이름 및 상태 설정 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우에는 메시지 세부 정보에서 근본 원인을 파악하는 데 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보낸 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        예를 들어 server1.contoso.com에 대한 SiteMailbox 상태 설정 세부 정보를 검색하려면 다음 명령을 실행합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "SiteMailbox"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고를 보낸 모니터의 **AlertValue** 값은 `Unhealthy`입니다.

## 문제 해결 단계

상태 설정에서 경고가 표시될 때는 다음 정보가 포함된 전자 메일 메시지를 받게 됩니다.

  - 경고를 보낸 서버의 이름

  - 경고가 발생한 날짜와 시간

  - 사용된 인증 메커니즘 및 자격 증명 정보

  - 마지막 오류의 전체 예외 추적(진단 데이터 및 특정 HTTP 헤더 정보 포함)  
    
    **참고**   전체 예외 추적의 정보를 사용하여 문제를 해결할 수 있습니다. 프로브에서 생성하는 예외에는 프로브가 실패한 원인을 설명하는 실패 이유가 포함되어 있습니다.

**백그라운드 동기화 오류**

백그라운드 동기화 프로세스가 실패하면 다음과 같은 경고가 표시될 수 있습니다.

사이트 사서함 백그라운드 동기화가 25% 이상 실패합니다. 87번 시도 중 41번 실패. 샘플 동기화 결과:

\[메시지: 원격 서버에서 오류가 반환되었습니다. (401) 권한이 없음\]\[유형: System.Net.WebException\]

지난 4시간 동안 동기화 실패의 비율이 지속적으로 높은 경우 이 경고가 트리거됩니다. 가양성을 방지하기 위해 지난 4시간 동안 15분 간격 이내에 다음 조건이 충족된 경우에만 경고가 전송됩니다.

  - 15분 동안 동기화가 20회 이상 실패한 경우

  - 15분 동안 총 시도 대비 실패 비율이 25%를 초과한 경우

Exchange의 모든 사이트 사서함은 SharePoint 사이트에 연결됩니다. 사서함 역할을 호스트하는 지정된 Exchange 서버의 각 사이트 사서함에 대해 서버는 SharePoint의 사이트 사서함 관련 정보를 동기화합니다.

이 프로세스 중에는 두 가지 유형의 동기화, 즉 구성원 자격 동기화와 문서 동기화가 수행됩니다. 이러한 동기화 프로세스의 메타데이터는 서로 다른 웹 서비스에서 생성됩니다. 또한, 지정된 Exchange 서버에 여러 SharePoint 서버 또는 팜에 연결된 사이트 사서함이 포함되어 있을 수도 있습니다. 따라서 다음과 같은 조건에 따라 경고가 여러 사서함 서버에서 생성될 수도 있습니다.

1.  조직에서 활발히 사용되고 있는 사이트 사서함이 배포되는 방식

2.  활발히 사용되고 있는 사이트 사서함이 연결된 SharePoint 서버

3.  사서함 서버에 경고 임계값을 충족하는 동기화 볼륨이 충분히 포함되어 있는지 여부

이 문제를 해결하려는 경우 경고의 샘플 동기화 결과를 확인하면 오류의 원인을 파악하는 데 도움이 됩니다. 각 동기화 시도의 성공 또는 실패에 대한 세부 정보는 *\<exExchangeSvrNoVersion 설치 디렉터리\>*Logging\\TeamMailbox 폴더에 기록됩니다. 최신 Microsoft.Exchange.ServiceHost\_TeamMailboxSyncLog\* 파일에서 **failed**라는 용어로 검색하여 오류를 검토합니다. **Test-OAuthConnectivity**, **Test-SiteMailbox** 및 **Get-SiteMailboxDiagnostics** cmdlet을 사용하여 추가로 문제를 해결할 수도 있습니다.

**MSExchangeServiceHost 서비스가 실행되고 있지 않음**

MSExchangeServiceHost 서비스가 실행되고 있지 않으면 다음과 같은 경고가 표시됩니다.

복구 시도 후 'MSExchangeServiceHost' 서비스가 실행되고 있지 않습니다. 서비스가 사용하지 않도록 설정되었거나 크래시 루프 상태일 수 있습니다.

이 문제를 해결하려면 경고를 보낸 서버에서 MSExchangeServiceHost 서비스가 실행되고 있는지 확인합니다. 서비스가 실행되고 있으면 Windows 이벤트 로그에서 이전에 서비스가 실행될 수 없었던 이유(예: 수동 서비스 제어, 반복적인 서비스 작동 중단)가 있는지 검토합니다.

**MSExchangeServiceHost 서비스 작동이 중단됨**

MSExchangeServiceHost 서비스의 작동이 중단되면 다음과 같은 경고가 표시됩니다.

MSExchangeServiceHost 프로세스 작동이 지난 60분 동안 3번 이상 중단되었습니다.  
Watson 메시지:

\<*메시지*\>

이 문제를 해결하려면 경고를 보낸 서버의 Windows 응용 프로그램 이벤트 로그에서 MSExchangeServiceHost 서비스에 대한 **4999** 이벤트를 검토합니다. 세부 정보 텍스트를 통해 문제의 원인에 대한 정보를 확인할 수 있습니다.

## 자세한 내용

[Exchange 2013의 새로운 기능](https://technet.microsoft.com/ko-kr/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\))

