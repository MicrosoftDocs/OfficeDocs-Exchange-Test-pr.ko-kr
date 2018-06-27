---
title: 'Exchange 검색에서 인덱싱하는 파일 형식: Exchange 2013 Help'
TOCTitle: Exchange 검색에서 인덱싱하는 파일 형식
ms:assetid: e5110ac1-28e1-4554-acc3-85d08c997bc5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633485(v=EXCHG.150)
ms:contentKeyID: 52058126
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 검색에서 인덱싱하는 파일 형식

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-07-21_

Microsoft Exchange Server 2013 및 Exchange Online에서 Exchange 검색에는 메시지 첨부 파일로 포함된 가장 일반적인 유형의 파일 형식을 인덱싱하기 위한 필터가 포함되어 있습니다. 추가 파일 형식을 인덱싱하기 위해 필터를 설치할 수도 있습니다.


> [!NOTE]
> Exchange 2013에서는 Microsoft Office Filter Pack을 설치 및 등록할 필요가 없습니다.<BR>기본적으로 Exchange Server 2013 온-프레미스 인덱싱할 수 있는 최대 크기 파일은 32 000MB입니다. 한계를 늘리려면이 크기, 조직에서 모든 CAS 서버 및 다중 역할 서버에 다음 레지스트리 키를 추가 해야 하면:<BR><CODE>@"SOFTWARE\Microsoft\ExchangeServer\V15\Search\SystemParameters" DWORD: "MaxAttachmentSize"</CODE>



