---
title: '연결이 끊어진 사서함: Exchange 2013 Help'
TOCTitle: 연결이 끊어진 사서함
ms:assetid: 508ebe2b-387d-4867-bdb0-028ef351ce56
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232039(v=EXCHG.150)
ms:contentKeyID: 50555986
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 연결이 끊어진 사서함

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Active Directory 사용자 계정과 Exchange 사서함 데이터베이스에 저장 된 사서함 데이터의 각 Microsoft Exchange 사서함 구성 됩니다. 사서함에 대 한 모든 구성 데이터 Active Directory 사용자 개체의 Exchange 특성에 저장 됩니다. 사서함 데이터베이스의 사서함에 연결 된 사용자 계정 메일 데이터를 포함 합니다. 다음 그림은 사서함의 구성 요소를 보여줍니다.

**사서함 구성 요소**

![사서함을 구성하는 요소](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "사서함을 구성하는 요소")

*사서함 연결을 끊은* 은 Active Directory 사용자 계정과 연결 되어있지 않은 사서함 데이터베이스에서 사서함 개체입니다. 연결이 끊긴된 사서함의 두가지 유형이 있습니다.

  - **사서함을 사용 하지 않도록 설정**   사서함을 사용 하지 않도록 설정 하거나 Exchange 관리 센터 (EAC)에서 삭제할 시기나 **Disable-Mailbox** 또는 **Remove-Mailbox** cmdlet을 사용 하 여 Exchange 관리 셸에서 Exchange 사서함 데이터베이스에서 삭제 된 사서함을 유지 하 고 사서함을 비활성된 상태로 전환 합니다. 이 때문에 비활성화 하거나 삭제 된 사서함을 *사용할 수 없는 사서함*이라고 합니다. 된다는 점에서 차이가 사서함을 사용 하지 않도록 설정, Exchange 특성은 해당 Active Directory 사용자 계정에서 제거 된 있지만 사용자 계정을 그대로 유지 됩니다. 사서함을 삭제 하는 경우에 Exchange 특성 및 Active Directory 사용자 계정을 모두 삭제 됩니다.
    
    비활성화 및 삭제 된 사서함은 사서함 데이터베이스에서 삭제 된 사서함 보존 기간이 만료 되 면 30 일 때까지 기본적으로 유지 됩니다. 보존 기간이 만료 되 면 후 사서함이 영구적으로 삭제 ( *비우기*이 라고도 함). **Remove-Mailbox** cmdlet을 사용 하 여 사서함 삭제 하는 경우의 보존 기간 동안에도 유지 됩니다.
    

    > [!IMPORTANT]
    > <STRONG>Remove-Mailbox</STRONG> cmdlet 및 <EM>Permanent</EM> 또는 <EM>StoreMailboxIdentity</EM> 매개 변수를 사용 하 여 사서함 삭제 하는 경우 해당 즉시 삭제할 사서함 데이터베이스에서 합니다.

    
    조직에서 사용할 수 없는 사서함을 확인 하려면 셸에서 다음 명령을 실행 합니다.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "Disabled" } | ft DisplayName,Database,DisconnectDate

  - **일시 삭제 된 사서함**   다른 사서함 데이터베이스에 사서함이 움직일 Exchange 삭제 되지는 않습니다 완벽 하 게 사서함 원본 사서함 데이터베이스에서 이동이 완료 되 면. 대신, 원본 사서함 데이터베이스에서 사서함을 *일시적으로 삭제 된* 상태로 전환 됩니다. Like 사용할 수 없는 사서함을 일시적으로 삭제 된 사서함은 삭제 된 사서함 보존 기간이 만료 될 때까지 또는 **Remove-StoreMailbox** cmdlet를 사용 하는 사서함을 삭제 하려면 원본 데이터베이스에 유지 됩니다.
    
    조직에서 일시 삭제 된 사서함을 확인 하려면 다음 명령을 실행 합니다.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | ft DisplayName,Database,DisconnectDate

**목차**

사용할 수 없는 사서함 (영문)

작업을 보관 사서함을 사용 하지 않도록 설정

일시 삭제 된 사서함 (영문)

연결이 끊긴된 사서함 (영문)의 요약

연결이 끊긴된 사서함 설명서

## 사용할 수 없는 사서함 (영문)

