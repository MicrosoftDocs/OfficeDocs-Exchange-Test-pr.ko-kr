---
title: '분할 권한 이해: Exchange 2013 Help'
TOCTitle: 분할 권한 이해
ms:assetid: 2b709e15-63a2-4841-94bc-b289b71166d0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638106(v=EXCHG.150)
ms:contentKeyID: 50482699
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 분할 권한 이해

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-07_

Microsoft Exchange Server 2013 개체 및 Active Directory 개체의 관리를 구분 하는 조직은 *분할 권한* 모델 이라는 것을 사용 합니다. 분할 권한이 있는 조직에서 조직 내에서 특정 그룹에 특정 사용 권한 및 관련된 작업을 할당할 수 있습니다. 이렇게이 분리 된 작업의 표준 및 워크플로, 유지 관리 하는 데 도움이 및 조직에서 변경 제어 하는 데 도움이 됩니다.

가장 높은 분할 된 사용 권한 수준은 Exchange 관리 및 Active Directory 관리의 분리 합니다. 많은 조직에는 두 그룹: 서버 및 받는 사람을 포함 하 여 조직의 Exchange 인프라를 관리 하는 관리자 및 Active Directory 인프라를 관리 하는 관리자입니다. Active Directory 인프라 종종에 걸쳐 많은 위치, 도메인, 서비스, 응용 프로그램을 Active Directory 포리스트도 하기 때문에 대부분의 조직에 대 한 중요 한 분리입니다. Active Directory 관리자 Active Directory 에 대 한 변경 내용을 다른 서비스에 부정적인 영향 하지 확인 해야 합니다. 결과적으로, 일반적으로 해당 인프라를 관리 하려면 소규모의 관리자만 허용 됩니다.

같은 시간에 Exchange, 서버 및 받는 사람을 포함 하 여에 대 한 인프라는 복잡 해질 및 전문된 지식이 요구도 수 있습니다. 또한 Exchange 는 조직의 비즈니스에 대 한 매우 기밀 정보를 저장합니다. Exchange 관리자가이 정보에 액세스할 가능성이 수 있습니다. Exchange 관리자의 수를 제한 하 여 조직 Exchange 구성을 변경할 수 있는 사용자 및 중요 한 정보에 액세스할 수 있는 사용자를 제한 합니다.

분할 된 사용 권한을 검색할 Active Directory, 사용자 및 보안 그룹 및 해당 개체의 후속 구성 등의 보안 주체를 만들 때 일반적으로 확인 하십시오. 이에 대 한 액세스 권한을 부여 하는 개체를 만들 수 있는 사용자를 제어 하 여 네트워크에 무단으로 액세스 가능성을 줄일 수는 있습니다. 대부분의 자주 유일한 Active Directory 관리자가 Exchange 관리자와 같은 다른 관리자 하는 동안 보안 주체를 만들 수, 기존 Active Directory 개체의 특정 특성을 관리할 수 있습니다.

Exchange 2013 는 별도의 Exchange 및 Active Directory 관리를 다양 한 요구를 지원 하기 위해 공유 사용 권한 모델 또는 분할 권한 모델을 지정할지를 선택할 수 있습니다. 두 유형의 분할 권한 모델을 제공 하는 Exchange 2013: RBAC 및 Active Directory 합니다. Exchange 2013 공유 사용 권한 모델을 기본값으로 사용 됩니다.

**목차**

설명은 역할 기반 액세스 제어 및 Active Directory

공유 권한

분할 된 사용 권한

RBAC 분할 사용 권한

Active Directory 분할 사용 권한

## 설명은 역할 기반 액세스 제어 및 Active Directory


분할 된 사용 권한을 이해 하려면 Active Directory 와 Exchange 2013 에 대 한 액세스 제어 RBAC (역할 기반) 사용 권한 모델의 작동 방식을 이해 해야 합니다. RBAC 모델 컨트롤 어떤 작업을 수행할 수 있는 되며 어떤 개체에 대해 이러한 작업을 수행할 수 있습니다. 이 항목에서 설명 하는 RBAC의 다양 한 구성 요소에 대 한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)을 참조 하십시오.

Exchange 2013 Exchange 관리 셸 또는 Exchange 관리 센터 (EAC) 인터페이스를 통해 Exchange 개체에서 수행 하는 모든 작업을 수행 해야 합니다. 이러한 관리 도구를 모두 RBAC를 사용 하 여 수행 하는 모든 작업에 권한을 부여 합니다.

