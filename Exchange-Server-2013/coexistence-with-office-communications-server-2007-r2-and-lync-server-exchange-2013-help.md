---
title: 'Office Communications Server 2007 R2 및 Lync Server와 동시 사용: Exchange 2013 Help'
TOCTitle: Office Communications Server 2007 R2 및 Lync Server와 동시 사용
ms:assetid: f12d65c7-0b2c-46a1-a14a-802a76296fa1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ851069(v=EXCHG.150)
ms:contentKeyID: 50556102
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Office Communications Server 2007 R2 및 Lync Server와 동시 사용

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2015-03-09_

Communications Server 2007 R2 및 Lync Server에는 IM (인스턴트 메시징)을 포함 하 여 다양 한 최종 사용자 기능을, 현재 상태, 단체 IM 및 해당 음성 메일 기능 통합 될 수 있는 Exchange UM (통합 메시징)를 제공 합니다. Lync Server 2010 또는 2013을 통합 하는 배포의 경우 사용자가 음성 메일 액세스 Lync Server 구성 요소를 사용 하 여 음성 메일에 대해 사용할 수 있는 사용자를 사용할 수 있는 Enterprise Voice에 대해 사용할 수 있습니다.

이전 버전의 Office Communications Server 또는 Lync Server와 UM을 통합 하는 경우 일부 기능을 사용할 수 있습니다. 고해상도 사진, 통합된 연락처 저장소 Lync 보관 통합 등 새로운 향상 된 최종 사용자 기능을 최대한 활용 하려면 사용자에 대 한 Lync Server 2013 및 Exchange Server 2013 사용자 계정을 있어야 하며 Lync 2013 클라이언트 소프트웨어의 최신 버전을 사용 해야 합니다. 예, 통합된 연락처 저장소는 Lync Server 2010에 Enterprise Voice에 대해 활성화 된 했을 때 사용자에 게 제공 되지 않습니다. 또한 고해상도 사진 Lync 2010에 표시할 수 없습니다.

Lync Server 2010 또는 Office Communications Server 2007 r 2와 Exchange UM 통합 하는 경우 조직에 배포 된 Office Communications Server 2007 R2 또는 Lync 2010 서버에는 추가 핫픽스가, 롤업, 누적 업데이트 및 서비스 팩을 설치 해야 합니다. 설치 시 필요한 자신이 기능 배포 토폴로지 및 Exchange UM과 통합 하는 제품 버전에 따라 다릅니다.

## 필수 핫픽스, 롤업, 누적 업데이트 및 서비스 팩

다음 표에서 필요한 UM과의 통합에 대 한 제품의 각 버전에 대 한 픽스를 보여줍니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>Office 누적 업데이트 10 이상 Communications Server 2007 r 2입니다.</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>Lync Server 2010 누적 업데이트 3 이상입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>없음 업데이트가 필요 합니다.</p></td>
</tr>
</tbody>
</table>

