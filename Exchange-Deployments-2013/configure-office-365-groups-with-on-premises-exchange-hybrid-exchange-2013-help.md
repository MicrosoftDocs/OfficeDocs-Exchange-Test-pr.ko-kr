---
title: '온-프레미스 Exchange 하이브리드로 Office 365의 그룹을 구성합니다.: Exchange 2013 Help'
TOCTitle: 온-프레미스 Exchange 하이브리드로 Office 365의 그룹을 구성합니다.
ms:assetid: 184dfcfe-4b8e-450a-adc6-e647213b9501
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt668829(v=EXCHG.150)
ms:contentKeyID: 72513073
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 온-프레미스 Exchange 하이브리드로 Office 365의 그룹을 구성합니다.

 

_**마지막으로 수정된 항목:** 2016-12-06_

하이브리드 배포에서 Office 365 그룹을 사용하기 위해 온-프레미스 Exchange 사용자를 사용하도록 설정하는 방법을 알아보세요.

그룹은 팀에서 커뮤니케이션, 모임 예약 및 문서 공동 작업을 보다 원활하게 수행할 수 있도록 하는 Office 365 서비스입니다. 그룹을 통해 그룹으로 전송된 전자 메일 메시지부터 그룹의 비즈니스용 OneDrive 또는 SharePoint 라이브러리에 저장된 파일로 공유되는 모든 정보는 그룹의 모든 구성원이 사용할 수 있습니다. Office 365와 온-프레미스 Exchange 조직 간에 하이브리드 배포를 구성한 경우 이 항목의 단계를 수행하여 Office 365에서 만든 그룹을 온-프레미스 사용자가 사용하도록 할 수 있습니다.


> [!IMPORTANT]
> Exchange 하이브리드 배포에서는 온-프레미스 사용자와 함께 Office 365 그룹을 사용하는 것은 새로운 기능입니다. 새로운 기능이기 때문에 설정할 때 몇 가지 문제가 발생할 수 있습니다. 발생할 수 있는 문제의 해결 방법을 보려면 이 항목 끝부분에 나오는 알려진 문제 섹션을 확인하세요.



## 필수 구성 요소

