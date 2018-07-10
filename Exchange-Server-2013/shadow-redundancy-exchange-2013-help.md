---
title: '섀도 중복성: Exchange 2013 Help'
TOCTitle: 섀도 중복성
ms:assetid: a40dbe61-2a18-48a8-b2e0-4e81a6678d11
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351027(v=EXCHG.150)
ms:contentKeyID: 50483815
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 섀도 중복성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

섀도 중복성은 메시지가 사서함으로 배달되기 전에 메시지의 복사본을 복제하기 위해 Microsoft Exchange Server 2010에서 도입되었습니다. Exchange 2010에서 섀도 중복성은 서버가 메시지 배달 경로의 다음 홉이 배달을 완료했음을 확인할 때까지 전송 서버의 전송 데이터베이스에서 메시지를 삭제하는 작업을 지연시킵니다. 배달 성공을 전송 서버로 다시 보고하기 전에 다음 홉이 실패하면 전송 서버는 메시지를 해당 다음 홉에 다시 전송합니다. Exchange 2010 서버는 XSHADOW 동사를 사용하여 섀도 중복성 지원을 보급합니다. SMTP 서버가 섀도 중복성을 지원하지 않는 경우 Exchange 2010에서는 수신 커넥터에 구성된 시간 간격에 따른 지연된 확인을 사용하여 메시지의 중복 복사본을 만듭니다.

Microsoft Exchange Server 2013에서 섀도 중복성의 주요 개선 사항은 이제 보내는 서버에서 성공적인 메시지 수신을 확인하기 전에 전송 서버가 수신하는 모든 메시지의 중복 복사본을 만든다는 점입니다. 보내는 서버가 섀도 중복성을 지원하는지 여부는 상관 없습니다. 따라서 Exchange 2013 전송 파이프라인의 모든 메시지를 전송 중에 복제할 수 있습니다. Exchange 2013에서 원본 메시지가 전송 중 손실된 것으로 판단하면 메시지의 중복 복사본이 다시 배달됩니다.

**목차**

Shadow redundancy components

Requirements for shadow redundancy

Shadow redundancy is enabled by default

How shadow messages are created

SMTP timeouts

How shadow messages are maintained

Message processing after an outage

## 섀도 중복성 구성 요소

다음 표에서는 섀도 중복성의 구성 요소를 설명합니다. 이 항목에서는 다음 용어가 사용되고 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>용어</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>전송 서버</p></td>
<td><p>메시지 큐가 있고 메시지 라우팅을 담당하는 Exchange 서버입니다. Exchange 2013에서 전송 서버는 사서함 서버(사서함 서버의 전송 서비스)입니다.</p></td>
</tr>
<tr class="even">
<td><p>전송 데이터베이스</p></td>
<td><p>Exchange 2013 전송 서버의 메시지 큐 데이터베이스입니다. 섀도 큐 및 보안 네트워크도 전송 데이터베이스에 저장됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>전송 고가용성 경계</p></td>
<td><p>DAG 환경의 DAG(데이터베이스 사용 가능 그룹) 또는 DAG가 아닌 환경의 Active Directory 사이트입니다. 메시지가 전송 고가용성 경계의 전송 서버에 도착하면 Exchange는 경계 내 전송 서버에 2개의 메시지 중복 복사본을 유지하려고 시도합니다. 메시지가 전송 고가용성 경계를 벗어나면 Exchange는 메시지의 중복 복사본 유지를 중지합니다.</p></td>
</tr>
<tr class="even">
<td><p>기본 메시지</p></td>
<td><p>메시지가 배달을 위해 전송 파이프라인에 제출되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p>섀도 메시지</p></td>
<td><p>기본 서버가 기본 메시지를 성공적으로 처리했음이 확인될 때까지 섀도 서버에서 유지하는 메시지의 중복 복사본입니다.</p></td>
</tr>
<tr class="even">
<td><p>기본 서버</p></td>
<td><p>현재 기본 메시지를 처리하고 있는 전송 서버입니다.</p></td>
</tr>
<tr class="odd">
<td><p>섀도 서버</p></td>
<td><p>기본 서버에 대한 섀도 메시지가 있는 전송 서버입니다. 전송 서버는 일부 메시지의 기본 서버인 동시에 다른 메시지의 섀도 서버일 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>섀도 큐</p></td>
<td><p>섀도 서버가 섀도 메시지를 저장하는 배달 큐입니다. 받는 사람이 여러 명인 메시지의 경우 기본 메시지에 대한 다음 홉 각각에 별도의 섀도 큐가 필요합니다.</p></td>
</tr>
<tr class="odd">
<td><p>삭제 상태</p></td>
<td><p>전송 서버가 섀도 메시지에 대해 유지하는 정보이며 기본 메시지가 성공적으로 처리되었음을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p>삭제 알림</p></td>
<td><p>섀도 서버가 기본 서버에서 수신하는 응답이며 섀도 메시지를 삭제할 준비가 되었음을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>보안 네트워크</p></td>
<td><p>전송 휴지통의 Exchange 2013에서 향상된 버전입니다. 사서함 서버의 전송 서비스를 통해 성공적으로 처리되거나 사서함으로 배달된 메시지는 보안 네트워크로 이동됩니다. 자세한 내용은 <a href="safety-net-exchange-2013-help.md">보안 네트워크</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>섀도 중복성 관리자</p></td>
<td><p>섀도 중복성을 관리하는 전송 구성 요소입니다.</p></td>
</tr>
<tr class="odd">
<td><p>하트비트</p></td>
<td><p>기본 서버와 섀도 서버가 서로의 가용성을 확인할 수 있는 프로세스입니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 섀도 중복성에 대한 요구 사항

