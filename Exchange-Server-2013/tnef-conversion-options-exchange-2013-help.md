---
title: 'TNEF 변환 옵션: Exchange 2013 Help'
TOCTitle: TNEF 변환 옵션
ms:assetid: 989a62fc-4bc1-448f-90c8-7c7b56fe1084
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb310786(v=EXCHG.150)
ms:contentKeyID: 52057945
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# TNEF 변환 옵션

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

전송 형식 TNEF (Neutral Encapsulation)을 유지 하거나 Exchange 조직 하는 메시지에서 제거를 지정할 수 있습니다. TNEF, Outlook 서식 있는 텍스트 또는 Exchange 서식 있는 텍스트 형식으로 라고도 Microsoft-MAPI 메시지 속성을 캡슐화 하는 것에 대 한 특정 형식입니다. 모든 버전의 MicrosoftOutlook TNEF를 완벽 하 게 이해합니다. Outlook Web App MAPI에 TNEF를 변환 하 고 서식이 지정 된 메시지를 표시 하는 합니다. 그러나 모르고 TNEF TNEF를 일반적으로 표시 하는 다른 전자 메일 클라이언트도 서식이 지정 된 메시지 Win.dat 또는 Winmail.dat 첨부 파일이 있는 일반 텍스트 메시지입니다.

**목차**

원격 도메인에 대 한 TNEF 변환 옵션

메일 사용자 및 메일 연락처에 대 한 TNEF 변환 옵션

Outlook에서 TNEF 변환 옵션

TNEF 변환 옵션의 우선순위

## 원격 도메인에 대 한 TNEF 변환 옵션

