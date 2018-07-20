---
title: 'cmdlet 확장 에이전트: Exchange 2013 Help'
TOCTitle: cmdlet 확장 에이전트
ms:assetid: 0257790d-3988-46c3-8882-25ca11559e84
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335054(v=EXCHG.150)
ms:contentKeyID: 50555930
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# cmdlet 확장 에이전트

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

cmdlet 확장 에이전트는 cmdlet을 실행할 때 Exchange Server 2013 cmdlet에서 호출하는 Microsoft Exchange 2013의 구성 요소입니다. 이름에서 알 수 있듯이, cmdlet 확장 에이전트는 데이터 처리를 지원하거나 cmdlet의 요구 사항에 따라 추가 작업을 수행하여 자신을 호출하는 cmdlet의 기능을 확장합니다. cmdlet 확장 에이전트는 모든 서버 역할에서 사용할 수 있습니다.

에이전트는 Exchange 관리 셸 cmdlet의 기능을 수정하거나 바꾸거나 확장할 수 있습니다. 이외에도 에이전트는 명령에 제공되지 않은 필수 매개 변수의 값을 제공하고, 사용자가 제공한 값을 재정의하고, cmdlet이 실행되는 동안 cmdlet 워크플로 외부의 다른 작업을 수행할 수 있습니다.

예를 들어 **New-Mailbox** cmdlet은 새 사서함을 만들 사서함 데이터베이스를 지정하는 *Database* 매개 변수를 사용합니다. Microsoft Exchange Server 2007에서는 **New-Mailbox** cmdlet을 실행할 때 *Database* 매개 변수를 지정하지 않을 경우 명령이 실패합니다. 그러나 Exchange 2013에서는 **New-Mailbox** cmdlet이 실행 시 `Mailbox Resources Management` 에이전트를 호출합니다. *Database* 매개 변수를 지정하지 않으면 `Mailbox Resources Management` 에이전트가 새 사서함을 만들 적절한 사서함 데이터베이스를 자동으로 확인하여 해당 값을 *Database* 매개 변수에 삽입합니다.

cmdlet 확장 에이전트는 Exchange 2013 및 Microsoft Exchange Server 2010 cmdlet을 통해서만 호출할 수 있습니다. Exchange 2007 cmdlet과 다른 Microsoft 제품 및 타사 제품에서 제공하는 cmdlet은 cmdlet 확장 에이전트를 호출할 수 없습니다. 스크립트도 cmdlet 확장 에이전트를 직접 호출할 수 없습니다. 그러나 스크립트에 Exchange 2013 cmdlet이 포함되어 있는 경우 해당 cmdlet은 계속해서 cmdlet 확장 에이전트를 호출합니다.

cmdlet 확장 에이전트와 관련된 관리 작업에 대한 자세한 내용은 [Cmdlet 확장 에이전트를 관리 합니다.](manage-cmdlet-extension-agents-exchange-2013-help.md) 항목을 참조하십시오.

## 에이전트 우선 순위

에이전트 우선 순위는 cmdlet이 실행되는 동안 에이전트가 호출되는 순서를 결정합니다. 우선 순위가 더 높고 0에 더 가까운 에이전트가 먼저 호출됩니다. 에이전트 우선 순위는 둘 이상의 에이전트가 동일한 속성의 값을 설정하려고 하는 경우에 중요합니다. 속성 값을 설정하려고 하는 에이전트 중 우선 순위가 가장 높은 에이전트만 성공하고 우선 순위가 더 낮은 에이전트가 이후에 동일한 속성을 설정하려고 하면 모두 무시됩니다. 예를 들어 우선 순위가 3인 에이전트가 개체의 **Name** 속성을 수정하고 우선 순위가 6인 다른 에이전트가 동일한 개체를 수정하는 경우 우선 순위가 6인 에이전트의 수정 내용은 무시됩니다.

