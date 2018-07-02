---
title: 'Exchange 2013 저장소 구성 옵션: Exchange 2013 Help'
TOCTitle: Exchange 2013 저장소 구성 옵션
ms:assetid: 37cdeacf-74f9-4399-9860-4d1dbec12bb1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee832792(v=EXCHG.150)
ms:contentKeyID: 50482858
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 저장소 구성 옵션

 

_**적용 대상:** Exchange Online, Exchange Server, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013의 사서함 서버 역할에 대한 저장 옵션 및 요구 사항을 이해하는 것은 사서함 서버 저장소 설계 솔루션에 있어서 중요합니다.

**목차**

Storage architectures

Physical disk types

Best practices for supported storage configurations

## 저장소 아키텍처

다음 표에서는 지원되는 저장소 아키텍처에 대해 설명하고 각 저장소 아키텍처 유형에 대한 모범 사례 지침(해당되는 경우)을 제공합니다.

### 지원되는 저장소 아키텍처

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>저장소 아키텍처</th>
<th>설명</th>
<th>모범 사례</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DAS(직접 연결 저장소)</p></td>
<td><p>DAS는 서버 또는 워크스테이션에 직접 연결된 디지털 저장소 시스템으로, 사이에 저장소 네트워크가 필요하지 않습니다. 예를 들어, DAS 전송에는 SAS(Serial Attached SCSI) 및 Serial Attached ATA(Advanced Technology Attachment)가 포함됩니다.</p></td>
<td><p>사용할 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>SAN(저장 영역 네트워크): iSCSI(Internet Small Computer System Interface)</p></td>
<td><p>SAN은 장치가 운영 체제에 로컬 연결된 것으로 나타나는 방식(예: 블록 저장소)으로 원격 컴퓨터 저장소 장치(예: 디스크 배열 및 테이프 라이브러리)를 서버에 연결하는 아키텍처입니다. iSCSI SAN은 IP 패킷 내에 SCSI 명령을 캡슐화하고 표준 네트워킹 인프라를 저장소 전송으로 사용합니다(예: 이더넷).</p></td>
<td><p>Exchange 데이터를 백업하는 실제 디스크를 다른 응용 프로그램과 공유하지 않습니다.</p>
<p>전용 저장소 네트워크를 사용합니다.</p>
<p>독립 실행형 구성에 대해 여러 네트워크 경로를 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>SAN: 파이버 채널</p></td>
<td><p>파이버 채널 SAN은 파이버 채널 패킷 내에 SCSI 명령을 캡슐화하고 일반적으로 특수 파이버 채널 네트워크를 저장소 전송으로 사용합니다.</p></td>
<td><p>Exchange 데이터를 백업하는 실제 디스크를 다른 응용 프로그램과 공유하지 않습니다.</p>
<p>독립 실행형 구성에 대해 여러 개의 파이버 채널 네트워크 경로를 사용합니다.</p>
<p>FC HBA(호스트 버스 어댑터) 조정(예: 큐 크기 및 큐 대상)에 대한 저장소 공급업체의 모범 사례에 따릅니다.</p></td>
</tr>
</tbody>
</table>


NAS(Network Attached Storage) 장치는 네트워크에 있는 다른 장치에 파일 기반 데이터 저장소 서비스를 제공하기 위한 목적으로 네트워크에 연결된 자체 포함 컴퓨터입니다. NAS 장치의 운영 체제 및 기타 소프트웨어는 데이터 저장소, 파일 시스템 및 파일 액세스 기능과 이러한 기능의 관리(예: 파일 저장소) 기능을 제공합니다.

Exchange 2013에서는 [Exchange 2013 가상화](exchange-2013-virtualization-exchange-2013-help.md) 항목에 나오는 SMB 3.0 시나리오가 아닌 이상 NAS 볼륨의 사용을 지원하지 않으므로 Exchange에서 Exchange 데이터를 저장하는 데 사용하는 모든 저장소는 블록 수준 저장소여야 합니다. 또한 가상화된 환경에서는 하이퍼바이저를 통해 게스트에게 블록 수준 저장소로 제공되는 NAS 저장소는 지원되지 않습니다.

저장소 계층을 사용 하 여 권장 되지 않습니다, 시스템 성능을 저하 시킬 수 있습니다. 이러한 이유로 자동으로 "속도" 저장소로 가장 액세스 한 파일을 이동 하는 저장소 컨트롤러를 허용 하지 않습니다.

맨 위로 이동

## 실제 디스크 유형

다음 표에서는 지원되는 실제 디스크 유형 목록과 각 실제 디스크 유형에 대한 모범 사례 지침(해당되는 경우)을 제공합니다.