원격 도메인에 대 한 TNEF 변환 옵션을 구성 하는 경우 해당 TNEF 변환 옵션이 해당 도메인에 보내는 모든 메시지에 적용 됩니다.

  - Exchange 관리 센터 (EAC) 옵션을 설정 하려면 TNEF 변환 원격 도메인에 대 한 **메일 흐름** 에 사용 하면 Exchange Online 전용에 대 한 \> **원격 도메인** \> (![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")) **편집** \> **Exchange를 사용 하 여 서식 있는 텍스트 형식** 입니다.

  - Exchange Online 및 Exchange 2013 에 대 한 원격 도메인에 대 한 TNEF 변환 옵션을 설정 하려면 **Set-RemoteDomain** cmdlet에서 *TnefEnabled* 매개 변수를 사용 합니다.

조직에서 원격 도메인에 대 한 TNEF 변환에 대 한 다음과 같은 구성 옵션 해야 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>설정</th>
<th>EAC에서</th>
<th>셸에서</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>원격 도메인에 보내는 모든 메시지에 TNEF를 사용 합니다.</p></td>
<td><p><strong>Always</strong></p></td>
<td><p><code>$true</code></p></td>
</tr>
<tr class="even">
<td><p>원격 도메인에 보내는 메시지에 대 한 TNEF를 사용 하지 마십시오.</p></td>
<td><p><strong>Never</strong></p></td>
<td><p><code>$false</code></p></td>
</tr>
<tr class="odd">
<td><p>TNEF 메시지 구체적으로 허용 되지 않거나 원격 도메인의 받는 사람에 대 한 금지 합니다. TNEF 메시지는 원격 도메인의 받는 사람에 게 보낼지 여부는 메일 연락처 또는 메일 사용자의 특정 설정과 또는 Outlook에서 보낸 사람이 지정한 설정에 따라 달라 집니다. 값은 기본값입니다.</p></td>
<td><p><strong>기능 \ 사용자 설정에 따라</strong></p></td>
<td><p><code>$null</code> (빈)</p></td>
</tr>
</tbody>
</table>


원격 도메인에 대 한 자세한 내용은 [원격 도메인](remote-domains-exchange-2013-help.md) 또는 [Exchange Online의 원격 도메인](https://technet.microsoft.com/ko-kr/library/jj966211\(v=exchg.150\))를 참조 하십시오.

맨 위로 이동

## 메일 사용자 및 메일 연락처에 대 한 TNEF 변환 옵션

메일 연락처 또는 메일 사용자에 대 한 TNEF 변환 옵션을 구성할 때 해당 TNEF 변환 옵션이 있는 특정 받는 사람에 게 보낸 모든 메시지에 적용 됩니다. **Set-MailUser** 및 **Set-MailContact** cmdlet에서 *UseMapiRichTextFormat* 매개 변수를 사용 하 여 메일 사용자 및 메일 연락처에 대 한 TNEF 변환 옵션을 구성 합니다.

메일 사용자 및 조직에서 메일 연락처에 대 한 TNEF 변환에 대 한 다음과 같은 구성 옵션 해야 합니다.

  - **항상**   TNEF 받는 사람에 게 보낸 모든 메시지에 사용 됩니다. *UseMapiRichTextFormat* 매개 변수에 대 한 해당 값은 `Always`입니다.

  - **안함**   받는 사람에 게 보내는 메시지에 TNEF 사용 되지 않습니다. *UseMapiRichTextFormat* 매개 변수에 대 한 해당 값은 `Never`입니다.

  - **기본 설정 사용**   TNEF 메시지 구체적으로 허용 되지 않거나 메일 사용자 또는 메일 연락처에 대 한 금지 합니다. TNEF 메시지 받는 사람에 게 보낼지 여부를 해당 원격 도메인에 대 한 특정 설정이 나 Outlook에서 보낸 사람이 지정 된 설정에 따라 달라 집니다. *UseMapiRichTextFormat* 매개 변수에 대 한 해당 값은 `UseDefaultSettings`입니다. 이것이 기본 설정입니다.

맨 위로 이동

## Outlook에서 TNEF 변환 옵션

보낸 사람이 Exchange 조직 외부의 모든 받는 사람에 게 전송 된 TNEF 메시지에 대 한 기본 TNEF 메시지 변환 옵션을 제어할 수 있습니다. 이러한 옵션을 *인터넷 메시지 형식* 옵션 이라고 합니다. 옵션 원격 받는 사람에 게 하 고 Exchange 조직에 받는 사람에 게 하지에 적용 됩니다.


> [!NOTE]
> 다음 옵션을 외부 받는 사람에 게 보낼 때 Outlook 서식 있는 텍스트를 포함 하는 메시지 처리 되는 방식을 정의 합니다. 사용 중인 메시지 형식이 HTML 또는 일반 텍스트, 이러한 설정은 적용 되지 않습니다.



Outlook에서 다음과 같은 TNEF 변환 옵션을 사용할 수 있습니다.

  - **HTML 형식으로 변환**   이것이 기본 옵션입니다. 원격 받는 사람에 게 전송 된 모든 TNEF 메시지를 HTML로 변환 됩니다. 메시지의 서식을 원본 메시지 밀접 하 게 비슷해야 합니다. MIME 인코딩 HTML 메시지는 많은, 모두는 아니지만, 전자 메일 클라이언트에서 지원 됩니다.

  - **일반 텍스트 형식으로 변환**   원격 받는 사람에 게 전송 된 모든 TNEF 메시지는 일반 텍스트로 변환 됩니다. 메시지에서 모든 서식이 손실 됩니다.

  - **Outlook 서식 있는 텍스트를 사용 하 여 보내기**   원격 받는 사람에 게 전송 된 모든 TNEF 메시지에 TNEF 메시지 상태로 유지 됩니다.

Outlook의 다음 위치에서 이러한 옵션을 구성할 수 있습니다.

  - **Outlook 2010 또는 Outlook 2013** **파일** \> **옵션** \> **메일** \> **메시지 형식** 입니다.   

  - **Outlook 2007** **도구** \> **옵션** \> **메일 형식** \> **인터넷 메일 형식** 입니다.   

보낸 사람이 Exchange 조직 외부의 특정 받는 사람에 게 전송 된 TNEF 메시지에 대 한 기본 TNEF 메시지 변환 옵션과 제어할 수도 있습니다. 이러한 옵션을 *인터넷 받는 사람 메시지 형식* 옵션 이라고 합니다. 옵션 대화 연락처 폴더에 저장 된 원격 받는 사람에 게 하 고 Exchange 조직에 받는 사람에 게 하지에 적용 됩니다. 연락처 폴더에 원격 받는 사람에 게 다음 TNEF 변환 옵션을 있습니다.

  - **Outlook에서 최적의 보내기 형식**   이것이 기본 설정입니다. 이 설정을 사용 하면 Outlook 기본 인터넷 메일 형식으로 지정 된 TNEF 변환 옵션을 사용 합니다. 사용 가능한 값은 **HTML 형식으로 변환**, **일반 텍스트 형식으로 변환**, 또는 **Outlook 서식 있는 텍스트를 사용 하 여 보낼** 입니다. 따라서 TNEF 메시지 수 수 TNEF 소위, HTML로 변환 또는 일반 텍스트로 변환 합니다. TNEF 메시지가 받는이 사람에 대해 TNEF를 유지 하는지 확인 하려면 **Outlook 서식 있는 텍스트 형식을 사용 하 여** 보낼 **수 있도록 Outlook에서 최적의 보내기 형식에서** 이 설정을 변경 해야 합니다.

  - **보내기 일반 텍스트만**   받는 사람에 게 전송 된 모든 TNEF 메시지는 일반 텍스트로 변환 됩니다. 메시지에서 모든 서식이 손실 됩니다.

  - **Outlook 서식 있는 텍스트 형식으로 보내기**   원격 받는 사람에 게 전송 된 모든 TNEF 메시지에 TNEF 메시지 상태로 유지 됩니다.

Outlook의 다음 위치에서 대화 상대에 대 한 이러한 옵션을 구성할 수 있습니다.

  - **Outlook 2010 또는 Outlook 2013**   버디 카드를 엽니다, 그리고 전자 메일 주소를 두번클릭 하, **이 사용자와 상호작용 하기 위한 자세한 옵션 보기** 아이콘을 클릭 하 고 **Outlook 속성** 을 선택 합니다. **전자 메일 속성** 대화 상자에서 **인터넷** 형식을 선택 합니다.

  - **Outlook 2007**   버디 카드를 열고 **전자 메일** 필드를 두번클릭 **인터넷 형식** 을 선택 합니다.

맨 위로 이동

## TNEF 변환 옵션의 우선순위

Exchange를 사용 하 여 우선순위에 따라 다음 목록에서 설명한 대로 Exchange 조직 외부의 받는 사람에 게 보내는 메시지에 대 한 TNEF 변환 옵션을 결정 합니다.

1.  원격 도메인 설정

2.  메일 사용자 또는 메일 연락처 설정

3.  Outlook 설정

목록에 가장 낮은에서 가장 높은 우선순위 순서를 지정합니다. Outlook 또는 메일 사용자, 메일 연락처에 TNEF 설정을 재정의 하는 원격 도메인에 TNEF 설정 합니다. 등 outlook에서 서식 있는 텍스트 메시지를 보내면 하지만 받는 사람이 없는 원격 도메인 설정 구체적으로 허용 하지 않고 TNEF 형식의 메시지를 도메인에 있는 경우를 가정해 보겠습니다. 받는 사람이 받은 메시지는 일반 텍스트 또는 HTML, 하지만 하지 TNEF 됩니다.

또한이 Exchange 요약 Transport Neutral 인코딩 형식 (STNEF) 메시지를 하지 외부 받는 사람에 게 보냅니다. TNEF 메시지에만 Exchange 조직 외부의 받는 사람에 게 보낼 수 있습니다.

맨 위로 이동

