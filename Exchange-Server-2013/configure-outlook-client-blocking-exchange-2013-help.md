---
title: '차단 하는 Outlook 클라이언트를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 차단 하는 Outlook 클라이언트를 구성 합니다.
ms:assetid: 3a579c83-8bc7-4adc-a25c-8eb6eed7220c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335207(v=EXCHG.150)
ms:contentKeyID: 51407689
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 차단 하는 Outlook 클라이언트를 구성 합니다.

 

_**적용 대상:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Exchange Server 2013 메시징 레코드 관리 (MRM)에 대 한 보존 정책 또는 관리 되는 폴더를 사용할 수 있습니다. Microsoft Outlook 2010 를 실행 하는 사용자만 하며 나중에 보존 정책에 대 한 모든 클라이언트 기능에 대 한 액세스를 포함 합니다. 그러나 보존 정책은 관리 하는 폴더 도우미에 의해, 사용자가 사용 되는 Outlook 클라이언트 버전에 관계 없이 사서함 서버에 적용 됩니다. 이전 버전의 Outlook 클라이언트에서 이러한 기능 MRM 기능을 제공 하지 않습니다. 예, Outlook 2007에는 보존 정책을 지원 하지 않으므로, 사용자는 항목 또는 폴더에 개인 태그를 적용할 수 없습니다.

Exchange 사서함에 액세스 하지 못하도록 Outlook 의 이전 버전을 실행 하는 사용자를 차단할 수 있습니다. 또한 당 클라이언트 액세스 서버 별로 또는 당 사서함에 대 한 액세스를 차단할 수 있습니다.

MRM과 관련된 기타 관리 작업에 대한 자세한 내용은 [메시징 레코드 관리 절차](messaging-records-management-procedures-exchange-2013-help.md)를 참조하십시오.

## 클라이언트 응용 프로그램 및 버전에 의해 MRM 기능 사용 가능 여부

다음 표에서 다양 한 클라이언트 응용 프로그램 및 버전에서 사용할 수 있는 MRM 기능을 보여줍니다.

### MRM 기능

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>클라이언트 응용 프로그램</th>
<th>사용 가능한 MRM 클라이언트 기능</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 및 Outlook 2010</p></td>
<td><p>모두</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>관리되는 폴더</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2003 와 이전</p></td>
<td><p>지원되지 않음</p></td>
</tr>
<tr class="even">
<td><p>다른 전자 메일 클라이언트 소프트웨어</p></td>
<td><p>None</p></td>
</tr>
</tbody>
</table>


다음 표에서 Outlook 에 대 한 버전 번호를 표시 합니다.

### Outlook 버전

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Outlook 버전</th>
<th>버전 번호</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>14</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>12</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2003</p></td>
<td><p>11</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2002</p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2000</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 98</p></td>
<td><p>8.5</p></td>
</tr>
<tr class="even">
<td><p>Outlook 97</p></td>
<td><p>8</p></td>
</tr>
</tbody>
</table>



> [!NOTE]  
> 모든 변경 작업을 수행 하기 전에 핫픽스와 서비스 팩 출시 메모 클라이언트 버전 문자열에 영향을 줄 수 있습니다. 서버쪽 Exchange 구성 요소에 로그온 하려면 MAPI 사용 해야 하기 때문에 클라이언트 액세스를 제한할 때 주의 해야 합니다. 일부 구성 요소 구성 요소 이름 (예: SMTP 또는 OLE DB)으로 클라이언트 버전을 보고, 다른 사용자에 게 하는 동안 보고서 Exchange 빌드 번호 (예: 6.0.4712.0). 이러한 이유로 6로 시작 하는 버전 번호를 포함 하는 클라이언트에 대 한 제한 되지 않도록 합니다. &lt;<EM>x</EM>합니다. <EM>x</EM>. &gt;. 예, <STRONG>0.0.0-6.5535.65535.65535</STRONG>지정 하는 대신 완전히, MAPI 액세스를 방지 하기 위해 범위를 지정 두 서버 구성 요소에 로그온 할 수 있도록 합니다. 예, 다음을 지정: <STRONG>0.0.0-5.9.9; 7.0.0-</STRONG>합니다.



이러한 절차를 수행한 후에 사용자가 자신의 사서함에 액세스 하지 못하도록 차단 되는 경우 받게 됩니다 다음과 같은 경고 메시지가 유의 합니다.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Exchange 서버 관리자를 사용 하는 Outlook 의 버전을 차단 했습니다. 프로그램 관리자에 게 문의 합니다.</p></td>
</tr>
</tbody>
</table>


MRM 기능 OutlookOutlook 2010 보다 이전 버전을 실행 하는 전자 메일 클라이언트에 대 한 지원 되지 않습니다는 경고를 무시 하도록 셸에서 **New-Mailbox**, **Enable-Mailbox**및 **Set-Mailbox** cmdlet의 *ManagedFolderMailboxPolicyAllowed* 매개 변수를 사용할 수 있습니다. 관리 되는 폴더 사서함 정책을 *ManagedFolderMailboxPolicy* 매개 변수를 사용 하 여 사서함에 게 할당 되 면 *ManagedFolderMailboxPolicyAllowed* 매개 변수를 사용 하지 않으면 기본적으로는 경고가 표시 됩니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

## 무슨 작업을 하고 싶으십니까?

## 블록 버전의 Outlook 사서함 별로

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "사용자 사서함" 항목.

이 예제에서는 11.8010.8036 이전의 모든 Outlook 버전을 차단합니다.

```powershell
Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions "-11.8010.8036"
```

Outlook 의 버전에 의해 차단 되는 사서함에 대 한 액세스를 복원 하는이 예제입니다.

```powershell
Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions $null
```

구문과 매개 변수에 대한 자세한 내용은 [Set-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb125264\(v=exchg.150\))를 참조하십시오.

## 클라이언트 액세스 서버에서 블록 Outlook 버전

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "RPC 클라이언트 액세스 설정" 항목.

이 예제에서는 버전 12.0.0는 Exchange 2010 또는 이후 클라이언트 액세스 서버에 있는 사서함에 액세스 하지 못하도록 하기 전에 Outlook 클라이언트를 차단 합니다.


> [!IMPORTANT]  
> <EM>BlockedClientVersions</EM> 매개 변수에 사용되는 값은 예로 제공됩니다. <CODE>%ExchangeInstallPath%Logging\RPC Client Access</CODE>에 있는 RPC 클라이언트 액세스 로그 파일을 구문 분석하면 정확한 클라이언트 소프트웨어 버전을 확인할 수 있습니다.


```powershell
Set-RpcClientAccess -Server CAS01 -BlockedClientVersions "0.0.0-5.65535.65535;7.0.0;8.02.4-11.65535.65535"
```

자세한 구문 및 매개 변수 정의 대 한 [Set-RpcClientAccess](https://technet.microsoft.com/ko-kr/library/dd351072\(v=exchg.150\))를 참조 하십시오.