RBAC는 Exchange 2013 를 실행 하는 모든 서버에 있는 구성 요소입니다. RBAC 그렇게 작업을 수행 하는 사용자 권한이 있는지 여부를 확인 합니다.

  - 사용자는 작업을 수행 하도록 허용 되지 않습니다, RBAC를 계속 하려면 매크로 함수를 허용 하지 않습니다.

  - 사용자에 게 작업을 수행 하려면 권한이 있으면 RBAC 사용자가 요청 되는 특정 개체에 대 한 작업을 수행할 수 있는 권한이 있는지 확인 합니다.
    
      - 사용자에 게 권한이 있으면 RBAC를 계속 하려면 작업을 허용 합니다.
    
      - 사용자에 게 권한이 없는, RBAC를 계속 하려면 매크로 함수를 허용 하지 않습니다.

RBAC 작업 진행을 허용 하는 경우 Exchange 신뢰할 수 있는 하위 시스템 컨텍스트 및 하지는 사용자의 상황에 맞는 작업이 수행 됩니다. Exchange 신뢰할 수 있는 하위 시스템 모든 Exchange 에 대 한 읽기/쓰기 권한이 있는 권한이 높은 유니버설 보안 그룹 (USG)- Exchange 조직에서 관련된 개체입니다. 관리자가 로컬 보안 그룹 및 ExchangeExchange 를 만들고 Active Directory 개체를 관리할 수 있는 Windows 사용 권한 USG 구성원 이기도 합니다.


> [!WARNING]
> 변경 하지 않은 수동 Exchange 신뢰할 수 있는 하위 시스템 보안 그룹의 구성원에 게 있습니다. 또한 하지 패키지를 추가 하거나 개체 액세스 제어 목록 (Acl)에서 제거 합니다. 변경 Exchange 신뢰할 수 있는 하위 시스템 USG 사용자가 직접 작업을 수행 하 여 Exchange 조직에 복구할 수 없는 손상이 발생할 수 있습니다.



것은 사용자가 Exchange 관리 도구를 사용 하는 경우 Active Directory 사용 권한을 상관이 이해 하는 것이 중요 합니다. RBAC를 통해 사용자가 승인 하는 경우 Exchange 관리 도구에서 작업을 수행 하는 사용자 작업을 수행할 수가 자신의 Active Directory 사용 권한과 상관 합니다. 이와 반대로 사용자 Active Directory 에 엔터프라이즈 관리자가 하 고 관리 도구, Exchange 에 사서함을 만드는 등의 작업을 수행할 수 있는 권한이 없습니다 RBAC에 따라 필요한 사용 권한 권한이 없습니다. 작업이 성공 하지 않습니다.


> [!IMPORTANT]
> RBAC 권한 모델 Active Directory 사용자 및 컴퓨터 관리 도구에 적용 되지 않습니다, 하지만 Active Directory 사용자 및 컴퓨터 Exchange 구성을 관리할 수 없습니다. 따라서 사용자는 사용자의 표시 이름 등의 Active Directory 개체의 일부 특성 수정에 대 한 액세스를 있을 수 있지만 사용자 Exchange 관리 도구를 사용 해야 및 따라서 해야 의해 권한이 부여 되어야 RBAC, Exchange 속성을 관리 합니다.



맨 위로 이동

## 공유 권한

공유 사용 권한 모델은 Exchange 2013 에 대 한 기본 모델입니다. 이 사용 권한 모델을 사용 하려는 경우 아무것도 변경 하지 않아도 됩니다. 이 모델 Exchange 관리 도구를 사용 하는 내에서 Exchange 및 Active Directory 개체의 관리를 구분 하지 않습니다. 관리자가 Exchange 관리 도구를 사용 하 여 Active Directory 에서 보안 주체를 만들 수 있도록 합니다.

다음 표에서 Exchange 및 기본적으로 할당 하는 관리 역할 그룹의 보안 주체를 만들 수 있도록 하는 역할을 보여줍니다.

### 보안 계정 관리 역할

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>관리 역할</th>
<th>역할 그룹</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Mail Recipient Creation 역할</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">보안 그룹 만들기 및 멤버 자격 역할</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
</tbody>
</table>


역할 그룹, 사용자 또는 Usg Mail Recipient Creation 역할에 할당 된 Active Directory 사용자와 같은 보안 주체를 만들 수 있습니다. 기본적으로 조직 관리 및 Recipient Management 역할 그룹에는이 역할에 할당 됩니다. 따라서 이러한 역할 그룹의 구성원 보안 주체를 만들 수 있습니다.