당연한 일이지만 섀도 중복성에는 여러 개의 Exchange 2013 사서함 서버가 필요합니다. 사서함 서버는 독립 실행형 서버이거나 동일한 컴퓨터에 설치된 사서함 서버 및 클라이언트 액세스 서버일 수 있습니다.

  - 사서함 서버가 DAG의 구성원이 아닌 경우에는 다른 사서함 서버가 로컬 Active Directory 사이트에 있어야 합니다.

  - 사서함 서버가 DAG의 구성원인 경우 다른 사서함 서버가 동일한 DAG에 속해야 합니다. DAG에 속하는 다른 사서함 서버는 로컬 Active Directory 사이트 또는 원격 Active Directory 사이트에 있을 수 있습니다. DAG가 여러 Active Directory 사이트에 걸쳐 있는 경우 섀도 중복성은 사이트 복구를 위해 원격 Active Directory 사이트에 메시지의 중복 복사본을 생성하는 방식을 선호합니다.

전송 중인 메시지를 섀도 중복성으로 보호할 수 없는 상황은 다음과 같습니다.

  - 단일 Exchange 서버 환경

  - 프로비전 중인 DAG

  - 메시지의 섀도 중복성에 관여된 두 대 이상의 전송 서버가 동시에 실패한 경우

맨 위로 이동

## 섀도 중복성은 기본적으로 사용하도록 설정됨

기본적으로 섀도 중복성은 **Set-TransportConfig** cmdlet에서 *ShadowRedundancyEnabled* 매개 변수를 사용하여 사서함 서버의 전송 서비스에서 전체적으로 사용하도록 설정됩니다. 기본적으로 사서함 서버의 전송 서비스가 메시지의 중복 복사본을 만들 수 없는 경우 메시지가 거부되지 않습니다. 하지만 **Set-TransportConfig** cmdlet에서 *RejectMessageOnShadowFailure* 매개 변수를 사용하여 메시지의 중복 복사본이 생성되지 않는 경우 메시지를 거부하도록 Exchange 2013을 구성할 수 있습니다. 메시지가 일시적 실패로 거부되지만 보내는 서버에서 메시지를 다시 전송할 수 있습니다. SMTP 응답 코드는 `451 4.4.0 Message failed to be made redundant.`입니다. 조직에 사용 가능한 Exchange 2013 사서함 서버가 여러 개인 경우에만 중복이 불가능한 메시지를 거부하도록 Exchange 2013을 구성해야 합니다.

다음 표에서는 섀도 중복성을 사용하도록 설정하는 매개 변수를 설명합니다.

