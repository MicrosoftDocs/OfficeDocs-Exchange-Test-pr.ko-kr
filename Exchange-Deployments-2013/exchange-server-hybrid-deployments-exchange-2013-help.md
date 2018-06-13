---
title: 'Exchange Server 하이브리드 배포: Exchange 2013 Help'
TOCTitle: '@NoTitle'
ms:assetid: 59e32000-4fcf-417f-a491-f1d8f9aeef9b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ200581(v=EXCHG.150)
ms:contentKeyID: 50484631
ms.date: 04/20/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 하이브리드 배포

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2018-04-16_

**요약:** Exchange 하이브리드 배포를 계획하기 위해 알아야 할 사항입니다.

조직에서 하이브리드 배포를 활용하면 기존 온-프레미스 Microsoft Exchange 조직의 풍부한 기능과 관리 제어 능력을 클라우드로 확장할 수 있습니다. 하이브리드 배포에서는 온-프레미스 Exchange 조직과 Microsoft Office 365의 Exchange Online 간에 단일 Exchange 조직의 원활한 모양과 느낌을 제공합니다. 또한 Exchange Online 조직으로 완전하게 이전하는 중간 단계로 하이브리드 배포를 활용할 수 있습니다.

**목차**

Exchange 하이브리드 배포 기능

Exchange 하이브리드 배포 시 고려 사항

Exchange 하이브리드 배포 구성 요소

Exchange 하이브리드 배포 예제

Exchange 하이브리드 배포를 구성하기 전에 고려해야 할 사항

주요 용어

Exchange 하이브리드 배포 설명서

## Exchange 하이브리드 배포 기능

