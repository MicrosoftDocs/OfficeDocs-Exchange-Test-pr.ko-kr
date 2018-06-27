---
title: '자동 검사-Active Directory 내 문제를 식별 하는 데 도움이: Exchange 2013 Help'
TOCTitle: 자동 검사-Active Directory 내 문제를 식별 하는 데 도움이
ms:assetid: af08e7a1-775a-4e56-a6fe-4ffc10460514
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn793979(v=EXCHG.150)
ms:contentKeyID: 62633034
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 자동 검사-Active Directory 내 문제를 식별 하는 데 도움이

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

이 페이지에 check(s)는 가장 일반적인 구성 문제 중 일부를 식별 하는 데 도움이 됩니다. 구성 및 환경을 업데이트 하는 도움말의 유효성을 검사 하려면 아래 자동 check(s)를 사용할 수 있습니다.

Office 365 사용자 계정을 이미 있으면 **로그인** 을 선택 합니다. Azure ID 계정이 필요 하지 않습니다. 수 메시지가 사용자 계정에 대 한 다시 검사를 실행 하는 경우. 그럴 경우에 사용자 계정이 username@youroffice365login.domain와 암호의 형식에서입니다.

## 필수 구성 요소

Azure Active Directory 로그인 도우미 및 설치 Windows PowerShell용 Azure Active Directory 모듈 있는지를 검사 합니다.

두 버전에는 Azure Active Directory 로그인 도우미: [32 비트](https://go.microsoft.com/fwlink/?linkid=286261) 및 [64 비트](https://go.microsoft.com/fwlink/?linkid=286262)합니다.

두 버전에는 Windows PowerShell용 Azure Active Directory 모듈: [32 비트](https://go.microsoft.com/fwlink/?linkid=286258) 및 [64 비트](https://go.microsoft.com/fwlink/?linkid=286259)합니다.

## Active Directory 검사


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
<td><p>Exchange 버전</p></td>
<td><p>확실 하지가 설치 된 Exchange Server 온-프레미스 또는 어떤 경우 해야 합니까 버전입니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834879">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>자격 증명</p></td>
<td><p>Office 365로 이동 하려면 오른쪽 자격 증명을 갖고 I 있는지 없으므로</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834880">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p>3 번째 타사 도구</p></td>
<td><p>확실 하지 어떤 타사 통합/응용 프로그램 내 메시징 환경에 설치 합니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834907">이 검사를 실행 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>공유 사서함</p></td>
<td><p>다른 사용자 (대리인)에 대 한 사서함을 관리 되는 확인 하고자 합니다.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834917">이 검사를 실행 합니다.</a></p></td>
</tr>
</tbody>
</table>