`Scripting agent`를 사용하여 우선 순위가 더 높은 다른 에이전트가 설정했을 수 있는 속성의 값을 설정하려는 경우 다음 옵션을 사용할 수 있습니다.

  - 현재 속성을 설정하는 에이전트를 사용하지 않도록 설정합니다.

  - `Scripting agent`를 바꾸려는 기존 에이전트보다 높은 우선 순위로 설정합니다.

  - 에이전트 우선 순위를 동일하게 유지하고 `Scripting agent`에서 실행되는 스크립트가 다른 에이전트에서 제공한 값을 사용하도록 합니다.


> [!WARNING]
> 기본 제공 에이전트의 우선 순위를 변경하거나 기능을 바꾸는 것은 고급 작업입니다. 변경 내용을 완전히 이해해야 합니다.



에이전트 우선 순위를 변경하는 방법에 대한 자세한 내용은 [Cmdlet 확장 에이전트를 관리 합니다.](manage-cmdlet-extension-agents-exchange-2013-help.md)을 참조하십시오.

## 기본 제공 에이전트

Exchange 2013에는 cmdlet을 실행할 때 호출될 수 있는 여러 에이전트가 포함되어 있습니다. 다음 표에서는 에이전트, 에이전트 순서 및 에이전트가 기본적으로 사용하도록 설정되는지 여부를 보여 줍니다. Exchange 2013을 실행하는 서버에서는 에이전트를 추가하거나 제거할 수 없습니다. 그러나 `Scripting agent`를 사용하여 Windows PowerShell 스크립트를 실행하면 해당 에이전트를 사용하는 cmdlet의 기능을 확장할 수 있습니다. `Scripting agent`에 대한 자세한 내용은 이 항목 뒷부분의 "스크립팅 에이전트" 섹션을 참조하십시오.

특정 에이전트의 기능을 `Scripting agent`로 호출하는 사용자 지정 스크립트에 제공한 기능으로 바꾸려는 경우 대부분의 에이전트를 사용 또는 사용하지 않도록 설정하거나 에이전트 우선 순위를 변경할 수 있습니다. 그러나 일부 에이전트는 사용하지 않도록 설정할 수 없습니다. 사용하지 않도록 설정할 수 없는 에이전트를 *시스템 에이전트*라고 하며 해당 *IsSystem* 속성은 `$True`로 설정되어 있습니다. 다음 표에서는 시스템 에이전트를 포함하여 Exchange 2013 cmdlet 확장 에이전트에 대한 정보를 제공합니다.

에이전트 구성은 조직 수준에 저장됩니다. 에이전트를 사용 또는 사용하지 않도록 설정하거나 에이전트 우선 순위를 설정하면 조직의 모든 서버에서 에이전트 구성이 설정됩니다. 단, `Scripting agent`에 스크립트를 추가하는 경우는 예외입니다. 각 서버에서 스크립트를 개별적으로 업데이트해야 합니다. `Scripting agent`에서 사용할 스크립트를 구성하는 방법에 대한 자세한 내용은 이 항목 뒷부분의 "스크립팅 에이전트" 섹션을 참조하십시오.


> [!WARNING]
> 각 에이전트의 기능 및 Exchange cmdlet과의 상호 작용 방식을 완전히 이해하지 못한 경우 에이전트 우선 순위를 변경하거나 에이전트를 사용 또는 사용하지 않도록 설정하면 의도하지 않은 결과가 발생할 수 있습니다. 에이전트 구성을 변경하기 전에 원하는 변경 내용 및 결과를 완전히 이해하고 사용자 지정 스크립트가 의도한 대로 작동하는지 확인해야 합니다.