### 지원되는 실제 디스크 유형

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>실제 디스크 유형</th>
<th>설명</th>
<th>지원됨 또는 모범 사례</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SATA(Serial ATA)</p></td>
<td><p>SATA는 ATA 및 IDE(Integrated Device Electronics) 디스크를 위한 직렬 인터페이스입니다. SATA 디스크는 다양한 폼 요소, 속도 및 용량으로 제공됩니다.</p>
<p>일반적으로 다음과 같은 설계 요구 사항이 있을 경우 Exchange 2013 사서함 저장소에 대해 SATA 디스크를 선택합니다.</p>
<ul>
<li><p>대용량</p></li>
<li><p>보통 수준의 성능</p></li>
<li><p>보통 수준의 전원 사용률</p></li>
</ul></td>
<td><p>지원:  Windows Server 2008 및 Windows Server 2008 R2의 경우 512바이트 섹터 디스크. 다음 구성 요소가 포함된 Windows Server 2008 R2의 경우 512e 디스크가 지원됩니다.</p>
<ul>
<li><p>핫픽스는 <a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 기술 자료 문서 982018</a>에서 설명되어 있으며 고급 포맷 디스크와 Windows 7 및 Windows Server 2008 R2와의 호환성을 개선한 업데이트를 사용할 수 있습니다.</p></li>
<li><p>서비스 팩 1(SP1)을 포함한 Windows Server 2008 R2 및 Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 이상에서는 전용 4KB 섹터 디스크 및 512e 디스크가 지원됩니다. 지원을 위해서는 모든 데이터베이스 복사본이 동일한 실제 디스크 유형에 있어야 합니다. 예를 들어, 512바이트 섹터 디스크에 주어진 데이터베이스의 복제본 하나와 512e 디스크의 또는 4K 디스크의 동일한 데이터베이스에 있는 또 다른 복제본을 호스팅하는 것은 지원되지 않는 구성입니다.</p>
<p>모범 사례: 일반적으로 열, 진동 및 신뢰성 특징을 가진 엔터프라이즈급 SATA 디스크가 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>Serial Attached SCSI</p></td>
<td><p>Serial Attached SCSI는 SCSI 디스크를 위한 직렬 인터페이스입니다. Serial Attached SAS 디스크는 다양한 폼 요소, 속도 및 용량으로 제공됩니다.</p>
<p>일반적으로 다음과 같은 설계 요구 사항이 있을 경우 Exchange 2013 사서함 저장소에 대해 Serial Attached SAS 디스크를 선택합니다.</p>
<ul>
<li><p>보통 수준의 용량</p></li>
<li><p>고성능</p></li>
<li><p>보통 수준의 전원 사용률</p></li>
</ul></td>
<td><p>지원:  Windows Server 2008 및 Windows Server 2008 R2의 경우 512바이트 섹터 디스크. 다음 구성 요소가 포함된 Windows Server 2008 R2의 경우 512e 디스크가 지원됩니다.</p>
<ul>
<li><p>핫픽스는 <a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 기술 자료 문서 982018</a>에서 설명되어 있으며 고급 포맷 디스크와 Windows 7 및 Windows Server 2008 R2와의 호환성을 개선한 업데이트를 사용할 수 있습니다.</p></li>
<li><p>서비스 팩 1(SP1)을 포함한 Windows Server 2008 R2 및 Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 이상에서는 전용 4KB 섹터 디스크 및 512e 디스크가 지원됩니다. 지원을 위해서는 모든 데이터베이스 복사본이 동일한 실제 디스크 유형에 있어야 합니다. 예를 들어, 512바이트 섹터 디스크에 주어진 데이터베이스의 복제본 하나와 512e 디스크의 또는 4K 디스크의 동일한 데이터베이스에 있는 또 다른 복제본을 호스팅하는 것은 지원되지 않는 구성입니다.</p>
<p>모범 사례: UPS 없이 사용할 경우 실제 디스크 쓰기 캐싱을 사용하지 않도록 설정해야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>파이버 채널</p></td>
<td><p>파이버 채널은 디스크를 파이버 채널 기반 SAN에 연결하는 데 사용되는 전기 인터페이스입니다. 파이버 채널 디스크는 다양한 속도 및 용량으로 제공됩니다.</p>
<p>일반적으로 다음과 같은 설계 요구 사항이 있을 경우 Exchange 2013 사서함 저장소에 대해 파이버 채널 디스크를 선택합니다.</p>
<ul>
<li><p>보통 수준의 용량</p></li>
<li><p>고성능</p></li>
<li><p>SAN 연결</p></li>
</ul></td>
<td><p>지원:  Windows Server 2008 및 Windows Server 2008 R2의 경우 512바이트 섹터 디스크. 다음 구성 요소가 포함된 Windows Server 2008 R2의 경우 512e 디스크가 지원됩니다.</p>
<ul>
<li><p>핫픽스는 <a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 기술 자료 문서 982018</a>에서 설명되어 있으며 고급 포맷 디스크와 Windows 7 및 Windows Server 2008 R2와의 호환성을 개선한 업데이트를 사용할 수 있습니다.</p></li>
<li><p>서비스 팩 1(SP1)을 포함한 Windows Server 2008 R2 및 Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 이상에서는 전용 4KB 섹터 디스크 및 512e 디스크가 지원됩니다. 지원을 위해서는 모든 데이터베이스 복사본이 동일한 실제 디스크 유형에 있어야 합니다. 예를 들어, 512바이트 섹터 디스크에 주어진 데이터베이스의 복제본 하나와 512e 디스크의 또는 4K 디스크의 동일한 데이터베이스에 있는 또 다른 복제본을 호스팅하는 것은 지원되지 않는 구성입니다.</p>
<p>모범 사례: UPS 없이 사용할 경우 실제 디스크 쓰기 캐싱을 사용하지 않도록 설정해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>SSD(반도체 드라이브)(플래시 디스크)</p></td>
<td><p>SSD는 고체 메모리를 사용하여 지속적 데이터를 저장하는 데이터 저장소 장치입니다. SSD는 하드 디스크 드라이브 인터페이스를 에뮬레이트합니다. SSD 디스크는 다양한 속도(여러 I/O 성능 기능) 및 용량으로 제공됩니다.</p>
<p>일반적으로 다음과 같은 설계 요구 사항이 있을 경우 Exchange 2013 사서함 저장소에 대해 SSD 디스크를 선택합니다.</p>
<ul>
<li><p>저용량</p></li>
<li><p>매우 우수한 성능</p></li>
</ul></td>
<td><p>지원:  Windows Server 2008 및 Windows Server 2008 R2의 경우 512바이트 섹터 디스크. 다음 구성 요소가 포함된 Windows Server 2008 R2의 경우 512e 디스크가 지원됩니다.</p>
<ul>
<li><p>핫픽스는 <a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 기술 자료 문서 982018</a>에서 설명되어 있으며 고급 포맷 디스크와 Windows 7 및 Windows Server 2008 R2와의 호환성을 개선한 업데이트를 사용할 수 있습니다.</p></li>
<li><p>서비스 팩 1(SP1)을 포함한 Windows Server 2008 R2 및 Exchange Server 2010 SP1.</p></li>
</ul>
<p>Exchange 2013 이상에서는 전용 4KB 섹터 디스크 및 512e 디스크가 지원됩니다. 지원을 위해서는 모든 데이터베이스 복사본이 동일한 실제 디스크 유형에 있어야 합니다. 예를 들어, 512바이트 섹터 디스크에 주어진 데이터베이스의 복제본 하나와 512e 디스크의 또는 4K 디스크의 동일한 데이터베이스에 있는 또 다른 복제본을 호스팅하는 것은 지원되지 않는 구성입니다.</p>
<p>모범 사례: UPS 없이 사용할 경우 실제 디스크 쓰기 캐싱을 사용하지 않도록 설정해야 합니다.</p>
<p>일반적으로 Exchange 2013 사서함 서버에는 SSD 저장소의 성능 특성이 필요하지 않습니다.</p></td>
</tr>
</tbody>
</table>


