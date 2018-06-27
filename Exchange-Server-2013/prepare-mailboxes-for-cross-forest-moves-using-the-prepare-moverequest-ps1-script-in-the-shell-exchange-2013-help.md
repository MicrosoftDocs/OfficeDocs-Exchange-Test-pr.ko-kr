---
title: '셸에서 준비 MoveRequest.ps1 스크립트를 사용 하 여 크로스 포리스트 이동에 대 한 준비 사서함: Exchange 2013 Help'
TOCTitle: 셸에서 준비 MoveRequest.ps1 스크립트를 사용 하 여 크로스 포리스트 이동에 대 한 준비 사서함
ms:assetid: 2cea59fb-69b7-4a2f-833f-de4d93cf1810
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee861103(v=EXCHG.150)
ms:contentKeyID: 50482721
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 셸에서 준비 MoveRequest.ps1 스크립트를 사용 하 여 크로스 포리스트 이동에 대 한 준비 사서함

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-11-22_

**요약:** Exchange 관리 셸 에서 준비 MoveRequest.ps1 스크립트를 사용 하 여 크로스 포리스트 사서함 이동 및 마이그레이션 Exchange 2013 에서 관리 하는 방법에 알아봅니다.

Microsoft Exchange 2013 사서함 이동 및 **New-MoveRequest** 및 **New-MigrationBatch** cmdlet을 사용 하 여 마이그레이션을 지원 합니다. Exchange 관리 센터 (EAC)를 통해 사서함에 이동할 수도 있습니다. 대상 Exchange 2013 포리스트에 원본 Exchange 포리스트의 Exchange 2010 또는 Exchange 2013 사서함을 이동할 수 있습니다.

**New-MoveRequest** 및 **New-MigrationBatch** cmdlet을 실행하려면 메일 사용자가 대상 Exchange 포리스트에 존재해야 하며 필요한 Active Directory 특성의 최소 집합을 갖고 있어야 합니다.

이 항목에서 설명하는 Windows PowerShell 샘플 스크립트는 Exchange 2013 원본 포리스트의 사서함 사용자를 메일 사용이 가능한 사용자로 Exchange 2013 대상 포리스트와 동기화하여 이 작업을 지원합니다. 스크립트는 원본 포리스트에 속하는 사서함 사용자의 Active Directory 특성을 대상 포리스트로 복사한 후 **Update-Recipient** cmdlet을 사용하여 대상 개체를 메일 사용이 가능한 사용자로 전환합니다.

