---
title: 'Exchange 검색에서 인덱싱하는 메시지 속성: Exchange 2013 Help'
TOCTitle: Exchange 검색에서 인덱싱하는 메시지 속성
ms:assetid: a9754dc1-44aa-4076-8b59-a5d39246d5b0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ983804(v=EXCHG.150)
ms:contentKeyID: 52058119
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 검색에서 인덱싱하는 메시지 속성

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-17_

Exchange 검색에서는 전자 메일 메시지의 보낸 사람, 받는 사람, 메시지 본문, 첨부 파일 등 다양한 항목 속성을 인덱싱합니다.

## Exchange 검색에서 인덱싱하는 속성

다음 표에는 Exchange 검색에서 인덱싱하는 모든 항목 속성의 목록이 포함되어 있습니다.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>속성</th>
<th>유형</th>
<th>쿼리 가능</th>
<th>검색 가능</th>
<th>조회 가능</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Account</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Assistantname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Attachmentfilenames</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Attachmentmetaproperties</p></td>
<td><p>문자열</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Attachmentcount</p></td>
<td><p>정수</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Bcc</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Businessaddress</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Businessmainphone</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Businessphonenumber</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Carphonenumber</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>범주</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Companyname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Compositeitemid</p></td>
<td><p>문자열</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Conversationid</p></td>
<td><p>정수</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>Conversationtopic</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Departmentname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Displayname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Displaynameprefix</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Documentid</p></td>
<td><p>정수</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Emailaddress</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Emaildisplayname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Emailoriginaldisplayname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Errorcode</p></td>
<td><p>정수</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Fileas</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Firstname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Folderid</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>From</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Homeaddress</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Homephone</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>정수</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Ispartiallyprocessed</p></td>
<td><p>부울</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Ispermanentfailure</p></td>
<td><p>부울</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>Itemclass</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Lastattempttime</p></td>
<td><p>DateTime</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Lastname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Mailboxguid</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Manager</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Meetinglocation</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Middlename</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Mobilephonenumber</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Nickname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Officelocation</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Otheraddress</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Primarytelephonenumber</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>DateTime</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Receivedby</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Receivedrepresenting</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Recipients</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>DateTime</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Sharinginfo</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>정수</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Tasktitle</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Title</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Umaudionotes</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Watermark</p></td>
<td><p>정수</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>Yomicompanyname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>Yomifirstname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>Yomilastname</p></td>
<td><p>문자열</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
</tbody>
</table>


**인덱싱되는 속성에 대한 참고 사항**:

  - Outlook Web App `property:value` 쌍, `from:bsuneja@cotoso.com`등의 예: 검색 클라이언트에 의해 AQS 쿼리에서 **쿼리 가능 속성** 을 사용할 수 있습니다. 앞의 표에 나열 된 쿼리 가능 속성의 하위 집합 검색 쿼리에서 원본 위치 eDiscovery에 대 한 사용할 수도 있습니다. 이러한 속성의 목록이 [원본 위치 eDiscovery에 대 한 메시지의 속성 및 검색 연산자](message-properties-and-search-operators-for-in-place-ediscovery-exchange-2013-help.md)을 참조 하십시오.

  - **검색 가능 속성**은 `property:value` 쌍에서는 지정할 수 없는 속성이지만 키워드 검색에서는 검색 가능 속성에서 값이 발견되는 경우 해당 값을 반환합니다. 예를 들어 `body:Contoso`를 사용하여 메시지 본문에서만 `contoso` 문자열을 검색할 수는 없습니다. 그러나 해당 문자열을 검색하면 검색 가능 속성에서 해당 속성이 발견되는 모든 항목이 반환됩니다.

  - `documenteid` 및 `ispartiallyprocessed` 등의 **조회 가능 속성**은 모든 검색에서 반환됩니다.