역할 그룹, 사용자 또는 Usg의 보안 그룹 만들기 및 멤버 자격 역할에 할당 된 보안 그룹을 만들 하거나 자신의 구성원 자격을 관리할 수 있습니다. 기본적으로 조직 관리 역할 그룹에만이 역할을 할당 됩니다. 따라서 조직 관리 역할 그룹의 구성원만 만들거나 보안 그룹의 구성원 자격을 관리할 수 있습니다.

다른 사용자가 보안 주체를 만들 수 있도록 하려는 경우 다른 역할 그룹, 사용자 또는 Usg를 Mail Recipient Creation 역할 및 보안 그룹 만들기 및 멤버 자격 역할을 할당할 수 있습니다.

Exchange 2013 에서 기존 보안 주체의 관리를 사용 하도록 설정 하려면 편지 병합 받는 사람 역할은 기본적으로 조직 관리 및 Recipient Management 역할 그룹에 할당 됩니다. 역할 그룹, 사용자 또는 Usg 편지 병합 받는 사람 역할에 할당 된 기존 보안 주체를 관리할 수 있습니다. 다른 역할 그룹, 사용자 또는 Usg 기존 보안 주체를 관리할 수 있도록을 하려는 경우에 자신에 게 메일 받는 사람에 게 역할을 할당 해야 합니다.

역할 그룹, 사용자 또는 Usg에 역할을 추가 하는 방법에 대 한 자세한 내용은 다음 항목을 참조 합니다.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

분할 권한 모델으로 전환 하 고 공유 사용 권한 모델을 다시 변경 하려고 하는 경우 [Exchange 2013 공유 사용 권한 구성](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)를 참조 하십시오.

맨 위로 이동

## 분할 된 사용 권한

조직에는 Exchange 관리 및 Active Directory 관리 구분을 하는 경우 Exchange 분할 권한 모델을 지원 하도록 구성 해야 합니다. Active Directory 관리자와 같은 보안 주체를 만들려는 하는 관리자만 그렇게 수 올바르게 구성 하는 경우 및 Exchange 관리자만 기존 보안 주체에 Exchange 특성을 수정할 수 있게 됩니다. 사용 권한의 분할이 줄어들면 대략 Active Directory 에서 도메인 및 구성 파티션의 줄을 따라 합니다. 파티션 명명 컨텍스트 라고도 합니다. 도메인 파티션 사용자, 그룹 및 특정 도메인에 대 한 다른 개체를 저장합니다. 구성 파티션 Active Directory, Exchange 등을 사용 하는 서비스에 대 한 포리스트 전체 구성 정보를 저장 합니다. 도메인 파티션에 저장 된 데이터는 일반적으로 Active Directory 관리자가 관리 개체에는 Exchange 포함 될 수 있지만- Exchange 관리자가 관리 될 수 있는 특정 특성입니다. 구성 파티션에 저장 된 데이터는이 파티션에에서 데이터를 저장 하는 각 개별 서비스에 대 한 관리자에 의해 관리 됩니다. Exchange 이 일반적으로 Exchange 관리자입니다.

Exchange 2013 에서는 다음과 같은 두 유형의 분할 권한 지원 됩니다.

  - **RBAC 분할 사용 권한**   Active Directory 도메인 파티션에서 보안 주체를 만들 수 있는 권한이 RBAC로 제어 됩니다. 만 Exchange 서버, 서비스 및 적절 한 역할 그룹의 구성원 인 받는 사람이 보안 주체를 만들 수 있습니다.

  - **Active Directory 분할 권한**   Active Directory 도메인 파티션에서 보안 주체를 만들 권한이 Exchange 사용자, 서비스 또는 서버에서 완전히 제거됩니다. RBAC에는 보안 주체를 만들 수 있는 옵션이 제공되지 않습니다. Active Directory에서 보안 주체를 만들려면 Active Directory 관리 도구를 사용해야 합니다.
    

    > [!IMPORTANT]
    > Active Directory 분할 수 있지만 사용 권한은 사용 하도록 설정 하거나 Exchange 2013 및 Exchange 2010 모두 서버에 적용 하는 사용 권한을 구성 하는 Active Directory 분할이 Exchange 2013 설치 하는 컴퓨터에서 설치 프로그램을 실행 하 여 사용 하지 않도록 설정 수 있습니다. 그러나 않은 모든 영향 Microsoft Exchange Server 2007 서버에 있습니다.



