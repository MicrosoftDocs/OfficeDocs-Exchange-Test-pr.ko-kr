---
title: '크로스 포리스트 토폴로지에 대 한 가용성 서비스를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 크로스 포리스트 토폴로지에 대 한 가용성 서비스를 구성 합니다.
ms:assetid: f1e7d407-f0d3-47a7-8cc3-03c5980445d5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125182(v=EXCHG.150)
ms:contentKeyID: 52058148
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 크로스 포리스트 토폴로지에 대 한 가용성 서비스를 구성 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-10-22_

가용성 서비스는 MicrosoftOutlook을 실행하는 클라이언트에 일관성 있고 보안된 최신 약속 있음/없음 정보를 제공하여 정보 근로자의 약속 있음/없음 정보를 향상시킵니다. 기본적으로 이 서비스는 Exchange Server 2013과 함께 설치됩니다. 모든 연결 클라이언트가 Outlook을 실행하는 포리스트 간 토폴로지에서 가용성 서비스는 약속 있음/없음 정보를 검색하는 유일한 방법입니다. 셸을 사용하여 포리스트 간 토폴로지에 대한 가용성 서비스를 구성할 수 있습니다.


> [!NOTE]
> EAC를 사용하여 포리스트 간 토폴로지에 대한 가용성 서비스를 구성할 수는 없습니다.



## 신뢰할 수 있는 포리스트와 신뢰할 수 없는 포리스트에서 가용성 서비스 사용

트러스트된 포리스트 또는 트러스트되지 않은 포리스트에 대해 포리스트 간 토폴로지에서 가용성 서비스를 사용할 수 있습니다. 사용할 수 있는 약속 있음/없음 정보의 유형은 신뢰할 수 있는 포리스트와 신뢰할 수 없는 포리스트 중 어느 것을 사용하는지에 따라 결정됩니다.

**신뢰할 수 있는 포리스트**   신뢰할 수 있는 포리스트에서는 사용자별로 약속 있음/없음 정보를 검색하도록 가용성 서비스를 구성할 수 있습니다. 가용성 서비스가 사용자별로 약속 있음/없음 정보를 검색하도록 구성된 경우는 서비스에서 특정 사용자를 대신하여 포리스트 간 요청을 수행할 수 있습니다. 그러면 원격 포리스트에 있는 사용자가 같은 포리스트에 있지 않은 사람에 대해 자세한 약속 있음/없음 정보를 검색할 수 있습니다.

**신뢰할 수 없는 포리스트**   신뢰할 수 없는 포리스트에서는 조직 차원에서만 약속 있음/없음 정보를 검색하도록 가용성 서비스를 구성할 수 있습니다. 가용성 서비스가 조직 수준에서 포리스트 간 약속 있음/없음 요청을 수행하면 조직의 각 사용자에 대해 약속 있음/없음 정보가 반환됩니다. 신뢰할 수 없는 포리스트에서는 사용자별로 반환되는 약속 있음/없음 정보의 수준을 제어할 수 없습니다.

## 포리스트 간 토폴로지에 대해 Windows 구성

기본적으로 GAL(전체 주소 목록)에는 단일 포리스트의 메일 받는 사람이 수록되어 있습니다. 크로스 포리스트 환경에서 Microsoft ILM(Identity Lifecycle Manager) 2007 FP1(기능 팩 1)을 사용하여 해당 포리스트의 GAL에 다른 포리스트의 메일 받는 사람이 포함되어 있는지 확인하는 것이 좋습니다. ILM 2007 FP1은 다른 포리스트의 받는 사람을 나타내는 메일 사용자를 만들기 때문에 사용자는 GAL에서 해당 사용자를 보고 메일을 보낼 수 있습니다. 예를 들어 포리스트 A의 사용자가 포리스트 B에 메일 사용자로 표시되거나 포리스트 B의 사용자가 포리스트 A에 메일 사용자로 표시됩니다. 대상 포리스트의 사용자는 다른 포리스트의 받는 사람을 나타내는 메일 사용자 개체를 선택하여 메일을 보낼 수 있습니다.

