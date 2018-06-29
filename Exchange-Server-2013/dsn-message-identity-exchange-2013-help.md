---
title: 'DSN 메시지 id: Exchange 2013 Help'
TOCTitle: DSN 메시지 id
ms:assetid: 70ffba22-e4fd-4cd3-98f5-8bfca2df89e4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998835(v=EXCHG.150)
ms:contentKeyID: 50483412
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DSN 메시지 id

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

구문을 기반으로 하여 사용자 지정된 DSN(배달 상태 알림) 메시지를 식별할 수 있습니다. ID는 사용자 지정된 DSN 메시지의 GUID이거나 다음 값으로 구성된 문자열입니다.

  - **로캘**   이 변수는 DSN 메시지를 표시하는 언어 로캘을 지정합니다. **New-SystemMessage** 명령과 함께 사용할 수 있는 로캘 코드 목록에 대해서는 [시스템 메시지에 대 한 지원 되는 언어](supported-languages-for-system-messages-exchange-2013-help.md)을 참조하십시오.

  - **내부 또는 외부**   이 변수는 DSN 메시지를 내부 Microsoft Exchange Server 2013 조직의 일부인 보낸 사람에게만 보내거나 Exchange 조직 외부의 보낸 사람에게도 보낼지 여부를 지정합니다. 내부의 보낸 사람에게 보내는 DSN 메시지에 특정 전자 메일 연락처나 확인을 포함하지만 조직 외부의 보낸 사람에게 해당 정보가 노출되지 않도록 하려는 경우에는 내부 옵션을 사용할 수 있습니다.

  - **DSN 코드**   이 변수는 사용자 지정된 DSN 메시지의 DSN 코드를 지정합니다.

DSN 메시지 ID 구문은 `<Locale>\<Internal or External>\<DSN code>`입니다.

각 DSN 코드에 대해 내부의 보낸 사람이나 외부의 보낸 사람 및 서로 다른 로캘을 대상으로 할 수 있는 사용자 지정 DSN 메시지를 두 개 이상 만들 수 있습니다. 예를 들어 다음 표에서는 DSN 코드 5.1.2 및 해당 DSN 메시지 ID에 대해 일부 가능한 구성을 보여 줍니다.

### DSN 구성 및 ID 예

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>DSN 구성</th>
<th>DSN ID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>영어(en) 로캘을 사용하는 내부의 보낸 사람에게 DSN 메시지 표시</p></td>
<td><p>En\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>영어(en) 로캘을 사용하는 외부의 보낸 사람에게 DSN 메시지 표시</p></td>
<td><p>En\External\5.1.2</p></td>
</tr>
<tr class="odd">
<td><p>일본어(ja) 로캘을 사용하는 내부의 보낸 사람에게 DSN 메시지 표시</p></td>
<td><p>Ja\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>일본어(ja) 로캘을 사용하는 외부의 보낸 사람에게 DSN 메시지 표시</p></td>
<td><p>Ja\External\5.1.2</p></td>
</tr>
</tbody>
</table>

