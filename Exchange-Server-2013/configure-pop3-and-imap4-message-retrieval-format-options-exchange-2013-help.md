---
title: 'POP3 및 IMAP4 메시지 검색 형식 옵션 구성: Exchange 2013 Help'
TOCTitle: POP3 및 IMAP4 메시지 검색 형식 옵션 구성
ms:assetid: 481096e0-4492-46c2-8ca8-bdf84a84531e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997869(v=EXCHG.150)
ms:contentKeyID: 50555983
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# POP3 및 IMAP4 메시지 검색 형식 옵션 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

POP3 및 IMAP4를 사용하여 전자 메일에 연결하는 사용자에 대한 메시지 검색 형식을 구성할 수 있습니다. 메시지 검색 옵션은 EAC 또는 셸을 사용하여 서버 수준에서 구성할 수 있으며 셸을 사용하여 사용자 수준에서 구성할 수 있습니다.

POP3 및 IMAP4에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "POP3 설정" 및 \&quot;IMAP4 설정\&quot; 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 서버 수준에서 POP3 메시지 검색 형식 설정

## EAC를 사용하여 서버 수준에서 POP3 메시지 검색 형식 설정

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  서버 목록에서 클라이언트 액세스 서버를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **POP3**를 클릭합니다.

4.  **메시지 MIME 형식**의 다음 설정 중에서 선택합니다.
    
      - 텍스트
    
      - HTML
    
      - HTML 및 대체 텍스트
    
      - Enriched 텍스트
    
      - Enriched 텍스트 및 대체 텍스트
    
      - Best Body Format
    
      - TNEF

5.  **저장**을 클릭합니다.

POP3에 대해 메시지 검색 형식을 설정한 후에는 POP3 서비스를 다시 시작해야 설정이 적용됩니다. POP3 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md)를 참조하십시오.

## 셸을 사용하여 서버 수준에서 POP3 메시지 검색 형식 설정

이 예에서는 CAS01 서버의 모든 POP3 사용자에 대한 메시지 검색 형식 옵션을 텍스트로만 설정합니다.

    Set-PopSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

다음 설정 중에서 선택할 수 있습니다. 숫자 값 또는 텍스트 문자열을 사용하여 *MessageRetrievalMimeFormat* 매개 변수의 값을 지정할 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>메시지 형식</strong></p></td>
<td><p><strong>값</strong></p></td>
</tr>
<tr class="even">
<td><p>텍스트</p></td>
<td><p><code>0</code> 또는 <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 또는 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 및 대체 텍스트</p></td>
<td><p><code>2</code> 또는 <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched 텍스트</p></td>
<td><p><code>3</code> 또는 <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched 텍스트 및 대체 텍스트</p></td>
<td><p><code>4</code> 또는 <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best Body Format</p></td>
<td><p><code>5</code> 또는 <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 또는 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


POP3에 대해 메시지 검색 형식을 설정한 후에는 POP3 서비스를 다시 시작해야 설정이 적용됩니다. POP3 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md)를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-PopSettings](https://technet.microsoft.com/ko-kr/library/aa997154\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

서버에서 POP3 메시지 검색 설정이 성공적으로 설정되었는지 확인하려면 다음을 수행하십시오.

1.  셸에서 다음 명령을 실행합니다.
    
        Get-PopSettings | format-list

2.  *MessageRetrievalMimeFormat* 설정이 올바른지 확인합니다.

## 서버 수준에서 IMAP4 메시지 검색 형식 설정

## EAC를 사용하여 서버 수준에서 IMAP4 메시지 검색 형식 설정

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  서버 목록에서 클라이언트 액세스 서버를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **IMAP4**를 클릭합니다.

4.  **메시지 MIME 형식**의 다음 설정 중에서 선택합니다.
    
      - 텍스트
    
      - HTML
    
      - HTML 및 대체 텍스트
    
      - Enriched 텍스트
    
      - Enriched 텍스트 및 대체 텍스트
    
      - Best Body Format
    
      - TNEF

5.  **저장**을 클릭합니다.

IMAP4에 대해 메시지 검색 형식을 설정한 후에는 IMAP4 서비스를 다시 시작해야 설정이 적용됩니다. IMAP4 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 IMAP4 서비스를 중지 합니다.](start-and-stop-the-imap4-services-exchange-2013-help.md)를 참조하십시오.

## 셸을 사용하여 서버 수준에서 IMAP4 메시지 검색 형식 설정

이 예에서는 CAS01 서버의 모든 IMAP4 사용자에 대한 메시지 검색 형식 옵션을 텍스트로만 설정합니다.

    Set-ImapSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

다음 설정 중에서 선택할 수 있습니다. 숫자 값 또는 텍스트 문자열을 사용하여 *MessageRetrievalMimeFormat* 매개 변수의 값을 지정할 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>메시지 형식</strong></p></td>
<td><p><strong>값</strong></p></td>
</tr>
<tr class="even">
<td><p>텍스트</p></td>
<td><p><code>0</code> 또는 <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 또는 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 및 대체 텍스트</p></td>
<td><p><code>2</code> 또는 <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched 텍스트</p></td>
<td><p><code>3</code> 또는 <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched 텍스트 및 대체 텍스트</p></td>
<td><p><code>4</code> 또는 <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best Body Format</p></td>
<td><p><code>5</code> 또는 <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 또는 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


