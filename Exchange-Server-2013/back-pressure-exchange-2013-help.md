---
title: '역 압력: Exchange 2013 Help'
TOCTitle: 역 압력
ms:assetid: 03003544-e802-4988-9427-5fc4da64dcb8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201658(v=EXCHG.150)
ms:contentKeyID: 52058048
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역 압력

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

역 압력은 Microsoft Exchange 2013 사서함 서버 및 Edge 전송 서버에 있는 Microsoft Exchange Transport 서비스의 시스템 리소스 모니터링 기능입니다.

Exchange는 사용 가능한 하드 드라이브 공간 및 메모리와 같은 중요한 리소스가 압력 상태에 있음을 감지하면 서비스 비가용성을 방지하기 위한 조치를 취할 수 있습니다. 역 압력은 시스템 리소스가 과도하게 소모되는 것을 방지하고 Exchange 서버는 새 메시지를 받기 전에 기존 메시지의 처리를 시도합니다. 시스템 리소스 사용률이 보통 수준으로 돌아가면 Exchange 서버가 점차적으로 정상 작동을 다시 시작하고 새 메시지를 다시 받기 시작합니다.

Exchange 2013에서 사서함 서버의 전송 서비스 또는 Edge 전송 서버는 리소스 압력을 받고 있을 경우 들어오는 연결은 수락하지만 해당 연결을 통해 들어오는 메시지는 느린 속도로 수락하거나 거부합니다. SMTP 호스트가 리소스 압력을 받고 있는 Exchange 서버에 연결을 시도할 때 연결에 성공하지만 호스트가 메시지를 전송하기 위해 **MAIL FROM** 명령을 실행하면 압력을 받고 있는 리소스에 따라 전송 서비스에서는 **MAIL FROM** 명령의 승인을 지연하거나 연결을 거부합니다.

**목차**

Resources monitored

Actions taken by Exchange Transport when under resource pressure

Back pressure configuration options in the EdgeTransport.exe.config file

Back pressure logging information

## 모니터링된 리소스

다음 시스템 리소스는 역 압력 기능의 일부로 모니터링됩니다.

  - 메시지 큐 데이터베이스를 저장하는 하드 드라이브의 사용 가능한 공간

  - 메시지 큐 데이터베이스 트랜잭션 로그를 저장하는 하드 드라이브의 사용 가능한 공간

  - 메모리에 존재하는 커밋되지 않은 메시지 큐 데이터베이스 트랜잭션의 수

  - EdgeTransport.exe 프로세스에 사용되는 메모리

  - 다른 모든 프로세스에 사용되는 메모리

  - 전송 큐의 메시지 수입니다.

사서함 서버나 Edge 전송 서버에서 모니터링되는 각 시스템 리소스에 대해 다음 세 가지 수준의 리소스 사용률이 적용됩니다.

  - **보통**   리소스가 정상적인 수준으로 사용되고 있습니다. 서버가 새 연결 및 메시지를 수락합니다.

  - **중간**   리소스가 약간 과도하게 사용되고 있습니다. 역 압력이 제한된 방식으로 서버에 적용됩니다. 신뢰할 수 있는 도메인의 보낸 사람이 보낸 메일이 전송될 수 있습니다. 그러나 압력을 받고 있는 특정 리소스에 따라 서버는 타피팅을 사용하여 서버 응답을 지연시키거나 다른 원본에서 들어오는 **MAIL FROM** 명령을 거부합니다.

  - **높음**   리소스가 상당히 과도하게 사용되고 있습니다. 전체 역 압력이 적용됩니다. 모든 메시지 흐름이 중지되고 서버가 새로 들어오는 모든 **MAIL FROM** 명령을 거부합니다.

다음 섹션에서는 Exchange에서 특정 리소스가 압력을 받고 있는 상황을 처리하는 방법에 대해 설명합니다.

## 메시지 큐 데이터베이스에 대한 사용 가능한 하드 드라이브 공간

