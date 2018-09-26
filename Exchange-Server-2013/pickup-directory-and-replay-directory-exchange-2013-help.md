---
title: 'Pickup 디렉터리 및 Replay 디렉터리: Exchange 2013 Help'
TOCTitle: Pickup 디렉터리 및 Replay 디렉터리
ms:assetid: ae191700-953f-411c-906f-dc90feec3d5a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124230(v=EXCHG.150)
ms:contentKeyID: 50483925
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pickup 디렉터리 및 Replay 디렉터리 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

기본적으로 Pickup 및 Replay 디렉터리는 모든 Microsoft Exchange Server 2013 사서함 서버 또는 Edge 전송 서버에 있습니다. Pickup 또는 Replay 디렉터리에 복사된 올바른 형식의 전자 메일 메시지 파일이 배달을 위해 제출됩니다. Pickup 디렉터리는 관리자가 메일 흐름을 테스트하는 데 사용하거나, 자체 메시지를 만들고 전송해야 하는 응용 프로그램에서 사용됩니다. Replay 디렉터리는 외부 게이트웨이 서버에서 메시지를 수신하며 관리자가 Exchange 서버 큐에서 내보내는 메시지를 재전송하는 데에도 사용할 수 있습니다.

**목차**

Anatomy of an email message file

How the Pickup and Replay directories process messages

Pickup directory message file requirements

Pickup directory message header modifications

Replay directory message file requirements

Replay directory message header modifications

Failures in Pickup and Replay directory message processing

Security considerations for the Pickup and Replay directories

Permissions for the Pickup and Replay directories

## 전자 메일 메시지 파일 분석

표준 SMTP 전자 메일 메시지는 *메시지 봉투*와 메시지 콘텐츠로 구성됩니다. 메시지 봉투에는 메시지를 전송 및 배달하는 데 필요한 정보가 있습니다. 메시지 콘텐츠에는 메시지 헤더 필드(통칭 *메시지 헤더*) 및 메시지 본문이 들어 있습니다. 메시지 봉투는 RFC 2821에 설명되어 있고 메시지 헤더는 RFC 2822에 설명되어 있습니다.

보낸 사람이 전자 메일 메시지를 작성하여 배달하도록 전송하는 경우 메시지에는 보낸 사람, 받는 사람, 메시지가 작성된 날짜 및 시간, 제목 줄(옵션) 및 메시지 본문(옵션) 등 SMTP 표준을 준수하는 데 필요한 기본 정보가 포함됩니다. 이러한 정보는 메시지 자체에 포함되어 있으며 정의에 따라 메시지 헤더에 포함되어 있습니다.

보낸 사람의 메시징 서버에서 메시지 헤더에 있는 보낸 사람 및 받는 사람 정보를 사용하여 해당 메시지에 대한 메시지 봉투를 생성하고 받는 사람의 메시징 서버로 배달하기 위해 인터넷으로 메시지를 전송합니다. 메시지 봉투는 메시지 전송 프로세스에 의해 생성되며 실제로는 메시지의 일부가 아니기 때문에 받는 사람은 메시지 봉투를 볼 수 없습니다.

메시지 전송에 관여하는 각 서버가 메시지를 배달하는 서버 역할과 관련된 메시지 헤더 필드나 다른 응용 프로그램 관련 메시지 헤더 필드를 메시지 헤더에 삽입할 수도 있습니다. 받는 사람이 전자 메일 클라이언트를 사용하여 메시지를 열면 전자 메일 클라이언트는 메시지 헤더에서 보낸 사람, 받는 사람 및 제목 등 메시지와 연관성이 높은 일부 정보를 메시지 본문과 함께 표시합니다.

맨 위로 이동

## Pickup 및 Replay 디렉터리에서 메시지를 처리하는 방법

Exchange 2013에서 Pickup 디렉터리의 기본 위치는 `%ExchangeInstallPath%TransportRoles\Pickup`입니다. Replay 디렉터리의 기본 위치는 `%ExchangeInstallPath%TransportRoles\Replay`입니다. Pickup 또는 Replay 디렉터리로 복사된 올바른 형식의 .eml 메시지 파일을 전송하기 위한 처리 단계는 다음과 같습니다.

