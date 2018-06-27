---
title: 'Active Directory 사이트간 메일 라우팅: Exchange 2013 Help'
TOCTitle: Active Directory 사이트간 메일 라우팅
ms:assetid: 86b423e3-7bec-4430-9a5a-4f84ce9d82ea
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ916681(v=EXCHG.150)
ms:contentKeyID: 52058096
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory 사이트간 메일 라우팅

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Active Directory 사이트는 네트워크의 물리적 측면을 기반으로 하는 논리적 구성 요소입니다. Active Directory 사이트를 만드는 주요 목적은 네트워크에서 Active Directory 복제 트래픽을 최적으로 제어할 수 있는 방식으로 연결되어 있는 서브넷을 정의하기 위한 것입니다. Microsoft Exchange Server 2013은 DAG(데이터베이스 사용 가능 그룹) 및 Active Directory 사이트를 라우팅 경계로 인식하며, Exchange 2013 서버는 Active Directory 사이트 토폴로지를 기반으로 라우팅 결정을 내립니다.

기본적으로 Active Directory 포리스트에는 하나의 Active Directory 사이트만 포함됩니다. 이 Active Directory 사이트의 기본 이름은 `Default-First-Site-Name`입니다. 그 이외의 다른 Active Directory 사이트는 만들어지지 않은 경우 포리스트의 모든 도메인 구성원 컴퓨터가 `Default-First-Site-Name`의 구성원이 됩니다. 따라서 서브넷과 사이트 간 연결을 구성할 필요가 없습니다. Active Directory 사이트를 추가로 만드는 경우에는 해당 Active Directory 사이트에 할당되는 서브넷을 지정해야 합니다.

**목차**

Determining site membership

IP site links

Controlling IP site link costs

Implementing hub sites

Topology discovery

## 사이트 구성원 자격 확인

각 Active Directory 사이트는 하나 이상의 IP 서브넷에 연결됩니다. 관리자는 도메인 컨트롤러 및 글로벌 카탈로그 서버로 구성된 컴퓨터에 Active Directory 사이트 구성원 자격을 할당합니다. Exchange 서버 등의 다른 도메인 구성원 컴퓨터는 Active Directory 사이트에 연결된 IP 서브넷에 있는 IP 주소를 사용하도록 구성될 때 자동으로 Active Directory 사이트 구성원 자격을 할당받습니다. 동일한 Active Directory 사이트 구성원 자격이 있는 컴퓨터의 경우 네트워크에 제대로 연결된 것으로 간주합니다. 서버는 항상 하나의 Active Directory 사이트에 속한 구성원이 됩니다.

응용 프로그램이 설치된 컴퓨터 및 포리스트에 있는 다른 컴퓨터의 Active Directory 사이트 구성원 자격을 확인할 수 있고, 해당 정보를 사용하여 통신 흐름을 제어할 수 있는 경우 이 응용 프로그램을 사이트 인식 응용 프로그램이라고 합니다. 사이트 인식 응용 프로그램이 도메인 컨트롤러나 글로벌 카탈로그 서버 등 다른 서버의 서비스를 사용해야 하는 경우 해당 서비스를 요청하는 컴퓨터와 동일한 Active Directory 구성원 자격이 있는 서버에 우선 순위가 주어집니다.

Exchange 2013은 사이트 인식 응용 프로그램이며 다른 Exchange 2013 컴퓨터에서 실행되는 서비스와의 통신 및 메시지 라우팅에 Active Directory 토폴로지를 사용합니다. Active Directory 사이트는 라우팅 경계일 뿐 아니라 서비스 검색 경계이기도 합니다.

