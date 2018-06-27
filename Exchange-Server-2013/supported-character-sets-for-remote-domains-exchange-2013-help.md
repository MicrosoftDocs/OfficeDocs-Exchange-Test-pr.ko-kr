---
title: '원격 도메인에 대해 지원되는 문자 집합: Exchange 2013 Help'
TOCTitle: 원격 도메인에 대해 지원되는 문자 집합
ms:assetid: 66023a62-1fd3-4019-be2b-4e7147db148a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998600(v=EXCHG.150)
ms:contentKeyID: 52057931
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원격 도메인에 대해 지원되는 문자 집합

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

원격 도메인에 보내는 메시지에 대 한 다음 문자 집합을 지정할 수 있습니다.

  - Exchange 관리 센터에서 (EAC) **원격 도메인** 설정 페이지에서 **MIME 문자 집합** 및 **MIME 이외 문자 집합** 드롭다운 목록에서 이름을 선택 합니다.

  - 셸에서 *CharacterSet* 매개 변수 또는 [Set-RemoteDomain](https://technet.microsoft.com/ko-kr/library/aa997857\(v=exchg.150\)) cmdlet에서 *NonMimeCharacterSet* 매개 변수는 다음 표에 이름 열에서 값을 사용 합니다.

### 원격 도메인 구성에 대해 지원되는 문자 집합

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>big5</p></td>
<td><p>중국어 번체(Big5)</p></td>
</tr>
<tr class="even">
<td><p>DIN_66003</p></td>
<td><p>독일어(IA5)</p></td>
</tr>
<tr class="odd">
<td><p>euc-jp</p></td>
<td><p>일본어(EUC)</p></td>
</tr>
<tr class="even">
<td><p>euc-kr</p></td>
<td><p>한국어(EUC)</p></td>
</tr>
<tr class="odd">
<td><p>GB18030</p></td>
<td><p>중국어 간체(GB18030)</p></td>
</tr>
<tr class="even">
<td><p>gb2312</p></td>
<td><p>중국어 간체(GB2312)</p></td>
</tr>
<tr class="odd">
<td><p>hz-gb-2312</p></td>
<td><p>중국어 간체(HZ)</p></td>
</tr>
<tr class="even">
<td><p>iso-2022-jp</p></td>
<td><p>일본어(JIS)</p></td>
</tr>
<tr class="odd">
<td><p>iso-2022-kr</p></td>
<td><p>한국어(ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-1</p></td>
<td><p>서유럽어(ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-2</p></td>
<td><p>중앙 유럽어(ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-3</p></td>
<td><p>라틴어 3(ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-4</p></td>
<td><p>발트어(ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-5</p></td>
<td><p>키릴 자모(ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-6</p></td>
<td><p>아랍어(ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-7</p></td>
<td><p>그리스어(ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-8</p></td>
<td><p>히브리어(ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-9</p></td>
<td><p>터키어(ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-13</p></td>
<td><p>에스토니아어(ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-15</p></td>
<td><p>라틴어 9(ISO)</p></td>
</tr>
<tr class="odd">
<td><p>koi8-r</p></td>
<td><p>키릴 자모(KOI8-R)</p></td>
</tr>
<tr class="even">
<td><p>koi8-u</p></td>
<td><p>키릴 자모(KOI8-U)</p></td>
</tr>
<tr class="odd">
<td><p>ks_c_5601-1987</p></td>
<td><p>한국어(Windows)</p></td>
</tr>
<tr class="even">
<td><p>NS_4551-1</p></td>
<td><p>노르웨이어(IA5)</p></td>
</tr>
<tr class="odd">
<td><p>SEN_850200_B</p></td>
<td><p>스웨덴어(IA5)</p></td>
</tr>
<tr class="even">
<td><p>shift_jis</p></td>
<td><p>일본어(Shift-JIS)</p></td>
</tr>
<tr class="odd">
<td><p>utf-8</p></td>
<td><p>유니코드(UTF-8)</p></td>
</tr>
<tr class="even">
<td><p>windows-1250</p></td>
<td><p>중앙 유럽어(Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1251</p></td>
<td><p>키릴 자모(Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1252</p></td>
<td><p>서유럽어(Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1253</p></td>
<td><p>그리스어(Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1254</p></td>
<td><p>터키어(Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1255</p></td>
<td><p>히브리어(Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1256</p></td>
<td><p>아랍어(Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1257</p></td>
<td><p>발트어(Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1258</p></td>
<td><p>베트남어(Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-874</p></td>
<td><p>태국어(Windows)</p></td>
</tr>
</tbody>
</table>