스크립트 사용 및 작성에 대한 자세한 내용은 [Exchange 관리 셸을 사용하여 스크립팅](https://technet.microsoft.com/ko-kr/library/bb123798\(v=exchg.150\))을 참조하십시오. 포리스트 간 이동 준비에 대한 자세한 내용은 [크로스 포리스트 이동 요청에 대 한 사서함을 준비](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)를 참조하십시오.

원격 이동 요청과 관련된 다른 관리 작업에 대한 자세한 내용은 [온-프레미스 이동 관리](manage-on-premises-moves-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 스크립트는 다음 위치에서 찾습니다. Program Files\\Microsoft\\Exchange Server\\V15\\Scripts

  - 이 샘플 스크립트를 실행하려면 다음이 필요합니다.
    
      - Exchange 원본 포리스트, 사서함은 현재 있습니다. 이 Exchange 2010 또는 Exchange 2013 사서함 수 있습니다.
    
      - Exchange 2013이 설치되어 있으며 사서함을 이동할 대상 포리스트.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## Prepare-MoveRequest.ps1 스크립트를 사용하여 사서함의 크로스 포리스트 이동 준비

대상 Exchange 2013 포리스트에서 Exchange 2013을 실행하는 서버 역할에 있는 셸에서 스크립트를 실행합니다. 이 스크립트는 원본 포리스트에서 사서함 특성을 복사합니다.

원격 포리스트의 도메인 컨트롤러에 대 한 특정 인증 자격 증명을 할당 하려면 Windows PowerShell **Get-Credential** cmdlet을 실행 하 고 사용자 입력을 임시 변수에 저장 먼저 해야 합니다. **Get-Credential** cmdlet을 실행 하는 경우 cmdlet은 사용자 이름 및 원격 포리스트의 도메인 컨트롤러를 사용 하 여 인증 하는 동안 사용 되는 계정의 암호를 묻습니다. 그런 다음 준비 MoveRequest.ps1 스크립트에서 임시 변수를 사용할 수 있습니다. **Get-Credential** cmdlet에 대 한 자세한 내용은 [Get-credential](https://go.microsoft.com/fwlink/p/?linkid=142122)을 참조 하십시오.


> [!NOTE]
> 이 스크립트를 호출할 때 로컬 포리스트와 원격 포리스트에 대해 서로 다른 두 가지 자격 증명을 사용해야 합니다.



1.  다음 명령을 실행하여 로컬 포리스트와 원격 포리스트 자격 증명을 가져옵니다.
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  다음 명령을 실행하여 자격 증명 정보를 Prepare-MoveRequest.ps1 스크립트의 *LocalForestCredential* 및 *RemoteForestCredential* 매개 변수로 전달합니다.
    
        Prepare-MoveRequest.ps1 -Identity JohnSmith@Fabrikan.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials

## 스크립트의 매개 변수 집합

다음 표에서는 스크립트의 매개 변수 집합에 대해 설명합니다.

### Prepare-MoveRequest.ps1 스크립트의 매개 변수 집합

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
<td><p><em>Identity</em></p></td>
<td><p>필수</p></td>
<td><p><em>Identity</em> 매개 변수는 원본 포리스트에서 사서함을 고유하게 식별합니다. ID는 다음 중 하나일 수 있습니다.</p>
<ul>
<li><p>CN(일반 이름)</p></li>
<li><p>별칭</p></li>
<li><p><strong>proxyAddress</strong> 속성</p></li>
<li><p><strong>objectGuid</strong> 속성</p></li>
<li><p><strong>DisplayName</strong> 속성</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RemoteForestCredential</em></p></td>
<td><p>필수</p></td>
<td><p><em>RemoteForestCredential</em> 매개 변수는 원본 포리스트 Active Directory에서 데이터를 복사할 권한을 가진 관리자를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>RemoteForestDomainController</em></p></td>
<td><p>필수</p></td>
<td><p><em>RemoteForestDomainController</em> 매개 변수는 사서함이 있는 원본 포리스트의 도메인 컨트롤러를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableEmailAddressPolicy</em></p></td>
<td><p>선택 사항</p></td>
<td><p><em>DisableEmailAddressPolicy</em> 매개 변수는 대상 포리스트에서 <strong>MailUser</strong> 개체를 만들 때 EAP(전자 메일 주소 정책)를 사용하지 못하도록 할지 여부를 지정합니다.</p>
<p>이 매개 변수를 지정할 때 대상 포리스트의 EAP는 적용되지 않습니다.</p>

> [!NOTE]
> 이 매개 변수를 지정할 때 <STRONG>MailUser</STRONG> 개체에는 로컬 포리스트 도메인의 전자 메일 주소 매핑에 대한 스탬프 처리가 되지 않습니다. 일반적으로 EAP에 의해 스탬프 처리가 됩니다.


</td>
</tr>
<tr class="odd">
<td><p><em>LinkedMailUser</em></p></td>
<td><p>선택 사항</p></td>
<td><p><em>LinkedMailUser</em> 스위치는 원격 포리스트의 사서함 사용자를 위해 로컬 포리스트에서 연결된 MailUser를 만들지 여부를 지정합니다.</p>
<p>이 스위치가 제공되는 경우 스크립트는 원본 사서함에 연결된 대상 <strong>MailUser</strong> 개체를 만듭니다. 스위치가 생략되면 스크립트는 일반 대상 <strong>MailUser</strong> 개체를 만듭니다.</p></td>
</tr>
<tr class="even">
<td><p><em>LocalForestCredential</em></p></td>
<td><p>선택 사항</p></td>
<td><p><em>LocalForestCredential</em> 매개 변수는 대상 포리스트 Active Directory에 데이터를 쓸 권한을 가진 관리자를 지정합니다.</p>
<p>Active Directory 권한 문제를 방지하기 위해 이 매개 변수를 명시적으로 지정하는 것이 좋습니다.</p>
<p>원격 포리스트와 로컬 포리스트를 신뢰할 수 있는 관계로 구성한 경우에는 원격 사용자 계정이 로컬 포리스트의 Active Directory를 수정할 권한을 갖고 있더라도 원격 포리스트의 사용자 계정을 로컬 포리스트 자격 증명으로 사용하지 마십시오.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalForestDomainController</em></p></td>
<td><p>선택 사항</p></td>
<td><p><em>LocalForestDomainController</em> 매개 변수는 메일 사용이 가능한 사용자를 만들 대상 포리스트의 도메인 컨트롤러를 지정합니다.</p>
<p>임의의 도메인 컨트롤러를 선택하는 경우 로컬 포리스트에서 발생될 수 있는 도메인 컨트롤러 복제 지연 문제를 방지하려면 이 매개 변수를 지정하는 것이 좋습니다.</p></td>
</tr>
<tr class="even">
<td><p><em>MailboxDeliveryDomain</em></p></td>
<td><p>선택 사항</p></td>
<td><p><em>MailboxDeliveryDomain</em> 매개 변수는 스크립트가 올바른 원본 사서함 사용자의 <strong>proxyAddress</strong> 속성을 대상 메일 사용이 가능한 사용자의 <strong>targetAddress</strong> 속성으로 선택할 수 있도록 원본 포리스트의 신뢰할 수 있는 도메인을 지정합니다.</p>
<p>기본적으로 원본 사서함 사용자의 기본 SMTP 주소는 대상 메일 사용이 가능한 사용자의 <strong>targetAddress</strong> 속성으로 설정됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>OverWriteLocalObject</em></p></td>
<td><p>선택 사항</p></td>
<td><p><em>OverWriteLocalObject</em> 매개 변수는 Active Directory 마이그레이션 도구로 만든 사용자에 대해 사용됩니다. 속성은 기존 메일 연락처에서 새로 만든 메일 사용자로 복사됩니다. 하지만 이 복사 이후 스크립트는 또한 원본 포리스트 사용자에서 새로 만든 메일 사용자로 해당 속성을 복사합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetMailUserOU</em></p></td>
<td><p>선택 사항</p></td>
<td><p><em>TargetMailuserOU</em> 매개 변수는 대상 메일 사용이 가능한 사용자를 만들 OU(조직 구성 단위)를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseLocalObject</em></p></td>
<td><p>선택 사항</p></td>
<td><p><em>UseLocalObject</em> 매개 변수는 스크립트가 로컬 포리스트에서 생성될 메일 사용이 가능한 사용자와 충돌하는 개체를 발견한 경우 기존의 로컬 개체를 필요한 대상 메일 사용이 가능한 사용자로 변환하도록 할지 여부를 지정합니다.</p></td>
</tr>
</tbody>
</table>


## 예

이 섹션에는 Prepare-MoveRequest.ps1 스크립트 사용 방법 예가 몇 가지 들어 있습니다.

## 예: 메일 사용이 가능한 연결된 단일 사용자

원격 포리스트와 로컬 포리스트 간의 포리스트 신뢰 관계가 있을 때 이 예제는 로컬 포리스트에 연결된 메일 사용이 가능한 단일 사용자를 프로비전합니다.

1.  다음 명령을 실행하여 로컬 포리스트와 원격 포리스트 자격 증명을 가져옵니다.
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  다음 명령을 실행하여 자격 증명 정보를 Prepare-MoveRequest.ps1 스크립트의 *LocalForestCredential* 및 *RemoteForestCredential* 매개 변수로 전달합니다.
    
        Prepare-MoveRequest.ps1 -Identity JamesAlvord@Contoso.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials -LinkedMailUser 

## 예: 파이프라이닝

사서함 ID 목록을 제공하면 이 예는 파이프라이닝을 지원합니다.

1.  다음 명령을 실행합니다.
    
        $UserCredentials = Get-Credential

2.  다음 명령을 실행하여 자격 증명 정보를 Prepare-MoveRequest.ps1 스크립트의 *RemoteForestCredential* 매개 변수로 전달합니다.
    
        "IanP@Contoso.com", "JoeAn@Contoso.com" | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## 예: .csv 파일을 사용하여 메일 사용 가능 사용자를 대량으로 만들기

원본 포리스트의 사서함 ID 목록을 포함하는 .csv 파일을 만든 후 이 파일의 내용을 스크립트로 파이프라이닝하여 메일 사용이 가능한 대상 사용자를 대량으로 만들 수 있습니다.

예를 들어 .csv 파일의 내용은 다음과 같을 수 있습니다.

Identity

Ian@contoso.com

John@contoso.com

Cindy@contoso.com

이 예에서는 .csv 파일을 호출하여 메일 사용이 가능한 대상 사용자를 대량으로 만듭니다.

1.  다음 명령을 실행하여 원격 포리스트 자격 증명을 가져옵니다.
    
        $UserCredentials = Get-Credential

2.  다음 명령을 실행하여 자격 증명 정보를 Prepare-MoveRequest.ps1 스크립트의 *RemoteForestCredential* 매개 변수로 전달합니다.
    
        Import-Csv Test.csv | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## 대상 개체별 스크립트 동작

이 섹션에서는 대상 개체에 대한 몇 가지 시나리오와 관련된 스크립트 수행 방법에 대해 설명합니다.

## 대상 메일 사용이 가능한 개체 복제

스크립트가 원본 사서함 사용자에서 대상 메일 사용이 가능한 사용자를 만들려 할 때 중복된 로컬 메일 사용이 가능한 개체를 발견하면 다음 로직을 사용합니다.

  - 원본 사서함 사용자의 **masterAccountSid** 특성이 대상 개체의 **objectSid** 또는 **masterAccountSid** 특성과 일치하는 경우:
    
      - 스크립트는 메일 사용이 불가능한 개체를 메일 사용이 가능한 사용자로 변환하는 기능을 지원하지 않으므로 대상 개체가 메일을 사용할 수 없는 경우 오류가 반환됩니다.
    
      - 대상 개체가 메일을 사용할 수 있으면 대상 개체는 복제본입니다.

  - 원본 사서함 사용자의 **proxyAddress** 속성(smtp/x500만 해당)에 포함되는 주소가 대상 개체의 **proxyAddress** 속성(smtp/x500만 해당)에 포함된 주소와 같은 경우 대상 개체는 복제본입니다.

스크립트를 실행하면 중복된 개체임을 사용자에게 알려줍니다.

대상 메일 사용이 가능한 개체가 주로 크로스 포리스트(Identity Lifecycle Management 2007 서비스 팩 1 기반) GAL(전체 주소 목록) 동기화 배포에 의해 생성된 메일 사용이 가능한 사용자 또는 연락처인 경우 사용자는 *UseLocalObject* 매개 변수를 통해 스크립트를 다시 실행하여 사서함 마이그레이션을 위한 대상 메일 사용이 가능한 개체를 사용할 수 있습니다.

## 메일 사용이 가능한 사용자

대상 개체가 메일 사용이 가능한 사용자인 경우 스크립트는 원본 사서함 사용자의 다음 특성을 대상 메일 사용이 가능한 사용자로 복사합니다.

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

*LinkedMailUser* 매개 변수가 설정된 경우 스크립트는 원본 **objectSid**/**masterAccountSid** 특성을 복사합니다.

## 메일 사용이 가능한 연락처

대상 개체가 메일 사용이 가능한 연락처인 경우 스크립트는 기존 연락처를 삭제하고 모든 특성을 새 메일 사용이 가능한 사용자로 복사합니다. 또한 스크립트는 원본 사서함 사용자의 다음과 같은 특성을 복사합니다.

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

  - **sAMAccountName**

  - **userAccountControl**(514 //equivalent to 0x202, ACCOUNTDISABLE | NORMAL\_ACCOUNT로 설정)

  - **userPrincipalName**

*LinkedMailUser* 매개 변수가 설정된 경우 스크립트는 원본 **objectSid**/**masterAccountSid** 특성을 복사합니다.

## LegacyExchangeDN 특성

**Update-Recipient** cmdlet가 호출 되는 메일 사용이 가능한 사용자로 대상 개체를 변환 하는 새 **LegacyExchangeDN** 특성은 대상 메일 사용이 가능한 사용자에 대해 생성 됩니다. x500으로 대상 메일 사용이 가능한 사용자의 **LegacyExchangeDN** 특성을 복사 하는 스크립트는 원본 사서함 사용자의 **proxyAddress** 속성에는 주소입니다.