조직 공유 사용 권한 대신 분할 권한 모델을 사용 하 여 선택, 하는 경우에 RBAC 분할 권한 모델을 사용 하는 것이 좋습니다. RBAC 분할 권한 모델 Active Directory 으로 분리 하 여 거의 동일한 관리를 제공 하는 동안 훨씬 더 큰 유연성 분할 된 경우를 제외 하 고 사용 권한을 해당 Exchange 서버 및 서비스 분할 권한 모델 RBAC에서 보안 주체를 만들 수를 제공 합니다.

Active Directory 설치 하는 동안 사용 권한을 분할할 수 있도록 할지 여부를 묻는 메시지가 표시 하려는 합니다. Active Directory 사용 권한 분할을 사용 하도록 설정 하려는 경우 공유 사용 권한 관리로 변경할 수 있습니다 또는 RBAC 설치 프로그램을 다시 실행 하 여 사용 권한을 분할 및 사용 권한 분할 Active Directory 를 사용 하지 않도록 설정 합니다. 조직에서 모든 Exchange 2010 및 Exchange 2013 서버에 적용 하는이 옵션을이 선택 합니다.

다음 섹션에서는 RBAC 및 Active Directory 자세히 사용 권한 분할을 설명 합니다.

맨 위로 이동

## RBAC 분할 사용 권한

RBAC 보안 모델에서 Active Directory 구성 파티션에 Exchange 조직 데이터를 관리 하는 모든 사람이 Active Directory 도메인 파티션에서 보안 주체를 만들 수 있는 사람을 구분 하는 기본 관리 역할 할당을 수정 합니다. 메일 받는 사람 만들기 및 보안 그룹 만들기 및 멤버 자격 역할의 구성원 인 관리자가 사서함 및 메일 그룹을 사용 하는 사용자와 같은 보안 주체를 만들 수 있습니다. 이러한 사용 권한은 Exchange 외부 보안 주체 관리 도구를 만들 때 필요한 권한을와 별개로 유지 합니다. 메일 받는 사람 만들기 또는 보안 그룹 만들기 및 멤버 자격 역할 할당 되지 않은 Exchange 관리자 Exchange 수정할 수 있으므로-관련 보안 주체에 대 한 특성입니다. Active Directory 관리자 만들기 Active Directory 보안 주체를 Exchange 관리 도구를 사용 하 여 설정할을 수도 있습니다.

Exchange 서버와 Exchange 신뢰할 수 있는 하위 시스템도 사용 권한이 RBAC와 통합 하는 타사 프로그램과 사용자를 대신 하 여 Active Directory 에서 보안 주체를 만들 수 있습니다.

사용 권한 분할 RBAC는 것이 좋습니다 조직에는 다음과 같은 경우:

  - 조직에만 Active Directory 관리 도구를 사용 하 여 수행 하 고만 보안 주체 생성 되도록 필요 하지 않습니다 사용자가 특정 Active Directory 권한이 할당 됩니다.

  - 조직에서 보안 주체를 만들려는 Exchange 서버 등의 서비스를 허용 합니다.

  - 관리 도구 Exchange 내에서 자신의 만들기를 허용 하 여 사서함, 메일 사용이 가능한 사용자, 메일 그룹 및 역할 그룹을 만드는데 필요한 프로세스를 단순화 하기 하려고 합니다.

  - 메일 그룹 및 Exchange 관리 도구를 사용 하는 내에서 역할 그룹의 구성원 자격 관리 하려고 합니다.

  - Exchange 서버를 자신을 대신해 보안 주체를 만들 수 필요로 하는 제 3 자 프로그램 해야 합니다.

없음 Active Directory 관리 Exchange 관리 도구를 사용 하 여 수행할 수 있는 또는 Exchange 서비스에 의해 Exchange 및 Active Directory 관리의 전체 분리를 요구 하는 조직, 하는 경우이 항목의 뒷부분에 Active Directory에 대 한 분할 된 사용 권한 섹션을 참조 합니다.

기본적으로 부여 되는 역할 그룹에서 보안 주체를 만들기 위해 필요한 사용 권한을 제거할 수동 프로세스는 공유 사용 권한에서 사용 권한 분할 RBAC로 전환 합니다. 다음 표에서 Exchange 및 기본적으로 할당 하는 관리 역할 그룹의 보안 주체를 만들 수 있도록 하는 역할을 보여줍니다.