### 섀도 중복성을 사용하도록 설정하는 매개 변수

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>기본값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong>의 <em>ShadowRedundancyEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code>로 설정하면 섀도 중복이 조직의 모든 전송 서버에서 사용하도록 설정됩니다.</p></li>
<li><p><code>$false</code>로 설정하면 섀도 중복이 조직의 모든 전송 서버에서 사용하지 않도록 설정됩니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportConfig</strong>의 <em>RejectMessageOnShadowFailure</em></p></td>
<td><p><code>$false</code></p></td>
<td><ul>
<li><p><code>$false</code>   메시지의 섀도 복사본을 만들 수 없는 경우에도 조직의 전송 서버가 기본 메시지를 수락합니다. 이러한 메시지는 전송 중일 때 중복되어 유지되지 않습니다.</p></li>
<li><p><code>$true</code>   메시지의 섀도 복사본이 성공적으로 생성되기 전에는 조직의 모든 전송 서버가 메시지를 수락하거나 확인하지 않습니다. 메시지의 섀도 복사본을 만들 수 없는 경우 기본 메시지가 일시적 오류로 거부됩니다. 조직의 모든 메시지는 전송 중에 중복되어 유지됩니다.</p>
<p>메시지의 섀도 복사본을 만들 수 있는 DAG 또는 Active Directory 사이트에 여러 개의 Exchange 2013 사서함 서버가 있는 경우에만 이 값을 <code>$true</code>로 설정해야 합니다.</p></li>
</ul>
<p>이 매개 변수는 <em>ShadowRedundancyEnabled</em>가 <code>$true</code>인 경우에만 의미가 있습니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 섀도 메시지가 만들어지는 방법

섀도 중복성의 기본 목적은 메시지가 전송 중일 때 전송 고가용성 경계 내에 항상 두 개의 메시지 복사본이 존재하도록 만드는 것입니다. 메시지의 중복 복사본이 만들어지는 위치와 시점은 메시지가 어디에서 왔으며 어디로 가는지에 따라 다릅니다. 세 가지 주요 결정 요소는 다음과 같습니다.

  - 전송 고가용성 경계 외부에서 받은 메시지

  - 전송 고가용성 경계 외부로 전송된 메시지

  - 전송 고가용성 경계 내의 사서함 서버의 사서함 전송 제출 서비스에서 받은 메시지

*전송 고가용성 경계*는 다음 중 하나입니다.

  - DAG의 구성원인 사서함 서버의 경우 DAG. 여기에는 여러 Active Directory 사이트에 걸쳐 있는 DAG가 포함됩니다.

  - DAG에 속하지 않는 사서함 서버의 경우 Active Directory 사이트.

섀도 중복성은 전송 고가용성 경계를 넘어 섀도 메시지를 추적하지 않습니다. 메시지가 전송 고가용성 경계를 넘으면 섀도 중복성이 시작되거나 다시 시작됩니다. 이를 통해 섀도 메시지 유지 관리 트래픽이 줄어들고 전송 고가용성 경계를 넘어 섀도 메시지가 다시 제출되는 상황이 방지됩니다. Exchange 2010 허브 전송 서버는 특별한 경우이며 이 항목의 뒷부분에서 설명합니다.

## 전송 고가용성 경계 외부에서 받은 메시지

Exchange 2013 사서함 서버의 전송 서비스가 전송 고가용성 경계 외부에서 메시지를 받은 경우 사서함 서버는 보내는 서버의 섀도 중복성 지원 여부를 고려하지 않습니다. 섀도 중복성이 사용 설정되어 있으면 메시지를 받는 사서함 서버는 보내는 서버에 메시지의 수신을 알리기 전에 전송 고가용성 경계 내의 다른 사서함 서버에 메시지의 중복 복사본을 만듭니다. 예를 들면 이 프로세스는 다음과 같은 방식으로 작동합니다.

![섀도 메시지 만들기](images/Dd351027.a97d383b-6ae4-458d-af3a-1ac0a41cd52b(EXCHG.150).gif "섀도 메시지 만들기")

1.  SMTP 서버가 사서함 서버의 전송 서비스에 메시지를 전송합니다. 사서함 서버는 기본 서버이며 메시지는 기본 메시지입니다.

2.  SMTP 서버와의 원래 SMTP 세션이 아직 활성화된 상태에서 기본 서버의 전송 서비스가 조직의 다른 사서함 서버에서 전송 서비스와의 새 SMTP 세션을 동시에 열고 메시지의 중복 복사본을 만듭니다.
    
      - 기본 서버가 DAG의 구성원이면 기본 서버가 동일한 DAG의 다른 사서함 서버에 연결합니다. DAG가 여러 Active Directory 사이트에 걸쳐 있는 경우 다른 Active Directory 사이트의 사서함 서버가 기본적으로 사용됩니다. 이 설정은 **Set-TransportService** cmdlet의 *ShadowMessagePreference* 매개 변수로 제어됩니다. 기본값은 `PreferRemote`이지만 `RemoteOnly` 또는 `LocalOnly`로 변경할 수 있습니다.
    
      - 기본 서버가 DAG의 구성원이 아닌 경우 기본 서버는 *ShadowMessagePreference* 매개 변수의 값에 관계없이 동일한 Active Directory 사이트에 있는 다른 사서함 서버에 연결합니다.