1.  5초마다 Pickup 및 Replay 디렉터리에 새로운 메시지 파일이 있는지 확인합니다. 이 폴링 간격은 수정할 수 없습니다. **Set-TransportService** cmdlet에 *PickupDirectoryMaxMessagesPerMinute* 매개 변수를 사용하여 메시지 파일 처리 속도를 조정할 수 있습니다. 이 매개 변수는 Pickup 디렉터리 및 Replay 디렉터리에 영향을 줍니다. 기본값은 분당 100개의 메시지입니다. 열 수 없는 파일은 Pickup 디렉터리에 남아 있으며 다음 폴링에서 다시 평가됩니다.

2.  헤더 최대 크기와 최대 받는 사람 수 등 Pickup 디렉터리의 메시지 파일에 대한 제한을 확인합니다. 기본적으로 헤더 최대 크기는 64KB이며 최대 받는 사람 수는 100명입니다. 이러한 제한을 변경하려면 **Set-TransportService** cmdlet을 사용합니다. 이러한 설정은 Pickup 디렉터리에만 적용됩니다.

3.  파일 이름이 *\<파일 이름\>*.eml에서 *\<파일 이름\>*.tmp로 바뀝니다. *\<파일 이름\>*.tmp 파일이 이미 있는 경우 파일 이름이 *\<파일 이름\>\<날짜/시간\>*.tmp로 바뀝니다. 파일 이름 바꾸기에 실패하면 이벤트 로그 오류가 생성되며 Pickup 프로세스는 다음 파일로 진행됩니다.

4.  .tmp 파일이 전자 메일 메시지로 변환된 후 **delete on close** 명령이 .tmp 파일에 전달됩니다. .tmp 파일이 Pickup 디렉터리에 남아 있는 것처럼 보이지만 해당 파일은 열 수 없습니다.

5.  배달할 메시지를 큐에 넣은 후 **close** 명령을 실행하여 .tmp 파일을 Pickup 디렉터리에서 삭제합니다. 삭제에 실패하면 이벤트 로그 오류가 생성됩니다. Pickup 디렉터리에 .tmp 파일이 있을 때 Microsoft Exchange Transport Service를 다시 시작하면 모든 .tmp 파일의 이름이 .eml 파일로 바뀌고 다시 처리됩니다. 이는 중복 메시지 전송을 유발할 수 있습니다.

맨 위로 이동

## Pickup 디렉터리의 메시지 파일 요구 사항

Pickup 디렉터리로 복사된 메시지 파일을 배달하기 위해 충족해야 하는 요구 사항은 다음과 같습니다.

  - 메시지 파일은 기본 SMTP 메시지 형식을 따르는 텍스트 파일이어야 합니다. MIME 메시지 헤더 파일 및 콘텐츠가 지원됩니다.

  - 메시지 파일의 파일 이름 확장명은 .eml이어야 합니다.

  - 메시지 헤더의 `Sender` 또는 `From` 메시지 헤더 필드에 전자 메일 주소가 한 개 이상 있어야 합니다. 동일한 전자 메일 주소가 `Sender` 및 `From` 필드 둘 다에 있으면 `From` 필드의 전자 메일 주소가 메시지 봉투에서 메시지를 보낸 사람으로 사용됩니다.

  - `Sender` 필드에는 전자 메일 주소가 하나만 있을 수 있으며, 여러 전자 메일 주소를 사용할 수 없습니다. `From` 필드에 전자 메일 주소가 하나만 있으면 `Sender` 필드는 옵션입니다.

  - `From` 필드에는 여러 전자 메일 주소를 사용할 수 있지만 `Sender` 필드에는 전자 메일 주소가 하나만 있어야 합니다. 그러면 `Sender` 필드의 주소가 메시지 봉투에서 메시지를 보낸 사람으로 사용됩니다.

  - 적어도 하나의 전자 메일 주소가 `To`, `Cc` 또는 `Bcc` 필드에 있어야 합니다.

  - 메시지 헤더와 메시지 본문 사이에는 빈 줄이 있어야 합니다.

이 예에서는 Pickup 디렉터리에 허용되는 형식을 사용하는 일반 문자 메시지를 보여줍니다.

  ```powershell  
    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    
    This is the body of the message.
  ```

