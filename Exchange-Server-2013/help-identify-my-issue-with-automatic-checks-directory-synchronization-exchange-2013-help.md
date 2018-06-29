---
title: '자동 검사-디렉터리 동기화와 내 문제를 식별 하는 데 도움이: Exchange 2013 Help'
TOCTitle: 자동 검사-디렉터리 동기화와 내 문제를 식별 하는 데 도움이
ms:assetid: e6ea900a-c382-444c-a8ce-54d392bfeca3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn793977(v=EXCHG.150)
ms:contentKeyID: 62633038
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 자동 검사-디렉터리 동기화와 내 문제를 식별 하는 데 도움이

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

구성 및 환경을 업데이트 하는 도움말의 유효성을 검사 하려면 아래 자동 검사를 사용할 수 있습니다.

Office 365 사용자 계정을 이미 있으면 로그인을 선택 합니다. Azure ID 계정이 필요 하지 않습니다. 수 메시지가 사용자 계정에 대 한 다시 검사를 실행 하는 경우. 그럴 경우에 사용자 계정이 username@youroffice365login.domain와 암호의 형식에서입니다.


> [!NOTE]
> Office 365 포털에서 동기화 서버 이벤트 로그 또는 비정상 디렉터리 동기화 알림 전자 메일이 Microsoft 온라인 서비스에서의 오류를 동기화 경고 메시지를 수신 하는 경우 발생할 수 있는 일종의 디렉터리 동기화 문제입니다. <A href="https://aka.ms/dsup">디렉터리 동기화 문제 해결사</A> 은 일반적인 유형의 동기화 오류를 식별 하 고 규정 발견 된 문제점에 대 한 대상으로 지정 된 솔루션을 설계 하는 웹 기반 진단 도구입니다. 디렉터리 동기화 문제 해결사 디렉터리 동기화 서버에서 실행 되어야 합니다.



## 필수 구성 요소

Azure Active Directory 로그인 도우미 및 설치 Windows PowerShell용 Azure Active Directory 모듈 있는지를 검사 합니다.

두 버전에는 Azure Active Directory 로그인 도우미: [32 비트](https://go.microsoft.com/fwlink/?linkid=286261) 및 [64 비트](https://go.microsoft.com/fwlink/?linkid=286262)합니다.

두 버전에는 Windows PowerShell용 Azure Active Directory 모듈: [32 비트](https://go.microsoft.com/fwlink/?linkid=286258) 및 [64 비트](https://go.microsoft.com/fwlink/?linkid=286259)합니다.

## 디렉터리 동기화 확인


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>응용 프로그램</p></td>
<td><p>문제</p></td>
<td><p>검사</p></td>
</tr>
<tr class="even">
<td><p>디렉터리 동기화</p></td>
<td><p>디렉터리 동기화를 위한 요구 사항을 충족 내 Active Directory 사용자 계정을 모두 있는지 없으므로.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834884">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>디렉터리 동기화</p></td>
<td><p>Windows Server 2003 이상을 내 Active Directory 도메인 기능 수준 올바르게 설정 하는 경우 있는지 없으므로.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p>디렉터리 동기화</p></td>
<td><p>지난 3 시간에서 디렉터리 동기화 발생 한 경우 있는지 없으므로.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>디렉터리 동기화</p></td>
<td><p>Active Directory 내에서 디렉터리 동기화를 차단 하는 중복 된 사용자 특성에 있는지 없으므로.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834883">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p>디렉터리 동기화</p></td>
<td><p>Office 365에서 디렉터리 동기화를 사용 하는 경우 있는지 없으므로.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>디렉터리 동기화</p></td>
<td><p>Office 365 견적 제한을 배포할 수 있는지 없으므로.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834920">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p>디렉터리 동기화</p></td>
<td><p>Office 365를 배포 하 고 기본 디렉터리 동기화 설치 프로그램을 사용 하는 경우 있는지 없으므로 합니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>디렉터리 동기화</p></td>
<td><p>Active Directory를 사용 하는 디렉터리 동기화를 지원할 수 있는지 없으므로.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834886">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p>디렉터리 동기화</p></td>
<td><p>디렉터리 동기화에 대 한 요구를 충족 하는 모든 Active Directory 그룹 내 경우 있는지 없으므로.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834913">이 검사를 실행 합니다.</a></p></td>
</tr>
</tbody>
</table>