3.  기본 서버는 메시지의 복사본을 다른 사서함 서버의 전송 서비스로 전송하고 다른 사서함 서버의 전송 서비스는 사서함의 복사본을 성공적으로 만들었음을 확인합니다. 메시지의 복사본은 섀도 메시지이며 이 메시지가 있는 사서함 서버는 기본 서버에 대한 섀도 서버입니다. 메시지는 섀도 서버의 섀도 큐에 존재합니다.

4.  기본 서버가 섀도 서버에서 확인을 수신하면 기본 서버는 원래 SMTP 세션에서 원래 SMTP 서버에 기본 메시지의 수신을 확인하고 SMTP 세션이 닫힙니다.

## 전송 고가용성 경계 외부로 전송된 메시지

Exchange 2013 전송 서버가 전송 고가용성 경계 외부로 메시지를 전송하고 다른 측의 SMTP 서버가 메시지의 성공적 수신을 확인하면 전송 서버는 메시지를 보안 네트워크로 이동합니다. 기본 메시지가 전송 고가용성 경계를 넘어 성공적으로 전송된 후에는 보안 네트워크에서 메시지의 다시 전송이 발생할 수 없습니다. 보안 네트워크에 대한 자세한 내용은 [보안 네트워크](safety-net-exchange-2013-help.md)를 참조하십시오.

## 전송 고가용성 경계 내에서 전송된 메시지

Exchange 2013에서는 메시지 라우팅이 최적화되므로 최종 목적지가 DAG 또는 Active Directory 사이트에 있는 경우 해당 DAG 또는 Active Directory 사이트의 사서함 서버에 있는 전송 서비스 간에는 일반적으로 여러 홉이 필요하지 않습니다. 메시지의 최종 목적지가 있는 DAG 또는 Active Directory 사이트의 사서함 서버에서 전송 서비스가 메시지를 수락한 경우 메시지에 대한 다음 홉은 일반적으로 최종 목적지 자체입니다. 메시지의 복사본을 두 개로 유지하고자 하는 섀도 중복성의 목표는 메시지의 섀도 복사본 하나가 DAG 또는 Active Directory 사이트 내에 존재할 경우 충족됩니다. 일반적으로 사서함 서버의 활성 큐를 비우기 위하여 **Redirect-Message** cmdlet이 필요한 DAG의 장애 조치(failover) 시나리오에서만 동일한 전송 고가용성 경계 내에 여러 개의 홉이 필요합니다.

## 동일한 Active Directory 사이트에 Exchange 2010 허브 전송 서버가 있는 경우 섀도 중복성

Exchange 2010 허브 전송 서버가 동일한 Active Directory 사이트의 Exchange 2013 사서함 서버로 메시지를 전송할 경우 Exchange 2010 허브 전송 서버는 XSHADOW 명령을 사용하여 섀도 중복성 지원을 보급하지만 사서함 서버는 섀도 중복성 지원을 보급하지 않습니다. 이로 인해 Exchange 2010 허브 전송 서버는 Exchange 2013 사서함 서버에 메시지의 섀도 복사본을 만들 수 없습니다.

Exchange 2013 사서함 서버의 전송 서비스가 동일한 Active Directory 사이트의 Exchange 2010 허브 전송으로 메시지를 전송할 경우 Exchange 2013 사서함 서버가 Exchange 2010 허브 전송 서버에 대해 메시지를 섀도합니다. Exchange 2013 사서함 서버가 메시지의 성공적 수신을 알리는 Exchange 2010 허브 전송 서버의 확인을 받은 후에는 Exchange 2013 사서함 서버가 성공적으로 처리된 메시지를 보안 네트워크로 이동합니다. 하지만 Exchange 2013 사서함이 보안 네트워크에 저장한 성공적으로 처리된 메시지는 Exchange 2010 허브 전송 서버로 다시 전송되지 않습니다.

맨 위로 이동

## SMTP 시간 제한

메시지의 중복 복사본을 만들려고 시도하는 동안 보내는 SMTP 서버와 기본 서버 간의 SMTP 연결 또는 기본 서버와 섀도 서버 간의 SMTP 세션이 시간 초과될 수 있습니다. 수신 커넥터와 송신 커넥터에는 모두 커넥터에서 데이터가 실제로 전송되는 시점에 대한 *ConnectionInactivityTimeOut* 매개 변수가 있습니다. 수신 커넥터에는 절대적 *ConnectionTimeOut* 매개 변수도 있습니다.

