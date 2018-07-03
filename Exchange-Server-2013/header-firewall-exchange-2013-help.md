---
title: '헤더 방화벽: Exchange 2013 Help'
TOCTitle: 헤더 방화벽
ms:assetid: 9b148f7b-47a9-4379-a55b-8d5310c1772f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232136(v=EXCHG.150)
ms:contentKeyID: 52058107
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 헤더 방화벽

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange Server 2013에서 *헤더 방화벽*은 인바운드와 아웃바운드 메시지에서 특정 헤더 필드를 제거하는 메커니즘입니다. 헤더 방화벽의 영향을 받는, 다음과 같은 두 가지 유형의 헤더 필드가 있습니다.

  - **X-헤더**   *X-헤더*는 사용자가 정의한 비공식 헤더 필드입니다. X-헤더는 RFC 2822에 구체적으로 언급되어 있지 않지만 **X-**로 시작하는 정의되지 않은 헤더 필드의 사용은 메시지에 비공식적인 헤더 필드를 추가하는 일반적인 방법이 되었습니다. 스팸 방지, 바이러스 백신 및 메시징 서버와 같은 메시징 응용 프로그램은 고유한 X-헤더를 메시지에 추가할 수 있습니다. Exchange에서 X-헤더 필드에는 SCL(스팸 지수), 콘텐츠 필터링 결과 및 규칙 처리 상태와 같이 전송 서비스에서 메시지에 대해 수행하는 작업에 대한 자세한 정보가 포함되어 있습니다. 이러한 정보를 인증되지 않은 소스에 공개하는 것은 잠재적 보안 위험을 내포할 수 있습니다.

  - **라우팅 헤더**   라우팅 헤더는 RFC 2821 및 RFC 2822에서 정의된 표준 SMTP 헤더 필드입니다. 라우팅 헤더는 메시지를 받는 사람에게 전달하는 데 사용된 서로 다른 메시징 서버에 대한 정보를 사용하여 메시지를 스탬프 처리합니다. 악의적인 사용자에 의해 메시지에 삽입된 라우팅 헤더는 메시지가 받는 사람에게 도달하기 위해 이동한 라우팅 경로를 잘못 표시할 수 있습니다.

헤더 방화벽은 신뢰되지 않은 원본에서 Exchange 조직에 들어오는 인바운드 메시지에서 X-헤더를 제거하여 이러한 Exchange 관련 X-헤더의 스푸핑을 방지합니다. 헤더 방화벽은 Exchange 조직 외부의 신뢰되지 않은 대상으로 이동하는 아웃바운드 메시지에서 X-헤더를 제거하여 이러한 Exchange 관련 X-헤더의 노출을 방지합니다. 헤더 방화벽은 또한 메시지의 라우팅 기록을 추적하는 데 사용되는 표준 라우팅 헤더의 스푸핑을 방지합니다.

**목차**

Message header fields affected by header firewall in Exchange

How header firewall is applied to Receive connectors and Send connectors

Header firewall for inbound messages on Receive connectors

Header firewall for outbound messages on Send connectors

Header firewall for other message sources

Organization X-headers and forest X-headers in Exchange

## Exchange의 헤더 방화벽의 영향을 받는 메시지 헤더 필드

다음과 같은 유형의 X-헤더 및 라우팅 헤더가 헤더 방화벽의 영향을 받습니다.

  - **조직 X-헤더**   이러한 X-헤더 필드는 **X-MS-Exchange-Organization-**으로 시작합니다.

  - **포리스트 X-헤더**   이러한 X-헤더 필드는 **X-MS-Exchange-Forest-**로 시작합니다.
    
    조직 X-헤더 및 포리스트 X-헤더의 예를 보려면 이 항목 끝부분에 있는 Organization X-headers and forest X-headers in Exchange 섹션을 참조하십시오.

  - **Received: 라우팅 헤더**   받는 사람에 대해 메시지를 수락하고 전달한 모든 메시징 서버에 의해 이 헤더 필드의 다른 인스턴스가 메시지 머리글에 추가됩니다. **Received:**  헤더에는 일반적으로 메시징 서버의 이름과 날짜 타임스탬프가 포함됩니다.

  - **Resent-\*: 라우팅 헤더**   Resent 헤더 필드는 메시지가 특정 사용자에 의해 전달되었는지 여부를 확인하는 데 사용할 수 있는 정보 헤더 필드입니다. 여기서는 **Resent-Date:** , **Resent-From:** , **Resent-Sender:** , **Resent-To:** , **Resent-Cc:** , **Resent-Bcc:**  및 **Resent-Message-ID:** 와 같은 Resent 헤더 필드를 사용할 수 있습니다. **Resent-** 필드는 메시지가 원래 보낸 사람이 직접 보낸 것처럼 받는 사람에게 나타나도록 하는 데 사용됩니다. 받는 사람은 메시지 머리글을 보고 메시지를 전달한 사람을 알 수 있습니다.

