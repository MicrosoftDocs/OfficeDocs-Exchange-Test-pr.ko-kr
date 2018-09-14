---
title: '전체에서 Exchange 2013의 보관: Exchange 2013 Help'
TOCTitle: 전체에서 Exchange 2013의 보관
ms:assetid: b5e4c0e9-0558-4b90-bc12-f67adbfb59ac
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd979800(v=EXCHG.150)
ms:contentKeyID: 50483957
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전체에서 Exchange 2013의 보관

 

_<strong>적용 대상:</strong> Exchange Online, Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2016-12-09_

*원본 위치 보관*을 사용하면 개인 저장소(.pst) 파일을 사용하지 않아도 사용자가 MicrosoftOutlook 2010 이상 버전 및 Microsoft OfficeOutlook Web App에서 액세스할 수 있는 *보관 사서함*에 메시지를 저장할 수 있으므로 조직의 메시징 데이터를 다시 제어할 수 있습니다.

Microsoft Exchange Server 2013의 원본 위치 보관은 기록 메시징 데이터를 저장할 대체 저장 위치를 사용자에게 제공합니다. 원본 위치 보관은 사서함 사용자에 대해 사용하도록 설정된 추가 사서함(보관 사서함이라고 함)입니다. Outlook 2007 이상 버전 및 Outlook Web App 사용자는 보관 사서함에 원활하게 액세스할 수 있습니다. 이러한 클라이언트 응용 프로그램을 통해 사용자는 보관 사서함을 보고 기본 사서함과 보관 간에 메시지를 이동하거나 복사할 수 있습니다. 원본 위치 보관은 사용자에게 메시징 데이터의 일관된 보기를 제공하며 .pst 파일을 관리하기 위해 사용자 오버헤드가 필요하지 않습니다.

사용자의 기본 사서함을 다른 사서함 데이터베이스는 동일한 사서함 서버와 동일한 사서함 데이터베이스 또는 동일한 Active Directory 사이트에 있는 다른 사서함 서버의 사서함 데이터베이스에는 사용자의 보관을 제공할 수 있습니다. 하이브리드 배포의 Exchange 2010 하 고 나중에 온-프레미스 사서함 서버에 있는 사서함에 대 한 클라우드 기반 보관을 제공할 수 있습니다.

<strong>목차</strong>

Messaging data and .pst files

Client access to archive mailboxes

Delegate access

Moving messages to the archive mailbox

Archive and retention policies

Default MRM policy

Archive quotas

In-Place Archives and other Exchange features

Managing archive mailboxes

## 메시징 데이터 및 .pst 파일

Outlook에서는 .pst 파일을 사용하여 사용자의 컴퓨터에 로컬로 또는 네트워크 공유에 데이터를 저장합니다. 캐시된 Exchange 모드의 Outlook에서 오프라인 액세스용으로 사서함 복사본을 저장하기 위해 사용하는 오프라인 저장소(.ost) 파일과 달리, .pst 파일은 사용자의 Exchange 사서함과 동기화되지 않습니다. 사용자가 메시지를 .pst 파일로 이동하면 사서함에서 해당 메시지가 제거됩니다.

.pst 파일을 사용하여 메시징 데이터를 관리하는 경우 다음과 같은 문제가 발생할 수 있습니다.

  - <strong>관리되지 않는 파일</strong>   일반적으로 .pst 파일은 사용자가 만들며 사용자 컴퓨터나 네트워크 공유에 상주합니다. 조직에서는 .pst 파일을 관리하지 않습니다. 따라서 사용자는 조직의 제어를 받지 않고 같거나 다른 메시지가 포함된 여러 .pst 파일을 만들어 서로 다른 위치에 저장할 수 있습니다.

  - <strong>검색 비용 증가</strong>   소송 및 특정 비즈니스 또는 규정 요구 사항에 의해 검색 요청이 발생하는 경우가 있습니다. 이때 사용자 컴퓨터의 .pst 파일에 있는 메시징 데이터를 찾으려면 상당히 번거로운 수작업이 필요합니다. 관리되지 않는 .pst 파일을 추적하는 것은 쉽지 않으며 많은 경우 .pst 데이터가 검색되지 않기도 합니다. 이로 인해 조직은 법적, 금전적 위험에 주로 노출될 수 있습니다.

  - <strong>메시징 보존 정책 적용 불가능</strong>   .pst 파일에 있는 메시지에는 메시징 보존 정책을 적용할 수 없습니다. 결과적으로 조직이 비즈니스 또는 적용 규정의 준수 의무를 위반할 수도 있습니다.

  - <strong>데이터 도난 위험</strong>   .pst 파일에 저장된 메시징 데이터는 데이터 도난에 취약합니다. 예를 들면, .pst 파일은 랩톱, 이동식 하드 드라이브, 이동식 미디어(예: USB 드라이브, CD 및 DVD) 같은 이동식 장치에 저장되는 경우가 많습니다.

  - <strong>메시징 데이터의 보기 제한</strong>   .pst 파일에 정보를 저장하는 사용자는 경우에 따라 데이터를 사용하지 못할 수 있습니다. .pst 파일에 저장된 메시지는 일반적으로 .pst 파일이 있는 컴퓨터에서만 사용할 수 있습니다. 따라서 사용자가 다른 컴퓨터에서 Outlook Web App 또는 Outlook을 사용하여 해당 사서함에 액세스하는 경우 .pst 파일에 저장된 메시지에 액세스할 수 없습니다.

