---
title: '공용 폴더: Exchange 2013 Help'
TOCTitle: 공용 폴더
ms:assetid: 94c4fb69-9234-4b34-8c1c-da2a0a11da65
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150538(v=EXCHG.150)
ms:contentKeyID: 50483698
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공용 폴더

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-03-27_

공용 폴더는 공유 액세스를 위해 설계된 폴더입니다. 이 폴더를 통해 간단하고 효율적으로 정보를 수집 및 구성하고 작업 그룹이나 조직의 다른 사람과 공유할 수 있습니다. 공용 폴더를 통해 콘텐츠를 쉽게 검색할 수 있는 상세 계층 구조로 구성할 수 있습니다. 사용자는 Outlook에서 전체 계층 구조를 확인하여 원하는 콘텐츠를 쉽게 찾을 수 있습니다.


> [!NOTE]
> 공용 폴더를 사용할 수 있는 Outlook 클라이언트는 Exchange 2013용 Outlook Web App, Outlook 2007, Outlook 2010, Outlook 2013 및 Outlook for Mac입니다.



메일 그룹의 보관 방법으로 공용 폴더를 사용할 수도 있습니다. 공용 폴더에서 메일을 사용하도록 설정한 다음 메일 그룹의 구성원으로 공용 폴더를 추가하면 해당 그룹으로 보낸 전자 메일이 나중에 참조할 수 있도록 공용 폴더에 자동으로 추가됩니다.


> [!NOTE]
> Exchange 2013 서버에서 공용 폴더에 액세스하려면 Outlook 2007 이상을 사용해야 합니다.



