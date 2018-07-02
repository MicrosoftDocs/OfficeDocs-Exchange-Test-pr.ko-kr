---
title: 'DLP 정책 검색 보고서 보기: Exchange 2013 Help'
TOCTitle: DLP 정책 검색 보고서 보기
ms:assetid: 5c3f1cf6-d8c7-4d83-bb24-641ea9d50cbc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150520(v=EXCHG.150)
ms:contentKeyID: 50482233
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DLP 정책 검색 보고서 보기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-16_

데이터 손실 방지 (DLP) 정책 검색 관리는 광범위 하 게 조직 식별, 조사 및 DLP 정책 위반을 해결 하기 위해 수행 하는 작업을 정의 합니다. 인시던트를 관리 하기 위해 DLP 정책에 의해 탐지 되는 항목을 식별 하는 정보에 대 한 액세스를 해야 합니다. 이 검색 정보는 기존 Microsoft Exchange Server 2013 데이터와 통합 됩니다 및 로그 나타나도록 서식을 설정 하 여 메일 흐름 문제를 관리 하는 데이터의 기존 풍부한 시스템을 활용할 수 있습니다.

단일 정책 검색 이벤트와 함께 문제 보고서 만들기 (영문) 하는 방법에 대 한 정보를 [DLP 정책 감지에 대 한 문제 보고서 만들기](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)을 참조 하십시오. 메시지 로그에 대 한 자세한 내용은 [배달 보고서로 메시지 추적](track-messages-with-delivery-reports-exchange-2013-help.md)을 참조 하십시오.


> [!NOTE]
> Exchange 2013: DLP는 CAL(Exchange Enterprise Client) 액세스 라이선스가 필요한 고급 기능입니다. CAL 및 서버 라이선스에 대한 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 라이선스</A>를 참조하세요.



## 감사 정보

Exchange의 DLP 검색 관리와 관련 된 데이터는 배달 보고서로 알려져 메시지 추적 로그에 통합 됩니다. 대부분의 시스템에서 사용할 수 있는 기존 로깅 프레임 워크의 다시 사용 하는 기능. 메시지 추적 로그 파일의 구조 이해 (영문)을 비롯 한 일반적인 내용은 [이해 메시지 추적](message-tracking-exchange-2013-help.md) 또는 [배달 보고서로 메시지 추적](track-messages-with-delivery-reports-exchange-2013-help.md)의 기존 콘텐츠를 검토 하십시오.

배달 보고서 모든 메시지 활동에 대 한 자세한 로그는 사서함 서버의 전송 서비스를 실행 하는 컴퓨터에서 메시지가 전송 됩니다. 메시지 추적 로그 **Get-MessageTrackingLog** cmdlet을 사용 하 여 Exchange 관리 셸을 통해 액세스할 수 있습니다. DLP 데이터는 기존 데이터 형식 및 규칙에 따라 배달 보고서에 통합 됩니다.

## 데이터 로깅 형식

메일 흐름 콘텐츠 처리와 관련 된 에이전트에서 데이터를 포함 하는 메시지 추적 로그. DLP, 전송 규칙 에이전트 (다음) 상세 메시지 콘텐츠 검사를 호출 하 고는 ETRs의 일부로 정의 된 정책을 적용 하려면 사용 됩니다. DLP에 추가할 기존 AgentInfo 이벤트는 사용 하는 항목의 메시지 추적 로그에서에서 관련 합니다.

에이전트 이름 AgentInfo 이벤트에서 **다음** 또는 **전송 규칙 에이전트** 됩니다. 메시지에 적용 된 DLP 처리를 설명 하는 메시지 당 단일 AgentInfo 이벤트가 기록 됩니다. 메시지 추적 로그 항목 필드의 **CustomData** 필드는 전송 규칙 에이전트에 의해 기록 되는 DLP 데이터 표시 되는 위치. 이 필드는 여러 항목을 포함할 수: 메시지, 메시지에 적용 되는 각 규칙에 대 한 규칙을 하나 선 및 부하 또는 실행 시간이 임계값을 초과 하는 각 규칙에 대 한 상태 모니터링 줄에 있는 각 데이터 분류에 대 한 데이터 분류 및 클라이언트 정보 선입니다.

DLP 로그 항목의 예는 여기에 표시 됩니다. 문자열 사이 새 줄와 별도 줄에 표시 하는 출력 포맷 하였습니다.

원본: 에이전트

이벤트 Id: AGENTINFO

CustomData: S:TRA DC = | dcid 41BFDBC6C9D811E0816A3CD34824019B = | count = 10 | conf 77; =

S:TRA DC = | dcid C7ECCBA0CA0011E0B6C00B124924019B = | count = 3 | conf; 81 =

