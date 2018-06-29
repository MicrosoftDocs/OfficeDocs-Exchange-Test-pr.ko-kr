---
title: '자동 검사-Office 배포와 내 문제를 식별 하는 데 도움이: Exchange 2013 Help'
TOCTitle: 자동 검사-Office 배포와 내 문제를 식별 하는 데 도움이
ms:assetid: 77d4587c-7fd5-4231-931e-3d6608e622f4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn793978(v=EXCHG.150)
ms:contentKeyID: 62633032
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 자동 검사-Office 배포와 내 문제를 식별 하는 데 도움이

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

이 페이지에 check(s)는 가장 일반적인 구성 문제 중 일부를 식별 하는 데 도움이 됩니다. 구성 및 환경을 업데이트 하는 도움말의 유효성을 검사 하려면 아래 자동 check(s)를 사용할 수 있습니다.

Office 365 사용자 계정을 이미 있으면 **로그인** 을 선택 합니다. Azure ID 계정이 필요 하지 않습니다. 수 메시지가 사용자 계정에 대 한 다시 검사를 실행 하는 경우. 그럴 경우에 사용자 계정이 username@youroffice365login.domain와 암호의 형식에서입니다.

## 필수 구성 요소

Azure Active Directory 로그인 도우미 및 설치 Windows PowerShell용 Azure Active Directory 모듈 있는지를 검사 합니다.

두 버전에는 Azure Active Directory 로그인 도우미: [32 비트](https://go.microsoft.com/fwlink/?linkid=286261) 및 [64 비트](https://go.microsoft.com/fwlink/?linkid=286262)합니다.

두 버전에는 Windows PowerShell용 Azure Active Directory 모듈: [32 비트](https://go.microsoft.com/fwlink/?linkid=286258) 및 [64 비트](https://go.microsoft.com/fwlink/?linkid=286259)합니다.

## 하이브리드 마법사 검사


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
<td><p>클라이언트</p></td>
<td><p>내 도메인 컴퓨터를 준비가 되 면 Office 있는지 없으므로.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834911">이 검사를 실행 합니다.</a></p></td>
</tr>
</tbody>
</table>

