---
title: '메시지 인코딩 옵션: Exchange 2013 Help'
TOCTitle: 메시지 인코딩 옵션
ms:assetid: c1d9edbb-d87c-41e5-881b-cd612d83d7e4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb310794(v=EXCHG.150)
ms:contentKeyID: 50484085
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지 인코딩 옵션

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange에서 사용할 수 있는 메시지 인코딩 옵션은 MIME 및 비 MIME 문자 집합, 이진 인코딩, 첨부 파일 형식 등, 메시지 특성을 지정합니다. 메시지 인코딩 옵션은 다음 위치에 지정할 수 있습니다.

  - 원격 도메인 설정

  - 메일 사용자 및 메일 연락처 설정

  - Microsoft Outlook 설정
    
      - 메시지 형식
    
      - 인터넷 메시지 형식
    
      - 인터넷 받는 사람 메시지 형식
    
      - 메시지 문자 집합 인코딩 옵션

**콘텐츠**

Message encoding options for messages sent to remote domains

Message encoding options for mail users and mail contacts

Message encoding options available in Outlook

메시지 인코딩 Outlook Web App에서 사용할 수 있는 옵션

Order of precedence for message encoding options

자세한 내용은

## 원격 도메인에 보내는 메시지에 대한 메시지 인코딩 옵션

원격 도메인에 대해 메시지 인코딩 옵션을 구성할 경우 특정 설정은 해당 도메인으로 전송되는 모든 메시지에 적용됩니다. 조직의 원격 도메인에 대해 다음과 같은 메시지 인코딩 구성 옵션을 사용할 수 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>설정</strong></p></td>
<td><p><strong>Exchange Online 전용 환경의 EAC에서 사용 가능</strong></p></td>
<td><p><strong>셸에서 사용 가능</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>MIME 문자 집합</strong>   지정한 문자 집합은 고유의 문자 집합이 지정되지 않은 MIME 메시지에만 사용됩니다. 이 매개 변수를 설정해도 보내는 메일에 이미 지정되어 있는 문자 집합은 그대로 사용됩니다.</p>
<p><strong>비 MIME 문자 집합</strong>   이 설정은 다음 조건 중 일부가 true인 경우 사용됩니다.</p>
<ul>
<li><p>원격 도메인으로부터 받는 메시지의 MIME Content-Type: 헤더 필드에 <em>charset=</em> 설정 값이 없는 경우</p></li>
<li><p>원격 도메인으로 보내는 메시지에 MIME 문자 집합 값이 없는 경우</p></li>
</ul>
<p></p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p><strong>콘텐츠 형식</strong>   원격 도메인의 받는 사람에게 전송되는 MIME 메시지의 콘텐츠 형식을 지정할 수 있습니다. 다음 설정을 사용할 수 있습니다.</p>
<ul>
<li><p><strong>MimeHtmlText</strong>   원본 메시지가 텍스트 메시지가 아니면 모든 메시지는 HTML 서식을 사용하는 MIME 메시지로 변환됩니다. 원본 메시지가 텍스트 메시지인 경우 보내는 메시지는 텍스트 서식을 사용하는 MIME 메시지가 됩니다. 기본 설정입니다.</p></li>
<li><p><strong>MimeText</strong>   모든 메시지를 텍스트 서식을 사용하는 MIME 메시지로 변환합니다.</p></li>
<li><p><strong>MimeHtml</strong>   모든 메시지를 HTML 서식을 사용하는 MIME 메시지로 변환합니다.</p></li>
</ul></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p><strong>줄 바꿈 크기</strong>   전자 메일 메시지 본문의 텍스트 한 줄에 입력할 수 있는 최대 문자 수를 지정할 수 있습니다. 이전의 전자 메일 클라이언트 응용 프로그램에서는 한 줄당 78자인 경우가 많았습니다. 이 옵션은 셸에서만 사용할 수 있습니다.</p>
<p></p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 메일 사용자 및 메일 연락처에 대한 메시지 인코딩 옵션