시작하기 전에 다음을 수행했는지 확인합니다.

  - 테넌트에 대한 Azure Active Directory 프리미엄 라이선스를 구매했습니다. Azure Active Directory Connect에서 그룹 쓰기 저장 기능을 사용하도록 설정하는 데 필요합니다.

  - Exchange 온-프레미스 조직과 Office 365 간에 하이브리드 배포를 구성했으며 제대로 작동하는지 확인했습니다. Exchange 하이브리드 배포에 대한 자세한 내용은 다음을 참조하세요.
    
      - [Exchange Server 하이브리드 배포](exchange-server-hybrid-deployments-exchange-2013-help.md)
    
      - [하이브리드 배포 필수 구성 요소](hybrid-deployment-prerequisites-exchange-2013-help.md)

  - 설치된 지원되는 버전의 온-프레미스 Exchange와 Office 365 그룹과의 통합은 CU1 및 최신 Exchange 2016 릴리스, CU11 및 최신 Exchange 2013 릴리스에서 사용할 수 있습니다. 그러나 Exchange 하이브리드를 사용하려면 온-프레미스 Exchange 서버에 최신 Exchange 2013 또는 Exchange 2016 CU(누적 업데이트)를 설치해야 합니다. 최신 CU를 설치할 수 없는 경우 현재 CU 직전에 출시된 업데이트를 사용할 수 있습니다.

  - Azure AD Connect(Azure Active Directory Connect)를 사용하여 구성된 Single Sign-On입니다. 사용자가 그룹 전자 메일 메시지의 클라우드 첨부 파일 링크 또는 **그룹 파일 보기**에서 클릭할 수 있도록 하려면 필요합니다.
    
    Exchange 하이브리드 배포에서 Single Sign-On에 대해 Azure AD Connect를 구성하는 경우 암호 동기화를 사용하는 것이 좋습니다. AD FS(Active Directory Federation Services)는 사용자가 큰 조직에 소속된 경우, 복잡한 온-프레미스 Active Directory 배포를 가지고 있는 경우(예: 여러 Active Directory 포리스트), Office 365로 작업하는 데 다른 Microsoft 제품에 AD FS가 필요한 경우 또는 준수 정책으로 인해 온-프레미스 네트워크 외부에서 암호를 동기화할 수 없는 경우에만 사용해야 합니다. Single Sign-On에 대한 자세한 내용은 [Azure Active Directory로 온-프레미스 ID 통합](http://go.microsoft.com/fwlink/p/?linkid=723513)을 참조하세요.

## Azure AD Connect에서 그룹 쓰기 저장 사용

1.  Azure AD Connect 마법사에서 **동기화 옵션 사용자 지정다음**을 클릭합니다.

2.  **Azure AD에 연결** 페이지에서 Office 365 및 온-프레미스 자격 증명을 입력합니다. **다음**을 클릭합니다.

3.  **선택적 기능** 페이지에서 이전에 구성한 옵션이 계속 선택되어 있는지 확인합니다. 가장 일반적으로 선택되는 옵션은 **Exchange 하이브리드** 및 **암호 해시 동기화**입니다.

4.  **그룹 쓰기 저장** 을 선택하고 **다음**을 클릭합니다.

5.  **쓰기 저장** 페이지에서 Office 365에서 온-프레미스 조직과 동기화되는 개체를 저장하는 Active Directory OU(조직 구성 단위)의 위치를 선택하고 **다음**을 클릭합니다.

6.  **구성 준비 완료** 페이지에서 **구성**을 클릭합니다.

7.  마법사가 완료되면 **구성 완료** 페이지에서 **끝내기**를 클릭합니다.

8.  Active Directory 도메인 컨트롤러에서 Active Directory 사용자 및 컴퓨터를 열고 **AAD\_**로 시작하는 사용자를 찾습니다. 이 계정의 이름을 적어 둡니다.

9.  온-프레미스 Exchange Server에서 Exchange 관리 셸을 열고 다음 명령을 실행합니다.
    
        $AzureADConnectSWritebackAccount = <AAD_ account name from step 8>
        
        $GroupsOU = <writeback Active Directory OU selected in step 5>
        
        Import-Module "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1"
        
        Initialize-ADSyncGroupWriteBack -ADConnectorAccount $AzureADConnectSWritebackAccount -GroupWriteBackContainerDN $GroupsOU

## 그룹 도메인 구성

Office 365 그룹의 기본 SMTP 도메인은 *그룹 도메인*이라고 합니다. 기본적으로 조직의 기본 허용 도메인은 그룹 도메인으로 선택되어 있습니다. 전용 그룹 도메인을 추가하려는 경우 다음 단계를 수행하여 도메인을 추가할 수 있습니다. Office 365 그룹의 다중 도메인 지원에 대한 자세한 내용은 [Office 365 그룹에 대한 다중 도메인 지원](https://support.office.com/en-us/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)을 참조하세요.

1.  Office 365 조직에 새 도메인을 추가합니다. Office 365에 도메인을 추가하는 데 도움이 필요한 경우 [Office 365에 사용자 및 도메인 추가](https://support.office.com/en-us/article/add-users-and-domain-to-office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611?ui=en-us%26rs=en-us%26ad=us)를 참조하세요.

2.  다음 명령을 사용하여 해당 그룹 도메인을 온-프레미스 Exchange 조직의 허용 도메인으로 추가합니다. 이 작업은 하이브리드 송신 커넥터를 사용하여 Office 365의 그룹 도메인으로 아웃바운드 메일을 배달하는 데 필요합니다.
    
        New-AcceptedDomain -Name groups.contoso.com -DomainName groups.contoso.com -DomainType InternalRelay

3.  DNS 공급자와 함께 다음 공용 DNS 레코드를 만듭니다.
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>DNS 레코드 이름</p></th>
    <th><p>DNS 레코드 형식</p></th>
    <th><p>DNS 레코드 값</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>groups.contoso.com</p></td>
    <td><p>MX</p></td>
    <td><p>groups-contoso-com.mail.protection.outlook.com</p>

    > [!NOTE]
    > 이 DNS 레코드 값의 형식은 <EM>&lt;domain key&gt;</EM>.mail.protection.outlook.com입니다. 도메인 키를 알아보려면 <A href="https://support.office.com/en-us/article/gather-the-information-you-need-to-create-office-365-dns-records-77f90d4a-dc7f-4f09-8972-c1b03ea85a67?ui=en-us%26rs=en-us%26ad=us">Office 365 DNS 레코드를 만드는 데 필요한 정보 수집</A> 문서를 참조하세요.


</td>
    </tr>
    <tr class="even">
    <td><p>autodiscover.groups.contoso.com</p></td>
    <td><p>CNAME</p></td>
    <td><p>autodiscover.outlook.com</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!WARNING]
    > 그룹 도메인의 MX DNS 레코드가 온-프레미스 Exchange 서버로 설정되어 있으면 온-프레미스 Exchange 조직의 사용자와 Office 365 그룹 간의 메일 흐름이 제대로 작동하지 않습니다.



4.  다음 명령을 사용하여 온-프레미스 Exchange 조직에서 하이브리드 구성 마법사로 만든 하이브리드 송신 커넥터에 그룹 도메인을 추가합니다.
    
        Set-SendConnector -Identity "Outbound to Office 365" -AddressSpaces "contoso.mail.onmicrosoft.com","groups.contoso.com"
    

    > [!NOTE]
    > 송신 커넥터가 업데이트되지 않거나 그룹 도메인이 온-프레미스 Exchange 조직의 허용 도메인으로 추가되지 않으면, 해당 그룹이 외부 보낸 사람의 메일을 받도록 구성되지 않는 한, 온-프레미스 사서함에서 보낸 메일이 그룹으로 전달되지 않습니다.



## 작동 여부는 어떻게 확인합니까?

그룹이 Exchange 하이브리드 배포를 사용하는지 확인하려면 온-프레미스 사서함 및 온-프레미스 조직에서 Office 365로 이동된 사서함을 사용하여 테스트해야 합니다. 다음 섹션의 단계에 따라 각 테스트를 수행합니다.

## 온-프레미스 사서함을 사용하여 테스트

1.  온-프레미스 사서함을 Office 365 그룹에 추가합니다.

2.  Office 365 사서함을 동일한 Office 365 그룹에 추가합니다.

3.  웹용 Outlook을 사용하여 Office 365 사서함에 로그인합니다.

4.  Office 365 사서함을 사용하여 그룹에 메시지를 게시합니다.

5.  Outlook 2016 또는 웹용 Outlook을 사용하여 온-프레미스 사서함을 엽니다.

6.  사서함에 Office 365 그룹으로 전송한 게시물이 들어 있는 전자 메일 메시지가 수신되었는지 확인합니다.

7.  동일한 사서함에서 메시지 회신을 작성하고 그룹으로 보냅니다.

8.  그룹의 모든 구성원이 메시지를 볼 수 있는지 확인합니다.

## Office 365로 이동된 사서함을 사용하여 테스트

1.  온-프레미스 Exchange 조직에서 Office 365로 사서함을 이동합니다.

2.  Office 365 그룹에 사서함을 추가합니다.

3.  새 브라우저 세션에서 Office 365로 이동된 사서함에 로그인합니다.

4.  웹용 Outlook에서 그룹이 왼쪽 탐색 모음에 나열되는지 확인합니다.

5.  그룹에 메시지를 게시합니다.

6.  그룹의 모든 구성원이 메시지를 볼 수 있는지 확인합니다.

## 알려진 문제

  - **그룹이 Office 365로 이동된 사서함에 나타나지 않음** 사용자가 온-프레미스 Exchange 조직에서 Office 365로 이동된 경우 Outlook이나 웹용 Outlook의 왼쪽 탐색 창에 그룹이 나타나지 않습니다. 이 문제를 해결하려면 사서함이 소속된 그룹에서 해당 사서함을 제거한 후 각 그룹에 다시 추가합니다.

  - **새 그룹이 온-프레미스 Exchange GAL(전체 주소 목록)에 표시되지 않음** Office 365에서 새 그룹을 만든 경우 온-프레미스 GAL에 자동으로 나타나지 않습니다. 이 문제를 해결하려면 온-프레미스 Exchange 서버에서 Exchange 관리 셸을 열고 다음 명령을 실행합니다.
    
        Update-Recipient "<group name>"

  - **그룹이 온-프레미스 사용자가 보낸 메시지를 수신하지 않음** 온-프레미스 사용자가 다음과 같은 경우에 Office 365 그룹으로 메일을 보낼 수 없습니다.
    
      - 그룹 도메인은 온-프레미스 Exchange 조직에서 신뢰할 수 있는 도메인으로 구성됩니다.
    
      - 그룹이 최근에 생성되었으며 해당 정보가 온-프레미스 Active Directory에 아직 기록되지 않았습니다.
    
    이 문제는 Azure AD Connect가 다음에 Office 365와 온-프레미스 조직 간에 동기화를 수행하면 자체적으로 해결됩니다. Azure Connect AD 동기화는 기본적으로 30분마다 발생합니다.

  - **온-프레미스 사용자가 그룹 메시지 바닥글에 포함된 링크를 사용할 수 없음**온-프레미스 사용자가 전송된 각 그룹 메시지의 바닥글에 포함된 **그룹 대화 보기** 또는 **구독 취소** 링크를 사용할 수 없습니다. 그룹에서 구독을 취소하려면 온-프레미스 사용자는 그룹 관리자에게 문의해야 합니다.

  - **그룹의 보조 SMTP 주소로 전송된 메일이 배달되지 못함** 여러 개의 전자 메일 주소를 그룹에 추가하면 기본 SMTP 주소만 온-프레미스 Active Directory에 다시 기록됩니다. 온-프레미스 사용자가 그룹의 보조 SMTP 주소로 메시지를 보내려고 시도할 경우 메시지가 배달되지 못합니다. 이 문제를 방지하려면 각 그룹에서 1개의 SMTP 주소만 구성합니다.

  - **온-프레미스 사용자가 그룹의 관리자가 될 수 없음** 온-프레미스 사용자는 그룹 공간에 직접 액세스할 수 없습니다. 따라서 그룹의 관리자로 추가할 수 없습니다.

  - **중앙 집중식 메일 흐름을 사용하도록 설정한 경우 외부 메일을 그룹에 배달할 수 없음** 중앙 집중식 메일 흐름을 사용하도록 설정한 경우 외부 사용자가 보낸 메일을 그룹에 배달할 수 없으며, 그룹이 외부 보낸 사람의 메일도 허용합니다.

  - **온-프레미스 사용자가 그룹으로 메일을 보낼 수 없음** 메시지를 Office 365 그룹으로 보내려는 온-프레미스 사용자가 그룹의 다른 사람 이름으로 보내기 권한을 받은 경우에도 권한 거부 오류를 받습니다. 그룹의 다른 사람 이름으로 보내기 권한은 Exchange Online 사서함 사용자에 대해서만 작동합니다.

  - **Outlook의 왼쪽 탐색 창에서 그룹을 선택하면 그룹의 사서함이 열리지 않음** 그룹 사서함을 열기 위해 Outlook에서 자동 검색 URL을 사용합니다. 그룹의 기본 전자 메일 주소가 Office 365의 자동 검색 URL(autodiscover.outlook.com)을 가리키지 않는 도메인에 있으므로 Outlook에서 그룹의 사서함을 열 수 없습니다. 이 문제를 해결하려면 Office 365의 자동 검색 URL을 가리키는 도메인의 기본 주소를 사용하여 그룹을 제공하면 됩니다. 전자 메일 주소 정책을 구성하여 Office 365의 자동 검색 URL을 가리키는 각 그룹 사서함의 기본 전자 메일 주소를 추가할 수 있습니다. 자세한 내용은 [Office 365 그룹에 대한 다중 도메인 지원](https://support.office.com/en-us/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)을 참조하세요.

