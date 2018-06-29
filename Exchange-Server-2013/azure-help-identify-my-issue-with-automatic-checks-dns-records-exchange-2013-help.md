---
title: 'Azure: 자동 검사-DNS 레코드와 내 문제를 식별 하는데 도움이: Exchange 2013 Help'
TOCTitle: 'Azure: 자동 검사-DNS 레코드와 내 문제를 식별 하는데 도움이'
ms:assetid: 1ef42cde-4df4-401a-b8f2-494630996ca8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn793619(v=EXCHG.150)
ms:contentKeyID: 62630001
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Azure: 자동 검사-DNS 레코드와 내 문제를 식별 하는데 도움이

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

가장 일반적인 구성 설치 문제 중 하나를 잘못 구성 DNS 레코드. 구성 및 환경을 업데이트 하는 도움말의 유효성을 검사 하려면 아래에 나열 된 자동 검사를 사용할 수 있습니다.

Office 365 사용자 계정을 이미 있으면 로그인을 선택 합니다. Azure ID 계정이 필요 하지 않습니다. 수 메시지가 사용자 계정에 대 한 다시 검사를 실행 하는 경우. 그럴 경우에 사용자 계정이 username@youroffice365login.domain와 암호의 형식에서입니다.

## 필수 구성 요소

Azure Active Directory 로그인 도우미 및 설치 Windows PowerShell용 Azure Active Directory 모듈 있는지를 검사 합니다.

두 버전에는 Azure Active Directory 로그인 도우미: [32 비트](https://go.microsoft.com/fwlink/?linkid=286261) 및 [64 비트](https://go.microsoft.com/fwlink/?linkid=286262)합니다.

두 버전에는 Windows PowerShell용 Azure Active Directory 모듈: [32 비트](https://go.microsoft.com/fwlink/?linkid=286258) 및 [64 비트](https://go.microsoft.com/fwlink/?linkid=286259)합니다.

## DNS 레코드 검사


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
<td><p>도메인</p></td>
<td><p>내 사용자 지정 도메인 (예: contoso.com) Office 365를 사용 하 여 구성에 적합 하지 않습니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>도메인</p></td>
<td><p>내 사용자 지정 도메인 (예: contoso.com) (I CNAME 레코드를 사용 함)는 Office 365를 사용 하 여 구성에 적합 하지 않습니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p>도메인</p></td>
<td><p>내 사용자 지정 도메인 (예: contoso.com) (I TXT 레코드를 사용 함)는 Office 365를 사용 하 여 구성에 적합 하지 않습니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>인스턴트 메시징</p></td>
<td><p>내 사용자는 문제가 작동 하도록 자신의 Lync 클라이언트를 시작 합니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834901">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p>인스턴트 메시징</p></td>
<td><p>사용자가 문제가 있는 다른 조직과 작동 하도록 자신의 Lync 클라이언트를 시작 합니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834902">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>메일</p></td>
<td><p>Office 365와 함께 자동으로 구성 하는 Outlook 받았을 수 없음</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834897">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p>메일</p></td>
<td><p>내 전자 메일을 Office 365로 라우팅 되어야 하는 것</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834898">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>메일</p></td>
<td><p>내 조직에 많은 스팸 꽉 합니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834903">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p>메일</p></td>
<td><p>Exchange 하이브리드 기능을 작동 하지 않습니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834904">이 검사를 실행 합니다.</a></p></td>
</tr>
</tbody>
</table>

