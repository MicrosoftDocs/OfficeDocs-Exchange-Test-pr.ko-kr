---
title: '스팸 지수 임계값: Exchange 2013 Help'
TOCTitle: 스팸 지수 임계값
ms:assetid: 0009b4af-be6d-41d2-98bc-b5487272c74a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa995744(v=EXCHG.150)
ms:contentKeyID: 50482365
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 스팸 지수 임계값

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-11-17_


> [!NOTE]
> 2016년 11월 1일, Microsoft가 Exchange 및 Outlook에서 SmartScreen 필터에 대한 스팸 정의 업데이트 생성을 중지했습니다. 기존 SmartScreen 스팸 정의는 제자리에 남게 되지만 시간 경과에 따라 효율성이 저하될 가능성이 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook 및 Exchange에서 SmartScreen에 대한 지원 삭제</A>를 참조하세요.



Microsoft Exchange Server 2013에서는 SCL(스팸 지수) 임계값에 따라 특정 동작을 정의할 수 있습니다. 예를 들어 콘텐츠 필터 에이전트를 실행 중인 Exchange 서버에서 메시지를 거부, 삭제 또는 격리하기 위한 다양한 임계값을 정의할 수 있습니다.

콘텐츠 필터 에이전트에 있는 이 SCL 임계값 구성과 사용자의 사서함에 있는 SCL 정크 메일 폴더 구성을 함께 사용하면 보다 광범위하고 정교한 스팸 방지 전략을 구현할 수 있습니다. Exchange 2013에서 보다 정확하고 자세한 SCL 임계값 조정 기능을 사용하면 Exchange 조직 전반에 스팸 방지 솔루션을 배포하고 유지 관리하는 총 비용을 줄일 수 있습니다.

콘텐츠 필터 에이전트는 다른 스팸 방지 에이전트가 인바운드 메시지를 처리한 후 스팸 방지 주기 후반에 메시지에 SCL 등급을 할당합니다. 콘텐츠 필터 에이전트에서 처리하기 전에 인바운드 메시지를 처리하는 대부분의 다른 스팸 방지 에이전트는 결정적 방식으로 메시지에 대한 작업을 수행합니다. 예를 들어 Edge 전송 서버의 연결 필터 에이전트는 실시간 차단 목록에 있는 IP 주소에서 보낸 메시지를 모두 거부합니다. 보낸 사람 필터 에이전트 및 받는 사람 필터 에이전트는 이와 유사한 결정적 방식으로 메시지를 처리합니다.

Exchange 2013에서는 이러한 결정적 방식의 스팸 방지 에이전트가 메시지를 먼저 처리하므로 콘텐츠 필터 에이전트에서 처리해야 하는 메시지의 수가 대폭 줄어듭니다. 스팸 방지 에이전트에서 메시지를 처리하는 순서에 대한 자세한 내용은 [스팸 방지 보호](anti-spam-protection-exchange-2013-help.md) 항목을 참조하십시오.

콘텐츠 필터링은 정확한 결정적 프로세스가 아니기 때문에 콘텐츠 필터 에이전트가 다른 SCL 값에 대해 수행하는 작업을 조정하는 기능이 중요합니다. SCL 임계값 구성을 신중하게 조정하여 다음 사항을 최소화할 수 있습니다.

  - 스팸 격리 저장소 크기

  - 실수로 격리된 합법적인 전자 메일 메시지의 수

  - Microsoft Outlook 사용자의 정크 메일 폴더에 도달하는 합법적인 전자 메일 메시지의 수

  - Outlook 사용자의 받은 편지함 또는 정크 메일 폴더에 도달하는 불쾌한 스팸 메일 메시지의 수

  - Outlook 사용자의 받은 편지함에 도달하는 스팸 메일 메시지의 수

## SCL 임계값 동작