기본적으로 메시지 큐 데이터베이스는 %ExchangeInstallPath%TransportRoles\\data\\Queue에 저장됩니다. Exchange는 이 위치의 하드 드라이브 공간 사용률을 모니터링합니다. 높음 수준의 하드 드라이브 공간 사용률은 다음 수식을 사용하여 계산됩니다.

100 \* (*하드 디스크 크기* - *고정 상수*) / *하드 드라이브 크기*

*고정 상수* 값은 500MB입니다.

이 수식의 결과는 사용 중인 총 하드 드라이브 공간에 대한 백분율로 표시됩니다. 이 수식의 결과는 항상 가장 가까운 정수로 내림됩니다. 기본적으로 중간 수준의 하드 드라이브 사용률은 높음 수준보다 2%가 적습니다. 또한 보통 수준의 하드 드라이브 사용률은 높음 수준보다 4%가 적습니다.

맨 위로 이동

## 메시지 큐 데이터베이스 트랜잭션 로그에 대한 사용 가능한 하드 드라이브 공간

기본적으로 메시지 큐 데이터베이스 트랜잭션 로그는 %ExchangeInstallPath%TransportRoles\\data\\Queue에 저장됩니다. Exchange는 이 위치의 하드 드라이브 공간 사용률을 모니터링합니다. %ExchangeInstallPath%Bin\\EdgeTransport.exe.config 응용 프로그램 구성 파일에는 기본값이 384MB인 *DatabaseCheckPointDepthMax* 키가 있습니다. 이 키는 하드 드라이브에 있는 커밋되지 않은 모든 트랜잭션 로그의 총 허용 크기를 제어합니다. 이 키는 하드 드라이브 사용률을 계산하는 수식에 사용됩니다.


> [!NOTE]
> <EM>DatabaseCheckPointDepthMax</EM> 키의 값은 사서함 서버 또는 Edge 전송 서버에 있는 모든 전송 관련 ESE(Extensible Storage Engine) 데이터베이스에 적용됩니다. 여기에는 메시지 큐 데이터베이스와 IP 필터 데이터베이스가 포함될 수 있습니다.



기본적으로 높음 수준의 디스크 사용률은 다음 수식을 사용하여 계산됩니다.

100 \* (*하드 드라이브 크기* - Min(5GB, 3\**DatabaseCheckPointDepthMax*)) / *하드 드라이브 크기*

이 수식의 결과는 항상 가장 가까운 정수로 내림됩니다. 기본적으로 중간 수준의 하드 드라이브 사용률은 높음 수준보다 2%가 적습니다. 또한 보통 수준의 하드 드라이브 사용률은 높음 수준보다 4%가 적습니다.

맨 위로 이동

## 메모리의 커밋되지 않은 메시지 큐 데이터베이스 트랜잭션 수

메시지 큐 데이터베이스 변경 내용 목록은 트랜잭션 로그로 커밋될 수 있을 때까지 메모리에 보관됩니다. 그런 다음 메시지 큐 데이터베이스 자체로 커밋됩니다. 메모리에 보관되어 있는 이러한 해결되지 않은 메시지 큐 데이터베이스 트랜잭션을 *버전 버킷*이라고 합니다. 예기치 않은 많은 양의 들어오는 메시지, 스팸 공격, 메시지 큐 데이터베이스 무결성 문제 또는 하드 드라이브 성능 때문에 버전 버킷 수가 감당할 수 없이 높은 수준까지 증가할 수 있습니다.

Exchange가 메시지 수신을 시작할 경우 이러한 메시지는 일괄적으로 그룹화된 다음 버전 버킷으로 준비됩니다. 들어오는 메시지에 큰 첨부 파일이 있는 경우 여러 일괄 처리로 구분될 수 있습니다. 이러한 처리 중인 일괄 처리는 *일괄 처리 지점*으로 알려져 있습니다. 특히 큰 첨부 파일이 있는 예기치 않은 많은 양의 들어오는 메시지가 있는 경우에 미해결 일괄 처리 지점 수는 설정된 임계값을 초과할 수 있습니다.

