---
title: '메시징 레코드 관리 오류 및 이벤트: Exchange 2013 Help'
TOCTitle: 메시징 레코드 관리 오류 및 이벤트
ms:assetid: 8bc3f5ae-403b-45af-86c1-b2fccab34e63
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb310783(v=EXCHG.150)
ms:contentKeyID: 51407721
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시징 레코드 관리 오류 및 이벤트

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

MRM(메시징 레코드 관리)을 사용하면 이벤트 뷰어에 표시되는 이벤트를 생성하고, 관리되는 폴더 도우미의 성능을 확인하며 문제를 해결할 수 있습니다. 이벤트 뷰어는 중요도에 따라 다음 순서로 다음과 같은 종류의 이벤트를 추적합니다.

1.  오류 이벤트

2.  경고 이벤트

3.  정보 이벤트

## MRM 오류 및 이벤트

다음 표에서는 MRM 문제를 해결하는 데 사용할 수 있는 이벤트 목록을 제공합니다. 로깅 유형에는 다음이 포함됩니다.

  - 레이블이 **LogAlways**로 지정된 이벤트는 항상 개별적으로 기록됩니다.

  - 레이블이 **LogPeriodic**으로 지정된 이벤트는 이벤트가 발생할 때마다 기록되는 것이 아니라 5분마다 한 번씩 기록됩니다. 이를 통해 과도한 로그 항목을 방지할 수 있습니다.

### 관리되는 폴더 도우미 범주에 있는 MRM 이벤트

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
<th><strong>이벤트 ID</strong></th>
<th><strong>범주</strong></th>
<th><strong>이벤트 유형</strong></th>
<th><strong>로깅</strong></th>
<th><strong>값 또는 설명</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10003</p></td>
<td><p>관리되는 폴더 도우미</p></td>
<td><p>오류</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Active Directory에서 서버 구성 개체를 가져올 수 없습니다. &lt;<em>예외 정보</em>&gt;. 도메인 컨트롤러 네트워크 연결 문제 또는 잘못된 DNS 구성이 없는지 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>10004</p></td>
<td><p>관리되는 폴더 도우미</p></td>
<td><p>오류</p></td>
<td><p>LogAlways</p></td>
<td><p>&lt;<em>사서함</em>&gt; 사서함의 &lt;<em>폴더</em>&gt; 폴더에 대한 보존 정책이 적용되지 않습니다. 관리되는 폴더 도우미는 &lt;<em>관리되는 폴더</em>&gt; 관리되는 폴더에 대한 &lt;<em>콘텐츠 설정</em>&gt; 관리되는 콘텐츠 설정을 처리할 수 없습니다. RetentionAction은 MoveToFolder이지만 대상 폴더가 지정되지 않았습니다. 대상 폴더를 지정하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>10005</p></td>
<td><p>관리되는 폴더 도우미</p></td>
<td><p>오류</p></td>
<td><p>LogAlways</p></td>
<td><p>보존 정책이 &lt;<em>사서함</em>&gt; 사서함의 &lt;<em>폴더</em>&gt; 폴더에 적용되지 않습니다. &lt;<em>관리되는 폴더</em>&gt; 관리되는 폴더에 대한 &lt;<em>콘텐츠 설정</em>&gt; 관리되는 콘텐츠 설정을 처리할 수 없습니다. RetentionAction은 MoveToFolder이지만 &lt;<em>폴더</em>&gt; 대상 폴더가 &lt;<em>폴더</em>&gt; 원본 폴더와 같습니다. 원본 폴더와 다른 대상 폴더를 지정하십시오.</p></td>
</tr>
<tr class="even">
<td><p>10009</p></td>
<td><p>관리되는 폴더 도우미</p></td>
<td><p>오류</p></td>
<td><p>LogAlways</p></td>
<td><p>Active Directory에서 감사 로그 매개 변수를 읽을 수 없어 관리되는 폴더 도우미가 로컬 서버의 모든 데이터베이스 처리를 건너뛰었습니다. 나중에 일정 창에서 다시 시도합니다. 현재 데이터베이스: &lt;<em>데이터베이스</em> &gt;</p></td>
</tr>
<tr class="odd">
<td><p>10010</p></td>
<td><p>관리되는 폴더 도우미</p></td>
<td><p>오류</p></td>
<td><p>LogAlways</p></td>
<td><p>감사 로그를 사용할 수 있지만 Active Directory에 감사 로그 경로가 없어 관리되는 폴더 도우미가 로컬 서버의 모든 데이터베이스 처리를 건너뛰었습니다. 나중에 일정 창에서 다시 시도합니다. 현재 데이터베이스: &lt;<em>데이터베이스</em> &gt;</p></td>
</tr>
<tr class="even">
<td><p>10011</p></td>
<td><p>관리되는 폴더 도우미</p></td>
<td><p>오류</p></td>
<td><p>LogAlways</p></td>
<td><p>관리되는 폴더 도우미가 감사 로그를 구성할 수 없습니다. 현재 데이터베이스 '%1' 처리를 중지합니다 '%1'. 나중에 일정 창에서 다시 시도합니다. 예외 정보: &lt;<em>정보</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10012</p></td>
<td><p>관리되는 폴더 도우미</p></td>
<td><p>오류</p></td>
<td><p>LogAlways</p></td>
<td><p>관리되는 폴더 도우미가 감사 로그에 쓰지 못했습니다. 현재 데이터베이스 &lt;<em>데이터베이스</em>&gt; 처리를 중지합니다. 나중에 일정 창에서 감사 로그에 쓰기를 다시 시도합니다. 예외 정보: &lt;<em>정보</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10017</p></td>
<td><p>관리되는 폴더 도우미</p></td>
<td><p>오류</p></td>
<td><p>LogAlways</p></td>
<td><p>사서함: &lt;<em>사서함</em>&gt; 폴더: 이름: &lt;<em>폴더 이름</em>&gt; ID: &lt;<em>폴더 ID</em>&gt; 항목: ID: &lt;<em>ID</em>&gt;를 처리하는 동안 관리되는 폴더 도우미에서 예외가 발생했습니다. 예외: &lt;<em>예외</em>&gt;.</p></td>
</tr>
</tbody>
</table>


