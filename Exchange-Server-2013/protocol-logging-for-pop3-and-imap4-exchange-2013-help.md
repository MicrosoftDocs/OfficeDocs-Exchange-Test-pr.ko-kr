---
title: 'POP3 및 IMAP4 프로토콜 로깅: Exchange 2013 Help'
TOCTitle: POP3 및 IMAP4 프로토콜 로깅
ms:assetid: 212ed3d5-0c98-4346-a860-1cfcac5d73c4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335141(v=EXCHG.150)
ms:contentKeyID: 50555958
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# POP3 및 IMAP4 프로토콜 로깅

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

프로토콜 로깅을 사용하여 Exchange 환경의 POP3 및 IMAP4 연결을 검토할 수 있습니다. POP3 또는 IMAP4 성능 관련 문제를 해결하는 경우에 유용합니다.

## POP3 및 IMAP4 프로토콜 로깅 사용

Exchange 관리 셸을 사용하여 프로토콜 로깅을 사용하거나 사용하지 않도록 설정하거나, 변경할 수 있습니다. 셸을 사용하여 프로토콜 로깅을 사용하도록 설정하면 기본 프로토콜 로깅 설정이 사용됩니다. 대부분의 경우 기본 설정만으로도 충분합니다.

또는 Microsoft Exchange Server 2013 클라이언트 액세스 서버에 있는 Microsoft.Exchange.Pop3.exe.config 및 Microsoft.Exchange.Imap4.exe.config 구성 파일을 편집하여 프로토콜 로깅 옵션을 사용하거나 사용하지 않도록 설정하고 수정할 수 있습니다. POP3 및 IMAP4 프로토콜 설정을 관리하는 방법에 대한 자세한 내용은 [POP3 및 IMAP4 프로토콜 로깅 구성](configure-protocol-logging-for-pop3-and-imap4-exchange-2013-help.md)을 참조하십시오.

## 프로토콜 로그 검토

프로토콜 로그 파일은 CSV(쉼표로 구분된 값) 파일 형식으로 데이터가 포함된 텍스트 파일입니다. 프로토콜 로그는 각 프로토콜 이벤트를 한 줄에 저장합니다. 각 줄에 저장된 정보는 필드로 구성되고 이러한 필드는 쉼표로 분리됩니다. 다음 표에서는 각 프로토콜 이벤트를 분류하는 데 사용되는 필드에 대해 설명합니다.

### 각 프로토콜 이벤트를 분류하는 데 사용되는 필드

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>필드 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>date-time</p></td>
<td><p>프로토콜 이벤트의 날짜와 시간입니다. 값은 <em>yyyy-mm-ddhh:mm:ss.fffZ</em> 형식입니다. 여기서 <em>yyyy</em>는 년, <em>mm</em>은 월, <em>dd</em>는 일, <em>hh</em>는 시, <em>mm</em>은 분, <em>ss</em>는 초, <em>fff</em>는 밀리초이며, <em>Z</em>는 Zulu를 의미합니다. Zulu는 UTC(협정 세계시)를 표시하는 또 하나의 방법입니다.</p></td>
</tr>
<tr class="even">
<td><p>connector-id</p></td>
<td><p>이 필드는 POP3 및 IMAP4 프로토콜 로깅에는 사용되지 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p>session-id</p></td>
<td><p>프로토콜 이벤트와 관련된 SMTP 세션을 고유하게 식별하는 GUID입니다.</p></td>
</tr>
<tr class="even">
<td><p>sequence-number</p></td>
<td><p>같은 세션 내에서 각 이벤트에 대해 0에서 시작하여 증가되는 카운터입니다.</p></td>
</tr>
<tr class="odd">
<td><p>local-endpoint</p></td>
<td><p>POP3 또는 IMAP4 세션의 로컬 끝점입니다. IP 주소와 TCP 포트 번호로 구성되며, 그 형식은 <em>&lt;IP 주소&gt;</em>:<em>&lt;포트&gt;</em>입니다.</p></td>
</tr>
<tr class="even">
<td><p>remote-endpoint</p></td>
<td><p>POP3 또는 IMAP4 세션의 원격 끝점입니다. IP 주소와 TCP 포트 번호로 구성되며, 그 형식은 <em>&lt;IP 주소&gt;</em>:<em>&lt;포트&gt;</em>입니다.</p></td>
</tr>
<tr class="odd">
<td><p>event</p></td>
<td><p>프로토콜 이벤트를 표시하는 단일 문자입니다. 이벤트에 대해 가능한 값은 다음과 같습니다.</p>
<ul>
<li><p>+   연결</p></li>
<li><p>-   연결 끊기</p></li>
<li><p>&gt;   보내기</p></li>
<li><p>&lt;   받기</p></li>
<li><p>*   정보</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>데이터</p></td>
<td><p>POP3 또는 IMAP4 이벤트와 관련된 텍스트 정보입니다.</p></td>
</tr>
<tr class="odd">
<td><p>context</p></td>
<td><p>이 필드는 POP3 및 IMAP4 프로토콜 로깅에는 사용되지 않습니다.</p></td>
</tr>
</tbody>
</table>