버전 버킷 또는 일괄 처리 지점이 압력을 받고 있는 경우 Exchange 서버는 들어오는 메시지에 대한 승인을 지연시켜 들어오는 연결의 조정을 시작합니다. Exchange는 **MAIL FROM** 명령을 지연시키는 타피팅을 통해 인바운드 메시지 흐름 속도를 줄입니다. 리소스 압력 상태가 계속되면 Exchange는 타피팅 지연을 점차적으로 증가시킵니다. 리소스 사용률이 정상으로 돌아온 후 Exchange는 점차적으로 승인 지연을 줄이기 시작하고 정상 작동으로 들어갑니다. 기본적으로 Exchange는 리소스 압력을 받고 있을 때 메시지 승인을 10초 지연시키기 시작합니다. 리소스가 계속해서 압력을 받고 있는 경우 지연은 5초 단위로 최대 55초까지 증가합니다.

Exchange는 버전 버킷 및 일괄 처리 지점 리소스 사용률의 기록을 유지합니다. 리소스 사용률이 기록 깊이라고 알려진 특정 폴링 간격 수의 정상 수준으로 내려가지 않을 경우 Exchange는 타피팅 지연을 중지하고 리소스 사용률이 정상으로 돌아올 때까지 들어오는 메시지를 거부하기 시작합니다. 기본적으로 버전 버킷 및 일괄 처리 지점의 기록 깊이는 각각 10개 및 300개의 폴링 간격에 해당합니다.

맨 위로 이동

## EdgeTransport.exe 프로세스에 의해 사용된 메모리

기본적으로 높음 수준의 EdgeTransport.exe 프로세스 메모리 사용률은 다음 수식을 사용하여 계산됩니다.

총 실제 메모리의 75% 또는 1TB 중에서 더 작은 크기

이 계산에는 하드 드라이브의 페이징 파일에 사용할 수 있는 가상 메모리나 다른 프로세스에 사용되는 메모리는 포함되지 않습니다. 이 수식의 결과는 EdgeTransport.exe 프로세스에 사용되는 총 메모리에 대한 백분율로 표시됩니다. 이 수식의 결과는 항상 가장 가까운 정수로 내림됩니다.

기본적으로 중간 수준의 EdgeTransport.exe 파일 메모리 사용률은 총 실제 메모리의 73%나 높음 수준 값에서 2%를 뺀 값 중에서 더 작은 값으로 계산됩니다. 또한 보통 수준의 EdgeTransport.exe 파일 메모리 사용률은 총 실제 메모리의 71%나 높음 수준 값에서 4%를 뺀 값 중에서 더 작은 값으로 계산됩니다.

EdgeTransport.exe 프로세스의 메모리 사용률이 지정한 보통 수준보다 더 높으면 *가비지 수집*이 적용됩니다. 가비지 수집은 메모리에 있는 사용되지 않은 개체를 확인하는 프로세스이며 이러한 사용되지 않은 개체에 사용된 메모리를 회수합니다.

Exchange는 EdgeTransport.exe 프로세스의 메모리 사용률 기록을 유지합니다. 사용률이 기록 깊이라고 알려진 특정 폴링 간격 수의 정상 수준으로 내려가지 않을 경우 Exchange는 리소스 사용률이 정상으로 돌아올 때까지 들어오는 메시지를 거부하기 시작합니다. 기본적으로 EdgeTransport.exe 메모리 사용률의 기록 깊이는 30개의 폴링 간격에 해당합니다.

맨 위로 이동

## 모든 프로세스에 의해 사용된 메모리

기본적으로 모든 프로세스의 높음 수준의 메모리 사용률은 총 실제 메모리의 94%입니다. 이 값에는 하드 드라이브의 페이징 파일에 사용할 수 있는 가상 메모리는 포함되지 않습니다.

지정된 메모리 사용률 수준에 도달하면 *메시지 디하이드레이션*이 발생합니다. 메시지 디하이드레이션은 메모리에 캐시된 대기 중인 메시지의 불필요한 요소를 제거하는 작업입니다. 성능 향상을 위해 전체 메시지가 메모리에 캐시됩니다. 메모리에서 대기 중인 메시지의 MIME 콘텐츠를 제거하면 메시지가 메시지 큐 데이터베이스에서 직접 읽히므로 길어지는 대기 시간으로 인해 사용되는 메모리가 줄어듭니다. 기본적으로 메시지 디하이드레이션을 사용할 수 있도록 설정되어 있습니다.

