---
title: 'Exchange 2013에 대 한 다중 포리스트 토폴로지를 배포 합니다.: Exchange 2013 Help'
TOCTitle: Exchange 2013에 대 한 다중 포리스트 토폴로지를 배포 합니다.
ms:assetid: d51f2b7d-9045-40cf-8b9f-43787a6fff6d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124734(v=EXCHG.150)
ms:contentKeyID: 51407749
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013에 대 한 다중 포리스트 토폴로지를 배포 합니다.

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

이 항목에서는 여러 포리스트 토폴로지에서 Microsoft Exchange Server 2013 배포의 개요를 제공 합니다. 다음 주제에 대 한 정보를 찾을 수 있습니다.

  - **지원 되는 다중 포리스트 토폴로지** Exchange 2013 에서는 두 유형의 다중 포리스트 토폴로지를 지원: 크로스 포리스트 및 리소스 포리스트 합니다.   

  - **GAL 동기화**   크로스 포리스트 환경을 사용 하는 경우 지정 된 포리스트의 모든 GAL에에서 다른 포리스트의 메일 받는 사람이 포함 되어있는지 확인 해야 합니다.

  - **포리스트 간에 사서함 이동**    Exchange 관리 셸 **New-MoveRequest** 및 **New-MigrationBatch** cmdlet는 하나의 포리스트에서 사서함 이동 하는 데 도움이 됩니다.

  - **여러 포리스트 관리 이해 (영문)**   구성 하 고 포리스트 간에 사용 권한을 관리 하 여 사용 권한 모델에 알아봅니다.

## 지원 되는 다중 포리스트 토폴로지

Exchange 2013 에서는 다음과 같은 유형의 다중 포리스트 토폴로지를 지원합니다.

  - **크로스 포리스트**   크로스 포리스트 토폴로지를 여러 Exchange 포리스트를 사용한 하나입니다. 다중 포리스트 토폴로지에서 Exchange 2013 배포 하기 위해 필요한 대 한 개요는 다음과 같습니다.
    
    1.  각 포리스트에 Exchange 2013 를 먼저 설치 해야 합니다. 자세한 내용은 [Exchange 2013 새 설치 배포](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)를 참조 하십시오.
    
    2.  다음으로 주소 목록 GAL (전체) 각 포리스트의 모든 동기화 된 포리스트의 사용자가 포함 되도록 각 포리스트, 받는 사람을 동기화 해야 합니다. 자세한 내용은 아래 "GAL을 동기화" 섹션을 참조 하십시오.
    
    3.  마지막으로 한 포리스트의 사용자가 다른 포리스트의 사용자에 대 한 가용성 데이터를 볼 수 있도록 가용성 서비스를 구성 해야 합니다. 자세한 내용은 [크로스 포리스트 토폴로지에 대 한 가용성 서비스를 구성 합니다.](configure-the-availability-service-for-cross-forest-topologies-exchange-2013-help.md)을 참조 하십시오.
    
    크로스 포리스트 토폴로지에서 Exchange 2013 배포 하는 방법에 대 한 자세한 내용은, [크로스 포리스트 토폴로지에서 Exchange 2013 배포](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)을 참조 하십시오.

  - **리소스 포리스트**   리소스 포리스트 토폴로지를 Exchange 포리스트와 하나 및 하나 이상의 사용자 계정 포리스트는 합니다. 리소스 포리스트 토폴로지의에서 Exchange 2013 배포 하기 위해 필요한 대 한 개요는 다음과 같습니다.
    
    1.  Exchange 설치와 포리스트에 있어야 합니다. Exchange 포리스트에 Exchange 사서함이 있는 사용자 계정을 비활성화 해야 합니다.
    
    2.  사용자 계정이 포함 된 하나 이상의 포리스트에 있어야 합니다. 이 포리스트 해야 *하지* 않은 Exchange 설치 합니다.
    
    3.  그런 다음, Exchange 포리스트에서 비활성화 된 사용자 계정을 계정 포리스트의 사용자 계정에 연결 해야 합니다.
    
    리소스 포리스트 토폴로지에서 Exchange 2013 배포 하는 방법에 대 한 자세한 내용은, [Exchange 리소스 포리스트 토폴로지에서 Exchange 2013 배포](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md)을 참조 하십시오.