사서함 데이터베이스에서 제거 되기 전에 비활성화 된 사서함에 대 한 여러 작업을 수행할 수 있습니다.

  - 동일한 사용자 계정에 다시 연결 합니다.

  - 메일 사용이 가능한 없는 다른 사용자 계정에 연결, 사서함이 없는 사용자 계정 하는 의미 합니다.

  - 사용자 계정을 사용 하는 기존 사서함에 복원 합니다. 예 사서함 삭제 된 사용자에 게 새 사서함을 하는 경우 새 사서함을 사용할 수 없는 사용자의 사서함을 복원할 수 있습니다.

  - 영구적으로 Exchange 사서함 데이터베이스에서 삭제 합니다.

## 연결 또는 사용할 수 없는 사서함 복원

다음은 시나리오 사서함 보존 기간이 만료 되기 전에 또는 영구적으로 삭제 되기 전에 비활성화 된 사서함을 복원 또는 연결을 사용할 수 있습니다.

  - 사서함을 사용 하지 않도록 설정 하 고 동일한 Active Directory 사용자 계정에 사서함을 다시 연결 해야 합니다.

  - EAC 또는 [Remove-Mailbox](https://technet.microsoft.com/ko-kr/library/aa995948\(v=exchg.150\)) cmdlet을 사용 하 여 사서함을 삭제 하 고 다른 Active Directory 사용자 계정에 사서함을 다시 연결 해야 합니다.

  - 사서함을 삭제 하 고 기존 사서함에 사서함을 복원 해야 합니다. 예 사서함 삭제 된 사용자에 게 새 사서함을 하는 경우 새 사서함을 사용할 수 없는 사용자의 사서함을 복원할 수 있습니다.

  - 외부 Exchange 조직에 존재 하는 포리스트에 있는 사용자 계정에 연결 된 연결된 된 사서함을 사용자 사서함으로 변환 하려고 합니다. 리소스 포리스트 시나리오는 외부 계정을 사용 하 여 사서함을 연결 하려는 경우의 예입니다. 이 시나리오에서는 사용자 포리스트의 개체에는 Exchange 사서함을 되었지만 로그온 사용자 개체에서 사용할 수 없습니다. 외부 계정 포리스트에 있는 사용자 계정을 사용 하 여 Exchange 포리스트에 있는 사서함을 연결 해야 합니다.

두 가지 다시 연결 하거나 사용할 수 없는 사서함을 복원할 수 있습니다. 첫번째 방법은를 사용 하 여 EAC 또는 **Connect-Mailbox** cmdlet은 사용자 계정에 사용할 수 없는 사서함에 연결 하는 것입니다. 사용할 수 없는 사서함에 다시 연결 하는 절차를 [비활성화 된 사서함에 연결](connect-a-disabled-mailbox-exchange-2013-help.md)을 참조 하십시오.

두번째 방법 **New-MailboxRestoreRequest** cmdlet을 사용 하 여 기존 사서함을 사용 하 여 사용할 수 없는 사서함의 내용을 병합. 이 cmdlet는 사서함 복제 서비스 (MRS)를 사용 하 여 사서함을 복원 합니다. 사서함 사용 하지 않도록 설정 하는 복원 하는 절차를 [삭제 된 사서함을 복원 또는 연결](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)을 참조 하십시오.

## 비활성화 된 사서함을 영구적으로 삭제

앞서 설명한 것 처럼 Exchange 해당 사서함 데이터베이스에 대해 구성 하는 삭제 된 사서함 보존 설정에 기초 하 여 사서함 데이터베이스에 사용할 수 없는 사서함을 유지 합니다. 지정 된 보존 기간 이후에 사용할 수 없는 사서함 Exchange 사서함 데이터베이스에서 제거 됩니다. **Remove-StoreMailbox** cmdlet을 사용 하 여 사서함 데이터베이스에서 사용할 수 없는 사서함 및 모든 메시지 내용을 영구적으로 삭제할 수 있습니다. 비활성화 된 사서함을 자동으로 삭제 하거나 관리자가 영구적으로 삭제 된 후 데이터 손실을 영구적 이며 사서함을 복구할 수 없습니다.

자세한 내용은 [사서함을 영구적으로 삭제](permanently-delete-a-mailbox-exchange-2013-help.md)을 참조 하십시오.

맨 위로 이동

## 작업을 보관 사서함을 사용 하지 않도록 설정

사용 하지 않도록 보관 사서함 끊어질 수 있습니다. 비활성화 된 기본 사서함와 마찬가지로 연결이 끊어진된 보관 함을 사서함 *Archive* 매개 변수와 함께 **Connect-Mailbox** cmdlet을 사용 하 여 연결할 수 있습니다.

기본 사서함 및 보관 사서함에 이전에 연결 된 동일한 사용자 사서함을 보관 사서함에 연결 해야 하므로 같은 레거시 DN (고유 이름)을 공유 합니다. 다른 사용자 사서함에 보관 사서함을 연결할 수 없습니다.

연결이 끊어진된 보관 사서함에 대 한 두 작업을 수행할 수 있습니다.

  - **기존 기본 사서함에 연결**   연결이 끊긴된 기본 사서함 처럼 연결이 끊어진된 보관 함을 사서함 그대로 유지 됩니다 사서함 데이터베이스에서 삭제 된 사서함 보존 기간이 만료 되 면 30 일 때까지 기본적으로 합니다. 이 시간 동안 비활성화 되기 전에에 연결 된 동일한 사용자 계정에 다시 연결 하 여 보관 사서함을 복구할 수 있습니다.
    

    > [!NOTE]
    > 사용자 사서함에 대 한 보관 사서함을 사용 하지 않도록 설정 하 고 다음 해당 동일한 사용자에 대 한 보관 사서함을 사용 하도록 설정 하는 경우 해당 사용자 사서함에는 새 보관 사서함을 발생 합니다. <STRONG>Connect-Mailbox</STRONG> cmdlet을 사용 하 여 주 사서함 사용자에 게 연결 수를 하는 동안에 기존 사서함을 사용할 수 없는 보관 사서함에 연결 하려면 <STRONG>Enable-Mailbox</STRONG> cmdlet을 사용 해야 합니다.

    
    자세한 내용은 [Exchange 2013에서 원본 위치 보관 관리](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)을 참조 하십시오.

  - **Exchange 사서함 데이터베이스에서 영구적으로 삭제**    Exchange는 사서함 데이터베이스에 대해 구성 된 삭제 된 사서함 보존 설정에 따라 연결이 끊어진된 보관 사서함을 유지 합니다. 기본 보존 기간은 30 일입니다. 지정 된 사서함 보존 기간이 지난 후 연결이 끊어진된 보관 사서함이 Exchange 사서함 데이터베이스에서 제거 됩니다.
    
    비활성화 된 기본 사서함 처럼 **Remove-StoreMailbox** cmdlet을 사용 하 여 언제 든 지 비활성화 된 보관 사서함을 영구적으로 삭제할 수 있습니다. 자세한 내용은 [사서함을 영구적으로 삭제](permanently-delete-a-mailbox-exchange-2013-help.md)을 참조 하십시오.

맨 위로 이동

## 일시 삭제 된 사서함 (영문)

일시 삭제 된 사서함을 Exchange 사서함 데이터베이스 다른 사서함 데이터베이스에는 사서함이 이동할 때 만들어집니다. Exchange 하지 완벽 하 게 사서함을 삭제할 원본 데이터베이스에서 이동 후 실패 대상 데이터베이스에서 사서함을 되도록 지정 하는 이동 하는 동안 오류가 발생 하는 경우. 항상 원본 사서함을 복원 하 고 다시 시도 수 있습니다. Exchange는 사서함 보존 기간 동안 일시 삭제 된 사서함을 유지 합니다.

일시 삭제 된 사서함에 대 한 두 작업을 수행할 수 있습니다.

  - 기존 사서함 복원 합니다.

  - 영구적으로 Exchange 사서함 데이터베이스에서 삭제 합니다.

일시 삭제 된 사서함을 영구적으로 삭제 하 고 복원 하는 절차는 사용할 수 없는 사서함에 대 한 경우와 비슷합니다. 자세한 내용은 다음 항목을 참조 하십시오.

  - [일시 삭제 된 사서함 복원](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

  - [사서함을 영구적으로 삭제](permanently-delete-a-mailbox-exchange-2013-help.md)

맨 위로 이동

## 연결이 끊긴된 사서함 (영문)의 요약

다음 표에서 연결이 끊긴된 사서함을 어떻게 사서함 연결이 끊어졌습니다, 사서함 연결이 끊어지면 해당 Active Directory 사용자 계정에 수행 되는 작업을 포함 하는 방법에 대 한 정보를 요약 하 고 연결이 끊긴 사서함의 옵션 및 도구에 연결 하거나 복원 해야 합니다.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>사서함을 비활성화 하는 방법</th>
<th><em>DisconnectReason</em> 속성의 값</th>
<th>Active Directory 사용자 계정 유지</th>
<th>연결 또는 복원 옵션</th>
<th>도구</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>EAC: <strong>받는 사람</strong> &gt; <strong>사서함</strong> &gt; <strong>사용 하지 않도록 설정</strong></p></li>
<li><p>셸: <strong>Disable-Mailbox</strong> cmdlet</p></li>
</ul></td>
<td><p>사용 안 함</p></td>
<td><p>예</p></td>
<td><p>동일한 사용자 계정에 연결</p></td>
<td><ul>
<li><p>EAC: <strong>받는 사람</strong> &gt; <strong>사서함</strong> &gt; <strong>사서함에 연결</strong></p></li>
<li><p>셸: <strong>Connect-Mailbox</strong> cmdlet</p></li>
</ul></td>
</tr>
<tr class="even">
<td><ul>
<li><p>EAC: <strong>받는 사람</strong> &gt; <strong>사서함</strong> &gt; <strong>삭제</strong></p></li>
<li><p>셸: <strong>Remove-Mailbox</strong> cmdlet</p></li>
</ul></td>
<td><p>사용 안 함</p></td>
<td><p>아니요</p></td>
<td><ul>
<li><p>다른 사용자 계정에 연결</p></li>
<li><p>다른 사서함으로 복원 합니다.</p></li>
</ul></td>
<td><ul>
<li><p>EAC: <strong>받는 사람</strong> &gt; <strong>사서함</strong> &gt; <strong>사서함에 연결</strong></p></li>
<li><p>셸: <strong>Connect-Mailbox</strong> cmdlet</p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>셸: <strong>New-MailboxRestore</strong> cmdlet</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>다른 사서함 데이터베이스로 이동</p></td>
<td><p>SoftDeleted</p></td>
<td><p>예</p></td>
<td><ul>
<li><p>다른 사용자 계정에 연결</p></li>
<li><p>다른 사서함으로 복원 합니다.</p></li>
</ul></td>
<td><ul>
<li><p>EAC: <strong>받는 사람</strong> &gt; <strong>사서함</strong> &gt; <strong>사서함에 연결</strong></p></li>
<li><p>셸: <strong>Connect-Mailbox</strong> cmdlet</p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>셸: <strong>New-MailboxRestore</strong> cmdlet</p></li>
</ul></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 연결이 끊긴된 사서함 설명서

다음 표에 연결이 끊긴된 사서함을 관리 하는데 도움이 되는 항목에 대 한 링크를 포함 합니다. 연결이 끊어진된 사용자 사서함, 연결 된 사서함, 리소스 사서함 및 공유 사서함을 관리 하는입니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="disable-or-delete-a-mailbox-exchange-2013-help.md">사용 하지 않거나 사서함 삭제</a></p></td>
<td><p>사용 하지 않도록 설정 하거나 사서함을 삭제 하는 방법에 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-a-disabled-mailbox-exchange-2013-help.md">비활성화 된 사서함에 연결</a></p></td>
<td><p>기존 사용자 계정에 사용할 수 없는 사서함을 연결 하는 방법에 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="connect-or-restore-a-deleted-mailbox-exchange-2013-help.md">삭제 된 사서함을 복원 또는 연결</a></p></td>
<td><p>사용자 계정에 삭제 된 사서함을 연결 하거나 기존 사서함을 삭제 된 사서함의 내용을 복원 하는 방법에 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="restore-a-soft-deleted-mailbox-exchange-2013-help.md">일시 삭제 된 사서함 복원</a></p></td>
<td><p>사용자 계정에 일시 삭제 된 사서함을 연결 하거나 기존 사서함을 일시적으로 삭제 된 사서함을 복원 하는 방법에 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mailbox-restore-requests-exchange-2013-help.md">사서함 복원 요청 관리</a></p></td>
<td><p>셸을 사용 하 여 사서함 복원 요청을 관리 하는 방법에 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><a href="permanently-delete-a-mailbox-exchange-2013-help.md">사서함을 영구적으로 삭제</a></p></td>
<td><p>사서함을 영구적으로 삭제 하는 방법에 알아봅니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