## 디스크 유형을 선택할 때 고려할 요소

Exchange 2013 저장소의 디스크 유형을 선택할 때는 여러 가지 사항을 고려해야 합니다. 적절한 디스크는 성능(순차적 및 임의 성능 모두)과 용량, 안정성, 전원 사용률 및 자본 비용 사이의 균형이 맞는 디스크입니다. 지원되는 실제 디스크 유형에 대한 다음 표에서는 이러한 요소를 고려할 때 도움이 되는 정보를 제공합니다.

성능에서 측면에 Exchange 저장소는에 대 한 대규모, 속도가 느린 디스크를 사용 하 여 디스크 수를 평균 읽기를 유지 관리 하 고 쓰기 20ms의 대기 시간을 제공 또는 부하가 줄어듭니다.

### 디스크 유형 선택 요소

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>디스크 속도(RPM)</th>
<th>디스크 폼 요소</th>
<th>인터페이스 또는 전송</th>
<th>용량</th>
<th>임의 I/O 성능</th>
<th>순차적 I/O 성능</th>
<th>전원 사용률</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5,400</p></td>
<td><p>2.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>보통</p></td>
<td><p>나쁨</p></td>
<td><p>나쁨</p></td>
<td><p>좋음</p></td>
</tr>
<tr class="even">
<td><p>5,400</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>좋음</p></td>
<td><p>나쁨</p></td>
<td><p>나쁨</p></td>
<td><p>보통 이상</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>2.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>보통</p></td>
<td><p>보통</p></td>
<td><p>보통</p></td>
<td><p>좋음</p></td>
</tr>
<tr class="even">
<td><p>7,200</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>보통</p></td>
<td><p>보통</p></td>
<td><p>보통 이상</p></td>
<td><p>좋음</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>좋음</p></td>
<td><p>보통</p></td>
<td><p>보통 이상</p></td>
<td><p>보통 이상</p></td>
</tr>
<tr class="even">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>좋음</p></td>
<td><p>보통</p></td>
<td><p>보통 이상</p></td>
<td><p>보통 이상</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>파이버 채널</p></td>
<td><p>좋음</p></td>
<td><p>보통</p></td>
<td><p>보통 이상</p></td>
<td><p>보통</p></td>
</tr>
<tr class="even">
<td><p>10,000</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>보통 이하</p></td>
<td><p>좋음</p></td>
<td><p>보통 이상</p></td>
<td><p>보통 이상</p></td>
</tr>
<tr class="odd">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>보통</p></td>
<td><p>보통</p></td>
<td><p>보통 이상</p></td>
<td><p>보통 이상</p></td>
</tr>
<tr class="even">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>보통</p></td>
<td><p>보통 이상</p></td>
<td><p>보통 이상</p></td>
<td><p>보통 이하</p></td>
</tr>
<tr class="odd">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>파이버 채널</p></td>
<td><p>보통</p></td>
<td><p>보통 이상</p></td>
<td><p>보통 이상</p></td>
<td><p>보통 이하</p></td>
</tr>
<tr class="even">
<td><p>15,000</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>나쁨</p></td>
<td><p>좋음</p></td>
<td><p>좋음</p></td>
<td><p>보통</p></td>
</tr>
<tr class="odd">
<td><p>15,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>보통</p></td>
<td><p>좋음</p></td>
<td><p>좋음</p></td>
<td><p>보통 이하</p></td>
</tr>
<tr class="even">
<td><p>15,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>파이버 채널</p></td>
<td><p>보통</p></td>
<td><p>좋음</p></td>
<td><p>좋음</p></td>
<td><p>나쁨</p></td>
</tr>
<tr class="odd">
<td><p>SSD: 엔터프라이즈급</p></td>
<td><p>해당 없음</p></td>
<td><p>SATA, Serial Attached SCSI, 파이버 채널</p></td>
<td><p>나쁨</p></td>
<td><p>좋음</p></td>
<td><p>좋음</p></td>
<td><p>좋음</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 지원되는 저장소 구성에 대한 모범 사례

이 섹션에서는 지원되는 디스크 및 배열 컨트롤러 구성에 대한 모범 사례 정보를 제공합니다.