Exchange에서는 다음과 같은 두 개의 방법을 사용하여 메시지에 있는 조직 X-헤더, 포리스트 X-헤더 및 라우팅 헤더에 헤더 방화벽을 적용합니다.

  - 커넥터를 통해 메시지가 전송될 때 메시지에 특정 유형의 헤더를 보존하거나 제거하는 데 사용할 수 있는 사용 권한을 송신 커넥터 또는 수신 커넥터에 할당합니다.

  - 다른 유형의 메시지 전송 동안 헤더 방화벽이 메시지의 특정 유형의 헤더에 대해 자동으로 구현됩니다.

맨 위로 이동

## 헤더 방화벽을 수신 커넥터 및 송신 커넥터에 적용하는 방법

헤더 방화벽은 커넥터에 할당된 특정 사용 권한을 바탕으로 수신 커넥터 및 송신 커넥터를 통과하는 메시지에 적용됩니다.

사용 권한이 수신 커넥터나 송신 커넥터에 할당된 경우 헤더 방화벽은 커넥터를 통과하는 메시지에 적용되지 않습니다. 영향을 받는 헤더 필드는 메시지에 보존됩니다.

사용 권한이 수신 커넥터나 송신 커넥터에 할당되지 않은 경우에는 헤더 방화벽이 커넥터를 통과하는 메시지에 적용됩니다. 영향을 받는 헤더 필드는 메시지에서 제거됩니다.

다음 표에는 헤더 방화벽을 적용하는 데 사용되는 송신 커넥터 및 수신 커넥터에 대한 사용 권한 및 영향을 받는 헤더 필드가 나와 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>커넥터 유형</th>
<th>사용 권한</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>수신 커넥터</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong></p></td>
<td><p>이 사용 권한은 인바운드 메시지에서 <strong>X-MS-Exchange-Organization-</strong>으로 시작하는 조직 X-헤더 필드에 영향을 줍니다.</p></td>
</tr>
<tr class="even">
<td><p>수신 커넥터</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><p>이 사용 권한은 인바운드 메시지에서 <strong>X-MS-Exchange-Forest-</strong>로 시작하는 포리스트 X-헤더 필드에 영향을 줍니다.</p></td>
</tr>
<tr class="odd">
<td><p>수신 커넥터</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>이 사용 권한은 인바운드 메시지에서 <strong>Received:</strong> 및 <strong>Resent-*:</strong> 라우팅 헤더 필드에 영향을 줍니다.</p></td>
</tr>
<tr class="even">
<td><p>송신 커넥터</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong></p></td>
<td><p>이 사용 권한은 아웃바운드 메시지에서 <strong>X-MS-Exchange-Organization-</strong>으로 시작하는 조직 X-헤더 필드에 영향을 줍니다.</p></td>
</tr>
<tr class="odd">
<td><p>송신 커넥터</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><p>이 사용 권한은 아웃바운드 메시지에서 <strong>X-MS-Exchange-Forest-</strong>로 시작하는 포리스트 X-헤더 필드에 영향을 줍니다.</p></td>
</tr>
<tr class="even">
<td><p>송신 커넥터</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>이 사용 권한은 아웃바운드 메시지에서 <strong>Received:</strong> 및 <strong>Resent-*:</strong> 라우팅 헤더 필드에 영향을 줍니다.</p></td>
</tr>
</tbody>
</table>


