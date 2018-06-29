---
title: '사서함 가져오기 및 내보내기 요청: Exchange 2013 Help'
TOCTitle: 사서함 가져오기 및 내보내기 요청
ms:assetid: 157a7d88-d3aa-4056-9a50-df67451b14be
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633455(v=EXCHG.150)
ms:contentKeyID: 50482536
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 가져오기 및 내보내기 요청

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-07_

Exchange 관리 셸에서 설정 하는 **MailboxImportRequest** 또는 **MailboxExportRequest** cmdlet을 사용 하 여,.pst 파일에서 데이터 또는 데이터를 가져올 수 있습니다. 사서함 가져오기 작업을 시작 하거나 내보내기 요청을 한 후에 Microsoft Exchange 사서함 복제 서비스 (MRS) 하 여 프로세스 비동기적으로 완료 됩니다. MRS가 모든 Exchange 2010 클라이언트 액세스 서버에 있어야 하 고는 사서함을 이동 하 고 가져오기 (영문) 및.pst 파일 내보내기 (영문)를 담당 하는 서비스입니다.

**목차**

Reasons to import or export mailbox data

Advantages to using import and export requests

Considerations

Importing mailbox data

Exporting mailbox data

## 사서함 데이터를 가져오거나 내보내는 이유

사서함 데이터를 가져오거나 내보내는 이유는 다음과 같습니다.

  - **준수 요구 사항 충족**   법적 개시를 위해 사서함 콘텐츠를 .pst 파일로 내보낼 수 있습니다. 내보내기가 완료된 후 특별히 준수 목적으로 사용되는 사서함으로 콘텐츠를 가져올 수 있습니다.

  - **지정 시간 사서함 스냅숏 만들기**   특정 사서함의 스냅숏을 만들면 사서함 데이터베이스의 전체 백업 세트를 유지하지 않아도 됩니다.

  - **사용자의 .pst 파일을 사서함 또는 개인 보관함으로 이동**   Microsoft Outlook 사용자는 전자 메일을 로컬에 .pst 파일로 저장할 수 있습니다. [New-MailboxImportRequest](https://technet.microsoft.com/ko-kr/library/ff607310\(v=exchg.150\)) cmdlet을 사용하면 사용자 .pst 파일의 데이터를 해당 사서함이나 개인 보관으로 이동할 수 있습니다. 이 방법은 사용자 로컬 컴퓨터에서 Exchange 서버로 전자 메일을 전송하는 편리한 방법입니다.

## 가져오기 및 내보내기 요청 사용 시의 이점

Exchange 2013에서 가져오기 및 내보내기 요청을 사용할 경우의 이점은 다음과 같습니다.

  - Exchange 2013에는 .pst 파일을 읽고 쓸 수 있는 .pst 공급자가 포함되어 있습니다.

  - 가져오기 및 내보내기 요청이 비동기적으로 처리됩니다. 큐 및 제한 프레임워크를 이용하는 MRS에서 프로세스를 수행합니다.

  - .pst 파일을 사용자의 개인 보관으로 직접 가져올 수 있습니다.

  - 여러 .pst 파일을 동시에 가져오거나 내보낼 수 있습니다.

  - Exchange 서버가 액세스할 수 있는 모든 공유 네트워크 드라이브에 .pst 파일이 상주할 수 있습니다.

  - Exchange 2013에서는 다음 .pst 파일을 지원합니다. Office Outlook 2007 및 Outlook 2010에서 생성된 유니코드 파일

## 고려 사항

사서함 데이터를 가져오거나 내보내기 전에 다음을 고려합니다.

  - 사서함 데이터를 가져오거나 내보내려면 Exchange 서버가 액세스할 수 있는 네트워크 공유 폴더를 설정해야 합니다. 사서함 데이터를 가져오고 내보내는 네트워크 공유에 Exchange Trusted Subsystem 그룹이 액세스할 수 있도록 이 그룹에 읽기/쓰기 권한도 부여해야 합니다. 이 권한을 부여하지 않으면 Exchange에서 대상 사서함에 연결할 수 없다는 오류 메시지가 표시됩니다.

  - Outlook에서 지원되는 최대 .pst 파일 크기는 50GB입니다. 따라서 50GB보다 큰 .pst 파일은 가져오지 않는 것이 좋습니다. 50GB보다 큰 사서함의 경우 포함 또는 제외할 특정 폴더를 지정하거나 콘텐츠 필터를 사용하여 .pst 파일을 여러 개 만들 수 있습니다.

  - 가져오기 및 내보내기 요청은 MRS에서 수행되며, 이동 요청과 사서함 복원 요청도 MRS에서 처리됩니다. 모든 요청은 MRS에 의해 대기되고 제한됩니다.

  - 파일 크기, 네트워크 대역폭 및 MRS 제한에 따라 사서함 데이터를 가져오고 내보내는 데 몇 시간 정도 걸릴 수 있습니다.

  - 공용 폴더 또는 공용 폴더 데이터베이스로 데이터를 가져올 수는 없습니다.

## 사서함 데이터 가져오기

**MailboxImportRequest** cmdlet 집합을 사용하면 .pst 파일의 데이터를 사서함이나 개인 보관으로 가져올 수 있습니다. .pst 파일에서 사서함 데이터를 가져올 때 지정할 수 있는 옵션 목록은 다음과 같습니다.


> [!NOTE]
> 데이터를 가져올 사서함이 존재해야 합니다. 사서함이 없는 사용자 계정으로는 데이터를 가져올 수 없습니다.



  - 데이터를 내보낸 계정이 아닌 다른 사용자 계정으로 데이터를 가져올 수 있습니다. 예를 들어 john@contoso.com에서 데이터를 내보낸 후 legaldiscovery@contoso.com으로 가져올 수 있습니다.

  - *IsArchive* 매개 변수를 지정하여 사용자의 개인 보관으로만 항목을 가져올 수 있습니다.

  - 관련 폴더 메시지가 .pst 파일에 있는 경우 *AssociatedMessagesCopyOption* 매개 변수를 사용하여 가져올 수 있습니다. 연결된 메시지에는 규칙, 보기 및 양식에 대한 정보가 있는 숨겨진 데이터가 포함되어 있습니다. 이 데이터가 .pst 파일에 있을 경우 보안 네트워크의 모든 메시지를 가져옵니다.

  - *IncludeFolders* 또는 *ExcludeFolders* 매개 변수를 사용하여 특정 폴더를 포함하거나 제외할 수 있습니다.

  - *ExcludeDumpster* 매개 변수를 사용하여 복구 가능한 항목 폴더를 제외할 수 있습니다. .pst 파일에 복구 가능한 항목 폴더가 있는 경우 이 폴더는 기본적으로 가져오기 요청에 포함됩니다.

## 사서함 가져오기 요청 cmdlet

사서함 가져오기 요청에 사용되는 cmdlet은 다음과 같습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>cmdlet</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607310(v=exchg.150)">New-MailboxImportRequest</a></p></td>
<td><p>.pst 파일을 사서함이나 개인 보관함으로 가져오는 프로세스를 시작합니다. 사서함당 가져오기 요청을 두 개 이상 만들 수 있습니다. 각 요청에 고유 이름이 있어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607317(v=exchg.150)">Set-MailboxImportRequest</a></p></td>
<td><p>요청이 생성되거나 실패한 요청에서 복구된 후 가져오기 요청 옵션을 변경합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607309(v=exchg.150)">Suspend-MailboxImportRequest</a></p></td>
<td><p>요청이 생성된 후 완료 상태에 이르기 전에 언제든지 가져오기 요청을 일시 중단합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607306(v=exchg.150)">Resume-MailboxImportRequest</a></p></td>
<td><p>일시 중단되었거나 실패한 가져오기 요청을 다시 시작합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607311(v=exchg.150)">Remove-MailboxImportRequest</a></p></td>
<td><p>전체 또는 일부 완료된 가져오기 요청을 제거합니다. 완료된 가져오기 요청은 자동으로 지워지지 않습니다. 제거하려면 이 cmdlet을 사용해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607368(v=exchg.150)">Get-MailboxImportRequest</a></p></td>
<td><p>가져오기 요청에 대한 일반적인 정보를 봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607315(v=exchg.150)">Get-MailboxImportRequestStatistics</a></p></td>
<td><p>가져오기 요청에 대한 자세한 정보를 봅니다.</p></td>
</tr>
</tbody>
</table>


## 사서함 데이터 내보내기

**MailboxExportRequest** cmdlet을 사용하면 사서함 데이터를 .pst 파일로 내보낼 수 있습니다. 사서함을 하나 또는 여러 개 내보낼 수 있지만 한 번에 하나의 요청만 각 .pst 파일에 기록됩니다. 사서함 데이터를 .pst 파일로 내보낼 때 지정할 수 있는 옵션 목록은 다음과 같습니다.

  - *IsArchive* 매개 변수를 사용하여 개인 보관 데이터를 내보낼 수 있습니다.

  - *ContentFilter* 매개 변수를 사용하여 내보낸 메시지를 필터링할 수 있습니다. 메시지 콘텐츠, 첨부 파일, 보낸 사람, 받는 사람, 받은 편지함 범주, 중요도, 메시지 유형, 메시지 크기, 메시지가 전송, 수신 또는 만료된 시기를 기준으로 필터링할 수 있습니다.

  - *IncludeFolders* 또는 *ExcludeFolders* 매개 변수를 사용하여 포함하거나 제외할 폴더를 지정할 수 있습니다. Exchange 2013 사서함에서 데이터를 내보내는 경우 *ExcludeDumpster* 매개 변수를 사용하여 복구 가능한 항목 폴더를 제외할 수도 있습니다.

  - *AssociatedMessagesCopyOption* 매개 변수를 사용하여 관련 메시지를 내보낼 수 있습니다. 연결된 메시지에는 규칙, 보기 및 양식에 대한 정보가 있는 숨겨진 데이터가 포함되어 있습니다. 기본적으로 관련 항목은 .pst 파일에 복사되지 않습니다.

## 사서함 내보내기 요청 cmdlet

사서함 내보내기 요청에 사용되는 cmdlet은 다음과 같습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>cmdlet</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607299(v=exchg.150)">New-MailboxExportRequest</a></p></td>
<td><p>기본 사서함이나 개인 보관함의 데이터를 .pst 파일로 내보내는 프로세스를 시작합니다. 사서함당 내보내기 요청을 두 개 이상 만들 수 있습니다. 각 요청에 고유 이름이 있어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607312(v=exchg.150)">Set-MailboxExportRequest</a></p></td>
<td><p>요청이 생성되거나 실패한 요청에서 복구된 후 내보내기 요청 옵션을 변경합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607305(v=exchg.150)">Suspend-MailboxExportRequest</a></p></td>
<td><p>요청이 생성된 후 완료 상태에 이르기 전에 언제든지 내보내기 요청을 일시 중단합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607476(v=exchg.150)">Resume-MailboxExportRequest</a></p></td>
<td><p>일시 중단되었거나 실패한 내보내기 요청을 다시 시작합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607464(v=exchg.150)">Remove-MailboxExportRequest</a></p></td>
<td><p>전체 또는 일부 완료된 내보내기 요청을 제거합니다. 완료된 내보내기 요청은 자동으로 지워지지 않습니다. 제거하려면 이 cmdlet을 사용해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607479(v=exchg.150)">Get-MailboxExportRequest</a></p></td>
<td><p>내보내기 요청에 대한 일반적인 정보를 봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/ff607316(v=exchg.150)">Get-MailboxExportRequestStatistics</a></p></td>
<td><p>내보내기 요청에 대한 자세한 정보를 봅니다.</p></td>
</tr>
</tbody>
</table>

