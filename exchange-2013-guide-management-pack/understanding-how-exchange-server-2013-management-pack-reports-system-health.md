---
title: Exchange Server 2013 관리 팩에서 시스템 상태를 보고하는 방법 이해
TOCTitle: Exchange Server 2013 관리 팩에서 시스템 상태를 보고하는 방법 이해
ms:assetid: 6ca8847f-93fe-458d-bd43-7afad7fdd2f4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn195910(v=EXCHG.150)
ms:contentKeyID: 53275605
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 관리 팩에서 시스템 상태를 보고하는 방법 이해

 

_**마지막으로 수정된 항목:** 2013-04-17_

이 항목은 Exchange Server 2013 관리 팩이 Exchange 시스템 상태를 모니터링하고 보고하는 방법에 대한 정보를 제공합니다. Exchange 2013 관리 팩에서 상태 정보는 간단한 방법으로 롤업됩니다. 상태 설정이 비정상이고 에스컬레이션 응답기가 트리거될 때마다 Windows 이벤트 로그에 다음 이벤트가 기록됩니다.

## 관리되는 가용성

Exchange Server 2013에서는 아키텍처와 관련하여 몇 가지 항목이 변경되었습니다. 주요 변경 내용 중 하나는 *관리되는 가용성* 기능으로, 모든 Exchange 2013 구성 요소에는 문제를 감지하고 서비스 가용성을 복구하려고 시도하는 기본 제공 모니터가 포함됩니다. Exchange 2013 관리 팩에서 이 기능이 사용됩니다. 자동으로 복구할 수 없는 모든 문제는 Exchange 2013 관리 팩에 자동으로 경고로 에스컬레이션됩니다. Exchange 2013의 각 구성 요소는 프로브, 모니터 및 응답기라고 하는 세 개의 기본 구성 요소를 사용하여 자신을 모니터링합니다.

![관리되는 가용성](images/Dn195910.dd5febae-d05e-4089-a3f5-1691b2d9a3d7(EXCHG.150).png "관리되는 가용성")

  - **프로브**   여러 구성 요소를 측정하는 일련의 데이터 수집기로, 다음과 같은 세 개의 고유한 프로브 유형이 있습니다.
    
      - 가상 종단 간 최종 사용자 작업을 측정하는 가상 트랜잭션 및 실제 트래픽을 측정하는 검사
    
      - 실제 고객 트래픽을 측정하는 검사
    
      - Exchange에서 즉각적인 작업을 수행할 수 있도록 해주는 알림. 대표적인 예로 인증서가 만료될 때 트리거되는 알림을 들 수 있습니다.

  - **모니터**   프로브에 의해 수집된 데이터는 특정 조건에 대해 데이터를 분석하고 조건에 따라 특정 구성 요소가 정상인지 비정상인지 여부를 판단하는 모니터로 전달됩니다.

  - **응답기**   구성 요소가 비정상이라고 모니터가 판단하면 응답기가 트리거됩니다. 복구 가능한 문제일 경우 응답기는 기본 제공 논리를 사용하여 구성 요소 복구를 시도합니다. 각 구성 요소에 사용할 수 있는 여러 응답기가 있지만 Exchange 2013 관리 팩과 관련된 응답기는 *에스컬리에션 응답기*입니다. 에스컬레이션 응답기가 트리거되면 Exchange 2013 관리 팩에서 인식되는 이벤트가 생성되고 관리자에게 문제를 해결하는 데 필요한 정보를 제공하는 적절한 정보가 해당 경고에 제공됩니다.

Exchange 2013의 각 구성 요소는 특정 집합의 프로브, 모니터 및 응답기를 사용하여 자신을 모니터링합니다. 이러한 프로브 및 모니터 모음을 *상태 설정*이라고 합니다. 예를 들어 ActiveSync 서비스의 다양한 측면에 대한 데이터를 수집하는 여러 프로브가 있습니다. 이 데이터는 ActiveSync 서비스에서 감지되는 모든 문제를 수정하기 위해 적합한 응답기를 트리거하는 지정된 모니터 집합에서 처리됩니다. 종합적으로 이러한 구성 요소는 ActiveSync 상태 설정을 구성합니다.

