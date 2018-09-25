---
title: '메시지-관리자 도움말에 대 한 검색 및 삭제: Exchange 2013 Help'
TOCTitle: 메시지-관리자 도움말에 대 한 검색 및 삭제
ms:assetid: 8c36bb03-e716-4fdd-9958-4aa7a2a1db42
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff459253(v=EXCHG.150)
ms:contentKeyID: 52058007
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지-관리자 도움말에 대 한 검색 및 삭제

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-12-20_

관리자는 사용자 사서함을 검색 하 고 다음 사서함에서 메시지를 삭제 하려면 **Search-Mailbox** cmdlet을 사용할 수 있습니다.

한 번에 메시지를 검색하여 삭제하려면 *DeleteContent* 스위치와 함께 **Search-Mailbox** cmdlet을 실행합니다. 하지만, 이 경우 검색 결과를 미리 보거나 검색에 의해 반환되는 메시지 로그를 생성할 수 없으며, 삭제하면 안 되는 메시지를 실수로 삭제할 수 있습니다. 메시지를 삭제하기 전에 검색되는 메시지에 대한 로그를 미리 보려면 *LogOnly* 스위치와 함께 **Search-Mailbox** cmdlet을 실행합니다.

추가적인 안전 장치로서, *TargetMailbox* 및 *TargetFolder* 매개 변수를 사용하여 먼저 메시지를 다른 사서함에 복사할 수 있습니다. 이렇게 하면 삭제되는 메시지의 복사본을 보관하여 필요할 때 다시 액세스할 수 있습니다.

