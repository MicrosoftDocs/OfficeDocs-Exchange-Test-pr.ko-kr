---
title: '큐: Exchange 2013 Help'
TOCTitle: 큐
ms:assetid: e7ad0ba5-3789-4a2b-9825-6bb1b321609c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125022(v=EXCHG.150)
ms:contentKeyID: 51407762
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 큐

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

*큐*는 다음 처리 단계 또는 대상으로의 배달을 기다리는 메시지를 임시로 보관하는 위치입니다. 각 큐는 Exchange 서버가 특정 순서로 처리할 논리적 메시지 집합을 나타냅니다. Microsoft Exchange Server 2013에서 큐에는 배달 전/중/후의 메시지가 보관됩니다. 큐는 사서함 서버와 Edge 전송 서버에 있습니다. 이 항목 전체에서는 사서함 서버와 Edge 전송 서버를 *전송 서버*로 지칭합니다.

Exchange 2013에서는 이전 버전의 Exchange와 같이 큐 저장소로 단일 ESE(Extensible Storage Engine) 데이터베이스를 사용합니다.

Exchange 도구 상자의 큐 뷰어와 Exchange 관리 셸을 사용하여 큐 및 큐의 메시지를 관리할 수 있습니다. 이러한 인터페이스를 통해 큐의 상태 및 내용과 자세한 메시지 속성을 볼 수 있습니다. 또한 이러한 인터페이스를 사용하여 큐 또는 큐의 메시지를 수정하는 작업을 수행할 수 있습니다.

**목차**

  - Types of queues

  - Queue database files

  - Queue properties
    
      - NextHopSolutionKey
    
      - IncomingRate, OutgoingRate, and Velocity
    
      - Queue status
    
      - Other queue properties

  - Message properties
    
      - Message status
    
      - Other message properties

  - Manage queues and messages in queues

## 큐 유형

