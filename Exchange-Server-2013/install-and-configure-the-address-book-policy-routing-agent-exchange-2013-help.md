---
title: '주소 주소록 정책 라우팅 에이전트 설치 및 구성: Exchange 2013 Help'
TOCTitle: 주소 주소록 정책 라우팅 에이전트 설치 및 구성
ms:assetid: 20e8a43d-4508-4388-a2c9-aa3073593cc2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ907308(v=EXCHG.150)
ms:contentKeyID: 51407679
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주소 주소록 정책 라우팅 에이전트 설치 및 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-01-09_

주소록 정책 라우팅 에이전트는 사서함 서버에서 실행되며 조직에서 받는 사람을 확인하는 방법을 제어하는 전송 에이전트입니다. ABP 라우팅 에이전트를 설치 및 구성하면 서로 다른 GAL에 할당된 사용자는 외부 받는 사람의 대화 상대 카드를 볼 수 없으므로 외부 받는 사람으로 표시됩니다.

ABP와 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 주소록 정책 절차](address-book-policy-procedures-exchange-2013-help.md)를 참조하십시오.

이 항목의 Exchange Online 버전은 [주소록 정책 \[Online\] 라우팅 설정](https://technet.microsoft.com/ko-kr/library/jj891095\(v=exchg.150\))을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 15분

  - ABP 라우팅 에이전트를 설치 및 구성한 후 조직의 전자 메일을 에이전트가 평가하는 데 최대 30분이 걸릴 수 있습니다.

  - EAC를 사용하여 이 절차를 수행할 수는 없으며, 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: ABP 라우팅 에이전트 설치

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 에이전트" 항목

다음 명령을 실행하여 ABP 라우팅 에이전트를 설치합니다. 정확히 아래 명령과 구문을 사용해야 합니다.

    Install-TransportAgent -Name "ABP Routing Agent" -TransportAgentFactory "Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.AddressBookPolicyRoutingAgentFactory" -AssemblyPath $env:ExchangeInstallPath\TransportRoles\agents\AddressBookPolicyRoutingAgent\Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.dll

변경 내용을 적용하려면 전송 서비스를 다시 시작해야 한다는 경고가 표시되지만, 2단계를 먼저 수행하면 전송 서비스를 한 번만 다시 시작하면 됩니다.

구문과 매개 변수에 대한 자세한 내용은 [Install-TransportAgent](https://technet.microsoft.com/ko-kr/library/aa997998\(v=exchg.150\))를 참조하십시오.

## 2단계: 전송 라우팅 에이전트 사용

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 에이전트" 항목

ABP 라우팅 에이전트를 설치한 후 다음 명령을 실행하여 에이전트를 사용하도록 설정해야 합니다.

```powershell
Enable-TransportAgent "ABP Routing Agent"
```

구문과 매개 변수에 대한 자세한 내용은 [Enable-TransportAgent](https://technet.microsoft.com/ko-kr/library/bb124921\(v=exchg.150\))를 참조하십시오.

## 3단계: 전송 서비스를 다시 시작하고 ABP 라우팅 에이전트가 설치 및 사용 설정되었는지 확인

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 에이전트" 항목

1.  다음 명령을 실행하여 전송 서비스를 다시 시작합니다.
    
    ```powershell
Restart-Service MSExchangeTransport
```

2.  서비스를 다시 시작한 후 다음 cmdlet을 실행하여 ABP 라우팅 에이전트가 설치되었으며 사용하도록 설정되었는지 확인합니다.
    
    ```powershell
Get-TransportAgent
```
    
    목록에 ABP 라우팅 에이전트가 표시되면 에이전트가 올바르게 설치된 것입니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-TransportAgent](https://technet.microsoft.com/ko-kr/library/bb123536\(v=exchg.150\))를 참조하십시오.

## 4단계: ABP 라우팅 에이전트 사용

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 구성" 항목

이 프로세스의 마지막 단계는 조직에 대해 ABP 라우팅을 사용하도록 설정하는 것입니다. 다음 명령을 실행합니다.

```powershell
Set-TransportConfig -AddressBookPolicyRoutingEnabled $true
```

구문과 매개 변수에 대한 자세한 내용은 [Set-TransportConfig](https://technet.microsoft.com/ko-kr/library/bb124151\(v=exchg.150\))를 참조하십시오.

