---
title: 'AD LDS 구성 수정: Exchange 2013 Help'
TOCTitle: AD LDS 구성 수정
ms:assetid: 381f582c-15ec-43bc-b674-5399fad72c97
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997269(v=EXCHG.150)
ms:contentKeyID: 61183420
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# AD LDS 구성 수정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

Edge 전송 서버를 Exchange 조직에 구독하기 전에 $env:ExchangeInstallPath\\Scripts에 있는 **ConfigureAdam.ps1** 스크립트를 사용하여 Edge 전송 서버의 기본 AD LDS(Active Directory Lightweight Directory Services) 구성을 수정할 수 있습니다.


> [!IMPORTANT]
> <STRONG>ConfigureAdam.ps1</STRONG> 스크립트는 <STRONG>dsdbutil</STRONG> 명령을 호출하여 AD&nbsp;LDS에 대한 레지스트리 설정을 변경합니다. <STRONG>dsdbutil</STRONG> 숙련된 관리자만 사용해야 하는 AD LDS 관리 도구입니다. AD LDS 구성을 변경하려면 <STRONG>ConfigureAdam.ps1</STRONG>을 사용하는 것이 좋습니다.



다음 표에는 **ConfigureAdam.ps1** 스크립트에 사용할 수 있는 매개 변수가 나와 있습니다. 이러한 매개 변수를 하나 또는 모두 사용하거나 원하는 대로 조합하여 AD LDS를 수정할 수 있습니다.

### ConfigureAdam.ps1 스크립트에 사용할 수 있는 매개 변수

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Ldapport</em></p></td>
<td><p>LDAP 통신에 사용되는 포트를 수정합니다. 기본적으로 Edge 전송 서버는 비표준 포트 50389를 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>Sslport</em></p></td>
<td><p>보안 LDAP 통신에 사용되는 포트를 수정합니다. 기본적으로 Edge 전송 서버는 비표준 포트 50636을 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogPath</em></p></td>
<td><p>로그 파일 위치를 수정합니다. Edge 전송 서버는 기본적으로 %ExchangeInstallPath%Transport Roles\Data\adam 경로에 로그 파일을 만듭니다.</p></td>
</tr>
<tr class="even">
<td><p><em>DataPath</em></p></td>
<td><p>디렉터리 데이터베이스 파일의 위치를 수정합니다. Edge 전송 서버는 기본적으로 디렉터리 데이터베이스를 %ExchangeInstallPath%Transport Roles\Data\adam 경로에 저장합니다.</p></td>
</tr>
</tbody>
</table>


## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "Edge 전송 서버" 섹션

  - Edge 전송 서버의 AD LDS 구성을 수정해야 하는 경우 Edge 전송 서버를 Exchange 조직에 구독하기 전에 구성을 수정합니다. 구독된 Edge 전송 서버의 AD LDS 구성을 수정하는 경우에는 해당 Edge 전송 서버를 Exchange 조직에 다시 구독해야 합니다.

  - 레지스트리 설정을 수정하려면 항상 스크립트를 사용합니다. AD LDS 구성에 대해 레지스트리를 수동으로 변경하면 AD LDS 인스턴스를 사용하지 못하게 될 수 있습니다.

  - AD LDS에서 사용하는 LDAP 포트나 SSL 포트를 수정해야 하는 경우 먼저 선택한 포트를 다른 응용 프로그램에서 사용하고 있지 않은지 확인합니다. **netstat** 명령을 사용하여 Edge 전송 서버에서 사용되는 포트를 확인할 수 있습니다.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## Edge 전송 서버에서 AD LDS 구성 수정

이 예에서는 AD LDS에서 사용하는 LDAP 포트를 5000으로 변경합니다. 앰퍼샌드(&)는 명령 구문의 일부분입니다.

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000

이 예에서는 AD LDS 구성을 다음과 같이 변경합니다. 앰퍼샌드(&)는 명령 구문의 일부분입니다. 각 매개 변수와 해당 값 사이에는 콜론(:)이 사용됩니다.

  - LDAP 포트를 5000으로 변경합니다.

  - SSL 포트를 500으로 변경합니다.

  - 로그 경로를 D:\\Exchange Server\\Data\\ADLDS로 변경합니다.

  - 데이터 경로를 D:\\Exchange Server\\Data\\ADLDS로 변경합니다.

<!-- end list -->

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000 -SslPort:5001 -LogPath:"D:\Exchange Server\Data\ADLDS" -DataPath:"D:\Exchange Server\Data\ADLDS"

