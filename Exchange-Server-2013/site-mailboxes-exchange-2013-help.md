---
title: '사이트 사서함: Exchange 2013 Help'
TOCTitle: 사이트 사서함
ms:assetid: 2c4393f4-d274-4e6c-bd09-9577e68c5a33
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150499(v=EXCHG.150)
ms:contentKeyID: 50482712
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사이트 사서함

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

전자 메일과 문서는 일반적으로 두 가지 고유한 별도의 데이터 리포지토리에 보관됩니다. 대부분의 조직에서는 두 매체를 모두 사용하여 공동 작업을 합니다. 문제는 전자 메일과 문서가 여러 가지 클라이언트를 사용하여 액세스된다는 점입니다. 이에 따라 사용자 생산성이 감소하고 사용자 환경이 저하되는 경우가 많습니다.

*사이트 사서함*은 이 문제를 해결하기 위한 Microsoft Exchange 2013의 새로운 개념입니다. 사이트 사서함은 동일한 클라이언트 인터페이스를 사용하여 Microsoft SharePoint 2013 문서와 Exchange 전자 메일에 액세스할 수 있도록 하여 공동 작업과 사용자 생산성을 향상시킵니다. 사이트 사서함은 기능적으로 SharePoint 2013 사이트 구성원(소유자 및 구성원), 전자 메일 메시지의 경우 Exchange 2013 사서함을 통한 공유 저장소, 문서의 경우 SharePoint 2013 사이트를 통한 공유 저장소 및 프로비전과 수명 주기 요구를 처리하는 관리 인터페이스로 구성되어 있습니다.