SCL 임계값 동작을 조정하여 스팸 메일이 될 위험성이 높은 메시지에서 수행되는 콘텐츠 필터링 작업을 에스컬레이션할 수 있습니다. 다른 SCL 임계값 동작과 이들이 구현되는 방법을 이해하면 이러한 기능을 파악하는 데 도움이 됩니다.

  - **SCL 삭제 임계값**   특정 메시지에 대한 SCL 값이 SCL 삭제 임계값보다 크거나 같은 경우 콘텐츠 필터 에이전트에서 메시지를 삭제합니다. 보내는 시스템이나 보낸 사람에게 메시지가 삭제되었음을 알리는 프로토콜 수준의 통신이 없습니다. 메시지에 대한 SCL 값이 SCL 삭제 임계값보다 작은 경우 콘텐츠 필터 에이전트는 메시지를 삭제하지 않습니다. 대신 SCL 값과 SCL 거부 임계값을 비교합니다.

  - **SCL 거부 임계값**   특정 메시지에 대한 SCL 값이 SCL 거부 임계값보다 크거나 같은 경우 콘텐츠 필터 에이전트에서 메시지를 삭제하고 보내는 시스템에 거부 응답을 보냅니다. 거부 응답을 사용자 지정할 수 있습니다. 경우에 따라 NDR(배달 못 함 보고서)을 메시지를 처음 보낸 사람에게 보냅니다. 메시지에 대한 SCL 값이 SCL 삭제 및 SCL 거부 임계값보다 작은 경우 콘텐츠 필터 에이전트는 메시지를 삭제 또는 거부하지 않습니다. 대신 SCL 값과 SCL 격리 임계값을 비교합니다.

  - **SCL 격리 임계값**   특정 메시지에 대한 SCL 값이 SCL 격리 임계값보다 크거나 같은 경우 콘텐츠 필터 에이전트에서 격리 사서함으로 메시지를 보냅니다. 전자 메일 관리자는 격리 사서함을 정기적으로 검토해야 합니다. 메시지에 대한 SCL 값이 SCL 삭제, 거부 및 격리 임계값보다 작은 경우 콘텐츠 필터 에이전트는 메시지를 삭제, 거부 또는 격리하지 않습니다. 대신 해당 사서함 서버에 메시지를 보냅니다. 이 서버에서는 메시지에 대해 받는 사람당 SCL 정크 메일 폴더 임계값을 평가합니다.

  - **SCL 정크 메일 폴더 임계값**   특정 메시지의 SCL 값이 SCL 정크 메일 폴더 임계값을 초과하면 메시지가 사용자의 정크 메일 폴더로 배달됩니다. 메시지의 SCL 값이 SCL 삭제, 거부, 격리 및 정크 메일 폴더 임계값보다 작으면 메시지가 사용자의 받은 편지함으로 배달됩니다.

콘텐츠 필터 에이전트와 정크 메일 폴더는 SCL 임계값을 다르게 처리합니다. 콘텐츠 필터 에이전트의 경우 사용자가 구성한 SCL 임계값에 따라 작업을 실행합니다. 정크 메일 폴더의 경우에는 사용자가 구성한 SCL 임계값에 1을 더한 값에 따라 작업을 실행합니다. 예를 들어 삭제 작업을 SCL 콘텐츠 필터 에이전트에 SCL 값 8로 구성하면 SCL 값이 8 이상인 모든 메시지가 삭제됩니다. 그러나 SCL 임계값을 4로 지정하여 정크 메일 폴더를 구성하면 SCL 값이 5 이상인 모든 메시지는 정크 메일 폴더로 이동됩니다.

예를 들어 SCL 삭제 임계값, 거부 임계값, 격리 임계값 및 정크 메일 폴더 임계값을 각각 8, 7, 6, 5로 설정하면 SCL 값이 5보다 작은 메시지는 모두 사용자의 사서함으로 배달됩니다. SCL 값이 5인 메시지는 사용자의 정크 메일 폴더에 배치됩니다. SCL 값이 4 이하인 메시지는 사용자의 받은 편지함에 배치됩니다.

