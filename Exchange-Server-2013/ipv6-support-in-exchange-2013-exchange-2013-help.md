---
title: 'Exchange 2013의 IPv6 지원: Exchange 2013 Help'
TOCTitle: Exchange 2013의 IPv6 지원
ms:assetid: 33543023-eb9a-4102-b990-84a818a52814
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg144561(v=EXCHG.150)
ms:contentKeyID: 50482802
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013의 IPv6 지원

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

인터넷 프로토콜 버전 6 (IPv6)는 최신 버전의는 IP (인터넷 프로토콜)입니다. I p v 6은 다양 한 i p v 4 이전 버전의 IP 이었던의 단점 수정 되었습니다.

Microsoft Exchange Server 2013, i p v 6 i p v 4도 설치 되어 있고 사용 하도록 설정 하는 경우에 지원 됩니다. Exchange 2013 이 구성에서 배포 되는 네트워크 p v 4와 i p v 6을 지원 하는 경우 모든 Exchange 서버 데이터를 보낼를 업데이트 하 고 장치, 서버 및 IPv6 주소를 사용 하는 클라이언트에서 데이터를 받을 수 있습니다.

이 항목에서는 Exchange 2013 에 IPv6 주소 지정에 대해 설명 합니다. I p v 6에 대 한 추가 배경 정보, [i p v 6](https://go.microsoft.com/fwlink/p/?linkid=92582)을 참조 하십시오.

**목차**

Exchange 2013 구성 요소의 IPv6 지원

운영 체제에서 프로토콜을 사용 하지 않도록 설정 하거나 사용

IPv6 주소 기본 (영문)

## Exchange 2013 구성 요소의 IPv6 지원

다음 표에서 i p v 6의 영향을 받는 Exchange 2013 의 구성 요소를 설명 합니다.

### Exchange 2013의 기능 및 IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>IPv6 지원</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IP 허용 목록 및 연결 필터링 에이전트에서 IP 차단 목록</p></td>
<td><p>예</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>IP 허용 목록 공급자 및 연결 필터링 에이전트에서 IP 차단 목록 공급자입니다.</p></td>
<td><p>아니요</p></td>
<td><p>현재 IPv6 주소를 조회 하는 것에 대 한 없는 널리 사용 되는 업계 표준 프로토콜이입니다. 대부분의 IP 차단 목록 공급자는 IPv6 주소를 지원 하지 않습니다. 수신 커넥터에 알 수 없는 IPv6 주소에서 익명 연결을 허용 하는 경우에 스팸 IP 차단 목록 공급자를 무시 하 고 조직에 대 한 스팸을 성공적으로 배달 됩니다 위험이 증가 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>프로토콜 분석 에이전트에서 보낸사람 신뢰도</p></td>
<td><p>아니요</p></td>
<td><p>프로토콜 분석 에이전트 IPv6 보낸에서 발생 하는 메시지에 대 한 보낸사람 신뢰도 수준 (SRL)을 계산 하지 않습니다. 보낸사람 신뢰도 대 한 자세한 내용은 <a href="sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md">보낸사람 신뢰도 및 프로토콜 분석 에이전트</a>을 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p>보낸 사람 ID</p></td>
<td><p>예</p></td>
<td><p>자세한 내용은 <a href="sender-id-exchange-2013-help.md">보낸사람 ID</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>수신 커넥터</p></td>
<td><p>예</p></td>
<td><p>다음과 같은 구성 요소에 대 한 IPv6 주소 허용 됩니다.</p>
<ul>
<li><p>로컬 IP 주소 바인딩</p></li>
<li><p>원격 IP 주소</p></li>
<li><p>IP 주소 범위</p></li>
</ul>
<p>것이 좋습니다 수신 커넥터를 구성 하는 것에 대 한 알 수 없는 IPv6 주소에서 익명 연결을 수락 합니다. 조직에서 IPv6 주소를 사용 하 여 발신자의 메일을 받을 해야 하는 경우 해당 보낸사람을 사용 하는 특정 IPv6 주소를 원격 IP 주소를 제한 하는 전용된 수신 커넥터를 만듭니다.</p>
<p>자세한 내용은 <a href="receive-connectors-exchange-2013-help.md">수신 커넥터</a>을 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p>송신 커넥터</p></td>
<td><p>예</p></td>
<td><p>다음과 같은 구성 요소에 대 한 IPv6 주소 허용 됩니다.</p>
<ul>
<li><p>스마트 호스트 IP 주소</p></li>
<li><p>Edge 전송 서버에서 구성 된 송신 커넥터에 대 한 <em>SourceIPAddress</em> 매개 변수</p></li>
</ul>

> [!NOTE]
> <EM>SourceIPAddress</EM> 매개 변수에 대 한 IPv6 주소를 지정 하려는 경우 적절 한 DNS AAAA 및 메일 교환 (MX) 레코드가 올바르게 구성 되었는지 확인 합니다. 이렇게 하면 원격 메시징 서버에서 모든 종류의 지정 된 IPv6 주소에 역방향 조회 테스트를 시도 하는 경우 메시지 배달이 보장 합니다.


<p>자세한 내용은 <a href="send-connectors-exchange-2013-help.md">송신 커넥터</a>을 참조 하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>들어오는 메시지 속도 제한</p></td>
<td><p>부분</p></td>
<td><p>예: <em>MaxInboundConnectionPercentagePerSource</em> 매개 변수, 매개 변수는 <em>MaxInboundConnectionPerSource</em> 및 <em>TarpitInterval</em> 매개 변수는 수신 커넥터에서 설정할 수 있는 받는 메시지 속도 제한 글로벌 IPv6 주소에만 적용 됩니다. 링크 로컬 IPv6 주소 및 사이트 로컬 IPv6 주소 지정 된 모든 받는 메시지 속도 제한 하 여 영향을 받지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>통합 메시징</p></td>
<td><p>예</p></td>
<td><p>자세한 내용은 <a href="ipv6-support-in-unified-messaging-exchange-2013-help.md">통합 메시징의 IPv6 지원</a>을 참조 하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>데이터베이스 가용성 그룹 (DAG) 구성원</p></td>
<td><p>예</p></td>
<td><p>정적 IPv6 주소 Windows Server 및 클러스터 서비스에 의해 지원 됩니다. 그러나 정적 IPv6 주소를 사용 하는 모범 사례에 대해 이동 합니다. Exchange 2013 설치 하는 동안 정적 IPv6 주소 구성을 지원 하지 않습니다.</p>
<p>장애 조치 클러스터 사이트 내 자동 터널 주소 지정 ISATAP (프로토콜)를 지원합니다. 동적 DNS 등록을 허용 하는 IPv6 주소만 지원 합니다. 링크 로컬 주소는 클러스터에서 사용할 수 없습니다.</p>
<p>DAG 네트워크 요구 사항에 대 한 자세한 내용은 <a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">고가용성 및 사이트 복원 계획</a>에서 &quot;네트워크 요구 사항&quot; 섹션을 참조 하십시오.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 운영 체제에서 프로토콜을 사용 하지 않도록 설정 하거나 사용

Exchange 2013 서버는 i p v 6 네트워크를 완벽 하 게 지원 합니다. 따라서 i p v 6을 사용 하지 않는 경우에 Exchange 서버에서 i p v 6을 사용 하지 않도록 설정할 필요가 없습니다.

Exchange 2013 의 IPv6 지원에는 i p v 4를 설치 하 고 모든 Exchange 2013 서버에서 사용 하도록 설정 해야 합니다. I p v 4 Exchange 2013 서버에서 제거 하는 지원 되지 않습니다.

Microsoft Windows의 IPv6 지원에 대 한 자세한 내용은 참조 [Microsoft Windows에 대 한 IPv6: 질문과 대답](https://go.microsoft.com/fwlink/p/?linkid=147465)합니다.

맨 위로 이동

## IPv6 주소 기본 (영문)

IPv6 주소는 긴 128 비트입니다. 주소 콜론 16 진수 표기법을 사용 하 여 설명 합니다. 콜론 16 진수 표기법 콜론 (:)으로 구분 하 여 8 개의 16 비트, 4 자리 16 진수 숫자를 사용 하 여 128 비트 주소를 설명 합니다. IPv6 주소 콜론 16 진수 표기법에서의 예로 2001:0DB8:0000:0000:02AA:00FF:C0A8:640A 합니다.

다음 방법을 사용 하 여 IPv6 주소를 표현할 수 있습니다.

  - **앞에 0을 표시 하지 않습니다.**   IPv6 주소에 8 개의 4 자리 16 진수 번호 중 하나에서 앞에 오는 0을 생략할 수 있습니다.

  - **이중 콜론 압축**   모두 0을 포함 하는 인접 한 16 비트 16 진수를 나타내는 두 콜론 (:)를 사용할 수 있습니다. 이러한 모든 0 자릿수 시작, 중간 또는 IPv6 주소의 끝에 있을 수도 있습니다. IPv6 주소에 이중 콜론 압축 한 시간을만 사용할 수 있습니다.

  - **후행 십진수 표기법**   8 비트 자리에 마침표 (.) 구분 하 여 십진수 표기법에서 IPv6 주소의 끝에 마지막 32 비트를 표현할 수 있습니다. 십진수 표기법 후행 IPv4 호환 가능 주소와 자주 사용 됩니다.

다음 표에서 IPv6 주소 표기법과 해당 하는 IPv6 주소 구문을의 예제를 제공 합니다.

### IPv6 주소 표기법과 구문

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>IPv6 주소 표기법</th>
<th>IPv6 주소 구문</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>전체 IPv6 주소</p></td>
<td><p>2001:0DB8:0000:0000:02AA:00FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>IPv6 주소를 사용 하는 앞에 오는 0을 억제</p></td>
<td><p>2001:DB8:0:0:2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="odd">
<td><p>이중 콜론 압축을 사용 하는 IPv6 주소</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>뒤에 오는 십진수 표기법을 사용 하는 IPv6 주소</p></td>
<td><p>2001:DB8::2AA:FF:192.168.100.10</p></td>
</tr>
</tbody>
</table>


IPv6 주소는 다음과 같은 범주로 분류 됩니다.

  - **유니캐스트 주소**   패킷은 하나의 인터페이스에 전달 됩니다.

  - **멀티 캐스트 주소**   여러 인터페이스에 패킷을 전달 됩니다.

  - **애니캐스트 주소**   패킷을에 게 전달 되는 여러 인터페이스의 가장 가까운 합니다. 인터페이스 사이의 거리 라우팅 비용으로 정의 됩니다.

IPv6 유니캐스트 주소는 다음과 같은 가능한 범위:

  - **로컬 링크**   IPv6 주소 범위는 로컬 서브넷입니다. I p v 6 링크 로컬 주소 i p v 4 링크 로컬 주소에 자동 개인 IP 주소 지정 (APIPA)를 사용 하는 것과 비슷합니다.

  - **로컬 사이트**   IPv6 주소 범위는 로컬 조직입니다. 사이트 로컬 주소는 RFC 3879에서 더이상 사용 되지 않아 RFC 4193에 정의 된 로컬 주소를 고유 하 여 대체 합니다. I p v 6 사이트 로컬 주소 및 i p v 6 고유 로컬 주소는 i p v 4 개인 IP 주소를 비교할 수 있습니다.

  - **글로벌**   IPv6 주소 범위는 세상 합니다. I p v 6 전역 주소는 IPv4 공용 IP 주소와 비슷합니다.

다음 표에서 i p v 4와 i p v 6 요소가의 비교를 제공합니다.

### IPv4 및 IPv6 요소

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>항목</th>
<th>IPv4</th>
<th>IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>개인 IP 주소</p></td>
<td><p>10.0.0.0/8</p>
<p>172.16.0.0/12</p>
<p>192.168.0.0/16</p></td>
<td><p>FD00:: 8 /</p></td>
</tr>
<tr class="even">
<td><p>링크 로컬 주소</p></td>
<td><p>169.254.0.0/16</p></td>
<td><p>FE80:: / 64</p></td>
</tr>
<tr class="odd">
<td><p>루프백 주소</p></td>
<td><p>127.0.0.1</p></td>
<td><p>:: 1</p></td>
</tr>
<tr class="even">
<td><p>지정 되지 않은 주소</p></td>
<td><p>0.0.0.0</p></td>
<td><p>::</p></td>
</tr>
<tr class="odd">
<td><p>주소 확인</p></td>
<td><p>주소 확인 프로토콜 (ARP)</p></td>
<td><p>네트워크 환경 검색 (ND)</p></td>
</tr>
<tr class="even">
<td><p>도메인 이름 시스템 (DNS) 호스트 이름 확인</p></td>
<td><p>주소 record (레코드)</p></td>
<td><p>AAAA 레코드 또는 a 6 레코드</p></td>
</tr>
</tbody>
</table>


IPv6 주소 지정 하는 방법에 대 한 자세한 내용은 [IPv6 주소 유형](https://go.microsoft.com/fwlink/p/?linkid=98357)을 참조 하십시오.

## 지원 되는 IPv6 주소 입력된 형식

다음과 같은 유형의 IPv6 주소 입력된 형식 Exchange 2013 에서 지원 됩니다.

  - 단일 IPv6 주소를

  - IPv6 주소 범위를

  - 서브넷 마스크를 함께 IPv6 주소

  - 라우팅 CIDR (Classless Interdomain) 표기법을 사용 하는 서브넷 마스크를 함께 IPv6 주소

다음 표에서 Exchange 2013 에서 적절 한 IPv6 주소 입력된 형식의 예제를 제공 합니다.

### IPv6 주소 예

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>종류</th>
<th>IPv6 주소의 예</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>단일 주소</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>주소 범위</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A-2001:DB8::2AA:FF:C0A8:6414</p></td>
</tr>
<tr class="odd">
<td><p>서브넷 마스크와 함께 주소</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A(FFFF:FFFF:FFFF:FFFF::)</p></td>
</tr>
<tr class="even">
<td><p>CIDR 표기법을 사용 하는 서브넷 마스크와 함께 주소</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A / 64</p></td>
</tr>
</tbody>
</table>


Exchange 2013 다음과 같은 입력된 형식은 지원 됩니다.

  - 앞에 오는 0의 비 표시

  - 이중 콜론 압축

  - 뒤에 오는 십진수 표기법

맨 위로 이동