## 시작하기 전에 알아야 할 사항은 무엇입니까?

  - 예상 완료 시간: 10분 실제 시간은 사서함 및 검색 쿼리의 크기에 따라 다를 수 있습니다.

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 모두 검색 하 여 사용자의 사서함에서 메시지를 삭제 하려면 다음 관리 역할을 할당 해야 합니다.
    
      - **사서함 검색**   이 역할을 통해 사용자는 조직의 여러 사서함에 있는 메시지를 검색할 수 있습니다. 관리자에게는 기본적으로 이 역할이 할당되지 않습니다. 사서함을 검색할 수 있도록 이 역할을 자신에게 할당하려면 자신을 검색 관리 역할 그룹의 구성원으로 추가합니다. [Exchange eDiscovery 사용 권한 할당](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions)를 참조하세요.
    
      - **사서함 가져오기 내보내기**   이 역할을 사용 하면 사용자의 사서함에서 메시지를 삭제할 수 있습니다. 기본적으로이 역할은 모든 역할 그룹에 할당 되지 않습니다. 사용자의 사서함에서 메시지를 삭제 하려면 조직 관리 역할 그룹에는 사서함 가져오기 내보내기 역할을 추가할 수 있습니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 의 "역할을 역할 그룹에 게 추가" 섹션을 참조 하십시오.

  - 메시지를 삭제 하려는 사서함 단일 항목 복구를 사용할 수 있으면 먼저 기능을 비활성화 해야 합니다. 자세한 내용은 [사서함에 대 한 단일 항목 복구를 사용 하지 않도록 설정 하거나 사용](https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-user-mailboxes/enable-or-disable-single-item-recovery)을 참조 하십시오.

  - 메시지를 삭제 하려는 사서함은 보류 상태로 변경 하는 경우에 레코드 관리 또는 보류를 제거 하 고 사서함 콘텐츠를 삭제 하기 전에 법률 부서를 확인 하는 것이 좋습니다. 승인을 얻으려면 항목 [복구 가능한 항목 폴더를 정리](clean-up-the-recoverable-items-folder-exchange-2013-help.md)에 나열 된 단계를 수행 합니다.

  - 최대 10, 000 사서함 **Search-Mailbox** cmdlet을 사용 하 여 검색할 수 있습니다. Exchange Online 조직 이며 10, 000 개 이상의 사서함이 있을 경우 무제한 사서함을 검색 하려면 준수 검색 기능 (또는 해당 **New-ComplianceSearch** cmdlet)를 사용할 수 있습니다. 그런 다음 준수 검색을 통해 반환 되는 메시지를 삭제 하려면 **New-ComplianceSearchAction** cmdlet을 사용할 수 있습니다. 자세한 내용은 [Office 365 조직에서 전자 메일 메시지를 삭제 하 고 검색에 대 한](https://go.microsoft.com/fwlink/p/?linkid=786856)을 참조 하십시오.

  - ( *SearchQuery* 매개 변수를 사용 하 여) 하 여 검색 쿼리를 포함 하는 경우 **Search-Mailbox** cmdlet은 검색 결과에서 최대 10, 000 개의 항목이 반환 됩니다. 따라서 검색 쿼리를 포함 하는 경우에 10, 000 개 이상의 항목을 삭제 하려면 **Search-Mailbox** 명령을 여러 번 실행 해야할 수 있습니다.

  - **Search-Mailbox** cmdlet을 실행 하는 경우에 사용자의 보관 사서함을 검색 합니다. 마찬가지로, *DeleteContent* 스위치와 함께 **Search-Mailbox** cmdlet을 사용 하는 경우 기본 보관 사서함에 항목이 삭제 됩니다. 이 방지 하려면 *DoNotIncludeArchive* 스위치를 포함할 수 있습니다. 또한 예기치 않은 데이터 손실이 발생할 수 있으므로 사용 보관 자동 확장 된 Exchange Online 사서함에서 메시지를 삭제 하려면 *DeleteContent* 스위치를 사용 하지 않는 것이 좋습니다.

## 메시지 검색 및 검색 결과 기록

이 예에서는 April Stewart의 사서함에서 제목에 "Your bank statement" 구가 포함된 메시지를 검색하고 관리자 사서함의 SearchAndDeleteLog 폴더에 검색 결과를 기록합니다. 메시지는 대상 사서함에 복사되거나 대상 사서함에서 삭제되지 않습니다.

```powershell
Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full
```
이 예제에서는 모든 유형의 파일 이름에 "트로이" 단어를 포함 하 고 관리자의 사서함에 로그 메시지를 전송 하는 첨부 파일이 있는 메시지에 대 한 조직에서 모든 사서함을 검색 합니다.

```powershell
Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery attachment:trojan* -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full
```
구문과 매개 변수에 대한 자세한 내용은 [Search-Mailbox](https://technet.microsoft.com/ko-kr/library/dd298173\(v=exchg.150\))를 참조하십시오.

맨위로 돌아가기

## 메시지 검색 및 삭제

이 예에서는 April Stewart의 사서함에서 제목 필드에 "Your bank statement" 구가 포함된 메시지를 검색하고 검색 결과를 다른 폴더에 복사하지 않고 원본 사서함에서 메시지를 삭제합니다. 앞에서 설명한 것처럼 사용자 사서함에서 메시지를 삭제하려면 사서함 가져오기 내보내기 관리 역할이 할당되어 있어야 합니다.


> [!IMPORTANT]
> <EM>DeleteContent</EM> 스위치와 함께 <STRONG>Search-Mailbox</STRONG> cmdlet을 사용할 경우 메시지는 원본 사서함에서 영구 삭제됩니다. 영구히 메시지를 삭제하기 전에 <EM>LogOnly</EM> 스위치를 사용하여 검색으로 찾은 메시지에 대해 로그를 생성한 후 삭제하거나 해당 메시지를 다른 사서함에 복사한 후 원본 사서함에서 삭제하는 것이 좋습니다.



```powershell
Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -DeleteContent
```

이 예에서는 April Stewart의 사서함에서 제목 필드에 "Your bank statement" 구가 포함된 메시지를 검색하고 BackupMailbox 사서함의 AprilStewart-DeletedMessages 폴더에 검색 결과를 복사한 후 April 사서함에서 메시지를 삭제합니다.

```powershell
Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox "BackupMailbox" -TargetFolder "AprilStewart-DeletedMessages" -LogLevel Full -DeleteContent
```

이 예제에서는 "이이 파일 다운로드" 제목줄이 있는 메시지에 대 한 조직에서 모든 사서함을 검색 한 다음 영구적으로 삭제 합니다.

```powershell
Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery 'Subject:"Download this file"' -DeleteContent
```

구문과 매개 변수에 대한 자세한 내용은 [Search-Mailbox](https://technet.microsoft.com/ko-kr/library/dd298173\(v=exchg.150\))를 참조하십시오.

맨위로 돌아가기

## \-LogLevel 전체 매개 변수를 사용 하 여

앞의 예제를 *LogLevel* 매개 변수 중 일부에 **Search-Mailbox** cmdlet에 의해 반환 된 결과 대 한 자세한 정보를 기록 하려면 `Full` 와 값 사용 됩니다. 이 매개 변수를 포함 하는 경우 전자 메일 메시지를 만들고 *TargetMailbox* 매개 변수에 의해 지정 된 사서함에 전송 합니다. (즉, 검색 Results.csv 라는 CSV 형식의 파일) 로그 파일이 전자 메일 메시지에 첨부 되 고 *TargetFolder* 매개 변수에 의해 지정 된 폴더에 배치 됩니다. 로그 파일 **Search-Mailbox** cmdlet을 실행 하면 검색 결과에 포함 된 각 메시지에 대 한 행을 포함 합니다.

