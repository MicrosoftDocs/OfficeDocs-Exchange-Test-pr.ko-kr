---
title: 'Exchange 하이브리드 배포의 사용 권한: Exchange 2013 Help'
TOCTitle: Exchange 하이브리드 배포의 사용 권한
ms:assetid: 58b46b2c-a6b2-424a-8fc2-0f1fe1ad8e18
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ906433(v=EXCHG.150)
ms:contentKeyID: 51407770
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 하이브리드 배포의 사용 권한

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2018-05-02_

Office 365 조직의 Exchange Online은 Exchange Server을 기반으로 하며, 온-프레미스 조직과 같이 RBAC(역할 기반 액세스 제어)를 사용하여 사용 권한을 제어합니다. 관리자에게는 관리 역할 그룹을 사용하여 사용 권한이 부여되고 최종 사용자에게는 관리 역할 할당 정책을 사용하여 사용 권한이 부여됩니다.

Exchange Online 및 온-프레미스 Exchange의 사용 권한에 대한 자세한 내용은 [사용 권한](https://technet.microsoft.com/ko-kr/library/dd351175\(v=exchg.150\))을 참조하세요.

## 관리자 사용 권한

기본적으로 Office 365 테넌트를 만드는 데 사용된 사용자는 Exchange Online 조직에서 조직 관리 역할 그룹의 구성원으로 지정됩니다. 이 사용자는 조직 수준 설정 구성 및 Exchange Online 받는 사람 관리를 비롯하여 전체 Exchange Online 조직을 관리할 수 있습니다.

수행해야 하는 관리에 따라 Exchange Online 조직에서 관리자를 추가할 수 있습니다. 예를 들어 조직 관리자 및 받는 사람 관리자를 추가하고, 전문가 사용자가 검색 등의 준수 작업을 수행할 수 있게 하고, 사용자 지정 사용 권한을 구성하는 등의 작업을 수행할 수 있습니다. Office 365 관리자에 대한 모든 Exchange Online 사용 권한 관리는 EAC(Exchange 관리 센터) 또는 원격 PowerShell을 사용하여 Exchange Online 조직에서 수행해야 합니다.


> [!IMPORTANT]
> 온-프레미스 조직과 Office&nbsp;365 조직 간 사용 권한이 전송되지 않습니다. 온-프레미스 조직에서 정의한 사용 권한은 Office&nbsp;365 조직에서 다시 만들어야 합니다.



자세한 내용은 [역할 그룹 관리](https://technet.microsoft.com/ko-kr/library/jj657480\(v=exchg.150\)) 및 [역할 그룹 구성원 관리](https://technet.microsoft.com/ko-kr/library/jj657492\(v=exchg.150\))를 참조하십시오.

## 사서함 권한 위임

온-프레미스 Exchange 배포에서 사용자가 다양 한 다른 사용자의 사서함에 대 한 사용 권한 부여할 수 있습니다. 이 사서함 위임 된 사용 권한 및 해당 유용한 경우 라고 비서가 다른 사용자의 사서함;의 일부를 관리 해야 합니다. 예 경영진의 일정을 관리 합니다. Exchange 하이브리드 배포 온-프레미스 Exchange 조직에 있는 사서함 및 Office 365에 있는 사서함 간에, 모두는 아니지만, 일부 사서함 권한의 사용을 지원 합니다. 다음 섹션에서는 어떤 권한을 자세히 설명 하며, 지원 되지 않습니다 하이브리드 사서함 사용 권한;를 지원 하기 위해 필요한 추가 구성 및 온-프레미스 조직과 Office 365 간에 사서함 사용 권한을 동기화 되는 방식입니다.

## 하이브리드 환경에서 지원 되는 사서함 사용 권한

다음 사용 권한을 지원 합니다.

  - **모든 권한** 사서함 온-프레미스 Exchange 서버에 **대 한 전체 액세스** 권한을 부여할 수는 Office 365 사서함으로 이동 하 고 그 반대의 경우도 마찬가지입니다. 예, Office 365 사서함이 있는 온-프레미스 공유 사서함에 **대 한 전체 액세스** 권한을 부여할 수 있습니다. 사용자가 Outlook 데스크톱 클라이언트;를 사용 하 여 사서함을 열 해야 합니다. 크로스-프레미스 사서함 사용 권한 웹에 있는 Outlook에서 지원 되지 않습니다.
    

    > [!NOTE]
    > 사용자는 다른 조직에 있는 사서함에 처음 액세스할 때 추가 자격 증명을 받아 자신의 Outlook 프로필에 추가할 수 있습니다.



  - **대신 보내기** 온-프레미스 Exchange 서버에 사서함 **대신 보내기** 권한을 부여할 수는 Office 365 사서함으로 이동 하 고 그 반대의 경우도 마찬가지입니다. 예, Office 365 사서함이 있는 온-프레미스 공유 사서함에는 **대신 보내기** 권한을 부여할 수 있습니다. 사용자가 Outlook 데스크톱 클라이언트;를 사용 하 여 사서함을 열 해야 합니다. 크로스-프레미스 사서함 사용 권한 웹에 있는 Outlook에서 지원 되지 않습니다.
    
    일부 변경 내용은 온-프레미스 Exchange 서버와 Exchange Online 간에 동기화 할 수 있는 권한 대신 보내기 용 Azure Active Directory 연결 서버에 필요 합니다. 자세한 내용은이 항목 뒷부분에 나오는 Azure Active Directory 연결에 하이브리드 사서함 권한에 대 한 활성화 지원 를 참조 하십시오.

  - **Folder permissions** Grants access to the contents of a particular folder.

  - **개인 항목** 대리인을 추가 하는 경우 개인 일정 항목을 보려면 폴더 사용 권한 가진 사용자를 허용 하는 옵션을 구성할 수 있습니다.


> [!NOTE]
> 2 월 2018를 기준으로 모든 액세스를 지원 하기 위한 보내기를 대신 하 여 및 폴더 권한 크로스 포리스트 롤아웃 되 고 년 4 월 2018 하 여 완료 된 것으로 예상 되는 기능입니다.



다음과 같은 사용 권한이 나 기능 **되지** 지원 합니다.

  - **Send-As** 사용자를 다른 사용자의 사서함에서 들리는 수를 표시 하는 것에 처럼 메일을 보낼 수 있습니다.

  - **자동 매핑** 자동으로 사용자에 **대 한 모든 권한** 을 부여 하는 모든 사서함을 열려면 시작 될 때 Outlook을 수 있습니다.

이러한 사용 권한은 다른 사서함에서 수신 하는 모든 사서함을 부여 하는 것은 사서함으로 동시에 이동 해야 합니다. 여러 사서함에서 사용 권한을 수신 하는 사서함을 하는 경우 해당 사서함을 지정 하 고, 권한을 부여 하는 사서함의 모든 동시에 이동 해야 합니다.

## 하이브리드 사서함 권한을 지원 하기 위해 온-프레미스 Exchange 서버를 구성 합니다.

전체 액세스를 사용 하도록 변경 하이브리드 배포의 경우 추가 구성 권한 대신 보낼 수 있습니다를 설치한 Exchange의 버전에 따라 필요한. 다음 표에서 버전의 Exchange Office 365를 사용한 하이브리드 배포에서 사용 권한을 위임 된 사서함을 지원 하 고 어떤 추가 구성이 필요 합니다. Exchange 2013 및 2010 서버와 사서함 Acl을 지원 하도록 구성 하는 방법에 대 한 단계를 [하이브리드 배포에서 사용 권한을 위임 된 사서함을 지원 하도록 Exchange 구성](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md)을 참조 하십시오.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 버전</th>
<th>필수 구성 요소</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2016</p></td>
<td><p>추가 구성이 필요 하지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p>Exchange 2013 서버 다음이 필요 합니다.</p>
<ul>
<li><p>최신 누적 업데이트 (CU) 또는 설치 하는 바로 이전 CU 합니다. 오래 된 cu로 실행 하는 Exchange 2013 서버는 지원 되지 않습니다 하 고 하이브리드 배포에서 사서함 위임 된 사용 권한으로 작동 하지 않을 수 있습니다.</p></li>
<li><p>Exchange 조직 (Acl) 메일 개체에 스탬프가 지정 된 수를 나열 하 고 Office 365와 동기화 하는 액세스 제어를 허용 하도록 구성 됩니다.</p></li>
<li><p>온-프레미스 원격 사서함을 Exchange 2013 CU10 하기 전에 Office 365로 이동 하는 사서함과 연관 된 Acl을 지원 하도록 수동으로 구성 해야 합니다. 원격 사서함을 Exchange 2013 CU10를 실행 하는 서버에서 만든 또는 이상, 그리고 조직 Acl을 허용 하도록 설정 되어 Exchange 후 자동으로 구성 됩니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Exchange 2010 SP3 서버 다음이 필요 합니다.</p>
<ul>
<li><p>최신 업데이트 롤업 (RU) 또는 설치 하는 바로 이전 RU 합니다. 오래 된 RU를 실행 하는 Exchange 2010 SP3 서버 지원 되지 않습니다 및 하이브리드 배포에서 사서함 위임 된 사용 권한으로 작동 하지 않을 수 있습니다.</p></li>
<li><p>온-프레미스 원격 사서함을 Office 365 사서함과 연관 된 Acl을 지원 하도록 구성 해야 합니다. 이 Office 365 사서함과 연결 된 각 온-프레미스 원격 사서함에 대 한 작업을 수행 해야 합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 또는 이전 버전</p></td>
<td><p>지원되지 않습니다.</p></td>
</tr>
</tbody>
</table>


## Azure Active Directory 연결에 하이브리드 사서함 권한에 대 한 지원 사용

또한 온-프레미스 Exchange 서버를 구성 하는 것 외에도 Azure Active Directory에 연결 (AAD 연결) 서버는 하이브리드 사서함 사용 권한을 동기화 할 수 있도록 설정 되어 있는지 확인 해야 합니다. AAD 연결 하는 서버에는 이러한 사용 권한은 지원 하기 위해 준비 되었는지 확인 하기 위해 필요한 다음과 같습니다.

  - **업그레이드 AAD 연결** 이상으로 업그레이드 해야 AAD 연결 1.1.553.0 버전입니다. [Microsoft Azure Active Directory 연결](http://go.microsoft.com/fwlink/p/?linkid=510956)에서 AAD 연결의 최신 버전을 다운로드할 수 있습니다.

  - **Exchange 하이브리드 AAD에 사용 연결** 하이브리드 사서함 사용 권한 (특히 권한 대신 보내기)를 사용 하도록 설정 하는 특성을 동기화 하려면 **Exchange 하이브리드 배포** 구성 옵션 AAD 연결에서 사용 하도록 설정 되었는지 확인 해야 합니다. 체크아웃 해당 구성을 업데이트 하려면 다시 AAD 연결 설치 마법사를 실행 하는 방법에 대 한 내용은, [Azure AD 연결 동기화: 번째로 설치 마법사를 실행 하](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnectsync-installation-wizard)

## 온-프레미스 조직과 Office 365 조직 간에 사서함 사용 권한은 동기화 되는 방식

## 최종 사용자 사용 권한

관리자 사용 권한과 마찬가지로 Exchange Online의 최종 사용자에게 사용 권한을 부여할 수 있습니다. 기본적으로 기본 역할 할당 정책을 통해 최종 사용자에게 사용 권한이 부여됩니다. 이 정책은 Exchange Online 조직의 모든 사서함에 적용됩니다. 기본적으로 부여된 사용 권한이 충분하면 변경할 사항이 없습니다.

최종 사용자 사용 권한을 사용자 지정하려는 경우 기존의 기본 역할 할당 정책을 수정하거나 새로운 할당 정책을 만들 수 있습니다. 여러 할당 정책을 만드는 경우 각 사서함 그룹에 서로 다른 정책을 할당하여, 요구 사항에 따라 각 그룹에 부여된 사용 권한을 제어할 수 있습니다. Exchange Online 최종 사용자에 대한 모든 사용 권한 관리는 EAC 또는 원격 PowerShell을 사용하여 Exchange Online 조직에서 수행해야 합니다.

관리자 사용 권한과 마찬가지로 최종 사용자 사용 권한도 온-프레미스 조직과 Exchange Online 조직 간에 전송되지 않습니다. 온-프레미스 조직에서 정의한 사용 권한은 Exchange Online 조직에서 다시 만들어야 합니다.

자세한 내용은 [역할 할당 정책 관리](https://technet.microsoft.com/ko-kr/library/jj657511\(v=exchg.150\)) 및 [사서함에 할당 정책 변경](https://technet.microsoft.com/ko-kr/library/dd638076\(v=exchg.150\))을 참조하십시오.

다음 표에서는 Exchange Online 조직에서 기본 역할 할당 정책에 의해 부여되는 사용 권한을 보여줍니다.

### 기본 역할 할당 정책 사용 권한

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>관리 역할</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyTeamMailboxes</p></td>
<td><p><code>MyTeamMailboxes</code> 관리 역할을 사용하면 개별 사용자가 사이트 사서함을 만들고 이를 Microsoft SharePoint 사이트에 연결할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>내 마켓플레이스 앱</p></td>
<td><p><code>My Marketplace Apps</code> 관리 역할을 사용하면 개별 사용자가 자신의 Microsoft Office 마켓플레이스 앱을 보고 수정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>MyBaseOptions</p></td>
<td><p>개별 사용자는 <code>MyBaseOptions</code> 관리 역할을 사용하여 자신의 사서함 및 연결된 설정의 기본 구성을 보고 수정할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>MyContactInformation</p></td>
<td><p><code>MyContactInformation</code> 관리 역할을 사용하면 개별 사용자가 주소와 전화 번호를 비롯한 연락처 정보를 수정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>MyDistributionGroupMembership</p></td>
<td><p>조직의 메일 그룹에서 그룹 구성원을 조작할 수 있는 경우 개별 사용자는 <code>MyDistributionGroupMembership</code> 관리 역할을 사용하여 조직의 메일 그룹에서 구성원을 보고 수정할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>MyDistributionGroups</p></td>
<td><p><code>MyDistributionGroups</code> 관리 역할을 사용하면 개별 사용자가 메일 그룹을 만들고 수정하고 볼 수 있으며 소유한 메일 그룹을 수정하고 보고 제거하고 구성원을 추가할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>MyMailSubscription</p></td>
<td><p><code>MyMailSubscription</code> 역할은 개별 사용자가 메시지 형식 및 프로토콜 기본값 등의 전자 메일 구독 설정을 보고 수정할 수 있게 해줍니다.</p></td>
</tr>
<tr class="even">
<td><p>MyProfileInformation</p></td>
<td><p><code>MyProfileInformation</code> 관리 역할을 사용하면 개별 사용자가 자신의 이름을 수정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>MyRetentionPolicies</p></td>
<td><p>개별 사용자는 <code>MyRetentionPolicies</code> 관리 역할을 사용하여 보존 태그를 보고, 보존 태그 설정 및 기본값을 보고 수정할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>MyTextMessaging</p></td>
<td><p><code>MyTextMessaging</code> 관리 역할을 사용하면 개별 사용자가 텍스트 메시징 설정을 만들고, 보고, 수정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>MyVoiceMail</p></td>
<td><p><code>MyVoiceMail</code> 관리 역할을 사용하면 개별 사용자가 음성 메일 설정을 보고 수정할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>MyReadWriteMailbox 앱</p></td>
<td><p><code>My ReadWriteMailbox Apps</code> 관리 역할을 사용하면 사용자가 ReadWriteMailbox 사용 권한으로 앱을 설치할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>MyCustom 앱</p></td>
<td><p><code>My Custom Apps</code> 관리 역할을 사용하면 사용자가 사용자 지정 앱을 보고 수정할 수 있습니다.</p></td>
</tr>
</tbody>
</table>