메일 연락처 또는 메일 사용자에 대해 메시지 인코딩 옵션을 구성할 경우 이 옵션은 특정 받는 사람에게 전송되는 모든 메시지에 적용됩니다. 조직의 메일 연락처 및 메일 사용자에 대해 다음과 같은 메시지 인코딩 구성 옵션을 사용할 수 있습니다.

  - **UsePreferMessageFormat**   이 매개 변수는 메일 연락처에 대해 구성된 메시지 형식 설정이 원격 도메인에 대해 구성된 전역 설정을 재정의하는지 여부를 지정합니다. 이 설정을 사용하지 않을 경우 Exchange는 이 받는 사람에 대한 다른 메시지 인코딩 옵션을 무시하며 메시지 인코딩은 원격 도메인의 구성 또는 메시지 보낸 사람이 구성한 설정에 의해 결정됩니다.

  - **MessageFormat**   이 매개 변수는 메시지 형식을 지정합니다. Text 또는 Mime을 메시지 형식으로 지정할 수 있습니다. 이 설정의 값은 *MessageBodyFormat* 매개 변수에 따라 달라집니다. 메시지 본문 형식이 Html 또는 TextAndHtml인 경우에는 이 매개 변수를 Mime으로 설정해야 합니다.

  - **MessageBodyFormat**   이 매개 변수는 메시지 본문 형식을 지정합니다. Text, Html 또는 TextAndHtml을 지정할 수 있습니다. 이 설정의 값은 *MessageFormat* 매개 변수에 따라 달라집니다. 메시지 형식이 Text인 경우에는 이 매개 변수도 Text로 설정해야 합니다.

  - **MacAttachmentFormat** 이 매개 변수는 메시지의 Apple Macintosh 운영 체제 첨부 파일 형식을 지정합니다. BinHex, UuEncode, AppleSingle 또는 AppleDouble을 지정할 수 있습니다. 이 설정의 값은 *MessageFormat* 매개 변수에 따라 달라집니다. 메시지 형식이 Text로 설정된 경우에는 이 매개 변수를 BinHex 또는 UuEncode로 설정해야 합니다. 메시지 형식이 Mime으로 설정된 경우에는 이 매개 변수를 BinHex, AppleSingle 또는 AppleDouble로 설정해야 합니다.