MIME 콘텐츠도 Pickup 디렉터리 메시지 파일에서 지원됩니다. MIME는 7비트 ASCII 텍스트, HTML 및 기타 멀티미디어 콘텐츠로 나타낼 수 없는 언어를 포함하여 광범위한 메시지 콘텐츠를 정의합니다. MIME에 대한 자세한 정보와 해당 요구 사항은 이 항목에서 다루지 않습니다. 이 예에서는 Pickup 디렉터리에 허용되는 형식을 사용하는 간단한 MIME 메시지를 보여줍니다.

  ```powershell
    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>
  ```

맨 위로 이동

## Pickup 디렉터리의 메시지 헤더 수정

Pickup 디렉터리는 메시지 헤더에서 다음 메시지 헤더 필드를 모두 제거합니다.

  - `Received`

  - `Resent-*`

  - `Bcc`
    

    > [!NOTE]  
    > 메시지 헤더의 옵션인 <CODE>Bcc</CODE> 메시지 헤더 필드에 있는 모든 전자 메일 주소는 올바르게 처리됩니다. <CODE>Bcc</CODE> 받는 사람을 볼 수 없는 메시지 봉투 받는 사람으로 올린 후 메시지 헤더에서 제거하여 해당 받는 사람의 ID를 보호합니다. 메시지에 <CODE>Bcc</CODE> 받는 사람만 있는 경우 <STRONG>Undisclosed Recipients</STRONG>의 값이 메시지 헤더의 <CODE>To</CODE> 필드에 추가됩니다.



Pickup 디렉터리는 메시지 전송 프로세스의 일부로 자체 `Received` 헤더 필드를 메시지에 추가합니다. `Received` 헤더 필드는 다음과 같은 형식으로 적용됩니다.

  ```powershell
  Received: from localhost by Pickup with Microsoft SMTP Server id <ExchangeServerVersion><datetime>
  ```

Pickup 디렉터리는 다음 메시지 헤더 필드가 누락되거나 잘못된 경우 해당 필드를 수정합니다.

  - **Message-Id**   이 `Message-Id` 필드가 누락되거나 비어 있으면 Pickup 디렉터리는 *\<GUID\>*@*\<defaultdomain\>* 형식을 사용하여 Message-Id 필드를 추가합니다.

  - **Date**   `Date` 필드가 누락되거나 잘못된 경우 Pickup 디렉터리는 Pickup 디렉터리의 메시지 처리 날짜 및 시간을 추가합니다.

맨 위로 이동

## Replay 디렉터리의 메시지 파일 요구 사항

Replay 디렉터리는 내보낸 Exchange 메시지를 다시 전송하고 외부 게이트웨이 서버로부터 메시지를 받는 데 사용됩니다. 이러한 메시지는 이미 Replay 디렉터리에 맞게 형식이 지정되어 있습니다. 관리자 또는 응용 프로그램에서 Replay 디렉터리를 사용하여 새로운 메시지 파일을 작성하거나 전송할 필요가 거의 또는 전혀 없습니다. Pickup 디렉터리는 새로운 메시지 파일을 만들고 전송하는 데 사용합니다.

Replay 디렉터리 메시지는 *X-Header*를 포괄적으로 사용합니다. X-Header는 사용자가 정의하며 메시지 헤더에 있는 비공식적인 메시지 헤더 필드입니다. X-Header는 RFC 2822에 구체적으로 언급되어 있지 않지만 "X-"로 시작하는 정의되지 않은 메시지 헤더 필드를 사용하여 메시지에 비공식적인 메시지 헤더 필드를 추가하는 데 적합한 방법이 되었습니다. Replay 디렉터리의 메시지 파일에 사용되는 Exchange 관련 X-헤더는 일반적으로 메시지 봉투에 있는 배달 정보를 실제로 설정할 수 있습니다. 이 기능은 Replay 디렉터리를 사용하여 다른 Exchange 서버에서 내보낸 메시지를 처리하는 경우 원본 메시지 정보를 유지하는 데 필요합니다.

