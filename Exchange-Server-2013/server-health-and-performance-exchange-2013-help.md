---
title: '서버 상태 및 성능: Exchange 2013 Help'
TOCTitle: 서버 상태 및 성능
ms:assetid: 9d1fdec8-8273-4c71-88f1-b4edfd542c4f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150551(v=EXCHG.150)
ms:contentKeyID: 50483767
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 서버 상태 및 성능

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

이해 서버 상태 및 성능을 디자인 하 고 유지 관리 하 고성능 메시징 인프라에 중요 한 됩니다. Microsoft Exchange Server 2013 서버 상태 및 성능 향상을 소개합니다.

모든 서버 상태 및 성능 항목 목록이 필요 하신가요? 서버 상태 및 성능 설명서를 참조 하십시오.

## 관리되는 가용성

*관리 되는 가용성의*개념을 소개 하는 Exchange 2013 합니다. 모든 Exchange 2013 서버에 대 한 가용성 실행을 관리합니다. 것은 두 프로세스, Exchange Health Manager 서비스 (MSExchangeHMHost.exe) 및 Exchange Health Manager 작업자 프로세스 (MSExchangeHMWorker.exe) 및 구성 다음과 같은 비동기 구성 요소:

  - **검색 엔진**   *프로브 엔진* 은 서버에서 측정 단위를 수행합니다.

  - **모니터링 프로브 엔진**   *모니터링 프로브 엔진* 기능 정상 상태를 구성 하는 방법에 대 한 비즈니스 논리를 저장 합니다. 패턴 및 정상 상태는 다른 측정 단위에 대 한 자세한 내용은 패턴 인식 엔진을 다음과 같이 작동 하 고 정상 없는 구성 요소 또는 기능이 있는지 여부를 평가 합니다.

  - **응답자 엔진**   *응답자 엔진* 비정상 있는 구성 요소에 대 한 경고를 수신할 때 해당 첫번째 작업은 해당 구성 요소 복구를 시도입니다. 가용성 수 있도록 다중 단계 복구 작업을 관리합니다. 첫번째 시도 응용 프로그램 풀을 다시 시작할 수 있습니다, 두번째 시도 해당 서비스를 다시 시작할 수 있습니다 및 서버를 다시 시작 하 여 세번째 시도 수도 있습니다. 및 더이상 트래픽을 수락 되도록 서버를 오프 라인으로 전환 하 여 최종 시도 수도 없습니다. 이러한 모든 작업에 실패 하는 경우 지원 센터에 알림이 전송 됩니다.

고가용성에 대한 자세한 내용은 [관리되는 가용성](managed-availability-exchange-2013-help.md) 항목을 참조하세요.

## 작업 관리

Exchange 2013 작업 부하 관리에는 다음 구성 요소가 포함 됩니다.

  - *사용자 작업 부하 관리* 은 Exchange Server 2010 의 기능을 제한 하는 사용자에 대 한 새 이름입니다. 이 설정은 환경 요구에 따라 사용자 지정할 수 있습니다.

  - *시스템 작업 부하 관리* Exchange 2013 에 대 한 새로운 및 주요 서버 리소스의 상태를 모니터링 하 여 특정 Exchange 작업 부하를 자동으로 제한 하는 데 사용 됩니다. Microsoft 고객 서비스 및 지원의 지시에 따라만 이러한 설정은 사용자 지정 해야 합니다.

자세한 내용은 [Exchange 작업 관리](exchange-workload-management-exchange-2013-help.md)을 참조 하십시오.

## 서버 상태 및 성능 설명서

다음 표에을 소개 하 고 서버 상태 및 성능 Exchange 2013 에서 관리 하는데 도움이 되는 항목에 대 한 링크를 포함 합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="exchange-workload-management-exchange-2013-help.md">Exchange 작업 관리</a></p></td>
<td><p>개별 사용자가 리소스를 사용 하는 방식을 제어 하 여 Exchange 작업 부하를 관리 하는 방법에 대 한 설명 합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="managed-availability-exchange-2013-help.md">관리되는 가용성</a></p></td>
<td><p>Exchange 2013 에서 사용할 수 있는 기본 제공 리소스 모니터링 및 복구 작업에 알아봅니다.</p></td>
</tr>
</tbody>
</table>