## 수신 커넥터의 인바운드 메시지에 대한 헤더 방화벽

다음 표에서는 수신 커넥터에서 헤더 방화벽 사용 권한의 기본 적용에 대해 설명합니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>사용 권한</th>
<th>할당된 사용 권한이 있는 기본 Exchange 보안 주체</th>
<th>보안 주체가 구성원인 사용 권한 그룹</th>
<th>사용 권한 그룹을 수신 커넥터에 할당하는 기본 사용 유형</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong> 및 <strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><ul>
<li><p>허브 전송 서버</p></li>
<li><p>Edge 전송 서버</p></li>
<li><p>Exchange Server</p>

> [!NOTE]  
> 허브 전송 서버에서만 해당


</li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>익명 사용자 계정</p></td>
<td><p><strong>Anonymous</strong></p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>인증된 사용자 계정</p></td>
<td><p><strong>ExchangeUsers</strong></p></td>
<td><p><code>Client</code>(Edge 전송 서버에서는 사용할 수 없음)</p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><ul>
<li><p>허브 전송 서버</p></li>
<li><p>Edge 전송 서버</p></li>
<li><p>Exchange Server</p>

> [!NOTE]  
> 허브 전송 서버만 해당


</li>
<li><p>외부 보안 서버</p></li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>파트너 서버 계정</p></td>
<td><p><strong>파트너</strong></p></td>
<td><p><code>Internet</code> 및 <code>Partner</code></p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 사용자 지정 수신 커넥터의 헤더 방화벽

사용자 지정 수신 커넥터 시나리오에서 헤더 방화벽을 메시지에 적용하려는 경우 다음 방법을 사용합니다.

  - 메시지에 헤더 방화벽이 자동으로 적용되는 사용 유형의 수신 커넥터를 만듭니다. 사용 유형은 수신 커넥터를 만들 때에만 설정할 수 있습니다.
    
      - 메시지에서 조직 X-헤더나 포리스트 X-헤더를 제거하려면 수신 커넥터를 만들고 `Internal` 이외의 사용 유형을 선택합니다.
    
      - 메시지에서 라우팅 헤더를 제거하려면 다음 작업 중 하나를 수행합니다.
        
          - 수신 커넥터를 만들고 사용 유형으로 `Custom`을 선택합니다. 수신 커넥터에 사용 권한을 할당하지 마십시오.
        
          - 기존의 수신 커넥터를 수정하고 *PermissionGroups* 매개 변수를 `None` 값으로 설정합니다.
        
        수신 커넥터에 할당된 사용 권한 그룹이 없는 수신 커넥터가 있는 경우 마지막 단계에서 설명한 대로 수신 커넥터에 보안 주체를 추가해야 합니다.

  - **Remove-ADPermission** cmdlet을 사용하여 수신 커넥터에 대해 구성된 보안 주체에서 **Ms-Exch-Accept-Headers-Organization** 사용 권한, **Ms-Exch-Accept-Headers-Forest** 사용 권한 및 **Ms-Exch-Accept-Headers-Routing** 사용 권한을 제거합니다. 사용 권한 그룹의 그룹 구성원 자격이나 사용 권한 할당을 수정할 수 없으므로 사용 권한이 수신 커넥터의 사용 권한 그룹을 사용하여 보안 주체에 할당된 경우에는 이 방법을 실행할 수 없습니다.

  - **Add-ADPermission** cmdlet을 사용하여 수신 커넥터의 메일 흐름에 필요한 해당 보안 주체를 추가합니다. 보안 주체에 **Ms-Exch-Accept-Headers-Organization** 사용 권한, **Ms-Exch-Accept-Headers-Forest** 사용 권한 및 **Ms-Exch-Accept-Headers-Routing** 사용 권한이 할당되지 않았는지 확인합니다. 필요한 경우 **Add-ADPermission** cmdlet을 사용하여 수신 커넥터에 대해 구성된 보안 주체에 대한 **Ms-Exch-Accept-Headers-Organization** 사용 권한, **Ms-Exch-Accept-Headers-Forest** 사용 권한 및 **Ms-Exch-Accept-Headers-Routing** 사용 권한을 거부합니다.