메시지의 섀도 복사본이 성공적으로 생성되고 확인되기 전에 시간 초과되는 SMTP 세션이 있는 경우 결과는 **Set-TransportConfig** cmdlet의 *RejectMessageOnShadowFailure* 매개 변수를 통해 제어됩니다. 기본적으로 이 매개 변수의 값은 `$false`이며, 이는 섀도 복사본을 만들지 않고 기본 메시지가 수락된다는 것을 의미합니다. 이 매개 변수의 값이 `$true`이면 기본 메시지는 일시적 오류 `451 4.4.0`과 함께 거부됩니다.

메시지의 섀도 복사본이 성공적으로 생성되었지만 보내는 SMTP 서버와 기본 서버 간의 SMTP 세션이 시간 초과된 경우에는 기본 서버가 기본 메시지를 수락하고 처리합니다. 보내는 SMTP 서버는 확인되지 않은 메시지를 다시 배달하지만 중복 메시지 삭제를 통해 Exchange 사서함 사용자에게 중복 메시지가 표시되지 않습니다. 보내는 SMTP 서버가 메시지를 다시 전송하면 기본 서버는 메시지의 다른 섀도 복사본을 만듭니다. 보내는 SMTP 서버가 메시지를 다시 전송할 때 생성되는 섀도 메시지는 서로 관계가 없습니다.

다음 표에서는 섀도 메시지의 생성을 제어하는 매개 변수를 설명합니다.

