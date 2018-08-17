---
title: '사용자의 사서함에서 삭제 된 메시지를 복구 합니다.: Exchange 2013 Help'
TOCTitle: 사용자의 사서함에서 삭제 된 메시지를 복구 합니다.
ms:assetid: 9e0e34ce-efc5-454e-8d15-57b4da867f12
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff660637(v=EXCHG.150)
ms:contentKeyID: 50556042
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자의 사서함에서 삭제 된 메시지를 복구 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

(이 항목은 관리자를 위한 Exchange 합니다.)

관리자가 검색 하 고 사용자의 사서함에서 삭제 된 전자 메일 메시지를 복구할 수 있습니다. 예: 사용자 사서함에 할당 된 보존 정책 (비우기) (지운 편지함 복구 기능 Outlook 또는 Outlook Web App )을 사용 하 여 사용자 또는 자동화 된 프로세스에 의해 삭제 된 항목에 의해 영구적으로 삭제 하는 항목이 포함 됩니다. 이러한 경우에는 사용자가 제거 된 항목을 복구할 수 없습니다. 하지만 관리자가 해당 항목에 대 한 삭제 된 항목 보존 기간 기간이 만료 되지 않도록 하는 경우 제거 된 메시지를 복구할 수 있습니다.


> [!NOTE]
> 이 절차를 사용하면 삭제된 항목(단일 항목 복구 또는 소송 자료 보호를 사용하도록 설정된 경우 Recoverable Items\Purges 폴더로 이동됨)을 검색 및 복구할 수 있는 것은 물론이고 사서함의 다른 폴더에 있는 항목을 검색하여 원본 사서함에서 항목을 삭제할 수도 있습니다(<EM>검색 및 제거</EM>).



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15 ~ 30분

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 단일 항목 복구를 복구 하려는 항목을 삭제 하기 전에 사서함에 대해 활성화 되어야 합니다. Exchange Online 단일 항목 복구는 새 사서함을 만들 때 기본적으로 활성화 됩니다. Exchange 2013 사서함을 만들 때 단일 항목 복구 불가능 합니다. 자세한 내용은 [사서함에 대 한 단일 항목 복구를 사용 하지 않도록 설정 하거나 사용](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md)을 참조 하십시오.

  - 항목을 검색 및 복구하려면 다음 정보가 있어야 합니다.
    
      - **원본 사서함**   검색 중인 사서함입니다.
    
      - **대상 사서함**   메시지 복구할 수 검색 사서함입니다. Exchange 설치 프로그램을 기본 검색 사서함을 만듭니다. Exchange Online 기본적으로 검색 사서함도 생성 됩니다. 필요한 경우에 추가 검색 사서함을 만들 수 있습니다. 자세한 내용은 [검색 사서함 만들기](create-a-discovery-mailbox-exchange-2013-help.md)을 참조 하십시오.
        

        > [!NOTE]
        > <STRONG>Search-Mailbox</STRONG> cmdlet을 사용할 경우 검색 사서함이 아닌 대상 사서함을 지정할 수도 있습니다. 하지만 원본과 대상 사서함으로 동일한 사서함을 지정할 수는 없습니다.

    
      - **검색 조건**   조건에는 보낸 사람이나 받는 사람 또는 메시지의 키워드(단어 또는 구)가 포함됩니다.

  - 이 항목 PowerShell을 사용 하 여 사용자의 사서함에서 삭제 된 항목을 복구 하에 중점을 둡니다. 또한를 찾아 삭제 된 항목 PST 파일을 내보낼 GUI 기반 원본 위치 eDiscovery 도구를 사용할 수 있습니다. 사용자가 사서함에 삭제 된 메시지를 복원 하려면이 PST 파일을 사용 합니다. 자세한 내용은 [사용자의 사서함-관리자 도움말 항목을 삭제 된 복구](https://go.microsoft.com/fwlink/p/?linkid=722928)을 참조 하십시오.

## (선택 사항) 1 단계: 원격 PowerShell을 사용 하는 Exchange Online에 연결

Exchange Online 또는 Office 365 조직이 있는 경우이 단계를 수행 해야 합니다. Exchange 2013 조직이 있는 경우 다음 단계로 이동 하 고 Exchange 관리 셸 에서 명령을 실행 합니다.

1.  로컬 컴퓨터에서 Windows PowerShell을 열고 다음 명령을 실행합니다.
    
        $UserCredential = Get-Credential
    
    **Windows PowerShell 자격 증명 요청** 대화 상자에서 Office 365 전역 관리자 계정의 사용자 이름 및 암호를 입력한 다음 **확인**을 클릭합니다.

2.  다음 명령을 실행합니다.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  다음 명령을 실행합니다.
    
        Import-PSSession $Session

4.  Exchange Online 조직에 연결 하려는 있는지를 확인 하려면 조직에 있는 모든 사서함의 목록을 가져오려면 다음 명령을 실행 합니다.
    
        Get-Mailbox

자세한 내용은 하거나 Exchange Online 조직에 연결할 때 문제가 있으면 [원격 PowerShell을 사용 하는 Exchange Online에 연결](https://go.microsoft.com/fwlink/p/?linkid=517283)을 참조 하십시오.

## 2 단계: 검색 하 고 누락 된 항목을 복구

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "원본 위치 eDiscovery" 항목.


> [!NOTE]
> 누락 된 항목을 검색 하려면 Exchange 관리 센터 (EAC)의 원본 위치 eDiscovery를 사용할 수 있습니다. 그러나 EAC를 사용 하는 경우 복구 가능한 항목 폴더에는 검색을 제한할 수 없습니다. 검색 매개 변수를 일치 하는 메시지는 삭제 하지 되기 하는 경우에 반환 됩니다. 지정 된 검색 사서함으로 복구한 후 검색 결과 검토 하 고 나머지 메시지는 사용자의 사서함을 복구 하거나.pst 파일을 내보내 하기 전에 불필요 한 메시지를 제거 해야할 수 있습니다.<BR>EAC를 사용하여 원본 위치 eDiscovery 검색을 수행하는 방법에 대한 자세한 내용은 <A href="create-an-in-place-ediscovery-search-exchange-2013-help.md">원본 위치 eDiscovery 검색 만들기</A> 항목을 참조하십시오.



복구 프로세스의 첫 번째 단계는 원본 사서함에서 메시지를 검색하는 것입니다. 다음 방법 중 하나를 사용하여 사용자 사서함을 검색하고 메시지를 검색 사서함으로 복사합니다.

이 예에서는 April Stewart의 사서함에서 다음 조건을 충족하는 메시지를 검색합니다.

  - 보낸 사람: Ken Kwok

  - 키워드: Seattle

<!-- end list -->

    Search-Mailbox "April Stewart" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "Discovery Search Mailbox" -TargetFolder "April Stewart Recovery" -LogLevel Full


> [!NOTE]
> <STRONG>Search-Mailbox</STRONG> cmdlet을 사용할 때 <EM>SearchQuery</EM> 매개 변수로 KQL(Keyword Query Language) 형식의 쿼리를 지정하여 검색 범위를 지정할 수 있습니다. <EM>SearchDumpsterOnly</EM> 스위치를 사용하여 복구할 수 있는 항목 폴더에 있는 항목만 검색할 수도 있습니다.



구문과 매개 변수에 대한 자세한 내용은 [Search-Mailbox](https://technet.microsoft.com/ko-kr/library/dd298173\(v=exchg.150\))를 참조하십시오.

**작동 여부는 어떻게 확인합니까?**

복구할 메시지가 검색되었는지 확인하려면 대상 사서함으로 선택한 검색 사서함에 로그온하여 검색 결과를 검토합니다.

## 3 단계: 복구 된 항목 복원

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "원본 위치 eDiscovery" 항목.


> [!NOTE]
> 복구된 항목을 복원하는 데 EAC를 사용할 수 없습니다.



메시지를 검색 사서함으로 복구 되었지만 후 **Search-Mailbox** cmdlet을 사용 하 여 사용자의 사서함 복원할 수 있습니다. 또한 Exchange 2013.pst 파일에서 메시지를 가져오거나 내보내려면 메시지를 **New-MailboxExportRequest** 및 **New-MailboxImportRequest** cmdlet을 사용할 수 있습니다.

## 셸을 사용하여 메시지 복원

이 예에서는 April Stewart의 사서함으로 메시지를 복원하고 검색 사서함에서 삭제합니다.

    Search-Mailbox "Discovery Search Mailbox" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "April Stewart" -TargetFolder "Recovered Messages" -LogLevel Full -DeleteContent

구문과 매개 변수에 대한 자세한 내용은 [Search-Mailbox](https://technet.microsoft.com/ko-kr/library/dd298173\(v=exchg.150\))를 참조하십시오.

**작동 여부는 어떻게 확인합니까?**

메시지가 사용자 사서함으로 복구되었는지 확인하려면 사용자에게 위의 명령에 지정된 대상 폴더에서 메시지를 검토하도록 합니다.

## (Exchange 2013) 셸을 사용 하 여 내보내기 및.pst 파일에서 메시지를 가져오려면

Exchange 2013 사서함에서 내용을.pst 파일로 내보낼 수 있으며.pst 파일의 내용을 사서함으로 가져올 키를 누릅니다. 사서함 가져오기 및 내보내기에 대 한 자세한 내용은, [사서함 가져오기 및 내보내기 요청](mailbox-import-and-export-requests-exchange-2013-help.md)를 참조 하십시오. Exchange Online 에서이 작업을 수행할 수 없습니다.

이 예에서는 다음 설정을 사용하여 검색 사서함에 있는 April Stewart Recovery 폴더의 메시지를 .pst 파일로 내보냅니다.

  - **사서함**   검색 사서함

  - **원본 폴더**   April Stewart Recovery

  - **ContentFilter**   April travel plans

  - **PST 파일 경로**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxExportRequest -Mailbox "Discovery Search Mailbox" -SourceRootFolder "April Stewart Recovery" -ContentFilter {Subject -eq "April travel plans"} -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst

구문과 매개 변수에 대한 자세한 내용은 [New-MailboxExportRequest](https://technet.microsoft.com/ko-kr/library/ff607299\(v=exchg.150\))를 참조하십시오.

이 예에서는 다음 설정을 사용하여 .pst 파일에서 April Stewart의 사서함에 있는 Recovered By Helpdesk 폴더로 메시지를 가져옵니다.

  - **사서함**   April Stewart

  - **대상 폴더**   Recovered By Helpdesk

  - **PST 파일 경로**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxImportRequest -Mailbox "April Stewart" -TargetRootFolder "Recovered By Helpdesk" -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst 

구문과 매개 변수에 대한 자세한 내용은 [New-MailboxImportRequest](https://technet.microsoft.com/ko-kr/library/ff607310\(v=exchg.150\))를 참조하십시오.

**작동 여부는 어떻게 확인합니까?**

메시지가 .pst 파일로 내보내졌는지 확인하려면 Outlook에서 .pst 파일을 열고 내용을 검사합니다. .pst 파일에서 메시지를 가져왔는지 확인하려면 사용자에게 위의 명령에 지정된 대상 폴더의 내용을 검사하도록 합니다.

## 추가 정보

  - *단일 항목 복구*는 관리자가 제거 된 사용자가 또는 보존 정책에 의해 해당 항목에 대 한 삭제 된 항목 보존 기간 만료 되지 않았으면으로 하는 메시지를 복구할 수 있도록 하는 하 여 삭제 된 항목을 복구 하는 기능 활성화 됩니다. 단일 항목 복구 하는 방법에 대 한 자세한 내용은, [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)를 참조 하십시오.

  - Exchange Online 사서함은 기본적으로 14 일에 대 한 삭제 된 항목을 유지 하도록 구성 됩니다. 최대 30 일에이 설정을 변경할 수 있습니다. Exchange 2013 사서함 데이터베이스는 기본적으로 14 일에 대 한 삭제 된 항목을 유지 하도록 구성 됩니다. 사서함 또는 사서함 데이터베이스에 대 한 삭제 된 항목 보존 설정을 구성할 수 있습니다. 자세한 내용은 다음을 참조 합니다.
    
      - [Exchange Online 사서함에 대 한 변경 얼마나 오래 영구적으로 삭제 된 항목 보관 됩니다.](https://technet.microsoft.com/ko-kr/library/dn163584\(v=exchg.150\))
    
      - [삭제 된 항목 보존 및 복구 가능한 항목 할당량 구성](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)

  - 앞에서 설명한 것 처럼를 찾아 삭제 된 항목 PST 파일을 내보낼 수도 원본 위치 eDiscovery 도구를 사용할 수 있습니다. 사용자가 사서함에 삭제 된 메시지를 복원 하려면이 PST 파일을 사용 합니다. 자세한 내용은 [삭제 된 사용자의 사서함-관리자 도움말 항목을 복구](https://go.microsoft.com/fwlink/p/?linkid=722928)을 참조 하십시오.

  - 사용자는 지워진 하지 않은 경우 및 해당 항목에 대 한 삭제 된 항목 보존 기간 기간이 만료 되지 않도록 하는 경우 삭제 된 항목을 복구할 수 있습니다. 사용자를 복구할 수 있는 항목 폴더에서 삭제 된 항목을 복구 해야하는 경우 다음 항목을 가리킵니다.
    
      - [삭제 된 Outlook 2010의 항목 복구](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [삭제 된 Outlook 2013의 항목 복구](https://go.microsoft.com/fwlink/p/?linkid=624829)
    
      - [삭제 된 항목 또는 Outlook Web App에서 전자 메일을 복구 합니다.](https://go.microsoft.com/fwlink/p/?linkid=524924)

  - 이 항목에서는 검색 하 고 누락 된 항목을 복구 **Search-Mailbox** cmdlet을 사용 하는 방법을 보여줍니다. 이 cmdlet을 사용 하는 경우에 한번에 하나씩만 사서함을 검색할 수 있습니다. 동시에 여러 사서함을 검색 하려면 [원본 위치 eDiscovery](in-place-ediscovery-exchange-2013-help.md) (EAC)의 Exchange 관리 센터에서 또는 Windows PowerShell 에서 [New-MailboxSearch](https://technet.microsoft.com/ko-kr/library/dd298064\(v=exchg.150\)) cmdlet을 사용할 수 있습니다.

  - 이 절차에 대 한 검색 및 복구를 사용 하 여 외에도 지운 편지함, 비슷한 절차를을 사용 하 여 사용자 사서함에서 항목을 검색 하 고 원본 사서함에서 이러한 항목을 삭제 하려면 수도 있습니다. 자세한 내용은 [메시지-관리자 도움말에 대 한 검색 및 삭제](search-for-and-delete-messages-admin-help-exchange-2013-help.md)을 참조 하십시오.

