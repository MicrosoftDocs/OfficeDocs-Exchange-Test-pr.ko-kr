---
title: '하이브리드 배포에서 사용 권한을 위임 된 사서함을 지원 하도록 Exchange 구성: Exchange 2013 Help'
TOCTitle: 하이브리드 배포에서 사용 권한을 위임 된 사서함을 지원 하도록 Exchange 구성
ms:assetid: a2a10cb3-4557-4ff5-8191-c653522f4512
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt784505(v=EXCHG.150)
ms:contentKeyID: 74447327
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 하이브리드 배포에서 사용 권한을 위임 된 사서함을 지원 하도록 Exchange 구성

 

_**마지막으로 수정된 항목:**2018-01-30_

사서함 위임 된 권한이 있는 다른 사용자가 다른 사용자 사서함의 일부를 관리할 수 있습니다. 이 일반적인 예로 비서가 경영진의 사서함 및 일정 관리 해야 합니다. 사서함 사용 권한을 위임 하는 온-프레미스 Exchange 조직 및 Office 365 지원에 **대 한 전체 액세스** 및 **대신 보내기** 간의 하이브리드 배포. 그러나의 온-프레미스 조직에 설치 하는 Exchange 버전에 따라 하이브리드 배포에서 사용 권한을 위임 된 사서함을 사용 하 여 추가 구성 작업을 수행 해야할 수 있습니다. 다음 지원 위임 하이브리드 배포에서 사서함 사용 권한 및 해당 버전에 대 한 추가 구성이 필요 여부는 버전의 Exchange 나열 합니다.

  - **Exchange 2016** 추가 구성은 필요 하지 않습니다.

  - **Exchange 2013** A Exchange 2013 누적 업데이트 (CU)를 지원 하 고 추가 구성 요소가 필요 합니다.

  - **Exchange 2010** 지원 되는 Exchange 2010 업데이트를 배포할 (RU) 및 추가 구성 요소가 필요 합니다.

하이브리드 배포에서 사용 권한을 위임 된 사서함을 지원 하기 위해 특정 요구 사항에 대 한 자세한 내용은 [Exchange 하이브리드 배포의 사용 권한](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md)를 살펴보겠습니다.

다음 섹션에서는 과정을 안내 Exchange 2013의 구성 및 Exchange 2010 온-프레미스 배포 사용 권한 위임 된 사서함에 대 한 지원을 사용 하도록 설정 합니다. 다음이 단계를 수행 하기 전에 최신 Exchange 2013 CU 또는 Exchange SP3 RU 이동 중일 있는지 확인 해야 합니다. 자세한 내용은 [하이브리드 배포 필수 구성 요소](hybrid-deployment-prerequisites-exchange-2013-help.md)을 참조 하십시오.

## Exchange 2013

사용 권한 위임 된 사서함에 대 한 지원을 활성화 하려면 수행 하는데 필요한 몇가지 요인에 따라 달라 집니다. Office 365에 및 당시에 사서함을 이동 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>다음은 설치 된...</th>
<th>및 조직에서 ACLable 개체 동기화 된...</th>
<th>그런 다음 해야하는...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU9 또는 이전 버전</p></td>
<td><p>이 기능을 이전 하 고 Exchange 2013 CU9에서 사용할 수 없습니다.</p></td>
<td><p>Acl을 지원 하기 위해 각 사서함을 수동으로 구성</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU10 이상</p></td>
<td><p>사용 안 함</p></td>
<td><ol>
<li><p>조직 수준에서 ACLable 개체 동기화를 사용 하도록 설정</p></li>
<li><p>수동으로 ACLable 개체 동기화 조직 수준에서 사용 하기 전에 Office 365로 이동한 각 사서함에 대 한 Acl을 사용 하도록 설정 합니다.</p></li>
</ol>
<p>조직 수준에서 ACLable 개체 동기화를 설정한 후 Office 365로 이동 하는 사서함에 대 한 없음 추가 구성이 필요 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2013 CU10 이상</p></td>
<td><p>Enabled</p></td>
<td><p>추가 구성이 필요 하지 않습니다.</p></td>
</tr>
</tbody>
</table>