S:TRA CI = | sndOverride = 또는 | 방금 비즈니스 이유 =

S:TRA=CI|sndOverride=fp;

S:TRA=ETR|ruleId=FC2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=PrependSubject|action=Encrypt|sev=2|mode=audit|dcid=41BFDBC6C9D811E0816A3CD34824019B|sndOverride=or;

S:TRA=ETR|ruleId=AB2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=Encrypt|sev=1|mode=enabled|dcid=C7ECCBA0CA0011E0B6C00B124924019B|sndOverride=fp;

S:TRA=ETRP|ruleId=C27D21EECA0311E0BCB896154924019B|LoadW=200|LoadC=100|ExecW=5500|ExecC=200;

전송 규칙 에이전트의 ID, DLP 정책 ID (선택 사항) 마지막으로 수정한 날짜, 작업, 심각도, 모드, 규칙의 그룹화 한 (선택 사항) 데이터 분류를 감지 하 고 규칙 ID를 기반으로 보낸 사람이 재정의 (선택 사항) 요구 사항은 (에 지정 된 "다음 ETR =" 로그 줄에서). 또한 데이터 분류 ID, count 및 분류의 신뢰 수준을 분류 이름으로 그룹화 할 필요 (에 지정 된 "다음 DC =" 로그 줄에서).

추가 그룹화 데이터 분류 ID, 보낸 사람이 재정의 (선택 사항)를 포함 하 고 클라이언트에서 발견 된 모든 분류에 대 한 데이터 분류 ID에 따라 맞춤 (선택 사항)를 재정의 (에 지정 된 "다음 CI =" 로그 줄에서). 전송 규칙 에이전트의도 요구 사항은 규칙 ID, 벽 시계 (선택 사항), 부하 CPU 클록 (선택 사항), 실행 벽 시계 (선택 사항) 및 실행 CPU 부하 부하 또는 실행 벽 또는 CPU를 초과 하는 모든 규칙 클럭 임계값에 대해 시계 (선택 사항) 규칙 ID로 그룹화 (지정 된 "다음 ETRP =" 로그 줄에서).