자세한 내용은 다음 항목을 참조하십시오.

  - [수신 커넥터](receive-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/ko-kr/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/ko-kr/library/aa996048\(v=exchg.150\))

맨 위로 이동

## 송신 커넥터의 아웃바운드 메시지에 대한 헤더 방화벽

다음 표에서는 송신 커넥터에서 헤더 방화벽 사용 권한의 기본 적용에 대해 설명합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>사용 권한</th>
<th>할당된 사용 권한이 있는 기본 Exchange 보안 주체</th>
<th>보안 주체를 송신 커넥터에 할당하는 기본 사용 유형</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong> 및 <strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><ul>
<li><p>허브 전송 서버</p></li>
<li><p>Edge 전송 서버</p></li>
<li><p>Exchange Server</p>

> [!NOTE]  
> 허브 전송 서버에서만 해당


</li>
<li><p>외부 보안 서버</p></li>
<li><p><strong>ExchangeLegacyInterop</strong> 유니버설 보안 그룹</p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><ul>
<li><p>허브 전송 서버</p></li>
<li><p>Edge 전송 서버</p></li>
<li><p>Exchange Server</p>

> [!NOTE]  
> 허브 전송 서버에서만 해당


</li>
<li><p>외부 보안 서버</p></li>
<li><p><strong>ExchangeLegacyInterop</strong> 유니버설 보안 그룹</p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>익명 사용자 계정</p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>파트너 서버</p></td>
<td><p><code>Partner</code></p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 사용자 지정 송신 커넥터의 헤더 방화벽

사용자 지정 송신 커넥터 시나리오에서 헤더 방화벽을 메시지에 적용하려는 경우 다음 방법을 사용합니다.

  - 메시지에 헤더 방화벽이 자동으로 적용되는 사용 유형의 송신 커넥터를 만듭니다. 사용 유형은 송신 커넥터를 만들 때에만 설정할 수 있습니다.
    
      - 메시지에서 조직 X-헤더나 포리스트 X-헤더를 제거하려면 송신 커넥터를 만들고 `Internal` 또는 `Partner` 이외의 사용 유형을 선택합니다.
    
      - 메시지에서 라우팅 헤더를 제거하려면 송신 커넥터를 만들고 사용 유형으로 `Custom`을 선택합니다. **Ms-Exch-Send-Headers-Routing** 사용 권한은 `Custom`을 제외한 모든 송신 커넥터 사용 유형에 할당됩니다.

  - 커넥터에서 **Ms-Exch-Send-Headers-Organization** 사용 권한, **Ms-Exch-Send-Headers-Forest** 및 **Ms-Exch-Send-Headers-Routing** 사용 권한을 할당하는 보안 주체를 제거합니다.

  - **Remove-ADPermission** cmdlet을 사용하여 송신 커넥터에 대해 구성된 보안 주체 중 하나에서 **Ms-Exch-Send-Headers-Organization** 사용 권한, **Ms-Exch-Send-Headers-Forest** 사용 권한 및 **Ms-Exch-Send-Headers-Routing** 사용 권한을 제거합니다.

  - **Add-ADPermission** cmdlet을 사용하여 송신 커넥터에 대해 구성된 보안 주체 중 하나에 대한 **Ms-Exch-Send-Headers-Organization** 사용 권한, **Ms-Exch-Send-Headers-Forest** 사용 권한 및 **Ms-Exch-Send-Headers-Routing** 사용 권한을 거부합니다.

자세한 내용은 다음 항목을 참조하십시오.

  - [송신 커넥터](send-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/ko-kr/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/ko-kr/library/aa996048\(v=exchg.150\))

맨 위로 이동

## 다른 메시지 원본의 헤더 방화벽