도메인 구성원 컴퓨터에 대한 사이트 구성원 자격을 결정하는 작업은 로컬 IP 주소를 정의된 서브넷과 비교한 다음 적절한 사이트 구성원 자격 연결을 결정하는 일련의 DNS 쿼리에 따라 달라집니다. DNS 쿼리와 연관된 오버헤드를 줄이기 위해 Exchange 2013 Active Directory 스키마 추가 사항에는 Exchange 서버 개체에 대한 **msExchServerSite** 특성이 포함되어 있습니다. 이 특성의 값은 Exchange 서버의 Active Directory 사이트 고유 이름입니다. 이 특성은 각 Exchange 서버 개체의 속성입니다. 사이트 구성원 자격 선호도가 서버 개체의 특성으로 저장될 때 DNS 쿼리를 사용하는 대신 현재 토폴로지를 Active Directory에서 직접 읽을 수 있으며, 가입된 Edge 전송 서버와 같은 비도메인 컴퓨터에 대해 사이트 구성원 자격 연결을 사용할 수 있습니다.

**msExchServerSite** 특성의 값은 Microsoft Exchange Active Directory 토폴로지 서비스에 의해 사용되고 최신 상태로 유지됩니다. Windows 기반 컴퓨터가 시작되면 네트워크 로그온 서비스가 해당 컴퓨터의 사이트 구성원 자격을 확인합니다. 네트워크 로그온 서비스는 해당 정보를 사용하여 로컬 컴퓨터와 동일한 Active Directory 사이트에 있는 도메인 컨트롤러를 찾은 다음 해당 서버에 대해 권한 부여 및 인증 요청을 지시합니다. Microsoft Exchange Active Directory 토폴로지 서비스는 **DsGetSiteName** API 호출을 사용하여 Net Logon 서비스에서 사이트 구성원 자격 값을 검색하고 Active Directory 사이트의 고유 이름을 Active Directory에 있는 Exchange 서버 개체의 **msExchServerSite** 특성에 씁니다.

다음 표에서는 조직에서 Active Directory 사이트를 정의하는 방법을 보여줍니다. 이 예에서는 세 개의 Active Directory 사이트를 정의하며 각 Active Directory 사이트는 둘 이상의 IP 서브넷에 연결되어 있습니다.

**Active Directory 사이트와 서브넷 간 연결 예**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Active Directory 사이트 이름</th>
<th>연결된 IP 서브넷</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>사이트 A</p></td>
<td><p>192.168.1.0/24</p>
<p>192.168.2.0/24</p></td>
</tr>
<tr class="even">
<td><p>사이트 B</p></td>
<td><p>192.168.3.0/24</p>
<p>192.168.4.0/24</p></td>
</tr>
<tr class="odd">
<td><p>사이트 C</p></td>
<td><p>192.168.5.0/24</p>
<p>192.168.6.0/24</p></td>
</tr>
</tbody>
</table>


Mailbox01 서버의 IP 주소가 192.168.1.1인 경우 이 서버는 사이트 A의 구성원입니다. 서버의 IP 주소를 변경하면 사이트 구성원 자격도 변경할 수 있습니다. Mailbox01의 IP 주소를192.168.2.1로 변경해도 해당 서버의 Active Directory 사이트 구성원 자격은 변경되지 않습니다. 해당 서브넷은 사이트 A에도 연결되어 있기 때문입니다. 그러나 서버를 이동하여 IP 주소가 192.168.3.1로 변경된 경우 해당 서버는 사이트 B의 구성원으로 간주됩니다.

서브넷 연결을 Active Directory 사이트로 변경하는 경우에도 사이트 구성원 자격이 변경될 수 있습니다. 예를 들어, 서브넷 192.168.3.0을 사이트 B와의 연결에서 제거하고 사이트 A에 연결하면 IP 주소가 192.168.3.1인 서버의 사이트 구성원 자격도 사이트 A로 변경됩니다. 사이트 구성원 자격이 변경될 때마다 Exchange는 구성 데이터를 업데이트하여 Exchange에서 라우팅 결정을 내릴 때 변경 내용이 반영되도록 해야 합니다. Active Directory 사이트 구성원 자격이 변경되고 토폴로지 변경 내용이 완전히 전파되는 사이에 약간의 대기 시간이 발생합니다.

맨 위로 이동

## IP 사이트 링크