다음은 데이터 필드의 전체 목록입니다. 모든 데이터의 MTL에은 형식 문자열입니다. 형식 열에서 메시지 추적 로그의 각 필드를 인식 하는 방법을 설명 합니다. 선택적 필드 열 지정 기능 필드 되지 않을 수도 있습니다 일치 하는 규칙을 기록 합니다. DLP 특정 열 DLP 기능 관련 있는 필드를 나타냅니다.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>필드 이름</strong></p></td>
<td><p><strong>설명</strong></p></td>
<td><p><strong>형식</strong></p></td>
<td><p><strong>선택적 필드</strong></p></td>
<td><p><strong>DLP 관련</strong></p></td>
</tr>
<tr class="even">
<td><p>다음</p></td>
<td><p>전송 규칙 에이전트입니다. AgentName를 입력 합니다.</p></td>
<td><p>다음 DC, ETR, CI, 또는 ETRP =</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>DC</p></td>
<td><p>데이터 분류 합니다. 그룹 이름 입력</p></td>
<td><p>다음 DC =</p></td>
<td><p>옵션</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>ETR</p></td>
<td><p>Exchange 전송 규칙입니다. 그룹 이름 입력</p></td>
<td><p>다음 ETR =</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>CI</p></td>
<td><p>클라이언트 정보, 형식 그룹 이름</p></td>
<td><p>다음 CI =</p></td>
<td><p>옵션</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>ETRP</p></td>
<td><p>Exchange 전송 규칙 성능이 개선 됩니다. 그룹 이름 입력</p></td>
<td><p>다음 ETRP =</p></td>
<td><p>옵션</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>dcid</p></td>
<td><p>데이터 분류의 ID</p></td>
<td><p>dcid = GUID</p></td>
<td><p>옵션</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>count</p></td>
<td><p>데이터 분류의 수</p></td>
<td><p>count = 정수</p></td>
<td><p>옵션</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>회의</p></td>
<td><p>데이터 분류의 신뢰 수준</p></td>
<td><p>회의 = 정수 (%)</p></td>
<td><p>옵션</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>sndOverride</p></td>
<td><p>보낸 사람이 재정의 합니다. 필드 선택 사항입니다.</p>
<p>다음 CI 선 = 필드로 설정 된 &quot;또는&quot; 데이터 분류를 재정의 하는 의미 있는 경우. 필드로 설정 된 경우 &quot;fp&quot; 데이터 분류 가양성으로 보고 된 것을 의미 합니다.</p>
<p>다음 ETR 줄 = 규칙의 일부를 재정의 또는 필드로 설정 된 &quot;또는&quot; 규칙을 의미 있는 경우. 필드로 설정 된 경우 &quot;fp&quot; 의미 규칙 또는 규칙의 일부 가양성으로 보고 되었습니다.</p></td>
<td><p>sndOverride = 또는 또는 fp</p>
<p>여기서 &quot;또는&quot; 나타냅니다 재정의 하 고 &quot;fp&quot; 가양성을 의미 합니다. SndOverride 필드는이 매개 변수가 재정의 또는 가양성 규칙에 대 한 최종 사용자가 보고 했습니다.</p></td>
<td><p>옵션</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>방금</p></td>
<td><p>양쪽 맞춤입니다. 필드 항목은 선택적 이며만 사용할 수 있는 보낸 사람이 재정의 필드에 &quot;또는&quot;는 다음에는 다음과 같을 경우 CI 선 = 합니다. 근거 텍스트 제공한 최종 사용자가 데이터 분류를 재정의 해야 합니다.</p></td>
<td><p>방금 = 정보 근로자가 입력된 근거 문자열</p>
<p>양쪽 맞춤 필드는 최종 사용자는 재정의 보고 하는 경우에 기록 됩니다.</p></td>
<td><p>옵션</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>ruleId</p></td>
<td><p>규칙 ID</p></td>
<td><p>ruleId=GUID</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>dlpId</p></td>
<td><p>DLP 정책에 대 한 ID입니다. 필드는 선택 사항입니다. 없음 dlpId 없으면 규칙 DLP 정책에 속하지 않습니다.</p></td>
<td><p>dlpId=GUID</p></td>
<td><p>옵션</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>st</p></td>
<td><p>규칙의 마지막으로 수정한 날짜</p></td>
<td><p>st UTC 날짜 및 시간 =</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>작업</p></td>
<td><p>규칙,이 수행한 작업 규칙 당 여러 작업을 가질 수 있습니다.</p></td>
<td><p>동작 = 단일 작업</p>
<p>규칙에 대해 적용 하는 여러 작업을 하는 경우 여러 작업 필드 됩니다.</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>sev</p></td>
<td><p>규칙의 감사 심각도</p></td>
<td><p>sev = 1, 2 또는 3</p>
<p>1 낮은 나타냅니다, 여기서 2는 중간 규모 및 3 높은 것을 의미 합니다.</p></td>
<td><p>옵션</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>모드</p></td>
<td><p>상태 규칙의 되었을 때 적중 (적용, 감사, 또는 auditandnotify) 합니다.</p></td>
<td><p>모드 = 감사, auditandnotify, 또는 적용</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>loadW</p></td>
<td><p>부하 벽 시계입니다. 필드는 선택 사항</p></td>
<td><p>loadW = ms에는 시간</p></td>
<td><p>옵션</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>loadC</p></td>
<td><p>CPU 클럭; 로드 필드는 선택 사항</p></td>
<td><p>loadC = ms에는 시간</p></td>
<td><p>옵션</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>execW</p></td>
<td><p>실제 시계;를 실행 합니다. 필드는 선택 사항</p></td>
<td><p>execW = ms에서 시간</p></td>
<td><p>옵션</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>execC</p></td>
<td><p>CPU 클럭;를 실행 합니다. 필드는 선택 사항</p></td>
<td><p>execC = ms에서 시간</p></td>
<td><p>옵션</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>메시지 id</p></td>
<td><p>메시지의 ID</p></td>
<td><p>메시지 id = 메시지의 ID</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>date-time</p></td>
<td><p>세계시에서 메시지를 보낸 날짜 및 시간</p></td>
<td><p>날짜 및 시간 = UTC 날짜 및 시간</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>보낸사람 주소</p></td>
<td><p>보낸사람 필드에 지정 된 전자 메일 주소</p></td>
<td><p>보낸사람 주소 = 전자 메일 주소</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>받는 사람 주소</p></td>
<td><p>메시지의 받는 사람에 게의 주소를 전자 메일로 보내기</p></td>
<td><p>받는 사람 주소 = 전자 메일 주소</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>메시지 제목</p></td>
<td><p>메시지의 제목 필드에 있는 데이터</p></td>
<td><p>메시지 제목 = 최종 사용자 입력된 제목 문자열</p></td>
<td><p>필수</p></td>
<td><p>아니요</p></td>
</tr>
</tbody>
</table>


## 자세한 내용

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[DLP 정책 감지에 대 한 문제 보고서 만들기](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)

[배달 보고서로 메시지 추적](track-messages-with-delivery-reports-exchange-2013-help.md)

