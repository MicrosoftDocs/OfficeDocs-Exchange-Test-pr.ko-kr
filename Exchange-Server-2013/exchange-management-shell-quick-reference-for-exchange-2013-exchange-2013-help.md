---
title: 'Exchange 2013에 대 한 Exchange 관리 셸 빠른 참조: Exchange 2013 Help'
TOCTitle: Exchange 2013에 대 한 Exchange 관리 셸 빠른 참조
ms:assetid: 3ea4a105-a93c-48ba-96ce-6170125354e1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ619302(v=EXCHG.150)
ms:contentKeyID: 50482930
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013에 대 한 Exchange 관리 셸 빠른 참조

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

이 항목에서는 RTM(Release To Manufacturing) 및 최신 버전의 Microsoft Exchange Server 2013에서 제공하는 가장 일반적으로 사용되는 cmdlet에 대해 설명하며 사용 예를 보여 줍니다.


> [!NOTE]
> Exchange 2013의 다른 분야에 대한 자세한 내용이 곧 추가될 예정입니다.



Exchange의 Exchange 2013 관리 셸 및 사용 가능한 모든 cmdlet에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [PowerShell을 사용 하 여 Exchange 2013 (Exchange 관리 셸)](https://technet.microsoft.com/ko-kr/library/bb123778\(v=exchg.150\))

  - [Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\))

## 알아보려는 내용

## 일반적인 cmdlet 작업

다음 동사는 대부분의 cmdlet에서 지원되며 특정 작업과 연결되어 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>New</p></td>
<td><p>New 동사는 새 구성 설정, 새 데이터베이스 또는 새 SMTP 커넥터 등 개체의 인스턴스를 만듭니다.</p></td>
</tr>
<tr class="even">
<td><p>Remove</p></td>
<td><p>Remove 동사는 사서함 또는 전송 규칙 등 개체의 인스턴스를 제거합니다.</p>
<p>모든 Remove cmdlet은 <em>WhatIf</em> 및 <em>Confirm</em> 매개 변수를 지원합니다. 이러한 매개 변수에 대한 자세한 내용은 Important Parameters를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>Enable</p></td>
<td><p>Enable 동사는 설정을 사용할 수 있게 하거나 받는 사람이 메일을 사용할 수 있게 합니다.</p></td>
</tr>
<tr class="even">
<td><p>Disable</p></td>
<td><p>Disable 동사는 사용할 수 있는 설정을 사용할 수 없게 하거나 받는 사람이 메일을 사용할 수 없게 합니다.</p>
<p>모든 Disable 작업도 <em>WhatIf</em> 및 <em>Confirm</em> 매개 변수를 지원합니다. 이러한 매개 변수에 대한 자세한 내용은 Important Parameters를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>Set</p></td>
<td><p>Set 동사는 연락처의 별칭 또는 사서함 데이터베이스의 삭제된 항목 보존 등 개체의 특정 설정을 수정합니다.</p></td>
</tr>
<tr class="even">
<td><p>Get</p></td>
<td><p>Get 동사는 특정 사서함, 모든 사서함 사용자 또는 도메인의 사서함 사용자 등 특정 개체 또는 개체 유형의 하위 집합을 쿼리합니다.</p></td>
</tr>
</tbody>
</table>


## 중요한 매개 변수

