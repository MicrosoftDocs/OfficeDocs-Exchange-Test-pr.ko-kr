---
title: '셸에서 RollAlternateserviceAccountCredential.ps1 스크립트를 사용 하 여: Exchange 2013 Help'
TOCTitle: 셸에서 RollAlternateserviceAccountCredential.ps1 스크립트를 사용 하 여
ms:assetid: 6ac55aae-472a-4ed6-83df-2d0e7b48e05c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff808311(v=EXCHG.150)
ms:contentKeyID: 63915415
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 셸에서 RollAlternateserviceAccountCredential.ps1 스크립트를 사용 하 여

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

대체 서비스 계정 자격 증명 (ASA 자격 증명) Exchange Server 2013 fto 업데이트에 RollAlternateServiceAccountPassword.ps1 스크립트를 사용할 수 있으며 지정 된 클라이언트 액세스 서버에 대 한 업데이트를 배포할 수 있습니다.


> [!NOTE]
> Exchange 관리 셸 스크립트를 자동으로 로드 하지 않습니다. 앞에 있는 모든 스크립트 해야하는 "<STRONG>. \</STRONG> " 등 RollAlternateServiceAccountPassword.ps1 스크립트를 실행 하려면 <CODE>.\RollAlternateServiceAccountPassword.ps1</CODE>를 입력 합니다.




> [!NOTE]
> 이 스크립트는 영어로 제공 됩니다.