### 섀도 메시지 생성 매개 변수

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>원본</th>
<th>기본값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong>의 <em>ShadowMessagePreferenceSetting</em></p></td>
<td><p><code>PreferRemote</code></p></td>
<td><ul>
<li><p><code>PreferRemote</code>   다른 Active Directory 사이트의 사서함 서버에 메시지의 섀도 복사본을 만들려고 시도합니다. 작업이 실패하면 로컬 Active Directory 사이트의 서버에서 메시지 섀도의 복사본을 만들려고 시도합니다.</p></li>
<li><p><code>LocalOnly</code>   메시지의 섀도 복사본을 로컬 Active Directory 사이트의 전송 서버에서만 만들어야 합니다.</p></li>
<li><p><code>RemoteOnly</code>: 메시지의 섀도 복사본을 다른 Active Directory 사이트의 전송 서버에서만 만들어야 합니다.</p></li>
</ul>
<p>이 매개 변수는 메시지의 섀도 복사본을 만들려고 시도하는 기본 서버가 여러 Active Directory 사이트에 걸쳐 있는 DAG의 구성원인 사서함 서버인 경우에만 의미가 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportConfig</strong>의 <em>MaxRetriesForRemoteSiteShadow</em></p></td>
<td><p>4</p></td>
<td><p>이 매개 변수는 사서함 서버가 여러 Active Directory 사이트에 걸쳐 있는 DAG의 구성원일 때 사용됩니다.</p>
<ul>
<li><p><em>ShadowMessagePreferenceSetting</em>을 <code>PreferRemote</code>로 설정하면 먼저 사서함 서버가 <em>MaxRetriesForRemoteSiteShadow</em>로 지정된 횟수까지 원격 Active Directory 사이트의 다른 사서함 서버에 메시지의 섀도 복사본을 만들려고 시도합니다. 이 시도에 실패하면 사서함 서버가 <em>MaxRetriesForLocalSiteShadow</em>로 지정된 횟수까지 로컬 Active Directory 사이트의 다른 사서함 서버에 메시지의 섀도 복사본을 만들려고 시도합니다.</p></li>
<li><p><em>ShadowMessagePreferenceSetting</em>을 <code>RemoteOnly</code>로 설정하면 먼저 사서함 서버가 <em>MaxRetriesForRemoteSiteShadow</em>로 지정된 횟수까지 원격 Active Directory 사이트의 사서함 서버에 메시지의 섀도 복사본을 만들려고 시도합니다.</p></li>
<li><p>이</p></li>
</ul>
<p>메시지의 섀도 복사본을 성공적으로 만들 수 없는 경우</p>
<ul>
<li><p><em>RejectMessageOnShadowFailure</em>가 <code>$true</code>인 경우 일시적인 오류로 인해 기본 메시지가 거부됩니다.</p></li>
<li><p><em>RejectMessageOnShadowFailure</em>가 <code>$false</code>인 경우 기본 메시지가 수락되지만 중복되어 유지되지 않습니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong>의 <em>MaxRetriesForLocalSiteShadow</em></p></td>
<td><p>2</p></td>
<td><p>이 매개 변수는 다음과 같은 상황에서 사용됩니다.</p>
<ul>
<li><p>사서함 서버가 여러 Active Directory 사이트에 걸쳐 있는 DAG의 구성원일 때.</p>
<ol>
<li><p><em>ShadowMessagePreferenceSetting</em>을 <code>PreferRemote</code>로 설정하면 먼저 사서함 서버가 <em>MaxRetriesForRemoteSiteShadow</em>로 지정된 횟수까지 원격 Active Directory 사이트의 다른 사서함 서버에 메시지의 섀도 복사본을 만들려고 시도합니다. 이 시도에 실패하면 사서함 서버가 <em>MaxRetriesForLocalSiteShadow</em>로 지정된 횟수까지 로컬 Active Directory 사이트의 다른 사서함 서버에 메시지의 섀도 복사본을 만들려고 시도합니다.</p></li>
<li><p><em>ShadowMessagePreferenceSetting</em>을 <code>LocalOnly</code>로 설정하면 사서함 서버는 <em>MaxRetriesForLocalSiteShadow</em>로 지정된 횟수까지 로컬 Active Directory 사이트의 다른 사서함 서버에 메시지의 섀도 복사본을 만들려고 시도합니다.</p></li>
</ol></li>
<li><p>사서함 서버가 DAG의 구성원이 아니거나 사서함 서버가 하나의 Active Directory 사이트에 있는 DAG의 구성원인 경우 사서함 서버는 <em>MaxRetriesForLocalSiteShadow</em>로 지정된 횟수까지 로컬 Active Directory의 다른 사서함 서버에 메시지의 섀도 복사본을 만들려고 시도합니다.</p></li>
</ul>
<p>메시지의 섀도 복사본을 성공적으로 만들 수 없는 경우</p>
<ul>
<li><p><em>RejectMessageOnShadowFailure</em>가 <code>$true</code>인 경우 일시적인 오류로 인해 기본 메시지가 거부됩니다.</p></li>
<li><p><em>RejectMessageOnShadowFailure</em>가 <code>$false</code>인 경우 기본 메시지가 수락되지만 중복되어 유지되지 않습니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong>의 <em>ConnectionInactivityTimeout</em></p></td>
<td><p>사서함 서버의 전송 서비스에서 5분</p>
<p>클라이언트 액세스 서버의 프런트 엔드 전송 서비스에서 5분</p>
<p>Edge 전송 서버에서 1분</p></td>
<td><p>이 매개 변수는 원본 메시징 서버와의 열린 SMTP 연결이 닫히기 전에 유휴 상태를 유지할 수 있는 최대 시간을 지정합니다. 이 매개 변수의 값은 <em>ConnectionTimeout</em> 매개 변수로 지정된 값보다 작아야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong>의 <em>ConnectionTimeout</em></p></td>
<td><p>사서함 서버의 전송 서비스에서 10분</p>
<p>클라이언트 액세스 서버의 프런트 엔드 전송 서비스에서 10분</p>
<p>Edge 전송 서버에서 5분</p></td>
<td><p>이 매개 변수는 원본 메시징 서버가 데이터를 전송 중인 경우에도 원본 메시징 서버와의 SMTP 연결이 열린 상태로 유지될 수 있는 최대 시간을 지정합니다. 이 매개 변수의 값은 <em>ConnectionInactivityTimeout</em> 매개 변수로 지정된 값보다 커야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-SendConnector</strong>의 <em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10분</p></td>
<td><p>이 매개 변수는 대상 메시징 서버와의 열린 SMTP 연결이 닫히기 전에 유휴 상태를 유지할 수 있는 최대 시간을 지정합니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 섀도 메시지가 유지되는 방법

섀도 메시지가 성공적으로 만들어지면 섀도 중복성 작업이 시작된 것입니다. 기본 서버와 섀도 서버는 메시지의 진행 상태를 추적하기 위해 서로 연결된 상태를 유지해야 합니다.

기본 서버가 메시지를 다음 홉으로 성공적으로 전송하고 다음 홉이 메시지의 수신을 확인하면 기본 서버는 메시지의 *삭제 상태*를 배달 완료로 업데이트합니다. 삭제 상태는 기본적으로 모니터링 중인 메시지의 목록이 포함된 메시지입니다. 성공적으로 배달된 메시지는 섀도 큐에 유지할 필요가 없으므로, 기본 서버가 메시지를 다음 홉으로 성공적으로 전송했음을 섀도 서버가 확인한 후에는 섀도 서버가 섀도 메시지를 섀도 큐에서 보안 네트워크로 이동합니다.