사이트 링크는 Active Directory 사이트 간의 논리 경로입니다. 사이트 링크 개체는 동일한 비용으로 통신할 수 있는 사이트 집합을 나타냅니다. 사이트 링크는 실제 네트워크에서 네트워크 패킷이 이동하는 실제 경로에 해당하지 않습니다. 그러나 관리자가 사이트 링크에 할당하는 비용은 대개 기본 네트워크 안정성, 속도 및 사용 가능한 대역폭과 관련되어 있습니다. 예를 들어, Active Directory 관리자는 속도가 100Mbps(메가비트/초)인 네트워크 연결에 대해 속도가 10Mbps인 네트워크 연결보다 낮은 비용을 할당할 수도 있습니다.

기본적으로 모든 사이트 링크는 전이적입니다. 즉, 사이트 A에 사이트 B에 대한 링크가 있고 사이트 B에는 사이트 C에 대한 링크가 있는 경우 사이트 A는 사이트 C에 전이적으로 연결되어 있습니다. 사이트 A와 사이트 C 간의 전이적 링크를 *사이트 링크 브리지*라고도 합니다.

Exchange에서는 IP 사이트 링크만 사용하여 Active Directory 사이트 라우팅 토폴로지를 결정합니다. IP 사이트 링크에 할당되는 비용은 라우팅 테이블을 계산할 때 Exchange의 라우팅 구성 요소에 의해 고려됩니다. 이러한 비용은 메시지를 최종적으로 배달할 대상에 대한 최저 비용 라우팅 경로를 계산하는 데 사용됩니다.

모든 Active Directory 사이트는 하나 이상의 IP 사이트 링크와 연결되어야 합니다. 단일 기본 IP 사이트 링크의 이름은 `DEFAULTIPSITELINK`입니다. Active Directory 사이트를 만들 때는 해당 사이트를 IP 사이트 링크에 연결해야 합니다. IP 사이트 링크를 추가로 만들어 원하는 토폴로지를 구현하거나 모든 Active Directory 사이트를 `DEFAULTIPSITELINK`에 연결할 수 있습니다. IP 사이트 링크에 속하는 각 Active Directory 사이트는 동일한 비용으로 해당 링크에 있는 다른 모든 사이트와 직접 통신할 수 있습니다.

다음 그림에서는 포리스트에 네 개의 Active Directory 사이트가 구성되어 있습니다. 각 사이트는 `DEFAULTIPSITELINK`에 연결되어 있습니다. 따라서 각 Active Directory 사이트는 동일한 비용 메트릭을 사용하여 다른 모든 사이트와 직접 통신합니다. 여러 통신 경로가 표시되어 있지만 IP 사이트 링크는 하나만 정의되어 있습니다.

**단일 IP 사이트 링크를 사용하는 풀 메시 토폴로지**

![단일 IP 사이트 링크를 사용한 풀 메시 토폴로지](images/JJ916681.af38d41d-e768-4221-ab4b-b782aa388b73(EXCHG.150).gif "단일 IP 사이트 링크를 사용한 풀 메시 토폴로지")

다음 그림에서는 포리스트에 네 개의 Active Directory 사이트가 구성되어 있습니다. 그러나 이 토폴로지의 경우 관리자가 Active Directory 사이트의 *허브 및 스포크 토폴로지*를 만들도록 IP 사이트 링크를 구성했습니다. 각 스포크 사이트는 중앙 사이트와 직접 통신할 수 있으며 전이적 IP 사이트 링크를 사용하여 서로 통신할 수 있습니다.

**Active Directory IP 사이트 링크의 허브 및 스포크 토폴로지**

![IP 사이트 링크의 허브 및 스포크 토폴로지](images/JJ916681.eca6cd51-8c2e-4996-81ea-070cd9766ef8(EXCHG.150).gif "IP 사이트 링크의 허브 및 스포크 토폴로지")

Exchange는 최저 비용 경로를 결정할 때만 사이트 링크를 사용하고 항상 대상 Exchange 서버로 메시지를 직접 배달하려고 시도한다는 점에 유의해야 합니다. 예를 들어, 위 그림에 나온 토폴로지에서 사이트 B의 사용자가 사이트 C의 다른 사용자에게 메시지를 보내는 경우 사이트 B의 사서함 서버는 사이트 C의 사서함 서버에 직접 연결합니다. 만일 메시지가 사이트 A를 거쳐 가게 하려면 사이트 A를 허브 사이트로 설정해야 합니다. 허브 사이트에 대한 자세한 내용은 이 항목 뒷부분에 있는 "허브 사이트 구현"을 참조하십시오.