RAID(Redundant Array of Independent Disks)는 여러 디스크 간에 데이터를 스트라이프하여 개별 디스크의 성능 특성을 향상시킬 뿐 아니라 개별 디스크 오류로부터 보호하는 데 종종 사용됩니다. Exchange 2013의 고가용성이 향상되어 RAID는 Exchange 2013 저장소 설계에 있어 필수 구성 요소가 아닙니다. 그러나 RAID는 여전히 독립 실행형 서버와 저장소 내결함성이 필요한 솔루션에 대한 Exchange 2013 저장소 설계의 필수 구성 요소입니다.

**운영 체제, 시스템 또는 페이지 파일 볼륨**

운영 체제, 시스템 또는 페이지 파일 볼륨에 대해 권장되는 구성은 RAID 기술을 사용하여 이 데이터 형식을 보호하는 것입니다. 권장되는 RAID 구성은 RAID-1 또는 RAID-1/0이지만 모든 RAID 유형이 지원됩니다.

**구분된 사서함 데이터베이스 및 로그 볼륨**

독립 실행형 사서함 서버 역할 아키텍처를 배포하는 경우 사서함 데이터베이스 및 로그 볼륨에 RAID 기술이 필요합니다. 사서함 볼륨에 권장되는 RAID 구성은 RAID-1/0(특히 5.4K 또는 7.2K 디스크를 사용 중인 경우)이지만 모든 RAID 유형이 지원됩니다. 로그 볼륨의 경우 RAID-1 또는 RAID-1/0이 권장되는 RAID 구성입니다.

운영 체제, 페이지 파일 또는 Exchange 데이터 볼륨에 RAID-5 또는 RAID-6 구성을 사용하는 경우 다음 사항에 유의합니다.

  - RAID-5 구성(RAID-50, RAID-51 등의 변형 포함)에서는 배열 그룹당 7개 이하의 디스크가 있어야 하며 배열 컨트롤러의 높은 우선 순위 스크러빙 및 영역 검사를 사용하도록 설정해야 합니다.

  - RAID-6 구성에서는 배열 컨트롤러의 높은 우선 순위 스크러빙 및 영역 검사를 사용하도록 설정해야 합니다.

고가용성 데이터베이스 복사본이 세 개 이상 있는 고가용성 아키텍처에서 JBOD가 지원되기는 하지만 로그 볼륨과 사서함 데이터베이스 볼륨이 분리되어 있기 때문에 JBOD는 사용하지 않는 것이 좋습니다.

**사서함 데이터베이스 및 로그 볼륨 배치**

독립 실행형 아키텍처에서는 사서함 데이터베이스 및 로그 볼륨 배치를 사용하지 않는 것이 좋습니다. 고가용성 아키텍처에서는 이 시나리오에 대한 두 가지 가능성이 있습니다.

1.  볼륨당 단일 데이터베이스

2.  볼륨당 여러 개의 데이터베이스

**볼륨당 단일 데이터베이스**

Exchange 관점에서 JBOD는 데이터베이스와 단일 디스크에 저장된 자체 관련 로그를 모두 가지고 있음을 의미합니다. JBOD에서 배포하려면 최소한 세 개의 고가용성 데이터베이스 복사본을 배포해야 합니다. 디스크에 오류가 발생하는 경우 해당 디스크에 있는 데이터베이스 복사본이 손실되기 때문에 단일 디스크 사용은 단일 실패 지점에 해당합니다. 최소한 세 개의 데이터베이스 복사본이 있으면 하나의 복사본(또는 디스크 하나)에 오류가 생기는 경우 두 개의 추가 복사본이 있으므로 내결함성이 보장됩니다. 하지만 세 개의 고가용성 데이터베이스 복사본 배치 및 지연된 데이터베이스 복사본 사용은 저장소 디자인에 영향을 줄 수 있습니다. 다음 표에서는 RAID 또는 JBOD 고려 사항에 대한 지침이 나와 있습니다.

### RAID 또는 JBOD 고려 사항

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>데이터 센터 서버</th>
<th>2개의 고가용성 복사본(합계)</th>
<th>3개의 고가용성 복사본(합계)</th>
<th>데이터 센터당 2~3개의 고가용성 복사본</th>
<th>1개의 지연된 복사본</th>
<th>데이터 센터당 2개 이상의 지연된 복사본</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 데이터 센터 서버</p></td>
<td><p>RAID</p></td>
<td><p>RAID 또는 JBOD(2개의 복사본)</p></td>
<td><p>RAID 또는 JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID 또는 JBOD</p></td>
</tr>
<tr class="even">
<td><p>보조 데이터 센터 서버</p></td>
<td><p>RAID</p></td>
<td><p>RAID(1개의 복사본)</p></td>
<td><p>RAID 또는 JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID 또는 JBOD</p></td>
</tr>
</tbody>
</table>


기본 데이터 센터 서버가 포함된 JBOD에서 배포하려면 DAG 내에 고가용성 데이터베이스 복사본이 세 개 이상 필요합니다. 고가용성 데이터베이스 복사본을 호스팅하는 동일한 서버에서 지연된 복사본을 혼합하는 경우(예: 지연된 전용 데이터베이스 복사본 서버 사용 안 함) 지연된 데이터베이스 복사본이 두 개 이상 필요합니다.

JBOD를 사용하기 위한 보조 데이터 센터 서버의 경우 보조 데이터 센터에 고가용성 데이터베이스 복사본이 두 개 이상 있어야 합니다. 보조 데이터 센터의 복사본이 손실되어도 보조 데이터 센터가 활성화되는 경우 WAN에서 다시 시드를 필요로 하거나 단일 실패 지점을 가지게 되지 않습니다. 고가용성 데이터베이스 복사본을 호스팅하는 동일한 서버에서 지연된 데이터베이스 복사본을 혼합하는 경우(예: 지연된 전용 데이터베이스 복사본 서버 사용 안 함) 지연된 데이터베이스 복사본이 두 개 이상 필요합니다.