사이트 사서함을 사용하려면 Exchange 2013 및 SharePoint Server 2013의 통합과 구성이 필요합니다. Exchange 2013 조직이 SharePoint Server 2013 조직과 함께 작동하도록 구성하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [SharePoint Server 2013에서 사이트 사서함 구성](https://go.microsoft.com/fwlink/p/?linkid=258264)합니다.

  - [SharePoint 및 Lync와의 통합](integration-with-sharepoint-and-lync-exchange-2013-help.md)

Exchange Server 2013의 공동 작업 기능에 대한 자세한 내용은 [공동 작업](collaboration-exchange-2013-help.md)을 참조하십시오.

**목차**

How do site mailboxes work?

Site mailbox provisioning policies

## 사이트 사서함의 작동 방식

한 프로젝트 구성원이 사이트 사서함을 사용하여 메일이나 문서를 보관하는 경우 모든 프로젝트 구성원이 해당 콘텐츠에 액세스할 수 있습니다. 사이트 사서함은 Outlook 2013에 표시되므로, 사용자는 관심이 있는 프로젝트에 대한 전자 메일과 문서에 쉽게 액세스할 수 있습니다. 또한 SharePoint 사이트 자체에서도 동일한 콘텐츠에 액세스할 수 있습니다. 사이트 사서함을 사용하면 콘텐츠가 자신이 속한 곳에 보관됩니다. Exchange는 전자 메일을 저장하여, 사용자에게 자신의 사서함에 대해 매일 사용하는 것과 동일한 전자 메일 대화용 메시지 보기를 제공합니다. 한편, SharePoint는 문서를 저장하여 문서 공동 작성 및 버전 관리 정보를 표로 생성합니다. Exchange는 SharePoint에서 필요한 만큼의 메타데이터를 동기화하여 Outlook에 문서 보기를 만듭니다(예: 문서 제목, 마지막으로 수정한 날짜, 마지막으로 수정한 작성자, 크기).

![사이트 사서함 저장소 및 사용 다이어그램](images/JJ150499.b98be571-d2e0-4ebd-9fe2-440a14e91e35(EXCHG.150).gif "사이트 사서함 저장소 및 사용 다이어그램")

## 사이트 사서함 프로비전 정책

Exchange 관리 셸에서 **SiteMailboxProvisioningPolicy** cmdlet을 사용하여 사이트 사서함 할당량을 설정할 수 있습니다. 사이트 사서함 프로비전 정책은 사이트 사서함 내외로 전송되는 전자 메일 및 Exchange 서버의 사이트 사서함 크기에만 적용됩니다. 문서 리포지토리 설정은 SharePoint에서 구성됩니다. **New-SiteMailboxProvisioningPolicy** cmdlet을 사용하여 사이트 사서함 프로비전 정책을 여러 개 만들 수 있지만 기본 프로비전 정책만 모든 사이트 사서함에 적용됩니다. 조직 내에 여러 정책을 적용할 수 없습니다. 프로비전 정책을 사용하면 다음과 같은 할당량을 설정할 수 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>할당량</th>
<th>설명</th>
<th>기본 설정</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IssueWarningQuota</p></td>
<td><p><em>IssueWarningQuota</em> 매개 변수는 사이트 사서함에 대한 경고 메시지를 트리거하는 사이트 사서함 크기를 지정합니다.</p></td>
<td><p>4.5 GB</p></td>
</tr>
<tr class="even">
<td><p>MaxReceiveSize</p></td>
<td><p><em>MaxReceiveSize</em> 매개 변수는 사이트 사서함에서 받을 수 있는 전자 메일 메시지의 최대 크기를 지정합니다.</p></td>
<td><p>36 MB</p></td>
</tr>
<tr class="odd">
<td><p>ProhibitSendReceiveQuota</p></td>
<td><p><em>ProhibitSendReceiveQuota</em> 매개 변수는 더 이상 메시지를 보내거나 받을 수 없는 사이트 사서함 크기를 지정합니다.</p></td>
<td><p>5 GB</p></td>
</tr>
</tbody>
</table>


사이트 사서함 프로비전 정책을 구성하는 방법에 대한 자세한 내용은 [사이트 사서함 프로 비전 정책 관리](manage-site-mailbox-provisioning-policies-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 수명 주기 정책 및 보존

사이트 사서함의 수명 주기는 Sharepoint를 통해 관리됩니다. 사이트 사서함을 만들고 제거하는 등의 모든 사이트 사서함 작업은 SharePoint를 통해 수행해야 합니다. 또한 SharePoint 수명 주기 정책을 만들어 사이트 사서함의 수명 주기를 관리할 수 있습니다. 예를 들어 6개월 후에 모든 사이트 사서함을 자동으로 닫는 수명 주기 정책을 SharePoint에서 만들 수 있습니다. 사이트 사서함을 계속 사용해야 하는 사용자는 SharePoint를 통해 사이트 사서함을 다시 활성화할 수 있습니다. 팜에서는 수명 주기 응용 프로그램을 사용하는 것이 좋습니다. Exchange에서 활성 사이트 사서함을 수동으로 삭제하면 분리된 사이트 사서함이 생성됩니다. .

SharePoint에서 수명 주기 응용 프로그램이 사이트 사서함을 닫는 경우 사이트 사서함은 수명 주기 정책에 지정된 기간 동안 닫힌 상태로 보존됩니다. 이 사서함은 SharePoint에서 관리자나 최종 사용자가 다시 활성화할 수 있습니다. 보존 기간 후에 사서함 데이터베이스에 보관되는 Exchange 사이트 사서함의 이름 앞에는 삭제하도록 표시되었음을 나타내기 위해 **MDEL:** 이 붙습니다. 저장소 공간과 별칭을 해제하려면 사서함 데이터베이스에서 이러한 사이트 사서함을 수동으로 제거해야 합니다. SharePoint 수명 주기 정책을 사용하도록 설정하지 않으면 삭제하도록 표시된 사이트 사서함을 확인할 수 없게 됩니다. 관리자가 사이트 사서함을 제거할 때까지 사서함의 내용은 여전히 복구 가능합니다.

다음 명령을 사용하여 삭제하도록 표시된 사이트 사서함을 검색하고 제거할 수 있습니다.

    Get-Mailbox MDEL:* | ?{$_.RecipientTypeDetails -eq "TeamMailbox"} | Remove-Mailbox -Confirm:$false

사이트 사서함은 항목 수준에서 보존을 지원하지 않습니다. 사이트 사서함의 보존은 프로젝트 수준에서 이루어지므로 전체 사이트 사서함이 삭제될 때 보존된 항목이 삭제됩니다.

## 규정 준수

SharePoint의 eDiscovery Console을 사용하면 사용자 사서함 또는 사이트 사서함에 대해 키워드 검색을 수행할 수 있으므로 사이트 사서함이 원본 위치 eDiscovery 범위의 일부가 될 수 있습니다. 또한 사이트 사서함을 법적 보유 상태로 설정할 수 있습니다. 자세한 내용은 [원본 위치 eDiscovery](in-place-ediscovery-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> 사이트 사서함 Office 365 에서 법적 대기 시키려면 Exchange Online (계획 2) 라이선스를 할당 해야 합니다. 사이트 사서함 Exchange Online (계획 1) 라이선스를 할당 하는 경우에 보류에 추가 하는 별도 Exchange Online 보관 라이선스가 할당 해야 합니다.



맨 위로 이동

## 백업 및 복원

사서함 서버에 보관된 Exchange 사이트 사서함의 백업과 복원에서는 모든 Exchange 사서함에 사용하는 동일한 백업 및 복원 방법을 사용합니다. 자세한 내용은 [DAG(데이터베이스 가용성 그룹)](database-availability-groups-dags-exchange-2013-help.md)을 참조하십시오.

SharePoint 문서의 경우 백업한 후 동일한 위치에 복원해야 합니다. SharePoint 콘텐츠를 동일한 URL에 복원하는 경우 사이트 사서함이 계속 작동하고 추가 구성이 필요하지 않습니다. 다른 URL에 복원하면 **Set-SiteMailbox** cmdlet을 실행하여 *SharePointURL* 속성을 업데이트해야 합니다. SharePoint를 새 포리스트에 복원하지 않는 것이 좋습니다.