섀도 서버는 기본 서버를 쿼리하여 해당 섀도 큐에 있는 섀도 메시지의 삭제 상태를 확인합니다. 섀도 서버가 다른 관련 없는 메시지의 전송을 비롯한 이유로 기본 서버와의 SMTP 세션을 여는 경우 섀도 서버는 기본 메시지의 삭제 상태를 확인하기 위해 **XQDISCARD** 명령을 실행합니다. 미리 구성된 간격이 지난 후에도 섀도 서버가 기본 서버와의 SMTP 세션을 열지 않은 경우 섀도 서버는 기본 서버와의 SMTP 세션을 열고 **XQDISCARD** 명령을 실행합니다. 시간 간격은 **Set-TransportConfig** cmdlet의 *ShadowHeartbeatFrequentcy* 매개 변수로 제어됩니다. 기본값은 2분입니다. 섀도 서버가 기본 서버와의 SMTP 세션을 열면 기본 서버는 쿼리하는 섀도 서버에 적용되는 메시지에 대한 *삭제 알림*으로 응답합니다. Exchange 2013에서 삭제 알림은 메모리가 아니라 디스크에 저장됩니다. 따라서 Microsoft Exchange Transport Service가 다시 시작되더라도 삭제 알림이 유지됩니다. 서비스가 시작된 후에도 기본 서버는 여전히 성공적으로 처리한 메시지에 대해 알고 있으며 섀도 서버가 이 정보를 사용할 수 있습니다.

섀도 서버와 기본 서버 간의 SMTP 통신은 서버의 가용성을 확인하는 *하트비트*로 사용됩니다. 섀도 서버가 미리 구성된 시간 간격이 지난 후에 기본 서버와의 SMTP 세션을 열 수 없거나 기본 서버 전송 데이터베이스의 데이터베이스 ID가 다른 경우 섀도 서버는 자신을 기본 서버로 승격하고, 섀도 메시지를 기본 메시지로 승격하고, 메시지를 다음 홉으로 전송합니다. 시간 간격은 **Set-TransportConfig** cmdlet의 *ShadowResubmitTimeSpan* 매개 변수로 제어됩니다. 기본값은 3시간입니다.

*섀도 중복성 관리자*는 섀도 중복성의 관리를 담당하는 Exchange 2013 전송 서버의 핵심 구성 요소입니다. 섀도 중복성 관리자는 서버에서 현재 처리 중인 모든 기본 메시지에 대한 다음 정보를 유지 관리합니다.

  - 처리 중인 각 기본 메시지의 섀도 서버

  - 섀도 서버로 보낼 삭제 상태

섀도 중복성 관리자는 섀도 서버가 해당 섀도 큐에 갖고 있는 모든 섀도 메시지에 대해 다음을 수행합니다.

  - 각 섀도 메시지에 대한 기본 서버 목록을 유지 관리합니다.

  - 메시지의 기본 복사본이 저장된 큐 데이터베이스의 원래 데이터베이스 ID와 현재 데이터베이스 ID를 비교합니다.

  - 섀도 메시지를 큐에 넣을 각 기본 서버의 가용성을 확인합니다.

  - 기본 서버에서의 삭제 알림을 처리합니다.

  - 예상된 모든 삭제 알림을 받은 후 섀도 큐에서 섀도 메시지를 제거합니다.

  - 섀도 서버가 섀도 메시지의 소유권을 갖게 되어 기본 서버가 되는 시점을 결정합니다.

  - DSN(배달 상태 알림) 및 저널 보고서와 같은 메시지 분기 및 기타 파생 메시지를 추적하여 메시지의 모든 분기가 완전히 처리될 때까지 메시지의 중복 복사본이 해제되지 않는지 확인합니다.

