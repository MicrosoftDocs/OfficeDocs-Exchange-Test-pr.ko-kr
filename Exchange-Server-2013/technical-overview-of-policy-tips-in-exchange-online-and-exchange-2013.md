---
title: '정책 팁: Exchange 2013 Help'
TOCTitle: 정책 팁
ms:assetid: 4266b83c-dd8a-4b3d-99ff-402e68fc810c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150512(v=EXCHG.150)
ms:contentKeyID: 50482213
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 정책 팁

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-07-22_

장치 전자 메일 사용자에 대 한 조직의 Microsoft Outlook, Outlook Web App (OWA) 및 OWA를 부적절 하 게 *정책 팁* 알림 메시지를 포함 하는 데이터 손실 방지 (DLP) 정책을 작성 하 여 중요 한 정보를 보내지 못하게 방지 하는데 도움이 됩니다. Microsoft Exchange Server 2010 에 도입 된 메일 설명을 마찬가지로 정책 팁 알림 메시지는 사용자에에서 게 표시 Outlook 전자 메일 메시지를 작성 되는 동안 합니다. 정책 팁 알림 메시지는만 표시 하는 경우 보낸 사람의 전자 메일 메시지에 대 한 무언가 원본 위치에 있는 DLP 정책 위반 하 고 정책 규칙을 설정 하는 조건을 만족 하는 경우 보낸사람에 게 알리기를 포함 하는 있습니다. 자세한 내용은이 비디오를 시청 합니다.