Replay 디렉터리로 복사된 메시지 파일을 배달하기 위해 충족해야 하는 요구 사항은 다음과 같습니다.

  - 메시지 파일은 기본 SMTP 메시지 형식을 따르는 텍스트 파일이어야 합니다. MIME 메시지 헤더 파일 및 콘텐츠가 지원됩니다.

  - 메시지 파일의 파일 이름 확장명은 .eml이어야 합니다.

  - X-Header는 모든 일반 헤더 필드 전에 발생해야 합니다.

  - 헤더 필드와 메시지 본문 사이에는 빈 줄이 있어야 합니다.

다음 목록에 설명되어 있는 X-Header는 Replay 디렉터리의 메시지에 필요합니다.

  - **X-Sender**   이 X-헤더는 일반적인 SMTP 메시지의 `From` 메시지 헤더 필드 요구 사항을 대체합니다. 하나의 전자 메일 주소가 포함된 `X-Sender` 필드 한 개가 있어야 합니다. 받는 사람의 전자 메일 클라이언트가 `From` 메시지 헤더 필드의 값을 메시지의 보낸 사람으로 표시하지만 Replay 디렉터리는 `From` 메시지 헤더 필드가 있는 경우 이를 무시합니다. 다른 매개 변수는 일반적으로 다음 예에 표시된 것처럼 `X-Sender` 필드에 있습니다.
    
    ```powershell
    X-Sender: <bob@fabrikam.com> BODY=7bit RET=HDRS ENVID=12345ABCD auth=<someAuth>
    ```    

    > [!NOTE]
    > 이러한 매개 변수는 보내는 서버에서 일반적으로 생성되는 메시지 봉투 값입니다. 내보낸 메시지 파일에서 이와 유사한 매개 변수를 볼 수 있습니다.<BR><CODE>RET</CODE>는 메시지를 배달할 수 없는 경우 보낸 사람에게 전체 메시지를 반환할지, 헤더만 반환할지 지정합니다. <CODE>RET</CODE>는 <CODE>HDRS</CODE> 또는 <CODE>FULL</CODE>을 값으로 가질 수 있습니다. <CODE>ENVID</CODE>는 메시지 봉투 식별자입니다. <CODE>BODY</CODE>는 메시지의 텍스트 인코딩을 지정합니다. <CODE>auth</CODE>는 RFC 2554에 설명된 대로 메시징 서버에 대한 인증 메커니즘을 지정합니다.


  - **X-Receiver**   이 X-헤더는 일반적인 SMTP 메시지의 `To` 메시지 헤더 필드 요구 사항을 대체합니다. 하나의 전자 메일 주소가 포함된 `X-Receiver` 필드가 적어도 한 개는 있어야 합니다. 여러 `X-Receiver` 필드가 여러 받는 사람에 대해 허용됩니다. 받는 사람의 전자 메일 클라이언트가 `To` 메시지 헤더 필드의 값을 메시지의 받는 사람으로 표시하지만 Replay 디렉터리는 `To` 메시지 헤더 필드가 있는 경우 이를 무시합니다. 다음 예와 같이 `X-Receiver` 필드에 다른 옵션 매개 변수가 있을 수 있습니다.
    
    ```powershell
    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    ```
    

    > [!NOTE]   
    > 이러한 매개 변수는 보내는 서버에서 일반적으로 생성되는 메시지 봉투 값입니다. 내보낸 메시지 파일에서 이와 유사한 매개 변수를 볼 수 있습니다. 이러한 매개 변수는 RFC 1891에 설명된 것처럼 DSN(배달 상태 알림) 메시지와 관련되어 있습니다.<BR><CODE>NOTIFY</CODE>는 <CODE>NEVER</CODE>, <CODE>DELAY</CODE> 또는 <CODE>FAILURE</CODE>를 값으로 가질 수 있습니다. <CODE>ORcpt</CODE>는 메시지의 원래 받는 사람을 보존합니다.