GAL 동기화가 가능하도록 하려면 메일 사용 가능 사용자, 연락처 및 그룹을 지정된 Active Directory 서비스에서 중앙 집중식 메타디렉터리로 가져오는 관리 에이전트를 만들어야 합니다. 메타디렉터리에서 메일 사용 가능 개체는 메일 사용자로 표시됩니다. 그룹은 관련 구성원이 없는 연락처로 표시됩니다. 관리 에이전트는 이 메일 사용자를 지정된 대상 포리스트의 조직 단위로 내보냅니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "가용성 서비스 사용 권한" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 신뢰할 수 있는 포리스트 간 토폴로지에서 사용자 단위 약속 있음/없음 정보 구성

이 예에서는 가용성 서비스가 대상 포리스트의 사서함 서버에서 사용자별 약속 있음/없음 정보를 검색하도록 구성합니다.

```powershell
Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedrights "ms-Exch-
EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"
```

이 예에서는 가용성 서비스가 원본 포리스트의 로컬 사서함 서버에서 사용하는 약속 있음/없음 액세스 방법을 정의합니다. 로컬 사서함 서버는 포리스트 ContosoForest.com에서 사용자별로 약속 있음/없음 정보에 액세스하도록 구성됩니다. 이 예에서는 서비스 계정을 사용하여 약속 있음/없음 정보를 검색합니다.

```powershell
Add-AvailabilityAddressSpace -Forestname ContosoForest.com -AccessMethod PerUserFB -UseServiceAccount:$true
```


> [!NOTE]
> 양방향 포리스트 간 가용성을 구성하려면 대상 포리스트에서 이 단계를 반복합니다.



신뢰할 수 있는 포리스트 간 가용성을 구성하고 조직 전체 또는 사용자별 자격 증명을 지정하는 대신 서비스 계정을 사용하도록 선택한 경우 "셸을 사용하여 서비스 계정으로 신뢰할 수 있는 포리스트 간 가용성 구성" 섹션의 예와 같이 권한을 확장해야 합니다. 대상 포리스트에서 절차를 수행하면 원본 포리스트의 사서함 서버에 원본 사용자 컨텍스트를 직렬화할 권한이 생깁니다.

## 셸을 사용하여 서비스 계정으로 신뢰할 수 있는 포리스트 간 가용성 구성

이 예에서는 서비스 계정으로 신뢰할 수 있는 포리스트 간 가용성을 구성합니다.

```powershell
Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedright "ms-Exch-EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"
```

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Get-MailboxServer](https://technet.microsoft.com/ko-kr/library/bb123539\(v=exchg.150\))

  - [Add-ADPermission](https://technet.microsoft.com/ko-kr/library/bb124403\(v=exchg.150\))

  - [Add-AvailabilityAddressSpace](https://technet.microsoft.com/ko-kr/library/bb124122\(v=exchg.150\))

  - [Set-AvailabilityConfig](https://technet.microsoft.com/ko-kr/library/bb124103\(v=exchg.150\))

## 셸을 사용하여 신뢰할 수 없는 포리스트 간 토폴로지에서 조직 차원의 약속 있음/없음 정보를 구성

이 예에서는 가용성 구성 개체에 조직 차원의 계정을 설정하여 대상 포리스트에서 약속 있음/없음 정보 액세스 수준을 구성합니다.

```powershell
Set-AvailabilityConfig -OrgWideAccount "Contoso.com\User"
```

이 예에서는 원본 포리스트의 가용성 주소 공간 구성 개체를 추가합니다.

```powershell
$a = Get-Credential (Enter the credentials for organization-wide user in Contoso.com domain)
Add-AvailabilityAddressspace -Forestname Contoso.com -Accessmethod OrgWideFB -Credential:$a
```

