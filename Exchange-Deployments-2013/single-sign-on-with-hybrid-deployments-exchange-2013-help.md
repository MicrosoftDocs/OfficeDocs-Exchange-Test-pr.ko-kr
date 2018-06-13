---
title: '하이브리드 배포 SSO(Single Sign-On): Exchange 2013 Help'
TOCTitle: 하이브리드 배포 SSO(Single Sign-On)
ms:assetid: 050606f9-718d-4a1f-b7a6-50b08c6e9e07
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh563846(v=EXCHG.150)
ms:contentKeyID: 50484623
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 하이브리드 배포 SSO(Single Sign-On)

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-01-29_

Single Sign-On을 사용하면 사용자는 단일 사용자 이름과 암호로 온-프레미스 조직과 Office 365 조직 모두에 액세스할 수 있습니다. Single Sign-On은 사용자에게 익숙한 로그온 환경을 제공하고 이를 통해 관리자는 온-프레미스 Active Directory 관리 도구를 사용하여 Exchange Online 조직 사서함에 대한 계정 정책을 쉽게 제어할 수 있습니다. Single Sign-On을 사용하여 하이브리드 배포를 구성하지 않아도 되는 경우라도 수행하는 것이 좋습니다. Single Sign-On을 수행하지 않으면 사용자가 온-프레미스 조직 및 Office 365에 대한 서로 다른 두 개의 자격 증명을 기억해야 합니다. Single Sign-On에 대한 기타 몇 가지 장점은 다음과 같습니다.

  - **Exchange Online Archiving**   Single Sign-On을 배포하면 온-프레미스 Outlook 사용자가 Exchange Online 조직에서 보관된 콘텐츠에 처음 액세스할 때 자격 증명을 묻는 메시지가 표시됩니다. "암호 저장"을 선택하여 이후에 자격 증명을 묻는 메시지가 임시로 표시되지 않도록 할 수 있지만 온-프레미스 계정 암호가 변경되면 다시 표시됩니다. Single Sign-On을 Exchange 조직에 배포하지 않고 Exchange Online Archiving이 사용하도록 설정된 경우에는 온-프레미스 UPN(사용자 계정 이름)이 해당 Exchange Online 계정과 일치해야 합니다. 사용자에게는 보관된 콘텐츠에 액세스할 때 온-프레미스 자격 증명을 묻는 메시지가 항상 표시됩니다.

  - **정책 제어**Active Directory를 통해 계정 정책을 제어할 수 있으므로, Office 365 조직에서 추가 작업을 수행하지 않고도 암호 정책, 워크스테이션 제한, 잠금 제어 등을 관리할 수 있습니다.

  - **지원 전화 감소**   암호를 잊어버리는 것은 모든 회사에서 지원 전화를 하는 일반적인 이유입니다. 사용자가 기억해야 할 암호가 적으면 잊어버릴 가능성도 줄어듭니다.

Single Sign-On을 배포할 때 암호 동기화 및 Active Directory AD FS(페더레이션 서비스)의 두 가지 옵션이 있습니다. 두 옵션은 Azure Active Directory Connect에서 제공됩니다. AD FS가 필요한 특정 요구 사항이 없다면 암호 동기화 방법을 사용하는 것이 좋습니다. 암호 동기화에서 배포의 복잡함 없이 AD FS의 동일한 혜택을 다수 제공합니다. 다음 표에는 각 옵션에 대한 일부 일반적인 장점 및 단점이 나와 있습니다.


> [!NOTE]
> 기본적으로 어떤 이유로 인터넷에서 연결할 수 없는 AD FS 및 온-프레미스 AD FS 서버를 배포하는 경우 Office 365는 사용자를 인증하기 위해 암호 동기화로 변경합니다. 이렇게 하면 사용자는 Office 365 사서함을 사용하여 온-프레미스 서버를 사용할 수 없는 경우에도 중단 없이 작업을 계속할 수 있습니다.



각 옵션에 대한 자세한 내용은 [Azure AD Connect 사용자 로그인 옵션](http://go.microsoft.com/fwlink/p/?linkid=723514)을 참조하세요.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Single Sign-On 방법</p></th>
<th><p>장점</p></th>
<th><p>단점</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>암호 동기화(권장)</p></td>
<td><ul>
<li><p>AD FS 보다 현저히 낮은 복잡성</p></li>
<li><p>사용자가 온-프레미스 Active Directory를 사용할 수 없는 경우에도 Office 365에 로그인할 수 있습니다.</p></li>
<li><p>암호 동기화를 배포하는 데 더 적은 서버가 추가로 필요합니다.</p></li>
<li><p>타사 인증서가 필요하지 않습니다.</p></li>
<li><p>AD FS 통해 온-프레미스 Active Directory에 대한 외부 액세스가 필요하지 않습니다.</p></li>
<li><p>배포를 몇 시간 내에 완료할 수 있는 경우가 많습니다.</p></li>
</ul></td>
<td><ul>
<li><p>온-프레미스 Active Directory에서 사용자 계정을 사용하지 않으면 Office 365에서 사용하지 않도록 설정되지 않습니다. Office 365 관리자 포털에서 계정을 수동으로 사용하지 않도록 설정해야 합니다.</p></li>
<li><p>온-프레미스 Active Directory가 필요합니다. 다른 디렉터리 서비스는 지원되지 않습니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AD FS</p></td>
<td><ul>
<li><p>암호가 즉시 변경됩니다.</p></li>
<li><p>온-프레미스 Active Directory에서 사용자를 사용하지 않으면 해당 온-프레미스 네트워크 액세스와 자신의 Office 365 계정을 모두 사용할 수 없습니다.</p></li>
<li><p>Active Directory 외 기타 디렉터리 서비스를 지원합니다.</p></li>
<li><p>매우 크고 다양한 배포를 지원합니다.</p></li>
<li><p>2단계 인증을 지원합니다.</p></li>
</ul></td>
<td><ul>
<li><p>경계 네트워크에 있어야 하는 서버가 하나 이상 더 필요합니다.</p></li>
<li><p>방화벽에서 열 수 있어야 하는 공용 IP 주소와 TCP 포트 443이 필요합니다.</p></li>
<li><p>계정 암호에 대한 변경 사항 및 계정이 최근에 사용하거나 사용하지 않도록 설정되었는지 검색할 수 있도록 온-프레미스 Active Directory와의 연결이 필요합니다.</p></li>
</ul></td>
</tr>
</tbody>
</table>