맨 위로 이동

## 전송 큐의 메시지 수

전송 큐는 Edge 전송 서버와 Exchange 2013 사서함 서버의 전송 서비스와 연결되어 있습니다. 분류기는 전송 큐의 각 메시지를 처리합니다. 이러한 분류를 통해 메시지가 배달 큐에 배치됩니다. 자세한 내용은 [메일 흐름](mail-flow-exchange-2013-help.md) 및 [큐](queues-exchange-2013-help.md) 항목을 참조하십시오. 전송 큐에 있는 대량 메시지는 분류기가 메시지를 처리하지 못할 수 있음을 의미합니다.

전송 큐가 압력을 받고 있는 경우 Exchange 서버는 들어오는 메시지에 대한 승인을 지연시켜 들어오는 연결의 조정을 시작합니다. Exchange는 **MAIL FROM** 명령을 지연시키는 타피팅을 통해 인바운드 메시지 흐름 속도를 줄입니다. 전송 큐 압력 상태가 계속되면 Exchange는 타피팅 지연을 점차적으로 증가시킵니다. 전송 큐 사용률이 정상으로 돌아온 후 Exchange는 점차적으로 승인 지연을 줄이기 시작하고 정상 작동으로 들어갑니다. 기본적으로 Exchange는 전송 큐 압력을 받고 있을 때 메시지 승인을 10초 지연시키기 시작합니다. 전송 큐가 계속해서 압력을 받고 있는 경우 지연은 5초 단위로 최대 55초까지 증가합니다.

Exchange는 전송 큐 사용률 기록을 유지합니다. 전송 큐 사용률이 기록 깊이라고 알려진 특정 폴링 간격 수의 정상 수준으로 내려가지 않을 경우 Exchange는 타피팅 지연을 중지하고 전송 사용률이 정상으로 돌아올 때까지 들어오는 메시지를 거부하기 시작합니다. 기본적으로 전송 큐 기록 깊이는 300개의 폴링 간격에 해당합니다.

## 리소스 압력을 받고 있을 때 Exchange Transport가 수행하는 작업

다음 표에는 특정 리소스가 압력을 받고 있는 경우 Exchange Transport가 수행하는 작업이 요약되어 있습니다.