### 보안 계정 관리 역할

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>관리 역할</th>
<th>역할 그룹</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Mail Recipient Creation 역할</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">보안 그룹 만들기 및 멤버 자격 역할</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
</tbody>
</table>


기본적으로 조직 관리 및 Recipient Management 역할 그룹의 구성원 보안 주체를 만들 수 있습니다. 만든 새 역할 그룹에 기본 제공 역할 그룹에서 보안 주체를 만들 수 있는 기능을 전송 해야 합니다.

사용 권한 분할 RBAC를 구성 하려면 다음을 수행 해야 합니다.

1.  활성화 된 경우 Active Directory 분할 된 사용 권한을 사용 하지 않도록 설정 합니다.

2.  보안 주체를 만들 수 있게 될 Active Directory 관리자가 포함 된 역할 그룹을 만듭니다.

3.  메일 받는 사람 만들기 역할과 새 역할 그룹 간에 일반 및 위임 역할 할당을 만듭니다.

4.  보안 그룹 만들기 및 구성원 역할과 새 역할 그룹 간에 일반 및 위임 역할 할당을 만듭니다.

5.  일반 및 위임 Mail Recipient Creation 역할 및 조직 관리 및 Recipient Management 역할 그룹 간에 관리 역할 할당을 제거 합니다.

6.  일반 및 위임 보안 그룹 만들기 및 멤버 자격 역할 및 조직 관리 역할 그룹 간에 역할 할당을 제거 합니다.

이 작업을 수행한 후 만든 새 역할 그룹의 구성원만 사서함과 같은 보안 주체를 만들 수 있게 됩니다. 새 그룹 개체를 만들 수만 있습니다. 새 개체에 Exchange 특성을 구성할 수 없습니다. 새 그룹의 구성원 인 Active Directory 관리자가 필요 개체 및 Exchange 관리자를 만들려면 해야 합니다 특성을 구성 하는 Exchange 개체에. Exchange 관리자는 다음 cmdlet을 사용 하 여 수 없습니다.

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

그러나 Exchange 관리자, 수 있게 됩니다 만들고 Exchange 관리-관련 개체, 전송 규칙, 메일 그룹 등 및 Exchange 관리-관련 모든 개체에 대해 특성입니다.

또한 EAC 및 Outlook Web App, 새 사서함 마법사 등의 관련된 기능 됩니다도 더이상 사용할 수 없거나이 사용 하려고 하면 오류가 발생 합니다.

또한 새 개체의 Exchange 특성을 관리할 수 있도록 새 역할 그룹을 하려는 경우 편지 병합 받는 사람 역할 새 역할 그룹에 게 할당할도 필요 합니다.

분할 권한 모델을 구성 하는 방법에 대 한 자세한 내용은 [Exchange 2013 분할 된 사용 권한 구성](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)을 참조 하십시오.

맨 위로 이동

## Active Directory 분할 사용 권한

Active Directory 사용 권한 분할 된 Active Directory 도메인 파티션 사서함 및 메일 그룹 등의 보안 주체를 만들 Active Directory 관리 도구를 사용 하 여 수행 되어야 합니다. Exchange 관리자 및 서버 수행할 수 있는 작업을 제한 하는 Exchange 신뢰할 수 있는 하위 시스템 및 Exchange 서버에 부여 된 사용 권한으로 여러 변경 됩니다. 기능에서 다음과 같이 변경 Active Directory 분할 권한 사용 하도록 설정 하면 발생 합니다.

  - 사서함, 메일 사용이 가능한 사용자, 메일 그룹 및 기타 보안 주체를 만들 Exchange 관리 도구에서 제거 됩니다.

  - 추가 (영문) 및 메일 그룹 구성원을 제거 하면 Exchange 관리 도구에서 수행할 수 없습니다.

  - 보안 주체를 만들려는 Exchange 신뢰할 수 있는 하위 시스템 및 Exchange 서버에 부여 되는 모든 권한 제거 됩니다.

  - Exchange 서버 및 Exchange 관리 도구를 사용 하는 Active Directory 에서 기존 보안 주체의 Exchange 특성을 수정할 수 있습니다.

예 사서함을 만들려면 Active Directory 함께 사용 하도록 설정 하는 분할 된 사용 권한, 사용자 먼저 만들어야 Active Directory 도구를 사용 하 여 필요한 Active Directory 사용 권한 가진 사용자가 합니다. 그런 다음, 사용자는 사서함 사용이 가능한 Exchange 관리 도구를 사용 하 여 하나일 수 있습니다. Exchange-관련 Exchange 관리자 Exchange 관리 도구를 사용 하 여 사서함의 특성을 수정할 수 있습니다.