Exchange 관리 셸에서 이러한 매개 변수를 사용하여 메일 사용자 및 메일 연락처에 대한 메시지 인코딩 옵션을 설정해야 합니다. 자세한 내용은 다음 항목을 참조하십시오.

  - [Enable-MailContact](https://technet.microsoft.com/ko-kr/library/aa996001\(v=exchg.150\))

  - [New-MailContact](https://technet.microsoft.com/ko-kr/library/bb124519\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/ko-kr/library/aa995950\(v=exchg.150\))

  - [Enable-MailUser](https://technet.microsoft.com/ko-kr/library/aa996549\(v=exchg.150\))

  - [New-MailUser](https://technet.microsoft.com/ko-kr/library/aa996335\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/ko-kr/library/aa995971\(v=exchg.150\))

맨 위로 이동

## Outlook에서 사용할 수 있는 메시지 인코딩 옵션

보낸 사람으로서 Outlook에서 다음과 같이 메시지 인코딩 옵션을 지정할 수 있습니다.

  - 기본 메시지 형식을 일반 텍스트 또는 HTML로 구성

  - 메시지를 작성하는 동안 **옵션** 탭의 **형식** 영역을 사용하여 메시지 형식을 일반 텍스트 또는 HTML로 설정

  - Exchange 조직 외부의 받는 사람 모두에게 보내는 메시지에 대한 메시지 인코딩 옵션 구성 이러한 옵션은 *인터넷 메시지 형식* 옵션이라고 하며 Exchange 조직 내 받는 사람이 아닌 원격 받는 사람에게만 적용됩니다.

  - Exchange 조직 외부의 받는 사람 일부에게 보내는 메시지에 대한 메시지 인코딩 옵션 지정 이러한 옵션은 *인터넷 받는 사람 메시지 형식* 옵션이라고 하며 Exchange 조직 내 받는 사람이 아닌 연락처 폴더의 원격 받는 사람에게만 적용됩니다.

기본적으로 Outlook에서는 보내는 메시지의 전체 텍스트를 검사하는 자동 문자 집합 메시지 인코딩을 사용하여 메시지에 사용할 적합한 인코딩을 결정합니다. 이 설정은 인터넷상으로 받는 사람 및 Exchange 조직의 받는 사람에게 보내는 메시지에 적용됩니다. 그러나 이 과정을 생략하고 보내는 메시지에 대한 기본 인코딩을 지정할 수도 있습니다.

맨 위로 이동

## Outlook Web App에서 사용할 수 있는 메시지 인코딩 옵션

보낸 사람은 Outlook Web App에서 다음과 같이 메시지 인코딩 옵션을 지정할 수 있습니다.

  - By configuring the default message format to be either plain text or HTMLin the section of the **설정** \>**옵션** \> **설정** 페이지의 **메시지 형식** 섹션에서 기본 메시지 형식을 일반 텍스트 또는 HTML로 구성

  - **기타 옵션**(…) 메뉴에서 **일반 텍스트로 전환** 또는 **HTML로 전환**을 사용하여 작성 중인 메시지 형식을 일반 텍스트 또는 HTML로 설정

맨 위로 이동

## 메시지 인코딩 옵션의 우선 순위

Exchange에서는 다음 목록의 우선 순위를 사용하여 Exchange 조직 외부의 받는 사람에게 보내는 메시지의 메시지 인코딩 옵션을 결정합니다.

1.  원격 도메인 설정

2.  Outlook 또는 Outlook Web App 설정

3.  메일 사용자 또는 메일 연락처 설정

목록에는 최하위부터 최상위까지의 우선 순위 순서가 지정되어 있습니다. 상위 수준에서 만든 설정에 의해 하위 수준에서 만든 설정이 무시될 수도 있습니다.

다음 표에서는 낮은 우선 순위부터 높은 우선 순위까지, 메시지 문자 집합 인코딩 옵션의 우선 순위에 대해 설명합니다.

### 낮은 우선 순위부터 높은 우선 순위까지, 메시지 문자 집합 인코딩 옵션의 우선 순위

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>원본</th>
<th>매개 변수</th>
<th>값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>원격 도메인 항목 설정, EAC 또는 <strong>Set-RemoteDomain</strong> 사용</p></td>
<td><p><em>CharacterSet</em></p></td>
<td><p>지정됨</p></td>
</tr>
<tr class="even">
<td><p>원격 도메인 항목 설정, EAC 또는 <strong>Set-RemoteDomain</strong> 사용</p></td>
<td><p><em>NonMimeCharacterSet</em></p></td>
<td><p>지정됨</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 설정</p></td>
<td><p>메시지 문자 집합 인코딩</p></td>
<td><ul>
<li><p>자동 선택</p></li>
<li><p>지정됨</p></li>
</ul></td>
</tr>
</tbody>
</table>


원격 도메인에 대해 MIME이 아닌 문자 집합을 설정한 경우 이 문자 집합은 다음 유형의 메시지에 할당됩니다.

  - 지정된 문자 집합을 포함하지 않고, 구성된 원격 도메인으로 보내는 메시지

  - 지정된 문자 집합을 포함하지 않고, 구성된 원격 도메인으로부터 받는 메시지

다음 메시지 형식에 문자 집합을 지정할 때 전송 서버의 Windows ANSI 코드 페이지 값이 사용됩니다.

  - 지정된 문자 집합을 포함하지 않는 내부 메시지

  - 지정된 문자 집합을 포함하지만 지정된 서버 코드 페이지가 없는 내부 메시지

메시지에 유효하지 않은 문자 집합이 지정되어 있을 경우 전송 서버에서는 유효하지 않은 문자 집합을 유효한 문자 집합으로 바꾸려고 시도합니다.

다음 표에서는 낮은 우선 순위부터 높은 우선 순위까지, 일반 텍스트 메시지 인코딩 옵션의 우선 순위에 대해 설명합니다.

### 낮은 우선 순위부터 높은 우선 순위까지, 일반 텍스트 메시지 인코딩 옵션의 우선 순위

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>원본</th>
<th>매개 변수</th>
<th>값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>LineWrapSize</em></p></td>
<td><ul>
<li><p>0~132</p></li>
<li><p>제한 없음</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 설정</p></td>
<td><p>메시지 형식</p></td>
<td><p>일반 텍스트</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 설정</p></td>
<td><p>인터넷 메시지 형식</p></td>
<td><p>일반 텍스트 옵션:</p>
<ul>
<li><p>일반 텍스트 메시지를 보낼 때 UuEncode 형식으로 첨부 파일 인코딩</p></li>
<li><p><em>nn</em> 문자 길이 단위로 텍스트 자동 줄 바꿈</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 설정</p></td>
<td><p>인터넷 받는 사람 메시지 형식</p></td>
<td><p>일반 텍스트 형식:</p>
<ul>
<li><p>UuEncode 첨부 파일 형식으로 첨부 파일 인코딩</p></li>
<li><p>BinHex Mac 첨부 파일 형식 사용</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><ul>
<li><p><code>$true</code></p></li>
<li><p><code>$false</code></p></li>
</ul>
<p>값이 <code>$false</code>이거나 받는 사람이 Exchange 조직에서 메일 사용자 또는 메일 연락처로 정의되어 있지 않으면 메일 사용자 또는 메일 연락처 설정이 무시됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><p>텍스트</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><p>텍스트</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>UuEncode</p></li>
</ul></td>
</tr>
</tbody>
</table>


다음 표에서는 낮은 우선 순위부터 높은 우선 순위까지, MIME 메시지 인코딩 옵션의 우선 순위에 대해 설명합니다.

### 낮은 우선 순위부터 높은 우선 순위까지, MIME 메시지 인코딩 옵션의 우선 순위

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>원본</th>
<th>매개 변수</th>
<th>값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>ContentType</em></p></td>
<td><ul>
<li><p><code>MimeHtmlText</code></p></li>
<li><p><code>MimeText</code></p></li>
<li><p><code>MimeHtml</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 또는 Outlook Web App 설정</p></td>
<td><p>메시지 형식</p></td>
<td><ul>
<li><p>일반 텍스트</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 설정</p></td>
<td><p>인터넷 받는 사람 메시지 형식</p></td>
<td><p>MIME 메시지 형식</p>
<ul>
<li><p>일반 텍스트</p></li>
<li><p>일반 텍스트 및 HTML 모두 포함</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><p><code>$true</code></p>
<p><code>$false</code></p>
<p>값이 <code>$false</code>이거나 받는 사람이 Exchange 조직에서 메일 사용자 또는 메일 연락처로 정의되어 있지 않으면 메일 사용자 또는 메일 연락처 설정이 무시됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><ul>
<li><p>텍스트</p></li>
<li><p>Mime</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><ul>
<li><p><code>Text</code></p></li>
<li><p><code>Html</code></p></li>
<li><p><code>TextAndHtml</code></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>AppleSingle</p></li>
<li><p>AppleDouble</p></li>
</ul></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 자세한 내용

[메시지 인코딩 옵션](message-encoding-options-exchange-2013-help.md)

[TNEF 변환 옵션](tnef-conversion-options-exchange-2013-help.md)

[원격 도메인](remote-domains-exchange-2013-help.md)

[Exchange Online의 원격 도메인](https://technet.microsoft.com/ko-kr/library/jj966211\(v=exchg.150\))

[메일 사용자 관리](https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-mail-users)

[메일 연락처 관리](https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-mail-contacts)

[Outlook의 메시지 형식 변경](https://go.microsoft.com/fwlink/p/?linkid=397890)

