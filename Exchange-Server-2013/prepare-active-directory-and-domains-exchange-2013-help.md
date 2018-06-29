---
title: 'Active Directory 및 도메인 준비: Exchange 2013 Help'
TOCTitle: Active Directory 및 도메인 준비
ms:assetid: f895e1ce-d766-4352-ac46-ec959c9954a9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125224(v=EXCHG.150)
ms:contentKeyID: 50484568
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory 및 도메인 준비

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013을 설치하기 전에 Active Directory 포리스트 및 해당 도메인을 준비해야 합니다. Exchange는 조직에서 사용자 사서함 및 Exchange 서버의 구성에 대한 정보를 저장할 수 있도록 Active Directory를 준비해야 합니다. Active Directory 포리스트나 도메인에 익숙하지 않은 경우 [Active Directory 도메인 서비스 개요](https://go.microsoft.com/fwlink/p/?linkid=399226)를 확인하세요.


> [!NOTE]
> 환경에서 Exchange를 처음 설치하는 경우이거나 이전 버전의 Exchange Server가 이미 실행되고 있으면 Exchange 2013용 Active Directory를 준비해야 합니다. SP(서비스 팩) 및 CU(누적 업데이트)에 의해 추가되는 것을 비롯하여 Exchange 2013에서 Active Directory에 추가하는 새 스키마 클래스 및 특성에 대한 자세한 내용은 <A href="exchange-2013-active-directory-schema-changes-exchange-2013-help.md">Exchange 2013 Active Directory 스키마 변경 사항</A>을 참조하세요.



Exchange에 대해 Active Directory를 준비하는 방법에는 몇 가지가 있습니다. 첫 번째 방법은 Exchange 2013 설치 마법사를 통해 자동으로 수행하는 것입니다. Active Directory 배포 규모가 크지 않으며 Active Directory를 관리하는 별도의 팀이 없으면 마법사를 사용하는 것이 좋습니다. 사용하는 계정은 Schema Admins 및 Enterprise Admins 보안 그룹 둘 다의 구성원이어야 합니다. 설치 마법사 사용 방법에 대한 자세한 내용은 [설치 마법사를 사용하여 Exchange 2013 설치](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)를 참조하세요.

Active Directory 배포 규모가 크거나 별도의 팀이 Active Directory를 관리하는 경우 이 항목이 도움이 될 것입니다. 이 항목의 단계에 따라 각 준비 단계 및 각 단계를 수행할 수 있는 작업자를 제어할 수 있습니다. 예를 들어 Exchange 관리자는 Active Directory 스키마를 확장하는 데 필요한 권한이 없을 수 있습니다.

시작하기 전에 알아야 할 내용

1\. Active Directory 스키마 확장

2\. Active Directory 준비

3\. Active Directory 도메인 준비

작동 여부는 어떻게 확인합니까?

Exchange에 대해 Active Directory를 준비하는 경우 진행되는 과정이 궁금하십니까? [Exchange 2013이 설치될 때 Active Directory에서 변경되는 내용](what-changes-in-active-directory-when-exchange-2013-is-installed-exchange-2013-help.md)를 참조하세요.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10-15분 이상(Active Directory 복제 시간 제외). 조직 규모 및 하위 도메인 수에 따라 다릅니다.

  - 이러한 단계를 수행하는 데 사용하는 컴퓨터는 [Exchange 2013 시스템 요구 사항](exchange-2013-system-requirements-exchange-2013-help.md)을 충족해야 합니다. 또한 Active Directory 포리스트는 [Exchange 2013 시스템 요구 사항](exchange-2013-system-requirements-exchange-2013-help.md)의 "네트워크 및 디렉터리 서비스" 섹션의 요구 사항을 충족해야 합니다.

  - 조직에 여러 Active Directory 도메인이 있는 경우 다음 작업이 권장됩니다.
    
      - 모든 도메인의 Active Directory 서버가 있는 Active Directory 사이트에서 아래 단계를 수행합니다.
    
      - 모든 도메인에서 쓰기 가능 글로벌 카탈로그 서버가 있는 Active Directory 사이트에 첫 번째 Exchange 서버를 설치합니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 1\. Active Directory 스키마 확장

Exchange 2013을 사용할 수 있게 조직을 준비하는 첫 번째 단계는 Active Directory 스키마를 확장하는 것입니다. Exchange에서는 Active Directory에 많은 정보를 저장하지만 이를 위해서는 먼저 클래스, 특성 및 기타 항목을 추가하고 업데이트해야 합니다. 스키마가 확장될 때 변경되는 결과를 확인하려면 [Exchange 2013 Active Directory 스키마 변경 사항](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)을 참조하세요.

스키마를 확장하기 전에 다음 사항에 유의해야 합니다.

  - 로그인할 때 사용하는 계정은 Schema Admins 및 Enterprise Admins 보안 그룹 둘 다의 구성원이어야 합니다.

  - 스키마를 확장하기 위해 명령을 실행하는 컴퓨터는 스키마 마스터와 동일한 Active Directory 도메인 및 사이트에 있어야 합니다.

  - *DomainController* 매개 변수를 사용하는 경우 스키마 마스터인 도메인 컨트롤러의 이름을 사용해야 합니다.

  - Exchange에 대해 스키마를 확장하는 유일한 방법은 이 항목의 단계 또는 Exchange 2013 설치 프로그램을 사용하는 것입니다. 스키마를 확장하는 다른 방법은 지원되지 않습니다.


> [!TIP]
> Active Directory 스키마를 관리하는 별도의 팀이 없으면 이 단계를 건너뛰고 Active Directory 준비로 바로 이동할 수 있습니다. 1단계에서 스키마가 확장되지 않으면 2단계의 명령으로 스키마를 확장합니다. 1단계를 건너뛰기로 결정한 경우에도 위의 유의 사항을 여전히 고려해야 합니다.



준비가 끝나면 다음을 수행하여 Active Directory 스키마를 확장합니다. 여러 개의 Active Directory 포리스트가 있는 경우 올바른 포리스트로 로그인해야 합니다.

1.  컴퓨터에서 Exchange 2013 설치 프로그램을 실행할 준비가 되었는지 확인합니다. 설치 프로그램을 실행하는 데 필요한 사항을 확인하려면 [Exchange 2013 필수 구성 요소](exchange-2013-prerequisites-exchange-2013-help.md)의 [Active Directory preparation](exchange-2013-prerequisites-exchange-2013-help.md) 섹션을 참조하세요.

2.  Windows 명령 프롬프트 창을 열고 Exchange 설치 파일을 다운로드한 위치로 이동합니다.

3.  다음 명령을 실행하여 스키마를 확장합니다.
    
        Setup.exe /PrepareSchema /IAcceptExchangeServerLicenseTerms

설치 프로그램이 스키마 확장을 끝내면 Active Directory가 모든 도메인 컨트롤러로 변경 내용을 복제하는 동안 기다려야 합니다. 복제가 어떻게 진행되는지 확인하려면 `repadmin` 도구를 사용할 수 있습니다. `Repadmin`은 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2의 Active Directory 도메인 서비스 도구 기능에 포함됩니다. 이 도구의 사용 방법에 대한 자세한 내용은 [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879)을 참조하세요.

## 2\. Active Directory 준비

Active Directory 스키마가 확장되었으므로 Exchange 2013을 위해 Active Directory의 다른 부분을 준비할 수 있습니다. 이 단계를 수행하는 동안 Exchange에서는 정보를 저장하는 데 사용할 컨테이너, 개체 및 기타 항목을 Active Directory에 만듭니다. 모든 Exchange 컨테이너, 개체, 특성 등의 컬렉션을 *Exchange 조직*이라고 합니다.

Exchange를 위해 Active Directory를 준비하기 전에 다음 사항에 유의해야 합니다.

  - 로그인할 때 사용하는 계정은 Enterprise Admins 보안 그룹의 구성원이어야 합니다. *PrepareAD* 명령을 사용하여 스키마를 확장하기 위해 1단계를 건너뛴 경우 사용하는 계정 또한 Schema Admins 보안 그룹의 구성원이어야 합니다.

  - 명령을 실행하는 컴퓨터는 스키마 마스터와 동일한 Active Directory 도메인 및 사이트에 있어야 합니다. 또한 TCP 포트 389에서 포리스트의 모든 도메인에 연결해야 합니다.

  - 이 단계를 수행하기 전에 Active Directory가 1단계에서 수행한 변경 내용을 모든 도메인 컨트롤러로 복제할 때까지 기다립니다.

아래 명령을 실행하여 Exchange에 대한 Active Directory를 준비하는 경우 Exchange 조직의 이름을 지정해야 합니다. 이 이름은 Exchange에서 내부적으로 사용되며 일반적으로 사용자에게는 표시되지 않습니다. Exchange를 설치하는 회사 이름이 조직 이름에 사용되는 경우도 종종 있습니다. 사용하는 이름은 Exchange의 기능에 영향을 주지 않으며 전자 메일 주소에 사용할 수 있는 항목을 결정합니다. 다음 조건에 따라 원하는 이름을 지정할 수 있습니다.

  - 대/소문자 A-Z를 사용할 수 있습니다.

  - 0에서 9 까지의 숫자를 사용할 수 있습니다.

  - 맨 처음이나 끝이 아니면 이름에 공백을 포함할 수 있습니다.

  - 이름에 하이픈 또는 대시를 사용할 수 있습니다.

  - 이름은 64자까지 가능하지만 비워 둘 수 없습니다.

  - 설정한 후에는 이름을 변경할 수 없습니다.

준비가 끝나면 다음을 수행하여 Exchange에 대한 Active Directory를 준비합니다. 조직 이름에 공백을 사용하려면 큰따옴표(")로 묶어야 합니다.

1.  Windows 명령 프롬프트 창을 열고 Exchange 설치 파일을 다운로드한 위치로 이동합니다.

2.  다음 명령을 실행합니다.
    
        Setup.exe /PrepareAD /OrganizationName:"<organization name>" /IAcceptExchangeServerLicenseTerms

설치 프로그램이 Exchange를 위한 Active Directory 준비를 끝내면 Active Directory가 모든 도메인 컨트롤러로 변경 내용을 복제하는 동안 기다려야 합니다. 복제가 어떻게 진행되는지 확인하려면 `repadmin` 도구를 사용할 수 있습니다. `repadmin`은 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2의 Active Directory 도메인 서비스 도구 기능에 포함됩니다. 이 도구의 사용 방법에 대한 자세한 내용은 [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879)을 참조하세요.

## 3\. Active Directory 도메인 준비

Exchange를 위해 Active Directory를 준비하는 최종 단계는 Exchange가 설치되거나 메일 사용 가능 사용자가 위치할 모든 Active Directory 도메인을 준비하는 것입니다. 이 단계를 수행하면 추가 컨테이너 및 보안 그룹이 만들어지고 Exchange에서 액세스할 수 있게 사용 권한이 설정됩니다.

Active Directory 포리스트에 여러 개의 도메인이 있으면 몇 가지 중에서 준비 방법을 선택할 수 있습니다. 수행하려는 작업에 해당하는 옵션을 선택합니다. 도메인이 하나뿐이면 2단계의 *PrepareAD* 명령으로 이미 도메인이 준비되었을 것이므로 이 단계를 건너뛰어도 됩니다.

## Active Directory 포리스트의 모든 도메인 준비

모든 Active Directory 도메인을 준비하려면 설치 프로그램을 실행할 때 *PrepareAllDomains* 매개 변수를 사용할 수 있습니다. 설치 프로그램은 Active Directory 포리스트의 모든 도메인을 Exchange에 맞게 준비합니다.

Active Directory 포리스트의 모든 도메인을 준비하기 전에 다음에 유의합니다.

  - 사용하는 계정은 Enterprise Admins 보안 그룹의 구성원이어야 합니다.

  - Active Directory가 2단계에서 수행한 변경 내용을 모든 도메인 컨트롤러로 복제할 때까지 기다립니다. 그렇지 않으면 도메인을 준비하려고 할 때 오류가 발생할 수 있습니다.

준비되면 다음을 수행하여 Active Directory 포리스트에서 Exchange를 위해 모든 도메인을 준비합니다.

1.  Windows 명령 프롬프트 창을 열고 Exchange 설치 파일을 다운로드한 위치로 이동합니다.

2.  다음 명령을 실행합니다.
    
        Setup.exe /PrepareAllDomains /IAcceptExchangeServerLicenseTerms

## 준비할 Active Directory 도메인 선택

준비할 Active Directory 도메인을 선택하려면 설치 프로그램을 실행할 때 *PrepareDomain* 매개 변수를 실행할 수 있습니다. *PrepareDomain* 매개 변수를 사용할 때 준비할 도메인의 FQDN(정규화된 도메인 이름)을 포함해야 합니다.

Active Directory 포리스트에서 모든 도메인을 준비하기 전에 다음에 유의합니다.

  - 사용하는 계정에는 도메인을 만든 시기에 따라 다른 사용 권한이 필요합니다.
    
      - **PrepareAD를 실행하기 전에 만든 도메인**   도메인을 위의 2단계에서 *PrepareAD* 명령을 실행하기 **전에** 만들었으면 사용하는 계정은 준비할 도메인에서 Domain Admins 그룹의 구성원이어야 합니다.
    
      - **PrepareAD를 실행한 후에 만든 도메인**   도메인을 위의 2단계에서 *PrepareAD* 명령을 실행한 **후에** 만들었으면 사용하는 계정은 준비할 도메인에서 Organization Management 역할 그룹의 구성원이면서 Domain Admins 그룹의 구성원이어야 합니다.

  - Active Directory가 2단계에서 수행한 변경 내용을 모든 도메인 컨트롤러로 복제할 때까지 기다립니다. 그렇지 않으면 도메인을 준비하려고 할 때 오류가 발생할 수 있습니다.

  - Exchange 서버가 설치될 모든 도메인을 준비해야 합니다. 메일 사용 가능 사용자를 포함할 도메인을 준비해야 합니다. 이러한 도메인에 Exchange 서버가 들어 있는지 여부는 상관 없습니다.

  - *PrepareAD* 명령이 실행된 도메인에서는 *PrepareDomain* 명령을 실행할 필요가 없습니다. *PrepareAD* 명령은 자동으로 해당 도메인을 준비합니다.

준비되면 다음을 수행하여 Active Directory 포리스트에서 Exchange를 위한 개별 도메인을 준비합니다.

1.  Windows 명령 프롬프트 창을 열고 Exchange 설치 파일을 다운로드한 위치로 이동합니다.

2.  다음 명령을 실행합니다. 준비할 도메인의 FQDN을 포함합니다. 명령을 실행할 도메인을 준비하려면 FQDN을 포함할 필요가 없습니다.
    
        Setup.exe /PrepareDomain:<FQDN of the domain you want to prepare> /IAcceptExchangeServerLicenseTerms

3.  Exchange 서버를 설치하려고 하거나 메일 사용 가능 사용자가 위치할 각 Active Directory 도메인에 대해 이러한 단계를 반복합니다.

## 작동 여부는 어떻게 확인합니까?

위의 모든 단계를 완료한 후에는 모든 작업이 원활하게 진행되었는지 확인할 수 있습니다. 이렇게 하려면 ADSI Edit(Active Directory Service Interfaces Editor)이라는 도구를 사용합니다. ADSI Edit은 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2의 Active Directory 도메인 서비스 도구 기능에 포함됩니다. 이 도구에 대해 자세히 알아보려면 [ADSI Edit(adsiedit.msc)](https://go.microsoft.com/fwlink/p/?linkid=294644)을 참조하세요.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Microsoft 지원 서비스의 지시가 없는 경우 ADSI Edit에서는 절대 값을 변경하지 않도록 합니다. ADSI Edit에서 값을 변경하면 Exchange 조직 및 Active Directory에 치명적인 손상을 줄 수 있습니다.</td>
</tr>
</tbody>
</table>


Exchange에 의해 Active Directory 스키마가 확장되고 Exchange에서 사용할 수 있게 Active Directory가 준비되면 준비가 완료되었음을 나타내기 위해 몇 가지 속성이 업데이트됩니다. 다음 목록의 정보를 사용하여 이러한 속성이 올바른 값을 갖는지 확인합니다. 각 속성은 설치하려는 Exchange 2013 릴리스에 대해 아래 표에 나와 있는 값과 일치해야 합니다.

  - **스키마** 명명 컨텍스트에서 **ms-Exch-Schema-Verision-Pt**의 **rangeUpper** 속성이 Exchange 2013 Active Directory 버전 표에서 현재 사용 중인 Exchange 2013 버전에 표시된 값으로 설정되어 있는지 확인합니다.
    
     

  - **구성** 명명 컨텍스트에서 CN=\<*your organization*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*domain*\> 컨테이너의 **objectVersion** 속성이 Exchange 2013 Active Directory 버전 표에서 현재 사용 중인 Exchange 2013 버전에 표시된 값으로 설정되어 있는지 확인합니다.
    
     

  - **기본** 명명 컨텍스트에서 DC=\<*루트 도메인* 아래 **Microsoft Exchange System Objects** 컨테이너의 **objectVersion** 속성이 Exchange 2013 Active Directory 버전 표에서 현재 사용 중인 Exchange 2013 버전에 표시된 값으로 설정되어 있는지 확인합니다.
    
     

또한 Exchange 설치 로그를 확인하여 Active Directory 준비가 완료되었는지 확인할 수 있습니다. 자세한 내용은 [Exchange 2013 설치를 확인 합니다.](verify-an-exchange-2013-installation-exchange-2013-help.md)을 참조하십시오. Active Directory 사이트에서 하나 이상의 사서함 서버 역할 및 클라이언트 액세스 서버 역할 설치를 완료할 때까지 [Exchange 2013 설치를 확인 합니다.](verify-an-exchange-2013-installation-exchange-2013-help.md) 항목에 언급된 **Get-ExchangeServer** cmdlet을 사용할 수 없습니다.

## Exchange 2013 Active Directory 버전

다음 표에는 Exchange 2013의 새 버전을 설치할 때마다 업데이트되는 Active Directory의 Exchange 2013 개체가 나와 있습니다. 표시되는 개체 버전을 아래 표에 나오는 값과 비교하여 설치한 Exchange 2013의 버전이 설치 중에 Active Directory를 성공적으로 업데이트했는지 확인합니다.


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
<th> </th>
<th>Exchange 버전</th>
<th>rangeUpper</th>
<th>objectVersion</th>
<th>objectVersion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>명명 컨텍스트</strong></p></td>
<td><p> </p></td>
<td><p>Schema</p></td>
<td><p>Default</p></td>
<td><p>Configuration</p></td>
</tr>
<tr class="even">
<td><p><strong>컨테이너</strong></p></td>
<td><p> </p></td>
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>Microsoft Exchange 시스템 개체</p></td>
<td><p>CN=&lt;<em>your organization</em>&gt;, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=&lt;<em>domain</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU10 이상</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>16130</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU9</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU8</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU7</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU6</p></td>
<td><p>15303</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU5</p></td>
<td><p>15300</p></td>
<td><p>13236</p></td>
<td><p>15870</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 SP1</p></td>
<td><p>15292</p></td>
<td><p>13236</p></td>
<td><p>15844</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU3</p></td>
<td><p>15283</p></td>
<td><p>13236</p></td>
<td><p>15763</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU2</p></td>
<td><p>15281</p></td>
<td><p>13236</p></td>
<td><p>15688</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU1</p></td>
<td><p>15254</p></td>
<td><p>13236</p></td>
<td><p>15614</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 RTM</p></td>
<td><p>15137</p></td>
<td><p>13236</p></td>
<td><p>15449</p></td>
</tr>
</tbody>
</table>

