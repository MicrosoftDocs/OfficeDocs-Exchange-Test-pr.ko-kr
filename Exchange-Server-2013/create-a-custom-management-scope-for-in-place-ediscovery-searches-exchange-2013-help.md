---
title: '원본 위치 eDiscovery 검색의 사용자 지정 관리 범위 만들기: Exchange 2013 Help'
TOCTitle: 원본 위치 eDiscovery 검색의 사용자 지정 관리 범위 만들기
ms:assetid: 1543aefe-3709-402c-b9cd-c11fe898aad1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn741464(v=EXCHG.150)
ms:contentKeyID: 62219752
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원본 위치 eDiscovery 검색의 사용자 지정 관리 범위 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-21_

사용자 지정 관리 범위를 사용하여 특정 사람이나 그룹이 원본 위치 eDiscovery를 사용하여 Exchange 2013 또는 Exchange Online 조직에서 사서함 하위 집합을 검색하도록 할 수 있습니다. 예를 들어 검색 관리자가 특정 위치나 부서의 사용자 사서함만 검색하도록 할 수 있습니다. 이렇게 하려면 사용자 지정 관리 범위를 만듭니다. 이 사용자 지정 관리 범위는 받는 사람 필터를 사용하여 검색할 수 있는 사서함을 제어합니다. 받는 사람 필터 범위는 필터를 사용하여 받는 사람 유형 또는 기타 받는 사람 속성에 따라 특정 받는 사람을 대상으로 지정합니다.

원본 위치 eDiscovery의 경우 사용자 지정 범위에 대한 받는 사람 필터를 만드는 데 사용할 수 있는 사용자 사서함의 유일한 속성은 메일 그룹 구성원입니다(실제 속성 이름은 *MemberOfGroup*임). *CustomAttributeN*, *Department*, *PostalCode* 등의 다른 속성을 사용하는 경우 사용자 지정 범위에 할당된 역할 그룹의 구성원이 실행하는 검색은 실패합니다.