지연된 전용 데이터베이스 복사본 서버의 경우 JBOD를 사용하려면 데이터 센터 내에 지연된 데이터베이스 복사본이 두 개 이상 있어야 합니다. 그렇지 않으면 디스크 손실로 인해 지연된 데이터베이스 복사본 손실 및 보호 메커니즘 손실이 발생하게 됩니다.

**볼륨당 여러 개의 데이터베이스**

볼륨당 여러 개의 데이터베이스는 단일 디스크에 활성/수동 복사본(지연된 복사본 포함)이 모두 있을 수 있는 Exchange 2013에서 사용 가능한 새로운 JBOD 시나리오로, 디스크 사용률을 높여줍니다. 하지만 이 방법으로 지연된 복사본을 배포하려면 지연된 복사본 로그 파일 자동 재생을 사용하도록 설정해야 합니다. 다음 표에서는 볼륨당 여러 개의 데이터베이스에 대한 JBOD 고려 사항과 관련 지침이 나와 있습니다.

### JBOD 고려 사항

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>데이터 센터 서버</th>
<th>3개 이상의 복사본(전체)</th>
<th>데이터 센터당 2개 이상의 복사본</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 데이터 센터 서버</p></td>
<td><p>JBOD</p></td>
<td><p>JBOD</p></td>
</tr>
<tr class="even">
<td><p>보조 데이터 센터 서버</p></td>
<td><p>해당 없음</p></td>
<td><p>JBOD</p></td>
</tr>
</tbody>
</table>


다음 표에서는 Exchange 2013의 저장소 배열 구성에 대한 지침을 제공합니다.

### Exchange 2013 사서함 서버 역할에 지원되는 RAID 유형

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>RAID 유형</th>
<th>설명</th>
<th>지원됨 또는 모범 사례</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>디스크 배열 RAID 스트라이프 크기(KB)</p></td>
<td><p>스트라이프 크기는 RAID 세트 내에서의 데이터 분포의 디스크당 단위입니다. 스트라이프 크기는 <em>블록 크기</em>라고도 합니다.</p></td>
<td><p>모범 사례: 256KB 이상. 저장소 공급업체의 모범 사례에 따르십시오.</p></td>
</tr>
<tr class="even">
<td><p>저장소 배열 캐시 설정</p></td>
<td><p>캐시 설정은 배터리가 지원되는 캐싱 배열 컨트롤러에서 제공합니다.</p></td>
<td><p>모범 사례: 100%에서 작성 하 여 DAS 저장소 컨트롤러에 대 한 캐시 (배터리 또는 플래시 백업 캐시) 중 하나를 RAID 또는 JBOD 구성 합니다. 75% 쓰기 캐시를 25% 읽기 다른 유형의 SAN와 같은 저장소 솔루션에 대 한 캐시 (배터리 또는 플래시 백업 캐시). SAN 공급 업체의 해당 플랫폼에서 캐시 구성에 대 한 다른 유용한 있으면 SAN 공급 업체의 지침을 따릅니다.</p></td>
</tr>
<tr class="odd">
<td><p>실제 디스크 쓰기 캐싱</p></td>
<td><p>캐시에 대한 설정은 각각의 개별 디스크에 있습니다.</p></td>
<td><p>지원: UPS 없이 사용할 경우 실제 디스크 쓰기 캐싱을 사용하지 않도록 설정해야 합니다.</p></td>
</tr>
</tbody>
</table>


다음 표에서는 데이터베이스 및 로그 파일 선택에 대한 지침을 제공합니다.

### Exchange 2013 사서함 서버 역할에 대한 데이터베이스 및 로그 파일 선택

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>데이터베이스 및 로그 파일 옵션</th>
<th>설명</th>
<th>독립 실행형: 지원됨 또는 모범 사례</th>
<th>고가용성: 지원됨 또는 모범 사례</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>파일 배치: 데이터베이스/로그 격리</p></td>
<td><p>데이터베이스/로그 격리는 동일한 사서함 데이터베이스의 데이터베이스 파일과 로그를 여러 개의 실제 디스크에서 지원하는 여러 볼륨에 배치하는 것을 의미합니다.</p></td>
<td><p>모범 사례: 복구 기능을 위해 동일한 데이터베이스의 데이터베이스 파일(.edb)과 로그를 여러 개의 실제 디스크가 지원하는 여러 볼륨으로 이동합니다.</p></td>
<td><p>지원: 로그 및 데이터베이스의 격리는 필요하지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>파일 배치: 데이터베이스 파일/볼륨</p></td>
<td><p>데이터베이스 파일/볼륨은 디스크 볼륨 내에서 또는 디스크 볼륨 간에 데이터베이스 파일을 분산하는 방법을 나타냅니다.</p></td>
<td><p>모범 사례: 백업 방법을 기반으로 합니다.</p></td>
<td><p>지원: JBOD를 사용할 때 데이터베이스와 로그 파일용으로 별도의 디렉터리가 포함된 볼륨 하나를 만듭니다.</p></td>
</tr>
<tr class="odd">
<td><p>파일 배치: 로그 스트림/볼륨</p></td>
<td><p>로그 스트림/볼륨은 디스크 볼륨 내에서 또는 디스크 볼륨 간에 데이터베이스 로그 파일을 분산하는 방법을 나타냅니다.</p></td>
<td><p>모범 사례: 백업 방법을 기반으로 합니다.</p></td>
<td><p>지원: JBOD를 사용할 때 데이터베이스와 로그 파일용으로 별도의 디렉터리가 포함된 볼륨 하나를 만듭니다.</p>
<p>모범 사례: JBOD를 사용할 때 볼륨당 여러 데이터베이스를 활용합니다.</p></td>
</tr>
<tr class="even">
<td><p>데이터베이스 크기</p></td>
<td><p>데이터베이스 크기는 디스크 데이터베이스(.edb) 파일 크기를 의미합니다.</p></td>
<td><p>지원: 약 16테라바이트.</p>
<p>모범 사례:</p>
<ul>
<li><p>200GB 이하.</p></li>
<li><p>계산된 최대 데이터베이스 크기의 120%를 프로비전합니다.</p></li>
</ul></td>
<td><p>지원: 약 16테라바이트.</p>
<p>모범 사례:</p>
<ul>
<li><p>2TB 이하.</p></li>
<li><p>계산된 최대 데이터베이스 크기의 120%를 프로비전합니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>로그 자르기 방법</p></td>
<td><p>로그 자르기 방법은 오래된 데이터베이스 로그 파일의 자르기 및 삭제 프로세스입니다. 다음 두 가지 메커니즘이 있습니다.</p>
<ul>
<li><p>Exchange에서 로그를 삭제하는 순환 로깅.</p></li>
<li><p>성공적인 전체 또는 증분 VSS(볼륨 섀도 복사본 서비스) 백업 후 발생하는 로그 자르기.</p></li>
</ul></td>
<td><p>모범 사례:</p>
<ul>
<li><p>로그 자르기에 대한 백업을 사용합니다(예: 순환 로깅 사용 안 함).</p></li>
<li><p>3일간의 로그 생성 용량을 프로비전합니다.</p></li>
</ul></td>
<td><p>모범 사례:</p>
<ul>
<li><p>Exchange 기본 데이터 보호 기능을 사용하는 배포에 대해 Exchange 순환 로깅을 사용하도록 설정합니다.</p></li>
<li><p>로그 생성 용량의 3일 이상 재생 지연 설정을 프로비전합니다.</p></li>
</ul></td>
</tr>
</tbody>
</table>


