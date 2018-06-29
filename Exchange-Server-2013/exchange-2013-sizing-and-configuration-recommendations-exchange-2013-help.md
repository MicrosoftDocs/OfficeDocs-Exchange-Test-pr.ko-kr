---
title: 'Exchange 2013 크기 조정 및 구성 권장 사항: Exchange 2013 Help'
TOCTitle: Exchange 2013 크기 조정 및 구성 권장 사항
ms:assetid: 4c4ba2fc-014a-46fb-949a-2dabba92c4a5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn879075(v=EXCHG.150)
ms:contentKeyID: 63763757
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 크기 조정 및 구성 권장 사항

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-03-27_

Exchange 2013은 이전 버전의 Exchange 보다 더 많은 시스템 리소스를 까다로운 수입니다. 올바르게 Exchange 2013 인프라가 크기를 조정 하 고 해당 인프라 내에서 Exchange 관련 구성 요소에 권장 되는 일부 구성 후, 하 여 최적으로 수행 하는 배포에 대 한 토대 수 있습니다.

## Exchange 2013 크기 조정

Exchange 2013 크기 조정 올바르게 성능 문제를 방지 하는 가장 효과적인 방법 중 하나입니다. Exchange 2013 서버 역할 요구 사항 계산기는 [사용할 수 있는 여기](https://go.microsoft.com/fwlink/p/?linkid=523844)입니다. 최신 버전 6.6, 이지만 다시 확인 하는 것이 좋습니다 업데이트를 위한 업그레이드를 주기적으로 합니다. 이 계산기를 제대로 사용 하 여 [Exchange 2013 서버 역할 요구 사항 계산기](https://go.microsoft.com/fwlink/p/?linkid=386677) 및 [크기 조정 Exchange 2013 배포](https://go.microsoft.com/fwlink/p/?linkid=301990) 블로그 게시물에 대 한 지침에 문의 해야 합니다.

다음은 계산기를 구입 하 고, 하드웨어를 배포 하기 전에 시작을 고려해 야 먼저 계산기 결과에 따라 전체 리소스 요구 사항을 결정 해야 합니다. 다음은 계산기를 사용 하 여 조직의 요구 사항에 입력 수 있으며 사용자의 하드웨어를 확장 하는 방법에 대 한 지침에 대 한 결과 사용 하 여 수 있습니다. 계산기 알 수 없는 사용 하 여 서버 수 있지만 지정 된 서버 집합에는 Exchange 작업의 영향을 예측 수 있습니다. 하드웨어를 충족 하기 위해 성능, 어떻게 적용 되었는지 확인 하려면 다른 구성을 사용 하 여 학습 해야 하 고 비즈니스 요구를 환경에 특정 키를 누릅니다.

하기 위해 하드웨어의 모범 사례를 살펴보고 배포 간소화, Exchange 제품 그룹은 다중 역할 서버 권장 합니다. 요청을 처리 하는 동안 오류 시나리오를 사용할 수 있는 클라이언트 액세스 서버를 더 수 만큼 제공 클라이언트 액세스 서버 (CA) 계층에서 가용성을 향상 서버가 다중 역할을 사용 합니다. Exchange 2013에 대 한 주요 디자인 고려 사항 (수직 확장 하는 대신 확장) "작은" 상품 유형 서버를 활용 하는 것입니다. 최대 20 개 프로세서 코어, 최대 96 기가바이트 (GB ram)를 포함 하는 두 소켓 컴퓨터와 디자인 및 테스트 했습니다. 하드웨어를이 값 보다 큰 경우 해당 하드웨어를 사용 하 여 다른 요구 사항에 대해 Exchange 2013 환경의 더 작은 서버를 구입 하 고 가상화 등의 다른 옵션을 고려해 야 합니다.

더 많은 서버 (수평 확장) (수직 확장) 하는 기존, 더 큰 서버에 리소스를 추가 하는 것 보다를 구축 하는 것이 좋습니다. 수평 확장 환경을에 Exchange 2013의 기본 제공 고가용성 기능을 활용할 수 있습니다. 이 구성은 권장 되는 이유를 이해 하려면 검토 하십시오 자세하게에서 [기본적으로 사용 되는 아키텍처](https://go.microsoft.com/fwlink/p/?linkid=523782) 및 [가용성에 대 한 사이트 복원 력 영향](https://go.microsoft.com/fwlink/p/?linkid=523845)게시물 합니다.

다음은 계산기를 Exchange (내부적으로 개발 된 응용 프로그램 포함)을 고려 하 여 크기 조정 하는 동안 해야 해야 즉와 상호작용 하는 제품 또는 Exchange 서버에서 실행 되는 계정 타사 제품에 사용 되지 않습니다. Lync 서버 및 타사 Exchange 웹 서비스 (EWS) 응용 프로그램 및 ActiveSync 장치는 사용자 당 CPU 요구 사항 모두 상당히 높일 수 있습니다. Exchange에 영향을 방법에 대 한 내용은 타사 제품 설명서를 참조할 수 있습니다. 타사 솔루션을 구현 하기 전에 Exchange에 대 한 성능 초기 계획을 만드는 것이 좋습니다.

## 권장 되는 성능 구성

Exchange 2013 환경에 대 한 다음과 같은 성능 최적화를 사용 하는 것이 좋습니다.

## 전원

BIOS는 OS (운영 체제) 전원 관리를 허용 하도록 설정 합니다.

운영 체제에서 고성능 전원 관리 옵션을 설정 합니다.

## 처리

실제 Exchange 서버에 대해 하이퍼스레딩을 해제 합니다. 실제 서버에서 하이퍼스레딩을 사용할 수 있습니다, 가상화 하는 경우 수 있지만 각 가상 서버만 할당 되는 가상 Cpu (가상 Cpu를 할당할 재정의 하지), 필요한 수만 계산 크기 조정의 실제 프로세서 코어 수를 활용 하 고 있습니다.

Exchange Server 2013 서비스 팩 1 이상을 설정할 수 있습니다 SSL를 클라이언트 액세스 서버에서 CPU 소비를 줄이려면 오프 로딩 하지만 SSL 오프 로딩의 복잡 한 구성의 이점을 가치가 되지 않을 수 있습니다.

## .NET Framework


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 버전</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p> X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


다음 Microsoft 기술 자료를 참조 하십시오.net 4.5.2를 설치할 수 없는 경우 문서 2995145 "[성능 문제 또는 Exchange Server 2013 Windows 서버에서 실행 하는에 연결할 때 지연](https://go.microsoft.com/fwlink/p/?linkid=524159)." 해당 문서의 픽스 저장소 작업자 프로세스 메모리 사용률에 내부 결과에 따라 개발 되었습니다. 이러한 수정 프로그램을 적용 하 여 모든 관리 되는 프로세스 (저장소 작업자 프로세스가 포함)에 대 한 전체 메모리 소비를 줄일 수 있습니다 및.NET 가비지 수집에 소요 된 전체 CPU 시간을 줄일 수 있습니다.

## 핫픽스

Exchange 성능 팀에는 다음과 같은 성능 관련 핫픽스를 모두 설치 하는 것이 좋습니다.

  - [Windows Server 2012의 클러스터 복구 기능을 향상 하는 업데이트를 사용할 수](https://go.microsoft.com/fwlink/p/?linkid=524088)

  - [권장 되는 핫픽스 및 Windows Server 2012 기반 장애 조치 클러스터에 대 한 업데이트](https://go.microsoft.com/fwlink/p/?linkid=524089)

  - [권장 되는 핫픽스 및 Windows Server 2012 R2 기반 장애 조치 클러스터에 대 한 업데이트](https://go.microsoft.com/fwlink/p/?linkid=524090)

  - [Windows 8 또는 다중 코어 프로세서가 설치 된 Windows Server 2012 기반 컴퓨터에서 잘못 된 RSS 프로세서 배정](https://go.microsoft.com/fwlink/p/?linkid=324140)

  - [성능 문제 또는 Windows Server에서 실행 되는 Exchange Server 2013에 연결할 때 지연](https://go.microsoft.com/fwlink/p/?linkid=312962)

  - [Outlook 연결 문제 SSLOffloading은 "True" Exchange 2013 하는 경우](https://go.microsoft.com/fwlink/p/?linkid=524091)

  - [Exchange Server 2013의 데이터베이스 장애 조치 후 Outlook에 대 한 긴 서버 연결](https://go.microsoft.com/fwlink/p/?linkid=524092)

  - [Outlook Web App Lync는 Exchange Server 2013와 통합 하는 경우의 성능 저하](https://go.microsoft.com/fwlink/p/?linkid=524093)

  - [EMS Exchange Server 2013 누적 업데이트 5 환경에서 첫번째 명령을 실행 하려면 오래 걸림](https://go.microsoft.com/fwlink/p/?linkid=524094)

  - [Exchange Server 2013에서 i p v 6을 설정한 경우 라우팅 대기 시간을 메시지](https://go.microsoft.com/fwlink/p/?linkid=524095)

  - [WIndows Server 2008 R2 s p 1에서 Microsoft LDAP 클라이언트에 의존 하는 응용 프로그램에 의해 높은 CPU 사용량](https://go.microsoft.com/fwlink/p/?linkid=530287)

  - [CPU 사용률이 높은 RPC over HTTP 프로토콜 Windows 8.1 또는 Windows Server 2012 r 2를 사용 하는 경우](https://go.microsoft.com/fwlink/p/?linkid=619127)

## 네트워킹

Exchange 2013과 함께 단일 네트워크 어댑터는 것이 좋습니다, MAPI 및 복제 네트워크를 분할 하는 데 필요한 것이 더 이상. 자세한 내용은 [네트워크 요구](planning-for-high-availability-and-site-resilience-exchange-2013-help.md) 를 참조 하십시오.

기본 SNP를 사용할 수 있는 설정 오프 로드 및 RSS를 사용 해야를 사용 하 여 (기본 설정 Windows Server 2012 및 그 이후 버전). RSS는 10GbE에 특히 배율 CPU 사용률을 도움이 됩니다.

운영 체제는 하지 기능을 해제 전원을 절약 하기 위해 네트워크 카드를 확인 합니다.

NIC 드라이버를 최신 상태로 유지 관리 합니다. 관련 드라이버 업데이트에 대 한 매달 공급 업체에 문의 확인 합니다.

## IIS(인터넷 정보 서비스)

설치 하는 동안 Exchange IIS에 대 한 연결 제한 일부를 수정합니다. 더 이상 IIS의 조정 하는 것이 좋습니다.

가능 하면 항상 사용자 지정을 하지 마십시오. Web.config 또는 레지스트리 키에 어떠한 변경 시 데이터베이스 덮어쓰기 가능 Exchange 누적 업데이트 또는 Windows를 업데이트 합니다.

## 저장소

Exchange 2013 저장소에 대 한 지침을 [Exchange 2013 저장소 구성 옵션](exchange-2013-storage-configuration-options-exchange-2013-help.md)사용할 수 있습니다.

## 가상화

[하드웨어 가상화를 위한 요구 사항](exchange-2013-virtualization-exchange-2013-help.md)을 검토 하십시오. Exchange 인식 균일 하지 않은 메모리 액세스 (NUMA) 없는 메모 또한입니다. 따라서 하드웨어 제조업체의 기본 NUMA 설정을 사용 하는 것이 좋습니다.

## Active Directory

Active Directory 쿼리 Exchange 배포에 직접 영향을 줄 때문에 디렉터리 서버 성능을 모니터링 합니다.

LDAP 검색 시간은 Active Directory 상태에 관해서는 측정 하는 중요 한 카운터입니다. 도메인 컨트롤러에서 CPU를 모니터링 합니다. 도메인 컨트롤러에서 CPU 문제는 Exchange 서버의 적중 성능으로 렌더링 합니다.

기본 제공에서 실행 "Active Directory 진단" 성능 모니터 "데이터 수집기 집합" 도메인 컨트롤러 성능 문제의 원인을 확인할 수 있도록 아래에 있는 도메인의 도메인 컨트롤러에서.

전체 AD 데이터베이스 파일 수 캐시를 도메인 컨트롤러에 충분 한 RAM 대 한 계획.

(64 비트 글로벌 카탈로그 코어 기준) 현재 부하를 처리 하는 하는 모든 사서함 8 개 코어에 대 한 Active Directory 글로벌 카탈로그 코어를 배포 하는 것이 좋습니다.

## 부하 분산

모든 클라이언트 액세스 서버는 동일한 들어오는 연결 수 약 받아야 합니다.

모든 프로토콜에 대해 Exchange 2013에는 지정 된 클라이언트 액세스 서버와 부하 분산 장치 간의 세션 선호도 필요 하지 않습니다.

클라이언트 액세스 서버에 모든 인바운드 트래픽을 관리 하기 위해 하드웨어 또는 소프트웨어 부하 분산 장치를 사용 해야 합니다. "라운드 로빈," 각 인바운드 연결 순환 목록에서 다음 대상 서버로 이동 하는 등의 방법을 사용 하거나 "최소 연결," 부하 분산 장치 당시에 가장 적은 설정 된 연결 된 서버에는 각 새 연결을 보내는 대상 서버 선택 영역을 확인할 수 있습니다. 이러한 방법을 자세히 나와 [부하 분산](load-balancing-exchange-2013-help.md)에 추가 합니다. 또한 다음 고려해 야 합니다.

  - 라운드 로빈 느린 수렴 수명이 긴 연결 (예: RPC/HTTP)을 포함 하는 문제를 있습니다. 새 컴퓨터 온라인 상태가 되는 대상 컴퓨터에서 처리 하는 연결의 균형 수렴 시간이 매우 오래 걸립니다.

  - "최소 연결" 메서드인 것 이며 오버 로드 되는 클라이언트 액세스 서버에 대 한 가능한 응답 하지 않는 클라이언트 액세스 서버 중단 하는 동안 또는 유지 관리 패치를 적용 하는 동안을 염두에 두어야 합니다. Exchange 성능이의 컨텍스트에서 인증은 부담이 큰 작업입니다.

다양 한 [부하 분산](load-balancing-exchange-2013-help.md)자세히 설명 하는 Exchange 2013 환경에서 함께 Windows 네트워크 부하 분산 (NLB) 제한으로 인해 좋지 않습니다 Windows NLB를 사용 하 여.

## 사용자 및 데이터베이스 배포

데이터베이스와 서버당 활성 데이터베이스 당 사용자 잘 균형 있게 배포를 유지 관리 합니다. 균등 하 게 데이터베이스 디스크 공간 사용량을 분산으로 높은 사용자가 모든 데이터베이스에 걸쳐 균형 있게 조정 합니다.

Exchange (장치, Outlook 및 OWA)과 성능 관점에서 볼 때 이러한 상호작용 포함 될 영향 작용 하는 방식을 이해 하기 위해 기본 사용자 프로필을 작성 해야 합니다. 참조 하십시오 계산기 블로그 구역 2에서 Exchange 사용 사용자 당 프로필 하는 방법 이해.

장애 조치 또는 전환 하는 동안 간의 균형을 유지 하기 위해 DB 복사본 활성화 기본 설정 및 "MaximumPreferredActiveDatabases" (서버당) 설정을 구성 합니다.

RedistributeActiveDatabases.ps1 스크립트는 균형을 다시 활성 데이터베이스 DAG 노드.

Office 365와 일치 하는 엄격한 항목 수 제한 적용 (영문) 하는 것이 좋습니다. Set-mailbox cmdlet 및 [사서함 폴더 제한](https://go.microsoft.com/fwlink/p/?linkid=398779)에서 제공 되는 정보로이 수행할 수 있습니다.

## 페이지 파일

32GB 이상 RAM 사용 하는 경우 32778 MB의 페이지 파일에 대 한 최대 크기를 설정 합니다.

Exchange 데이터베이스 파일 또는 데이터베이스 로그 파일와 동일한 드라이브에 페이지 파일을 호스팅할 수 해야 합니다.

필수적 고정된 크기 페이지 파일을 사용 하 고 크기를 관리 하는 Windows를 허용 하지 않음 페이지 파일 크기를 증가 성능을 매우 많이 수행 작업은 매우 고 Exchange 스트레스 받고 때 문제가 발생할 수 있습니다.

전체 커널 덤프를 가져올 필요가 전용된 덤프 파일에 대 한 Microsoft 기술 자료 문서 969028, [커널 또는 Windows Server 2008 및 Windows Server 2008 r 2의 전체 메모리 덤프 파일을 생성 하는 방법](https://go.microsoft.com/fwlink/p/?linkid=524044)사용 합니다.

## Outlook이 모드

캐시 된 모드를 사용 하는 것이 좋습니다. 캐시 된 모드를 사용 하는 이점은 [캐시 된 Exchange 모드와 Outlook 2013에 대 한 온라인 모드 간에 선택](https://go.microsoft.com/fwlink/p/?linkid=524045)참조 하십시오.

것은 성능 서버 추가 기능 및 Outlook 제 3 자 추가 기능 모두에 의해 영향을 받을 수 있는지 확인 하는 것이 중요 합니다. 온라인 모드를 사용 하는 경우 클라이언트에서 제 3 자 추가 기능, 높은 항목 수, 제한 된 보기, 기타 요소는 사서함 액세스 하는 사용자 수가 일부 성능 문제를 이용할 수 있습니다. 레거시 클라이언트는 Outlook 2013가 보다 높은 항목 수 및 성능 하 여 더 많은 영향을 경험할 수 있습니다.

조직에서 외부에서 Outlook 온라인 모드에서 구성 하는 주된 이유 관련 보안 문제에 대 한 경우에 BitLocker를 대신 사용 하는 것이 좋습니다.

Outlook 2013 OST 파일의 크기 및 다운로드 시간을 최소화 하기 위해 새 "동기화 슬라이더" 기능을 제공 합니다. 자세한 내용은 [Outlook 2013에서 캐시 된 Exchange 모드 구성](https://go.microsoft.com/fwlink/p/?linkid=390456) 를 참조 하십시오.

사용자 환경에서 지원 되는 Outlook 클라이언트 업데이트를 매월를 확인 합니다.

## 제 3 자 소프트웨어

최상의 방법으로 제거 또는 Exchange 성능 문제를 해결 하는 동안 제 3 자 소프트웨어를 비활성화 합니다. 다음 목록에는 Microsoft 기술 지원 서비스 Exchange 2013 성능에 영향을 주는 볼 가장 자주는 제 3 자 소프트웨어의 종류를 포함 합니다.

  - 바이러스 백신 솔루션

  - 침입 방지 소프트웨어

  - 백업 소프트웨어

  - 파일 및 사용자 모두에 대 한 감사 소프트웨어

  - 보관 솔루션

