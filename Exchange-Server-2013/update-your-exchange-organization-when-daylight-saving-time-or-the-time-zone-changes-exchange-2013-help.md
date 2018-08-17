---
title: '일광 절약 시간제 또는 표준 시간대를 변경 하는 경우 Exchange 조직 업데이트: Exchange 2013 Help'
TOCTitle: 일광 절약 시간제 또는 표준 시간대를 변경 하는 경우 Exchange 조직 업데이트
ms:assetid: 5b12615c-24cf-4f46-bf3c-2334dc734ef8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh530051(v=EXCHG.150)
ms:contentKeyID: 66452419
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 일광 절약 시간제 또는 표준 시간대를 변경 하는 경우 Exchange 조직 업데이트

 

_**적용 대상:** Exchange Online, Exchange Server, Exchange Server 2010, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

조직이나 사용자 일부가 거주하는 국가나 지역에서 DST(일광 절약 시간제)를 인식하는 정책을 변경하거나 UTC(협정 세계시)에서 현지 시간 오프셋을 변경한 경우 Microsoft Windows, Microsoft Exchange, Microsoft Outlook 또는 기타 프로그램을 이러한 변경에 맞게 업데이트해야 합니다.

링크를 포함 하는 전세계 DST 변경 사항에 대 한 자세한 내용은 [Microsoft 일광 절약 시간제 도움말 및 지원 센터](https://go.microsoft.com/fwlink/p/?linkid=99640)을 참조 하십시오. 또한 지원 추가 업데이트를 모두 요구 하는 경우를 보는 다른 소프트웨어 공급 업체의 웹사이트를 방문 합니다.

표준 시간대가 변경되지 않아도 다른 컴퓨터나 사용자와 전역으로 상호 작용하는 경우 컴퓨터에서 세계 다른 국가의 정확한 날짜와 시간 계산을 수행할 수 있어야 합니다.

가능한 빨리 표준 시간대 업데이트를 설치하면 기존 날짜와 시간을 새로운 날짜와 시간으로 전송하는 동안 예약된 회의나 약속 수를 최소화할 수 있습니다.

## 어떻게 해야 합니까?

## 1단계: 모든 클라이언트 및 데스크톱 컴퓨터에 Windows DST 업데이트 설치

DST 또는 표준 시간대가 변경되면 Office 365 인증 시스템이 업데이트되므로 모든 Office 365 클라이언트 컴퓨터를 업데이트해야 합니다. 그렇지 않으면 연결 문제가 발생할 수 있습니다.

  - 모든 클라이언트 및 데스크톱 컴퓨터 Windows DST 업데이트 설치 되어있는지 확인 합니다. 자세한 내용은 [Microsoft Windows 운영 체제에 대 한 일광 절약 시간제를 구성 하는 방법](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=914387)를 참조 합니다.

## 2단계: 모든 서버에 Windows DST 업데이트 설치

1.  Windows DST 업데이트를 사용하여 모든 온-프레미스 서버를 업데이트합니다.

2.  Office 365를 실행 중이면 DirSync 또는 AD FS 서버 등 Office 365 인증 시스템과 상호 작용하는 서버를 업데이트합니다. 이러한 서버를 업데이트하여 가동 시간을 보장합니다.

**참고 사항**   서버 클러스터를 업데이트 하는 경우 클러스터를 업데이트 하는 일반적인 프로세스를 수행 해야 합니다. 하면 수동 서버를 먼저 업데이트, 수동 서버 (활성화 됨), 장애 조치 파일과 이전 활성 (이제 수동) 서버를 업데이트 합니다. 서버 클러스터 및 고가용성 서버 클러스터를 업데이트 하는 방법에 대 한 자세한 내용은 Exchange 서버 클러스터 및 높은 가용성 서버 업데이트 및 [Windows Server 장애 조치 클러스터를 업데이트 하는 방법](https://support.microsoft.com/en-us/kb/174799)를 참조 하십시오.

## 3 단계: 업데이트 Exchange 및 Outlook, 클라이언트 및 데스크톱 컴퓨터에서 필요한 곳에

1.  사용자는 Outlook 2007 또는 이전 버전의 클라이언트를 사용 하는 경우 결정 Exchange 또는 Outlook 표준 시간대 도구를 실행 하려면이 절차를 수행 하는 테이블을 사용 하 여.

2.  컴퓨터를 업데이트해야 하는 사용자에게 해당 도구에 대한 링크를 제공하는 메시지를 보냅니다.

다음 표와 사용자가 [Exchange 일정 업데이트 도구](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879) 나 [Microsoft Office Outlook 용 표준 시간대 데이터 업데이트 도구](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667)을 실행 해야 합니다. 조직의 서버를 실행 하는 버전을 확인 하 고 사용자가 실행 되는 클라이언트 프로그램을 결정 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>클라이언트 버전</strong></p></td>
<td> </td>
</tr>
<tr class="even">
<td><p><strong>조직 버전</strong></p></td>
<td><p><strong>Outlook 2003 또는 Outlook 2007</strong></p></td>
<td><p><strong>Outlook 2010</strong></p></td>
<td><p><strong>Outlook 2013</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2003 온-프레미스</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Exchange 일정 도구</a> 또는</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">표준 시간대 데이터 업데이트 Microsoft Office Outlook 용 도구</a></p></td>
<td><p>필요한 작업이 없습니다.</p></td>
<td><p>필요한 작업이 없습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2007 온-프레미스</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Exchange 일정 도구</a> 또는</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">표준 시간대 데이터 업데이트 Microsoft Office Outlook 용 도구</a></p></td>
<td><p>필요한 작업이 없습니다.</p></td>
<td><p>필요한 작업이 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2010 온-프레미스</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Exchange 일정 도구</a> 나</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">표준 시간대 데이터 업데이트 Microsoft Office Outlook 용 도구</a></p></td>
<td><p>필요한 작업이 없습니다.</p></td>
<td><p>필요한 작업이 없습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>온-프레미스 Exchange 2013</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">표준 시간대 데이터 업데이트 Microsoft Office Outlook 용 도구</a></p></td>
<td><p>필요한 작업이 없습니다.</p></td>
<td><p>필요한 작업이 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>BPOS-S(Exchange 2007)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">표준 시간대 데이터 업데이트 Microsoft Office Outlook 용 도구</a></p></td>
<td><p>필요한 작업이 없습니다.</p></td>
<td><p>필요한 작업이 없습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>BPOS-D(Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">표준 시간대 데이터 업데이트 Microsoft Office Outlook 용 도구</a></p></td>
<td><p>필요한 작업이 없습니다.</p></td>
<td><p>필요한 작업이 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Office 365(Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">표준 시간대 데이터 업데이트 도구 Microsoft Office Outlook 용</a> (Outlook 2003과 지원 되지 않음)</p></td>
<td><p>필요한 작업이 없습니다.</p></td>
<td><p>필요한 작업이 없습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 (Exchange 2013)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">표준 시간대 데이터 업데이트 도구 Microsoft Office Outlook 용</a> (Outlook 2003과 지원 되지 않음)</p></td>
<td><p>필요한 작업이 없습니다.</p></td>
<td><p>필요한 작업이 없습니다.</p></td>
</tr>
<tr class="odd">
<td> </td>
<td> </td>
<td> </td>
<td> </td>
</tr>
</tbody>
</table>

