---
title: '하이브리드 배포용으로 레거시 온-프레미스 공용 폴더 구성: Exchange 2013 Help'
TOCTitle: 하이브리드 배포용으로 레거시 온-프레미스 공용 폴더 구성
ms:assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn249373(v=EXCHG.150)
ms:contentKeyID: 54913269
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 하이브리드 배포용으로 레거시 온-프레미스 공용 폴더 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2018-05-22_

**요약:**  이 문서의 단계를 사용하여 Office 365dhk Exchange 2007 또는 Exchange 2010 온-프레미스 배포 간에 공용 폴더를 동기화할 수 있습니다.

하이브리드 배포에서는 사용자가 Exchange Online이나 온-프레미스 중 하나 또는 둘 다에 있을 수 있으며 공용 폴더는 Exchange Online이나 온-프레미스 중 하나에 있습니다. 공용 폴더는 한 곳에만 있을 수 있으므로 Exchange Online 또는 온-프레미스 중에서 공용 폴더를 배치할 곳을 결정해야 합니다. 두 위치에 모두 공용 폴더를 배치할 수는 없습니다. 공용 폴더 사서함은 디렉터리 동기화 서비스에 의해 Exchange Online에 동기화됩니다. 그러나 메일 사용 가능 공용 폴더는 프레미스 간에 동기화되지 않습니다.

이 항목에서는 사용자가 Office 365에 있고 Exchange 2010 SP3 또는 Exchange 2007 SP3 RU10 공용 폴더가 온-프레미스에 있는 경우 메일 사용 가능 공용 폴더를 동기화하는 방법에 대해 설명합니다. 그러나 온-프레미스에서 MailUser 개체로 표시되지 않는 Office 365 사용자(대상 공용 폴더 계층 구조의 로컬)는 레거시 또는 Exchange 2013 온-프레미스 공용 폴더에 액세스할 수 없습니다.


> [!NOTE]
> 이 항목에서는 Exchange 2010 SP3 및 Exchange 2007 SP3 RU10 서버를 <EM>레거시 Exchange 서버</EM>로 지칭합니다.



다음 스크립트를 사용하여 메일 사용 가능 공용 폴더를 동기화합니다. 이 스크립트는 온-프레미스 환경에서 실행되는 Windows 작업에 의해 시작됩니다.

1.  `Sync-MailPublicFolders.ps1`   이 스크립트는 로컬 Exchange 온-프레미스 배포의 메일 사용이 가능한 공용 폴더 개체를 Office 365과 동기화합니다. 또한 이 스크립트는 로컬 Exchange 온-프레미스 배포를 마스터로 사용하여 O365에 적용해야 하는 변경 내용을 결정합니다. 이 스크립트는 로컬 온-프레미스 Exchange 배포에 있는 항목을 기준으로 O365 Active Directory에 메일 사용이 가능한 공용 폴더 개체를 만들거나, 업데이트하거나, 삭제합니다.

2.  `SyncMailPublicFolders.strings.psd1`   앞에 나온 동기화 스크립트에서 사용하는 지원 파일로, 위의 스크립트와 같은 위치에 복사해야 합니다.

이 절차를 완료하면 온-프레미스 및 Office 365 사용자가 같은 온-프레미스 공용 폴더 인프라에 액세스할 수 있습니다.

## 공용 폴더를 사용할 수 있는 하이브리드 버전 Exchange

다음 표에서는 지원되는 사용자 사서함과 공용 폴더의 버전 및 위치 조합에 대해 설명합니다. "하이브리드 해당 없음"도 지원되는 시나리오이기는 하지만, 공용 폴더와 사용자가 같은 위치에 있으므로 하이브리드 시나리오로 간주되지 않습니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>온-프레미스 Exchange 2007 또는 Exchange 2010 사용자 사서함</th>
<th>온-프레미스 Exchange 2013 사용자 사서함</th>
<th>Exchange Online 사용자 사서함</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>온-프레미스 Exchange 2007 또는 Exchange 2010 공용 폴더</p></td>
<td><p>하이브리드 해당 없음</p></td>
<td><p>하이브리드 해당 없음</p></td>
<td><p>지원됨</p></td>
</tr>
<tr class="even">
<td><p>온-프레미스 Exchange 2013 공용 폴더</p></td>
<td><p>하이브리드 해당 없음</p></td>
<td><p>하이브리드 해당 없음</p></td>
<td><p>지원됨</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Online 공용 폴더</p></td>
<td><p>지원되지 않음</p></td>
<td><p>지원됨</p></td>
<td><p>하이브리드 해당 없음</p></td>
</tr>
</tbody>
</table>