다음 목록에 설명되어 있는 X-Header는 Replay 디렉터리의 메시지 파일에 대한 선택 사항입니다.

  - **X-CreatedBy**   헤더 방화벽 기능에 사용합니다. 이 X-Header가 있는 경우 비워두면 안 됩니다. `X-CreatedBy` 필드가 없으면 **Unspecified**의 값과 함께 추가됩니다. 일반적으로 이 필드의 값은 **MSExchange15**이지만 송신 커넥터에 설정된 비 SMTP 주소 공간 유형을 포함할 수도 있습니다(예: **Notes**).

  - **X-EndOfInjectedXHeaders**   모든 X-Header의 크기(바이트)입니다. 이 X-Header는 일반 메시지 헤더 필드가 시작되기 전에 마지막 X-Header를 나타내는 표시로 사용될 수도 있습니다.

  - **X-ExtendedMessageProps**   메시지의 확장 메시지 속성입니다.

  - **X-HeloDomain**   초기 SMTP 프로토콜 대화 중에 나타나는 HELO/EHLO 도메인 문자열입니다.

  - **X-Source**   큐 뷰어에서 **MessageSourceName** 열 아래에 사용됩니다. 이 X-헤더의 값이 지정되지 않은 경우 **Replay**의 값이 사용됩니다. 이 X-헤더에 대한 다른 가능한 값은 **Smtp Receive Connector** 및 **Smtp Send Connector**입니다.

  - **X-SourceIPAddress**  보내는 서버의 IP 주소입니다. IP 주소가 지정되지 않은 경우 이 필드는 `0.0.0.0`입니다.

이 예에서는 Replay 디렉터리에 허용되는 형식을 사용하는 일반 문자 메시지를 보여줍니다.

```powershell
X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345AB auth=<someAuth>
Subject: Optional message subject
    
This is the body of the message.
```
MIME 콘텐츠도 Replay 디렉터리 메시지 파일에서 지원됩니다. MIME는 7비트 ASCII 텍스트, HTML 및 기타 멀티미디어 콘텐츠로 나타낼 수 없는 언어를 포함하여 광범위한 메시지 콘텐츠를 정의합니다. MIME에 대한 자세한 정보와 해당 요구 사항은 이 항목에서 다루지 않습니다. 이 예에서는 Replay 디렉터리에 허용되는 형식을 사용하는 간단한 MIME 메시지를 보여줍니다.

```powershell
X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345ABCD auth=<someAuth>
To: mary@contoso.com
From: bob@fabrikam.com
Subject: Optional message subject
MIME-Version: 1.0
Content-Type: text/html; charset="iso-8859-1"
Content-Transfer-Encoding: 7bit
<HTML><BODY>
<TABLE>
<TR><TD>cell 1</TD><TD>cell 2</TD></TR>
<TR><TD>cell 3</TD><TD>cell 4</TD></TR>
</TABLE>

</BODY></HTML>
```

맨 위로 이동

## Replay 디렉터리의 메시지 헤더 수정

Replay 디렉터리는 메시지 파일에서 `Bcc` 메시지 헤더 필드를 삭제합니다.

Replay 디렉터리는 메시지 전송 프로세스의 일부로 자체 `Received` 메시지 헤더 필드를 메시지에 추가합니다. Received 메시지 헤더 필드는 다음과 같은 형식으로 적용됩니다.

  ```powershell
  Received: from <ReceivingServerName> by Replay with <ExchangeServerVersion><DateTime>
  ```
Replay 디렉터리는 메시지 헤더에서 다음 메시지 헤더 필드를 수정합니다.

  - **Message-Id**   이 메시지 헤더 필드가 누락되거나 비어 있으면 Replay 디렉터리는 *\<GUID\>*@*\<기본 도메인\>* 형식을 사용하여 Message-ID 메시지 헤더 필드를 추가합니다.

  - **Date**   이 메시지 헤더 필드가 누락되거나 해당 형식이 잘못된 경우 Replay 디렉터리는 Replay 디렉터리의 메시지 처리 날짜 및 시간을 사용하여 Date 메시지 헤더 필드를 추가합니다.

맨 위로 이동

## Pickup 및 Replay 디렉터리의 메시지 처리 실패