> [!VIDEO https://www.microsoft.com/ko-kr/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

정책 팁을 전자 메일 보낸 사람에게 표시하려면 규칙에 **정책 팁과 함께 보낸 사람에게 알림** 작업이 포함되어 있어야 합니다. Exchange 관리 센터의 규칙 편집기에서 이 작업을 추가할 수 있습니다. 자세한 내용은 [정책 팁 관리](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)을 참조하십시오.

DLP 정책을 적용하는 전송 규칙 에이전트는 메시지와 정책 내의 조건을 평가하는 동안 전자 메일 메시지, 첨부 파일, 본문 텍스트 또는 제목 줄을 구별하지 않습니다. 예를 들어 사용자가 메시지 본문에 신용 카드 번호가 포함된 전자 메일 메시지를 만든 다음 메시지의 주소를 조직 외부의 받는 사람으로 지정하려고 하면 그러한 정보에 대한 기업의 기대 사항을 알리는 정책 설명 알림 메시지가 Outlook 또는 Outlook Web App에서 해당 사용자에게 표시될 수 있습니다. 그러나 이러한 종류의 알림은 설명된 예 작업을 제한하는 DLP 정책을 구성한 경우에만 표시됩니다. 이 경우에는 신용 카드 데이터가 포함된 메시지의 헤더에 외부 전자 메일 별칭을 추가하는 작업입니다. DLP 정책을 만드는 동안 선택할 수 있는 조건, 작업 및 예외는 매우 다양합니다. 이러한 다양성 덕분에 데이터 손실 방지 노력을 조율하여 특정 조직의 요구를 충족할 수 있습니다.

규칙 내에서 보낸 사람에게 알림 작업이나 재정의 작업을 사용할 때마다 메시지가 조직에서 메시지를 보낸 조건도 포함하는 것이 좋습니다. 이 작업은 정책 규칙 편집기를 사용하여 **보낸 사람 위치...** \> **조직 내부** 등의 조건을 추가함으로써 수행할 수 있습니다. 기존 DLP 정책을 변경하는 방법에 대한 자세한 내용은 [DLP 정책 관리](manage-dlp-policies-exchange-2013-help.md)를 참조하십시오. 보낸 사람에게 알림 작업은 회사의 메시지 생성 환경의 일부로 적용되기 때문에 이는 모범 사례 권장 사항입니다. 이 작업이 참조하는 보낸 사람은 회사 내 메시지 작성자입니다. 보낸 사람이 조직 외부에 있는 경우 들어오는 메시지에 대해 정책 팁에서 제공하는 사용자 상호 작용은 사용자에 의해 처리될 수 없으며, 무시됩니다. DLP 정책을 적용하여 들어오는 메시지를 검사하고 이 메시지에 대해 다양한 작업을 수행할 수 있지만 이 경우 보낸 사람에게 알림 작업을 추가하지 마십시오.

메시지를 작성하고 있는, 조직의 전자 메일 보낸 사람이 정책 팁 알림을 통해 실시간으로 조직의 기대 사항과 표준에 대해 알게 되면 조직이 적용하려는 표준을 위반할 가능성이 줄어듭니다.


> [!NOTE]
> <UL>
> <LI>
> <P>Exchange Online: DLP는 Exchange Online 계획 2 구독이 필요한 고급 기능입니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online 라이선스</A>를 참조하세요.</P>
> <LI>
> <P>Exchange 2013: DLP는 CAL(Exchange Enterprise Client) 액세스 라이선스가 필요한 고급 기능입니다. CAL 및 서버 라이선스에 대한 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 라이선스</A>를 참조하세요.</P>
> <LI>
> <P>조직에서 Exchange 2013 SP1 또는 Exchange Online을 사용하는 경우 Outlook 2013, Outlook Web App 또는 장치용 OWA에서 메일을 보내는 사용자에게 정책 설명이 제공됩니다. 그러나 조직에서 현재 Exchange 2013을 사용하는 경우에는 Outlook 2013에서 전자 메일을 보내는 사용자에게만 정책 설명이 제공됩니다.</P></LI></UL>



## 정책 팁 및 규칙 옵션의 기본 텍스트

보낸 사람 알림 규칙을 DLP 정책에 추가하는 경우 일련의 가능한 옵션이 있습니다. DLP 정책 내에서 **정책 팁과 함께 보낸 사람에게 알림** 작업을 사용하여 보낸 사람에게 알리는 규칙을 추가하는 경우 제한하는 정도를 선택할 수 있습니다. 다음 표의 알림 옵션을 사용할 수 있습니다. 정책 편집에 대한 자세한 내용은 [DLP 정책 관리](manage-dlp-policies-exchange-2013-help.md)를 참조하십시오. 정책 팁을 만드는 방법에 대한 자세한 내용은 [정책 팁 관리](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)을 참조하십시오.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>알림 규칙</th>
<th>의미</th>
<th>Outlook 사용자에게 표시될 기본 정책 팁 알림 메시지</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>알림만</strong></p></td>
<td><p>MailTips와 유사하며 정책 위반에 대한 정보가 포함된 정책 팁 알림 메시지를 생성합니다. 보낸 사람은 Outlook에서 액세스할 수 있는 정책 팁 옵션 대화 상자를 사용하여 이러한 종류의 팁이 표시되는 것을 방지할 수 있습니다.</p></td>
<td><p>이 메시지는 중요한 콘텐츠를 포함할 수 있습니다. 모든 받는 사람은 이 콘텐츠를 받을 권한이 있어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>메시지 거부</strong></p></td>
<td><p>해당 조건이 더 이상 존재하지 않을 때까지 메시지가 배달되지 않습니다. 보낸 사람에게 전자 메일 메시지에 중요한 내용이 포함되어 있지 않음을 나타내는 옵션이 제공됩니다. 이를 가양성 재정의라고도 합니다. 보낸 사람이 이를 나타내면 Outlook에서는 사용자의 보고서가 감사될 수 있도록 메시지가 보낼 편지함을 떠나는 것을 허용하지만 Exchange에서는 메시지가 전송되는 것을 차단합니다.</p></td>
<td><p>이 메시지는 중요한 콘텐츠를 포함할 수 있습니다. 조직에서는 해당 콘텐츠가 제거될 때까지 이 메시지를 보낼 수 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>가양성을 재정의하지 않는 한 거부</strong></p></td>
<td><p>이 알림 규칙을 사용한 결과는 <strong>메시지 거부</strong> 알림 규칙의 경우와 유사합니다. 그러나 이 규칙을 선택하면 Exchange에서는 메시지를 차단하는 대신 메시지가 원하는 받는 사람에게 전송되도록 허용합니다.</p></td>
<td><p><strong>보낸 사람이 재정의 옵션을 선택하기 전:</strong> 이 메시지는 중요한 콘텐츠를 포함할 수 있습니다. 조직에서는 해당 콘텐츠가 제거될 때까지 이 메시지를 보낼 수 없습니다.</p>
<p><strong>보낸 사람이 재정의 옵션을 선택한 후:</strong> 메시지가 전송될 때 귀하의 의견이 관리자에게 제출됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>자동으로 재정의하지 않는 한 거부</strong></p></td>
<td><p>해당 조건이 더 이상 존재하지 않거나 보낸 사람이 재정의를 나타내지 않을 때까지 메시지가 배달되지 않습니다. 보낸 사람에게 정책을 재정의하고자 함을 나타내는 옵션이 제공됩니다.</p></td>
<td><p><strong>보낸 사람이 재정의 옵션을 선택하기 전:</strong> 이 메시지는 중요한 콘텐츠를 포함할 수 있습니다. 조직에서는 해당 콘텐츠가 제거될 때까지 이 메시지를 보낼 수 없습니다.</p>
<p><strong>보낸 사람이 재정의 옵션을 선택한 후:</strong> 이 메시지의 중요한 콘텐츠에 대한 조직의 정의를 재정의했습니다. 조직이 귀하의 작업을 감사합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>명시적으로 재정의하지 않는 한 거부</strong></p></td>
<td><p>이 알림 규칙을 사용한 결과는 <strong>자동으로 재정의하지 않는 한 거부</strong> 알림 규칙의 경우와 유사합니다. 단, 이 경우에는 보낸 사람이 정책을 재정의하려고 할 때 정책을 재정의하는 사유를 제공해야 합니다.</p></td>
<td><p><strong>보낸 사람이 재정의 옵션을 선택하기 전:</strong> 이 메시지는 중요한 콘텐츠를 포함할 수 있습니다. 조직에서는 해당 콘텐츠가 제거될 때까지 이 메시지를 보낼 수 없습니다.</p>
<p><strong>보낸 사람이 재정의 옵션을 선택한 후:</strong> 이 메시지의 중요한 콘텐츠에 대한 조직의 정의를 재정의했습니다. 조직이 귀하의 작업을 감사합니다.</p></td>
</tr>
</tbody>
</table>


## 정책 팁 알림 메시지를 사용 하 여 사용자 지정

전자 메일 보낸 사람의 전자 메일 프로그램에서 참조 하는 정책 팁 알림 텍스트를 사용자 지정 하려면 데이터 손실 방지 페이지에서 **정책 팁 관리** 를 선택 합니다. 사용자 정의 텍스트 중 하나에 대 한 표시 순서에서 DLP 정책 규칙을 **정책 설명과 함께 보낸사람에 게 알림** 작업을 포함 해야 합니다. DLP 규칙 편집기를 사용 하 여 규칙에는 작업을 추가 합니다.

사용자 고유의 정책 팁 만들기, [정책 팁 관리](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)를 참조 하는 방법에 설명 하는 절차입니다. 만든 사용자 지정 텍스트 앞의 표에 표시 된 기본 텍스트를 바꿀 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>정책 팁 알림 작업 및 설정</th>
<th>의미</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>보낸 사람에게 알림</strong></p></td>
<td><p>텍스트는 <strong>보낸사람에 게 알리지 하지만 보낼 수 있도록</strong> 작업을 시작 하는 경우에 표시 됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>보낸 사람이 재정의하도록 허용</strong></p></td>
<td><p>텍스트는 다음 작업이 시작 된 경우에 표시: <strong>하지 않은 경우 가양성 메시지를 차단</strong>, <strong>메시지를 차단 하지만 보낸 사람이 재정의 하 고 보내도록 허용</strong> 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>메시지 차단</strong></p></td>
<td><p>텍스트 <strong>블록 메시지</strong> 작업을 시작 하는 경우에 표시 됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>규정 준수 URL에 대한 링크</strong></p></td>
<td><p>규정 준수 URL에 준수에 설명 하 고 정책에 우선 수 있는 웹 페이지에 대 한 링크입니다. 이 링크는 사용자가 <strong>자세한 내용을 보려면</strong> 링크를 클릭할 때 정책 설명에 표시 됩니다.</p></td>
</tr>
</tbody>
</table>


## 자세한 내용

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[DLP 정책 관리](manage-dlp-policies-exchange-2013-help.md)

[정책 팁 관리](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)