### Exchange 2013 cmdlet 확장 에이전트

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>에이전트 이름</th>
<th>우선 순위</th>
<th>기본적으로 사용</th>
<th>시스템 에이전트</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Admin Audit Log agent</code></p></td>
<td><p>255</p></td>
<td><p>True</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p><code>Scripting agent</code></p></td>
<td><p>6</p></td>
<td><p>False</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Resources Management agent</code></p></td>
<td><p>5</p></td>
<td><p>True</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p><code>OAB Resources Management agent</code></p></td>
<td><p>4</p></td>
<td><p>True</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p><code>Query Base DN agent</code></p></td>
<td><p>3</p></td>
<td><p>True</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p><code>Provisioning Policy agent</code></p></td>
<td><p>2</p></td>
<td><p>True</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p><code>Rus agent</code></p></td>
<td><p>1</p></td>
<td><p>True</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Creation Time agent</code></p></td>
<td><p>0</p></td>
<td><p>True</p></td>
<td><p>아니요</p></td>
</tr>
</tbody>
</table>


## 스크립팅 에이전트

Exchange 2013의 `Scripting agent` cmdlet 확장 에이전트를 사용하여 고유한 스크립팅 논리를 Exchange cmdlet의 실행에 삽입할 수 있습니다. `Scripting agent`를 사용하면 조건을 추가하고 값을 재정의하고 보고를 설정할 수 있습니다.


> [!WARNING]
> <CODE>Scripting agent</CODE> cmdlet 확장 에이전트를 사용하도록 설정하면 Exchange 2013을 실행하는 서버에서 cmdlet이 실행될 때마다 이 에이전트가 호출됩니다. 이러한 cmdlet에는 Exchange 관리 셸에서 직접 실행하는 cmdlet뿐만 아니라 Exchange 서비스 및 EAC(Exchange 관리 센터)에서 실행되는 cmdlet도 포함됩니다. 업데이트된 구성 파일을 Exchange 2013 서버로 복사하고 <CODE>Scripting agent</CODE> cmdlet 확장 에이전트를 사용하도록 설정하기 전에 스크립트를 비롯하여 구성 파일에 대한 변경 사항을 반드시 테스트하는 것이 좋습니다.



Exchange cmdlet이 실행될 때마다 cmdlet은 `Scripting agent` cmdlet 확장 에이전트를 호출합니다. 이 에이전트가 호출되면 cmdlet은 스크립트가 cmdlet에 의해 호출되도록 구성되었는지 여부를 확인합니다. cmdlet에 대한 스크립트를 실행해야 하는 경우 cmdlet은 스크립트에 정의된 API를 호출하려 합니다. 사용 가능한 다음 API가 다음 순서대로 호출됩니다.

1.  **ProvisionDefaultProperties**   이 API는 개체를 만들 때 속성 값을 설정하는 데 사용할 수 있습니다. 값을 설정하면 해당 값이 cmdlet으로 반환되며 cmdlet은 해당 속성에 값을 설정합니다. 사용자가 값을 지정하지 않은 경우 속성에 값을 채울 수도 있고 사용자가 지정한 값을 재정의할 수도 있습니다. 이 API는 우선 순위가 더 높은 에이전트가 설정한 값을 사용합니다. `Scripting agent` cmdlet 확장 에이전트는 우선 순위가 더 높은 에이전트가 설정한 값을 덮어쓰지 않습니다.

2.  **UpdateAffectedIConfigurable**   이 API는 다른 모든 처리가 완료되었지만 `Validate` API가 아직 호출되지 않은 경우 개체에 대한 속성 값을 설정하는 데 사용할 수 있습니다. 이 API는 우선 순위가 더 높은 에이전트가 설정한 값을 사용합니다. `Scripting agent` cmdlet 확장 에이전트는 우선 순위가 더 높은 에이전트가 설정한 값을 덮어쓰지 않습니다.

3.  **Validate**   이 API는 cmdlet에 의해 설정될 개체의 속성에 대한 값을 확인하는 데 사용할 수 있습니다. 이 API는 cmdlet이 데이터를 작성하기 직전에 호출됩니다. cmdlet의 성공 또는 실패를 결정하는 유효성 검사를 구성할 수 있습니다. cmdlet이 이 API에서 유효성 검사를 통과하면 cmdlet은 데이터를 쓸 수 있게 됩니다. cmdlet이 유효성 검사에서 탈락하면 이 API에 정의된 오류가 반환됩니다.

