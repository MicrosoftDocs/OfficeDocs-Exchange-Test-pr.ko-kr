---
title: '파이프라인 추적: Exchange 2013 Help'
TOCTitle: 파이프라인 추적
ms:assetid: e7780499-9a6f-48b1-aea8-df88ecd8b18a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125018(v=EXCHG.150)
ms:contentKeyID: 52058145
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 파이프라인 추적

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

파이프라인 추적 사서함 서버의 사서함 전송 배달 서비스 사서함 서버의 전송 서비스를 통해 및 Edge 전송 서버를 통해 이동 하는 것에 따라 특정 사용자가 보낸에서 전자 메일 메시지의 복사본을 캡처합니다. 파이프라인 추적 각 전송 에이전트에 메시지 스냅숏 파일이 전송 파이프라인에 메시지에 적용 되는 변경 내용에 대 한 자세한 정보를 캡처합니다. 메시지 스냅숏 파일의 내용을 검사 하 여 전송 에이전트 예상한 전송 파이프라인에 메시지에 변경 내용을 적용을 확인할 수 있습니다. 확인 해야가 문제를 해결 하는 경우 전송 에이전트는 내결함성에 있습니다. 다음 문제를 해결 하려면 해당 에이전트에서 모든 문제 해결 노력을 집중할 수 있습니다. 그런 다음 솔루션 성공 인지 확인 하는 다시 메시지 스냅숏 파일을 볼 수 있습니다.


> [!WARNING]
> <UL>
> <LI>
> <P>보낸 사람의 전자 메일 주소에서 보내는 전자 메일 메시지의 전체 내용을 복사 하는 파이프라인 추적 합니다. 원치 않는 노출 기밀 정보를 방지 하려면 파이프라인 추적 폴더에 적절 한 보안 사용 권한을 설정 해야 합니다.</P>
> <LI>
> <P>오랜 시간 동안 파이프라인 추적을 사용 하지 마십시오. 파이프라인 추적 신속 하 게 누적 될 수 있는 파일을 만듭니다. 파이프라인 추적을 사용 하는 경우에 항상 사용 가능한 디스크 공간을 모니터링 합니다.</P></LI></UL>



## 파이프라인 추적 구성

파이프라인 추적을 사용 하도록 설정 하기 전에 모니터링 하려는 보낸 사람의 전자 메일 주소를 지정 해야 합니다. 파이프라인 추적은 특정 전자 메일 주소에서 보낸 메시지를 기록 하도록 설계 되었습니다. 보낸 사람의 전자 메일 주소는 Exchange 조직 내부 또는 외부 수 있습니다. 또는 자동 회신, 배달 상태 알림 (DSN) 메시지, 저널 보고서 및 파이프라인 추적 폴더의 위치를 수정할 수도 있습니다 다른 시스템에서 생성 된 메시지와 같은 지정된 된 사서함 또는 Edge 전송 서버에서 전송 서비스에서 생성 하는 시스템 메시지에 대 한 파이프라인 추적을 설정할 수 있습니다.

사용 하 여 파이프라인 추적을 구성 하는 매개 변수는 다음 표에 요약 된


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>cmdlet</th>
<th>매개 변수</th>
<th>기본값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingSenderAddress</em></p></td>
<td><p>공백 (<code>$null</code>)</p></td>
<td><p>모니터링 하려는 보낸 사람의 전자 메일 주소를 지정 합니다.</p>
<p>서버에서 지정 된 전송 서비스에 의해 전송 된 시스템에서 생성 된 메시지를 모니터링 하는 값 &quot;&lt;&gt;&quot; 를 지정 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingPath</em></p></td>
<td><p><strong>전송 서비스</strong> <code>%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing</code>   </p>
<p><strong>사서함 전송 서비스</strong> <code>%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing</code>   </p></td>
<td><p>경로 로컬 서버에 있어야 합니다. UNC 경로 지원 되지 않습니다.</p>
<p>지정된 된 경로 파이프라인 추적 파일이 저장 된 <code>MessageSnapshots</code> 폴더를 포함 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingEnabled</em></p></td>
<td><p><code>$false</code></p></td>
<td><p>모니터링 하려는 보낸사람 주소를 구성한 후에 서버에서 지정 된 전송 서비스에 대 한 파이프라인 추적을 사용할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


파이프라인 추적을 사용 하도록 설정 하 고 구성 하는 방법에 대 한 자세한 내용은 파이프라인 추적 보낸사람 주소 [파이프라인 추적 구성](configure-pipeline-tracing-exchange-2013-help.md)를 참조 합니다.

## 메시지 스냅숏 파일

메시지 스냅숏을 파일 전송 서비스 또는 사서함 전송 배달 서비스에서 전송 에이전트에 의해 메시지에 대 한 모든 변경 내용을 캡처하려면입니다. 이러한 파일은 전송 서비스에 대 한 대응 하는 파이프라인 추적 경로에서 `MessageSnapshots` 폴더에 저장 됩니다.

`MessageSnapshots` 폴더를 Exchange 지정한 전송 서비스를 통해 전달 되는 모니터링 된 보낸 사람이 보낸 각 메시지에 대 한 폴더를 만듭니다. 각 폴더의 메시지에 할당 된 GUID 따서 지정 됩니다. 전송 서비스와 같은 사서함 서버의 사서함 전송 서비스에 대 한 파이프라인 추적을 사용 하도록 설정 하는 경우 메시지 이므로 전송 서비스에 대 한 `MessageSnapshots` 폴더에 메시지에 대 한 폴더 이름을 사서함 전송 서비스에 대 한 `MessageSnapshots` 폴더에 동일한 메시지에 대 한 폴더 이름과 다른 각 전송 서비스에 의해 동일한 메시지에 다른 GUID 할당 됩니다. 둘 이상의 Exchange 서버에서 파이프라인 추적을 사용 하도록 설정 하는 경우 각 Exchange 서버에서 지정 된 전송 서비스를 통해 전달 되는 것 처럼 다른 GUID는 동일한 메시지에 할당 됩니다.