## GAL 동기화

기본적으로 GAL 단일 포리스트의 메일 받는 사람이 포함 됩니다. 크로스 포리스트 환경을 사용 하는 경우에 다른 포리스트의 메일 받는 사람이 포함 되어 제공 되는 포리스트의 모든 GAL 되었는지 확인 하려면 Microsoft 수명 주기 ILM (Identity Manager) 2007 기능 팩 1 (FP1)를 사용 하는 것이 좋습니다. ILM 2007 FP1 사용자가 메일을 보내고 GAL에서 볼 수 있으므로 다른 포리스트의 받는 사람을 표시 하는 메일 사용자를 만듭니다. 포리스트 A 표시 포리스트 B에 그 반대의 메일 사용자로의 사용자 예입니다. 대상 포리스트의 사용자가 메일을 보낼 다른 포리스트의 받는 사람을 나타내는 메일 사용자 개체를 선택 합니다 수 있습니다.

GAL 동기화가 가능하도록 하려면 메일 사용 가능 사용자, 연락처 및 그룹을 지정된 Active Directory 서비스에서 중앙 집중식 메타디렉터리로 가져오는 관리 에이전트를 만들어야 합니다. 메타디렉터리에서 메일 사용 가능 개체는 메일 사용자로 표시됩니다. 그룹은 관련 구성원이 없는 연락처로 표시됩니다. 관리 에이전트는 이 메일 사용자를 지정된 대상 포리스트의 조직 단위로 내보냅니다.

자세한 내용은 Forefront Identity Manager (FIM)에 대 한 [Forefront Identity Manager 2010](https://go.microsoft.com/fwlink/p/?linkid=279864)을 참조 하십시오.

## 포리스트 간에 사서함 이동

크로스 포리스트 토폴로지에서 하나의 포리스트에서 다른 사서함을 이동 하는 것이 좋습니다. 이 작업을 수행 하려면 Exchange 관리 셸 **New-MoveRequest** 또는 **New-MigrationBatch** cmdlet을 사용 해야 합니다. 포리스트 간에 사서함을 이동 하는 방법에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

  - [크로스 포리스트 이동 요청에 대 한 사서함을 준비](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [셸에서 준비 MoveRequest.ps1 스크립트를 사용 하 여 크로스 포리스트 이동에 대 한 준비 사서함](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

  - [예제 코드를 사용 하 여 크로스 포리스트 이동에 대 한 사서함을 준비](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

## 여러 포리스트 관리 이해 (영문)

Exchange 2013 새 사용 권한 기능을 사용 하 여 다중 포리스트 환경 관리.

Exchange 2013 는 액세스 제어 RBAC (역할 기반) 사용 권한 모델을 사용 합니다. 관리 역할 그룹의 구성원 인 관리자 및 최종 사용자에 게 할당 된 관리 역할 할당 정책에는 각 관리자 및 최종 사용자로 수행할 수 있는 결정 합니다. 여러 포리스트 권한을 이해 하려면 RBAC 잘 알고 있어야 해야 합니다. RBAC 및 역할 그룹 및 역할 할당 하는 방법에 대 한 자세한 내용은 정책 특히 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참조 합니다.

구성 및 사용자 포리스트 간에 사용 권한을 관리 하는 RBAC 권한 모델을 사용할 수 있습니다. 여러 포리스트 사용 권한에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

  - [다중 포리스트 사용 권한을 이해 (영문)](understanding-multiple-forest-permissions-exchange-2013-help.md)

  - [연결 된 역할 그룹 관리](manage-linked-role-groups-exchange-2013-help.md)

  - [기본 제공 역할 그룹을 미러링 하는 연결 된 역할 그룹 만들기](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