송신 커넥터 또는 수신 커넥터를 사용하지 않고 메시지가 사서함 서버 또는 Edge 전송 서버의 전송 파이프라인에 들어갈 수 있습니다. 헤더 방화벽은 다음 목록에 설명된 대로 다음과 같은 다른 메시지 원본에 적용됩니다.

  - **Pickup 디렉터리 및 Replay 디렉터리**   Pickup 디렉터리는 관리자 또는 응용 프로그램에서 메시지를 전송하는 데 사용됩니다. Replay 디렉터리는 Exchange 메시지 큐에서 내보낸 메시지를 다시 전송하는 데 사용됩니다. Pickup 및 Replay 디렉터리에 대한 자세한 내용은 [Pickup 디렉터리 및 Replay 디렉터리](pickup-directory-and-replay-directory-exchange-2013-help.md)를 참조하십시오.
    
    조직 X-헤더, 포리스트 X-헤더 및 라우팅 헤더가 Pickup 디렉터리의 메시지 파일에서 제거됩니다.
    
    라우팅 헤더는 Replay 디렉터리에서 전송된 메시지에 보존됩니다.
    
    조직 X-헤더 및 포리스트 X-헤더가 Replay 디렉터리의 메시지에 보존되는지 이 메시지에서 제거되는지 여부는 메시지 파일의 **X-CreatedBy:**  헤더 필드에 의해 제어됩니다.
    
      - **X-CreatedBy:**  값이 `MSExchange15`일 경우 조직 X-헤더 및 포리스트 X-헤더는 메시지에 보존됩니다.
    
      - **X-CreatedBy:**  값이 `MSExchange15`가 아닐 경우 조직 X-헤더 및 포리스트 X-헤더는 메시지에서 제거됩니다.
    
      - 메시지 파일에 **X-CreatedBy:**  헤더 필드가 없는 경우 조직 X-헤더 및 포리스트 X-헤더는 메시지에서 제거됩니다.

  - **Drop 디렉터리**   Drop 디렉터리는 사서함 서버의 외부 커넥터에서 SMTP를 사용하여 메시지를 전송하지 않는 메시징 서버에 메시지를 전송하는 데 사용됩니다. 외부 커넥터에 대한 자세한 내용은 [외부 커넥터](foreign-connectors-exchange-2013-help.md)를 참조하십시오.
    
    조직 X-헤더 및 포리스트 X-헤더가 메시지 파일이 Drop 디렉터리에 저장되기 전에 메시지 파일에서 제거됩니다.
    
    라우팅 헤더는 Drop 디렉터리에서 전송된 메시지에 보존됩니다.

  - **사서함 전송**   사서함 서버의 사서함으로 메시지를 보내고 이 사서함에서 메시지를 받기 위해 사서함 서버에는 사서함 전송 서비스가 있습니다. 사서함 전송 서비스에 대한 자세한 내용은 [메일 흐름](mail-flow-exchange-2013-help.md)을 참조하십시오.
    
    조직 X-헤더, 포리스트 X-헤더 및 라우팅 헤더는 사서함 전송 제출 서비스에 의해 사서함에서 전송된 보내는 메시지에서 제거됩니다.
    
    라우팅 헤더는 사서함 전송 배달 서비스에 의해 사서함 받는 사람에게 배달되는 인바운드 메시지에서 보존됩니다. 다음 조직 X-헤더는 사서함 전송 배달 서비스에 의해 사서함 받는 사람에게 배달되는 인바운드 메시지에서 보존됩니다.
    
      - **X-MS-Exchange-Organization-SCL**
    
      - **X-MS-Exchange-Organization-AuthDomain**
    
      - **X-MS-Exchange-Organization-AuthMechanism**
    
      - **X-MS-Exchange-Organization-AuthSource**
    
      - **X-MS-Exchange-Organization-AuthAs**
    
      - **X-MS-Exchange-Organization-OriginalArrivalTime**
    
      - **X-MS-Exchange-Organization-OriginalSize**

  - **DSN 메시지**   조직 X-헤더, 포리스트 X-헤더 및 라우팅 헤더는 DSN 메시지에 첨부된 원본 메시지 헤더나 원본 메시지에서 제거됩니다. DSN 메시지에 대한 자세한 내용은 [Exchange 2013의 Dsn 및 Ndr](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md)을 참조하십시오.

  - **전송 에이전트 제출**   조직 X-헤더, 포리스트 X-헤더 및 라우팅 헤더는 전송 에이전트에서 제출한 메시지에 보존됩니다.

맨 위로 이동

## Exchange의 조직 X-헤더 및 포리스트 X-헤더