4.  **OnComplete**   이 API는 모든 cmdlet 처리가 완료된 후에 사용됩니다. 이는 외부 데이터베이스에 데이터 쓰기와 같은 후처리 작업에 사용할 수 있습니다.


> [!NOTE]
> <CODE>Get</CODE> 동사를 포함한 cmdlet이 실행되는 경우에는 <CODE>Scripting agent</CODE> cmdlet 확장 에이전트가 호출되지 않습니다.



## 스크립팅 에이전트 구성 파일

`Scripting agent` 구성 파일에는 `Scripting agent`가 실행하도록 하려는 모든 스크립트가 포함됩니다. 구성 파일의 스크립트는 데이터를 스크립트에 전달하는 데 필요한 다양한 입력 매개 변수 및 스크립트의 시작과 끝을 정의하는 XML 태그 안에 포함되어 있습니다. 스크립트는 Windows PowerShell 구문을 사용하여 작성됩니다. 구성 파일은 다음 표에 나오는 요소 또는 특성을 사용하는 XML 파일입니다.

### 스크립팅 에이전트 구성 파일의 특성

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>요소</th>
<th>특성</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Configuration</code></p></td>
<td><p>해당 없음</p></td>
<td><p>이 요소는 <code>Scripting agent</code> cmdlet 확장 에이전트가 실행할 수 있는 모든 스크립트를 포함합니다. <code>Feature</code> 태그는 이 태그의 하위 태그입니다.</p>
<p>구성 파일당 <code>Configuration</code> 태그는 하나만 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Feature</code></p></td>
<td><p>해당 없음</p></td>
<td><p>이 요소는 기능과 관련된 스크립트 집합을 포함합니다. <code>ApiCall</code> 하위 태그에 정의된 각 스크립트는 cmdlet 실행 파이프라인의 특정 부분을 확장합니다. 이 태그에는 <code>Name</code> 및 <code>Cmdlets</code> 특성이 포함됩니다.</p>
<p><code>Feature</code> 태그 하에 여러 <code>Configuration</code> 태그가 있을 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>이 특성은 기능의 이름을 포함합니다. 이 특성을 사용하면 태그에 포함된 스크립트에 의해 확장되는 기능을 식별할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Cmdlets</code></p></td>
<td><p>이 특성에는 이 기능 확장에 포함된 스크립트 집합에서 사용되는 Exchange cmdlet의 목록이 포함됩니다. 각 cmdlet을 쉼표로 분리하여 여러 개의 cmdlet을 지정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>ApiCall</code></p></td>
<td><p>해당 없음</p></td>
<td><p>이 요소는 cmdlet 실행 파이프라인의 일부를 확장할 수 있는 스크립트를 포함합니다. 각 스크립트가 확장하는 cmdlet 실행 파이프라인에 포함된 API 호출 이름에 따라 스크립트가 정의됩니다. 다음은 확장 가능한 API 이름입니다.</p>
<ul>
<li><p><code>ProvisionDefaultProperties</code></p></li>
<li><p><code>UpdateAffectedIConfigurable</code></p></li>
<li><p><code>Validate</code></p></li>
<li><p><code>OnComplete</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>이 특성은 cmdlet 실행 파이프라인을 확장하는 API 호출의 이름을 포함합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Common</code></p></td>
<td><p>해당 없음</p></td>
<td><p>이 요소는 구성 파일의 스크립트에서 사용할 수 있는 기능을 포함합니다.</p></td>
</tr>
</tbody>
</table>