각 메시지 폴더를 Exchange.eml 파일 확장명을 포함 하는 여러 메시지 스냅숏 파일을 만듭니다. 이러한 메시지 스냅숏 파일이 각 SMTP 이벤트 및 전송 에이전트 만날 메시지의 내용을 포함 합니다.

전송 에이전트가 SMTP 이벤트에 등록 하는 경우 메시지에서 모든 전송 에이전트를 발생 하기 전에 Exchange에 메시지의 메시지 스냅숏을 만듭니다. 이렇게 하면 메시지의 복사본을 메시지에서 해당 이벤트에 등록 된 전송 에이전트를 발생 하기 전에 있습니다. 그런 다음, 새 메시지 스냅숏이 만들어집니다 각 전송 에이전트에 대 한 하는 메시지를 발견, 전송 에이전트는 메시지의 내용을 수정 하는 여부에 관계 없이. 그러나 에이전트가 이벤트에 등록 된, Exchange 해당 이벤트에 대 한 모든 메시지 스냅숏을 만들지 않습니다.

예, 에이전트가 세 **OnEndofData** 이벤트에 등록 된, 전송 에이전트의 두에만 메시지를 수정 하는 경우 4 개 메시지 스냅숏 만들어집니다. 첫번째 메시지 스냅숏 해당 이벤트에 등록 하는 전송 에이전트에 의해 적용 된 모든 수정 하기 전에 **OnEndofData** 이벤트가 발생할 때 메시지를 캡처합니다. 그런 다음, 전송 에이전트는 메시지를 수정 하는 여부에 관계 없이 각 전송 에이전트에 대해 하나의 메시지 스냅숏이 만들어집니다.

생성 되는 메시지 스냅숏 파일은 다음 목록에 설명 합니다.

  - **Original.eml** 이 파일 전송 에이전트 이나 SMTP 이벤트가 발생 하기 전에 전자 메일 메시지의 원래 수정 되지 않은 내용을 포함 됩니다.

  - **Routingnnnn.eml** 이러한 파일은 SMTP 전송 이벤트 및 전송 서비스의 분류 부분에 이러한 이벤트에 등록 된 전송 에이전트 만날 전자 메일 메시지의 내용을 포함 합니다. 개체 틀 *nnnn*`0001`로 시작 하는 integer 값을 나타냅니다. 이벤트 및 에이전트는 메시지에 대해 작동 하는 순서에 해당 이벤트에 등록 된 모든 SMTP 이벤트 및 전송 에이전트에 대 한 값이 증가 합니다. 사서함 전송 배달 서비스는 이러한 **Routing** 스냅숏 파일을 생성 하지 않습니다.

  - **SmtpReceivennnn.eml** 이러한 파일 **OnEndofData** 및 **OnEndOfHeaders** SMTP 이벤트를 발생 하 고 SMTP 하는 동안 해당 이벤트에 등록 된 전송 에이전트 전송 서비스 또는 사서함 전송 배달 서비스의 일부를 받을 때 전자 메일 메시지의 내용을 포함 합니다. 개체 틀 *nnnn*`0001`로 시작 하는 integer 값을 나타냅니다. 이벤트 및 에이전트는 메시지에 대해 작동 하는 순서에 해당 이벤트에 등록 된 모든 SMTP 이벤트 및 전송 에이전트에 대 한 값이 증가 합니다.

메모장 이나 다른 텍스트 편집기를 사용 하 여 메시지 스냅숏 파일을 열 수 있습니다.

각 메시지 스냅숏 파일이 메시지 내용을에 추가 되 고 메시지 스냅숏 파일에 관련 된 SMTP 이벤트 및 전송 에이전트를 나열 하는 헤더도 시작 됩니다. 이러한 헤더는 `X-CreatedBy: MessageSnapshot-Begin injected headers` 로 시작 하 고 `X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers`를 끝나야 합니다. 이러한 헤더는 각 메시지 스냅숏 파일에서 각 후속 전송 에이전트 및 SMTP 이벤트도 대체 됩니다. 다음은 전자 메일 메시지 파일에 추가 되는 머리글의 한 예입니다.

    X-CreatedBy: MessageSnapshot-Begin injected headers
    X-MessageSnapshot-UTC-Time: 2013-01-23T23:20:18.138Z
    X-MessageSnapshot-Record-Id: 21474836486
    X-MessageSnapshot-Source: OnSubmittedMessageX-Sender: michelle@nwtraders.com
    X-Receiver: chris@contoso.com
    X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers

메시지 스냅숏 헤더 파일 모든 원본 메시지 헤더를 포함 하 여 메시지의 내용을 들어 있습니다. 전송 에이전트는 메시지의 내용을 수정 하는 경우 변경 내용이 메시지와 함께 통합 나타납니다. 각 전송 에이전트에 의해 메시지 처리는 각 에이전트에 의해 적용 된 변경 내용은 메시지 내용을에 적용 됩니다. 전송 에이전트 메시지 내용을 변경할 수 없습니다가 해당 에이전트에 의해 생성 되는 메시지 스냅숏 이전 전송 에이전트에 의해 만들어진 메시지 스냅숏 동일 됩니다.