다음 표에서는 Windows 디스크 유형에 대한 지침을 제공합니다.

### Exchange 2013 사서함 서버 역할에 대한 Windows 디스크 유형

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows 디스크 유형</th>
<th>설명</th>
<th>독립 실행형: 지원됨 또는 모범 사례</th>
<th>고가용성: 지원됨 또는 모범 사례</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 디스크</p></td>
<td><p>기본 저장소용으로 초기화된 디스크를 기본 디스크라고 합니다. 기본 디스크에는 주 파티션, 확장 파티션, 논리 드라이브 등의 기본 볼륨이 포함됩니다.</p></td>
<td><p>지원됨.</p>
<p>모범 사례: 기본 디스크를 사용합니다.</p></td>
<td><p>지원됨.</p>
<p>모범 사례: 기본 디스크를 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p>동적 디스크</p></td>
<td><p>동적 저장소용으로 초기화된 디스크를 동적 디스크라고 합니다. 동적 디스크에는 단순 볼륨, 스팬 볼륨, 스트라이프 볼륨, 미러 볼륨, RAID-5 볼륨 등의 동적 볼륨이 포함됩니다.</p></td>
<td><p>지원됨.</p></td>
<td><p>지원됨.</p></td>
</tr>
</tbody>
</table>


다음 표에서는 볼륨 구성에 대한 지침을 제공합니다.