Exchange 검색 및 종속 기능(예: [원본 위치 eDiscovery](in-place-ediscovery-exchange-2013-help.md))을 관리하거나 사용할 때는 인덱싱하지 않도록 설정되거나 인덱싱할 수 없는 콘텐츠를 포함하는 파일 형식과 검색할 수 없는 항목 간의 차이점을 고려하십시오.

  - **검색할 수 없는 항목**   Exchange 검색이 어떠한 이유로 특정 파일 형식을 인덱싱할 수 없는 경우(예: 필터가 설치되지 않은 경우) 이러한 파일 형식에 대한 검색이 실패합니다. 이러한 첨부 파일을 포함하는 메시지는 *부분적으로 인덱싱됨*으로 표시됩니다. 검색할 수 없는 항목은 [Get-FailedContentIndexDocuments](https://technet.microsoft.com/ko-kr/library/dd351154\(v=exchg.150\)) cmdlet을 사용하면 검색할 수 있습니다. 원본 위치 eDiscovery 검색 결과를 검색 사서함에 복사하거나 PST 파일로 검색 결과를 내보낼 때는 검색할 수 없는 항목을 포함할 수 있습니다. 자세한 내용은 [Exchange eDiscovery의 검색할 수 없는 항목](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)을 참조하세요.

  - **인덱싱할 수 없는 콘텐츠가 포함된 파일 형식**   WMV(Windows Media 비디오) 등의 특정 파일 형식은 인덱싱할 수 있는 콘텐츠를 포함하지 않으므로 인덱싱할 수 없습니다. 이러한 파일 형식의 첨부 파일을 포함하는 메시지도 원본 위치 eDiscovery 검색에서 검색할 수 없는 항목으로 반환됩니다.

  - **사용하지 않도록 설정된 파일 형식** 온-프레미스 조직에서는 지정된 파일 형식을 관리자가 인덱싱하지 않도록 설정할 수 있습니다. 사용하지 않도록 설정된 형식의 첨부 파일을 포함하는 메시지는 검색할 수 없는 항목으로 반환됩니다.


> [!IMPORTANT]
> 메시지 첨부 파일은 검색할 수 없는 상태이거나 인덱싱할 수 없는 파일 형식이더라도 메시지 제목, 메시지 본문 및 기타 메타데이터는 인덱싱할 수 있으므로 검색에서 메시지를 반환할 수 있습니다.



온-프레미스 조직의 Exchange 검색과 관련된 추가 관리 작업에 대한 자세한 내용은 [Exchange 검색 절차](exchange-search-procedures-exchange-2013-help.md)를 참조하십시오.

## 기본 필터

다음 표에는 Exchange 2013 사서함 서버 및 Exchange Online에 설치된 기본 검색 필터가 나와 있습니다. [Get-SearchDocumentFormat](https://technet.microsoft.com/ko-kr/library/jj873755\(v=exchg.150\)) cmdlet을 사용하여 기본 필터 목록을 검색할 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>필터</th>
<th>파일 확장명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>전자 메일 메시지</p></td>
<td><p>.eml</p></td>
</tr>
<tr class="even">
<td><p>GIF(Graphics Interchange Format)</p></td>
<td><p>.gif</p></td>
</tr>
<tr class="odd">
<td><p>JPEG</p></td>
<td><p>.jpeg</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Excel</p></td>
<td><p>.xls, .xlt, .xlsx, .xlsm, .xlb, .xlc, .xlsb</p></td>
</tr>
<tr class="odd">
<td><p>Excel 파일</p></td>
<td><p>odbcexcel</p></td>
</tr>
<tr class="even">
<td><p>Microsoft InfoPath</p></td>
<td><p>.infopathml</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office Binder</p></td>
<td><p>.obt, obd</p></td>
</tr>
<tr class="even">
<td><p>Microsoft PowerPoint</p></td>
<td><p>.pptx, .pptm, .ppt, .ppsx, .ppsm, .pps, .ppam, .potm, .pot, .potx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Publisher</p></td>
<td><p>.pub</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Word</p></td>
<td><p>.doc, .docm, .dotx, .dotm, .dot, .docx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft XPS(XML Paper Specification)</p></td>
<td><p>.xps</p></td>
</tr>
<tr class="even">
<td><p>OneNote</p></td>
<td><p>.one</p></td>
</tr>
<tr class="odd">
<td><p>OpenDocument 프레젠테이션</p></td>
<td><p>.odp</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument 스프레드시트</p></td>
<td><p>.ods</p></td>
</tr>
<tr class="odd">
<td><p>OpenDocument 텍스트</p></td>
<td><p>.odt</p></td>
</tr>
<tr class="even">
<td><p>Outlook 항목</p></td>
<td><p>.msg</p></td>
</tr>
<tr class="odd">
<td><p>PDF(Portable Document Format)</p></td>
<td><p>.pdf</p></td>
</tr>
<tr class="even">
<td><p>서식 있는 텍스트</p></td>
<td><p>.rtf</p></td>
</tr>
<tr class="odd">
<td><p>텍스트</p></td>
<td><p>.txt</p></td>
</tr>
<tr class="even">
<td><p>vCalendar</p></td>
<td><p>.vcs</p></td>
</tr>
<tr class="odd">
<td><p>vCard</p></td>
<td><p>.vcf</p></td>
</tr>
<tr class="even">
<td><p>Visio</p></td>
<td><p>.vdw, .vsd, .vss, .vst, .vsx, .vtx, .vssx, .vssm, .vsdm, .vstx, .vstm, .vdx</p></td>
</tr>
<tr class="odd">
<td><p>웹 보관 파일</p></td>
<td><p>.mhtml</p></td>
</tr>
<tr class="even">
<td><p>웹 페이지</p></td>
<td><p>.html</p></td>
</tr>
<tr class="odd">
<td><p>XML 문서</p></td>
<td><p>.xml</p></td>
</tr>
<tr class="even">
<td><p>ZIP 보관 파일</p></td>
<td><p>.zip</p></td>
</tr>
</tbody>
</table>


## 사용할 수 없는 파일 형식

다음 표에는 Exchange 2013 사서함 서버 및 Exchange Online에서 기본적으로 인덱싱할 수 없도록 설정된 검색 필터가 나와 있습니다. Exchange 2013에서는 관리자가 [Set-SearchDocumentFormat](https://technet.microsoft.com/ko-kr/library/jj873756\(v=exchg.150\)) cmdlet을 사용하여 인덱싱을 위해 지원되는 파일 형식을 사용하지 않도록 설정하거나 다시 사용하도록 설정할 수 있습니다. Exchange Online에서는 이 cmdlet이 제공되지 않습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>필터</th>
<th>파일 확장명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVI</p></td>
<td><p>.avi</p></td>
</tr>
<tr class="even">
<td><p>비트맵</p></td>
<td><p>.bmp</p></td>
</tr>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>.mp3</p></td>
</tr>
<tr class="even">
<td><p>MPEG</p></td>
<td><p>.mpeg</p></td>
</tr>
<tr class="odd">
<td><p>PNG</p></td>
<td><p>.png</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Windows 웨이브 오디오</p></td>
<td><p>.wav</p></td>
</tr>
</tbody>
</table>