사용 권한 분할 Active Directory 는 것이 좋습니다 조직에는 다음과 같은 경우:

  - 조직에서는 보안 주체 되어야 Active Directory 관리 도구를 사용 하 여 만든 또는 단일 사용자가 Active Directory 의 특정 사용 권한을 부여 받습니다.

  - 받는 사람이 Exchange 조직 관리에서 보안 주체를 만들 수 있는 기능을 완전히 구분 하려고 합니다.

  - 수행 하려는 모든 메일 그룹 관리, 메일 그룹 만들기를 포함 하 고 추가 (영문) 및 Active Directory 관리 도구를 사용 하 여 해당 그룹의 구성원을 제거 합니다.

  - 보안 주체를 만들려는 자신을 대신해, Exchange 를 사용 하는 제 3 자 프로그램 또는 Exchange 서버 하지 않으려고 합니다.


> [!IMPORTANT]
> 설치 마법사를 사용 하 여 또는 명령줄에서 <CODE>setup.exe</CODE> 를 실행 하는 동안 <EM>ActiveDirectorySplitPermissions</EM> 매개 변수를 사용 하 여 Exchange 2013 를 설치 하는 경우 변경할 수 있는 옵션은 Active Directory 사용 권한 분할로 전환 합니다. 또한 Active Directory 명령줄에서 <CODE>setup.exe</CODE> 다시 실행 하 여 Exchange 2013 를 설치한 후 사용 권한 분할을 사용 하지 않도록 설정 하거나 설정할 수 있습니다. Active Directory 사용 권한 분할을 활성화 하려면 <CODE>true</CODE>를 <EM>ActiveDirectorySplitPermissions</EM> 매개 변수를 설정 합니다. 을 해제 하려면 <CODE>false</CODE>를 설정 합니다. 항상 <EM>PrepareAD</EM> 스위치는 <EM>ActiveDirectorySplitPermissions</EM> 매개 변수를 사용 하 여 지정 해야 합니다.<BR>같은 포리스트 내의 여러 도메인을 설치한 경우 수행 해야도 Active Directory 를 적용 하는 경우 <EM>PrepareAllDomains</EM> 스위치는 사용 권한 분할 또는 각 도메인에 <EM>PrepareDomain</EM> 스위치와 함께 설치 프로그램을 실행 지정 하거나 합니다. <EM>PrepareAllDomains</EM> 스위치를 사용 하는 대신 각 도메인에 <EM>PrepareDomain</EM> 스위치와 함께 설치 프로그램을 실행 하려는 경우 Exchange 서버, 메일 사용이 가능한 개체 또는 Exchange 서버에서 액세스할 수 있는 글로벌 카탈로그 서버를 포함 하는 모든 도메인을 준비 해야 합니다.




> [!IMPORTANT]
> Active Directory Exchange 2010 또는 Exchange 2013 도메인 컨트롤러에서 설치한 경우 사용 권한 분할을 사용할 수 없습니다.<BR>Active Directory 사용 권한 분할을 사용 하지 않도록 설정 하거나 사용 후에 업데이트 된 사용 권한 가진 새 Active Directory 액세스 토큰을 선택 하도록 조직에서 Exchange 2010 및 Exchange 2013 서버를 다시 시작 하는 것이 좋습니다.



Exchange 2013 Exchange Windows 사용 권한 보안 그룹에서 사용 권한 및 구성원을 제거 하 여 Active Directory 분할 권한을 얻을 수 있습니다. 이 보안 그룹에 있는 공유 사용 권한 및 RBAC 분할 된 사용 권한에서 많은 비-Exchange 개체 및 Active Directory 를 통해 특성에 사용 권한은 부여 됩니다. 사용 권한 및이 보안 그룹에 구성원을 제거 하 여 Exchange 관리자 및 서비스 만들기 또는 이러한 비-ExchangeActive Directory 개체를 수정할 수 없게 됩니다.

사용 또는 사용 권한 분할 Active Directory 를 사용 하지 않도록 설정 하는 경우 ExchangeWindows 사용 권한 보안 그룹 및 기타 Exchange 구성 요소에 발생 하는 변경 내용 목록은 다음 표를 참조 합니다.