다음 매개 변수는 명령 실행 방법을 제어하고 명령이 데이터에 적용되기 전에 명령의 역할을 정확히 나타내도록 도와줍니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Identity</p></td>
<td><p><em>Identity</em> 매개 변수는 작업에 대한 고유한 개체를 식별합니다. 일반적으로 Enable, Disable, Remove, Set 및 Get cmdlet에 사용됩니다. 또한 <em>Identity</em>는 위치 매개 변수이기 때문에 명령줄에 매개 변수의 값을 지정할 때 <em>Identity</em>를 지정하지 않아도 됩니다.</p>
<p>예를 들어 <em>Get-Mailbox -Identity user1</em>은 <em>user1</em>의 사서함을 쿼리합니다. <em>Get-Mailbox user1</em>은 <em>Get-Mailbox -Identity user1</em>과 동일합니다.</p></td>
</tr>
<tr class="even">
<td><p>WhatIf</p></td>
<td><p><em>WhatIf</em> 매개 변수는 개체에 대해 수행하는 작업을 시뮬레이트하도록 cmdlet에 지시합니다. 사용자는 <em>WhatIf</em> 매개 변수를 사용하여 변경 내용을 실제로 적용하지 않고 어떠한 사항이 변경되는지 확인할 수 있습니다. 기본값은 <em>$true</em>입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Confirm</p></td>
<td><p><em>Confirm</em> 매개 변수를 사용하면 cmdlet이 처리를 일시 중지하므로 관리자는 처리를 계속하기 전에 cmdlet의 역할을 확인해야 합니다. 기본값은 <em>$true</em>입니다.</p></td>
</tr>
<tr class="even">
<td><p>Validate</p></td>
<td><p><em>Validate</em> 매개 변수를 사용하면 cmdlet이 작업 실행에 필요한 모든 선행 조건의 충족 여부와 작업의 완료 여부를 확인합니다.</p></td>
</tr>
</tbody>
</table>


## 팁과 트릭

다음은 Exchange 2013을 관리할 때 사용할 수 있는 다양한 작업과 연관된 명령입니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-Command</p></td>
<td><p>이 cmdlet은 Exchange 2013에서 실행할 수 있는 모든 작업을 검색합니다.</p></td>
</tr>
<tr class="even">
<td><p>Get-Command *<em>keyword</em>*</p></td>
<td><p>이 cmdlet은 cmdlet에 <em>keyword</em>가 있는 작업을 검색합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Get-<em>task</em> | Get-Member</p></td>
<td><p>이 cmdlet은 <em>task</em>의 모든 속성 및 메서드를 검색합니다.</p></td>
</tr>
<tr class="even">
<td><p>Get-<em>task</em> | Format-List</p></td>
<td><p>이 cmdlet은 서식 있는 목록에 쿼리의 출력을 표시합니다. Get cmdlet의 출력을 Format-List로 파이프하여 해당 명령에 의해 반환된 개체에 있는 속성의 전체 집합을 확인하거나 다음 예와 같이 확인할 개별 속성을 쉼표로 구분하여 지정할 수 있습니다. <em>Get-Mailbox *john* | Format-List alias,*quota</em></p></td>
</tr>
<tr class="odd">
<td><p>Help <em>task</em></p></td>
<td><p>이 cmdlet은 다음 예와 같이 Exchange 작업에 대한 Exchange 2013 관리 셸 도움말 정보를 검색합니다. <em>Help Get-Mailbox</em></p></td>
</tr>
<tr class="even">
<td><p>Get-<em>task</em> | Format-List &gt; <em>file.txt</em></p></td>
<td><p>이 cmdlet은 <em>task</em>의 출력을 다음 텍스트 파일로 내보냅니다. <em>file.txt</em></p></td>
</tr>
</tbody>
</table>


