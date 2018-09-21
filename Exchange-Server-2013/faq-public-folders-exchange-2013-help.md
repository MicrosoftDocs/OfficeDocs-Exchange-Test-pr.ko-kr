---
title: 'FAQ: 공용 폴더: Exchange 2013 Help'
TOCTitle: 'FAQ: 공용 폴더'
ms:assetid: 1cdcdcb7-f11b-45ca-ad23-7c38f640208c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ552408(v=EXCHG.150)
ms:contentKeyID: 50482641
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# FAQ: 공용 폴더

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-03-27_

이 항목에서는 Exchange Server 2013의 공용 폴더에 관련된 자주 묻는 질문의 목록을 제공합니다. 공용 폴더에 대한 자세한 내용은 [공용 폴더](public-folders-exchange-2013-help.md)를 참조하십시오.

여기에 답변되지 않은 공용 폴더에 대한 궁금한 점이 있습니까? [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com)으로 전자 메일을 보내십시오.

## 공용 폴더 마이그레이션에 대한 FAQ

이 섹션에서는 공용 폴더 마이그레이션에 대 한 질문과 대답 합니다. 자세한 내용은 [마이그레이션 일괄 처리를 사용 하 여 이전 버전에서 Exchange 2013 공용 폴더 마이그레이션](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md), [마이그레이션 일괄 처리를 사용 하 여 Office 365 및 Exchange Online으로 레거시 공용 폴더 마이그레이션](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/batch-migration-of-legacy-public-folders)또는 [마이그레이션 일괄 처리를 사용 하 여 Exchange Online으로 Exchange 2013 공용 폴더 마이그레이션](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/batch-migration-of-exchange-2013-public-folders)를 참조 하십시오.

## 지원 되는 공용 폴더 마이그레이션 시나리오는 무엇입니까?

다음 목록에는 Exchange 2013 또는 Exchange Online에 공용 폴더 마이그레이션에 대 한 사용 가능한 옵션에 자세히 설명 합니다.

  - Exchange 2007 공용 폴더 (SP3 RU15 이상) Exchange 2013 또는 Exchange Online으로 마이그레이션될 수 있습니다.

  - Exchange 2010 공용 폴더 (SP3 RU8 이상) Exchange 2013 또는 Exchange Online으로 마이그레이션될 수 있습니다.

  - Exchange 2013 공용 폴더 (CU15 이상) Exchange Online으로 마이그레이션될 수 있습니다.

동일한 Active Directory 포리스트에 Exchange 2013 현재 유일한 마이그레이션이 지원 됩니다. 크로스 포리스트 마이그레이션 나중에 지원 됩니다.

## 마이그레이션 후 원본 Exchange 2010 서버의 계층 구조는 어떻게 됩니까?

마이그레이션의 완료 작업 단계에서 원본 서버는 사용자가 액세스하지 못하도록 잠깁니다. 이 잠금은 마이그레이션이 완료된 후 사용자가 원본 공개 폴더에 액세스하지 못하도록 하기 위해 유지됩니다. 이 잠금을 해제할 수는 있지만 변경 내용이 Exchange 2013에 동기화되지 않으므로 권장하지 않습니다.

## 공용 폴더를 마이그레이션하는 경우 기존 공용 폴더 규칙에 변화가 있습니까?

공용 폴더 규칙은 데이터와 함께 마이그레이션되며 사서함 규칙으로 변환되지 않고 공용 폴더 규칙으로 유지됩니다.

## 초기 .csv 파일이 생성된 후 소스의 계층 구조를 변경하면 어떻게 됩니까? 이 변경 내용이 대상에 어떻게 반영됩니까?

.csv 파일은 원본 계층 구조와 대상 사서함 간의 매핑을 확인하는 데 사용됩니다. 여기에는 최상위 폴더만 포함됩니다. 최상위 폴더 아래의 자식 폴더는 자동으로 마이그레이션됩니다. 따라서 새 자식 폴더가 추가되면 프로세스 중에 마이그레이션됩니다. 새로운 최상위 폴더가 생성되면 이 폴더는 계층 구조의 쓰기 가능한 복사본이 포함된 사서함에 생성됩니다.