## 보관 사서함에 대한 클라이언트 액세스

다음 표는 보관 사서함에 액세스하는 데 사용할 수 있는 클라이언트 응용 프로그램을 보여 줍니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>클라이언트</th>
<th>보관 사서함에 대한 액세스</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013, Outlook 2010, Outlook 2007 및 Outlook Web App</p></td>
<td><p>예. Outlook 2013, Outlook 2010, Outlook 2007 및 Outlook Web App 사용자는 기본 사서함에서 보관 사서함으로 항목을 복사하거나 이동할 수 있고, 보존 정책을 사용하여 항목을 보관으로 이동할 수도 있습니다.</p>

> [!NOTE]
> Outlook 2010 이상 및 Outlook 2007 사용자도 복사 하거나 이동할 수 항목.pst 파일에서 보관 사서함에 있습니다. Outlook 2007 사용자가 2011 년 2 월에 Office 2007 누적 업데이트를 필요로 합니다. Outlook 2010 이상 및 Outlook 2007 사이도 보관 지원 하의 일부 차이점이 있습니다. 자세한 내용은 <A href="https://blogs.technet.com/b/exchange/archive/2010/12/20/3411710.aspx">예 버지니아 방법이 Outlook 2007에서 Exchange 2010 보관 지원</A>를 참조 하는 Exchange 팀 블로그 (영문) 문서를 참조 합니다.


</td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><p>아니요</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 원본 위치 보관 프리미엄 기능 요소 이며 Exchange 엔터프라이즈 클라이언트 액세스 라이선스 (CAL) 필요 합니다. Exchange 라이선스 하는 방법에 대 한 자세한 내용은, <A href="https://go.microsoft.com/fwlink/?linkid=237292">Exchange 서버 라이선스</A>을 참조 하십시오. 보관 사서함에 액세스 하는 데 필요한 Outlook의 버전에 대 한 자세한 내용은, <A href="https://go.microsoft.com/fwlink/?linkid=237276">개인 보관 함 및 보존 정책에 대 한 라이선스 요구 사항</A>을 참조 하십시오.



Outlook은 캐시된 Exchange 모드를 사용하도록 구성된 경우에도 사용자 컴퓨터에 보관 사서함의 로컬 복사본을 만들지 않습니다. 사용자는 온라인 모드에서만 보관 사서함에 액세스할 수 있습니다.

## 위임 액세스

*위임 액세스*는 사용자 또는 사용자 집합에 다른 사용자 사서함에 대한 액세스 권한이 제공되는 경우입니다. 다음을 비롯하여 위임 액세스를 제공하기 위한 몇 가지 시나리오가 있습니다.

  - 더 이상 조직에 고용되어 있지 않은 사용자 사서함에 대한 액세스 권한을 하나 이상의 사용자에게 제공. 이 경우 위임 액세스 권한이 제공될 수 있는 사용자는 퇴직한 사용자의 관리자 또는 감독자이거나 퇴직한 사용자의 업무를 담당할 다른 사용자입니다.

  - 공유 사서함에 대한 액세스 권한을 하나 이상의 사용자에게 제공

  - 보좌하는 임원 사서함에 대한 액세스 권한을 비서에게 제공