공용 폴더는 다음을 수행 하도록 설계 되지 않습니다.

  - **데이터 보관** 때때로 사서함 제한을 가진 사용자 사서함 대신 공용 폴더를 사용 하 여 데이터를 보관할 수 있습니다. 공용 폴더의 저장소에 영향을 하 고 사서함 제한의 목표 저하 있기 때문에이 방법은 권장 되지 않습니다. 대신, 보관 솔루션으로 [전체에서 Exchange 2013의 보관](in-place-archiving-in-exchange-2013-exchange-2013-help.md) 를 사용 하는 것이 좋습니다.

  - **문서 공유 및 공동 작업** 공용 폴더 제공 하지 버전 관리 또는 다른 문서 체크인 및 체크아웃 기능을 제어 하 고 콘텐츠 변경 자동 알림 등의 관리 기능입니다. 대신, [SharePoint](https://go.microsoft.com/fwlink/?linkid=282474) 를 사용 하 여 솔루션을 공유 하 여 설명서도 하는 것이 좋습니다.

Exchange 2013의 공용 폴더 및 기타 공동 작업 방법에 대한 자세한 내용은 [공동 작업](collaboration-exchange-2013-help.md)을 참조하십시오.

Exchange 2013의 공용 폴더에 대한 질문과 대답을 찾아보려면 [FAQ: 공용 폴더](faq-public-folders-exchange-2013-help.md)를 참조하십시오.

제한 및 공용 폴더에 대 한 할당량에 대 한 자세한 내용은 [공용 폴더의 제한](limits-for-public-folders-exchange-2013-help.md)을 참조 하십시오.

공용 폴더 관리 작업 목록이 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조 하십시오.

이 항목의 Exchange Online 버전은 필요 하신가요? [Office 365 및 Exchange Online의 공용 폴더](https://technet.microsoft.com/ko-kr/library/jj200758\(v=exchg.150\))를 참조 하십시오.

**목차**

Public folder architecture

공용 폴더 마이그레이션

Public folder moves

Public folder quotas

Disaster recovery

## 공용 폴더 아키텍처

Exchange 2013의 공용 폴더는 사서함 인프라를 사용하여 사서함 데이터베이스의 기존 고가용성 및 저장소 기술을 활용하도록 새로워졌습니다. 공용 폴더 아키텍처에서는 특별히 설계된 사서함을 사용하여 공용 폴더 계층 구조와 콘텐츠를 모두 저장합니다. 이는 또한 공용 폴더 데이터베이스가 더 이상 존재하지 않음을 의미합니다. DAG(데이터베이스 가용성 그룹)를 통해 공용 폴더 사서함의 고가용성이 제공됩니다. DAG에 대한 자세한 내용은 [DAG(데이터베이스 가용성 그룹)](database-availability-groups-dags-exchange-2013-help.md) 항목을 참조하십시오.

공용 폴더의 주요 아키텍처 구성 요소는 공용 폴더 사서함으로, 하나 이상의 사서함 데이터베이스에 있을 수 있습니다.

## 공용 폴더 사서함

공용 폴더 사서함에는 *기본 계층 구조 사서함*과 *보조 계층 구조 사서함*의 두 가지 유형이 있습니다. 두 사서함 유형 모두 콘텐츠를 포함할 수 있습니다.

  - **기본 계층 구조 사서함**   기본 계층 구조 사서함은 공용 폴더 계층 구조 하나 쓰기 가능한 복사본입니다. 이러한 읽기 전용 복사본 될 수 있지만 공용 폴더 계층 구조는 다른 모든 공용 폴더 사서함에 복사 됩니다.

  - **보조 계층 구조 사서함**   보조 계층 구조 사서함에서는 공용 폴더 콘텐츠를 포함 하는 공용 폴더 계층의 읽기 전용 복사본입니다.


> [!NOTE]
> 공용 폴더 사서함에 대해 보존 정책이 지원되지 않습니다.



공용 폴더 사서함은 두 가지 방법으로 관리할 수 있습니다.

  - EAC(Exchange 관리 센터)에서 **공용 폴더** \> **공용 폴더 사서함**으로 이동합니다.

  - Exchange 관리 셸에서 **\*-Mailbox** cmdlet 집합을 사용합니다. 공용 폴더 사서함을 지원하도록 다음 매개 변수가 [New-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997663\(v=exchg.150\)) cmdlet에 추가되었습니다.
    
      - *PublicFolder*   이 매개 변수는 **New-Mailbox** cmdlet과 함께 사용되어 공용 폴더 사서함을 만듭니다. 공용 폴더 사서함을 만들면 사서함 유형이 `PublicFolder`인 새 사서함이 만들어집니다. 자세한 내용은 [공용 폴더 사서함 만들기](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/create-public-folder-mailbox)를 참조하십시오.
    
      - *HoldForMigration*   이 매개 변수는 이전 버전의 Exchange 2013에서 공용 폴더를 마이그레이션한 경우에만 사용됩니다. 자세한 내용은 이 항목의 뒷부분에 있는 Migrate Public folders from previous versions을 참조하십시오.
    
      - *IsHierarchyReady*   이 매개 변수는 공용 폴더 사서함 사용자를 공용 폴더 계층 구조를 제공 하도록 준비 되었는지 여부를 나타냅니다. 공용 폴더 사서함에는 전체 계층 구조 동기화 되었다고 한 후에 `$True` 를 설정 됩니다. 매개 변수는 $False 로설정하면 사용자가 계층 구조에 액세스 하는데 사용 되지 않습니다. 그러나 특정 공용 폴더 사서함에 사용자 사서함에서 *DefaultPublicFolderMailbox* 속성을 설정 하는 경우 사용자가 계속 액세스할 지정 된 공용 폴더 사서함 *IsHierarchyReady* 매개 변수가 `$False`으로 설정 하는 경우에 합니다.
    
      - *IsExcludedFromServingHierarchy*   이 매개 변수는 사용자가 지정된 공용 폴더 사서함의 공용 폴더 계층 구조에 액세스하지 못하도록 합니다. 부하 분산을 위해 사용자는 기본적으로 각 공용 폴더 사서함에 균등하게 분산됩니다. 공용 폴더 사서함에 이 매개 변수가 설정되어 있는 경우 해당 사서함은 이 자동 부하 분산에 포함되지 않고 사용자가 공용 폴더 계층 구조를 검색하기 위해 액세스하지 못하게 됩니다. 그러나 사용자 사서함의 *DefaultPublicFolderMailbox* 속성을 특정 공용 폴더 사서함으로 설정한 경우에는 지정된 공용 폴더 사서함에 대해 *IsExcludedFromServingHierarchy* 매개 변수가 설정되었더라도 사용자가 해당 공용 폴더 사서함에 액세스할 수 있습니다.

*DefaultPublicFolderMailbox* 속성을 사용 하는 사용자의 사서함에 명시적으로 지정 하는 경우 또는 다음 조건이 충족 될 경우 보조 계층 구조 사서함 사용자에 게만 공용 폴더 계층 구조 정보를 사용할 됩니다.

  - 공용 폴더 사서함에서 *IsHierarchyReady* 속성은 `$True`로 설정 됩니다.

  - 공용 폴더 사서함에서 *IsExcludedFromServingHierarchy* 속성은 `$False`로 설정 됩니다.

## 공용 폴더 계층 구조

공용 폴더 계층 구조에는 트리 구조를 포함하여 폴더의 속성 및 구성 정보가 포함됩니다. 각 공용 폴더 사서함은 공용 폴더 계층 구조의 복사본을 포함합니다. 계층 구조의 쓰기 가능 복사본은 기본 공용 폴더 사서함에 포함된 복사본 하나뿐입니다. 특정 폴더에 대해 계층 구조 정보는 다음 사항을 식별하는 데 사용됩니다.

  - 폴더에 대한 사용 권한

  - 공용 폴더 트리에서의 폴더 위치(상위 폴더와 하위 폴더 포함)


> [!NOTE]
> 메일 사용 가능 공용 폴더의 전자 메일 주소에 대한 정보는 계층 구조에 저장되지 않습니다. 전자 메일 주소는 Active Directory의 디렉터리 개체에 저장됩니다.



## 계층 구조 동기화

공용 폴더 계층 구조 동기화 프로세스에서는 ICS(증분 변경 동기화)를 사용합니다. ICS는 Exchange 저장소 계층 구조 또는 콘텐츠의 변경 내용을 모니터링하고 동기화하는 메커니즘을 제공합니다. 변경에는 폴더 및 메시지 만들기/수정/삭제가 포함됩니다. 사용자가 콘텐츠 사서함에 연결하여 사서함을 사용할 때는 15분마다 동기화가 수행됩니다. 콘텐츠 사서함에 연결된 사용자가 없으면 동기화 트리거 빈도가 낮아집니다(24시간마다). 폴더 만들기 등의 쓰기 작업을 기본 계층 구조에서 수행하는 경우에는 콘텐츠 사서함에 대한 동기화가 즉시(동기식으로) 트리거됩니다.


> [!IMPORTANT]
> 계층 구조의 쓰기 가능 복사본은 하나뿐이므로 폴더 만들기는 사용자가 연결된 콘텐츠 사서함에 의해 계층 구조 사서함으로 프록시됩니다.



대규모 조직에서 새 공용 폴더 사서함을 만들 경우 계층 구조는 사용자가 사서함에 연결하기 전에 해당 공용 폴더로 동기화되어야 합니다. 그렇지 않으면 사용자가 Outlook에 연결될 때 불완전한 공용 폴더가 표시될 수 있습니다. 사용자가 새 공용 폴더 사서함에 연결을 시도하지 않고 이 동기화가 수행되도록 하려면 공용 폴더 사서함을 만들 때 **New-Mailbox** cmdlet에 대해 *IsExcludedFromServingHierarchy* 매개 변수를 설정합니다. 이 매개 변수는 사용자가 새로 만들어진 공용 폴더 사서함에 연결되지 못하도록 합니다. 동기화가 완료되면 *IsExcludedFromServingHierarchy* 매개 변수를 `false`로 설정한 상태에서 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) cmdlet을 실행합니다. 이는 공용 폴더 사서함이 연결될 준비가 되었음을 나타냅니다. [Get-PublicFolderMailboxDiagnostics](https://technet.microsoft.com/ko-kr/library/jj218720\(v=exchg.150\)) cmdlet을 사용하여 *SyncInfo* 및 *AssistantInfo* 속성으로 동기화 상태를 볼 수도 있습니다.

자세한 내용은 [공용 폴더 만들기](create-a-public-folder-exchange-2013-help.md)를 참조하십시오.

## 공용 폴더 콘텐츠

공용 폴더 콘텐츠에는 전자 메일 메시지, 게시물, 문서, eForm 등이 포함될 수 있습니다. 콘텐츠는 공용 폴더 사서함에 저장되지만 여러 공용 폴더 사서함으로 복제되지는 않습니다. 모든 사용자는 같은 공용 폴더 사서함의 같은 콘텐츠 집합에 액세스합니다. 공용 폴더 콘텐츠에 대한 전체 텍스트 검색을 수행할 수는 있지만, 여러 공용 폴더 간에 공용 폴더 콘텐츠를 검색할 수는 없으며 Exchange 검색에서는 콘텐츠를 인덱싱하지 않습니다.


> [!NOTE]
> Outlook Web App은 지원 되지만 제한 사항과 함께 합니다. 추가 하 고 하 고 즐겨찾기 공용 폴더를 제거 하 고, 만들기, 편집, 게시물, 삭제 및 게시물에 회신 하기 등의 항목 수준 작업을 수행할 수 있습니다. 그러나 만들 하거나 Outlook Web App에서 공용 폴더를 삭제할 수 없습니다. 또한 Outlook Web App에서 즐겨찾기 목록에만 메일, 게시, 일정 및 연락처 공용 폴더를 추가할 수 있습니다.



## 공용 폴더 마이그레이션

이전 버전의 Exchange Online으로 Exchange Server 또는 이전 버전의 Exchange 2013을 Exchange 서버에서 공용 폴더를 마이그레이션할 수 있습니다. 또한 Exchange Online으로 Exchange 2013 공용 폴더를 마이그레이션할 수 있습니다.

Exchange 2013을 설치 하기 전에 조직에서 Exchange 2010 SP3 또는 Exchange 2007 SP3 RU10 공용 폴더가 이미 있으면 해당 공용 폴더 Exchange 2013으로 마이그레이션해야 합니다. 이 작업을 수행 하려면 **PublicFolderMigrationRequst** cmdlet를 사용 합니다. 자세한 내용은 [마이그레이션 일괄 처리를 사용 하 여 이전 버전에서 Exchange 2013 공용 폴더 마이그레이션](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)을 참조 하십시오. 조직에 Exchange Online으로 이동 하는 경우에 공용 폴더를 클라우드로 마이그레이션할 수 있으며 동시에 업그레이드 수 있습니다. 자세한 내용은 [마이그레이션 일괄 처리를 사용 하 여 Office 365 및 Exchange Online으로 레거시 공용 폴더 마이그레이션](use-batch-migration-to-migrate-legacy-public-folders-to-office-365-and-exchange-online-exchange-online-help.md) 및 [마이그레이션 일괄 처리를 사용 하 여 Exchange Online으로 Exchange 2013 공용 폴더 마이그레이션](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/batch-migration-of-exchange-2013-public-folders)를 참조 하십시오.

공용 폴더가 저장되는 방식의 변경 사항으로 인해 레거시 Exchange 사서함에서 Exchange 2013 서버나 Exchange Online의 공용 폴더 계층 구조에 액세스할 수 없습니다. 하지만 Exchange 2013 서버나 Exchange Online의 사용자 사서함은 레거시 공용 폴더에 연결할 수 있습니다. Exchange 2013 공용 폴더 및 레거시 공용 폴더는 동시에 Exchange 조직에 있을 수 없습니다. 즉 버전 간 공존할 수 없습니다. 공용 폴더를 Exchange Server 2013이나 Exchange Online으로 마이그레이션하는 작업은 현재 일회성 단독형 프로세스입니다.

공용 폴더 마이그레이션 전에 해야 먼저 마이그레이션하는 레거시 사서함을 Exchange 2013 또는 Exchange Online 것이 좋습니다. 마이그레이션 대 한 자세한 내용은 [Exchange 2013 사서함 이동](mailbox-moves-in-exchange-2013-exchange-2013-help.md), [Office 365로 전자 메일의 단독형 마이그레이션 수행](https://go.microsoft.com/fwlink/p/?linkid=536689)하 고 [Office 365로 전자 메일의 미리 구성 된 마이그레이션 수행](https://go.microsoft.com/fwlink/p/?linkid=536687)사서함을 참조 하십시오.

## 공용 폴더 이동

공용 폴더를 다른 공용 폴더 사서함으로 이동할 수 있으며 공용 폴더 사서함을 다른 사서함 데이터베이스로 이동할 수 있습니다. 공용 폴더를 다른 공용 폴더 사서함으로 이동하려면 **PublicFolderMoveRequest** cmdlet 집합을 사용합니다. 이동 중인 공용 폴더 아래의 하위 폴더는 기본적으로 이동되지 않습니다. 공용 폴더의 분기를 이동하려면 Exchange 2013에 기본적으로 설치되는 `Move-PublicFolderBranch.ps1` 스크립트를 사용하면 됩니다. 자세한 내용은 [다른 공용 폴더 사서함에 공용 폴더 이동](move-a-public-folder-to-a-different-public-folder-mailbox-exchange-2013-help.md)을 참조하십시오.

공용 폴더를 이동하는 것 외에도 **MoveRequest** cmdlet 집합을 사용하여 공용 폴더 사서함을 다른 사서함 데이터베이스로 이동할 수 있습니다. 이 집합은 일반 사서함을 이동하는 데 사용되는 cmdlet 집합과 같습니다. 자세한 내용은 [공용 폴더 사서함을 다른 사서함 데이터베이스로 이동](move-a-public-folder-mailbox-to-a-different-mailbox-database-exchange-2013-help.md)을 참조하십시오.

**PublicFolderMoveRequest** cmdlet 및 **MoveRequest** cmdlet에서는 사서함 복제 서비스를 사용하여 공용 폴더를 비동기적으로 이동합니다. 즉 cmdlet에서 실제 작업을 수행하지 않으므로 사용자는 대부분 이동 동안 계속해서 공용 폴더 및 공용 폴더 사서함을 사용할 수 있습니다. 사서함 복제 서비스가 사서함 이동, 요청 가져오기 및 내보내기, 공용 폴더 이동 요청 등을 수행하므로 제한 및 작업 부하 관리를 고려해야 합니다.

## 공용 폴더 할당량

공용 폴더 사서함을 만들 때 이 사서함은 사서함 데이터베이스 기본값의 크기 제한을 자동으로 상속합니다. 따라서 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) cmdlet 사용 시 현재 저장소 할당량 상태를 정확하게 평가하려면 *ProhibitSendQuota*, *ProhibitSendReceiveQuota* 및 *IssueWarningQuota* 속성 외에도 *UseDatabaseQuotaDefaults* 속성에서 검토해야 합니다. *UseDatabaseQuotaDefaults* 속성이 `true`로 설정된 경우에는 사서함별 설정이 무시되고 사서함 데이터베이스 제한이 사용됩니다. 이 속성이 `true`로 설정된 경우 *ProhibitSendQuota*, *ProhibitSendReceiveQuota* 및 *IssueWarningQuota* 속성이 `unlimited`로 설정되었더라도 사서함 제한은 실제로 무제한이 아닙니다. 대신 **Get-MailboxDatabase** cmdlet을 사용하여 사서함 데이터베이스 저장소 제한을 검토하여 사서함 제한을 확인해야 합니다. *UseDatabaseQuotaDefaults* 속성이 `false`로 설정된 경우에는 사서함별 설정이 사용됩니다. Exchange 2013에서는 기본 사서함 데이터베이스 할당량 제한은 다음과 같습니다.

  - *경고 보내기 할당량*: 1.9GB

  - *보내기 금지 할당량*: 2GB

  - *받기 금지 할당량*: 2.3GB

사서함 데이터베이스 할당량을 찾아보려면 [Get-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb124924\(v=exchg.150\)) cmdlet을 실행합니다.

공용 폴더 사서함에 대해 할당량을 설정하려면 [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\)) cmdlet을 사용합니다.

## 재해 복구

Exchange 2013 공용 폴더는 사서함 인프라에 구축되며 가용성 및 중복에 대해 같은 메커니즘을 사용합니다. 모든 공용 폴더 사서함은 일반 사서함과 마찬가지로 자동 장애 조치(failover)가 포함된 여러 중복 복사본을 포함할 수 있습니다. 자세한 내용은 [고가용성 및 사이트 복구](high-availability-and-site-resilience-exchange-2013-help.md)를 참조하십시오.

전체 재해 복구 시나리오 외에도 다음과 같은 상황에서도 공용 폴더를 복원할 수 있습니다.

  - **일시적으로 삭제된 공용 폴더 복원**   공용 폴더가 삭제되었지만 아직 보존 기간에 포함됩니다.

  - **일시적으로 삭제된 공용 폴더 사서함 복원**   공용 폴더 사서함이 삭제되었지만 아직 사서함 보존 기간에 포함됩니다.

  - **복구 데이터베이스로부터 공용 폴더 사서함 복원**   삭제된 사서함 보존 기간이 경과된 경우 백업을 통해 개별 공용 폴더 사서함을 복구할 수 있습니다. 그런 다음 복원된 사서함에서 데이터를 추출하여 대상 폴더에 복사하거나 다른 사서함과 병합합니다.

이러한 모든 상황에서 공용 폴더나 공용 폴더 사서함은 **MailboxRestoreRequest** cmdlet을 사용하여 복구할 수 있습니다.

자세한 내용은 [실패 한 이동에서 공용 폴더 및 공용 폴더 사서함 복원](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)을 참조하십시오.