하이브리드 배포를 통해 다음 기능을 사용할 수 있습니다.

  - 온-프레미스 조직과 Exchange Online 조직 간의 보안 메일 라우팅

  - 공유 도메인 네임스페이스를 사용한 메일 라우팅. 예를 들어 온-프레미스 조직과 Exchange Online 조직 모두 @contoso.com SMTP 도메인을 사용합니다.

  - "공유 주소록"이라고도 하는 통합 GAL(전체 주소 목록)

  - 온-프레미스 조직과 Exchange Online 조직 간에 약속 있음/없음 및 일정 공유

  - 중앙 집중식 인바운드 및 아웃바운드 메일 흐름 제어. 모든 인바운드 및 아웃바운드 Exchange Online 메시지를 온-프레미스 Exchange 조직을 통해 라우팅되도록 구성할 수 있습니다.

  - 온-프레미스 조직과 Exchange 온라인 조직 모두에 대해 단일 웹에서 Outlook URL 사용

  - 기존 온-프레미스 사서함을 Exchange Online 조직으로 이동할 수 있는 기능 필요한 경우 Exchange Online 사서함을 온-프레미스 조직으로 되돌릴 수도 있습니다.

  - 온-프레미스 EAC(Exchange 관리 센터)를 사용한 중앙 집중식 사서함 관리.

  - 메시지 추적, 메일 설명 및 온-프레미스 조직과 Exchange Online 조직 간의 여러 사서함 검색

  - 온-프레미스 Exchange 사서함의 클라우드 기반 메시지 보관. Exchange Online Archiving은 하이브리드 배포와 함께 사용할 수 있습니다. Exchange Online Archiving에 대한 자세한 내용은 [Microsoft Office 365 추가 서비스](https://go.microsoft.com/fwlink/p/?linkid=233231)를 참조하십시오.

## Exchange 하이브리드 배포 시 고려 사항

Exchange 하이브리드 배포를 구현하기 전에 다음을 고려해야 합니다.

  - **하이브리드 배포 요구 사항** 하이브리드 배포를 구성하기 전에 온-프레미스 조직이 정상적인 배포에 필요한 필수 구성 요소를 모두 충족하는지 확인해야 합니다. 자세한 내용은 [하이브리드 배포 필수 구성 요소](hybrid-deployment-prerequisites-exchange-2013-help.md) 항목을 참조하세요.

  - **Exchange ActiveSync 클라이언트**  온-프레미스 Exchange 조직에서 Exchange Online으로 사서함을 이동하는 경우 해당 사서함에 액세스하는 모든 클라이언트를 Exchange Online을 사용하도록 업데이트해야 합니다. 여기에는 Exchange ActiveSync 장치가 포함됩니다. 이제 Exchange Online으로 사서함을 이동할 때 대부분의 Exchange ActiveSync 클라이언트가 자동으로 다시 구성됩니다. 자세한 내용은 [Exchange 하이브리드 배포를 사용한 Exchange ActiveSync 장치 설정](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md)을 참조하세요.

  - **사서함 권한 마이그레이션**  사서함에 명시적으로 적용된 다른 사람 이름으로 보내기, 모든 권한, 대신 보내기 및 폴더 사용 권한 등의 온-프레미스 사서함 사용 권한은 Exchange Online으로 마이그레이션됩니다. 상속된(비명시적) 사서함 사용 권한 및 Exchange Online에서 메일을 사용할 수 없는 개체에 부여된 사용 권한은 마이그레이션되지 않습니다. 마이그레이션 전에 모든 사용 권한이 명시적으로 부여되고 모든 개체가 메일을 사용할 수 있도록 설정해야 합니다. 따라서 조직에 해당하는 경우 Office 365에서 이러한 사용 권한 구성을 계획해야 합니다. 다른 사람 이름으로 보내기 사용 권한의 경우, 다른 이름으로 받을 사용자와 리소스가 동시에 이동하지 않으면 **Add-RecipientPermission** cmdlet을 사용하여 Exchange Online에서 다른 사람 이름으로 보내기 권한을 명시적으로 추가해야 합니다.

  - **프레미스 간 사서함 사용 권한에 대한 지원** Exchange 하이브리드 배포에서는 온-프레미스 Exchange 조직에 있는 사서함과 Office 365에 있는 사서함 간에 사용 권한의 대신 보내기 및 모든 권한을 사용할 수 있습니다. 대신 보내기 권한을 사용하려면 추가 단계가 필요합니다. 또한 일부 추가 구성의 경우 사용자 온-프레미스 조직에 설치된 Exchange 버전에 따라 프레미스 간 사서함 사용 권한이 필요할 수도 있습니다. 자세한 내용은 [Exchange 하이브리드 배포의 사용 권한](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md) 및 [하이브리드 배포에서 사용 권한을 위임 된 사서함을 지원 하도록 Exchange 구성](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md)에서 [사서함 사용 권한 위임](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md)을 참조하세요.
    

    > [!NOTE]
    > 2018년 2월부터 모든 권한, 다른 사람 이름으로 보내기 및 폴더 사용 권한 상호 포리스트를 지원하는 기능이 공개되고 2018년 4월에 완료될 예정입니다.



  - **오프보딩**  받는 사람 관리를 수행하는 동안 Exchange Online 사서함을 온-프레미스 환경으로 다시 이동해야 할 수 있습니다.
    
    Exchange 2010 기반 하이브리드 배포에서 사서함을 이동하는 방법에 대한 자세한 내용은 [온-프레미스 조직으로 Exchange Online 사서함 이동](https://technet.microsoft.com/ko-kr/library/hh882527\(v=exchg.150\))을 참조하세요.
    
    Exchange 2013 기반 하이브리드 배포에서 사서함을 이동하는 방법에 대한 자세한 내용은 [하이브리드 배포에서 온-프레미스 및 Exchange Online 조직 간의 사서함 이동](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md)을 참조하세요.

  - **사서함 전달 설정** 사서함에 전송된 메일을 다른 사서함으로 자동으로 전달하도록 사서함을 설정할 수 있습니다. 사서함 전달은 Exchange Online에서 지원되지만, 사서함이 마이그레이션되어도 전달 구성은 Exchange Online으로 복사되지 않습니다. Exchange Online으로 사서함을 마이그레이션하기 전에 각 사서함에 대해 전달 구성을 내보내야 합니다. 전달 구성은 각 사서함의 `DeliverToMailboxAndForward`, `ForwardingAddress` 및 `ForwardingSmtpAddress` 속성에 저장됩니다.

## Exchange 하이브리드 배포 구성 요소

하이브리드 배포에는 여러 서비스 및 구성 요소가 사용됩니다.

  - **Exchange 서버**  하이브리드 배포를 구성하려면 Exchange 서버가 온-프레미스 조직에 하나 이상 구성되어야 합니다. Exchange 2013 이전 릴리스를 실행 중인 경우 사서함 및 클라이언트 액세스 역할을 실행하는 서버를 하나 이상 설치해야 합니다. Exchange 2016 이상 릴리스를 실행 중인 경우 사서함 역할을 실행하는 서버를 하나 이상 설치해야 합니다. 필요한 경우 Exchange Edge 전송 서버를 경계 네트워크에 설치할 수도 있으며 Office 365와의 보안 메일 흐름이 지원됩니다.
    

    > [!NOTE]
    > 경계 네트워크에서 사서함 또는 클라이언트 액세스 서버 역할을 실행하는 Exchange 서버 설치는 지원하지 않습니다.



  - **Microsoft Office 365**   Office 365 서비스에는 구독 서비스의 일부로 Exchange 온라인 조직이 포함되어 있습니다. 하이브리드 배포를 구성하는 조직에서는 Exchange Online 조직에서 만들었거나 Exchange Online 조직으로 마이그레이션한 각 사서함에 대한 라이선스를 구입해야 합니다.

  - **하이브리드 구성 마법사**Exchange에는 온-프레미스 Exchange 조직과 Exchange Online 조직 간에 하이브리드 배포를 구성하도록 간소화된 프로세스를 제공하는 하이브리드 구성 마법사가 포함되어 있습니다.
    
    자세한 내용은 [하이브리드 구성 마법사](hybrid-configuration-wizard-exchange-2013-help.md)를 참조하세요.

  - **Azure AD 인증 시스템**   Azure AD(Active Directory) 인증 시스템은 온-프레미스 Exchange 2016 조직과 Exchange Online 조직 간의 트러스트 브로커 역할을 하는 클라우드 기반 무료 서비스입니다. 하이브리드 배포를 구성하는 온-프레미스 조직은 Azure AD 인증 시스템과 페더레이션 트러스트를 설정해야 합니다. 온-프레미스 Exchange 조직과 기타 페더레이션 Exchange 조직 간에 페더레이션 공유 기능을 구성하는 작업의 일부로 또는 하이브리드 구성 마법사를 통해 하이브리드 배포를 구성하는 작업의 일부로 페더레이션 트러스트를 직접 만들 수도 있습니다. Office 365 테넌트의 경우 Azure AD 인증 시스템과 설정한 페더레이션 트러스트는 Office 365 서비스 계정을 활성화할 때 자동으로 구성됩니다.
    
    자세한 내용은 다음을 참조하십시오. [Azure AD 인증 시스템](https://go.microsoft.com/fwlink/p/?linkid=135986)

  - **Azure Active Directory 동기화**   Azure AD 동기화는 Azure AD Connect를 사용하여 통합된 GAL(전체 주소 목록) 및 사용자 인증을 지원하도록 메일 사용이 가능한 개체에 대한 온-프레미스 Active Directory 정보를 Office 365 조직에 복제할 수 있습니다. 하이브리드 배포를 구성하는 조직에서는 Office 365를 사용하여 온-프레미스 Active Directory를 동기화하도록 Azure AD Connect를 별도 온-프레미스 서버에 배포해야 합니다.
    
    자세한 내용은 다음을 참조하십시오. [Azure AD Connect - 개요](https://go.microsoft.com/fwlink/p/?linkid=203007)

주요 용어

## 하이브리드 배포 예제

다음 시나리오를 잘 살펴보시기 바랍니다. 이는 일반적인 Exchange 2016 배포에 대한 개요를 제공하는 토폴로지 예입니다. Contoso, Ltd.는 설치된 도메인 컨트롤러 두 개와 Exchange 2016 서버 하나로 구성된 단일 포리스트의 단일 도메인 조직입니다. 원격 Contoso 사용자는 사서함을 확인하고 Outlook 일정에 액세스하기 위해 인터넷에서 웹에서 Outlook를 사용해 Exchange 2016에 연결합니다.

![Office 365를 사용한 하이브리드 배포를 구성하기 전에 온-프레미스 Exchange 배포](images/JJ200581.dad133ae-d18a-42ec-8f0a-dd1de391200e(EXCHG.150).png "Office 365를 사용한 하이브리드 배포를 구성하기 전에 온-프레미스 Exchange 배포")

Contoso의 네트워크 관리자가 하이브리드 배포 구성에 대해 알아보고 싶은 경우를 가정해 보겠습니다. 필요한 Azure AD Connect 서버를 배포 및 구성합니다. 또한 사용자가 온-프레미스 네트워크 계정과 자신의 Office 365 계정 둘 다에 대해 동일한 자격을 사용할 수 있도록 Azure AD Connect 암호 동기화 기능을 사용하기로 결정합니다. 하이브리드 배포 필수 구성 요소를 완료한 후 하이브리드 구성 마법사를 사용하여 하이브리드 배포에 대한 옵션을 선택할 수 있습니다. 새 토폴로지는 다음과 같이 구성됩니다.

  - 사용자는 온-프레미스 조직과 Exchange Online 조직에 로그온하기 위해 동일한 사용자 이름과 암호를 사용합니다("Single Sign-On").

  - 온-프레미스와 Exchange Online 조직에 있는 사용자 사서함은 동일한 전자 메일 주소 도메인을 사용합니다. 예를 들어, 온-프레미스에 있는 사서함과 Exchange Online 조직에 있는 사서함은 사용자 전자 메일 주소에 모두 @contoso.com을 사용합니다.

  - 모든 아웃바운드 메일은 온-프레미스 조직에 의해 인터넷으로 배달됩니다. 온-프레미스 조직은 모든 메시징 전송을 제어하고 Exchange Online 조직의 릴레이 역할을 합니다("중앙 집중식 메일 전송").

  - 온-프레미스와 Exchange Online 조직 사용자는 약속 있음/없음 일정 정보를 서로 공유할 수 있습니다. 두 조직에 구성된 조직 관계를 통해 크로스-프레미스 메시지 추적, 메일 설명, 메시지 검색을 할 수 있습니다.

  - 온-프레미스와 Exchange Online 사용자는 인터넷상에서 동일한 URL을 사용하여 자신의 사서함에 접속합니다.

![Office 365를 사용한 하이브리드 배포를 구성한 후에 온-프레미스 Exchange 배포](images/JJ200581.e8681849-f15d-4d0e-b77e-6105b6096c4b(EXCHG.150).png "Office 365를 사용한 하이브리드 배포를 구성한 후에 온-프레미스 Exchange 배포")

Contoso의 기존 조직 구성과 하이브리드 배포 구성을 비교해 보면 하이브리드 배포 구성에 추가 통신을 지원하는 서버와 서비스 그리고 온-프레미스 조직과 Exchange Online 조직 간에 공유되는 기능이 추가되었음을 알 수 있습니다. 다음은 하이브리드 배포가 초기 온-프레미스 Exchange 조직에서 만들어졌다는 변경에 대한 개요입니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>구성</th>
<th>혼성 배포 전</th>
<th>하이브리드 배포 후</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>사서함 위치</p></td>
<td><p>온-프레미스 사서함만 해당.</p></td>
<td><p>온-프레미스 및 Office 365의 사서함.</p></td>
</tr>
<tr class="even">
<td><p>메시지 전송</p></td>
<td><p>온-프레미스 사서함 서버는 모든 인바운드 및 아웃바운드 메시지 라우팅을 처리합니다.</p></td>
<td><p>온-프레미스 사서함 서버는 온-프레미스와 Office 365 조직 간의 내부 메시지 라우팅을 처리합니다.</p></td>
</tr>
<tr class="odd">
<td><p>웹에서 Outlook</p></td>
<td><p>온-프레미스 사서함 서버는 모든 웹에서 Outlook 요청을 수신하고 사서함 정보를 표시합니다.</p></td>
<td><p>온-프레미스 사서함 서버는 온-프레미스 Exchange 2016 사서함 서버 또는 Office 365에 로그온하는 링크 제공에 대한 웹에서 Outlook 요청을 리디렉션합니다.</p></td>
</tr>
<tr class="even">
<td><p>두 조직에 대한 통합 GAL</p></td>
<td><p>해당 없음, 단일 조직만 해당.</p></td>
<td><p>온-프레미스 Active Directory 동기화 서버는 메일 사용이 가능한 개체에 대한 Active Directory 정보를 Office 365에 복제합니다.</p></td>
</tr>
<tr class="odd">
<td><p>두 조직에 사용된 Single Sign-On</p></td>
<td><p>해당 없음, 단일 조직만 해당.</p></td>
<td><p>온-프레미스 Active Directory 및 Office 365에서 온-프레미스 또는 Office 365에 있는 사서함에 대해 동일한 사용자 이름과 암호를 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p>조직 관계 및 Azure AD 인증 시스템과의 페더레이션 트러스트가 설정됨</p></td>
<td><p>Azure AD 인증 시스템과 설정한 트러스트 관계 및 페더레이션된 다른 Exchange 조직과 맺은 조직 관계를 구성할 수 있습니다.</p></td>
<td><p>Azure AD 인증 시스템과 설정한 트러스트 관계가 필요합니다. 온-프레미스와 Office 365 간에 조직 관계가 설정됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>약속 있음/없음 공유</p></td>
<td><p>온-프레미스 사용자 간의 약속 있음/없음 공유.</p></td>
<td><p>온-프레미스 사용자와 Office 365 사용자 간의 약속 있음/없음 공유</p></td>
</tr>
</tbody>
</table>


## 하이브리드 배포를 구성하기 전에 고려해야 할 사항

하이브리드 배포가 무엇인지에 대해 어느 정도 익숙해졌으므로, 이제 몇 가지 중요한 문제에 대해 생각해봐야 합니다. 하이브리드 배포 구성은 현재 네트워크와 Exchange 조직의 여러 영역에 영향을 미칠 수 있습니다.

## 디렉터리 동기화 및 Single Sign-On

온-프레미스 및 Office 365 조직 간의 Active Directory 동기화는 Azure Active Directory Connect를 실행하는 서버에서 3시간마다 수행되며 하이브리드 배포를 구성하기 위한 요구 사항입니다. 디렉터리 동기화를 사용하면 한 조직의 받는 사람이 전체 주소 목록에서 서로 상대방을 확인할 수 있습니다. 또한 사용자 이름과 암호도 동기화하여 사용자가 Office 365와 온-프레미스 조직 모두에 동일한 자격 증명으로 로그인할 수 있습니다.


> [!NOTE]
> AD FS와 함께 Azure AD Connect를 구성하도록 선택하는 경우에도 기본적으로 온-프레미스 사용자의 사용자 이름과 암호가 Office 365에 계속 동기화됩니다. 그러나 사용자는 AD FS를 통해 온-프레미스 Active Directory에서 기본 인증 방법으로 인증하게 됩니다. 어떤 이유로 AD FS가 온-프레미스 Active Directory에 연결할 수 없는 경우 클라이언트가 Office 365에 동기화된 사용자 이름과 암호에 대한 인증 변경을 시도하게 됩니다.



Azure Active Directory 및 Office 365의 모든 고객은 기본적으로 개체 수가 50,000개(사용자, 메일 사용이 가능한 연락처 및 그룹)로 제한됩니다. 이 제한에 따라 Office 365 조직에서 만들 수 있는 개체 수가 결정됩니다. 첫 번째 도메인을 확인하면 이 개체 제한이 자동으로 300,000개 개체로 증가합니다. 도메인을 확인한 후 300,000개보다 더 많은 개체를 동기화해야 하는 경우 또는 확인할 도메인이 없고 50,000개보다 더 많은 개체를 동기화해야 하는 경우에는 Azure Active Directory 지원에 문의하여 개체 할당량 제한을 늘려 달라고 요청해야 합니다.

Azure AD Connect를 실행하는 서버뿐만 아니라 AD FS를 구성하는 경우 웹 응용 프로그램 프록시 서버를 배포하는 데에도 필요합니다. 이 서버는 경계 네트워크에 배치해야 하며 내부 Azure AD Connect 서버와 인터넷 사이의 매개 역할을 하게 됩니다. 웹 응용 프로그램 프록시 서버는 TCP 포트 443을 사용하여 인터넷의 서버와 클라이언트로부터의 연결을 수락해야 합니다.

## 하이브리드 배포 관리

Exchange 2016에서 온-프레미스 조직과 Exchange Online 조직을 모두 관리할 수 있는 단일 통합 관리 콘솔을 통해 하이브리드 배포를 관리합니다. Exchange 관리 콘솔 및 Exchange 제어판을 대신한 *EAC(Exchange 관리 센터)*를 사용하면 양 조직에 대해 연결하고 기능을 구성할 수 있습니다. 하이브리드 구성 마법사를 처음 실행하면 Exchange Online 조직에 연결하라는 메시지가 표시됩니다. EAC를 Exchange Online 조직에 연결하려면 조직 관리 역할 그룹의 구성원인 Office 365 계정을 사용해야 합니다.

## 인증서

SSL(Secure Sockets Layer) 디지털 인증서는 하이브리드 배포 구성에서 중요한 역할을 합니다. 이 디지털 인증서를 사용하면 온-프레미스 하이브리드 서버와 Exchange Online 조직 간의 통신에 대해 보안을 설정할 수 있습니다. 여러 유형의 서비스를 구성하려면 인증서가 반드시 필요합니다. Exchange 조직에서 이미 디지털 인증서를 사용하는 경우, 추가 도메인을 포함하거나 신뢰할 수 있는 인증 기관(CA)의 추가 인증서를 구매하기 위해 인증서를 수정해야 할 수도 있습니다. 인증서를 아직 사용하지 않고 있는 경우, 신뢰된 인증 기관으로부터 하나 이상의 인증서를 구매해야 합니다.

자세한 내용은 다음을 참조하십시오. [하이브리드 배포를 위한 인증서 요구 사항](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)

## 대역폭

인터넷에 대한 네트워크 연결은 온-프레미스 조직과 Office 365 조직 간의 통신 성능에 직접적으로 영향을 미칩니다. 특히 온-프레미스 Exchange 2016 서버의 사서함을 Office 365 조직으로 이동하는 경우에 그렇습니다. 사서함 크기와 이동한 사서함의 수를 모두 고려한 사용 가능한 네트워크 대역폭의 양은 사서함 이동을 완료하기 위해 다양하게 될 것입니다. 또한 SharePoint Server 2016, 비즈니스용 Skype 등의 다른 Office 365 서비스도 메시징 서비스에 대한 사용 가능 대역폭에 영향을 미칠 수 있습니다.

사서함을 Office 365로 이동하려면 먼저 다음을 수행해야 합니다.

  - Office 365로 이동할 사서함의 평균 사서함 크기를 확인합니다.

  - 온-프레미스 조직의 인터넷 연결에 대한 평균 연결 및 처리량 속도를 확인합니다.

  - 평균 예상 전송 속도를 계산하고 그에 따라 사서함 이동을 계획합니다.

자세한 내용은 다음을 참조하십시오. [네트워킹](https://go.microsoft.com/fwlink/p/?linkid=280178)

## 통합 메시징

UM(통합 메시징)은 온-프레미스와 Office 365 조직 간의 하이브리드 배포에서 지원됩니다. 온-프레미스 전화 통신 솔루션이 Office 365와 통신할 수 있어야 합니다. 이 경우 하드웨어와 소프트웨어를 추가로 구매해야 할 수 있습니다.

온-프레미스 조직에서 Office 365로 사서함을 이동하려는 경우 해당 사서함에 대해 UM이 구성되어 있으면 사서함을 이동하기 전에 하이브리드 배포에 UM을 구성해야 합니다. 하이브리드 배포에 UM을 구성하기 전에 사서함을 이동하면 사서함에서 더 이상 UM 기능에 액세스할 수 없게 됩니다.

자세한 내용은 다음을 참조하세요. [하이브리드 배포에서 통합 메시징 설정](https://go.microsoft.com/fwlink/p/?linkid=842271)

## 정보 권한 관리

IRM(정보 권한 관리)에서는 사용자가 보내는 메시지에 AD RMS(Active Directory Rights Management Services) 템플릿을 적용할 수 있습니다. AD RMS 템플릿을 사용하면 권한으로 보호된 메시지를 열 수 있는 사람과 메시지를 연 후 수행할 수 있는 작업을 사용자가 제어할 수 있으므로 정보 누출을 방지하는 데 도움이 됩니다.

하이브리드 배포에서 IRM을 사용하려면 계획 및 Office 365 조직의 수동 구성이 필요하며, 사서함이 온-프레미스에 있는지 아니면 Exchange Online 조직에 있는지에 따라 클라이언트에서 AD RMS 서버를 사용하는 방법을 이해해야 합니다.

자세한 내용은 다음을 참조하십시오. [Exchange 하이브리드 배포의 IRM](irm-in-exchange-hybrid-deployments-exchange-2013-help.md)

## 모바일 장치

모바일 장치는 하이브리드 배포에서 지원됩니다. 기존 서버에서 Exchange ActiveSync를 사용하도록 이미 설정한 경우 모바일 장치의 요청이 계속 온-프레미스 사서함 서버에 있는 사서함으로 리디렉션됩니다. 온-프레미스 조직에서 Office 365로 이동한 기존 사서함에 연결하는 모바일 장치의 경우 Exchange ActiveSync 프로필이 대다수 휴대폰에서 Office 365에 연결되도록 자동으로 업데이트됩니다. Exchange ActiveSync를 지원하는 모든 모바일 장치는 하이브리드 배포와 호환되어야 합니다.

자세한 내용은 다음을 참조하십시오. [휴대폰](https://go.microsoft.com/fwlink/p/?linkid=206387)

## 클라이언트 요구 사항

하이브리드 배포에서 최적의 환경과 성능을 보장하려면 클라이언트에서 Outlook 2016 또는 Outlook 2013을 사용하는 것이 좋습니다. Outlook 2010 이전의 클라이언트는 하이브리드 배포 또는 Office 365 서비스에서 지원되지 않습니다.

## Office 365에 대한 라이선스

Office 365에 사서함을 만들거나 Office 365로 사서함을 이동하려면 대기업용 Office 365에 등록해야 하며 사용 가능한 라이선스를 가지고 있어야 합니다. Office 365에 등록할 때 새 사서함이나 온-프레미스 조직에서 이동한 사서함에 할당할 수 있는 구체적인 라이선스 수를 받게 됩니다. Office 365의 각 사서함에 라이선스가 있어야 합니다.

## 바이러스 백신 및 스팸 방지 서비스

Office 365로 이동한 사서함의 경우 EOP(Exchange Online Protection)에서 바이러스 백신 및 스팸 방지 기능이 자동으로 제공됩니다. EOP 서비스를 통해 받는 인터넷 메일을 모두 라우팅하도록 선택한 경우 온-프레미스 사용자를 위해 추가 EOP 라이선스를 구매해야 할 수 있습니다. Office 365의 EOP 보호도 온-프레미스 조직의 바이러스 백신 및 스팸 방지 요구 사항을 충족하기에 적합한지 주의 깊게 평가하는 것이 좋습니다. 온-프레미스 조직에 대한 보호 수단이 마련되어 있는 경우 조직을 최대한 보호하도록 온-프레미스 바이러스 백신 및 스팸 방지 솔루션을 업그레이드하거나 구성해야 할 수 있습니다.

자세한 내용은 다음을 참조하십시오. [스팸 방지 및 맬웨어 방지 보호 기능](https://technet.microsoft.com/ko-kr/library/jj200731\(v=exchg.150\))

## 공용 폴더

이제 Office 365에서 공용 폴더가 지원되며, 온-프레미스 공용 폴더를 Office 365로 마이그레이션할 수 있습니다. 또한 Office 365의 공용 폴더를 온-프레미스 Exchange 2016 조직으로 이동할 수 있습니다. 온-프레미스 사용자와 Office 365 사용자 모두 웹의 Outlook, Outlook 2016, Outlook 2013, Outlook 2010 SP2 이후 버전을 사용하여 두 조직에 있는 공용 폴더에 액세스할 수 있습니다. 온-프레미스 사서함에 대한 기존 온-프레미스 공용 폴더 구성 및 액세스는 하이브리드 배포 구성 시 변경되지 않습니다.

자세한 내용은 다음을 참조하십시오. [공용 폴더](https://technet.microsoft.com/ko-kr/library/jj150538\(v=exchg.150\))

## 내게 필요한 옵션

이 검사 목록의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](https://technet.microsoft.com/ko-kr/library/jj150484\(v=exchg.150\))을 참조하세요.

## 주요 용어

다음 목록은 Exchange 2013의 하이브리드 배포와 관련된 핵심 구성 요소의 정의를 제공합니다.

  - **중앙 집중식 메일 전송**  
    모든 Exchange Online 인바운드 및 아웃바운드 인터넷 메시지가 온-프레미스 Exchange 조직을 통해 라우팅되는 하이브리드 구성 옵션입니다. 이 라우팅 옵션은 하이브리드 구성 마법사에서 구성됩니다. 자세한 내용은 [Exchange 하이브리드 배포의 전송 옵션](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md)을 참조하십시오.

<!-- end list -->

  - **동시 사용 도메인**  
    Office 365 서비스의 하이브리드 메일 흐름 및 자동 검색 요청을 위해 온-프레미스 조직에 추가된 허용 도메인입니다. 이 도메인은 하이브리드 구성 마법사에서 선택한 도메인용 *PrimarySmtpAddress* 템플릿이 있는 모든 전자 메일 주소 정책에 보조 프록시 도메인으로 추가됩니다. 기본적으로 이 도메인은 \<도메인\>.mail.onmicrosoft.com입니다.

<!-- end list -->

  - ***HybridConfiguration* Active Directory 개체**  
    하이브리드 구성 마법사에서 정한 선택에 의해 정의된 원하는 하이브리드 배포 구성 매개 변수를 포함하는 온-프레미스 조직의 Active Directory 개체 하이브리드 구성 엔진은 이러한 매개 변수를 사용하여 온-프레미스 및 Exchange Online 설정 구성 시에 하이브리드 기능을 사용할 수 있도록 합니다. 하이브리드 구성 마법사가 실행될 때마다 *HybridConfiguration* 개체의 콘텐츠가 다시 설정됩니다.

<!-- end list -->

  - **하이브리드 구성 엔진**  
    HCE(하이브리드 구성 엔진)는 하이브리드 배포 구성 및 업데이트에 필요한 주요 작업을 실행합니다. HCE는 *HybridConfiguration* Active Directory 개체의 상태와 현재 온-프레미스 Exchange 및 Exchange Online 구성 설정을 비교한 다음 *HybridConfiguration* Active Directory 개체에서 정의된 매개 변수와 배포 구성 설정을 일치시키는 작업을 실행합니다. 자세한 내용은 [하이브리드 구성 엔진](hybrid-configuration-wizard-exchange-2013-help.md)을 참조하세요.

<!-- end list -->

  - **HCW(하이브리드 구성 마법사)**  
    관리자가 온-프레미스와 Exchange Online 조직 간의 하이브리드 배포를 구성할 수 있도록 안내하는 Exchange에서 제공하는 적응 도구입니다. 마법사는 *HybridConfiguration* 개체의 하이브리드 배포 구성 매개 변수를 정의하고 하이브리드 구성 엔진이 정의된 하이브리드 기능을 사용하는 데 필요한 구성 작업을 실행하도록 지침을 제공합니다. 자세한 내용은 [하이브리드 구성 마법사](hybrid-configuration-wizard-exchange-2013-help.md)를 참조하세요.

<!-- end list -->

  - **Exchange 2010 기반 하이브리드 배포**  
    Office 365 및 Exchange Online 서비스의 연결 끝점으로 Exchange Server 2010 SP3(서비스 팩 3) 온-프레미스 서버를 사용하여 구성된 하이브리드 배포입니다. 온-프레미스 Exchange 2010, Exchange Server 2007 및 Exchange Server 2003 조직의 하이브리드 배포 옵션입니다.

<!-- end list -->

  - **Exchange 2013 기반 하이브리드 배포**  
    Office 365 및 Exchange Online 서비스의 연결 끝점으로 Exchange Server 2013 온-프레미스 서버를 사용하여 구성된 하이브리드 배포입니다. 온-프레미스 Exchange 2013, Exchange 2010 및 Exchange 2007 조직의 하이브리드 배포 옵션입니다.

<!-- end list -->

  - **Exchange 2016 기반 하이브리드 배포**  
    Office 365 및 Exchange Online 서비스의 연결 끝점으로 Exchange 2016 온-프레미스 서버를 사용하여 구성된 하이브리드 배포입니다. 온-프레미스 Exchange 2016, Exchange 2013 및 Exchange 2010 조직의 하이브리드 배포 옵션입니다.

<!-- end list -->

  - **보안 메일 전송**  
    하이브리드 배포의 자동 구성 기능으로 온-프레미스와 Exchange Online 조직 간의 보안 메시징이 가능합니다. 메시지는 하이브리드 구성 마법사에서 선택한 인증서와 함께 TLS(전송 계층 보안)를 사용하여 암호화되고 인증됩니다. Office 365 테넌트는 온-프레미스 조직에서 시작된 하이브리드 전송 연결의 끝점이자 Exchange Online에서 온-프레미스 조직으로의 하이브리드 전송 연결을 위한 소스입니다.

주요 용어

## Exchange 하이브리드 배포 설명서

다음 표에는 Microsoft Exchange에서의 하이브리드 배포에 대해 알아보고 이를 관리하는 데 도움이 될 항목에 대한 링크가 포함되어 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hybrid-configuration-wizard-exchange-2013-help.md">하이브리드 구성 마법사</a></p></td>
<td><p>하이브리드 구성 마법사 및 하이브리드 구성 엔진이 하이브리드 배포를 구성하는 방법에 대해 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployment-prerequisites-exchange-2013-help.md">하이브리드 배포 필수 구성 요소</a></p></td>
<td><p>호환되는 Exchange Server 조직, Office 365 요구 사항 및 기타 온-프레미스 구성 요구 사항을 비롯한 하이브리드 배포 선행 조건에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="certificate-requirements-for-hybrid-deployments-exchange-2013-help.md">하이브리드 배포를 위한 인증서 요구 사항</a></p></td>
<td><p>하이브리드 배포에서 디지털 인증서를 위한 요구 사항에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 하이브리드 배포의 전송 옵션</a></p></td>
<td><p>하이브리드 배포에서 인바운드 및 아웃바운드 메시지 전송 옵션에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 하이브리드 배포의 전송 라우팅</a></p></td>
<td><p>하이브리드 배포에서 인바운드 및 아웃바운드 메시지 라우팅 옵션에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 하이브리드 배포에서 하이브리드 관리</a></p></td>
<td><p>Exchange 관리 센터 및 Exchange 관리 셸로 하이브리드 배포를 관리하는 방법에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="shared-free-busy-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 하이브리드 배포에서의 공유 약속 있음/없음</a></p></td>
<td><p>하이브리드 배포에서 온-프레미스 조직과 Exchange Online 조직 간 약속 있음/없음 일정 공유에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="server-roles-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 하이브리드 배포에서의 서버 역할</a></p></td>
<td><p>하이브리드 배포에서 Exchange 서버 역할이 작동하는 방식에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="irm-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 하이브리드 배포의 IRM</a></p></td>
<td><p>하이브리드 배포에서 정보 권한 관리의 작동 방식에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="permissions-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 하이브리드 배포의 사용 권한</a></p></td>
<td><p>하이브리드 배포에서 RBAC(역할 기반 액세스 제어)를 사용하여 사용 권한을 제어하는 방식에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">하이브리드 배포의 Edge 전송 서버</a></p></td>
<td><p>Exchange Edge 전송 서버 및 하이브리드 배포에서 이러한 서버의 배포 및 운영 방식에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="single-sign-on-with-hybrid-deployments-exchange-2013-help.md">하이브리드 배포 SSO(Single Sign-On)</a></p></td>
<td><p>하이브리드 배포에서 암호 동기화 및 ADFS 기능을 사용하여 Single Sign-On하는 방식에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployment-procedures-exchange-2013-help.md">하이브리드 배포 절차</a></p></td>
<td><p>Exchange 온-프레미스 및 Exchange Online 조직에 대해 하이브리드 배포를 만들고 수정하는 절차에 대해 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2010-exchange-2013-help.md">Exchange 2013 및 Exchange 2007을 사용한 하이브리드 배포</a></p></td>
<td><p>Exchange 2007 조직에서의 Exchange 2010 기반 하이브리드 배포에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2007-exchange-2013-help.md">Exchange 2013 및 Exchange 2007을 사용한 하이브리드 배포</a></p></td>
<td><p>Exchange 2007 조직에서의 Exchange 2013 기반 하이브리드 배포에 대해 자세히 알아봅니다.</p></td>
</tr>
</tbody>
</table>


## Office 365의 새로운 기능


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning용 단축 아이콘" alt="LinkedIn Learning용 단축 아이콘" /> <strong>Office 365를 처음 사용하시나요?</strong><br />
LinkedIn Learning에서 제공하는 <a href="https://support.office.com/en-us/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>의 무료 비디오 과정을 확인해보세요.</p></td>
</tr>
</tbody>
</table>

