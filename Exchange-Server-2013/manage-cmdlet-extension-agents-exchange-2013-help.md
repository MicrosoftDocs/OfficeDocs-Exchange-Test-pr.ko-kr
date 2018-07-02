---
title: 'Cmdlet 확장 에이전트를 관리 합니다.: Exchange 2013 Help'
TOCTitle: Cmdlet 확장 에이전트를 관리 합니다.
ms:assetid: 9141b3cb-ad13-4415-be2f-aa89f91445f5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298143(v=EXCHG.150)
ms:contentKeyID: 50556037
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cmdlet 확장 에이전트를 관리 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-19_

이 항목에서는 Microsoft Exchange Server 2013에서 cmdlet 확장 에이전트를 사용하거나 사용하지 않도록 설정하고, 보고, 우선 순위를 변경하는 방법을 보여 줍니다. Exchange 2013의 cmdlet 확장 에이전트에 대한 자세한 내용은 [cmdlet 확장 에이전트](cmdlet-extension-agents-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "cmdlet 확장 에이전트" 항목

  - `Scripting Agent`를 사용하도록 설정하기 전에 올바르게 구성되어 있는지 확인해야 합니다. `Scripting Agent`에 대한 자세한 내용은 [cmdlet 확장 에이전트](cmdlet-extension-agents-exchange-2013-help.md)를 참조하십시오.

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## cmdlet 확장 에이전트를 사용하도록 설정

Exchange 2013에서 cmdlet 확장 에이전트를 사용하도록 설정하면 Exchange 2013을 실행하는 조직 내의 모든 서버에서 에이전트가 실행됩니다. 에이전트를 사용하도록 설정하면 cmdlet에서 해당 에이전트를 사용할 수 있으며, 에이전트를 사용하여 추가 작업을 수행할 수 있습니다.


> [!WARNING]
> 에이전트를 사용하도록 설정하기 전에 에이전트 작동 방식과 에이전트가 조직에 미치게 될 영향을 알고 있어야 합니다.



이 예에서는 **Enable-CmdletExtensionAgent** cmdlet을 사용하여 cmdlet 확장 에이전트를 사용하도록 설정합니다. Cmdlet을 실행할 때 사용하도록 설정할 에이전트의 이름을 지정해야 합니다. `Scripting Agent`를 사용하도록 설정하기 전에 `ScriptingAgentConfig.xml` 구성 파일을 조직의 모든 서버에 배포했는지 확인해야 합니다. 먼저 구성 파일을 배포하지 않고 `Scripting``Agent`를 사용하도록 설정하면 모든 비 **Get** cmdlet은 실행 시 실패합니다. 이 예에서는 `Scripting Agent`를 사용하도록 설정합니다.

    Enable-CmdletExtensionAgent "Scripting Agent"

구문과 매개 변수에 대한 자세한 내용은 [Enable-CmdletExtensionAgent](https://technet.microsoft.com/ko-kr/library/dd335192\(v=exchg.150\))를 참조하십시오.

## cmdlet 확장 에이전트를 사용하지 않도록 설정

Exchange 2013에서 cmdlet 확장 에이전트를 사용하지 않도록 설정하면 Exchange 2013을 실행하는 조직 내의 모든 서버에서 에이전트가 사용되지 않습니다. 사용하지 않도록 설정된 에이전트는 cmdlet에서 사용할 수 없습니다. cmdlet은 더 이상 에이전트를 사용하여 추가 작업을 수행할 수 없습니다.


> [!WARNING]
> 에이전트를 사용하지 않도록 설정하기 전에 에이전트 작동 방식과 에이전트를 사용하지 않도록 설정하는 것이 조직에 미치는 영향을 알고 있어야 합니다.



cmdlet 확장 에이전트를 사용하지 않도록 설정하려면 **Disable-CmdletExtensionAgent** cmdlet을 사용합니다. cmdlet을 실행할 때 사용하지 않도록 설정하려는 에이전트의 이름을 지정합니다. 이 예에서는 `Scripting Agent`를 사용하지 않도록 설정합니다.

    Disable-CmdletExtensionAgent "Scripting Agent"

구문과 매개 변수에 대한 자세한 내용은 [Disable-CmdletExtensionAgent](https://technet.microsoft.com/ko-kr/library/dd298132\(v=exchg.150\))를 참조하십시오.

## 기존 cmdlet 확장 에이전트 보기

cmdlet 확장 에이전트를 보면 첫 번째로 실행되는 에이전트와 Exchange 2013 조직에서 사용하도록 설정된 에이전트를 확인할 수 있습니다. **Format-Table** cmdlet과 파이프라이닝에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))

  - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)

이 예에서는 **Get-CmdletExtensionAgent** cmdlet을 사용하여 특정 cmdlet 확장 에이전트의 세부 정보를 가져옵니다. 이 예에서는 `Mailbox Permissions Agent`의 세부 정보가 반환됩니다.

    Get-CmdletExtensionAgent "Mailbox Permissions Agent"

이 예에서는 **Get-CmdletExtensionAgent** cmdlet을 사용하여 여러 cmdlet 확장 에이전트를 가져온 다음 출력을 **Format-Table** cmdlet에 파이프합니다. 이 예에서는 조직의 모든 cmdlet 확장 에이전트 목록을 표시하며, **Format-Table** cmdlet을 사용하면 각 에이전트의 **Name**, **Enabled** 및 **Priority** 속성이 테이블에 표시됩니다.

    Get-CmdletExtensionAgent | Format-Table Name, Enabled, Priority

구문과 매개 변수에 대한 자세한 내용은 [Get-CmdletExtensionAgent](https://technet.microsoft.com/ko-kr/library/dd297946\(v=exchg.150\))를 참조하십시오.

## cmdlet 확장 에이전트의 우선 순위 변경

Exchange 2013에서 cmdlet 확장 에이전트의 우선 순위를 변경하는 기능은 cmdlet에서 특정 에이전트를 다른 에이전트보다 먼저 호출하려는 경우에 유용합니다. 이 기능은 특히 `Scripting Agent`에서 실행되는 사용자 지정 스크립트를 만들고 해당 스크립트가 기본 제공 에이전트보다 우선하도록 하려는 경우에 유용합니다. `Scripting Agent`에 대한 자세한 내용은 [cmdlet 확장 에이전트](cmdlet-extension-agents-exchange-2013-help.md)를 참조하십시오.


> [!WARNING]
> 기본 제공 에이전트의 우선 순위를 변경하거나 기능을 바꾸는 것은 고급 작업입니다. 변경 내용을 완전히 이해해야 합니다.



0부터 최대 에이전트 수까지 에이전트에 순서가 지정됩니다. 에이전트가 0에 가까울수록 에이전트의 우선 순위가 더 높습니다. 우선 순위가 높은 에이전트가 먼저 호출됩니다. 에이전트 우선 순위에 대한 자세한 내용은 [cmdlet 확장 에이전트](cmdlet-extension-agents-exchange-2013-help.md)를 참조하십시오.

이 예에서는 **Set-CmdletExtensionAgent** cmdlet을 사용하여 cmdlet 확장 에이전트의 우선 순위를 변경합니다. 이 예에서 `Scripting Agent`의 우선 순위는 3으로 변경됩니다.

    Set-CmdletExtensionAgent "Scripting Agent" -Priority 3

구문과 매개 변수에 대한 자세한 내용은 [Set-CmdletExtensionAgent](https://technet.microsoft.com/ko-kr/library/dd335175\(v=exchg.150\))를 참조하십시오.