모든 Exchange 2013 서버의 \<*installation path*\>\\V15\\Bin\\CmdletExtensionAgents 폴더에는 ScriptingAgentConfig.xml.sample 파일이 포함됩니다. Scripting Agent cmdlet 확장 에이전트를 사용하도록 설정하는 경우에는 모든 Exchange 2013 서버에서 이 파일의 이름을 ScriptingAgentConfig.xml로 변경해야 합니다. 예제 구성 파일에는 구성 파일에 스크립트를 추가하는 방법을 이해하는 데 도움이 되는 예제 스크립트가 들어 있습니다.

스크립트를 구성 파일에 추가한 후 또는 구성 파일을 변경한 경우에는 조직의 모든 Exchange 2013 서버에서 파일을 업데이트해야 합니다. 이는 각 서버가 `Scripting Agent` cmdlet 확장 에이전트가 실행하는 스크립트의 최신 버전을 포함하도록 하기 위해서입니다.

스크립트에 기본적으로 사용되는 일부 문자가 XML에서는 특별한 의미를 갖기도 합니다. 이러한 문자를 스크립트에 사용하려면 이스케이프 시퀀스를 사용하십시오. 예를 들어, 다음 문자는 이스케이프 시퀀스를 사용합니다.

  - 보다 큼 기호( `>` ) 대신 `&gt;` 사용

  - 보다 작음 기호( `<` ) 대신 `$lt;` 사용

  - 앰퍼샌드( `&` ) 대신 `&amp;` 사용

## 스크립팅 에이전트를 사용하도록 설정

`Scripting agent` cmdlet 확장 에이전트는 기본적으로 사용되지 않도록 설정되어 있습니다. `Scripting agent`를 사용하도록 설정하면 전체 Exchange 2013 조직에 대해 이 에이전트가 사용됩니다. `Scripting agent`를 사용하도록 설정하기 전에 모든 Exchange 2013 서버에서 `Scripting agent` 구성 파일의 이름을 올바르게 변경하고 스크립트를 사용하여 구성 파일을 업데이트했는지 확인합니다. 구성 파일의 이름을 올바르게 변경하지 않거나 다른 Exchange 2013 서버에서 이 컴퓨터로 구성 파일을 복사하지 않은 경우에는 cmdlet을 실행할 때마다 오류 메시지가 나타납니다.

`Scripting agent`를 사용하도록 설정하려면 다음을 수행해야 합니다.

1.  조직의 모든 Exchange 2013 서버에서 **\<installation path\>\\V15\\Bin\\CmdletExtensionAgents**에 있는 ScriptingAgentConfig.xml.sample 파일의 이름을 ScriptingAgentConfig.xml로 변경합니다.
    

    > [!NOTE]
    > 한 Exchange 2013 서버의 구성 파일을 다른 Exchange 2013&nbsp;서버로 복사할 수 있습니다. 구성 파일을 복사하기 전에 먼저 업데이트해야 합니다.



2.  조직의 모든 Exchange 2013 서버에서 이름을 변경한 구성 파일에 스크립트를 추가합니다.

3.  `Scripting agent` cmdlet 확장 에이전트를 사용하도록 설정합니다. cmdlet 확장 에이전트 사용 설정에 대한 자세한 내용은 [Cmdlet 확장 에이전트를 관리 합니다.](manage-cmdlet-extension-agents-exchange-2013-help.md)을 참조하십시오.

## 스크립팅 에이전트 우선 순위

기본적으로 `Scripting agent` cmdlet 확장 에이전트는 `Scripting agent` 에이전트를 제외한 다른 모든 에이전트 이후에 실행됩니다. 새로 만든 스크립트가 기존의 에이전트를 대체하도록 하려면 다른 에이전트를 사용하지 않도록 설정하거나 다른 에이전트의 우선 순위를 변경하여 `Scripting agent` cmdlet 확장 에이전트가 먼저 실행되도록 해야 합니다. 에이전트를 사용하지 않도록 설정하는 방법이나 에이전트의 우선 순위를 변경하는 방법에 대한 자세한 내용은 [Cmdlet 확장 에이전트를 관리 합니다.](manage-cmdlet-extension-agents-exchange-2013-help.md) 항목을 참조하십시오.

