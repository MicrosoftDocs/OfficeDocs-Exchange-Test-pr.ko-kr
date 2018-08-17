---
title: 'Exchange 2013 개체 이름에 대 한 지원 되지않는 문자: Exchange 2013 Help'
TOCTitle: Exchange 2013 개체 이름에 대 한 지원 되지않는 문자
ms:assetid: 76fa4e23-f0f6-473b-9227-70ded907578f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn169553(v=EXCHG.150)
ms:contentKeyID: 54651820
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 개체 이름에 대 한 지원 되지않는 문자

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

이 문서에서는 Exchange 2013에서 개체나 구성 요소 이름에 사용할 수 없는 문자에 대해 설명합니다. Exchange 2013에서 개체나 구성 요소의 이름을 만들 때 지원되지 않는 문자를 사용하여 개체를 만들 수 있더라도 개체 이름에 지원되지 않는 문자가 포함되면 안 됩니다. 또한 이름에 지원되지 않는 문자가 포함된 개체를 가져오거나 이 개체에 연결할 경우 오류 메시지가 표시되거나 예기치 않은 동작이 수행될 수 있습니다.

## 지원되지 않는 문자

다음 표에는 Exchange 관련 개체나 구성 요소의 이름에서 지원되지 않는 문자가 나와 있습니다. 또한 지원되지 않는 문자를 사용할 경우 문제가 발생할 수 있는 시나리오도 나와 있습니다. 표에 나열된 각 개체에는 최대 64자까지 포함될 수 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 개체나 구성 요소</th>
<th>Exchange 시나리오</th>
<th>지원되지 않는 문자</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>전자 메일 도메인 이름</p></td>
<td><p>SMTP(Simple Mail Transfer Protocol) 커넥터</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>커넥터 주소 공간의 호스트 이름</p></td>
<td><p>메일 흐름</p></td>
<td><p><code>..</code>(마침표 두 개)</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 서버의 호스트 이름</p></td>
<td><p>SMTP</p></td>
<td><p><code>_</code>(밑줄)</p></td>
</tr>
<tr class="even">
<td><p>조직이나 사이트 이름</p></td>
<td><p>설치 프로그램 실행 또는 사서함 이동</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 내부 디렉터리 이름</p></td>
<td><p>디렉터리</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 트리 이름</p></td>
<td><p>공용 폴더 보기 및 만들기</p></td>
<td><p><code>: ;</code></p></td>
</tr>
<tr class="odd">
<td><p>받는 사람 이름</p></td>
<td><p>SMTP</p></td>
<td><p><code>' &quot;</code></p></td>
</tr>
<tr class="even">
<td><p>받는 사람 정책 SMTP 주소</p></td>
<td><p>공용 폴더 계층 구조 보기</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>받는 사람 정책 SMTP 주소 호스트 이름</p></td>
<td><p>메일 흐름</p></td>
<td><p><code>..</code>(마침표 두 개)</p></td>
</tr>
<tr class="even">
<td><p>사이트 내부 디렉터리 이름</p></td>
<td><p>공용 폴더 계층 구조 보기</p></td>
<td><p><code>? ( ) *</code></p></td>
</tr>
<tr class="odd">
<td><p>스마트 호스트 이름</p></td>
<td><p>SMTP</p></td>
<td><p>선행 공백 또는 후행 공백</p></td>
</tr>
</tbody>
</table>