> [!NOTE]
> 역할 할당을 Exchange 관리자가 보안 주체를 만들 수 있도록 하는 역할 그룹에는 Active Directory 사용 권한 분할을 사용 하는 경우 제거 됩니다. 이 작업은 연결 된 Active Directory 개체를 만들 수 있는 권한이 없기 때문에 실행 중인 경우 오류를 생성 그렇지 않은 경우이 cmdlet에 대 한 액세스를 제거 하려면 수행 합니다.



### Active Directory 분할 권한 변경

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>작업</th>
<th>Exchange로 인 한 변경</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Active Directory 첫번째 Exchange 2013 서버 설치 하는 동안 사용 권한 분할을 사용 하도록 설정</p></td>
<td><p>다음은 수행 되는 사용 하도록 설정 하면 Active Directory 분할 설치 마법사를 통해 또는 <code>/PrepareAD</code> 및 <code>/ActiveDirectorySplitPermissions:true</code> 매개 변수와 함께 <code>setup.exe</code> 를 실행 하 여 사용 권한:</p>
<ul>
<li><p><strong>Microsoft Exchange 보호 그룹</strong> 이라는 조직 구성 단위 (OU) 만들어집니다.</p></li>
<li><p><strong>Exchange Windows 사용 권한</strong> 보안 그룹 OU는 <strong>Microsoft Exchange 보호 되는 그룹</strong> 에 만들어집니다.</p></li>
<li><p><strong>Exchange 신뢰할 수 있는 하위 시스템</strong> 보안 그룹은 <strong>Exchange Windows 사용 권한</strong> 보안 그룹에 추가 되지 않습니다.</p></li>
<li><p>비 위임 관리 역할 할당의 관리 역할에는 다음 관리 역할 유형 만들기를 건너뜁니다.</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p><strong>Exchange Windows 사용 권한</strong> 보안 그룹에 할당 된 액세스 제어 항목 (Ace) Active Directory 도메인 개체에 추가 되지 않습니다.</p></li>
</ul>
<p><em>PrepareAllDomains</em> 또는 <em>PrepareDomain</em> 스위치와 함께 설치 프로그램을 실행 하는 경우 다음 수행 되는 도메인을 준비 하는 각 자식 도메인에서:</p>
<ul>
<li><p><strong>Exchange Windows 사용 권한</strong> 보안 그룹에 할당 된 모든 Ace는 도메인 개체에서 제거 됩니다.</p></li>
<li><p>Ace는 <strong>Exchange Windows 사용 권한</strong> 보안 그룹에 할당 된 모든 Ace 제외 하 고 각 도메인에 설정 됩니다.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>공유 사용 권한 또는 Active Directory 사용 권한 분할에 대 한 사용 권한 분할 RBAC에서 전환</p></td>
<td><p><code>/PrepareAD</code> 및 <code>/ActiveDirectorySplitPermissions:true</code> 매개 변수와 함께 <code>setup.exe</code> 명령을 실행 하는 경우는 다음과 같은 상황이 발생 합니다.</p>
<ul>
<li><p><strong>Microsoft Exchange 보호 그룹</strong> 이라고 하는 OU 만들어집니다.</p></li>
<li><p><strong>Exchange Windows 사용 권한</strong> 보안 그룹은 <strong>Microsoft Exchange 보호</strong> 그룹 OU로 이동 됩니다.</p></li>
<li><p><strong>Exchange 신뢰할 수 있는 하위 시스템</strong> 보안 그룹은 <strong>Exchange Windows 사용 권한</strong> 보안 그룹에서 제거 됩니다.</p></li>
<li><p>비 위임 역할 할당을 모두 관리 역할에는 다음 역할 유형 제거 됩니다.</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p><strong>Exchange Windows 사용 권한</strong> 보안 그룹에 할당 된 모든 Ace는 도메인 개체에서 제거 됩니다.</p></li>
</ul>
<p>설치 프로그램을 실행 중 나와 <em>PrepareAllDomains</em> 또는 <em>PrepareDomain</em> 스위치를 하는 경우 다음 수행 되는 도메인을 준비 하는 각 자식 도메인에서:</p>
<ul>
<li><p><strong>Exchange Windows 사용 권한</strong> 보안 그룹에 할당 된 모든 Ace는 도메인 개체에서 제거 됩니다.</p></li>
<li><p>Ace는 <strong>Exchange Windows 사용 권한</strong> 보안 그룹에 할당 된 모든 Ace 제외 하 고 각 도메인에 설정 됩니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>공유 사용 권한 또는 RBAC 분할 권한 권한 분할 Active Directory 에서 전환</p></td>
<td><p><code>/PrepareAD</code> 및 <code>/ActiveDirectorySplitPermissions:false</code> 매개 변수와 함께 <code>setup.exe</code> 명령을 실행 하는 경우는 다음과 같은 상황이 발생 합니다.</p>
<ul>
<li><p><strong>Microsoft Exchange 보안 그룹</strong> OU <strong>Exchange Windows 사용 권한</strong> 보안 그룹 이동 됩니다.</p></li>
<li><p><strong>Microsoft Exchange 보호 그룹</strong> OU가 제거 되었습니다.</p></li>
<li><p><strong>Exchange 신뢰할 수 있는 하위 시스템</strong> 보안 그룹은 <strong>Exchange Windows 사용 권한</strong> 보안 그룹에 추가 됩니다.</p></li>
<li><p>Ace는 <strong>Exchange Windows 사용 권한</strong> 보안 그룹에 대 한 도메인 개체에 추가 됩니다.</p></li>
</ul>
<p>설치 프로그램을 실행 중 나와 <em>PrepareAllDomains</em> 또는 <em>PrepareDomain</em> 스위치를 하는 경우 다음 수행 되는 도메인을 준비 하는 각 자식 도메인에서:</p>
<ul>
<li><p>Ace는 <strong>Exchange Windows 사용 권한</strong> 보안 그룹에 대 한 도메인 개체에 추가 됩니다.</p></li>
<li><p>Ace는 Ace <strong>Exchange Windows 사용 권한</strong> 보안 그룹에 할당을 포함 하 여 각 도메인에 설정 됩니다.</p></li>
</ul>
<p>메일 받는 사람 만들기 및 보안 그룹 만들기 및 멤버 자격 역할에 역할 할당 되지 않은 공유 사용 권한 관리로 분할 Active Directory 에서 전환 하는 경우 자동으로 생성 됩니다. 위임 역할 할당 Active Directory 사용 권한을 사용 하도록 설정 되 고 분할 하기 전에 사용자 지정 된 경우 이러한 사용자 지정은 그대로 유지 됩니다. 이러한 역할 및 조직 관리 역할 그룹 간에 역할 할당을 만들려면 <a href="configure-exchange-2013-for-shared-permissions-exchange-2013-help.md">Exchange 2013 공유 사용 권한 구성</a>을 참조 하십시오.</p></td>
</tr>
</tbody>
</table>