Exchange의 상태 설정은 관리 팩 대시보드에 해당하는, 다음과 같은 네 개의 범주로 구성됩니다.

  - 고객 접점

  - 서비스 구성 요소

  - 서버 리소스

  - 주요 종속성

Exchange 상태 설정의 전체 목록은 [Appendix A: Exchange health sets](appendix-a-exchange-health-sets.md)을 참조하십시오.

관리되는 가용성에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 상태 롤업 방법

이 항목은 Exchange Server 2013 관리 팩이 Exchange 시스템 상태를 모니터링하고 보고하는 방법에 대한 정보를 제공합니다. Exchange 2013 관리 팩에서 상태 정보는 간단한 방법으로 롤업됩니다. 상태 설정이 비정상이고 에스컬레이션 응답기가 트리거될 때마다 Windows 이벤트 로그에 다음 이벤트가 기록됩니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>로그 이름</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>원본</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>날짜</p></td>
<td><p>&lt;<em>이벤트 날짜 및 시간</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>이벤트 ID</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>작업 범주</p></td>
<td><p>모니터링</p></td>
</tr>
<tr class="even">
<td><p>수준</p></td>
<td><p>오류</p></td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><p>&lt;<em>없음</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>사용자</p></td>
<td><p>SYSTEM</p></td>
</tr>
<tr class="odd">
<td><p>컴퓨터</p></td>
<td><p>&lt;<em>Exchange 서버의 FQDN</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>설명</p></td>
<td><p>&lt;<em>에스컬레이션 응답기에서 동적으로 생성</em>&gt;</p></td>
</tr>
</tbody>
</table>


관리 팩 에이전트에서 이 이벤트가 감지 및 처리됩니다. 이 이벤트를 사용하면 관리되는 가용성이 SCOM에서 경고를 생성할 수 있습니다. 해당 문제가 해결되고 상태 설정이 다시 정상 상태로 돌아오면 Windows 이벤트 로그에 다음 이벤트가 기록됩니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>로그 이름</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>원본</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>날짜</p></td>
<td><p>&lt;<em>이벤트 날짜 및 시간</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>이벤트 ID</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>작업 범주</p></td>
<td><p>모니터링</p></td>
</tr>
<tr class="even">
<td><p>수준</p></td>
<td><p>정보</p></td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><p>&lt;<em>없음</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>사용자</p></td>
<td><p>SYSTEM</p></td>
</tr>
<tr class="odd">
<td><p>컴퓨터</p></td>
<td><p>&lt;<em>Exchange 서버의 FQDN</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>설명</p></td>
<td><p>&lt;<em>에스컬레이션 응답기에서 동적으로 생성</em>&gt;</p></td>
</tr>
</tbody>
</table>


이전 버전의 Exchange를 모니터링했던 관리 팩은 완전히 중앙 집중화되었었습니다. 각 Exchange 서버의 에이전트가 데이터를 수집하고 중앙 상관 관계 엔진이 에이전트에서 보고한 모든 데이터를 비교 및 평가하여 전체 서비스 상태를 판단했습니다. 대규모 환경에서는 이 프로세스로 인해 상관 관계가 복잡해져 경고 생성 시 지연이 발생했습니다. Exchange 2013부터 더 이상 경고 상관 관계가 사용되지 않습니다. 대신 각 서버는 자체 모니터링을 수행하고 필요한 경우 SCOM에 경고를 보내 아키텍처 확장성이 대폭 향상됩니다.

이벤트 영향 및 트리거되는 상태 설정에 따라 문제는 SCOM 콘솔의 서로 다른 범주에 표시됩니다. 이벤트가 사용자 영향을 야기할 경우 고객 접점 표시기가 비정상으로 표시됩니다. 이벤트가 OWA와 같은 전체 구성 요소를 사용할 수 없도록 할 경우 서비스 구성 요소 표시기가 비정상으로 표시됩니다. 특정 서버와 관련된 문제일 경우 해당 서버의 상태 표시기가 비정상으로 표시됩니다. 마지막으로, 문제가 Exchange에서 사용하는 리소스와 관련된 경우 주요 종속 관계 표시기가 비정상으로 표시됩니다. 이러한 범주에 대한 자세한 내용은 [Exchange Server 2013 관리 팩 시작](getting-started-with-exchange-server-2013-management-pack.md)를 참조하십시오.