### 도우미 범주의 MRM 이벤트

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
<th><strong>이벤트 ID</strong></th>
<th><strong>범주</strong></th>
<th><strong>이벤트 유형</strong></th>
<th><strong>로깅</strong></th>
<th><strong>값 또는 설명</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9004</p></td>
<td><p>도우미</p></td>
<td><p>경고</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>서비스</em>&gt;에서 &lt;<em>사서함</em>&gt; 사서함을 처리하지 못했습니다. 다음 예외로 인해 오류가 발생했습니다. &lt;<em>예외</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9014</p></td>
<td><p>도우미</p></td>
<td><p>경고</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. 일정 변경 내용을 처리할 수 없습니다. 다음 예외로 인해 오류가 발생했습니다. &lt;<em>예외</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9017</p></td>
<td><p>도우미</p></td>
<td><p>정보</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>데이터베이스</em>&gt; 데이터베이스의 &lt;<em>서비스</em>&gt;이(가) 예약된 시간 창을 시작하고 있습니다. 처리할 사서함이 &lt;<em>숫자</em>&gt;개 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>9018</p></td>
<td><p>도우미</p></td>
<td><p>정보</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>데이터베이스</em>&gt; 데이터베이스의 &lt;<em>서비스</em>&gt;이(가) 예약된 시간 창을 종료하고 있습니다. &lt;<em>숫자</em>&gt;개 중 &lt;<em>숫자</em>&gt;개의 사서함이 처리되었습니다. &lt;<em>숫자</em>&gt;개의 사서함은 오류 때문에 건너뛰었습니다. &lt;<em>숫자</em>&gt;개의 사서함은 별도로 처리되었습니다. &lt;<em>숫자</em>&gt;개의 사서함은 시간이 부족하여 처리되지 않았습니다.</p>

> [!NOTE]
> 다음에 관리되는 폴더 도우미를 실행할 때 이전에 중지되었던 곳부터 다시 시작됩니다.