Exchange 2003 공용 폴더와의 하이브리드 구성은 지원되지 않습니다. 조직에서 Exchange 2003을 실행하는 경우에는 모든 공용 폴더 데이터베이스 및 복제본을 Exchange 2007 SP3 RU10 이상으로 이동해야 합니다. 공용 폴더 복제본이 Exchange 2003에 남아 있어서는 안 됩니다.


> [!NOTE]
> Outlook 2016은 Exchange 2007 레거시 공용 폴더 액세스를 지원하지 않습니다. 사용자가 Outlook 2016을 사용하는 경우 공용 폴더를 좀 더 최신 버전의 Exchange로 이동해야 합니다. Exchange 2007 및 이전 버전과의 Outlook 2016 및 Office 2016 호환성에 대한 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=849053">이 문서</A>에서 찾을 수 있습니다.



## 1단계: 시작하기 전에 알아야 할 내용

1.  이러한 지침에서는 하이브리드 구성 마법사를 사용하여 온-프레미스 및 Exchange Online 환경을 구성하고 동기화했으며, 사용자 대부분의 자동 검색에 사용되는 DNS 레코드가 온-프레미스 끝점을 참조한다고 가정합니다. 자세한 내용은 [하이브리드 구성 마법사](https://technet.microsoft.com/ko-kr/library/hh529921\(v=exchg.150\))를 참조하십시오.

2.  이러한 지침에서는 온-프레미스 레거시 Exchange 서버에서 Outlook Anywhere가 사용되도록 설정되고 작동된다고 가정합니다. Outlook Anywhere를 사용하도록 설정하는 방법에 대한 자세한 내용은 [Outlook Anywhere](outlook-anywhere-exchange-2013-help.md)를 참조하세요.

3.  Exchange와 Office 365의 하이브리드 배포를 위한 레거시 공용 폴더 동시 사용을 구현하려면 가져오기 절차 중에 충돌을 해결해야 할 수 있습니다. 충돌은 메일 사용 가능 공용 폴더에 할당된 라우팅할 수 없는 전자 메일 주소, Office 365의 다른 사용자/그룹과의 충돌 및 기타 특성으로 인해 발생할 수 있습니다.

4.  이러한 지침에서는 공용 폴더를 지원하는 버전으로 Exchange Online 조직을 업그레이드했다고 가정합니다.

5.  Exchange Online에서 Organization Management 역할 그룹의 구성원이어야 합니다. 이 역할 그룹은 Exchange Online 구독 시 할당되는 사용 권한과는 다릅니다. Organization Management 역할 그룹을 사용하도록 설정하는 방법에 대한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)를 참조하십시오.