### Exchange 2013 사서함 서버 역할에 대한 볼륨 구성

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>볼륨 구성</th>
<th>설명</th>
<th>독립 실행형: 지원됨 또는 모범 사례</th>
<th>고가용성: 지원됨 또는 모범 사례</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GPT(GUID 파티션 테이블)</p></td>
<td><p>GPT는 이전 MBR(마스터 부트 레코드) 파티션 구성표에서 확장되는 디스크 아키텍처입니다. NTFS로 포맷된 파티션의 최대 크기는 256테라바이트입니다.</p></td>
<td><p>지원됨.</p>
<p>모범 사례: GPT 파티션을 사용합니다.</p></td>
<td><p>지원됨.</p>
<p>모범 사례: GPT 파티션을 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p>MBR</p></td>
<td><p>MBR 즉, 파티션 섹터는 하드 디스크와 같이 분할된 데이터 저장소 장치의 첫 번째 섹터(LBA 섹터 0)인 512바이트의 부팅 섹터입니다. NTFS로 포맷된 파티션의 최대 크기는 2테라바이트입니다.</p></td>
<td><p>지원됨.</p></td>
<td><p>지원됨.</p></td>
</tr>
<tr class="odd">
<td><p>파티션 맞춤</p></td>
<td><p>파티션 맞춤은 최적의 성능을 위해 섹터 경계에서 파티션을 맞추는 것을 나타냅니다.</p></td>
<td><p>지원: Windows Server 2008 R2 및 Windows Server 2012 기본값은 1MB입니다.</p></td>
<td><p>지원: Windows Server 2008 R2 및 Windows Server 2012 기본값은 1MB입니다.</p></td>
</tr>
<tr class="even">
<td><p>볼륨 경로</p></td>
<td><p>볼륨 경로는 볼륨에 액세스하는 방법을 나타냅니다.</p></td>
<td><p>지원: 드라이브 문자 또는 탑재 지점.</p>
<p>모범 사례: 탑재 지점 호스트 볼륨은 RAID를 사용하도록 설정되어 있어야 합니다.</p></td>
<td><p>지원: 드라이브 문자 또는 탑재 지점.</p>
<p>모범 사례: 탑재 지점 호스트 볼륨은 RAID를 사용하도록 설정되어 있어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>파일 시스템</p></td>
<td><p>파일 시스템은 컴퓨터 파일과 파일에 포함된 데이터를 찾아 액세스하기 쉽게 저장 및 구성하는 방법을 나타냅니다.</p></td>
<td><p>지원: NTFS 및 ReFS</p></td>
<td><p>지원: NTFS 및 ReFS</p></td>
</tr>
<tr class="even">
<td><p>NTFS 조각 모음</p></td>
<td><p>NTFS 조각 모음은 Windows 파일 시스템에 있는 조각 양을 줄이는 프로세스입니다. 이 프로세스는 디스크의 콘텐츠를 물리적으로 구성하여 각 파일 조각을 가까이 인접하여 저장합니다.</p></td>
<td><p>지원됨.</p>
<p>모범 사례: 필요하지 않으며 권장되지 않음. Windows Server 2012에서는 자동 디스크 최적화 및 조각 모음 기능도 사용하지 않도록 설정하는 것이 좋습니다.</p></td>
<td><p>지원됨.</p>
<p>모범 사례: 필요하지 않으며 권장되지 않음. Windows Server 2012에서는 자동 디스크 최적화 및 조각 모음 기능도 사용하지 않도록 설정하는 것이 좋습니다.</p></td>
</tr>
<tr class="odd">
<td><p>NTFS 할당 단위 크기</p></td>
<td><p>NTFS 할당 단위 크기는 파일 저장을 위해 할당할 수 있는 최소 디스크 공간을 나타냅니다.</p></td>
<td><p>지원: 모든 할당 단위 크기</p>
<p>모범 사례: .edb 및 로그 파일 볼륨 모두에 대해 64KB</p></td>
<td><p>지원: 모든 할당 단위 크기</p>
<p>모범 사례: .edb 및 로그 파일 볼륨 모두에 대해 64KB</p></td>
</tr>
<tr class="even">
<td><p>NTFS 압축</p></td>
<td><p>NTFS 압축은 하드 디스크에 저장된 파일의 실제 크기를 줄이는 프로세스입니다.</p></td>
<td><p>지원: Exchange 데이터베이스 또는 로그 파일에 대해서는 지원되지 않음.</p></td>
<td><p>지원: Exchange 데이터베이스 또는 로그 파일에 대해서는 지원되지 않음.</p></td>
</tr>
<tr class="odd">
<td><p>NTFS EFS(파일 시스템 암호화)</p></td>
<td><p>EFS를 통해 사용자는 개별 파일, 폴더 또는 전체 데이터 드라이브를 암호화할 수 있습니다. EFS는 업계 표준 알고리즘 및 공개 키 암호화를 통해 강력한 암호화를 제공하기 때문에 공격자가 시스템 보안을 통과하는 경우에도 암호화된 파일은 기밀로 유지됩니다.</p></td>
<td><p>지원: Exchange 데이터베이스 또는 로그 파일에 대해서는 지원되지 않음.</p></td>
<td><p>Exchange 데이터베이스 또는 로그 파일에 대해서는 지원되지 않음.</p></td>
</tr>
<tr class="even">
<td><p>Windows BitLocker(볼륨 암호화)</p></td>
<td><p>Windows BitLocker는 Windows Server 2008의 데이터 보호 기능입니다. BitLocker는 분실하거나 도난 당한 컴퓨터에 들어 있는 데이터가 도난 당하거나 노출되지 않도록 보호하며, 컴퓨터를 폐기할 때 데이터를 보다 안전하게 삭제할 수 있도록 합니다.</p></td>
<td><p>지원: 모든 Exchange 데이터베이스 및 로그 파일.</p></td>
<td><p>지원: 모든 Exchange 데이터베이스 및 로그 파일. Windows 장애 조치(failover) 클러스터를 사용하려면 Windows Server 2008 R2 또는 Windows Server 2008 R2 SP1과 다음 핫픽스가 있어야 합니다. <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2446607">컴퓨터가 장애 조치(failover) 클러스터 노드인 경우 Windows Server 2008 R2의 디스크 볼륨에서 BitLocker를 사용하도록 설정할 수 없다</a>. Bitlocker가 사용하도록 설정된 Exchange 볼륨은 이전 버전의 Windows를 실행하는 Windows 장애 조치(failover) 클러스터에서 지원되지 않습니다.</p>
<p>Windows 7 BitLocker 암호화에 대 한 자세한 내용은 참조 <a href="https://go.microsoft.com/fwlink/p/?linkid=220898">Windows 7에서 BitLocker 드라이브 암호화: 질문과 대답</a>합니다.</p></td>
</tr>
<tr class="odd">
<td><p>SMB(서버 메시지 블록) 3.0</p></td>
<td><p>SMB(서버 메시지 블록) 프로토콜은 컴퓨터의 응용 프로그램이 원격 서버의 파일과 리소스에 액세스할 수 있도록 하는 네트워크 파일 공유 프로토콜(TCP/IP 또는 기타 네트워크 프로토콜 위에 있음)입니다. 또한 SMB 프로토콜은 응용 프로그램이 SMB 클라이언트 요청을 받도록 설정된 모든 서버 프로그램과 통신할 수 있도록 합니다. Windows Server 2012에는 다음 기능이 포함된 SMB 프로토콜의 새로운 3.0 버전이 도입되었습니다.</p>
<ul>
<li><p>SMB 투명 장애 조치(failover)</p></li>
<li><p>SMB 스케일 아웃</p></li>
<li><p>SMB 다중 채널</p></li>
<li><p>SMB 다이렉트</p></li>
<li><p>SMB 암호화</p></li>
<li><p>SMB 파일 공유용 VSS</p></li>
<li><p>SMB 디렉터리 임대</p></li>
<li><p>SMB PowerShell</p></li>
</ul></td>
<td><p>제한된 지원. 지원되는 시나리오는 디스크가 SMB 3.0 공유 위치의 VHD에 호스트되는 하드웨어 가상화 배포입니다. 이러한 VHD는 하이퍼바이저를 통해 호스트에 제공됩니다. 자세한 내용은 <a href="exchange-2013-virtualization-exchange-2013-help.md">Exchange 2013 가상화</a>를 참조하십시오.</p></td>
<td><p>제한된 지원. 지원되는 시나리오는 디스크가 SMB 3.0 공유 위치의 VHD에 호스트되는 하드웨어 가상화 배포입니다. 이러한 VHD는 하이퍼바이저를 통해 호스트에 제공됩니다. 자세한 내용은 <a href="exchange-2013-virtualization-exchange-2013-help.md">Exchange 2013 가상화</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>저장소 공간</p></td>
<td><p>저장소 공간에는 Windows Server 2012에 대 한 가상화 기능을 제공 하는 새 저장소 솔루션입니다. 저장소 공간을 사용 하면 단순히 디스크를 추가 하 여 쉽게 확장할 수 있는 저장소 풀으로 실제 디스크를 구성할 수 있습니다. USB, SATA 또는 SAS을 통해 이러한 디스크를 연결할 수 있습니다. 또한 씬 프로비저닝와 같은 실제 미디어를 원본으로 사용 되는 오류에 대 한 복구 관련된 강력한 기능을 갖춘 실제 디스크 처럼 작동 하는 가상 디스크 (공백)를 활용 합니다. 저장소 공간에 대 한 자세한 내용은 <a href="https://technet.microsoft.com/en-us/library/hh831739.aspx">저장소 공간 개요</a>를 참조 하십시오.</p></td>
<td><p>지원됨. 이 항목에서 설명하는 실제 디스크 유형과 동일한 제한이 적용됩니다.</p></td>
<td><p>지원됨. 이 항목에서 설명하는 실제 디스크 유형과 동일한 제한이 적용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>ReFS(복원 파일 시스템)</p></td>
<td><p>ReFS는 NTFS의 기초 기반으로 구축 되는 Windows Server 2012 년 새로 설계 파일 시스템입니다. ReFS로 향상 된 데이터 확인 및 자동 고침 기술을 저장소 공간 기능을 함께 사용 하는 경우에 특히 손상에 통합 된 끝-복구를 제공 하는 동안 높은 수준의 NTFS와의 호환성을 유지 합니다. ReFS에 대 한 자세한 내용은 <a href="https://technet.microsoft.com/en-us/library/hh831724.aspx">복원 파일 시스템 개요</a>를 참조 하십시오.</p></td>
<td><p>Exchange 데이터베이스 파일, 로그 파일 및 콘텐츠 인덱스 파일에 포함 된 볼륨에 대 한 지원 합니다. Windows Server 2012를 배포 하는 경우에 다음의 핫픽스 Windows Server 2012에 설치 된 확인 합니다.</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Windows 8 및 Windows Server 2012 업데이트 롤업: 2013 년 4 월</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">가상 디스크 서비스 또는 가상 디스크 서비스 크래시를 사용 하 여 또는 Windows Server 2012의 고정 하는 응용 프로그램</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">Windows 8 또는 Windows Server 2012 기반 컴퓨터 동결 ReFS 볼륨에 'dir' 명령을 실행 하는 경우</a></p></li>
</ul>
<p>ReFS OS 볼륨에 대해 지원 되지 않습니다.</p>
<p>모범 사례: Exchange 데이터베이스 (.edb) 파일 또는 이러한 파일을 호스팅하는 볼륨에 대 한 데이터 무결성 기능을 비활성화 해야 합니다.</p></td>
<td><p>Exchange 데이터베이스 파일, 로그 파일 및 콘텐츠 인덱스 파일에 포함 된 볼륨에 대 한 지원 합니다. Windows Server 2012를 배포 하는 경우에 다음의 핫픽스 Windows Server 2012에 설치 된 확인 합니다.</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Windows 8 및 Windows Server 2012 업데이트 롤업: 2013 년 4 월</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">가상 디스크 서비스 또는 응용 프로그램 가상 디스크 서비스 충돌을 사용 하는 또는 Windows Server 2012에 고정</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">Windows 8 또는 Windows Server 2012 기반 컴퓨터 동결 ReFS 볼륨에 'dir' 명령을 실행 하는 경우</a></p></li>
</ul>
<p>ReFS OS 볼륨에 대해 지원 되지 않습니다.</p>
<p>모범 사례: Exchange 데이터베이스 (.edb) 파일 또는 이러한 파일을 호스팅하는 볼륨에 대 한 데이터 무결성 기능을 비활성화 해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>데이터 중복 제거</p></td>
<td><p>데이터 중복 제거는 Windows Server 2012의 저장소 사용을 최적화하기 위한 새로운 기술로, 데이터의 충실도나 무결성은 그대로 유지하면서 데이터 내 중복을 찾아서 제거하는 방법입니다. 이를 통해 파일을 작은 가변 크기 청크로 분할한 다음 중복 청크를 식별하여 각 청크의 단일 복사본을 유지함으로써 더 적은 공간에 더 많은 데이터를 저장하는 것이 목표입니다. 청크의 중복 복사본은 단일 복사본에 대한 참조로 바뀌고, 청크는 컨테이너 파일에 구성되며, 컨테이너는 보다 나은 공간 최적화를 위해 압축됩니다.</p></td>
<td><p>Exchange 데이터베이스 파일에 대해서는 지원되지 않습니다. 참고: 완전히 오프라인 상태인 백업 또는 보관용 Exchange 데이터베이스 파일에 대해 사용할 수 있습니다.</p></td>
<td><p>Exchange 데이터베이스 파일에 대해서는 지원되지 않습니다. 참고: 완전히 오프라인 상태인 백업 또는 보관용 Exchange 데이터베이스 파일에 대해 사용할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

