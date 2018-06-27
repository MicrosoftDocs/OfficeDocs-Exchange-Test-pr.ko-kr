---
title: '크로스 포리스트 이동 요청에 대 한 사서함을 준비: Exchange 2013 Help'
TOCTitle: 크로스 포리스트 이동 요청에 대 한 사서함을 준비
ms:assetid: fdbed4fc-a77e-40d5-a211-863b05d74784
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633491(v=EXCHG.150)
ms:contentKeyID: 50484603
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 크로스 포리스트 이동 요청에 대 한 사서함을 준비

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-11-22_

**요약:** Exchange 2013 에서 크로스 포리스트 이동에 대 한 사서함을 준비 하는 방법에 대 한 설명입니다.

사서함 이동 및 마이그레이션 Exchange 관리 셸을 사용 하 여 Microsoft Exchange 2013 지원 **New-MoveRequest** 및 **New-MigrationBatch** cmdlet 특히 합니다. Exchange 관리 센터 (EAC)를 통해 사서함에 이동할 수도 있습니다. Note Exchange 2013 포리스트에 Exchange 2010과 Exchange 2013 사서함을 이동할 수 있습니다.

사서함을 Exchange 포리스트에서 Exchange 2013 포리스트를 이동 하려면 Exchange 2013 대상 포리스트의 Active Directory 특성의 지정 된 집합을 사용 하는 유효한 메일 사용이 가능한 사용자를 포함 해야 합니다. 하나 이상의 Exchange 2013 클라이언트 액세스 서버는 포리스트에 배포 된 경우 포리스트 Exchange 2013 포리스트 것으로 간주 됩니다.

사서함 이동을 준비 하려면 대상 포리스트에서 필요한 특성을 가진 사용자가 메일 사용이 가능한 만들어야 합니다. 필요한 특성을 사용 하 여 메일 사용이 가능한 사용자를 만들기에 권장 되는 두가지 방법이 다음과 같습니다.

  - 크로스 포리스트 전체 주소 목록 (GAL) 동기화를 위한 Microsoft ILM Identity Lifecycle Manager ()를 배포 하는 경우 ILM 2007 기능 팩 1 (FP1)에 대 한 서비스 팩 1 (SP1)를 사용 하는 메일 사용이 가능한 사용자 만들기 (영문)에 권장 되는 방법이입니다. 원본 사서함 사용자 및 대상 메일 사용자를 동기화 하는 ILM를 사용자 지정 하는 방법을 설명 하는 데 사용할 수 있는 예제 코드를 작성 했을 때 되었습니다.
    
    자세한 내용과 예제 코드를 다운로드 하는 방법에 대 한 [예제 코드를 사용 하 여 크로스 포리스트 이동에 대 한 사서함을 준비](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)를 참조 합니다.

  - ILM/MIIS 이외의 Active Directory 도구를 사용 하는 대상 메일 사용자를 만든 경우 cmdlet을 사용 **Update-Recipient***Identity* 매개 변수와 함께 대상 메일 사용자에 대 한 **LegacyExchangeDN** 를 생성 하는 주소록 서비스를 실행 합니다. PowerShell 스크립트에서 읽고 및 Active Directory 에 기록 하 **Update-Recipient** cmdlet을 호출 하는 샘플 Windows 작성 했습니다.
    
    샘플 스크립트를 사용 하는 방법에 대 한 자세한 내용은 [셸에서 준비 MoveRequest.ps1 스크립트를 사용 하 여 크로스 포리스트 이동에 대 한 준비 사서함](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)을 참조 하십시오.

대상 메일 사용자를 만든 후 **New-MoveRequest** 또는 **New-MigrationBatch** cmdlet은 대상 Exchange 2013 포리스트로 사서함을 이동할를 실행할 수 있습니다.

원격 이동 요청에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

  - [New-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219166\(v=exchg.150\))

  - [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))

원격 사서함 이동 및 원격 레거시 이동 하는 방법에 대 한 자세한 내용은 [Exchange 2013 사서함 이동](mailbox-moves-in-exchange-2013-exchange-2013-help.md)을 참조 하십시오.

이 항목의 나머지 부분에서는 사서함 이동에 필요한 Active Directory 메일 사용자 특성을 설명 합니다. 사서함 이동 작업을 준비 하는 코드 또는 스크립트를 사용 하는 경우 이러한 특성의 경우에 대 한 구성 됩니다. 그러나 Active Directory 편집기를 사용 하 여 이러한 특성을 수동으로 복사할 수 있습니다.

## 사서함에 필요한 active Directory 사용자 특성 이동

원격 사서함 이동을 지원 하기 위해 대상 Exchange 2013 포리스트에 있는 메일 사용자 개체에이 섹션에 설명 된 Active Directory 특성이 있어야 합니다.

  - 필수 특성

  - 선택적 특성

  - 연결 된 특성

  - 연결 된 사용자 특성

  - 리소스 사서함 특성

  - 추가 특성

## 필수 특성

다음 표에서 최소 제대로 작동 하려면 **New-MoveRequest** cmdlet에 대 한 대상 메일 사용자에 대해 ILM에서 구성 해야 하는 특성 집합을 나열 합니다.