다음 표에서는 섀도 메시지를 유지하는 방법을 제어하는 매개 변수를 설명합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>기본값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong>의 <em>ShadowHeartbeatFrequency</em></p></td>
<td><p>2분</p></td>
<td><p>메시지의 삭제 상태를 확인하기 위해 기본 서버에 대한 SMTP 연결을 열기 전에 섀도 서버가 기다리는 최대 시간입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportConfig</strong>의 <em>ShadowResubmitTimeSpan</em></p></td>
<td><p>3시간</p></td>
<td><p>기본 서버가 실패했다고 결정하고 연결할 수 없는 기본 서버의 섀도 큐에 있는 섀도 메시지의 소유권을 갖기 전까지 서버가 대기하는 시간입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportConfig</strong>의 <em>ShadowMessageAutoDiscardInterval</em></p></td>
<td><p>2일</p></td>
<td><p>성공적으로 배달된 메시지에 대한 삭제 이벤트가 서버에 유지되는 시간입니다. 기본 서버는 섀도 서버에서 쿼리할 때까지 삭제 이벤트를 큐에 대기시킵니다. 그러나 섀도 서버가 이 매개 변수로 지정된 기간 동안 기본 서버를 쿼리하지 않으면 기본 서버가 대기 중인 삭제 이벤트를 삭제합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportConfig</strong>의 <em>SafetyNetHoldTime</em></p></td>
<td><p>2일</p></td>
<td><p>성공적으로 처리된 메시지가 보안 네트워크에 유지되는 시간입니다. 확인되지 않은 섀도 메시지는 <strong>Set-TransportService</strong>의 <em>SafetyNetHoldTime</em>과 <em>MessageExpirationTimeout</em>을 더한 시간이 지난 후 보안 네트워크에서 만료됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong>의 <em>MessageExpirationTimeout</em></p></td>
<td><p>2일</p></td>
<td><p>메시지가 만료되기 전에 큐에 남아 있을 수 있는 시간입니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 중단 후 메시지 처리

섀도 중복성은 서버 중단으로 인한 메시지 손실을 최소화합니다. 중단 후 전송 서버가 다시 온라인 상태가 될 경우 다음과 같은 두 가지 시나리오가 있습니다.

  - **서버가 새 전송 데이터베이스를 사용하여 다시 온라인 상태로 됩니다.**   이 시나리오에서는 데이터 손상 또는 하드웨어 오류로 인해 전송 데이터베이스를 복구할 수 없습니다. 이 경우 전송 서버는 새 데이터베이스 ID를 가지므로 조직의 다른 전송 서버에서 새 경로로 인식됩니다. 또한 이 시나리오는 서버를 복구할 수 없고 새 서버가 대체 서버로 프로비전된 상황에 적용됩니다.

  - **서버가 동일한 전송 데이터베이스를 사용하여 온라인 상태로 돌아옵니다.**   이 시나리오에서는 특정 전송 서버가 실패하지 않았지만 오랜 시간 동안 오프라인 상태였기 때문에 섀도 서버가 메시지 소유권을 가져오고 메시지를 다시 전송합니다. 예를 들어 네트워크 카드 오류 또는 오랜 시간 동안의 서버 유지 관리로 인해 이 시나리오가 발생합니다.

다음 표에서는 섀도 중복성이 이러한 두 가지 시나리오에 어떻게 반응하는지를 요약하여 보여줍니다. 이해를 돕기 위해 중단된 서버를 Mailbox01이라고 합니다.

### 복구 시나리오에서의 메시지 처리

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>복구 시나리오</th>
<th>수행한 작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox01은 새 데이터베이스를 사용하여 다시 온라인 상태가 됩니다.</p></td>
<td><p>Mailbox01을 사용할 수 없게 되면 Mailbox01에 대하여 대기된 섀도 메시지가 있는 각 서버는 이러한 메시지의 소유권을 갖게 되고 메시지를 다시 전송합니다. 그러면 메시지가 목적지에 배달됩니다.</p>
<p>메시지에 대한 최대 지연은 <strong>Set-TransportConfig</strong> cmdlet의 <em>ShadowHeartbeatFrequency</em> 매개 변수 값입니다. 기본값은 2분입니다.</p></td>
</tr>
<tr class="even">
<td><p>Mailbox01은 동일한 데이터베이스를 사용하여 다시 온라인 상태가 됩니다.</p></td>
<td><p>Mailbox01이 다시 온라인 상태가 되면 Mailbox01에 대한 메시지의 섀도 복사본을 저장하는 서버가 이미 배달한 큐의 메시지를 배달합니다. 이로 인해 이러한 메시지의 배달이 중복됩니다. 중복된 메시지가 검색되더라도 Exchange 사서함 사용자에게 중복된 메시지가 표시되지는 않습니다. 하지만 비 Exchange 메시징 시스템의 받는 사람은 중복된 메시지 복사본을 받을 수 있습니다.</p>
<p>메시지에 대한 최대 지연은 <strong>Set-TransportConfig</strong> cmdlet의 <em>ShadowResubmitTimeSpan</em> 매개 변수 값입니다. 기본값은 3시간입니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