## ACLable 개체 동기화를 사용 하도록 설정

조직 수준에서 ACLable 개체 동기화를 사용 하도록 설정 하려면 다음을 수행 합니다.

1.  모든 AAD 연결 서버에서 Azure Active Directory에 연결 (AAD 연결)의 최신 버전을 설치 합니다. AAD 하이브리드 권한을 지원 하기 위해 필요한 특성을 동기화에 연결할 수 있도록 필요 합니다. [Microsoft Azure Active Directory 연결](http://go.microsoft.com/fwlink/p/?linkid=510956)에서 AAD 연결을 다운로드할 수 있습니다.

2.  최신 사용할 수 있는 Exchange 2013 CU, 또는 바로 이전 CU를 실행 하는 서버에서 Exchange 관리 셸을 엽니다.

3.  다음 명령을 실행합니다.
    
        Set-OrganizationConfig -ACLableSyncedObjectEnabled $True

이 작업을 수행한 후 Office 365로 이동 하는 모든 사서함이 제대로 사용 권한을 위임 된 사서함을 지원 하도록 구성 됩니다. 사서함을 이러한 단계를 완료 하기 전에 Office 365로 이동 된 수동으로에서 원격 사서함에 Acl을 사용 하도록 설정하는 단계를 사용 하 여 해당 사서함에 대 한 Acl을 사용 하도록 설정 하려면 필요 합니다.


> [!IMPORTANT]
> Acl은 Office 365에서 만든 원격 사서함에서 사용 되지 않습니다. Office 365에서 원격 사서함을 만드는 경우 해당 원격 사서함에 대 한 Acl을 사용 하도록 설정 하려면 원격 사서함 섹션에서 사용 하도록 설정 Acl의 단계를 수행 하려면 필요 합니다. 이 추가 단계를 방지 하려면 온-프레미스 Exchange 서버에서 사서함을 만들 다음 Office 365로 사서함을 이동 하는 것이 좋습니다.



## 원격 사서함에 대 한 Acl을 사용 하도록 설정

ACLable 개체 동기화 조직 수준에서 사용 하기 전에 Office 365로 이동 하는 사서함에 대 한 Acl을 사용 하도록 설정 하려면 다음을 수행 합니다.

1.  최신 사용할 수 있는 Exchange 2013 CU, 또는 바로 이전 CU를 실행 하는 서버에서 Exchange 관리 셸을 엽니다.

2.  단일 사서함에 대 한 Acl을 사용 하도록 설정 하려면 다음 명령을 실행 합니다.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Office 365로 이동 하는 모든 사서함에 대 한 Acl을 사용 하도록 설정 하려면 다음 명령을 실행 합니다.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  사서함을 성공적으로 업데이트 된을 확인 하려면 다음 명령을 실행 합니다.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

## Exchange 2010

하지만이 구성을 각 사서함에 수동으로 설정 해야를 Exchange 2010 SP3 서버 원격 사서함에서 Acl의 구성을 지원 합니다. 최신 버전의 Exchange와는 달리 Exchange 2010 조직 수준에서이 기능을 설정 하는 기능을 제공 하지 않습니다. 이전에 Office 365로 이동 하 게 했을 때 모든 사서함 및 이동 될 Exchange 2010 SP3 서버에서 Office 365를 나중에 모든 사서함에 아래 단계를 수행 해야 합니다.

## 원격 사서함에 대 한 Acl을 사용 하도록 설정

Office 365로 이동 하는 사서함에 대 한 Acl을 사용 하도록 설정 하려면 다음을 수행 합니다.

1.  최신 사용할 수 있는 Exchange 2010 s p 3 RU, 또는 바로 이전 RU를 실행 하는 서버에서 Exchange 관리 셸을 엽니다.

2.  단일 사서함에 대 한 Acl을 사용 하도록 설정 하려면 다음 명령을 실행 합니다.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Office 365로 이동 하는 모든 사서함에 대 한 Acl을 사용 하도록 설정 하려면 다음 명령을 실행 합니다.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  사서함을 성공적으로 업데이트 된을 확인 하려면 다음 명령을 실행 합니다.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

