---
title: '보존 정책 태그를 지 원하는 기본 폴더: Exchange 2013 Help'
TOCTitle: 보존 정책 태그를 지 원하는 기본 폴더
ms:assetid: d2e2064f-4102-4018-b688-504d09da6d39
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn783294(v=EXCHG.150)
ms:contentKeyID: 62835902
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보존 정책 태그를 지 원하는 기본 폴더

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-04-20_

전자 메일 수명 주기를 관리 [보존 태그 및 보존 정책](retention-tags-and-retention-policies-exchange-2013-help.md) 를 사용할 수 있습니다. 보존 정책 설정이 삭제 해야할 때 또는 보관 사서함으로 메시지를 자동으로 이동 해야 하는 경우를 지정 하는데 사용할 수 있는 보존 태그를 포함 합니다.

보존 정책 태그 (RPT)은 **받은 편지함** 및 **지운 편지함**같은 사서함의 기본 폴더에 적용할 수 있는 보존 태그의 유형입니다.

![RPT(보존 정책 태그) 만들기](images/Dn783294.b59a96fd-94e1-4c9b-bff6-97a1bd98dfe7(EXCHG.150).png "RPT(보존 정책 태그) 만들기")

## 지원 되는 기본 폴더

다음 표에 표시 된 기본 폴더에 대 한 Rpt를 만들 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>폴더 이름</th>
<th>세부 정보</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>보관</p></td>
<td><p>이 폴더는 Outlook에서 보관 단추와 보관 된 메시지에 대 한 기본 대상입니다. 보관 기능을 삭제 하지 않고 받은 편지함에서 메시지를 제거 하는 사용자에 대 한 신속한을 제공 합니다.</p>
<p>이 RPT은 Exchange Online 에서만에서 사용할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>일정</p></td>
<td><p>이 기본 폴더는 모임 및 약속을 저장하는 데 사용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>낮은 우선 순위 메일</p></td>
<td><p>이 폴더는 낮은 우선순위는 전자 메일 메시지를 포함 합니다. 포함 되는 문서를 무시 하려면 일 가능성이 가장 높은 하 고 있는 메시지를 확인 하려면 이전에 수행한 기능에 대해 살펴봅니다. 그런 다음 해당 메시지는 <strong>간단 하 게 표시</strong> 폴더로 이동합니다.</p></td>
</tr>
<tr class="even">
<td><p>대화 기록</p></td>
<td><p>이 폴더는 Microsoft Lync(이전의 Microsoft Office Communicator)에서 만듭니다. 이 폴더는 Outlook에서 기본 폴더로 취급되지 않지만, Exchange에서는 특수 폴더로 취급되며 RPT를 적용할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>지운 편지함</p></td>
<td><p>이 기본 폴더는 사서함의 다른 폴더에서 삭제된 항목을 저장하는 데 사용됩니다. Outlook 및 Outlook Web App 사용자는 이 폴더를 직접 비울 수 있습니다. 또한 사용자는 Outlook을 종료할 때 이 폴더를 비우도록 Outlook을 구성할 수도 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>임시 보관함</p></td>
<td><p>이 기본 폴더는 사용자가 전송하지 않은 임시 메시지를 저장하는 데 사용됩니다. 또한 Outlook Web App는 사용자가 전송했지만 허브 전송 서버에 전달되지 않은 메시지를 저장할 때도 이 폴더를 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>받은 편지함</p></td>
<td><p>이 기본 폴더는 사서함에 전달된 메시지를 저장하는 데 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p>저널</p></td>
<td><p>이 기본 폴더에는 사용자가 선택한 작업이 포함됩니다. 이러한 작업은 Outlook에서 자동으로 기록하고 시간 표시줄 보기에 배치됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>정크 메일</p></td>
<td><p>이 기본 폴더는 Exchange 서버의 콘텐츠 필터 또는 Outlook의 스팸 방지 필터에 의해 정크 메일로 표시된 메시지를 저장하는 데 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p>참고</p></td>
<td><p>이 폴더에는 Outlook에서 사용자가 작성하는 메모가 포함됩니다. 이 메모는 Outlook Web App에서도 볼 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>보낼 편지함</p></td>
<td><p>이 기본 폴더는 사용자가 전송한 메시지를 허브 전송 서버에 전달될 때까지 임시로 보관하는 데 사용됩니다. 전송된 메시지의 복사본은 보낸 편지함 기본 폴더에 저장됩니다. 메시지는 대개 이 폴더에 단기간 보관되므로 이 폴더의 RPT를 만들 필요는 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>RSS 피드</p></td>
<td><p>이 기본 폴더는 RSS 피드를 포함합니다.</p></td>
</tr>
<tr class="odd">
<td><p>복구 가능한 항목</p></td>
<td><p>비 IPM 하위 트리에서 숨겨진된 폴더입니다. 삭제 &quot;,&quot; 버전 &quot;,&quot; 제거 &quot;,&quot; DiscoveryHolds, &quot;및&quot; 감사 하위 폴더 포함 됩니다. 이 폴더에 대 한 보존 태그 사용자의 보관 사서함의 복구 가능한 항목 폴더에 복구 가능한 항목 폴더는 사용자의 기본 사서함에서 항목을 이동합니다. <strong>보관 함으로 이동</strong> 보존 작업에만이 폴더에 대 한 태그를 할당할 수 있습니다. 자세한 내용은 <a href="recoverable-items-folder-exchange-2013-help.md">복구 가능한 항목 폴더</a>를 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p>보낸 편지함</p></td>
<td><p>이 기본 폴더는 허브 전송 서버로 전달된 메시지를 저장하는 데 사용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>동기화 문제</p></td>
<td><p>이 폴더 동기화 로그를 들어 있습니다. 자세한 내용은, <a href="https://go.microsoft.com/fwlink/p/?linkid=198215">동기화 오류 폴더</a>를 참조 합니다.</p></td>
</tr>
<tr class="even">
<td><p>Tasks</p></td>
<td><p>이 기본 폴더는 작업을 저장 하는데 사용 됩니다. 작업 폴더에 대 한 RPT를 만들려면 Exchange 관리 셸 를 사용 해야 합니다. 자세한 내용은 <a href="https://technet.microsoft.com/ko-kr/library/dd335226(v=exchg.150)">New-RetentionPolicyTag</a>을 참조 합니다. 작업 폴더에 대 한 RPT를 만든 후에 Exchange 관리 센터를 사용 하 여 관리할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