사서함 서버나 Edge 전송 서버의 전송 서비스는 메시지 헤더에 사용자 지정 X-헤더 필드를 삽입합니다.

조직 X-헤더는 **X-MS-Exchange-Organization-**으로 시작합니다. 포리스트 X-헤더는 **X-MS-Exchange-Forest-**로 시작합니다. 다음 표에서는 Exchange 조직의 메시지에 사용되는 몇 가지 조직 X-헤더 및 포리스트 X-헤더에 대해 설명합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>X-헤더</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Forest-RulesExecuted</strong></p></td>
<td><p>메시지에 대해 작동한 전송 규칙입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-Antispam-Report</strong></p></td>
<td><p>콘텐츠 필터 에이전트에 의해 메시지에 적용된 스팸 방지 필터 결과에 대한 요약입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthAs</strong></p></td>
<td><p>인증 원본을 지정합니다. 이 X-헤더는 메시지 보안을 평가한 경우 항상 표시됩니다. 가능한 값은 <code>Anonymous</code>, <code>Internal</code>, <code>External</code> 또는 <code>Partner</code>입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthDomain</strong></p></td>
<td><p>도메인 보안 인증 동안 채워집니다. 이 값은 원격 인증 도메인의 FQDN입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthMechanism</strong></p></td>
<td><p>메시지 전송을 위한 인증 메커니즘을 지정합니다. 값은 2자리 16진수입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthSource</strong></p></td>
<td><p>조직 대신 메시지 인증을 평가한 서버 컴퓨터의 FQDN을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Journal-Report</strong></p></td>
<td><p>전송 시 저널 보고서를 식별합니다. 메시지가 전송 서비스를 떠나는 즉시 헤더는 <strong>X-MS-Journal-Report</strong>가 됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalArrivalTime</strong></p></td>
<td><p>메시지가 처음으로 Exchange 조직에 들어온 시간을 식별합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Sender</strong></p></td>
<td><p>격리된 메시지가 처음으로 Exchange 조직에 들어왔을 때 해당 메시지의 원래 보낸 사람을 식별합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalSize</strong></p></td>
<td><p>격리된 메시지가 처음으로 Exchange 조직에 들어왔을 때 해당 메시지의 원래 크기를 식별합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Scl</strong></p></td>
<td><p>격리된 메시지가 처음으로 Exchange 조직에 들어왔을 때 해당 메시지의 원래 SCL을 식별합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-PCL</strong></p></td>
<td><p>피싱 지수를 식별합니다. 가능한 피싱 지수 값은 1~8이며 값이 클수록 의심스러운 메시지를 나타냅니다. 자세한 내용은 <a href="anti-spam-stamps-exchange-2013-help.md">스팸 방지 스탬프</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Quarantine</strong></p></td>
<td><p>메시지가 스팸 격리 사서함에 격리되었고 DSN(배달 상태 알림)이 전송되었음을 표시합니다. 또는 메시지가 관리자에 의해 격리되었다가 해제되었음을 표시합니다. 이 X-헤더 필드는 해제된 메시지가 스팸 격리 사서함에 다시 전송되지 않도록 합니다. 자세한 내용은 <a href="release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md">릴리스 스팸 격리 사서함에서 메시지를 격리</a>을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-SCL</strong></p></td>
<td><p>메시지의 SCL을 식별합니다. 가능한 SCL 값은 0~9이며 값이 클수록 의심스러운 메시지를 나타냅니다. 특수한 값 -1은 해당 메시지를 콘텐츠 필터 에이전트의 처리에서 제외시킵니다. 자세한 내용은 <a href="content-filtering-exchange-2013-help.md">콘텐츠 필터링</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-SenderIdResult</strong></p></td>
<td><p>보낸 사람 ID 에이전트의 결과를 포함합니다. 보낸 사람 ID 에이전트는 SPF(Sender Policy Framework)를 사용하여 메시지 원본 IP 주소를 보낸 사람의 전자 메일 주소에서 사용된 도메인과 비교합니다. 보낸 사람 ID 결과는 메시지의 SCL을 계산하는 데 사용됩니다. 자세한 내용은 <a href="sender-id-exchange-2013-help.md">보낸사람 ID</a>를 참조하십시오.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