Exchange 2013에서는 다음과 같은 유형의 큐가 사용됩니다.

  - **영구 큐**   *영구 큐*는 모든 Exchange 조직의 모든 전송 서버에 있는 큐입니다. Exchange 2013에는 이전 버전의 Exchange와 같이 세 가지 영구 큐가 있습니다.
    
      - **전송 큐**   전송 큐는 분류기에서 전송 서버의 전송 에이전트가 확인, 라우팅 및 처리해야 하는 모든 메시지를 수집하는 데 사용됩니다. 전송 서버에서 검색된 모든 메시지는 전송 큐에서 처리됩니다. 사서함 서버의 메시지는 수신 커넥터, Pickup/Replay 디렉터리 또는 사서함 전송 서비스를 통해 전송됩니다. Edge 전송 서버의 메시지는 일반적으로 수신 커넥터를 통해 전송되지만 Pickup 및 Replay 디렉터리도 사용할 수 있습니다.
        
        분류기는 이 큐에서 메시지를 검색하고 그 중에서 특히 받는 사람의 위치와 해당 위치에 대한 경로를 확인합니다. 분류 후에는 메시지가 배달 큐 또는 연결할 수 없는 큐로 이동합니다. 각 전송 서버에는 전송 큐가 하나씩만 있습니다. 전송 큐에 있는 메시지는 동시에 다른 큐에 있을 수 없습니다. 분류기 및 전송 파이프라인에 대한 자세한 내용은 [메일 흐름](mail-flow-exchange-2013-help.md)을 참조하십시오.
    
      - **연결할 수 없는 큐**   연결할 수 없는 큐에는 해당 대상으로 라우팅할 수 없는 메시지가 들어 있습니다. 일반적으로 배달할 라우팅 경로를 수정하는 등 구성을 변경하면 대상에 연결할 수 없게 됩니다. 대상에 관계 없이 받는 사람에게 연결할 수 없는 모든 메시지는 이 큐에 보관됩니다. 각 전송 서버에는 연결할 수 없는 큐가 하나씩만 있습니다.
        
        라우팅 변경이 검색되면 연결할 수 없는 큐의 메시지는 자동으로 다시 전송됩니다. 따라서 메시지가 연결할 수 없는 큐에 보관되도록 한 조건 또는 구성 오류가 복구된 후 추가 작업을 수행하여 배달을 위해 연결할 수 없는 큐 외부로 메시지를 이동할 필요가 없습니다.
        
        연결할 수 없는 큐는 일반적으로 비어 있습니다. 메시지를 포함하지 않는 연결할 수 없는 큐는 큐 뷰어 또는 **Get-Queue** 결과에 표시되지 않습니다.
    
      - **포이즌 메시지 큐**   포이즌 메시지 큐는 전송 서버 또는 서비스 오류가 발생한 후 Exchange 2013 시스템에 해로운 것으로 확인된 메시지를 격리하는 데 사용되는 특수한 큐입니다. 이 메시지의 콘텐츠와 형식이 실제로도 해로울 수 있습니다. 아니면, 잘못 작성된 에이전트의 결과일 수도 있는데, Exchange 서버가 잘못된 메시지를 처리할 때 이 에이전트로 인해 Exchange 서버에 오류가 발생하는 것입니다.
        
        포이즌 메시지 큐는 일반적으로 비어 있습니다. 메시지를 포함하지 않는 포이즌 메시지 큐는 큐 뷰어 또는 **Get-Queue** 결과에 표시되지 않습니다. 자동으로 다시 시작되거나 만료되지 않습니다. 포이즌 메시지 큐의 메시지는 관리자가 수동으로 다시 시작하거나 제거할 때까지 남아 있습니다.

  - **배달 큐**   배달 큐는 SMTP를 사용하여 로컬 또는 원격 서버로 배달 중인 메시지를 보관합니다. 모든 메시지는 SMTP를 사용하여 Exchange 서버 간에 전송됩니다. 배달 에이전트 커넥터에서 대상에 서비스를 제공하는 경우에는 비 SMTP 대상에서도 배달 큐를 사용합니다. . 각 배달 큐에는 같은 대상으로 라우팅 중인 메시지가 포함됩니다. 전송 서버에는 보통 배달 큐가 여러 개 있습니다. 배달 큐는 필요할 때 동적으로 만들어지며 큐가 비워지고 만료 시간이 지나면 자동으로 삭제됩니다. 큐 만료 시간은 **Set-TransportService** cmdlet의 *QueueMaxIdleTime* 매개 변수를 통해 제어됩니다. 기본값은 3분입니다.

  - **섀도 큐**   섀도 큐에는 전송 중인 메시지의 중복 복사본이 보관됩니다. 자세한 내용은 [섀도 중복성](shadow-redundancy-exchange-2013-help.md)을 참조하십시오.

  - **보안 네트워크**   보안 네트워크에는 전송 서버가 배달한 메시지의 복사본이 보관됩니다. 큐 관리 도구에서 보안 네트워크에 액세스할 수는 없지만, 보안 네트워크는 큐 데이터베이스의 큐 중 하나로 보면 됩니다. 자세한 내용은 [보안 네트워크](safety-net-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 큐 데이터베이스 파일

모든 다른 큐는 단일 ESE 데이터베이스에 저장됩니다. 이 큐 데이터베이스는 기본적으로 전송 서버의 `%ExchangeInstallPath%TransportRoles\data\Queue`에 있습니다.

ESE 데이터베이스와 마찬가지로 큐 데이터베이스는 로그 파일을 사용하여 데이터를 수락, 추적 및 유지 관리합니다. 성능을 향상시키기 위해 모든 메시지 트랜잭션이 먼저 로그 파일과 메모리에 기록된 후 데이터베이스 파일에 기록됩니다. 검사점 파일은 데이터베이스에 커밋된 트랜잭션 로그 항목을 추적합니다. Microsoft Exchange 전송 서비스를 정상적으로 종료하는 동안에는 트랜잭션 로그에 있는 커밋되지 않은 데이터베이스 변경 내용이 항상 데이터베이스에 커밋됩니다.

큐 데이터베이스에는 순환 로깅이 사용됩니다. 즉, 트랜잭션 로그에 있는 커밋된 트랜잭션 기록은 유지 관리되지 않습니다. 현재 검사점보다 오래된 트랜잭션 로그는 즉시 자동으로 삭제되므로, 큐 데이터베이스 복구를 위해 백업에서 트랜잭션 로그를 재생할 수 없습니다.

Exchange 2013에서는 *생성 테이블*을 사용하여 큐 데이터베이스의 메시지를 저장 및 정리합니다. 큐 데이터베이스에서는 큰 테이블 하나에서 개별 메시지 레코드를 처리 및 삭제하는 대신에 시간 기반 테이블에 메시지를 저장하고 해당 테이블의 모든 메시지가 처리된 후에 해당 전체 테이블만 삭제합니다. 예를 들어 큐 또는 대상에 관계없이 오후 1시~2시 사이에 큐에 대기한 모든 메시지는 `1p-2p_msgs` 테이블에 저장됩니다. 오후 2시부터는 새 메시지가 `2p-3p_msgs` 테이블에 저장됩니다. 그리고 오후 4시가 되면 `4p-5p_msgs` 테이블이 새로 만들어지며 해당 테이블의 모든 메시지가 처리된 경우에 한해 전체 `1p-2p_msgs` 테이블이 삭제됩니다. 이처럼 개별 메시지가 아닌 전체 메시지 테이블을 삭제하는 방식을 사용하면 큐 데이터베이스가 포함된 드라이브의 I/O 성능 개선에 도움이 됩니다.

다음 표에서는 큐 데이터베이스를 구성하는 파일을 보여줍니다.

### 큐 데이터베이스를 구성하는 파일

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>파일</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.que</p></td>
<td><p>이 큐 데이터베이스 파일은 대기 중인 모든 메시지를 저장합니다.</p></td>
</tr>
<tr class="even">
<td><p>Tmp.edb</p></td>
<td><p>이 임시 데이터베이스 파일은 시작 시에 큐 데이터베이스 스키마를 확인하는 데 사용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>Trn*.log</p></td>
<td><p>이 트랜잭션 로그는 큐 데이터베이스에 대한 모든 변경 내용을 기록합니다. 데이터베이스의 모든 변경 내용은 먼저 트랜잭션 로그에 기록된 후 데이터베이스에 커밋됩니다. Trn.log는 현재 활성 트랜잭션 로그 파일입니다. Trntmp.log는 다음에 프로비전되는 미리 만들어진 트랜잭션 로그 파일입니다. 기존 Trn.log 트랜잭션 로그 파일은 최대 크기에 도달하면 Trn.log가 Trn<em>nnnn</em>.log로 이름이 바뀝니다. 여기서 <em>nnnn</em>은 시퀀스 번호입니다. 그런 다음 Trntmp.log는 Trn.log로 이름이 바뀌어 현재의 활성 트랜잭션 로그 파일이 됩니다.</p></td>
</tr>
<tr class="even">
<td><p>Trn.chk</p></td>
<td><p>이 검사점 파일은 데이터베이스에 커밋된 트랜잭션 로그 항목을 추적합니다. 이 파일은 항상 mail.que 파일과 같은 위치에 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>Trnres00001.jrs</p>
<p>Trnres00002.jrs</p></td>
<td><p>이러한 예약 트랜잭션 로그 파일은 자리 표시자의 역할을 하며 트랜잭션 로그가 포함된 하드 디스크에 공간이 부족하여 큐 데이터베이스가 완전히 중지될 때만 사용됩니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 큐 데이터베이스 구성 옵션

`%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML 응용 프로그램 구성 파일에서 키를 추가하거나 수정하여 큐 데이터베이스를 구성합니다. 이 파일은 Microsoft Exchange Transport Service와 연결되어 있습니다. EdgeTransport.exe.config 파일에 대한 변경 내용은 Microsoft Exchange Transport Service를 다시 시작하고 나면 적용됩니다.

EdgeTransport.exe.config 파일의 `<appSettings>` 섹션에서 새 키를 추가하거나 기존 키를 수정할 수 있습니다. 특정 키가 없으면 수동으로 추가하여 해당 값을 변경할 수 있습니다.

다음 표에는 EdgeTransport.exe.config 파일에서 사용할 수 있는 큐 데이터베이스의 키에 대한 설명이 나와 있습니다.

### EdgeTransport.exe.config 파일에서 사용할 수 있는 메시지 큐 데이터베이스 키

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>키</th>
<th>기본값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabaseBatchSize</em></p></td>
<td><p>40</p></td>
<td><p>이 키는 데이터베이스 I/O 작업을 실행하기 전에 함께 그룹화될 수 있는 해당 작업의 수를 지정합니다. 이 키는 기본적으로 EdgeTransport.exe.config 파일에 없습니다.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseBatchTimeout</em></p></td>
<td><p>100</p></td>
<td><p>이 키는 데이터베이스가 여러 데이터베이스 I/O 작업을 실행하기 전에 해당 작업이 그룹화될 때까지 대기하는 최대 시간(밀리초)을 지정합니다. 데이터베이스 I/O 작업은 다음 조건을 만족할 때 더 이상 대기하지 않고 실행됩니다.</p>
<ul>
<li><p><em>QueueDatabaseBatchSize</em> 키로 지정된 데이터베이스 I/O 작업 수에 도달하지 않은 경우</p></li>
<li><p><em>QueueDatabaseBatchTimeout</em> 키로 지정된 시간이 경과한 경우</p></li>
</ul>
<p>이 키는 기본적으로 EdgeTransport.exe.config 파일에 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxConnections</em></p></td>
<td><p>4</p></td>
<td><p>이 키는 열 수 있는 ESE 데이터베이스 연결 수를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingBufferSize</em></p></td>
<td><p>5MB</p></td>
<td><p>이 키는 트랜잭션 로그 파일에 기록되기 전에 트랜잭션 레코드를 캐시하는 데 사용되는 메모리를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseLoggingFileSize</em></p></td>
<td><p>5MB</p></td>
<td><p>이 키는 트랜잭션 로그 파일의 최대 크기를 지정합니다. 최대 로그 파일 크기에 도달하면 새 로그 파일이 열립니다.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>이 키는 큐 데이터베이스 로그 파일의 기본 디렉터리를 지정합니다. 큐 데이터베이스의 위치를 변경하는 방법에 대한 지침은 <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">큐 데이터베이스의 위치를 변경 합니다.</a>을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxBackgroundCleanupTasks</em></p></td>
<td><p>32</p></td>
<td><p>이 키는 언제든지 데이터베이스 엔진 스레드 풀에 대기될 수 있는 백그라운드 정리 작업 항목의 최대 수를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragEnabled</em></p></td>
<td><p>True</p></td>
<td><p>이 키는 메일 큐 데이터베이스의 예약된 온라인 조각 모음을 사용하도록 설정하거나 사용하지 않도록 설정합니다. 이 키는 기본적으로 EdgeTransport.exe.config 파일에 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseOnlineDefragSchedule</em></p></td>
<td><p><code>1:00:00</code>(오전 1시)</p></td>
<td><p>이 키는 메일 큐 데이터베이스의 온라인 조각 모음을 시작하는 시간을 24시간 형식으로 지정합니다. 값을 지정하려면 해당 값을 시간, 즉 <em>hh:mm:ss</em>와 같이 입력합니다. 여기서 <em>h</em> = 시간, <em>m</em> = 분, <em>s</em> = 초를 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragTimeToRun</em></p></td>
<td><p><code>3:00:00</code>(3시간)</p></td>
<td><p>이 키는 온라인 조각 모음 작업의 실행이 허용되는 시간을 지정합니다. 조각 모음 작업이 지정된 시간 안에 완료되지 않아도 큐 데이터베이스는 일관성 있는 상태를 유지합니다. 값을 지정하려면 해당 값을 기간, 즉 <em>hh:mm:ss</em>와 같이 입력합니다. 여기서 <em>h</em> = 시간, <em>m</em> = 분, <em>s</em> = 초를 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>이 키는 큐 데이터베이스 파일의 기본 디렉터리를 지정합니다. 큐 데이터베이스의 위치를 변경하는 방법에 대한 지침은 <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">큐 데이터베이스의 위치를 변경 합니다.</a>을 참조하십시오.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 파일 또는 사서함 서버의 EdgeTransport.exe.config 파일)에 설정하는 사용자 지정된 모든 서버 단위 설정은 Exchange CU(누적 업데이트)를 설치하면 덮어쓰게 됩니다. 설치 후 서버를 쉽게 다시 구성할 수 있도록 이 정보를 저장했는지 확인하세요. 이러한 설정은 Exchange CU를 설치한 후에 다시 구성해야 합니다.



맨 위로 이동

## 큐 속성

큐에는 큐 상태와 용도를 설명하는 여러 속성이 있습니다. 큐를 만들 때 큐에 적용되어 변경되지 않는 큐 속성도 있고, 자주 업데이트되는 상태 크기, 시간 또는 기타 지표를 포함하는 큐 속성도 있습니다.

맨 위로 이동

## NextHopSolutionKey

Microsoft Exchange Transport Service의 분류기 라우팅 구성 요소는 메시지 대상을 선택하고, 이 대상은 배달 큐를 만드는 데 사용됩니다. 대상은 모든 받는 사람에 대해 **NextHopSolutionKey** 특성으로 스탬프 처리됩니다. **NextHopSolutionKey** 특성의 모든 고유한 값은 개별 배달 큐에 해당합니다.

**NextHopSolutionKey** 특성에는 다음 필드가 들어 있습니다.

  - **DeliveryType**   이 필드의 값은 메시지 분류 결과 및 전송 서비스에서 다음 홉(메시지의 최종 대상 또는 도중의 중간 홉일 수 있음)으로 메시지를 전송하는 방법을 나타냅니다. 전송 서비스는 해당하는 라우팅 대상 또는 배달 그룹에 따라 **DeliveryType**에 미리 정의된 값 목록을 사용합니다.

  - **NextHopDomain**   이 필드는 **DeliveryType** 필드의 값에 따라 특정 값을 사용합니다. 배달 큐의 경우 이 필드의 값은 큐의 이름입니다. **NextHopDomain**의 값이 항상 도메인 이름인 것은 아닙니다. 예를 들어 해당 값은 대상 Active Directory 사이트 또는 DAG(데이터베이스 사용 가능 그룹)의 이름이 될 수 있습니다. 이 필드는 다음 홉 이름으로 간주할 수 있으며 해당 값은 라우팅 대상 또는 대상 배달 그룹의 이름입니다.

  - **NextHopConnector**   이 필드는 **DeliveryType** 필드의 값에 따라 특정 값을 사용합니다. 해당 값은 항상 GUID로 표시됩니다. 이 필드를 사용하지 않으면 값은 0만 포함된 GUID가 됩니다. **NextHopConnector**의 값이 항상 커넥터의 GUID인 것은 아닙니다. 예를 들어 해당 값은 대상 Active Directory 사이트 또는 DAG의 GUID가 될 수 있습니다. 이 필드는 다음 홉 GUID로 간주할 수 있으며 해당 값은 라우팅 대상 또는 대상 배달 그룹의 GUID입니다.

Exchange 2013에서는 **DeliveryType**의 값에 따라 **NextHopCategory** 속성도 큐에 추가합니다. **NextHopCategory**의 값은 `External` 또는 `Internal`입니다. `External` 값은 큐의 다음 홉이 Exchange 조직 외부에 있음을 나타내고, `Internal` 값은 큐의 다음 홉이 Exchange 조직 내부에 있음을 나타냅니다. 외부 받는 사람에 대한 메시지를 외부로 배달하려면 내부 홉이 하나 이상 필요할 수 있습니다.

다음 표에는 **DeliveryType**, **NextHopCategory**, **NextHopDomain** 및 **NextHopConnector**의 값에 대한 설명이 나와 있습니다.


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
<th>큐 뷰어의 배달 유형</th>
<th>셸의 DeliveryType</th>
<th>설명</th>
<th>NextHopCategory</th>
<th>NextHopDomain</th>
<th>NextHopConnector</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>배달 에이전트</strong></p></td>
<td><p><strong>DeliveryAgent</strong></p></td>
<td><p>비 SMTP 주소 공간의 받는 사람에게 배달할 메시지가 큐에 보관됩니다. 메시지는 로컬 서버에 구성된 배달 에이전트 커넥터를 사용하여 배달됩니다.</p></td>
<td><p>External</p></td>
<td><p>이 값은 배달 에이전트 커넥터에 구성된 대상 주소 공간입니다.</p></td>
<td><p>이 값은 배달 에이전트 커넥터의 GUID입니다. 예: <code>4520e633-d83d-411a-bbe4-6a84648674ee</code></p></td>
</tr>
<tr class="even">
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p>SMTP 주소 공간의 받는 사람에게 배달할 메시지가 큐에 보관됩니다. 메시지는 로컬 서버에 구성된 송신 커넥터를 사용하여 배달됩니다. 송신 커넥터는 DNS 라우팅을 사용하도록 구성됩니다.</p></td>
<td><p>External</p></td>
<td><p>이 값은 송신 커넥터에 구성된 대상 주소 공간입니다. 예: <code>contoso.com</code></p></td>
<td><p>이 값은 송신 커넥터의 GUID입니다. 예: <code>4520e633-d83d-411a-bbe4-6a84648674ee</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p>비 SMTP 주소 공간의 받는 사람에게 배달할 메시지가 큐에 보관됩니다. 메시지는 로컬 서버에 구성된 외부 커넥터를 사용하여 배달됩니다.</p></td>
<td><p>External</p></td>
<td><p>이 값은 외부 커넥터에 구성된 대상 주소 공간입니다.</p></td>
<td><p>이 값은 외부 커넥터의 GUID입니다. 예: <code>4520e633-d83d-411a-bbe4-6a84648674ee</code></p></td>
</tr>
<tr class="even">
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p>SMTP 주소 공간의 받는 사람에게 배달할 메시지가 큐에 보관됩니다. 메시지는 로컬 서버에 구성된 송신 커넥터를 사용하여 배달됩니다. 송신 커넥터는 스마트 호스트 라우팅을 사용하도록 구성됩니다.</p></td>
<td><p>External</p></td>
<td><p>이 값은 송신 커넥터에 구성된 스마트 호스트의 목록입니다. 스마트 호스트는 FQDN이나 IP 주소, 또는 둘 다로 구성할 수 있습니다. 값은 다음 중 하나일 수 있습니다.</p>
<ul>
<li><p><strong>FQDN</strong>   구문은 <code>&lt;FQDN1,FQDN2,...&gt;</code>입니다. 예: <code>smarthost01.contoso.com</code> 또는 <code>smarthost01.contoso.com,smarthost02.fabrikam.com</code></p></li>
<li><p><strong>IP 주소</strong>   구문은 <code>&lt;[IPAddress1],[IPAddress2],...&gt;</code>입니다. 예: <code>[10.10.10.100]</code> 또는 <code>[10.10.10.100],[10.10.10.101]</code></p></li>
<li><p><strong>FQDN 및 IP 주소</strong>   구문은 <code>&lt;[IPAddress1],FQDN1,...&gt;</code>이며 스마트 호스트가 송신 커넥터에 나열되는 방식에 따라 달라집니다. 예: <code>[172.17.17.7],relay.tailspintoys.com</code> 또는 <code>mail.contoso.com,[192.168.1.50]</code></p></li>
</ul></td>
<td><p>이 값은 송신 커넥터의 GUID입니다. 예: <code>4520e633-d83d-411a-bbe4-6a84648674ee</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>사서함에 대한 SMTP 배달</strong></p></td>
<td><p><strong>SmtpDeliveryToMailbox</strong></p></td>
<td><p>Exchange 2013 사서함 받는 사람에게 배달할 메시지가 큐에 보관됩니다. 대상 사서함 데이터베이스는 다음 위치 중 한 곳에 있습니다.</p>
<ul>
<li><p>로컬 Exchange 2013 사서함 서버</p></li>
<li><p>같은 DAG의 Exchange 2013 사서함 서버</p></li>
<li><p>비 DAG 환경의 같은 Active Directory 사이트에 있는 Exchange 2013 사서함 서버</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>이 값은 대상 사서함 데이터베이스의 이름입니다. 예: <code>Mailbox Database 0471695037</code></p></td>
<td><p>이 값은 대상 사서함 데이터베이스의 GUID입니다. 예: <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code></p></td>
</tr>
<tr class="even">
<td><p><strong>송신 커넥터 원본 서버에 대한 SMTP 릴레이</strong></p></td>
<td><p><strong>SmtpRelayToConnectorSourceServers</strong></p></td>
<td><p>SMTP 또는 비 SMTP 받는 사람에게 배달할 메시지가 큐에 보관됩니다. 메시지는 원격 전송 서버에 구성된 송신 커넥터, 배달 에이전트 커넥터 또는 외부 커넥터를 사용하여 배달됩니다. 원격 전송 서버는 Exchange 2013 사서함 서버나 이전 버전 Exchange의 Exchange 2007 또는 Exchange 2010 허브 전송 서버일 수 있습니다. 원격 서버는 로컬 또는 원격 Active Directory 사이트에 있을 수 있습니다.</p></td>
<td><p>Internal</p></td>
<td><p>이 값은 대상 송신 커넥터, 배달 에이전트 커넥터 또는 외부 커넥터의 이름입니다. 예: <code>Contoso.com Send Connector</code></p></td>
<td><p>이 값은 대상 송신 커넥터, 배달 에이전트 커넥터 또는 외부 커넥터의 GUID입니다. 예: <code>4520e633-d83d-411a-bbe4-6a84648674ee</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>데이터베이스 사용 가능 그룹에 대한 SMTP 릴레이</strong></p></td>
<td><p><strong>SmtpRelayToDag</strong></p></td>
<td><p>Exchange 2013 사서함 받는 사람에게 배달할 메시지가 큐에 보관됩니다. 대상 사서함 데이터베이스는 원격 DAG에 있습니다. 원격 DAG는 로컬 또는 원격 Active Directory 사이트에 있을 수 있습니다.</p></td>
<td><p>Internal</p></td>
<td><p>이 값은 대상 DAG의 이름입니다. 예: <code>DAG1</code></p></td>
<td><p>이 값은 대상 DAG의 GUID입니다. 예: <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code></p></td>
</tr>
<tr class="even">
<td><p><strong>사서함 배달 그룹에 대한 SMTP 릴레이</strong></p></td>
<td><p><strong>SmtpRelayToMailboxDeliveryGroup</strong></p></td>
<td><p>레거시 사서함 받는 사람에게 배달할 메시지가 큐에 보관됩니다. 대상 사서함은 Exchange 2007 또는 Exchange 2010 사서함 서버에 있습니다. 메시지는 대상 사서함과 같은 Exchange 버전을 실행하는 허브 전송 서버와 관련됩니다. 대상 허브 전송 서버는 로컬 또는 원격 Active Directory 사이트에 있을 수 있습니다.</p></td>
<td><p>Internal</p></td>
<td><p>큐 이름은 <code>Site:&lt;ADSiteName&gt;;Version:&lt;ExchangeVersion&gt;</code> 구문을 사용합니다. 여기서 <em>&lt;ADSiteName&gt;</em>은 대상 Active Directory 사이트의 이름이고 <em>&lt;ExchangeVersion&gt;</em>은 사서함 서버의 Exchange 버전입니다.</p></td>
<td><p>이 값은 비어 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>원격 Active Directory 사이트에 대한 SMTP 릴레이</strong></p></td>
<td><p><strong>SmtpRelayToRemoteActiveDirectorySite</strong></p></td>
<td><p>원격 대상으로 배달할 메시지가 큐에 보관됩니다. 라우팅 토폴로지에서는 특정 Active Directory 사이트를 통해 메시지를 라우팅하도록 요구합니다. 이 사이트는 최종 대상으로 이동하는 도중의 중간 홉입니다. 다음과 같은 경우 이러한 상황이 발생합니다.</p>
<ul>
<li><p>허브 사이트를 통해 메시지를 라우팅해야 하는 경우</p></li>
<li><p>원격 Active Directory 사이트를 구독하는 Edge 전송 서버에 구성된 송신 커넥터를 통해 메시지를 배달해야 하는 경우</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>이 값은 대상 Active Directory 사이트 이름입니다. 예: <code>NorthAmericanSite</code></p></td>
<td><p>이 값은 대상 Active Directory의 GUID입니다. 예: <code>bfd6c3df-5b65-8bfb-53f1f2c0d55c</code></p></td>
</tr>
<tr class="even">
<td><p><strong>지정된 Exchange Server에 대한 SMTP 릴레이</strong></p></td>
<td><p><strong>SmtpRelayToServers</strong></p></td>
<td><p>특정 확장 서버용으로 구성된 메일 그룹으로 배달할 메시지가 큐에 보관됩니다. 확장 서버는 Exchange 2013 사서함 서버나 Exchange 2007 또는 Exchange 2010 허브 전송 서버일 수 있습니다. 해당 서버는 로컬 또는 원격 Active Directory 사이트에 있을 수 있습니다.</p></td>
<td><p>Internal</p></td>
<td><p>이 값은 대상 확장 서버의 FQDN입니다. 예: <code>mailbox01.contoso.com</code></p></td>
<td><p>이 값은 <code>00000000-0000-0000-0000-000000000000</code>입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Active Directory 사이트에서 Edge 전송 서버로 SMTP 릴레이</strong></p></td>
<td><p><strong>SmtpRelayWithinAdSiteToEdge</strong></p></td>
<td><p>SMTP 주소 공간으로 배달할 메시지가 큐에 보관됩니다. 메시지는 로컬 Active Directory 사이트를 구독하는 Edge 전송 서버에 구성된 송신 커넥터를 사용하여 배달됩니다.</p></td>
<td><p>Internal</p></td>
<td><p>이 값은 조직에서 인터넷으로 아웃바운드 인터넷 메일을 보내는 송신 커넥터의 이름입니다. 이 송신 커넥터는 Edge 구독에서 자동으로 만들어지며 <code>EdgeSync - &lt;ADSiteName&gt; to Internet</code>으로 이름이 지정됩니다. <em>&lt;ADSiteName&gt;</em>은 Edge 전송 서버를 구독하는 로컬 Active Directory 사이트의 이름입니다.</p></td>
<td><p>이 값은 송신 커넥터의 GUID입니다. 예: <code>4520e633-d83d-411a-bbe4-6a84648674ee</code></p></td>
</tr>
<tr class="even">
<td><p><strong>하트비트</strong></p></td>
<td><p><strong>하트비트</strong></p></td>
<td><p>이 값은 Microsoft 내부에서 사용하도록 예약되어 있습니다. 하트비트에 대한 자세한 내용은 <a href="shadow-redundancy-exchange-2013-help.md">섀도 중복성</a>을 참조하십시오.</p></td>
<td><p>해당 없음</p></td>
<td><p>해당 없음</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p><strong>섀도 중복성</strong></p></td>
<td><p><strong>ShadowRedundancy</strong></p></td>
<td><p>섀도 큐의 메시지가 큐에 보관됩니다. 섀도 큐는 기본 메시지가 배달되지 않을 경우에 대비해 전송 중인 메시지의 중복 복사본을 보관합니다. 자세한 내용은 <a href="shadow-redundancy-exchange-2013-help.md">섀도 중복성</a>을 참조하십시오.</p></td>
<td><p>Internal</p></td>
<td><p>이 값은 섀도 큐가 기본 메시지의 중복 복사본을 보관하는 기본 서버의 FQDN입니다. 예: <code>mailbox01.contoso.com</code></p></td>
<td><p>이 값은 <code>00000000-0000-0000-0000-000000000000</code>입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>정의되지 않음</strong></p></td>
<td><p><strong>정의되지 않음</strong></p></td>
<td><p>이 값은 전송 큐 및 포이즌 메시지 큐에서만 사용됩니다.</p></td>
<td><p>Internal</p></td>
<td><p>전송 큐의 경우 이 값은 <code>Submisssion</code>이고, 포이즌 메시지 큐의 경우 이 값은 <code>Poison Message</code>입니다.</p></td>
<td><p>이 값은 <code>00000000-0000-0000-0000-000000000000</code>입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>연결할 수 없음</strong></p></td>
<td><p><strong>연결할 수 없음</strong></p></td>
<td><p>이 값은 연결할 수 없는 큐에서만 사용됩니다.</p></td>
<td><p>Internal</p></td>
<td><p>이 값은 <code>Unreachable Domain</code>입니다.</p></td>
<td><p>이 값은 <code>00000000-0000-0000-0000-000000000000</code>입니다.</p></td>
</tr>
</tbody>
</table>


Exchange 2013에서는 이전 Exchange 버전과의 호환성을 위해 **DeliveryType**의 레거시 값을 지원합니다. 이러한 값은 큐 뷰어와 셸에서 사용 가능하지만 Exchange 2013에서는 사용되지 않습니다. 이러한 레거시 **DeliveryType** 값은 다음과 같습니다.

  - **MapiDelivery**   Exchange 2007 또는 Exchange 2010 허브 전송 서버가 로컬 Active Directory 사이트의 Exchange 2007 또는 Exchange 2010 사서함 서버에 있는 사서함으로 배달할 메시지가 큐에 보관됩니다.

  - **SmtpRelayWithinAdSite**   Exchange 2007 또는 Exchange 2010 허브 전송 서버가 동일한 Active Directory 사이트에 있는 다른 허브 전송 서버로 배달할 메시지가 큐에 보관됩니다. 대상 허브 전송 서버는 커넥터의 원본 서버 또는 메일 그룹 확장 서버일 수 있습니다.

  - **SmtpRelaytoTiRg**   Exchange 2007 또는 Exchange 2010 허브 전송 서버가 Exchange Server 2003 라우팅 그룹으로 배달할 메시지가 큐에 보관됩니다. 대상 서버는 커넥터의 원본 서버, 메일 그룹 확장 서버 또는 Exchange 2003 브리지헤드 서버일 수 있습니다.

맨 위로 이동

## IncomingRate, OutgoingRate, Velocity

Exchange 2013에서는 큐로 들어오고 큐에서 나가는 메시지의 속도를 측정한 다음 이러한 값을 큐 속성에 저장합니다. 이러한 속도를 큐 및 전송 서버 상태의 지표로 사용할 수 있습니다. 속성은 다음과 같습니다.

  - **IncomingRate**   이 속성은 메시지가 큐로 들어오는 속도입니다.
    
    지난 60초 동안 5초마다 큐로 들어온 메시지 수의 평균으로 이 값을 계산합니다. 수식은 `(i1+i2+i3+i4+i5+i6)/6`으로 표시할 수 있습니다. 여기서 i*n*은 5초 동안 들어온 메시지의 수입니다.

  - **OutgoingRate**   이 속성은 메시지가 큐에서 나가는 속도입니다.
    
    지난 60초 동안 5초마다 큐에서 나간 메시지 수의 평균으로 이 값을 계산합니다. 수식은 `(o1+o2+o3+o4+o5+o6)/6`으로 표시할 수 있습니다. 여기서 o*n*은 5초 동안 나간 메시지의 수입니다.

  - **Velocity**   이 속성은 큐의 드레이닝 속도로,**OutgoingRate** 값에서 **IncomingRate** 값을 빼서 계산합니다.
    
    **Velocity**의 값이 0보다 크면 메시지가 큐에서 나가는 속도가 큐로 들어오는 속도보다 더 빠른 것입니다.
    
    **Velocity**의 값이 0이면 메시지가 큐에서 나가는 속도와 큐로 들어오는 속도가 같은 것입니다. 큐가 비활성 상태일 때도 이 값은 0입니다.
    
    **Velocity**의 값이 0보다 작으면 메시지가 큐에서 나가는 속도보다 큐로 들어오는 속도가 더 빠른 것입니다.

기본 수준에서 **Velocity**의 값이 양수이면 드레이닝이 효율적으로 수행되는 정상 상태의 큐이고, **Velocity**의 값이 음수이면 큐의 드레이닝이 효율적이지 못한 것입니다. 그러나 큐의 **Velocity** 값 크기와 함께 **IncomingRate**, **OutgoingRate** 및 **MessageCount** 속성의 값도 고려해야 합니다. 예를 들어 큐에서 **Velocity**의 값은 큰 음수이고 **MessageCount** 값과 **IncominRate** 값이 크며 **OutgoingRate** 값은 작은 경우에는 큐가 적절하게 드레이닝되지 않음을 명확하게 파악할 수 있습니다. 반면 큐에서 **Velocity** 값이 0에 매우 가까운 음수이고 **IncomingRate**, **OutgoingRate**, **MessageCount** 값도 모두 매우 작으면 큐에 문제가 없는 것입니다.

맨 위로 이동

## 큐 상태

큐의 현재 상태는 큐의 **Status** 속성에 저장됩니다. 큐의 상태 값은 다음 중 하나일 수 있습니다.

  - **Active**   큐에서 현재 메시지를 전송하고 있습니다.

  - **Connecting**   큐가 다음 홉에 연결하는 중입니다.

  - **Ready**   큐가 최근에 메시지를 전송했으나 현재는 비어 있습니다.

  - **Retry**   마지막 자동 또는 수동 연결 시도가 실패했으며 큐가 연결을 다시 시도하려고 대기 중입니다.

  - **Suspended**   메시지 배달을 차단하기 위해 관리자가 수동으로 큐를 일시 중단했습니다. 새 메시지가 큐로 들어올 수 있으며 다음 홉으로 전송 중인 메시지는 배달을 마치고 큐에서 나갑니다. 그렇지 않으면 관리자가 큐를 수동으로 다시 시작할 때까지 메시지가 큐에서 나가지 않습니다. 큐를 일시 중단해도 큐의 개별 메시지 상태는 변경되지 않습니다.
    
    상태가 Active 또는 Retry인 큐를 일시 중단할 수 있습니다. 연결할 수 없는 큐와 전송 큐도 일시 중단할 수 있습니다.
    
    연결할 수 없는 큐를 일시 중단하면 구성 업데이트가 검색되어도 메시지가 자동으로 분류기에 다시 전송되지 않습니다. 이러한 메시지를 자동으로 다시 전송하려면 연결할 수 없는 큐를 수동으로 다시 시작해야 합니다. 전송 큐를 일시 중단할 경우 큐를 다시 시작해야만 분류기에서 메시지를 선택합니다.

맨 위로 이동

## 기타 큐 속성

이름을 통해 용도를 확인할 수 있는 기타 큐 속성이 있습니다. 대부분의 큐 속성은 필터 옵션으로 사용됩니다. 필터 기준을 지정하면 큐를 신속하게 찾아서 조치를 취할 수 있습니다. 필터링 가능한 큐 속성에 대한 자세한 내용은 [큐 필터입니다.](queue-filters-exchange-2013-help.md)을 참조하십시오.

여기서는 큐에 포함된 메시지의 수를 보여주는 중요한 큐 속성인 **MessageCount** 속성에 대해 설명하겠습니다. 이 속성은 큐 상태를 나타내는 중요한 지표입니다. 예를 들어 메시지를 많이 포함하는 배달 큐가 줄어들지 않고 계속 확장되는 경우 확인이 필요한 라우팅 또는 전송 파이프라인 문제가 있을 수 있습니다.

맨 위로 이동

## 메시지 속성

큐의 메시지에는 여러 속성이 포함되어 있습니다. 대부분의 속성은 메시지를 작성하는 데 사용된 정보를 반영합니다. 큐에 있는 해당 속성의 영향을 크게 받는 메시지 상태 및 정보 속성도 있습니다. 그러나 개별 메시지의 값은 큐의 해당 속성 값과 다를 수 있습니다. 자주 업데이트되는 상태, 시간 또는 기타 지표를 포함하는 속성도 있습니다.

맨 위로 이동

## 메시지 상태

메시지의 현재 상태는 메시지의 **Status** 속성에 저장됩니다. 메시지의 상태 값은 다음 중 하나입니다.

  - **Active**   메시지가 배달 큐에 있으면 대상으로 배달됩니다. 메시지가 전송 큐에 있으면 분류기에 의해 처리됩니다.

  - **Locked**   이 값은 Microsoft 내부에서 사용하도록 예약되어 있으며 온-프레미스 Exchange 조직에서는 사용되지 않습니다.

  - **PendingRemove**   이미 다음 홉으로 전송되는 중인 메시지를 관리자가 삭제했습니다. 배달 시에 오류가 발생하여 메시지가 큐에 다시 들어가게 되는 경우 해당 메시지는 삭제됩니다. 그렇지 않은 경우 메시지가 배달됩니다.

  - **PendingSuspend**   이미 다음 홉으로 전송되는 중인 메시지를 관리자가 일시 중단했습니다. 배달 시에 오류가 발생하여 메시지가 큐에 다시 들어가게 되는 경우 해당 메시지는 일시 중단됩니다. 그렇지 않은 경우 메시지가 배달됩니다.

  - **Ready**   메시지가 큐에 대기 중이며 처리할 준비가 되었습니다.

  - **Retry**   메시지가 있는 큐에 대한 마지막 자동 또는 연결 시도가 실패했습니다. 메시지가 다음 자동 큐 연결을 다시 시도하기 위해 대기 중입니다.

  - **Suspended**   관리자가 메시지를 수동으로 일시 중단했습니다. 포이즌 메시지 큐의 모든 메시지는 영구적으로 일시 중단된 상태입니다.

맨 위로 이동

## 기타 메시지 속성

이름을 통해 용도를 확인할 수 있는 기타 메시지 속성이 있습니다. 대부분의 메시지 속성은 필터 옵션으로 사용할 수 있습니다. 필터 조건을 지정하면 메시지를 빨리 찾아 조치를 취할 수 있습니다. 필터링 가능한 메시지 속성에 대한 자세한 내용은 [메시지 필터](message-filters-exchange-2013-help.md)을 참조하십시오.

맨 위로 이동

## 큐 및 큐의 메시지 관리

큐 뷰어 및 사실상 모든 큐 및 메시지 관리 cmdlet은 단일 Exchange 서버에서만 사용할 수 있습니다. 즉, 특정 서버에서만 개별 큐 또는 메시지나 여러 큐 또는 메시지를 보거나 작업할 수 있습니다.

Exchange 2013에 도입된 **Get-QueueDigest** cmdlet은 DAG, Active Directory 사이트, 서버 목록, 전체 Active Directory 포리스트 등의 특정 범위 내에 있는 모든 서버의 큐 상태에 대한 높은 수준의 집계 보기를 제공합니다. 경계 네트워크에서 구독된 Edge 전송 서버의 큐는 결과에 포함되지 않습니다. 또한 **Get-QueueDigest**는 Edge 전송 서버에서 제공되기는 하지만 결과는 Edge 전송 서버의 큐로 제한됩니다.


> [!NOTE]
> 기본적으로 <STRONG>Get-QueueDigest</STRONG> cmdlet은 메시지가 10개 이상 포함된 배달 큐를 표시하고 1~2분 후에 결과를 반환합니다. 이러한 기본값을 변경하는 방법에 대한 지침은 <A href="configure-get-queuedigest-exchange-2013-help.md">Get-QueueDigest 구성</A>을 참조하세요.



다음 표에서는 큐 또는 큐의 메시지에 대해 수행할 수 있는 관리 작업에 대해 설명합니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>작업</th>
<th>설명</th>
<th>사용할 도구</th>
<th>지침</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>서버의 큐 보기 및 필터링</p></td>
<td><p>이 작업을 수행하면 전송 서버의 큐가 하나 이상 표시됩니다. 해당 결과를 사용하여 큐에 대해 작업을 수행할 수 있습니다.</p></td>
<td><p>큐 뷰어 또는 <strong>Get-Queue</strong> cmdlet</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">큐 관리</a></p></td>
</tr>
<tr class="even">
<td><p>특정 DAG, Active Directory 사이트 또는 전체 Active Directory 포리스트에 있는 특정 서버의 큐를 보고 필터링합니다.</p></td>
<td><p>이 작업을 수행하면 서버, DAG, Active Directory 사이트 또는 전체 Active Directory 포리스트 등 정의된 범위의 큐에 대한 요약 보기가 표시됩니다.</p></td>
<td><p><strong>Get-QueueDigest</strong> cmdlet만</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">큐 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>큐 일시 중단</p></td>
<td><p>이 작업을 수행하면 현재 큐에 있는 메시지의 배달이 일시적으로 중단됩니다. 큐에는 계속 새 메시지가 들어오지만 큐에서 메시지가 나갈 수 없습니다.</p></td>
<td><p>큐 뷰어 또는 <strong>Suspend-Queue</strong> cmdlet</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">큐 관리</a></p></td>
</tr>
<tr class="even">
<td><p>큐 다시 시작</p></td>
<td><p>이 작업에서는 큐 일시 중단 작업과 반대되는 과정이 수행되어 대기 중인 메시지 배달을 다시 시작할 수 있습니다.</p></td>
<td><p>큐 뷰어 또는 <strong>Resume-Queue</strong> cmdlet</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">큐 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>큐 다시 시도</p></td>
<td><p>이 작업을 수행하면 즉시 다음 홉 연결을 시도합니다. 다음 홉 연결이 실패하면 별도의 수동 작업 없이도 각 시도 간에 일정한 시간 간격이 경과되면 특정 횟수만큼 연결을 시도합니다.</p>
<p>연결 시도 방식이 수동이든 자동이든 관계없이 연결 시도 시 다음 다시 시도 시간이 다시 설정됩니다. 자세한 내용은 <a href="message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md">메시지 다시 시도, 다시 전송, 및 만료 간격</a>을 참조하십시오.</p></td>
<td><p>큐 뷰어 또는 <strong>Retry-Queue</strong> cmdlet</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">큐 관리</a></p></td>
</tr>
<tr class="even">
<td><p>큐의 메시지 다시 전송</p></td>
<td><p>이 작업을 수행하면 큐의 메시지가 전송 큐로 다시 전송되고 분류 프로세스가 다시 진행됩니다.</p></td>
<td><p><strong>Retry-Queue</strong> cmdlet(<em>Resubmit</em> 매개 변수 포함)</p>
<p>포이즌 메시지 큐에서만 큐 뷰어를 사용하여 메시지를 다시 전송할 수 있습니다. 포이즌 메시지 큐의 메시지를 다시 전송하려면 큐 뷰어에서 메시지를 다시 시작하거나 <strong>Resume-Message</strong> cmdlet을 사용합니다.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">큐 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>큐의 메시지 일시 중단</p></td>
<td><p>이 작업을 수행하면 메시지 배달이 일시적으로 중단됩니다. 메시지 일시 중단 작업을 수행하면 특정 큐의 모든 받는 사람 또는 모든 큐의 모든 받는 사람에게 메시지가 배달되지 않도록 할 수 있습니다.</p></td>
<td><p>큐 뷰어 또는 <strong>Suspend-Message</strong> cmdlet</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">큐에서 메시지 관리</a></p></td>
</tr>
<tr class="even">
<td><p>큐의 메시지 다시 시작</p></td>
<td><p>이 작업에서는 메시지 일시 중단 작업과 반대되는 과정이 수행되어 대기 중인 메시지 배달을 다시 시작할 수 있습니다. 메시지 다시 시작 작업을 수행하면 특정 큐의 모든 받는 사람 또는 모든 큐의 모든 받는 사람에게 메시지를 다시 배달할 수 있습니다.</p></td>
<td><p>큐 뷰어 또는 <strong>Resume-Message</strong> cmdlet</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">큐에서 메시지 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>큐에서 메시지 제거</p></td>
<td><p>이 작업을 수행하면 메시지 배달이 영구적으로 중단됩니다. 메시지 제거 작업을 수행하면 지정한 큐의 모든 받는 사람 또는 모든 큐의 모든 받는 사람에게 메시지가 배달되지 않도록 할 수 있습니다. 또한 메시지를 제거할 때 NDR(배달 못 함 보고서)을 보낸 사람에게 보내도록 메시지 제거 작업을 구성할 수 있습니다.</p></td>
<td><p>큐 뷰어 또는 <strong>Remove-Message</strong> cmdlet</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">큐에서 메시지 관리</a></p></td>
</tr>
<tr class="even">
<td><p>큐에서 메시지 내보내기</p></td>
<td><p>이 작업을 수행하면 지정한 파일 경로에 메시지가 복사됩니다. 메시지가 큐에서 삭제되지 않고 메시지의 복사본이 파일 위치에 저장됩니다. 따라서 조직의 관리자 또는 담당자가 이후에 메시지를 검사할 수 있습니다. 메시지를 내보내기 전에 내보내기 프로세스 중에 일반적인 배달 작업이 계속 수행되지 않도록 큐에서 메시지를 일시 중단해야 합니다.</p></td>
<td><p><strong>Export-Message</strong> cmdlet만</p></td>
<td><p><a href="export-messages-from-queues-exchange-2013-help.md">큐에서 메시지 내보내기</a></p></td>
</tr>
</tbody>
</table>


맨 위로 이동