### 리소스 압력에 대응하여 사서함 및 Edge 전송 서버가 수행하는 역 압력 작업

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>압력을 받고 있는 리소스</th>
<th>사용률 수준</th>
<th>수행한 작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>메시지 큐 데이터베이스에 대한 하드 드라이브 공간</p></td>
<td><p>중간</p></td>
<td><ul>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>메시지 큐 데이터베이스에 대한 하드 드라이브 공간</p></td>
<td><p>높음</p></td>
<td><ul>
<li><p>다른 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>사서함 서버의 사서함 전송 서비스를 통해 사서함 데이터베이스로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>메시지 큐 데이터베이스 트랜잭션 로그에 대한 하드 드라이브 공간</p></td>
<td><p>중간</p></td>
<td><ul>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>메시지 큐 데이터베이스 트랜잭션 로그에 대한 하드 드라이브 공간</p></td>
<td><p>높음</p></td>
<td><ul>
<li><p>다른 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>사서함 서버의 사서함 전송 서비스를 통해 사서함 데이터베이스로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>버전 버킷</p></td>
<td><p>중간</p></td>
<td><p>들어오는 메시지에 대한 타피팅 지연을 시작하거나 증가시킵니다. 전체 버전 버킷 기록 깊이에 대한 정상 수준에 도달하지 않을 경우 다음 작업을 수행합니다.</p>
<ul>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>버전 버킷</p></td>
<td><p>높음</p></td>
<td><p>들어오는 메시지에 대한 타피팅 지연을 시작하거나 증가시킵니다. 전체 버전 버킷 기록 깊이에 대한 정상 수준에 도달하지 않을 경우 다음 작업을 수행합니다.</p>
<ul>
<li><p>다른 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>사서함 서버의 사서함 전송 서비스를 통해 사서함 데이터베이스로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>일괄 처리 지점</p></td>
<td><p>중간</p></td>
<td><p>들어오는 메시지에 대한 타피팅 지연을 시작하거나 증가시킵니다. 전체 일괄 처리 지점 기록 깊이에 대한 정상 수준에 도달하지 않을 경우 다음 작업을 수행합니다.</p>
<ul>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>일괄 처리 지점</p></td>
<td><p>높음</p></td>
<td><p>들어오는 메시지에 대한 타피팅 지연을 시작하거나 증가시킵니다. 전체 일괄 처리 지점 기록 깊이에 대한 정상 수준에 도달하지 않을 경우 다음 작업을 수행합니다.</p>
<ul>
<li><p>다른 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>사서함 서버의 사서함 전송 서비스를 통해 사서함 데이터베이스로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>EdgeTransport.exe 프로세스에 의해 사용된 메모리</p></td>
<td><p>중간</p></td>
<td><ul>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>가비지 수집을 강제합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe 프로세스에 의해 사용된 메모리</p></td>
<td><p>높음</p></td>
<td><ul>
<li><p>다른 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>사서함 서버의 사서함 전송 서비스를 통해 사서함 데이터베이스로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>모든 프로세스에 의해 사용된 메모리</p></td>
<td><p>중간</p></td>
<td><ul>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>가비지 수집을 강제합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>모든 프로세스에 의해 사용된 메모리</p></td>
<td><p>높음</p></td>
<td><ul>
<li><p>다른 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>사서함 서버의 사서함 전송 서비스를 통해 사서함 데이터베이스로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>메모리에서 향상된 DNS 캐시를 플러시합니다.</p></li>
<li><p>메시지 디하이드레이션을 시작합니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>전송 큐의 메시지 수</p></td>
<td><p>중간</p></td>
<td><p>들어오는 메시지에 대한 타피팅 지연을 시작하거나 증가시킵니다. 전체 전송 큐 기록 깊이에 대한 정상 수준에 도달하지 않을 경우 다음 작업을 수행합니다.</p>
<ul>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>가비지 수집을 강제합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>전송 큐의 메시지 수</p></td>
<td><p>높음</p></td>
<td><p>들어오는 메시지에 대한 타피팅 지연을 시작하거나 증가시킵니다. 전체 전송 큐 기록 깊이에 대한 정상 수준에 도달하지 않을 경우 다음 작업을 수행합니다.</p>
<ul>
<li><p>다른 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>사서함 서버의 사서함 전송 서비스를 통해 사서함 데이터베이스로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>비 Exchange 서버에서 들어오는 메시지를 거부합니다.</p></li>
<li><p>Pickup 및 Replay 디렉터리로부터의 메시지 전송을 거부합니다.</p></li>
<li><p>메모리에서 향상된 DNS 캐시를 플러시합니다.</p></li>
<li><p>메시지 디하이드레이션을 시작합니다.</p></li>
</ul></td>
</tr>
</tbody>
</table>


맨 위로 이동

## EdgeTransport.exe.config 파일의 역 압력 구성 옵션

역 압력에 대한 모든 구성 옵션을 %ExchangeInstallPath%Bin\\EdgeTransport.exe.config XML 응용 프로그램 구성 파일에서 사용할 수 있습니다.


> [!WARNING]
> 이러한 설정은 참조용으로만 나열되어 있습니다. EdgeTransport.exe.config 파일에서 역 압력 설정을 수정하지 않는 것이 좋습니다. 역 압력 설정을 수정하면 성능이 저하되거나 데이터가 손실될 수 있습니다. 발생 가능한 역 압력 이벤트의 근본적인 원인을 확인하여 해결하는 것이 좋습니다.