6.  Exchange 2010에서는 Organization Management 또는 Server Management RBAC 역할 그룹의 구성원이어야 합니다. 자세한 내용은 [역할 그룹에 구성원 추가](https://go.microsoft.com/fwlink/?linkid=299212)를 참조하세요.

7.  Exchange 2007에서는 Exchange Organization Administrator 역할 또는 Exchange Server Administrator 역할을 할당받아야 합니다. 또한 대상 서버에 대한 로컬 관리자 그룹 및 Public Folder Administrator 역할을 할당받아야 합니다. 자세한 내용은 [관리자 역할에 사용자 또는 그룹을 추가하는 방법](https://go.microsoft.com/fwlink/p/?linkid=81779)을 참조하세요.

8.  Windows Server 2008 x64에서 Exchange Server 2007을 실행하는 경우 [Windows Server 2008 x64 Edition용 Windows PowerShell 2.0 및 WinRM 2.0](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)으로 업그레이드해야 합니다. Windows Server 2003 x64에서 Exchange Server 2007을 실행하는 경우에는 Windows PowerShell 2.0으로 업그레이드해야 합니다. 자세한 내용은 [Windows Server 2003 x64 Edition용 업데이트](https://www.microsoft.com/ko-kr/download/details.aspx?id=10512)를 참조하세요.

9.  프레미스 간 공용 폴더에 액세스하려면 사용자는 Outlook 클라이언트를 2012년 11월 Outlook 공개 업데이트 이상으로 업그레이드해야 합니다.
    
    1.  Outlook 2010용 2012년 11월 Outlook 업데이트를 다운로드하려면 [Microsoft Outlook 2010 (KB2687623) 32비트 버전용 업데이트](https://www.microsoft.com/ko-kr/download/details.aspx?id=35702)를 참조하세요.
    
    2.  Outlook 2007용 2012년 11월 Outlook 업데이트를 다운로드하려면 [Microsoft Office Outlook 2007용 업데이트(KB2687404)](https://www.microsoft.com/ko-kr/download/details.aspx?id=35718)를 참조하세요.

10. 크로스-프레미스 레거시 공용 폴더의 경우 Mac용 Outlook 2016(및 이전 버전) 및 Office 365의 Mac용 Outlook이 지원되지 않으므로 사용자가 공용 폴더와 같은 위치에 있어야 Mac용 Outlook 또는 Office 365의 Mac용 Outlook에 액세스할 수 있습니다. 또한 사서함이 Exchange Online에 있는 사용자는 Outlook Web App을 사용하여 온-프레미스 공용 폴더에 액세스할 수 없습니다.

11. 이 문서의 지침에 따라 하이브리드 배포에 대한 온-프레미스 공용 폴더를 구성한 경우, 추가 단계를 수행하지 않으면 조직 외부의 사용자가 온-프레미스 공용 폴더에 메시지를 전송할 수 없습니다. 공용 폴더에 대한 허용 도메인을 내부 릴레이(자세한 내용은 [Exchange Online에서 허용 도메인 관리](https://technet.microsoft.com/ko-kr/library/jj945194\(v=exchg.150\)) 참조)로 설정하거나 [디렉터리 기반 Edge 차단을 사용하여 잘못된 받는 사람에게 전송된 메시지 거부](https://technet.microsoft.com/ko-kr/library/dn600322\(v=exchg.150\))에 설명된 대로 DBEB(디렉터리 기반 Edge 차단)를 사용하지 않도록 설정할 수 있습니다.

## 2단계: 원격 공용 폴더를 검색 가능하도록 설정

1.  공용 폴더가 Exchange 2010 이상 서버에 있으면 공용 폴더 데이터베이스가 있는 모든 사서함 서버에 클라이언트 액세스 서버 역할을 설치해야 합니다. 그러면 Microsoft Exchange RpcClientAccess 서비스를 실행할 수 있게 되어 모든 클라이언트가 공용 폴더에 액세스할 수 있습니다. Exchange 2007 공용 폴더 서버의 경우에는 클라이언트 액세스 역할이 필요하지 않으므로 이 단계를 수행할 필요가 없습니다. 자세한 내용은 [Exchange Server 2010 설치](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)를 참조하세요. Exchange 2007 공용 폴더의 경우에는 이 단계를 수행할 필요가 없습니다.
    

    > [!NOTE]
    > 이 서버는 클라이언트 액세스 부하 분산의 일부분이 아니어도 됩니다. 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/ff625247(v=exchg.141).aspx">Exchange 2010의 부하 분산 이해</A>를 참조하세요.



2.  각 공용 폴더 서버에 빈 사서함 데이터베이스를 만듭니다.
    
    Exchange 2010의 경우 다음 명령을 실행합니다. 이 명령은 부하 분산 장치를 프로비저닝하는 사서함에서 사서함 데이터베이스를 제외합니다. 그러면 이 데이터베이스에 새 사서함이 자동으로 추가되지 않습니다.
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true
    
    Exchange 2007의 경우 다음 명령을 실행합니다.
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    

    > [!NOTE]
    > 이 데이터베이스에는 3단계에서 만드는 프록시 사서함만 추가하는 것이 좋습니다. 이 사서함 데이터베이스에서 다른 사서함을 만들어서는 안 됩니다.



3.  새 사서함 데이터베이스 내에서 프록시 사서함을 만들고 주소록에서 해당 사서함을 숨깁니다. 이 사서함의 SMTP는 자동 검색에서 *DefaultPublicFolderMailbox* SMTP로 반환되므로 클라이언트는 이 SMTP를 확인하여 공용 폴더 액세스를 위해 레거시 Exchange 서버에 연결할 수 있습니다.
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs>
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  Exchange 2010의 경우 자동 검색에서 프록시 공용 폴더 사서함을 반환하도록 설정합니다. Exchange 2007의 경우에는 이 단계를 수행할 필요가 없습니다.
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  조직의 모든 공용 폴더 서버에 대해 위의 단계를 반복합니다.

## 3단계: 스크립트 다운로드

1.  [메일 사용이 가능한 공용 폴더 - 디렉터리 동기화 스크립트](https://www.microsoft.com/en-us/download/details.aspx?id=46381)에서 다음 파일을 다운로드하세요.
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  PowerShell을 실행할 로컬 컴퓨터에서 C:\\PFScripts 등의 위치에 파일을 저장합니다.

## 4단계: 디렉터리 동기화 구성

디렉터리 동기화 서비스에서는 메일 사용 가능 공용 폴더를 동기화하지 않습니다. 다음 스크립트를 실행하면 프레미스 간에 메일 사용 가능 공용 폴더가 동기화됩니다. 하이브리드 배포 시나리오에서는 크로스-프레미스 권한이 지원되지 않으므로 메일 사용이 가능한 공용 폴더에 할당된 특수 권한을 클라우드에서 다시 만들어야 합니다. 자세한 내용은 [Exchange Server 2013 하이브리드 배포](https://technet.microsoft.com/ko-kr/59e32000-4fcf-417f-a491-f1d8f9aeef9b\(exchg.150\)#doc)를 참조하세요.


> [!NOTE]
> 동기화된 메일 사용이 가능한 공용 폴더는 메일 흐름을 위한 메일 연락처 개체로 나타나며 Exchange 관리 센터에 표시되지 않습니다. Get-MailPublicFolder 명령을 참조하세요. 클라우드에서 SendAs 권한을 다시 만들려면 Add-RecipientPermission 명령을 사용합니다.



1.  레거시 Exchange 서버에서 다음 명령을 실행하여 로컬 온-프레미스 Active Directory의 메일 사용이 가능한 공용 폴더를 O365에 동기화합니다.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    여기서 `Credential`은 Office 365 사용자 이름 및 암호이고 `CsvSummaryFile`은 동기화 작업 및 오류를 기록하려는 .csv 형식 파일의 경로입니다.


> [!NOTE]
> 이 스크립트를 실행하기 전에 먼저 작업 환경에서 <CODE>-WhatIf</CODE> 매개 변수와 함께 스크립트를 실행하여 스크립트를 통해 수행될 작업을 시뮬레이트하는 것이 좋습니다.<BR>또한 이러한 스크립트를 매일 실행하여 메일 사용 가능 공용 폴더를 동기화하는 것이 좋습니다.



## 5단계: Exchange Online 사용자가 온-프레미스 공용 폴더에 액세스하도록 구성

이 절차의 마지막 단계에서는 Exchange Online 조직을 구성하고 레거시 온-프레미스 공용 폴더에 대한 액세스를 허용합니다.

Exchange Online 조직이 온-프레미스 공용 폴더에 액세스할 수 있도록 설정합니다. 이렇게 하려면 2단계: 원격 공용 폴더를 검색 가능하도록 설정에서 만든 모든 프록시 공용 폴더 사서함을 가리킵니다.

**Windows PowerShell**에서 다음 명령을 실행합니다.

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

Active Directory 동기화가 완료될 때까지 기다려야 변경 내용이 표시됩니다. 이 프로세스를 완료하는 데 최대 3시간 걸릴 수 있습니다. 3시간마다 발생하는 되풀이 동기화를 기다리지 않으려면 언제든지 강제로 디렉터리 동기화를 수행할 수 있습니다. 디렉터리 동기화를 강제로 수행하는 자세한 단계를 보려면 [강제 디렉터리 동기화](http://technet.microsoft.com/ko-kr/library/jj151771.aspx)를 참조하세요. Office 365는 이 명령에 제공된 공용 폴더 사서함 중 하나를 임의로 선택합니다.


> [!IMPORTANT]
> 온-프레미스에서 MailUser 개체로 표시되지 않는 Office 365 사용자(대상 공용 폴더 계층 구조의 로컬)는 레거시 또는 Exchange 2013 온-프레미스 공용 폴더에 액세스할 수 없습니다. 해결 방법에 대해서는 기술 자료 문서 <A href="https://go.microsoft.com/fwlink/p/?linkid=699451">Exchange Online 사용자가 온 프레미스 레거시 공용 폴더에 액세스할 수 없음</A>을 참조하세요.



## 작동 여부는 어떻게 확인합니까?

1.  Exchange Online의 사용자로 Outlook에 로그온하여 다음 공용 폴더 테스트를 수행합니다.
    
      - 계층 구조를 확인합니다.
    
      - 사용 권한을 확인합니다.
    
      - 공용 폴더를 만들고 삭제합니다.
    
      - 공용 폴더에 콘텐츠를 게시한 후 삭제합니다.

## Office 365의 새로운 기능


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning용 단축 아이콘" alt="LinkedIn Learning용 단축 아이콘" /> <strong>Office 365를 처음 사용하시나요?</strong><br />
LinkedIn Learning에서 제공하는 <a href="https://support.office.com/en-us/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>의 무료 비디오 과정을 확인해보세요.</p></td>
</tr>
</tbody>
</table>

