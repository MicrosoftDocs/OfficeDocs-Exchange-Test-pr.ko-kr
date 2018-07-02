---
title: '전송 에이전트를 관리 합니다.: Exchange 2013 Help'
TOCTitle: 전송 에이전트를 관리 합니다.
ms:assetid: f15ab7e4-015d-45b1-9c10-f733d7cd2a36
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125175(v=EXCHG.150)
ms:contentKeyID: 50484465
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전송 에이전트를 관리 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

전송 에이전트 SMTP 이벤트를 사용 하 여 전송 파이프라인을 통해 이동 하는 메시지에 따라 메시지에서 작동 하도록 합니다. Microsoft Exchange Server 2013 에 포함 된 기본 제공 전송 에이전트 대부분이 보이지 않게 하 고 관리 불가능 합니다. 그러나 설치 하 고 조직에서 Exchange 서버에서 타사 전송 에이전트를 구성할 수 있습니다. 전송 에이전트에 대 한 자세한 내용은 [전송 에이전트](transport-agents-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 에이전트" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 레거시 전송 에이전트에 대 한 지원 되지 않습니다 기본적으로 사용할 수 있지만 설정할 수 있습니다. 자세한 내용은 [레거시 전송 에이전트에 대 한 지원을 사용 하도록 설정](enable-support-for-legacy-transport-agents-exchange-2013-help.md)를 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 클라이언트 액세스 서버의 프런트엔드 전송 서비스에서 전송 에이전트 절차에 대 한

클라이언트 액세스 서버의 프런트엔드 전송 서비스에서 전송 에이전트를 관리 하려면 Exchange 관리 셸을 사용할 수 없습니다. 대신, 클라이언트 액세스 서버에서 Windows PowerShell을 열고 다음 Exchange cmdlet에는 Windows PowerShell 세션을 가져올 수 해야 합니다.


> [!WARNING]
> 프런트엔드 전송 서비스에서 전송 에이전트 관리 이외의 작업에 대 한 Windows PowerShell에서 Exchange cmdlet을 실행 하는 것은 지원 되지 않습니다. Windows PowerShell에서 Exchange cmdlet을 실행 하 여 Exchange 관리 셸 및 역할 기반 액세스 제어 rbac (역할)을 무시 하는 경우 발생할 수 있는 심각한 결과 있습니다. 항상 Exchange 관리 셸에서 Exchange cmdlet을 실행 해야 합니다. 자세한 내용은 <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange Server 2013 릴리스 정보</A>을 참조 하십시오.



프런트엔드 전송 서비스에서이 항목에서 설명 하는 전송 에이전트 절차 중 하나를 수행 하려면 다음 단계를 추가로 수행 해야 합니다.

1.  클라이언트 액세스 서버에서 Windows PowerShell을 열고 다음 명령을 실행 합니다.
    
        Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn

2.  명령을 실행 하 여 설명한 것 처럼, 명령에 다음 값을 추가 하지만: `-TransportService FrontEnd`합니다.
    
    예, 클라이언트 액세스 서버의 프런트엔드 전송 서비스에 전송 에이전트를 보려면 다음 명령을 실행 합니다.
    
        Get-TransportAgent -TransportService FrontEnd

## 셸을 사용 하 여 전송 에이전트를 설치 하려면

전송 에이전트를 설치 하는 경우 Exchange만 전송 에이전트와 관련 된 Dll을 등록 합니다. 모든 파일, 레지스트리 키 및 기타 개체를 사용 하는 전송 에이전트에 올바르게 설치 및 구성 되었는지 확인 해야 합니다. Exchange의 Dll 로드 된 후 명령이 완료 된 후에 Dll을 참조 하는 계속 실행 합니다.

전송 에이전트 자신이 발생 하는 모든 전자 메일 메시지에 전체 액세스할 수 있습니다. Exchange가 전송 에이전트의 동작에 제한이 없습니다. 안정적이 지는 또는 보안 결함을 포함 하는 전송 에이전트 안정성과 보안을 exchange에 영향을 줄 수 있습니다. 따라서 전송 에이전트를 완전히 신뢰 하 고 테스트 환경에서 완벽 하 게 테스트 된는 설치 해야 합니다.

전송 에이전트 메일 흐름 구성 하지 않은 된 전송 에이전트에 의해 영향을 받지 않습니다 있는지 확인 하는 사용할 수 없는 상태에 설치 됩니다. 따라서 전송 에이전트를 올바르게 구성 된 후 전송 에이전트를 사용 하도록 설정 해야 합니다.

전송 에이전트를 설치 하려면 다음 구문을 사용 합니다.

    Install-TransportAgent -Name <TransportAgentIdentity> -TransportAgentFactory <"TransportAgentFactory"> -AssemblyPath <"FilePath">

이 예제에서는 사서함 서버의 전송 서비스에서 전송 에이전트 Contoso 라는 가상의 전송 에이전트를 설치 합니다.

    Install-TransportAgent -Name "Contoso Transport Agent" -TransportAgentFactory "vendor.exchange.ContosoTransportAgentfactory" -AssemblyPath "C:\Program Files\Vendor\TransportAgent\ContosoTransportAgentFactory.dll"

## 작동 여부는 어떻게 확인합니까?

전송 에이전트 성공적으로 설치를 확인 하려면 `Get-TransportAgent` 명령을 실행 하 고 전송 에이전트가 나열 되는지 확인 합니다.

## 셸을 사용 하 여 전송 에이전트를 사용 하도록 설정 하려면

전송 에이전트를 사용 하도록 설정 하려면 다음 구문을 사용 합니다.

    Enable-TransportAgent <TransportAgentIdentity>

사서함 서버의 전송 서비스에서 Contoso 전송 에이전트 라는 전송 에이전트를 설정 하는이 예제입니다.

    Enable-TransportAgent "Contoso Transport Agent"

## 작동 여부는 어떻게 확인합니까?

전송 에이전트를 성공적으로 설정한 있는지를 확인 하려면 `Get-TransportAgent | Format-List Name,Enabled` 명령을 실행 하 고 전송 에이전트를 사용을 확인 합니다.

## 셸을 사용 하 여 전송 에이전트를 사용 하지 않도록 설정 하려면

전송 에이전트를 사용 하지 않도록 설정 하려면 다음 구문을 사용 하십시오.

    Disable-TransportAgent <TransportAgentIdentity>

이 예에서는 사서함 서버의 전송 서비스에서 Fabirkam 전송 에이전트 라는 전송 에이전트를 비활성화 합니다.

    Disable-TransportAgent "Fabrikam Transport Agent"

## 작동 여부는 어떻게 확인합니까?

성공적으로 전송 에이전트를 사용 하지 않도록 한를 확인 하려면 `Get-TransportAgent | Format-List Name,Enabled` 명령을 실행 하 고 전송 에이전트 사용 되지 않는지 확인 합니다.

## 셸을 사용 하 여 전송 에이전트를 볼 수

전송 에이전트의 요약 목록을 보려면 다음 명령을 실행 합니다.

    Get-TransportAgent

특정 전송 에이전트의 자세한 구성을 보려면 다음 명령을 실행 합니다.

    Get-TransportAgent <TransportAgentIdentity> | Format-List

이 예에서는 전송 규칙 에이전트 라는 전송 에이전트의 자세한 구성을 제공 합니다.

    Get-TransportAgent "Transport Rule Agent" | Format-List

## 셸을 사용 하 여 전송 에이전트의 우선순위를 구성 하려면

먼저 0 프로세스 전자 메일 메시지에 가장 가까운 우선순위로 에이전트를 전송 합니다. 그러나 SMTP 이벤트 전송 에이전트가 등록 되어 있는 전송 파이프라인에 더 높은 우선순위 에이전트 만료 되기 전에 메시지에서 작업을 수행할 수는 더 낮은 우선순위 에이전트를 일으킬 수 있습니다.

기존 전송 에이전트의 우선순위를 수정 하려면 다음 명령을 실행 합니다.

    Set-TransportAgent <TransportAgentIdentity> -Priority <Integer>

사서함 서버의 전송 서비스에서 Contoso 전송 에이전트 라는 기존 전송 에이전트에 대 한 3의 우선순위 에이전트 값을 설정 하는이 예제입니다.

    Set-TransportAgent "Contoso Transport Agent" -Priority 3

## 작동 여부는 어떻게 확인합니까?

전송 에이전트의 우선순위를 성공적으로 구성 했는지를 확인 하려면 `Get-TransportAgent | Format-List Name,Priority` 명령을 실행 하 고 전송 에이전트의 우선순위 값을 확인 합니다.

## 셸을 사용 하 여 전송 에이전트를 제거 하려면

전송 에이전트를 제거 하는 경우 Exchange는 에이전트와 함께 사용 되는 DLL 파일의 등록을 취소 합니다. Exchange 모든 파일, 레지스트리 키 또는 전송 에이전트를 설치 하 여 추가 된 다른 개체를 제거 하지 않습니다.

전송 에이전트를 제거 하려면 다음 명령을 실행 합니다.

    Uninstall-TransportAgent <TransportAgentIdentity>

이 예에서는 사서함 서버의 전송 서비스에서 Fabrikam 전송 에이전트 라는 전송 에이전트를 제거 합니다.

    Uninstall-TransportAgent "Fabrikam Transport Agent"

## 작동 여부는 어떻게 확인합니까?

전송 에이전트를 성공적으로 제거 했는지를 확인 하려면 `Get-TransportAgent` 명령을 실행 하 고 전송 에이전트 목록에 표시 되지 확인 합니다.