### 역 압력 구성 옵션

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>키 이름</th>
<th>기본값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>EnableResourceMonitoring</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>ResourceMonitoringInterval</em></p></td>
<td><p><code>00:00:02</code>(2초)</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. 이 값은 기본 수식이 사용됨을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. 이 값은 실제 값이 <em>PercentageDatabaseDiskSpaceUsedHighThreshold</em> 값보다 2% 더 작음을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. 이 값은 실제 값이 <em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em> 값보다 2% 더 작음을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. 이 값은 기본 수식이 사용됨을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. 이 값은 실제 값이 <em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em> 값보다 2% 더 작음을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. 이 값은 실제 값이 <em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em> 값보다 2% 더 작음을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedHighThreshold</em></p></td>
<td><p>0. 이 값은 기본 계산이 사용됨을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePrivateBytesUsedMediumThreshold</em></p></td>
<td><p>0. 이 값은 실제 값이 <em>PercentagePrivateBytesUsedHighThreshold</em> 값보다 2% 더 작음을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedNormalThreshold</em></p></td>
<td><p>0. 이 값은 실제 값이 <em>PercentagePrivateBytesUsedMediumThreshold</em> 값보다 2% 더 작음을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsHighThreshold</em></p></td>
<td><p>200</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsMediumThreshold</em></p></td>
<td><p>120</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsNormalThreshold</em></p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsHistoryDepth</em></p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointHighThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointMediumThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointNormalThreshold</em></p></td>
<td><p>1000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointUseCostForPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointBatchSize</em></p></td>
<td><p>40</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointBatchTimeout</em></p></td>
<td><p><code>00:00:00.100</code>(0.1초)</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointItemExpiryInterval</em></p></td>
<td><p><code>00:05:00</code>(5분)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPBaseThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:00</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPMaxThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:55</code>(55초)</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPStepThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:05</code>(5초)</p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPStartThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:10</code>(10초)</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePhysicalMemoryUsedLimit</em></p></td>
<td><p>94</p></td>
</tr>
<tr class="odd">
<td><p><em>DehydrateMessagesUnderMemoryPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateBytesHistoryDepth</em></p></td>
<td><p>30</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueHighThreshold</em></p></td>
<td><p>10000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueMediumThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueNormalThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 역 압력 로깅 정보

다음 목록에서는 Exchange의 특정 역 압력 이벤트에 의해 생성되는 이벤트 로그 항목에 대해 설명합니다.

  - **리소스 사용률 수준 증가에 대한 이벤트 로그 항목**
    
    이벤트 유형: 오류
    
    이벤트 원본: MSExchangeTransport
    
    이벤트 범주: 리소스 관리자
    
    이벤트 ID: 15004
    
    설명: 리소스 압력이 *이전 사용률 수준*에서 *현재 사용률 수준*으로 증가했습니다.

  - **리소스 사용률 수준 감소에 대한 이벤트 로그 항목**
    
    이벤트 유형: 정보
    
    이벤트 원본: MSExchangeTransport
    
    이벤트 범주: 리소스 관리자
    
    이벤트 ID: 15005
    
    설명: 리소스 압력이 *이전 사용률 수준*에서 *현재 사용률 수준*으로 감소했습니다.

  - **사용 가능한 디스크 공간이 매우 낮은 이벤트 로그 항목**
    
    이벤트 유형: 오류
    
    이벤트 원본: MSExchangeTransport
    
    이벤트 범주: 리소스 관리자
    
    이벤트 ID: 15006
    
    설명: 사용 가능한 디스크 공간이 구성된 임계값보다 작기 때문에 Microsoft Exchange Transport service에서 메시지를 거부하고 있습니다. 서비스에서 계속 작업하려면 관리 작업으로 디스크 공간을 비워야 할 수 있습니다.

  - **사용 가능한 메모리가 매우 낮은 이벤트 로그 항목**
    
    이벤트 유형: 오류
    
    이벤트 원본: MSExchangeTransport
    
    이벤트 범주: 리소스 관리자
    
    이벤트 ID: 15007
    
    설명: 서비스가 구성된 임계값보다 큰 메모리를 계속 사용하기 때문에 Microsoft Exchange Transport Service가 메시지 전송을 거부합니다. 정상 작업을 계속하려면 이 서비스를 다시 시작해야 할 수 있습니다.

맨 위로 이동