Active Directory 사용 권한 분할을 활성화 한 후 다음 cmdlet은 더이상 사용할 수 없습니다.

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Active Directory 를 사용 하도록 설정한 후 사용 권한, 분한 다음 cmdlet으로 액세스할 수 있지만 메일 그룹 만들기 또는 수정 메일 그룹 구성원 자격을 사용할 수 없습니다.

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Update-DistributionGroupMember**

계속 사용할 수 있지만 일부 cmdlet 사용 권한을 분할 Active Directory 와 함께 사용할 때만 제한 된 기능을 제공할 수 있습니다. 즉, 구성 Active Directory 파티션에 있는 구성 개체는 도메인 Active Directory 파티션 및 Exchange 에 있는 받는 사람 개체 구성 할 수 있도록 수 있습니다. 수도 할 수 있도록 Exchange 구성-도메인 파티션에 저장 된 개체의 특성을 관련 됩니다. Cmdlet를 사용 하 여 개체를 만드는 또는 비-Exchange 수정 하려고 함-관련 개체 도메인 파티션에 대 한 특성 오류가 발생 합니다. 예, **Add-ADPermission** cmdlet은 사서함에 사용 권한을 추가 하려고 하면 오류가 반환 됩니다. 그러나 수신 커넥터에서 사용 권한을 구성 하는 경우 **Add-ADPermission** cmdlet은 테스트가 성공 합니다. 수신 커넥터 구성 파티션에 저장 되는 동안 사서함 도메인 파티션에 저장 되기 때문입니다.

또한 Exchange 관리 센터 연결 된 기능 및 Outlook Web App, 새 사서함 마법사와 같은 더이상 사용할 수 있는 또는를 사용 하려고 하면 오류가 발생 합니다.

그러나 Exchange 관리자, 수 있게 됩니다 만들고 Exchange 관리-전송 규칙 등의 특정 개체입니다.

Active Directory 를 구성 하는 방법에 대 한 자세한 내용은 분할 권한 모델 [Exchange 2013 분할 된 사용 권한 구성](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)를 참조 하십시오.

맨 위로 이동