다음 위치에서 SCL 삭제, 거부, 격리 및 정크 메일 폴더 설정을 구성할 수 있습니다.

  - **콘텐츠 필터 에이전트 구성(전송 서버당 SCL 구성)**   **Set-ContentFilterConfig** cmdlet을 사용하여 콘텐츠 필터 에이전트를 실행 중인 Exchange 서버에 SCL 삭제, 거부 및 격리 임계값을 사용하거나 사용하지 않도록 설정하고, 이에 대한 설정을 구성할 수 있습니다. 시간이 지남에 따라 사용자가 스팸 방지 로깅 및 보고 기능에서 제공하는 스팸 기능 및 메트릭을 분석하기 때문에 필요한 경우 이러한 SCL 임계값 구성을 추가로 조정할 수 있습니다.
    
    **Set-ContentFilterConfig** cmdlet에서 사용할 수 있는 SCL 매개 변수는 다음 표에 설명되어 있습니다.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>매개 변수</th>
    <th>설명</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLDeleteEnabled</em></p></td>
    <td><p>이 매개 변수는 메시지의 SCL 값이 <em>SCLDeleteThreshold</em> 매개 변수로 지정된 값보다 크거나 같을 때 NDR(배달 못 함 보고서)이 없는 메시지를 삭제하는 기능을 사용하거나 사용하지 않도록 설정합니다. 이 매개 변수에 유효한 입력은 <code>$true</code> 또는 <code>$false</code>입니다.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLDeleteThreshold</em></p></td>
    <td><p>이 매개 변수에는 0에서 9까지의 정수를 입력할 수 있습니다. 이 매개 변수의 값은 다른 SCL 임계값 매개 변수보다 커야 합니다. 이 매개 변수는 <em>SCLDeleteEnabled</em> 매개 변수 값이 <code>$true</code>인 경우에만 의미가 있습니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLRejectEnabled</em></p></td>
    <td><p>이 매개 변수는 메시지의 SCL 값이 <em>SCLRejectThreshold</em> 매개 변수로 지정된 값보다 크거나 같을 때 NDR이 있는 메시지를 거부하는 기능을 사용하거나 사용하지 않도록 설정합니다. 이 매개 변수에 유효한 입력은 <code>$true</code> 또는 <code>$false</code>입니다.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLRejectThreshold</em></p></td>
    <td><p>이 매개 변수에는 0에서 9까지의 정수를 입력할 수 있습니다. 이 매개 변수의 값은 <em>SCLDeleteThreshold</em> 매개 변수보다는 작고 다른 SCL 임계값 매개 변수보다는 커야 합니다. 이 매개 변수는 <em>SCLRejectEnabled</em> 매개 변수의 값이 <code>$true</code>인 경우에만 유효합니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLQuarantineEnabled</em></p></td>
    <td><p>이 매개 변수는 메시지의 SCL 값이 <em>SCLQuarantineThreshold</em> 매개 변수로 지정된 값보다 크거나 같을 때 메시지를 스팸 격리 사서함으로 보내는 기능을 사용하거나 사용하지 않도록 설정합니다. 이 매개 변수에 유효한 입력은 <code>$true</code> 또는 <code>$false</code>입니다.</p>
    <p>스팸 메일 격리 사서함에 대한 자세한 내용은 <a href="spam-quarantine-exchange-2013-help.md">스팸 격리</a>를 참조하십시오.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLQuarantineThreshold</em></p></td>
    <td><p>이 매개 변수에는 0에서 9까지의 정수를 입력할 수 있습니다. 이 매개 변수의 값은 <strong>Set-OrganizationConfig</strong> 또는 <strong>Set-Mailbox</strong> cmdlet의 <em>SCLRejectThreshold</em> 매개 변수보다는 작고 <em>SCLJunkThreshold</em> 매개 변수보다는 커야 합니다. 이 매개 변수는 <em>SCLQuarantineThreshold</em> 매개 변수 값이 <code>$true</code>인 경우에만 의미가 있습니다.</p></td>
    </tr>
    </tbody>
    </table>


  - **조직 구성 설정(조직 차원의 SCL 구성)**   **Set-OrganizationConfig** cmdlet을 사용하여 조직에 있는 모든 사서함의 SCL 정크 메일 폴더 임계값을 설정할 수 있습니다.
    
    **Set-OrganizationConfig** cmdlet에서 사용할 수 있는 SCL 매개 변수는 다음 표에 설명되어 있습니다. SCLJunkThreshold를 사용한 예를 보려면 [사서함에 대해 스팸 방지 설정 구성](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)을 참조하세요.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>매개 변수</th>
    <th>설명</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkThreshold</em></p></td>
    <td><p>이 매개 변수는 메시지가 받는 사람 사서함의 정크 메일 폴더로 이동하기 전에 초과해야 하는 SCL 값을 지정합니다. 이 매개 변수에는 0에서 9까지의 정수를 입력할 수 있습니다. 이 매개 변수의 값은 다른 SCL 임계값 매개 변수보다 작아야 합니다. 예를 들어 값을 4로 지정하면 SCL 값이 5 이상인 메시지가 사용자의 정크 메일 폴더로 이동됩니다.</p></td>
    </tr>
    </tbody>
    </table>


  - **사용자 사서함(받는 사람당 SCL 구성)**   **Set-Mailbox** cmdlet을 사용하여 개별 사서함에 받는 사람당 SCL 삭제, 거부, 격리 및 정크 메일 폴더 임계값을 사용하거나 사용하지 않도록 설정하고, 이에 대한 설정을 구성할 수 있습니다. 개별 사서함에 SCL 정크 메일 폴더 임계값을 사용하거나 사용하지 않도록 설정하는 데는 **Set-Mailbox** cmdlet만 사용할 수 있습니다. 받는 사람당 SCL 삭제, 거부 및 격리 임계값은 Active Directory에 저장되고 Microsoft Exchange EdgeSync 서비스를 통해 구독되는 Edge 전송 서버에 복제됩니다. 사용자가 전송 서버당 SCL 구성을 설정한 경우에도 콘텐츠 필터 에이전트에서 받는 사람당 SCL 임계값 구성을 사용합니다. 따라서 받는 사람당 SCL 임계값을 설정한 경우 콘텐츠 필터 에이전트는 SCL 구성 대신 특정 사용자에 대해 받는 사람당 SCL 임계값을 사용합니다. 예를 보려면 [사서함에 대해 스팸 방지 설정 구성](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)을 참조하세요.
    

    > [!NOTE]
    > 받는 사람당 SCL 임계값은 메일 그룹을 통해 받은 메일에는 적용되지 않습니다.

    
    **Set-ContentFilterConfig** 및 **Set-OrganizationConfig** cmdlet에서 사용할 수 있는 것과 동일한 SCL 매개 변수를 **Set-Mailbox** cmdlet에서도 사용할 수 있습니다.
    
      - *SCLDeleteEnabled*
    
      - *SCLDeleteThreshold*
    
      - *SCLRejectEnabled*
    
      - *SCLRejectThreshold*
    
      - *SCLQuarantineEnabled*
    
      - *SCLQuarantineThreshold*
    
      - *SCLJunkThreshold*
    
    그러나 **Set-Mailbox** cmdlet의 모든 SCL 매개 변수는 `$null`도 값으로 받아들입니다. 사서함의 SCL 설정이 비어 있으면(`$null`) 해당 콘텐츠 필터 에이전트 설정이나 조직 구성 설정이 사서함에 적용됩니다. 사서함의 SCL 설정 값이 `$true` 또는 `$false`이면 사서함의 설정이 콘텐츠 필터 에이전트나 조직 구성의 해당 조직 차원의 설정을 다시 정의합니다.
    
    **Set-Mailbox** cmdlet에서만 사용할 수 있는 SCL 매개 변수는 다음 표에 설명되어 있습니다.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>매개 변수</th>
    <th>설명</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkEnabled</em></p></td>
    <td><p>이 매개 변수는 메시지의 SCL 값이 <em>SCLQuarantineThreshold</em> 매개 변수로 지정된 값보다 클 때 메시지를 사용자의 정크 메일 폴더로 배달하는 기능을 사용하거나 사용하지 않도록 설정합니다. 이 매개 변수에 유효한 입력은 <code>$true</code>, <code>$false</code> 또는 <code>$null</code>입니다.</p>
    <p>정크 메일 필터링은 조직의 모든 사용자 사서함에 대해 기본적으로 사용됩니다. 기본적으로 <em>Enabled</em> 매개 변수는 모든 사용자 사서함의 <strong>Set-MailboxJunkEmailConfiguration</strong> cmdlet에서 <code>$true</code> 값으로 설정됩니다.</p></td>
    </tr>
    </tbody>
    </table>
    
    사서함의 SCL 임계값 구성에 대한 자세한 내용은 [사서함에 대해 스팸 방지 설정 구성](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md) 항목을 참조하십시오.

## SCL 임계값 모니터링

`%ExchangeInstallPath%Scripts` 폴더에 있는 여러 기본 제공 스크립트(예: **get-AntispamSCLHistogram.ps1**)를 필터링 결과 데이터 수집에 사용할 수 있습니다. 데이터에서 사용자의 즉각적인 조정이 필요하다고 나타나는 경우 SCL 임계값을 다시 구성하십시오. 그렇지 않으면 데이터를 수집하고 스팸 보고를 분석하여 조정이 필요한 지 여부를 결정합니다.