## 자세한 정보

  - Rpt는 기본 폴더에 대 한 보존 태그입니다. Rpt- **삭제 및 복구 허용** 또는 **영구 삭제**중 하나에 대 한 삭제 작업을 선택할 수 있습니다.

  - 메시지 보관 사서함으로 이동 하는 RPT를 만들 수 없습니다. 이동 하려면 다음 보관 하려면 오래 된 항목을 만들 수 있습니다는 *기본 정책 태그* (DPT) 전체 사서함에 적용 되는 또는 *개인 태그*Outlook 및 보관 정책으로 Outlook Web App (OWA)에 표시 되는. 사용자 폴더 또는 개별 메시지에 적용 수 있습니다.

  - 연락처 폴더에는 RPT를 적용할 수 없습니다.

  - 보존 정책에는 특정 기본 폴더에 대 한 RPT 하나를 추가할 수 있습니다. 예, 보존 정책에는 받은 편지함 태그를 해당 보존 정책에 받은 편지함 유형의 다른 RPT를 추가할 수 없습니다.

  - Rpt를 만들거나 다른 유형의 보존 태그 및 보존 정책에 추가 하는 방법을 알아보려면 [보존 정책 만들기](create-a-retention-policy-exchange-2013-help.md)를 참조 하십시오.

  - Exchange 2013 및 Exchange Online DPT **일정** 및 **작업** 기본 폴더에도 적용 됩니다. 이 항목이 삭제 되거나 DPT 설정에 따라 보관 사서함으로 이동 되 고 늘어날 수 있습니다. 를 방지 하기 위해 이러한 폴더의 항목 삭제에서 DPT 설정을 사용 하지 않도록 설정 하는 보존 Rpt를 만듭니다. 를 방지 하기 위해 기본 폴더에서 항목을 이동에서 DPT 설정 작업을 보관, 보존 정책에 추가 되어 다음 기본 폴더에 적용 하는 사용자를 이동와 비활성화 된 개인 태그를 만들 수 있습니다. 자세한 내용은 [Exchange 2010의 기본 폴더에 있는 항목의 보관 되지 않도록](https://go.microsoft.com/fwlink/?linkid=511071)를 참조 합니다.