IMAP4에 대해 메시지 검색 형식을 설정한 후에는 IMAP4 서비스를 다시 시작해야 설정이 적용됩니다. IMAP4 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 IMAP4 서비스를 중지 합니다.](start-and-stop-the-imap4-services-exchange-2013-help.md)를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-ImapSettings](https://technet.microsoft.com/ko-kr/library/aa998252\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

서버에서 IMAP4 메시지 검색 설정이 성공적으로 설정되었는지 확인하려면 다음을 수행하십시오.

1.  셸에서 다음 명령을 실행합니다.
    
        Get-ImapSettings | format-list

2.  *MessageRetrievalMimeFormat* 설정이 올바른지 확인합니다.

## 사용자에 대한 POP3 메시지 검색 형식 설정

## 셸을 사용하여 사용자에 대한 POP3 메시지 검색 형식 설정

이 예에서는 `USER01`의 POP3 액세스에 대한 메시지 검색 형식을 텍스트로만 설정합니다.

    Set-CASMailbox -Identity USER01 -PopMessagesRetrievalMimeFormat TextOnly

다음 설정 중에서 선택할 수 있습니다. 숫자 값 또는 텍스트 문자열을 사용하여 *PopMessagesRetrievalMimeFormat* 매개 변수의 값을 지정할 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>메시지 형식</strong></p></td>
<td><p><strong>값</strong></p></td>
</tr>
<tr class="even">
<td><p>텍스트</p></td>
<td><p><code>0</code> 또는 <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 또는 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 및 대체 텍스트</p></td>
<td><p><code>2</code> 또는 <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched 텍스트</p></td>
<td><p><code>3</code> 또는 <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched 텍스트 및 대체 텍스트</p></td>
<td><p><code>4</code> 또는 <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best Body Format</p></td>
<td><p><code>5</code> 또는 <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 또는 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


POP3에 대해 메시지 검색 형식을 설정한 후에는 POP3 서비스를 다시 시작해야 설정이 적용됩니다. POP3 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md)를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb125264\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사용자에 대한 POP3 메시지 검색 형식 옵션이 성공적으로 설정되었는지 확인하려면 다음을 수행하십시오.

1.  셸에서 다음 명령을 실행합니다.
    
        Get-CAS Mailbox <identity> | format-list

2.  *PopMessagesRetrievalMimeFormat*의 값이 올바른지 확인합니다.

## 사용자에 대한 IMAP4 메시지 검색 형식 설정

## 셸을 사용하여 사용자에 대한 IMAP4 메시지 검색 형식 설정

이 예에서는 `USER01`의 IMAP4 액세스에 대한 메시지 검색 형식을 텍스트로만 설정합니다.

    Set-CASMailbox -Identity USER01 -ImapMessagesRetrievalMimeFormat TextOnly

숫자 값 또는 텍스트 문자열을 사용하여 *ImapMessagesRetrievalMimeFormat* 매개 변수의 값을 지정할 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>메시지 형식</strong></p></td>
<td><p><strong>값</strong></p></td>
</tr>
<tr class="even">
<td><p>텍스트</p></td>
<td><p><code>0</code> 또는 <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 또는 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 및 대체 텍스트</p></td>
<td><p><code>2</code> 또는 <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched 텍스트</p></td>
<td><p><code>3</code> 또는 <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched 텍스트 및 대체 텍스트</p></td>
<td><p><code>4</code> 또는 <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best Body Format</p></td>
<td><p><code>5</code> 또는 <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 또는 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


IMAP4에 대해 메시지 검색 형식을 설정한 후에는 IMAP4 서비스를 다시 시작해야 설정이 적용됩니다. IMAP4 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 IMAP4 서비스를 중지 합니다.](start-and-stop-the-imap4-services-exchange-2013-help.md)를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb125264\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사용자에 대한 IMAP4 메시지 검색 형식 옵션이 성공적으로 설정되었는지 확인하려면 다음을 수행하십시오.

1.  셸에서 다음 명령을 실행합니다.
    
        Get-CAS Mailbox <identity> | format-list

2.  *ImapMessagesRetrievalMimeFormat*의 값이 올바른지 확인합니다.

## 자세한 내용

IMAP4 및 POP3 사용자에 대한 메시지 검색 형식을 설정한 후 다음 작업을 수행할 수도 있습니다.

[사용 하도록 설정 하거나 사용자에 대 한 POP3 액세스를 사용 하지 않도록 설정](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[사용 하도록 설정 하거나 사용자에 대 한 IMAP4 액세스를 사용 하지 않도록 설정](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

[IMAP4에 대 한 일정 옵션 구성](configure-calendar-options-for-imap4-exchange-2013-help.md)

[P o p 3에 대 한 일정 옵션 구성](configure-calendar-options-for-pop3-exchange-2013-help.md)