</td>
</tr>
<tr class="odd">
<td><p>9019</p></td>
<td><p>도우미</p></td>
<td><p>경고</p></td>
<td><p>LogPeriodic</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>데이터베이스</em>&gt; 데이터베이스에서 &lt;<em>서비스</em>&gt;에 대한 진행률을 저장할 수 없습니다. (다음에 도우미가 시작할 때 중지 위치에서 다시 시작할 수 있도록 해당 위치를 저장할 수 없습니다.) 다음 예외로 인해 오류가 발생했습니다. &lt;<em>예외</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9020</p></td>
<td><p>도우미</p></td>
<td><p>경고</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>데이터베이스</em>&gt; 데이터베이스에 대해 &lt;<em>도우미 이름</em>&gt;을(를) 시작하지 못했습니다. 다음 예외로 인해 오류가 발생했습니다. &lt;<em>예외</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9021</p></td>
<td><p>도우미</p></td>
<td><p>정보</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>데이터베이스</em>&gt; 데이터베이스의 &lt;<em>서비스</em>&gt;이(가) 주문형 요청을 처리하고 있습니다. 처리할 사서함이 &lt;<em>숫자</em>&gt;개 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>9022</p></td>
<td><p>도우미</p></td>
<td><p>정보</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>데이터베이스</em>&gt; 데이터베이스의 &lt;<em>서비스</em>&gt;이(가) 주문형 요청을 완료했습니다. &lt;<em>숫자</em>&gt;개 중 &lt;<em>숫자</em>&gt;개의 사서함이 처리되었습니다. &lt;<em>숫자</em>&gt;개의 사서함은 오류 때문에 건너뛰었습니다.</p></td>
</tr>
<tr class="odd">
<td><p>9023</p></td>
<td><p>도우미</p></td>
<td><p>경고</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>서비스</em>&gt;에서 &lt;<em>데이터베이스</em>&gt; 데이터베이스에 대해 시간 창 처리를 시작할 수 없습니다. 다음 예외로 인해 오류가 발생했습니다. &lt;<em>예외</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9025</p></td>
<td><p>도우미</p></td>
<td><p>정보</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>서비스</em>&gt;이(가) &lt;<em>데이터베이스</em>&gt; 데이터베이스에서 &lt;<em>숫자</em>&gt;개 사서함을 건너뛰었습니다. 사서함: &lt;<em>사서함</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9026</p></td>
<td><p>도우미</p></td>
<td><p>경고</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>서비스</em>&gt;에서 &lt;<em>데이터베이스</em>&gt; 데이터베이스에 대한 주문형 처리를 시작할 수 없습니다. 다음 예외로 인해 오류가 발생했습니다. &lt;<em>예외</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9027</p></td>
<td><p>도우미</p></td>
<td><p>오류</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>데이터베이스</em>&gt; 데이터베이스에서 &lt;<em>사서함</em>&gt; 사서함을 처리하는 동안 &lt;<em>서비스</em>&gt;이(가) 프로세스를 &lt;<em>숫자</em>&gt;번 중지했습니다. 이 사서함은 더 이상 요청된 시간 창이나 주문형 요청에서 처리되지 않습니다. 다음 예외로 인해 오류가 발생했습니다. &lt;<em>예외</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9028</p></td>
<td><p>도우미</p></td>
<td><p>경고</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. &lt;<em>데이터베이스</em>&gt; 데이터베이스에서 &lt;<em>사서함</em>&gt; 사서함을 처리하는 동안 &lt;<em>서비스</em>&gt;이(가) 프로세스를 &lt;<em>숫자</em>&gt;번 중지했습니다. 다음 예외로 인해 오류가 발생했습니다. &lt;<em>예외</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9033</p></td>
<td><p>도우미</p></td>
<td><p>경고</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. 데이터베이스 &lt;<em>데이터베이스</em>&gt;의 &lt;<em>서비스</em>&gt;에서 주문형 요청을 받았습니다. 하지만 처리할 사서함이 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p>9034</p></td>
<td><p>도우미</p></td>
<td><p>정보</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>이(가) 데이터베이스 &gt; &lt;<em>데이터베이스</em>&gt;에서 관리되는 폴더 도우미의 시간 기반 작업을 중지했습니다.</p></td>
</tr>
<tr class="even">
<td><p>9035</p></td>
<td><p>도우미</p></td>
<td><p>경고</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. 시간이 부족하기 때문에 &lt;<em>도우미 이름</em>&gt;에서 &lt;<em>숫자</em>&gt;개의 사서함을 처리하지 못했습니다.</p></td>
</tr>
<tr class="odd">
<td><p>9037</p></td>
<td><p>도우미</p></td>
<td><p>오류</p></td>
<td><p>LogAlways</p></td>
<td><p>서비스 &lt;<em>서비스</em>&gt;. RPC를 처리하는 동안 예외가 발생했습니다. 메서드: &lt;<em>메서드</em>&gt;, 예외: &lt;<em>예외</em>&gt;</p></td>
</tr>
</tbody>
</table>