Pickup 또는 Replay 디렉터리로 복사된 메시지 파일이 배달을 위해 대기하지 못할 수도 있습니다. 발생할 수 있는 메시지 전송 오류 범주는 다음과 같습니다.

  - **배달 실패**   배달을 위해 성공적으로 전송하지 못한, 보낸 사람이 유효한 올바른 형식의 메시지 파일은 배달 못 함 보고서(NDR)를 생성합니다. 잘못된 콘텐츠 또는 Pickup 디렉터리 메시지 제한 위반에 의해서도 NDR이 생성될 수 있습니다. 메시지 처리 중에 NDR이 생성되는 경우 원본 메시지 파일이 NDR 메시지에 첨부되고 Pickup 디렉터리 또는 Replay 디렉터리에서 메시지 파일이 삭제됩니다.
    

    > [!NOTE]
    > 전송 파이프라인에 전송된 올바른 형식의 메시지가 나중에 배달 실패로 NDR과 함께 보낸 사람에게 반환될 수 있습니다. 이러한 유형의 실패는 Pickup 또는 Replay 디렉터리와 관련 없는 메시지 배달 경로에 따른 메시징 서버 오류나 라우팅 실패 등의 전송 문제로 인해 발생할 수 있습니다.



  - **Badmail**   *badmail*로 분류된 메시지는 Pickup 또는 Replay 디렉터리에서 배달을 위해 메시지를 전송하지 못하게 하는 문제를 가지고 있습니다. Badmail을 발생시키는 다른 조건은 메시지의 형식은 올바르지만 받는 사람이 유효하지 않은 경우로, 보내는 사람이 유효하지 않으므로 보내는 사람에게 NDR 메시지를 보낼 수 없습니다.
    
    Badmail로 확인된 메시지 파일은 Pickup 또는 Replay 디렉터리에 남아 있으며 *\<파일 이름\>*.eml에서 *\<파일 이름\>*.bad로 이름이 바뀝니다. *\<파일 이름\>*.bad 파일이 이미 있는 경우 해당 파일의 이름이 *\<파일 이름\>\<날짜/시간\>*.bad로 바뀝니다. Pickup 또는 Replay 디렉터리에 Badmail이 있는 경우 이벤트 로그 오류가 생성되지만 동일한 Badmail 메시지가 반복적인 이벤트 로그 오류를 생성하지는 않습니다.
    

    > [!NOTE]
    > 배달을 위해 메시지 파일을 Pickup 디렉터리에 복사하기 전에 항상 다른 위치에서 메시지 파일을 작성하고 저장하십시오. Pickup 디렉터리는 5초마다 새 메시지를 폴링합니다. 따라서 Pickup 디렉터리 자체에서 메시지 파일을 작성하고 저장하려는 경우 메시지 파일 작성을 마치기 전에 Pickup 디렉터리에서 메시지 파일을 처리하려 할 수 있습니다.



맨 위로 이동

## Pickup 및 Replay 디렉터리에 대한 보안 고려 사항

다음 목록에는 Pickup 디렉터리 및 Replay 디렉터리에 대한 일반적인 보안 문제가 설명되어 있습니다.

  - Pickup 디렉터리 또는 Replay 디렉터리를 통해 전송되는 메시지에 대해서는 맬웨어 방지, 바이러스 백신, 보낸 사람 필터링 또는 받는 사람 필터링 작업 등 수신 커넥터에 구성된 보안 검사가 수행되지 않습니다.

  - 구성된 Pickup 디렉터리나 Replay 디렉터리는 오픈 릴레이로 작동할 수 있습니다. 이를 통해 다른 서버를 사용하여 메시지를 다시 전송하거나 *릴레이*하여 실제 메시지 원본을 마스크할 수 있습니다.