## 사용 권한


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-RoleGroupMember &quot;<em>Organization Management</em>&quot;</p></td>
<td><p>이 명령은 <em>Organization Management</em> 관리 역할 그룹의 구성원을 검색합니다.</p></td>
</tr>
<tr class="even">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Mail Recipient Creation</em>&quot; -GetEffectiveUsers</p></td>
<td><p>이 명령은 <em>Mail Recipient Creation</em> 관리 역할을 통해 사용 권한이 부여된 모든 사용자의 목록을 검색합니다. 여기에는 Mail Recipient Creation 역할이 할당된 역할 그룹 또는 USG(유니버설 보안 그룹)의 구성원인 사용자가 포함됩니다. 반면, 다른 포리스트의 연결된 역할 그룹의 구성원인 사용자는 포함되지 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -RoleAssignee <em>Administrator</em> | Get-ManagementRole | Get-ManagementRoleEntry</p></td>
<td><p>이 명령은 <em>Administrator</em> 사용자가 실행할 수 있는 cmdlet의 목록을 검색합니다.</p></td>
</tr>
<tr class="even">
<td><p>ForEach ($RoleEntry in Get-ManagementRoleEntry *\<em>Remove-Mailbox</em> -parameters Identity) {Get-ManagementRoleAssignment -Role $RoleEntry.Role -GetEffectiveUsers -Delegating $False | Where-Object {$_.EffectiveUserName -Ne &quot;All Group Members&quot;} | FL Role, EffectiveUserName, AssignmentChain}</p></td>
<td><p>이 명령은 <em>Remove-Mailbox</em> cmdlet을 실행할 수 있는 모든 사용자의 목록을 검색합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -WritableRecipient <em>kima</em> -GetEffectiveUsers | FT RoleAssigneeName, EffectiveUserName, Role, AssignmentChain</p></td>
<td><p>이 명령은 <em>kima</em>의 사서함을 수정할 수 있는 모든 사용자의 목록을 검색합니다.</p></td>
</tr>
<tr class="even">
<td><p>New-ManagementScope &quot;<em>Seattle Users</em>&quot; -RecipientRestrictionFilter { <em>City</em> -Eq &quot;<em>Seattle</em>&quot; }</p>
<p>New-RoleGroup &quot;<em>Seattle Admins</em>&quot; -Roles &quot;<em>Mail Recipients</em>&quot;, &quot;<em>Mail Recipient Creation</em>&quot;, &quot;<em>Mailbox Import Export</em>&quot;, -CustomRecipientWriteScope &quot;<em>Seattle Users</em>&quot;</p></td>
<td><p>이 명령은 역할 그룹의 구성원이 Seattle의 받는 사람을 관리할 수 있도록 허용하는 새 관리 범위와 관리 역할 그룹을 만듭니다.</p>
<p>먼저 사용자 개체의 <em>City</em> 특성에 <em>Seattle</em>이라고 표시된 받는 사람만 일치시키는 <em>Seattle Users</em> 관리 범위를 만듭니다.</p>
<p>그런 다음 <em>Seattle Admins</em>라는 새 역할 그룹을 만들고 <em>Mail Recipients</em>, <em>Mail Recipient Creation</em> 및 <em>Mailbox Import Export</em> 역할을 할당합니다. 구성원이 <em>Seattle Users</em> 받는 사람 필터 범위와 일치하는 사용자만 관리할 수 있도록 역할 그룹의 범위를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>New-ManagementScope &quot;<em>Vancouver Servers</em>&quot; -ServerRestrictionFilter { <em>ServerSite</em> -Eq &quot;<em>Vancouver</em>&quot; }</p>
<p>$RoleGroup = Get-RoleGroup &quot;<em>Server Management</em>&quot;</p>
<p>New-RoleGroup &quot;<em>Vancouver Server Management</em>&quot; -Roles $RoleGroup.Roles -CustomConfigWriteScope &quot;<em>Vancouver Servers</em>&quot;</p></td>
<td><p>이 명령은 새 역할 그룹의 구성원이 Vancouver Active Directory 사이트에 있는 서버만 관리할 수 있도록 허용하는 새 관리 범위를 만들고 기존 역할 그룹을 복사합니다.</p>
<p>먼저 <em>Vancouver</em> Active Directory 사이트에 위치한 서버만 일치시키는 <em>Vancouver Servers</em> 관리 범위를 만듭니다. Active Directory 사이트는 서버 개체의 <em>ServerSite</em> 특성에 저장됩니다.</p>
<p>그런 다음 <em>Server Management</em> 역할 그룹의 복사본인 <em>Vancouver Server Management</em>라는 새 역할 그룹을 만듭니다. 그러나 구성원이 <em>Vancouver Servers</em> 구성 필터 범위와 일치하는 서버만 관리할 수 있도록 이 새 역할 그룹의 범위를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p>Add-RoleGroupMember &quot;<em>Organization Management</em>&quot; -Member <em>davids</em></p></td>
<td><p>이 명령은 <em>davids</em> 사용자를 <em>Organization Management</em> 역할 그룹에 추가합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Mail Recipient Creation</em>&quot; -RoleAssignee &quot;<em>Seattle Admins</em>&quot; | Remove-ManagementRoleAssignment</p></td>
<td><p>이 명령은 <em>Seattle Admins</em> 역할 그룹에서 <em>Mail Recipient Creation</em> 역할을 제거합니다. 이 명령은 역할 그룹에 역할을 할당하는 관리 역할 할당의 이름을 몰라도 되므로 유용합니다.</p></td>
</tr>
</tbody>
</table>