사용 하 고 스크립트를 작성 하는 방법에 대 한 자세한 내용은 [Exchange 관리 셸을 사용하여 스크립팅](https://technet.microsoft.com/ko-kr/library/bb123798\(v=exchg.150\))을 참조 하십시오.

## 구문

```powershell
RollAlternateServiceAccountPassword.ps1 -Scope <Object> -Identity <Object> -Source <Object> -
```

## 자세한 정보

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. 클라이언트 액세스 권한 항목의 "클라이언트 액세스 보안" 항목.

## 대체 서비스 계정 자격 증명 스크립트의 기술 세부 정보

이 스크립트 설치 및 유지 관리 ASA 자격 증명을 용이 하 게 합니다. ASA 자격 증명을 만들어 적절 한 서비스 사용자 이름을 설정 했을 때 후 자격 증명을 대상으로 지정 된 모든 클라이언트 액세스 서버를 배포 하는 스크립트를 사용할 수 있습니다.

스크립트를 사용 하려면 ASA 자격 증명으로 사용할는 자격 증명 및 대상으로 할 수 있는 서버를 식별 해야 합니다.

## 서버 범위

스크립트를 대상으로 포리스트에 있는 모든 클라이언트 액세스 서버, 특정 클라이언트 액세스 서버 배열 또는 특정 서버의 모든 구성원을 선택할 수 있습니다. 사용 가능한 매개 변수는 *ToEntireForest*, *ToArraryMembers*및 *ToSpecificServers*합니다. 특정 서버 또는 *Identity* 매개 변수는 특정 서버 배열의 구성원에 스크립트 대상 서버 또는 서버 배열 이름을 지정할 필요가 하려는 경우 대상으로 합니다.

## 자격 증명 원본

이 스크립트는 기존 서버에서 대체 서비스 계정 암호를 복사할 수 있습니다. 또는 사용 하 고 계정에 대 한 새 암호를 생성 하는 스크립트를 사용 하려는 계정을 지정할 수 있습니다. 사용 가능한 매개 변수에 *GenerateNewPasswordFor* 및 *CopyFrom*합니다. *GenerateNewPasswordFor* 매개 변수는 다음과 같은 형식에서 계정 문자열을 지정 하는 필요: 도메인 \\ 계정 이름입니다. 컴퓨터 계정을 사용 하는 경우 해야 "$"를 추가할 계정 이름, 예: CONTOSO\\ClientServerAcct $의 끝에 있습니다. *CopyFrom* 매개 변수는 기존 클라이언트 액세스 서버의 이름을 자격 증명 원본 변수로 사용 합니다.

## 자격 증명에 대 한 새 암호를 생성 (영문)

암호는 스크립트에 의해 만들어집니다. 없음 사용자 입력이 필요 합니다. 스크립트를 모든 대상 컴퓨터의 암호를 배포 하려고 하 고 새로 생성 된 암호를 통한 Active Directory 계정 자격 증명을 업데이트 하려면 시도 됩니다.

새로 생성 된 암호 73 자 이며 표준 강력한 암호 요구 사항을 충족 됩니다. 암호 요구 사항을 다를 경우 암호를 수동으로 설정 하 고 다음 대상 서버로 복사 해야할 수 있습니다.

서비스 중단을 방지 하기 위해 스크립트 각 클라이언트 액세스 서버를 검사 하 고 새 암호를 추가 하는 것 외에도 현재 암호를 유지 관리 합니다. 스크립트를 실행 한 후 공유 ASA 자격 증명에서 2 암호 중 하나를 사용할 수 있게 됩니다.: 현재 암호에 저장 된 Active Directory 또는 Active Directory 에서 아직 설정 하지 않은 새 암호입니다.

만료 된 암호와 같은 유효한 더이상 모든 암호는 대상 서버에서 제거 됩니다. Active Directory 에 암호를 변경할 수 없는 경우 아마도 암호 만료 되었기 때문에 스크립트는 시도 암호 다시 설정 하는 합니다. Active Directory 컴퓨터 계정 암호 또는 컴퓨터 계정 또는 사용자 계정에 대체 서비스 계정 인지에 따라 사용자 계정 암호를 다시 설정 하는 권한을 갖도록 스크립트를 실행 하는 계정이 필요 합니다.

암호를 모든 대상 클라이언트 액세스 서버에 대 한 성공적으로 변경 되지 않으면 Active Directory 암호가 업데이트 인증 오류가 발생할 수 있습니다. 스크립트를 무인 모드로 실행 하는 경우에 모든 대상 클라이언트 액세스 서버 성공적으로 업데이트 된 경우가 아니면 새 암호로 Active Directory 암호를 업데이트 되지 않습니다 것입니다. 스크립트를 유인된 모드에서 실행 하는 경우 Active Directory 에서 암호를 업데이트할 것인지 여부를 묻는 메시지가 나타납니다.

## 암호 유지 관리를 자동화 하는 예약 된 작업 만들기 (영문)

지속적으로 암호를 유지 하기 위해 예약 된 작업을 만들려면 스크립트, 원하는 경우 *CreateScheduledTask* 매개 변수를 사용 합니다. 이 매개 변수는 만들려는 작업의 이름에 대 한 문자열이 필요 합니다.


> [!NOTE]
> 스크립트를 실행 하 고 제대로 작동 하는지 유인된 모드에서 무인된 예약 된 작업을 만들기 전에 확인 합니다.



스크립트는 스크립트 위치한 폴더에.cmd 파일을 만듭니다. 그런 다음 3 주마다 해당.cmd 파일을 실행 하는 작업을 만듭니다. 같은 예약 된 작업을 수정 하려면, 더 많이 또는 적게 빈도로 실행 되도록 설정 하려면 Windows 작업 스케줄러를 사용할 수 있습니다. 기본적으로 작업에서 현재 로그온 한 사용자로 실행 됩니다. 또한이 스크립트는 사용자가 컴퓨터에 로그온 하는 경우에 실행 됩니다. 사용자의 로그온 여부를 실행 하도록 예약된 된 작업을 수정 하는 것이 좋습니다. 해당 계정에서 Active Directory 권한이 Exchange 엔터프라이즈 관리자 역할와 암호를 다시 설정 하는 경우 다른 계정으로 실행을 선택할 수 있습니다. 예약된 된 작업을 만들 때는 스크립트 무인된 모드에서 자동으로 실행 됩니다.

## 스크립트의 범위를 벗어났습니다 작업

스크립트는 ASA 자격 증명의 Spn을 관리 또는 대체 서비스 계정 하는 서버에서 제거할 수 되지 않습니다. 대체 서비스 계정을 하는 서버에서 제거 하려면 [부하 분산 된 클라이언트 액세스 서버에 대 한 Kerberos 인증 구성](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)에서 [해제를 설정 하는 Kerberos 인증](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md) 섹션을 참조 하십시오.

## 스크립트 문제해결

스크립트를 실행 하 고 제대로 작동 하는지 유인된 모드에서 무인된 예약 된 작업을 만들기 전에 확인 하는 것이 좋습니다. 정보 문제를 해결 하는 것에 대 한 [RollAlternateServiceAccountCredential.ps1 스크립트 문제해결](troubleshooting-the-rollalternateserviceaccountcredential-ps1-script-exchange-2013-help.md)를 참조 하십시오.

## 스크립트를 유효성 검사

스크립트를 실행 하면 출력-verbose 플래그를 사용 하 여 대화형으로 어떤 스크립트 작업이 성공한 나타내야 합니다. 클라이언트 액세스 서버가 업데이트 되었는지, 확인을 위해 ASA 자격 증명에 마지막으로 수정한 시간 스탬프를 확인할 수 있습니다. 다음 예제에서는 클라이언트 액세스 서버 목록을 오류가 발생 하 고 마지막으로 대체 서비스 계정 업데이트 되었습니다.

```powershell
Get-ClientAccessServer -IncludeAlternateServiceAccountCredentialstatus |Fl Name, AlternateServiceAccountConfiguration
```

스크립트 실행 되는 컴퓨터에서 이벤트 로그를 검토할 수 있습니다. 스크립트에 대 한 이벤트 로그 항목 응용 프로그램 이벤트 로그에는 하며 원본 *MSExchange Management Application*에서입니다. 다음 표에 각 로깅되는 이벤트와 이벤트 무엇을 의미 합니다.

### 이벤트 Id 및 해당 설명을 스크립트합니다

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>이벤트</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>14001</p></td>
<td><p>시작</p></td>
</tr>
<tr class="even">
<td><p>14002</p></td>
<td><p>성공 (정보)</p></td>
</tr>
<tr class="odd">
<td><p>14003</p></td>
<td><p>성공 하지만와 같은 경고가 발생 합니다.</p>
<p>스크립트 일부 문제가 발생 한 했지만, 극복 하기 위해 수 또는 필요한 되지 않은 사용자 입력 확인 합니다. 스크립트를 대화형 모드에서 실행 하는 경우 추가로 경고 세부 정보에 대 한 스크립트 출력을 읽습니다.</p></td>
</tr>
<tr class="even">
<td><p>14004</p></td>
<td><p>실패</p></td>
</tr>
</tbody>
</table>


예약 된 작업으로이 스크립트를 실행 하는 경우 해당 결과 **RollAlternateServiceAccountPassword** 라는 하위 폴더에 Exchange 서버 **로깅** 폴더에 기록 됩니다.

작업이 성공적으로 실행 되었는지 확인 하는 로그를 사용할 수 있습니다.

## 매개 변수


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>필수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ToEntireForest</em></p></td>
<td><p>옵션</p></td>
<td><p><em>ToEntireForest</em> 매개 변수는 포리스트에 있는 모든 클라이언트 액세스 서버에 스크립트를 대상으로 합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>ToArrayMembers</em></p></td>
<td><p>옵션</p></td>
<td><p><em>ToArrayMembers</em> 매개 변수는 특정 클라이언트 액세스 서버 배열의 모든 구성원에 게 스크립트를 대상으로 합니다.</p>

> [!NOTE]
> <EM>ToArrayMembers</EM> 매개 변수 또는 <EM>ToSpecificServers</EM> 매개 변수를 사용 하는 경우 서버 이름 또는 <EM>Identity</EM> 매개 변수를 사용 하 여 서버 배열 이름을 지정 해야 합니다.


</td>
</tr>
<tr class="odd">
<td><p><em>ToSpecificServers</em></p></td>
<td><p>옵션</p></td>
<td><p><em>ToSpecificServers</em> 매개 변수는 특정 서버에 스크립트를 대상으로 합니다.</p>

> [!NOTE]
> <EM>ToArrayMembers</EM> 매개 변수 또는 <EM>ToSpecificServers</EM> 매개 변수를 사용 하는 경우 서버 이름 또는 <EM>Identity</EM> 매개 변수를 사용 하 여 서버 배열 이름을 지정 해야 합니다.


</td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>필수</p></td>
<td><p><em>Identity</em> 매개 변수는 클라이언트 액세스 서버 배열의 이름 또는 대상으로 하는 특정 서버 이름을 지정 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>GenerateNewPasswordFor&lt;String&gt;</em></p></td>
<td><p>옵션</p></td>
<td><p><em>GenerateNewPasswordFor</em> 매개 변수는이 스크립트는 ASA에 대 한 새 암호를 생성 해야 함을 지정 합니다. 문자열 값의 형식은 ASA 계정으로 필요가: 도메인 \ 계정 이름입니다. 컴퓨터 계정을 사용 하는 경우 계정 이름 끝날 때 $ 문자를 추가 해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>CopyFrom&lt;String&gt;</em></p></td>
<td><p>옵션</p></td>
<td><p><em>CopyFrom</em> 매개 변수는 자격 증명이 다른 클라이언트 액세스 서버에서 복사 되는 것을 지정 합니다. 지정 된 문자열 값은 클라이언트 액세스 서버의 이름입니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>Mode</em></p></td>
<td><p>옵션</p></td>
<td><p><em>Mode</em> 스위치를 사용 하는 스크립트 유인 또는 무인 모드로 실행 되는지 여부를 지정 합니다. 무인 설치 모드 사용자 입력에 대 한 메시지를 표시 하지 하 고 자동으로 필요한 경우 보다 신중 옵션을 선택 합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>CreateScheduledTask&lt;String&gt;</em></p></td>
<td><p>옵션</p></td>
<td><p><em>CreateScheduledTask</em> 매개 변수는 ASA 자격 증명 업데이트를 수행 하려면 예약 된 작업을 만들려면 스크립트에 지시 합니다. 문자열 값은 작성 되는 예약 된 작업의 이름입니다.</p>

> [!NOTE]
> 이 스크립트는 스크립트 위치한 폴더에.cmd 파일을 만듭니다. 예약 된 작업.cmd 파일 3 주마다 한 번 실행 됩니다. Windows 작업의 빈도 변경 하려면 작업 스케줄러에서 직접 작업을 편집할 수 있습니다.


</td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>옵션</p></td>
<td><p><em>WhatIf</em> 스위치는 명령이 개체에 대해 수행하게 되는 작업을 시뮬레이션하도록 지시합니다. <em>WhatIf</em> 스위치를 사용하면 사용자는 변경 사항을 적용하지 않고도 어떠한 사항이 변경되는지 확인할 수 있습니다. <em>WhatIf</em> 스위치를 사용하여 값을 지정할 필요가 없습니다.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>옵션</p></td>
<td><p><em>Confirm</em> 스위치는 명령이 처리를 일시 중지하도록 하고 처리를 계속하기 전에 명령이 어떤 작업을 수행하는지 사용자가 확인하도록 합니다. <em>Confirm</em> 스위치를 사용하여 값을 지정할 필요가 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>Verbose</em></p></td>
<td><p>옵션</p></td>
<td><p><em>Verbose</em> 매개 변수는 스크립트의 작업에 대 한 추가 정보는 로그 파일에 기록 되도록 자세한 로깅을 수행 하려면 스크립트에 지시 합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>Debug</em></p></td>
<td><p>선택</p></td>
<td><p><em>Debug</em> 매개 변수는 디버깅 모드에서 실행 하려면 스크립트에 지시 합니다. 스크립트 오류가 발생 하는 이유를 확인 하려면이 매개 변수를 사용 해야 합니다.</p></td>
</tr>
</tbody>
</table>


## 예제

## 예 1

이 예제에서는 스크립트를 사용 하 여를 처음 설치에 대 한 포리스트에 있는 모든 클라이언트 액세스 서버에는 자격 증명을 게시 합니다.

```powershell
.\RollAlternateserviceAccountPassword.ps1 -ToEntireForest -GenerateNewPasswordFor "Contoso\ComputerAccount$" -Verbose
```

## 예 2

사용자 계정 ASA 자격 증명에 대 한 새 암호를 생성 하 고 일치 하는 이름이 클라이언트 액세스 서버 배열의 모든 구성원에 게 암호를 배포 하는이 예제 \* 사서함 \*.

```powershell
.\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers *mailbox* -GenerateNewPasswordFor "Contoso\UserAccount" -Verbose
```

## 예 3

이 예제에서는 "Exchange RollAsa" 라는 달 한 번 자동화 된 암호 roll 예약 된 작업을 예약 합니다. 새, 스크립트에서 생성 된 암호와 전체 포리스트에 있는 모든 클라이언트 액세스 서버에 대 한 ASA 자격 증명을 업데이트 됩니다. 예약 된 작업 만들어지지만 스크립트는 실행 되지 않습니다. 예약 된 작업을 실행 하는 경우 무인 설치 모드에서 스크립트를 실행 합니다.

```powershell
.\RollAlternateServiceAccountPassword.ps1 -CreateScheduledTask "Exchange-RollAsa" -ToEntireForest -GenerateNewPasswordFor 'contoso\computerAccount$'
```

## 예 4

이 예제에서는 c a s 01 이라는 클라이언트 액세스 서버 배열에 있는 모든 클라이언트 액세스 서버에 대 한 ASA 자격 증명을 업데이트 합니다. Contoso 도메인에서 Active Directory 컴퓨터 계정 ServiceAc1에서에서 자격 증명을 가져옵니다.

```powershell
.\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers "CAS01" -GenerateNewPasswordFor "CONTOSO\ServiceAc1$" 
```

## 예 5

이 예제 스크립트를 사용 하 여 새 컴퓨터 또는 되 고 다시 배치 서비스에 서버 배열의 크기를 늘리면 중인 또는 유지 관리 이후 배열 구성원을 다시 소개 하는 컴퓨터에 ASA를 배포 하는 방법을 보여줍니다.

클라이언트 액세스 서버에 트래픽을 수신 하기 전에 ASA 자격 증명을 업데이트 해야 합니다. 이미 올바르게 구성 된 모든 클라이언트 액세스 서버에서 공유 ASA 자격 증명을 복사 합니다. 예, 하는 경우 서버 A 현재 작업 ASA 자격 증명을가지고 및 서버 B 방금 추가한 배열에 하는데 사용할 수는 스크립트 (암호를 포함 하 여) 자격 증명을 복사 서버 A에서에서 서버 b 서버 B를 눌렀는지 하는 경우에 유용 하거나 암호를 마지막으로 출시 때 배열의 구성원 아직 합니다.

```powershell
.\RollAlternateServiceAccountPassword.ps1 -CopyFrom ServerA -ToSpecificServers ServerB -Verbose
```