다음 목록에서는 Replay 디렉터리에 적용되는 추가 보안 문제에 대해 설명합니다.

  - Replay 디렉터리에서 사용되는 X-Header로 메시지 봉투를 수동으로 만들 수 있습니다. `X-Sender` 및 `X-Receiver` 필드의 정보는 전자 메일 클라이언트에 의해 표시된 `To` 또는 `From` 메시지 헤더 필드와 완전히 다를 수 있습니다. 이러한 보낸 사람 및 도메인에 대한 가장을 일반적으로 *스푸핑*이라고 합니다. *스푸핑된 메일*은 실제로 메시지를 보내지 않은 사람이 전자 메일 메시지를 보낸 것처럼 보이도록 주소가 수정된 전자 메일 메시지입니다.

  - `X-CreatedBy` 필드에 **MSExchange15**의 값이 있는 경우 대상, 신뢰할 수 있는 것으로 간주 됩니다 및 헤더 방화벽에 적용 되지 않습니다. *헤더 방화벽* 은 신뢰할 수 있는 Exchange 서버 간에 전송 되는 Exchange 메시지에 X-헤더를 보존 하는 방법을 또는 잠재적으로 제거 하려면 Exchange 조직 외부의 신뢰할 수 없는 대상으로 전송 메시지에서 X-헤더를 표시 합니다. 이러한 X-헤더를 사용 하 여 신뢰 scl (스팸), 메시지 서명, 예: Exchange 정보를 공유할 수 또는 권한이 부여 된 Exchange 서버 간의 암호화 합니다. 허가 되지 않은 원본에이 정보를 공개 잠재적 보안 위험이 따를 수 있습니다. 헤더 방화벽에 대 한 자세한 내용은 [이해 헤더 방화벽](https://go.microsoft.com/fwlink/?linkid=268394)을 참조 하십시오.

Replay 디렉터리와 관련된 추가 보안 위험으로 인해 Replay 디렉터리에는 더 강력한 보안이 적용되어야 합니다. 메시지를 생성하고 전송해야 하는 사용자나 응용 프로그램은 Pickup 디렉터리에 대한 액세스 권한을 부여받을 수 있으나 Replay 디렉터리에 대한 액세스 권한은 필요하지 않습니다.

기본적으로 Pickup 디렉터리와 Replay 디렉터리는 둘 다 모든 사서함 서버와 Edge 전송 서버에서 사용하도록 설정되어 있습니다. Pickup 디렉터리나 Replay 디렉터리가 조직의 특정 사서함 서버나 Edge 전송 서버에서 필요하지 않으면 Pickup 디렉터리 경로 또는 Replay 디렉터리 경로를 `$null` 값으로 설정하여 해당 서버에서 Pickup 디렉터리나 Replay 디렉터리를 사용하지 않게 할 수 있습니다. 자세한 내용은 [Pickup 디렉터리 및 Replay 디렉터리 구성](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md)을 참조하십시오.

맨 위로 이동

## Pickup 및 Replay 디렉터리에 대한 사용 권한

Pickup 및 Replay 디렉터리에는 다음 사용 권한이 필요합니다.

  - 관리자: 모든 권한

  - 시스템: 모든 권한

  - 네트워크 서비스: 하위 폴더 및 파일 읽기, 쓰기, 삭제 권한

기본적으로 Microsoft Exchange Transport Service는 네트워크 서비스 사용자 계정의 보안 자격 증명을 사용하여 Pickup 및 Replay 디렉터리의 위치 및 사용 권한을 관리합니다. 네트워크 서비스 계정에 이러한 권한이 있어야 Pickup 디렉터리에서 .eml 파일을 열고, .tmp로 이름을 바꾸어 삭제하거나, 메시지가 Badmail로 분류되는 경우 .bad로 이름을 바꿀 수 있습니다.

**Set-TransportService** cmdlet에 *PickupDirectoryPath* 및 *ReplayDirectoryPath* 매개 변수를 사용하여 이러한 디렉터리의 위치를 이동할 수 있습니다. Pickup 디렉터리의 위치 변경 성공 여부는 새로운 Pickup 디렉터리 위치에서 네트워크 서비스 계정에 부여된 권한과 새로운 디렉터리가 이미 존재하는지에 따라 달라집니다. 새 디렉터리가 없고 네트워크 서비스 계정에 새 위치에서 폴더를 만들고 권한을 적용하는 데 필요한 권한이 있는 경우 디렉터리가 생성되고 올바른 권한이 적용됩니다. 새 디렉터리가 이미 있으면 기존 폴더 권한이 확인되지 않습니다. **Set-TransportService** cmdlet에 *PickupDirectoryPath* 또는 *ReplayDirectoryPath* 매개 변수를 사용하여 디렉터리 위치를 이동할 때마다 새 디렉터리가 있고 새 디렉터리에 올바른 사용 권한이 적용되었는지 확인하십시오.

맨 위로 이동