## 원격 셸


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos</p>
<p>Import-PSSession $Session</p></td>
<td><p>이 명령은 로컬 도메인 가입 컴퓨터와 FQDN이 <em>ExServer.contoso.com</em>인 원격 Exchange 2013 서버 간의 새로운 원격 셸 세션을 엽니다. Windows PowerShell 명령줄 인터페이스가 포함된 Windows 관리 프레임워크가 로컬 컴퓨터에 설치되어 있고 원격 Exchange 2013 서버를 관리하려는 경우에만 사용하십시오. 이 명령은 현재 로그온 자격 증명을 사용하여 원격 Exchange 2013 서버를 인증합니다.</p></td>
</tr>
<tr class="even">
<td><p>$UserCredential = Get-Credential</p>
<p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos -Credential $UserCredential</p>
<p>Import-PSSession $Session</p></td>
<td><p>이 명령은 로컬 도메인 가입 컴퓨터와 FQDN이 <em>ExServer.contoso.com</em>인 원격 Exchange 2013 서버 간의 새로운 원격 셸 세션을 엽니다. Windows PowerShell이 포함된 Windows 관리 프레임워크가 로컬 컴퓨터에 설치되어 있고 원격 Exchange 2013 서버를 관리하려는 경우에만 사용하십시오. 이 명령은 사용자가 명시적으로 지정한 자격 증명을 사용하여 원격 Exchange 2013 서버를 인증합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Remove-PSSession $Session</p></td>
<td><p>이 명령은 로컬 컴퓨터와 원격 Exchange 2013 서버 간의 원격 셸 세션을 닫습니다.</p></td>
</tr>
<tr class="even">
<td><p>Import-RecipientDataProperty -Identity &quot;Tony Smith&quot; -SpokenName -FileData <em>([Byte[]]$(Get-Content -Path &quot;M:\AudioFiles\TonySmith.wma&quot; -Encoding Byte -ReadCount 0))</em></p></td>
<td><p>이 명령은 cmdlet에 Exchange 2013 서버로 파일을 가져오는 데 필요한 FileData 매개 변수를 사용하는 구문(기울임꼴로 표시됨)의 예를 보여 줍니다. 이 구문은 <em>M:\AudioFiles\TonySmith.wma</em> 파일에 포함된 데이터를 캡슐화하고 Import-RecipientDataProperty cmdlet의 FileData 속성에 데이터를 스트림합니다.</p>
<p>FileData 매개 변수는 대부분의 cmdlet에 이 구문을 사용하여 로컬 컴퓨터에 있는 파일의 데이터를 수락합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Export-RecipientDataProperty -Identity tony@contoso.com -SpokenName <em>| ForEach { $_.FileData | Add-Content C:\tonysmith.wma -Encoding Byte}</em></p></td>
<td><p>이 명령은 원격 Exchange 2013 서버에서 파일을 내보내는 데 필요한 구문(기울임꼴로 표시됨)의 예를 보여 줍니다. 이 구문은 cmdlet에서 반환한 개체의 FileData 속성에 저장된 데이터를 캡슐화한 다음 로컬 컴퓨터로 데이터를 스트림합니다. 그런 다음 <em>C:\tonysmith.wma</em> 파일에 데이터가 저장됩니다.</p>
<p>FileData 속성이 포함된 개체를 출력하는 대부분의 cmdlet은 이 구문을 사용하여 로컬 컴퓨터의 파일로 데이터를 내보냅니다.</p></td>
</tr>
</tbody>
</table>