Exchange 2013 는 사서함에 대 한 전체 액세스 권한을 할당 하는 경우 사용 권한을 할당 하는 대리인에 액세스할 수도 사용자의 보관 합니다. 대리인은 사서함에 액세스 하려면 Outlook을 사용 해야 하 고 Exchange 2010 SP1 또는 자동 검색을 위해 이상의 클라이언트 액세스 서버에 연결 해야 합니다. 자동 검색은 자동으로 Outlook 클라이언트를 구성 하려면 구성 설정을 제공 하는 Exchange 서비스입니다. Exchange 2013 사서함에 액세스 하려면 Outlook을 사용 하는 대리인을 모두 기본 사서함 및 액세스 권한이 있는 보관 Outlook에서 표시 됩니다.

## 보관 사서함으로 메시지 이동

메시지를 보관 사서함으로 이동하는 몇 가지 방법이 있습니다.

  - <strong>수동으로 메시지 이동 또는 복사</strong>   사서함 사용자가 기본 사서함 또는 .pst 파일에서 보관 사서함으로 메시지를 수동으로 이동하거나 복사할 수 있습니다. Outlook 및 Outlook Web App에서 보관 사서함은 다른 사서함이나 .pst 파일로 표시됩니다.

  - <strong>받은 편지함 규칙을 사용하여 메시지 이동 또는 복사</strong>   사서함 사용자가 Outlook 또는 Outlook Web App에서 받은 편지함 규칙을 만들어 메시지를 보관 사서함의 폴더로 자동으로 이동할 수 있습니다. 자세한 내용은 [받은 편지함 규칙 정보](http://help.outlook.com/ko-kr/140/bb899620.aspx)를 참조하십시오.

  - <strong>보존 정책을 사용하여 메시지 이동</strong>   보존 정책을 사용하여 메시지를 보관함으로 자동으로 이동할 수 있습니다. 사용자가 개인 태그를 적용하여 메시지를 보관 사서함으로 이동할 수도 있습니다. 보관함 및 보존 정책에 대한 자세한 내용은 이 항목의 뒷부분에 있는 Archive and retention policies을 참조하십시오.
    

    > [!NOTE]
    > 개인 태그는 Outlook Web App과 Outlook 2010 이상 버전에서만 사용할 수 있습니다.



  - <strong>.Pst 파일에서 가져오기 메시지</strong>   Exchange 2013 메시지를 가져올.pst 파일에서 사용자의 보관 또는 기본 사서함에는 사서함 가져오기 요청을 사용할 수 있습니다. 자세한 내용은 [사서함 가져오기 및 내보내기 요청](mailbox-import-and-export-requests-exchange-2013-help.md)를 참조 합니다. 또한 조직에서 컴퓨터에서.pst 파일을 검색 하 고 사용자의 보관을.pst 파일 데이터를 가져올를 PST 캡처 도구를 사용할 수 있습니다.

## 보관함 및 보존 정책

Exchange 2013에서는 지정된 기간이 지나면 사용자의 기본 사서함에서 보관 사서함으로 메시지를 자동으로 이동하는 보관 정책을 사서함에 적용할 수 있습니다. 보관 정책은 <strong>보관 사서함으로 이동</strong> 보존 작업을 사용하는 보존 태그를 만들어 구현됩니다.

메시지는 기본 사서함의 원본 폴더와 이름이 같은 보관 사서함의 폴더로 이동됩니다. 보관 사서함에 같은 이름의 폴더가 없으면 관리되는 폴더 도우미가 메시지를 이동할 때 해당 폴더가 생성됩니다. 보관 사서함에 같은 폴더 계층을 다시 만들면 사용자가 메시지를 쉽게 찾을 수 있습니다.

보존 정책, 보존 태그 및 <strong>보관 사서함으로 이동</strong> 보존 작업에 대한 자세한 내용은 [보존 태그 및 보존 정책](retention-tags-and-retention-policies-exchange-2013-help.md)를 참조하십시오.

## 기본 MRM 정책

Exchange 2013 설치 프로그램은 <strong>기본 MRM 정책</strong>이라는 기본 보관 및 보존 정책을 만듭니다. 이 정책에는 다음 표와 같이 <strong>보관 사서함으로 이동</strong> 작업이 있는 보존 태그가 포함됩니다.


> [!NOTE]
> Exchange 2010에서 Exchange 설치 프로그램은 <STRONG>기본 보관함 및 보존 정책</STRONG>이라는 기본 보관함 및 보존 정책을 만듭니다.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>보존 태그 이름</th>
<th>태그 유형</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>기본 2년 후 보관함으로 이동</strong></p></td>
<td><p>기본(DPT)</p></td>
<td><p>메시지가 2년 후 자동으로 보관 사서함에 이동됩니다. 명시적으로 적용되거나 폴더에서 상속된 보존 태그가 없는 전체 사서함의 항목에 적용됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>개인 1년 후 보관함으로 이동</strong></p></td>
<td><p>개인</p></td>
<td><p>메시지가 1년 후 자동으로 보관 사서함으로 이동됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>개인 5년 후 보관함으로 이동</strong></p></td>
<td><p>개인</p></td>
<td><p>메시지가 5년 후 자동으로 보관 사서함으로 이동됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>개인 보관함으로 이동 안 함</strong></p></td>
<td><p>개인</p></td>
<td><p>메시지가 보관 사서함으로 이동되지 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>복구 가능한 항목 14일 후 보관함으로 이동</strong></p></td>
<td><p>복구 가능한 항목 폴더</p></td>
<td><p>메시지가 사용자 기본 사서함의 복구할 수 있는 항목 폴더에서 보관 사서함의 복구할 수 있는 항목 폴더로 이동합니다. 보관함에 있는 삭제된 항목을 복구하려는 사용자는 보관 사서함에 대해 지운 편지함 복구 기능을 사용해야 합니다.</p></td>
</tr>
</tbody>
</table>


사서함 사용자가 원본 위치 보관을 사용하도록 설정했는데 사서함에 보존 정책이 할당되어 있지 않으면 기본 보관함 및 보존 정책이 자동으로 할당됩니다. 관리되는 폴더 도우미가 사서함을 처리하면 사용자가 이러한 태그를 사용할 수 있게 됩니다. 사용자는 보관 사서함으로 이동할 폴더나 메시지에 태그를 지정할 수 있습니다. 기본적으로 전체 사서함의 전자 메일 메시지는 2년 후 이동됩니다.

사용자에 대해 보관 사서함을 프로비전하기 전에 사서함에 적용될 보관 정책에 대해 알리고 요구에 맞는 후속 교육이나 설명서를 프로비전하는 것이 좋습니다. 여기에는 다음에 대한 세부 정보가 포함되어야 합니다.

  - 보관함, 기본 보관함 및 보존 정책 내에서 사용 가능한 기능

  - 메시지가 보관함으로 자동으로 이동될 수 있는 시기에 대한 정보

  - 보관 사서함에서 생성된 폴더 계층에 대한 정보

  - 개인 태그를 적용하는 방법(Outlook 및 Outlook Web App의 보관 정책 메뉴에 표시됨)


> [!NOTE]
> 보관 사서함을 가진 사용자에게 보존 정책을 적용하는 경우 기본 MRM 정책이 보존 정책으로 바뀝니다. <STRONG>보관 사서함으로 이동</STRONG> 작업으로 하나 이상의 보존 태그를 만든 후 보존 정책에 해당 태그를 연결할 수 있습니다. 또한 설치 프로그램에서 생성되고 기본 MRM 정책에 연결된 기본 <STRONG>보관 사서함으로 이동</STRONG> 태그를 사용자가 만든 보존 정책에 추가할 수도 있습니다.



규정 준수 및 Outlook 2010에서 하 고 나중에 보관 하는 방법에 대 한 정보를 [준수 하 고 Outlook 2010에서 보관 기능에 대 한 계획](https://go.microsoft.com/fwlink/?linkid=210902)을 참조 하십시오.

## 보관 할당량

보관 사서함은 사용자가 기본 사서함 외부에 기록 메시징 데이터를 저장할 수 있도록 설계되었습니다. 경우에 따라 사용자는 사서함 저장소 할당량과 이 할당량이 초과될 때 적용되는 제한 때문에 .pst 파일을 사용하기도 합니다. 예를 들어 사용자의 사서함 크기가 *보내기 금지 할당량*을 초과하는 경우 사용자는 메시지를 보낼 수 없습니다. 또 이와 유사하게 사용자의 사서함 크기가 *보내기 및 받기 금지 할당량*을 초과하면 사용자는 메시지를 보내거나 받지 못할 수 있습니다.

.pst 파일을 사용할 필요가 없도록 사용자의 요구 사항을 충족하는 저장소 제한이 지정된 보관 사서함을 제공할 수 있습니다. 그러나 비용과 확장을 모니터링하기 위해 저장소 할당량과 보관 사서함의 증가를 계속 제어하는 것이 좋습니다.

이러한 제어가 가능하도록 보관 사서함에 *보관 경고 할당량* 및 *보관 할당량*을 구성할 수 있습니다. 보관 사서함이 지정된 보관 경고 할당량을 초과하면 경고 이벤트가 응용 프로그램 이벤트 로그에 로깅됩니다. 보관 사서함이 지정된 보관 할당량을 초과하는 경우에는 메시지가 더 이상 보관함으로 이동하지 않고 경고 이벤트가 응용 프로그램 이벤트 로그에 로깅되며 사서함 사용자에게 할당량 메시지가 전송됩니다. 기본적으로 Exchange 2013의 보관 경고 할당량은 45GB로 설정되고 보관 할당량은 50GB로 설정됩니다.

다음 표는 보관 경고 할당량과 보관 할당량이 충족될 때 전송되는 경고 메시지와 로깅되는 이벤트를 보여 줍니다.


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>할당량</th>
<th>이벤트 ID</th>
<th>종류</th>
<th>원본</th>
<th>범주</th>
<th>메시지</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>보관 경고 할당량</p></td>
<td><p>10022</p></td>
<td><p>경고</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>관리되는 폴더 도우미</p></td>
<td><p>보관 사서함 '&lt;표시 이름&gt;:&lt;GUID&gt;:&lt;사서함 데이터베이스&gt;:&lt;서버 FQDN&gt;'이(가) 보관 경고 할당량 '&lt;보관 경고 할당량&gt;'을(를) 초과했습니다. 보관 사서함 크기는 '&lt;크기&gt;'바이트입니다.</p></td>
</tr>
<tr class="even">
<td><p>보관 할당량</p></td>
<td><p>8537</p></td>
<td><p>경고</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>일반</p></td>
<td><p>&lt;레거시 DN&gt;을(를) 위한 보관 사서함이 최대 보관 사서함 크기를 초과하였습니다. 보관 사서함으로 항목을 복사하거나 이동할 수 없습니다. 보관 사서함으로 항목을 이동하는 모든 메시지 보존 작업이 실패하며 주 사서함에는 보관 사서함이 최대 크기 제한 내에 도달할 때까지 만료된 보존 태그가 있는 항목이 포함될 수 있습니다. 보관 사서함의 상태에 대해 사서함 사용자에게 알립니다.</p></td>
</tr>
</tbody>
</table>


## 원본 위치 보관 및 기타 Exchange 기능

이 섹션에서는 원본 위치 보관과 다양한 Exchange 기능에 대해 설명합니다.

  - <strong>Exchange Search</strong>   보관 사서함의 경우 메시지를 신속하게 검색하는 기능이 훨씬 더 중요합니다. Exchange Search에서는 기본 사서함과 보관 사서함이 구분되지 않습니다. 두 사서함의 콘텐츠가 모두 인덱싱됩니다. 캐시된 Exchange 모드에서 Outlook을 사용하는 경우에도 보관 사서함은 사용자 컴퓨터에 캐시되지 않으므로 보관함에 대한 검색 결과는 항상 Exchange Search에서 제공됩니다. Outlook 2010 이상 버전 및 Outlook Web App에서 전체 사서함을 검색하는 경우 검색 결과에 사용자의 기본 사서함과 보관 사서함이 포함됩니다.

  - <strong>원본 위치 eDiscovery</strong>   검색 관리자가 원본 위치 eDiscovery 검색을 수행하면 사용자의 보관 사서함도 검색됩니다. EAC(Exchange 관리 센터)에서 검색을 만들 때는 보관 사서함을 제외할 수 없습니다. Exchange 관리 셸을 사용하여 검색을 만드는 경우 *DoNotIncludeArchive* 스위치를 사용하여 보관함을 제외할 수 있습니다. 자세한 내용은 [New-MailboxSearch](https://technet.microsoft.com/ko-kr/library/dd298064\(v=exchg.150\))를 참조하십시오. 자세한 내용은 [원본 위치 eDiscovery](in-place-ediscovery-exchange-2013-help.md)를 참조하십시오.
    

    > [!IMPORTANT]
    > 원본 위치 eDiscovery를 사용하여 연결이 끊어진 사서함을 검색할 수는 없습니다.



  - <strong>원본 위치 유지 및 소송 보존</strong>   사서함에 대해 원본 위치 유지 또는 소송 보존을 사용할 경우 기본 사서함과 보관 사서함 모두에 적용됩니다. 원본 위치 유지 및 소송 보존에 대한 자세한 내용은 [원본 위치 유지 및 소송 보존](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-and-litigation-holds)를 참조하십시오.

  - <strong>복구할 수 있는 항목 폴더   </strong>보관 사서함에는 복구할 수 있는 항목 폴더가 포함되어 있으며 기본 사서함과 동일한 복구할 수 있는 항목 폴더 할당량이 적용됩니다. 복구 가능한 항목에 대한 자세한 내용은 [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)를 참조하십시오.

  - <strong>Lync 콘텐츠를 Exchange에 보관</strong>   인스턴트 메시징 대화 및 공유 온라인 모임 문서를 사용자의 기본 사서함에 보관할 수 있습니다. 이를 위해서 사서함은 Exchange 2013 사서함 서버에 있어야 하며 조직에 Microsoft Lync 2013이 배포되어 있어야 합니다. 자세한 내용은 [SharePoint 및 Lync와의 통합](integration-with-sharepoint-and-lync-exchange-2013-help.md)을 참조하십시오.

## 보관 사서함 관리

Exchange 2013에서는 보관 사서함의 생성 및 관리가 다음과 같은 일반적인 사서함 관리 작업에 통합되어 있습니다.

  - <strong>보관 사서함 만들기</strong>   사서함을 만들 때 보관 사서함을 만들거나 기존 사서함에 대해 보관 사서함을 사용하도록 설정할 수 있습니다. 자세한 내용은 [Exchange 2013에서 원본 위치 보관 관리](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)를 참조하십시오.

  - <strong>보관 사서함 이동</strong>   사용자의 보관 사서함을 기본 사서함과는 별개로 같은 사서함 서버의 다른 사서함 데이터베이스나 다른 서버로 이동할 수 있습니다. 사용자의 보관 사서함을 이동하려면 사서함 이동 요청을 만들어야 합니다. 자세한 내용은 [온-프레미스 이동 관리](manage-on-premises-moves-exchange-2013-help.md)를 참조하십시오.
    

    > [!IMPORTANT]
    > 사용자의 사서함을 찾아 다른 Exchange Server 버전에 보관할 수는 없습니다.



  - <strong>보관 사서함 사용 안 함</strong>   기본 사서함을 원본 위치 보관을 지원하지 않는 Exchange 버전으로 이동하려는 경우 또는 문제 해결을 위해 사용자의 보관 사서함을 사용하지 않도록 설정해야 할 경우가 있습니다. 보관함을 사용하지 않도록 설정하는 것은 기본 사서함을 사용하지 않도록 설정하는 것과 유사합니다. 자세한 내용은 [Exchange 2013에서 원본 위치 보관 관리](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)를 참조하십시오. 온-프레미스 배포에서 사용하지 않도록 설정된 보관 사서함은 해당 데이터베이스에 대한 삭제된 사서함 보존 기간에 도달할 때까지 사서함 데이터베이스에 보관됩니다. 이 기간 중에 보관함을 사서함 사용자에 다시 연결할 수 있습니다. 삭제된 사서함 보존 기간에 도달한 후에는 연결이 끊어진 보관 사서함이 사서함 데이터베이스에서 제거됩니다.

  - <strong>사서함 통계 및 폴더 통계 검색</strong>   [Get-MailboxStatistics](https://technet.microsoft.com/ko-kr/library/bb124612\(v=exchg.150\)) 및 [Get-MailboxFolderStatistics](https://technet.microsoft.com/ko-kr/library/aa996762\(v=exchg.150\)) cmdlet에 *Archive* 스위치를 사용하여 사용자의 보관 사서함에 대한 사서함 폴더 통계와 사서함 통계를 검색할 수 있습니다.

  - <strong>보관함 연결 테스트</strong>   Exchange 2013에서는 [Test-ArchiveConnectivity](https://technet.microsoft.com/ko-kr/library/hh529914\(v=exchg.150\)) cmdlet을 사용하여 지정된 사용자의 온-프레미스 또는 클라우드 기반 보관함과의 연결을 테스트할 수 있습니다.