관리 범위에 대해 자세히 알아보려면 다음을 참조하세요.

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

  - [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 앞서 언급한 것처럼 eDiscovery에 사용할 사용자 지정 받는 사람 필터 범위를 만들려면 받는 사람 필터로 그룹 구성원만 사용할 수 있습니다. 다른 받는 사람 속성은 eDiscovery 검색에 대한 사용자 지정 범위를 만드는 데 사용할 수 없습니다. 동적 메일 그룹의 구성원도 이러한 작업에 사용할 수 없습니다.

  - 1~3단계를 수행하여 검색 관리자가 사용자 지정 관리 범위를 사용하는 eDiscovery 검색에 대한 검색 결과를 내보내도록 할 수 있습니다.

  - 검색 관리자가 검색 결과를 미리 볼 필요가 없으면 4단계는 건너뛰어도 됩니다.

  - 검색 관리자가 검색 결과를 복사할 필요가 없으면 5단계는 건너뛰어도 됩니다.

## 1단계: 사용자를 eDiscovery를 위한 메일 그룹으로 구성

조직에서 사서함 하위 집합을 검색하거나 검색 관리자가 검색할 수 있는 원본 사서함의 범위를 좁히려면 사서함 하위 집합을 하나 이상의 메일 그룹으로 그룹화해야 합니다. 2단계에서 사용자 지정 관리 범위를 만들 때 이러한 메일 그룹을 받는 사람 필터로 사용하여 사용자 지정 관리 범위를 만듭니다. 이를 통해 검색 관리자는 지정된 그룹의 구성원인 사용자의 사서함만 검색할 수 있습니다.

eDiscovery 용도로 기존 메일 그룹을 사용하거나 새 메일 그룹을 만들 수 있습니다. eDiscovery 검색 범위를 지정하는 데 사용할 수 있는 메일 그룹을 만드는 방법에 대한 팁은 이 항목 끝에 나오는 추가 정보를 참조하세요.

## 2단계: 사용자 지정 관리 범위 만들기

이제 메일 그룹의 구성원으로 정의된 사용자 지정 관리 범위를 만듭니다(*MemberOfGroup* 받는 사람 필터 사용). 이 범위가 eDiscovery에 사용되는 역할 그룹에 적용되면 역할 그룹의 구성원은 사용자 지정 관리 범위를 만드는 데 사용된 메일 그룹의 구성원인 사용자의 사서함을 검색할 수 있습니다.

이 절차에서는 Exchange 관리 셸 명령을 사용하여 Ottawa Users eDiscovery Scope라는 사용자 지정 범위를 만듭니다. 이렇게 하면 사용자 지정 범위의 받는 사람 필터에 대해 Ottawa Users라는 메일 그룹이 지정됩니다.

1.  이 명령을 실행하여 Ottawa Users 그룹의 속성을 가져온 후 다음 명령에 사용되는 변수에 저장합니다.
    
        $DG = Get-DistributionGroup -Identity "Ottawa Users"

2.  이 명령을 실행하여 Ottawa Users 메일 그룹의 구성원을 기반으로 사용자 지정 관리 범위를 만듭니다.
    
        New-ManagementScope "Ottawa Users eDiscovery Scope" -RecipientRestrictionFilter "MemberOfGroup -eq '$($DG.DistinguishedName)'"
    
    **$DG** 변수에 포함되어 있는 메일 그룹의 고유 이름은 새 관리 그룹에 대한 받는 사람 필터를 만드는 데 사용됩니다.

## 3단계: 관리 역할 그룹 만들기

이 단계에서는 새 관리 역할 그룹을 만든 후 2단계에서 만든 사용자 지정 범위를 할당합니다. 역할 그룹 구성원이 원본 위치 eDiscovery 검색을 수행하고 사서함에 원본 위치 유지 또는 소송 보존을 적용할 수 있도록 법적 보전 및 사서함 검색 역할을 추가합니다. 2단계에서 사용자 지정 범위를 만드는 데 사용된 메일 그룹 구성원의 사서함을 검색할 수 있도록 이 역할 그룹에 구성원을 추가할 수도 있습니다.

다음 예에서 Ottawa Users eDiscovery Managers 보안 그룹이 이 역할 그룹의 구성원으로 추가됩니다. 이 단계를 위해 셸 또는 EAC를 사용할 수 있습니다.

## 셸을 사용하여 관리 역할 그룹 만들기

이 명령을 사용하여 2단계에서 만든 사용자 지정 범위를 사용하는 새 역할 그룹을 만듭니다. 또한 이 명령은 법적 보존 및 사서함 검색 역할을 추가하고 Ottawa Users eDiscovery Managers 보안 그룹을 새 역할 그룹의 구성원으로 추가합니다.

    New-RoleGroup "Ottawa Discovery Management" -Roles "Mailbox Search","Legal Hold" -CustomRecipientWriteScope "Ottawa Users eDiscovery Scope" -Members "Ottawa Users eDiscovery Managers"

## EAC를 사용하여 관리 역할 그룹 만들기

1.  EAC에서 **사용 권한** \> **관리자 역할**로 이동한 후 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 역할 그룹**에서 다음 정보가 제공됩니다.
    
      - **이름**   새 역할 그룹을 설명하는 이름이 제공됩니다. 예를 들어 **Ottawa Discovery Management**를 사용합니다.
    
      - **쓰기 범위**   2단계에서 만든 사용자 지정 관리 범위를 선택합니다. 이 범위는 새 역할 그룹에 적용됩니다.
    
      - **역할**   **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하고 새 역할 그룹에 **법적 보존** 및 **사서함 검색** 역할을 추가합니다.
    
      - **구성원**   **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하고 새 역할 그룹의 구성원으로 추가할 사용자, 보안 그룹 또는 역할 그룹을 선택합니다. 이 예에서 **Ottawa Users eDiscovery Managers** 보안 그룹의 구성원은 **Ottawa Users** 메일 그룹의 구성원인 사용자의 사서함만 검색할 수 있습니다.

3.  **저장**을 클릭하여 역할 그룹을 만듭니다.
    
    다음은 작업을 완료했을 때 **새 역할 그룹** 창 모습의 예입니다.
    
    ![사용자 지정 범위에 대한 새 역할 그룹 만들기](images/Dn741464.a6e3419f-d5d9-404f-890d-ad35f499756f(EXCHG.150).gif "사용자 지정 범위에 대한 새 역할 그룹 만들기")  

## (옵션) 4단계: 검색 관리자를 사용자 지정 관리 범위를 만드는 데 사용되는 메일 그룹의 구성원으로 추가

검색 관리자가 eDiscovery 검색 결과를 미리 볼 수 있도록 하려는 경우에만 이 단계를 수행합니다.

이 명령을 실행하여 Ottawa Users eDiscovery Managers 보안 그룹을 Ottawa Users 메일 그룹의 구성원으로 추가합니다.

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Users eDiscovery Managers"

EAC를 사용하여 메일 그룹에 구성원을 추가할 수도 있습니다. 자세한 내용은 [메일 그룹 만들기 및 관리](create-and-manage-distribution-groups-exchange-2013-help.md)를 참조하세요.

## (옵션) 5단계: 검색 사서함을 사용자 지정 관리 범위를 만드는 데 사용되는 메일 그룹의 구성원으로 추가

검색 관리자가 eDiscovery 검색 결과를 복사할 수 있도록 하려는 경우에만 이 단계를 수행합니다.

이 명령을 실행하여 Ottawa Discovery Mailbox이라는 검색 사서함을 Ottawa Users 메일 그룹의 구성원으로 추가합니다.

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Discovery Mailbox"


> [!NOTE]
> 검색 사서함을 열고 검색 결과를 보려면 검색 관리자에게 검색 사서함에 대한 모든 액세스 권한이 지정되어야 합니다. 자세한 내용은 <A href="create-a-discovery-mailbox-exchange-2013-help.md">검색 사서함 만들기</A>를 참조하세요.



## 작동 여부는 어떻게 확인합니까?

다음은 eDiscovery에 대한 사용자 지정 관리 범위를 성공적으로 구현했는지 확인하는 몇 가지 방법입니다. 확인 시 eDiscovery 검색을 실행하는 사용자가 사용자 지정 관리 범위를 사용하는 역할 그룹의 구성원인지 확인합니다.

  - eDiscovery 검색을 만들고, 사용자 지정 관리 범위를 검색할 사서함의 원본으로 만드는 데 사용된 메일 그룹을 선택합니다. 모든 사서함을 검색할 수 있어야 합니다.

  - eDiscovery 검색을 만들고 사용자 지정 관리 범위를 만드는 데 사용한 메일 그룹의 구성원이 아닌 사용자의 사서함을 검색합니다. 검색 관리자가 사용자 지정 관리 그룹을 만드는 데 사용된 메일 그룹의 구성원인 사용자의 사서함만 검색할 수 있으므로 이 검색은 실패합니다. 이 경우 "현재 사용자에게 사서함에 액세스할 수 있는 권한이 없으므로 \<*사서함 이름*\> 사서함을 검색할 수 없습니다"와 같은 오류 메시지가 반환됩니다.

  - eDiscovery 검색을 만들고 사용자 지정 관리 범위를 만드는 데 사용한 메일 그룹의 구성원인 사용자의 사서함을 검색합니다. 같은 검색에 구성원이 아닌 사용자의 사서함을 포함합니다. 검색이 부분적으로 수행됩니다. 사용자 지정 관리 범위를 만드는 데 사용된 메일 그룹의 구성원 사서함이 검색됩니다. 그룹의 구성원이 아닌 사용자의 사서함 검색은 실패합니다.

## 추가 정보

  - 메일 그룹은 이 시나리오에서 메시지 배달이 아니라 eDiscovery 검색의 범위를 지정하기 위해 사용되므로 eDiscovery를 위해 메일 그룹을 만들고 구성할 때는 다음을 고려하세요.
    
      - 그룹 소유자만 그룹에서 구성원을 추가 또는 제거할 수 있도록 구성원이 차단된 메일 그룹을 만듭니다. 셸에서 그룹을 만드는 경우에는 `MemberJoinRestriction closed` 및 `MemberDepartRestriction closed` 구문을 사용합니다.
    
      - 그룹으로 전송된 메시지가 그룹 중재에 따라 메시지를 승인 또는 거부할 수 있는 그룹 중재자에게 먼저 전송되도록 그룹 중재를 사용하도록 설정합니다. 셸에서 그룹을 만드는 경우에는 `ModerationEnabled $true` 구문을 사용합니다. EAC를 사용하는 경우 그룹이 만들어진 후에 중재를 사용하도록 설정할 수 있습니다.
    
      - 조직의 공유 주소록에서 메일 그룹을 숨깁니다. 그룹이 만들어진 후에 EAC 또는 **Set-DistributionGroup** cmdlet을 사용합니다. 셸을 사용하는 경우 `HiddenFromAddressListsEnabled $true` 구문을 사용합니다.
    
    다음 예에서 첫 번째 명령은 중재를 사용하도록 설정하고 차단된 구성원을 사용하여 메일 그룹을 만듭니다. 두 번째 명령은 공유 주소록에서 그룹을 숨깁니다.
    
        New-DistributionGroup -Name "Vancouver Users eDiscovery Scope" -Alias VancouverUserseDiscovery -MemberJoinRestriction closed -MemberDepartRestriction closed -ModerationEnabled $true
    
        Set-DistributionGroup "Vancouver Users eDiscovery Scope" -HiddenFromAddressListsEnabled $true
    
    메일 그룹을 만들고 관리하는 방법에 대한 자세한 내용은 [메일 그룹 만들기 및 관리](create-and-manage-distribution-groups-exchange-2013-help.md)를 참조하세요.

  - eDiscovery에 사용되는 사용자 지정 관리 범위에 대한 받는 사람 필터로 메일 그룹 구성원만 사용할 수 있지만 다른 받는 사람 속성을 사용하여 해당 메일 그룹에 사용자를 추가할 수 있습니다. 다음은 **Get-Mailbox** 및 **Get-Recipient** cmdlet을 사용하여 일반 사용자 또는 사서함 특성에 따라 특정 사용자 그룹을 반환하는 방법의 예입니다.
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "VancouverSubsidiary"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -OrganizationalUnit "namsr01a002.sdf.exchangelabs.com/Microsoft Exchange Hosted Organizations/contoso.onmicrosoft.com"

  - 그 다음 이전 글머리 기호 목록에 나온 예를 사용하여 사용자 그룹을 메일 그룹에 추가하기 위해 **Add-DistributionGroupMember** cmdlet과 함께 사용할 수 있는 변수를 만들 수 있습니다. 다음 예에서 첫 번째 명령은 해당 사용자 계정에 *Department* 속성 값으로 **Vancouver**를 갖는 모든 사용자 사서함이 포함된 변수를 만듭니다. 두 번째 명령은 이러한 사용자를 Vancouver Users 메일 그룹에 추가합니다.
    
        $members = Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "Vancouver"'
    
        $members | ForEach {Add-DistributionGroupMember "Ottawa Users" -Member $_.Name}

  - **Add-RoleGroupMember** cmdlet을 사용하여 eDiscovery 검색 범위를 지정하는 데 사용되는 기존 역할 그룹에 구성원을 추가할 수 있습니다. 예를 들어 다음 명령은 Ottawa Discovery Management 역할 그룹에 사용자 admin@ottawa.contoso.com을 추가합니다.
    
        Add-RoleGroupMember "Vancouver Discovery Management" -Member paralegal@vancouver.contoso.com
    
    EAC를 사용 하 여 역할 그룹에 구성원을 추가 하 수도 있습니다. 자세한 내용은 [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)의 "역할 그룹에 구성원 추가" 섹션을 참조 하십시오.

  - Exchange Online 비활성 사서함을 검색할 수 eDiscovery에 사용 되는 사용자 지정 관리 범위를 사용할 수 없습니다. 비활성 사서함이 있는 메일 그룹의 구성원 일 수 없으므로입니다. 예, 사용자 eDiscovery에 대 한 사용자 지정 관리 범위를 만들 때 사용한 메일 그룹의 구성원 인지 가정해 보겠습니다. 그런 다음 해당 사용자가 조직을 떠날 하 고 해당 사서함이 수행한 비활성 (소송 보존으로 설정 또는 전체 사서함 보존에 배치 하 고 해당 Office 365 사용자 계정을 삭제). 결과 사용자가 eDiscovery에 사용 되는 사용자 지정 관리 범위를 만드는데 사용 된 그룹을 포함 하 여 모든 메일 그룹의 구성원으로 제거 됩니다. 하는 경우 (인, 사용자 지정 관리 범위에 할당 된 역할 그룹의 구성원) 검색 관리자가 비활성 사서함 검색을 검색을 시도 실패 합니다. 비활성 사서함을 검색 하려면 검색 관리자는 검색 관리 역할 그룹 또는 전체 조직 검색에 사용 권한이 있는 모든 역할 그룹의 구성원 이어야 합니다.
    
    비활성 사서함에 대 한 자세한 내용은 [Exchange Online에서 비활성 사서함](https://technet.microsoft.com/ko-kr/library/dn798632\(v=exchg.150\))을 참조 하십시오.