## Exchange 2013 공용 폴더로 마이그레이션하는 동안 일시 중단 후 완료될 때까지의 시간이 너무 오래 걸릴 경우 최종 동기화 동안 사용자가 공용 폴더에 액세스할 수 있도록 델타 동기화를 강제 수행하려면 어떻게 해야 합니까?

다음 셸 명령을 실행하면 완료 전에(소스를 잠그기 전에) 델타 동기화를 강제로 수행할 수 있습니다.

```powershell
Resume-PublicFolderMigrationRequest \PublicFolderMigration
```

구문과 매개 변수에 대한 자세한 내용은 [Resume-PublicFolderMigrationRequest](https://technet.microsoft.com/ko-kr/library/jj218689\(v=exchg.150\))를 참조하십시오.

## 지리적으로 분산된 계층 구조를 마이그레이션할 때 공용 폴더가 대상 사용자에게 가장 가까운 위치에 생성되도록 하려면 어떻게 해야 합니까?

마이그레이션 프로세스의 일환으로 `publicfoldertomailboxmapgenerator.ps1` 스크립트를 사용하여 .csv 파일이 생성됩니다. 이 파일에는 새 계층 구조에 대한 폴더와 사서함 매핑이 포함되어 있습니다. 그러면 이 .csv 파일을 사용하여 적절한 지리적 위치에 공용 폴더 사서함을 만들고, 필요한 폴더가 대상 사용자에게 가까운 적절한 사서함에 포함되도록 이 파일을 수정할 수 있습니다.

입력 .csv 파일은 \<*Exchange Installation Directory*\>\\V15\\Scripts 디렉터리에 있는 `AggregatePFData.ps1` 스크립트를 실행하여 생성할 수 있습니다. 다음과 같이 스크립트를 실행합니다.

    .\AggregatePFData.ps1 | Select-Object -property @{Name="FolderName"; Expression = {$_.Identity}}, @{Name="FolderSize"; Expression = {$_.TotalItemSize.Value.ToBytes()}} | Export-CSV -Path <Path followed by the name of the CSV>

## 기존 공용 폴더 사용 권한은 마이그레이션됩니까?

예, 사용 권한은 데이터와 함께 폴더 수준에서 자동으로 마이그레이션됩니다. 이 단계를 별도로 수행할 필요가 없습니다.

## 공용 폴더는 더 이상 사용하지 않습니까?

아니요. 공용 폴더는 Outlook 통합, 간단한 공유 시나리오 및 동일한 데이터에 액세스할 수 있는 다수 사용자에게 편리한 기능입니다.

## 공용 폴더를 지원하는 클라이언트는 무엇입니까?

Outlook 2007/2010/2013 및 Outlook 2011 for Mac 사용자는 공용 폴더에 액세스할 수 있습니다. 그렇지만 해당 사서함이 Exchange 2013 서버에 있는 사용자는 Outlook for Mac과 같이 EWS(Exchange Web Services)를 사용하는 클라이언트에서 Exchange 2007 또는 Exchange 2010 공용 폴더에 연결할 수 없습니다. 이러한 사용자의 액세스 권한을 유지하려면 레거시 공용 폴더를 Exchange 2013으로 마이그레이션하는 것이 좋습니다.

## 클라이언트의 제한 사항이 있습니까?

Outlook Web App은 지원 되지만 일부 제한 된 합니다. 추가 하 고 하 고 (메일, 게시, 일정 및 연락처 공용 폴더 경우) 즐겨찾기 공용 폴더를 제거 하 고, 만들기, 편집, 게시물, 삭제 및 게시물에 회신 하기 예: 항목 수준 작업을 수행할 수 있습니다. 하지만 Outlook Web App에서 다음을 수행할 수 없습니다.

  - 공용 폴더 만들기 또는 삭제

  - 내용 끌어서 놓기

  - 이전 버전의 Exchange가 실행되는 서버에 있는 공용 폴더에 액세스


> [!NOTE]
> 만 요소 <STRONG>특정 서식 파일을 사용 하 여 회신</STRONG> 메일 사용이 가능한 공용 폴더에 포함 된 공용 폴더 규칙을 만들 수 있습니다. 것이 <STRONG>특정 서식 파일을 사용 하 여 회신</STRONG> 을 포함 하는 기존 규칙을 계속 하 여 메일 사용 가능 공용 폴더에서 수행할 수 있지만 해당 폴더에이 서식 파일 요소를 사용 하 여 새 규칙 만들기 또는이 요소와 기존 규칙을 편집할 수는 없습니다.



하이브리드 시나리오에서 크로스-프레미스 공용 폴더에 대 한 웹에 있는 Outlook 및 Outlook 2011 for Mac 지원 되지 않습니다. 사용자가 Outlook 2011와 Mac 또는 웹에서 Outlook에 대 한 액세스를 공용 폴더와 같은 위치에 있어야 합니다. Mac 용 Outlook 2016의 사용자가 [하이브리드 배포 절차](https://technet.microsoft.com/en-us/library/jj200788\(v=exchg.150\).aspx) 아래 절차를 진행 않으면 및 Mac 용 Outlook 2016 년 4 월 2016 업데이트가 모든 클라이언트에 설치 하는 경우 하이브리드 시나리오에서는 공용 폴더에 액세스할 수 있습니다.

## 매우 큰 계층 구조를 공용 폴더 사서함에 저장하려면 어떻게 합니까?

공용 폴더 저장소 제한에 대한 자세한 내용은 [공용 폴더의 제한](limits-for-public-folders-exchange-2013-help.md)을 참조하세요.

## 계층 구조 공용 폴더 사서함은 어떻게 볼 수 있습니까?

다음 명령을 실행합니다.

```powershell
Get-OrganizationConfig | Format-List RootPublicFolderMailbox
```

구문과 매개 변수에 대한 자세한 내용은 [Get-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997571\(v=exchg.150\))를 참조하세요.

## Exchange 관리 셸 cmdlet을 사용하여 공용 폴더에 대한 콘텐츠 사서함을 만들려면 어떻게 해야 합니까?

다음 명령을 실행하여 첫 번째 마스터 계층 구조 공용 폴더 사서함과 두 번째 계층 구조 사서함을 만듭니다.

```powershell
New-Mailbox -PublicFolder -Name <name of public folder>
```

자세한 내용은 [공용 폴더 만들기](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/create-public-folder)를 참조하세요.

## 이전 버전의 Exchange에서는 각 사서함 데이터베이스마다 공용 폴더 데이터베이스를 지정하는 옵션이 있었습니다. 이 기능은 Exchange 2013에서 어떤 방식으로 작동합니까?

Exchange 2013에는 데이터베이스 수준 설정이 없습니다. Exchange 2013에는 공용 폴더 사서함을 지정할 수 있는 사서함 수준 기능이 있지만 기본적으로 Exchange는 사용자별 계층 구조 사서함을 자동 계산합니다.

## Exchange 2013에서는 공용 폴더 메트릭 도구가 어떻게 사용됩니까?

Exchange 2013에서는 [Get-PublicFolderStatistics](https://technet.microsoft.com/ko-kr/library/aa998663\(v=exchg.150\)) 및 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/ko-kr/library/ee332344\(v=exchg.150\)) cmdlet을 사용하여 공용 폴더 메트릭 데이터를 가져올 수 있습니다. 이 방법은 Exchange 2010에서와 동일하므로 변경된 사항은 없습니다. 공용 폴더에는 추가적인 보고 추가 기능이 필요하지 않습니다.

## 공용 폴더는 공용 폴더에 대한 내부 액세스와 타사 액세스를 구분할 수 있습니까?

Exchange 2013에서 공용 폴더 사용 권한은 RBAC(역할 기반 액세스 제어)를 사용하여 관리됩니다. ACL(액세스 제어 목록)은 Exchange 2013에서 사용되지 않습니다. [Get-PublicFolderStatistics](https://technet.microsoft.com/ko-kr/library/aa998663\(v=exchg.150\)) 및 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/ko-kr/library/ee332344\(v=exchg.150\)) cmdlet을 사용하여 관리 작업을 수행하는 계정을 추적하고 그에 따라 액세스를 감사할 수 있습니다. RBAC에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참조하십시오.

## 사서함 감사 로깅이 공용 폴더에 대해서 작동합니까?

현재로서는 작동하지 않습니다.

## 공용 폴더에 대한 제한은 무엇이며 권장 사항은 무엇입니까?

공용 폴더 제한에 대한 자세한 내용은 [공용 폴더의 제한](limits-for-public-folders-exchange-2013-help.md)을 참조하세요.

## 공용 폴더 사서함 분할에 대한 권장 사항은 무엇입니까? 분할된 공용 폴더 사서함이 동일한 데이터베이스에 있어야 합니까?

이전 버전의 Exchange에서는 전체 공용 폴더 데이터베이스에 대해 공용 폴더를 분할할 수 있습니다. 또한 공용 폴더 사서함의 콘텐츠를 같은 사서함 데이터베이스에 분할할지, 다른 데이터베이스에 분할할지를 결정할 수 있습니다. 일반적으로 저장소와 입출력 간의 균형을 유지해야 하므로 분할된 폴더를 별도의 데이터베이스에 두는 것이 좋습니다.

## 공용 폴더에 보존 정책을 설정할 수 있습니까?

마찬가지로 이전 버전의 Exchange 보존 제한을 항목에 대해 설정할 수 있습니다. 자세한 내용은 [공용 폴더의 제한](limits-for-public-folders-exchange-2013-help.md)를 참조 합니다.

## 특정 공용 폴더 사서함을 사용할 수 있는 사용자를 지정할 수 있습니까?

Exchange 2007 및 Exchange 2010에서는 특정 공용 폴더에 대한 액세스 권한을 가진 사용자를 지정할 수 있었습니다. Exchange 2013에서는 사용자별로 기본 공용 폴더 사서함을 설정할 수 있습니다. 이렇게 하려면 *DefaultPublicFolderMailbox* 매개 변수를 사용하여 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) cmdlet을 실행합니다.

```powershell
Set-Mailbox -Identity kweku@contoso.com -DefaultPublicFolderMailbox "PF_Administration"
```

## 마스터 계층 구조가 중단되면 사용자에게 어떤 영향이 미칩니까?

마스터 계층 구조 공용 폴더 사서함이 다운되더라도 사용자는 공용 폴더를 볼 수 있지만 공용 폴더에 쓸 수는 없습니다. 계층 구조 작동이 중단되지 않도록 하는 데 도움이 되도록 공용 폴더를 DAG(데이터베이스 사용 가능 그룹)에 포함하는 것이 좋습니다. DAG에 대한 자세한 내용은 [DAG(데이터베이스 가용성 그룹)](database-availability-groups-dags-exchange-2013-help.md)을 참조하십시오.

## 마스터 계층 구조 사서함인 공용 폴더 사서함을 변경할 수 있습니까?

아니요. 마스터 계층 구조 사서함을 변경하려고 하면 오류가 나타납니다.

## 공용 폴더에는 전체 텍스트 검색 기능이 있습니까?

예, Exchange 2013의 공용 폴더에서는 전체 텍스트를 검색할 수 있습니다. 그러나 여러 공용 폴더에서 검색할 수는 없습니다.