Active Directory 관리자는 포리스트의 연결성 및 통신 요구 사항을 가장 효율적으로 나타내는 토폴로지를 구현합니다. Exchange에서도 이러한 토폴로지를 사용하므로 현재 토폴로지가 효율적인 메시지 통신을 지원하는지를 확인해야 합니다.

사이트 링크의 기본 비용은 100이며 유효한 사이트 링크 비용은 1부터 99,999 사이의 숫자입니다. 중복 링크를 지정하는 경우에는 가장 낮은 비용이 할당된 링크가 항상 기본적으로 사용됩니다. Exchange 조직 관리자는 Exchange 관련 비용을 IP 사이트 링크에 할당할 수 있습니다. Exchange 비용이 IP 사이트 링크에 할당되면 Exchange에서 이 비용이 사용됩니다. 그렇지 않은 경우에는 Active Directory 비용이 사용됩니다. IP 사이트 링크에 대해 Exchange 비용을 설정하는 방법에 대한 자세한 내용은 이 항목 뒷부분의 "IP 사이트 링크 비용 제어"를 참조하십시오. Enterprise Administrators 그룹의 구성원인 관리자는 IP 사이트 링크를 추가로 만들 수 있습니다.

Active Directory 사이트 구성에 대 한 자세한 내용은 [사이트 토폴로지 디자인 (영문)](https://go.microsoft.com/fwlink/p/?linkid=33551)을 참조 하십시오.

맨 위로 이동

## IP 사이트 링크 비용 제어

Active Directory IP 사이트 링크 비용은 WAN의 모든 네트워크 연결과 비교한 상대적 네트워크 속도를 기반으로 하며 안정적이고 효율적인 복제 토폴로지를 제공하도록 설계되었습니다. 따라서 대부분의 경우 기존 IP 사이트 링크 비용은 Exchange 메시지 라우팅에 적합해야 합니다. 그러나 기존 Active Directory 사이트 및 IP 사이트 링크 토폴로지를 문서화한 후에 Active Directory IP 사이트 링크 비용과 트래픽 흐름 패턴이 Exchange에 대해 최적 상태가 아니라고 생각되면 Exchange에서 평가한 비용을 조정할 수 있습니다. Active Directory 도구를 사용하여 IP 사이트 링크에 할당된 비용을 변경하면 전체 환경에 영향을 줄 수 있으므로, 대신 Exchange 관리 셸에서 **Set-AdSiteLink** cmdlet을 사용하여 IP 사이트 링크에 Exchange 관련 비용을 할당합니다. 예를 들어 SITELINKAB이라는 IP 사이트에서 Exchange 관련 비용 값을 25를 구성하려면 셸에서 다음 명령을 실행합니다. `Set-AdSiteLink SITELINKAB -ExchangeCost 25`.

Exchange 관련 비용이 IP 사이트 링크에 할당되면 Exchange 비용은 메시지 라우팅에 대한 Active Directory 비용만 다시 정의하며 최저 비용 라우팅 경로를 평가할 때 라우팅에서 Exchange 비용만 고려됩니다.

IP 사이트 링크 비용 조정은 메시지 라우팅 토폴로지가 Active Directory 복제 토폴로지와 달라야 하는 경우에 유용합니다. Exchange 비용은 모든 메시지 경로에서 허브 사이트를 강제 사용하도록 하는 데 사용할 수 있습니다. 또한 Exchange 비용은 Active Directory 사이트에 대한 통신이 실패하는 경우 메시지 대기 위치를 제어하는 데에도 사용할 수 있습니다. 다음 그림에서는 네 개의 사이트를 가진 Active Directory 토폴로지를 보여줍니다.

**IP 사이트 링크에 Exchange 비용이 구성된 토폴로지**

![IP 사이트 링크에 대한 Exchange 비용이 있는 토폴로지](images/JJ916681.56ac2bab-99de-4ddf-b968-80cd34ab8c21(EXCHG.150).gif "IP 사이트 링크에 대한 Exchange 비용이 있는 토폴로지")

위 그림에서 사이트 C와 사이트 D 간의 네트워크 연결은 Active Directory 복제용으로만 사용되며 메시지 라우팅에 사용해서는 안 되는 낮은 대역폭 연결입니다. 그러나 이 링크는 Active Directory IP 사이트 링크 비용으로 인해 다른 Active Directory 사이트에서 사이트 D로의 최저 비용 라우팅 경로에 포함됩니다. 따라서 메시지는 사이트 C의 사이트 D 큐로 배달됩니다. Exchange 관리자는 최저 비용 라우팅 경로에 사이트 B를 대신 포함하여 사이트 D를 사용할 수 없는 경우 메시지가 사이트 B에 대기하도록 설정하고자 합니다. 이때 사이트 C와 사이트 D 간의 IP 사이트 링크에 높은 Exchange 비용을 구성하면 해당 IP 사이트 링크가 사이트 D에 대한 최저 비용 라우팅 경로에 포함되지 않습니다.

Exchange는 Active Directory IP 사이트 링크에 최대 메시지 크기 제한을 구성하기 위한 지원을 제공합니다. 기본적으로 Exchange는 서로 다른 Active Directory 사이트에 있는 Exchange 서버 간에 릴레이되는 메시지에 대해 최대 크기 제한을 적용하지 않습니다. **Set-AdSiteLink** cmdlet을 사용하여 Active Directory IP 사이트 링크에 최대 메시지 크기를 구성하면 라우팅 시 최저 비용 라우팅 경로의 Active Directory 사이트 링크에 구성되어 있는 최대 메시지 크기 제한보다 큰 메시지에 대해서는 배달 못 함 보고서(NDR)가 생성됩니다. 이러한 구성은 대역폭이 낮은 연결을 통해 통신해야 하는 원격 Active Directory 사이트로 보내는 메시지의 크기를 제한하는 데 유용합니다. 자세한 내용은 [메시지 크기 제한](message-size-limits-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 허브 사이트 구현

Exchange 조직에서 모든 메시지 배달이 특정 Active Directory 사이트를 통해 강제로 릴레이되도록 하려고 할 수 있습니다. 셸을 사용하여 Active Directory 사이트를 허브 사이트로 지정할 수 있습니다. 이 작업을 수행하면 더 많은 서버가 메시지 배달에 참여하게 되므로 전체적인 오버헤드가 추가될 수 있습니다. 예를 들어, 사이트 A에서 사이트 E로 메시지를 보낸다고 가정해 봅시다. 최저 비용 라우팅 경로가 사이트 A-사이트 B-사이트 C-사이트 D-사이트 E이고 사이트 C를 허브 사이트로 지정하는 경우 메시지는 사이트 A에서 사이트 C로 릴레이된 다음 사이트 C에서 사이트 E로 릴레이됩니다.

**Set-AdSite** cmdlet을 사용하여 Active Directory 사이트를 허브 사이트로 지정합니다. 허브 사이트가 메시지 배달을 위한 최저 비용 라우팅 경로에 있을 때는 메시지는 최종 대상으로 릴레이되기 전에 허브 사이트의 사서함 서버에 있는 Transport Service에 의해 대기 및 처리됩니다.

최저 비용 라우팅 경로를 선택하면 라우팅 과정에서 허브 사이트가 해당 라우팅 경로에 있는지 확인합니다. 허브 사이트가 구성되어 있는 경우 메시지는 대상 위치로 릴레이되기 전에 허브 사이트의 사서함 서버에서 중지됩니다. 최저 비용 라우팅 경로에 둘 이상의 허브 사이트가 있으면 메시지는 라우팅 경로의 각 허브 사이트에서 중지됩니다.

이 같은 직접 릴레이 라우팅의 변형은 허브 사이트가 최저 비용 라우팅 경로에 있을 때만 유효합니다. 다음 그림에서는 올바른 허브 사이트 사용법을 보여줍니다. 이 다이어그램에서는 사이트 B가 허브 사이트로 구성되어 있습니다. 사이트 A에서 사이트 D로 릴레이되는 메시지는 먼저 사이트 B로 릴레이된 다음 사이트 D로 배달됩니다.

**허브 사이트를 통한 메시지 배달**

![허브 사이트를 사용한 메시지 배달](images/JJ916681.93238bcb-6bbc-4a48-aeb0-09342a421b5b(EXCHG.150).gif "허브 사이트를 사용한 메시지 배달")

다음 그림에서는 IP 사이트 링크 비용이 허브 사이트에 대한 라우팅에 어떤 영향을 미치는지 보여줍니다. 이 시나리오에서는 사이트 B가 허브 사이트로 지정되어 있습니다. 그러나 사이트 B는 다른 사이트 간의 최저 비용 라우팅 경로에 있지 않기 때문에 사이트 A에서 사이트 D로 릴레이된 메시지는 사이트 B를 통해 릴레이되지 않습니다. Active Directory 사이트는 서로 다른 두 사이트 간의 최저 비용 라우팅 경로에 있지 않으면 허브 사이트로 사용되지 않습니다.

**잘못 구성된 허브 사이트**

![잘못 구성된 허브 사이트](images/JJ916681.c010d4d8-5cd3-4b79-b7db-0367ba3cc287(EXCHG.150).gif "잘못 구성된 허브 사이트")

모든 Active Directory 사이트를 허브 사이트로 구성할 수 있습니다. 그러나 이 구성이 제대로 작동하도록 하려면 허브 사이트에 적어도 하나 이상의 사서함 서버가 있어야 합니다.

맨 위로 이동

## 토폴로지 검색

다음과 같은 필수 요소가 있어야 Active Directory 토폴로지를 Exchange에서 사용할 수 있습니다.

  - Microsoft Exchange Active Directory 토폴로지 서비스

  - Microsoft Exchange Transport Service 내의 토폴로지 검색 모듈

Microsoft Exchange Active Directory 토폴로지 서비스는 모든 Exchange 2013 클라이언트 액세스 서버 및 사서함 서버에서 실행됩니다. 이러한 서버는 Microsoft Exchange Active Directory 토폴로지 서비스를 사용하여 Exchange 서버가 Active Directory 데이터를 읽고 쓰는 데 사용할 수 있는 글로벌 카탈로그 서버 및 도메인 컨트롤러를 검색합니다. Exchange 2013은 Exchange에서 Active Directory에 대한 읽기 또는 쓰기 작업을 수행해야 할 때마다 확인된 디렉터리 서버에 바인딩됩니다.

Microsoft Exchange Transport Service의 일부인 토폴로지 검색 모듈은 Active Directory 토폴로지에 대한 정보를 Exchange 서버에 제공합니다. 이 API는 조직에서 Exchange 서버 및 역할을 검색하며 Active Directory 구성 개체에 대한 각 항목의 관계를 결정합니다. 구성 데이터는 Active Directory에서 검색되어 해당 컴퓨터에서 실행 중인 Exchange 서비스에서 액세스할 수 있도록 캐시됩니다.

토폴로지 검색 모듈은 다음 단계를 수행하여 Exchange 라우팅 토폴로지를 생성합니다.

1.  Active Directory에서 데이터를 읽습니다. 다음 개체가 모두 검색됩니다.
    
      - Active Directory 사이트
    
      - IP 사이트 링크
    
      - 모든 Exchange 서버

2.  1단계에서 검색된 데이터는 초기 토폴로지를 만들고 관련 구성 개체를 연결 및 매핑하는 데 사용됩니다.

3.  Active Directory에 저장된 Exchange 서버 개체에서 사이트 특성 값을 검색하여 Exchange 서버를 Active Directory 사이트에 일치시킵니다.

4.  검색된 정보 모음으로 라우팅 테이블을 업데이트합니다.

이 프로세스를 통해 모든 Exchange 2013 서버는 조직의 다른 Exchange 서버를 인식하고 또 각 Exchange 서버 간의 거리가 어느 정도 가까운지 인식할 수 있게 됩니다.

맨 위로 이동