### 메일 사용자의 특성

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>메일 사용자의 Active Directory 특성</th>
<th>작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>displayName</strong></p></td>
<td><p>원본 사서함의 해당 특성을 복사 하거나 새 값을 생성 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Mail</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>mailNickname</strong></p></td>
<td><p>원본 사서함의 해당 특성을 복사 하거나 새 값을 생성 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchArchiveGUID and msExchArchiveName</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다. 특성은 원본 사서함 Exchange 2010 인 경우 사용할 수만 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMailboxGUID</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>-0x80000006 (16 진수)를 2147483642 (10 진수) //equivalent 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientTypeDetails</strong></p></td>
<td><p>128 (10 진수) / (16 진수) 0x80입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUserCulture</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchVersion</strong></p></td>
<td><p>44220983382016 (10 진수)입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>cn</strong></p></td>
<td><p>원본 사서함의 해당 특성을 복사 하거나 새 값을 생성 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>proxyAddresses</strong></p></td>
<td><p>원본 사서함의 <strong>proxyAddresses</strong> 특성에 복사 합니다. 또한 복사본 원본 사서함의 <strong>LegacyExchangeDN</strong> 는 X500으로 대상 메일 사용자의 <strong>proxyAddresses</strong> 특성에는 주소입니다.</p>

> [!NOTE]
> 원본 사서함 사용자의 <STRONG>proxyAddresses</STRONG> 대상 포리스트의 신뢰할 수 있는 도메인과 일치 하는 SMTP 주소를 포함 해야 합니다. 이렇게 하면 올바르게 <STRONG>targetAddress</STRONG> 를 선택 하려면 <STRONG>New-MoveRequest</STRONG> cmdlet (사서함 이동 요청 완료 되 면 원본 사서함 사용자에서 변환) 원본 메일 사용이 가능한 사용자의 되어있는지 확인 하려면 해당 메일 라우팅 여전히 작동 합니다.


</td>
</tr>
<tr class="even">
<td><p><strong>sAMAccountName</strong></p></td>
<td><p>원본 사서함의 해당 특성을 복사 하거나 새 값을 생성 합니다.</p>
<p>값에는 대상 메일 사용자에 속하는 대상 포리스트 도메인 내에서 고유한 지 확인 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>targetAddress</strong></p></td>
<td><p>원본 사서함의 <strong>proxyAddresses</strong> 특성에 SMTP 주소를 설정 합니다.</p>
<p>이 SMTP 주소는 원본 포리스트에의 신뢰할 수 있는 도메인에 속해 있어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>userAccountControl</strong></p></td>
<td><p>상수: 0x202, ACCOUNTDISABLE에 514 //equivalent | NORMAL_ACCOUNT 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>userPrincipalName</strong></p></td>
<td><p>원본 사서함의 해당 특성을 복사 하거나 새 값을 생성 합니다. 메일 사용자는 사용 하지 않도록 설정 하는 로그온 이기 때문에이 <strong>userPrincipalName</strong> 사용 되지 않습니다.</p></td>
</tr>
</tbody>
</table>


## 선택적 특성

필수는 다음과 같은 특성이; 제대로 작동 하려면 **New-MoveRequest** cmdlet에 대 한 구성 되었는지 아니면 그러나 해당 동기화 (영문) 사서함을 이동한 후 아주 좋음 끝-사용자 환경을 제공 합니다. 대상 포리스트의 GAL에에서이 대상 메일 사용자를 표시 하기 때문에 다음과 같은 GAL 관련 특성을 설정 해야 합니다.

### GAL 관련 특성

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>메일 사용자의 Active Directory 특성</th>
<th>작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>c</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>co</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>countryCode</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>company</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>department</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>facsimileTelephoneNumber</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>givenName</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>homePhone</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>info</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>initials</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>l</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>mobile</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchAssistantName</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchHideFromAddressLists</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherHomePhone</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherTelephone</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>pager</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>physicalDeliveryOfficeName</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalCode</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>sn</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>st</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>streetAddress</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>telephoneAssistant</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>telephoneNumber</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>title</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
</tbody>
</table>


## 연결 된 특성

연결 된 특성은 로컬 포리스트에 있는 다른 Active Directory 개체를 참조 하는 Active Directory 특성입니다. 직접 대상 포리스트에 있는 메일 사용자에 게 원본 포리스트에 있는 사서함에서 연결 된 특성 값을 복사할 수 없습니다. 첫째, 원본 사서함 특성에서 참조 하는 원본 포리스트에 있는 Active Directory 개체 찾아야 합니다. 그런 다음, 찾아야 해당 하는 Active Directory 개체 대상 포리스트에서 위에서 언급 한 Active Directory 개체에 대 한 원본 포리스트에 있는 합니다. 및 마지막으로, 대상 포리스트에서 Active Directory 개체를 참조 하는 대상 메일 사용자의 특성을 설정 합니다.

