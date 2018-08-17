---
title: '전화걸기 규칙을 사용 하 여 전화 대 한 권한 부여: Exchange 2013 Help'
TOCTitle: 전화걸기 규칙을 사용 하 여 전화 대 한 권한 부여
ms:assetid: 4c18bc07-f55c-42b7-81c1-729878aa93aa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ898499(v=EXCHG.150)
ms:contentKeyID: 51407693
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전화걸기 규칙을 사용 하 여 전화 대 한 권한 부여

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-03-09_

기본적으로 사용자는 발신 전화를 걸 수 없습니다. 사용자가 걸 수 있는 전화 유형을 지정하려면 먼저 전화 걸기 규칙을 만들고 UM 다이얼 플랜, UM 사서함 정책 또는 UM 자동 전화 교환에서 이 전화 걸기 규칙의 그룹에 권한을 부여합니다. 전화 걸기 규칙 그룹에 권한을 부여하려면 UM 다이얼 플랜에서 전화 걸기 규칙을 정의해야 합니다. 자세한 내용은 [사용자에 대 한 전화걸기 규칙 만들기](create-dialing-rules-for-users-exchange-2013-help.md)를 참조하십시오.

만든 각 전화 걸기 규칙에는 사용자에게 액세스 권한을 부여할 번호 패턴이나 전화 유형이 포함됩니다. 여러 유형의 사용자가 여러 유형의 전화를 걸도록 허용할 수 있습니다. 허용한 전화는 국내 전화이거나 국제 전화가 될 수 있습니다.

전화 걸기에 권한을 부여하거나 전화 걸기를 제한하려면 다음 설정을 제대로 구성해야 합니다.

  - **전화 걸기 규칙**   전화 걸기 규칙은 UM 사용 가능 사용자가 전화를 거는 번호, 통합 메시징에서 보내고 PBX(Private Branch eXchange) 또는 IP PBX에서 전화를 걸 번호를 정의합니다. 전화 걸기 규칙을 추가하여 전화 걸기 규칙 그룹을 만듭니다. 전화 걸기 규칙 그룹을 만들었으면 국내 또는 국제 전화 걸기 규칙 그룹에 대해 권한이 부여된 통화 목록에 이 그룹을 추가합니다.

  - **전화 걸기 규칙 그룹**   전화 걸기 규칙 그룹은 전화 걸기 그룹 내 사용자가 걸 수 있는 전화 유형을 결정합니다.

  - **전화 걸기 권한 부여**   전화 걸기 권한 부여는 사용자가 불필요한 전화 비용을 발생시키거나 시외 전화를 걸지 못하게 하기 위해 적용하는 제한을 결정하는 데 사용됩니다.

## 전화 걸기 규칙 그룹에 어떻게 권한을 부여합니까?

전화 걸기 규칙 그룹에 권한을 부여하는 위치에 따라 발신 전화를 허용할 발신자 유형이 결정됩니다. 예를 들어 Outlook Voice Access 사용자만 발신 전화를 걸 수 있도록 하려면 전화 걸기 규칙을 만든 다음 Outlook Voice Access 사용자가 연결된 UM 사서함 정책에 대한 전화 걸기 규칙 그룹에 권한을 부여합니다. 다음 표에는 다양한 발신자 유형에 대해 전화에 권한을 부여하는 방법이 나와 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>발신자 유형</th>
<th>전화 걸기 규칙 그룹에 권한을 부여하는 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook Voice Access 번호로 전화를 걸었지만 PIN을 입력하지 않은 인증되지 않은 발신자</p></td>
<td><p>UM 다이얼 플랜. 자세한 내용은 <a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">사용자에 대 한 호출 다이얼 플랜에 대 한 권한 부여</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>Outlook Voice Access 번호로 전화를 걸고 PIN을 입력한 인증된 발신자</p></td>
<td><p>발신자의 UM 사서함 정책. 자세한 내용은 <a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">사용자 그룹에 대 한 통화 권한 부여</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>UM 자동 전화 교환에서 구성된 전화 번호로 전화를 건 인증되지 않은 발신자</p></td>
<td><p>UM 자동 전화 교환. 자세한 내용은 <a href="authorize-calls-for-auto-attendant-callers-exchange-2013-help.md">자동 전화 교환 발신자에 대 한 통화 권한 부여</a>를 참조하십시오.</p></td>
</tr>
</tbody>
</table>


발신 전화에 권한을 부여할 사용자에 따라 다이얼 플랜, 자동 전화 교환 또는 UM 사서함 정책의 EAC(Exchange 관리 센터)에서 **전화 걸기 권한 부여** 페이지를 사용합니다.