### 연결 된 특성

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>메일 사용자의 Active Directory 특성</th>
<th>작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>altRecipient</strong></p></td>
<td><p>원본 사서함의 <strong>altRecipient</strong> 특성에 해당 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>deliverAndRedirect</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다. 이 특성은 <strong>altRecipient</strong>함께 설정 되어야 하는 부울 값입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Manager</strong> (및 해당 역방향 연결)</p></td>
<td><p>원본 사서함의 관리자 특성에 해당 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>MemberOf</strong> (역방향 연결)</p></td>
<td><p>그룹 구성원 특성의 백 링크가입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>publicDelegates</strong> (및 해당 역방향 연결)</p></td>
<td><p>원본 사서함의 <strong>publicDelegates</strong> 특성에 해당 합니다.</p></td>
</tr>
</tbody>
</table>


## 연결 된 사용자 특성

Exchange 2013 리소스 포리스트는 사서함을 이동 하려는 경우 리소스 포리스트에 있는 사서함에 *연결 된 사서함*으로 간주 됩니다. 이 시나리오에서는 (대상) 리소스 포리스트에 연결 된 메일 사용자를 만들려면 해야 합니다. 연결 된 메일 사용자를 만들려면 다음 표에 표시 된 특성을 설정 해야 합니다.

### 연결 된 메일 사용자 특성

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>메일 사용자의 Active Directory 특성</th>
<th>작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchMasterAccountHistory</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMasterAccountSid</strong></p></td>
<td><p>원본 사서함에 <strong>msExchMasterAccountSid</strong>을 복사 합니다. 그렇지 않은 경우 원본 사서함의 <strong>objectSid</strong>에 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>상수:를-1073741818 (10 진수) //equivalent * 서명 되지 않은 * 0xC0000006 합니다.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 연결된 된 사서함 원본 포리스트와 대상 포리스트 사이 포리스트 트러스트 하는 경우에 만들 수 있습니다.



원본 개체 비활성화 되 고 **msExchMasterAccountSid** 특성은 self (리소스 사서함, 공유 사서함)로 설정 하지 스탬프 아무것도 대상 사용자에 대해.

원본 개체를 사용 하지 않도록 설정 하는 경우 **msExchMasterAccountSid** 특성은 설정 되지 사서함 유효 하지 않습니다.

원본 개체를 사용할 수 **msExchMasterAccountSid** 특성을 설정 하는 경우 사서함 유효 하지 않습니다.

## 리소스 사서함 특성

Exchange 2013 포리스트 리소스 사서함을 이동 하려는 경우 대상 메일 사용자에 대해 다음 표에 표시 된 특성을 설정 해야 합니다.

### 리소스 사서함 특성

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>메일 사용자의 Active Directory 특성</th>
<th>작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>원본 사서함은 회의실 하는 경우:</p>
<ul>
<li><p><strong>상수</strong> -2147481850 (10 진수) //equivalent * 서명 되지 않은 * 0x80000706 합니다.</p></li>
</ul>
<p>원본 사서함 장비 사서함이 있는 경우:</p>
<ul>
<li><p><strong>상수</strong> -2147481594 (10 진수) //equivalent * 서명 되지 않은 * 0x80000806 합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceCapacity</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceDisplay</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceMetaData</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceSearchProperties</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
</tbody>
</table>


## 추가 특성

Exchange 2007 **Move-Mailbox** cmdlet도 사서함을 이동할 때 다음 표에 표시 된 특성을 복사 합니다. 필요에 따라 조직에 필요한 경우 이러한 특성을 복사할 수 있습니다.

### 리소스 사서함 특성

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>메일 사용자의 Active Directory 특성</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>comment</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>deletedItemFlags</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>delivContLength</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>departmentNumber</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>description</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>division</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeID</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>employeeNumber</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeType</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>extensionAttribute1-15</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>homePostalAddress</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>internationalISDNNumber</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ipPhone</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>language</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>lmPwdHistory</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>localeID</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>mAPIRecipient</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>middleName</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticCompanyName</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticDepartment</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticDisplayName</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticFirstName</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticLastName</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchBlockedSendersHash</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCExpirySuspensionEnd</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchELCExpirySuspensionStart</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCMailboxFlags</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchExternalOOFOptions</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneFlags</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLDeleteThreshold</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLJunkThreshold</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLQuarantineThreshold</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLRejectThreshold</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMDBRulesQuota</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchPoliciesExcluded</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchSafeRecipientsHash</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchSafeSendersHash</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUMSpokenName</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherFacsimileTelephoneNumber</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherIpPhone</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherMobile</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>otherPager</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>preferredDeliveryMethod</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>personalPager</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>personalTitle</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>photo</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>pOPCharacterSet</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>pOPContentFormat</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalAddress</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>postOfficeBox</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>primaryInternationalISDNNumber</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>primaryTelexNumber</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>showInAdvancedViewOnly</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>street</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>terminalServer</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>textEncodedORAddress</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>thumbnailLogo</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>thumbnailPhoto</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>url</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>userCert</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>userCertificate</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>userSMIMECertificate</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>wWWHomePage</strong></p></td>
<td><p>직접 원본 사서함의 해당 특성을 복사 합니다.</p></td>
</tr>
</tbody>
</table>

