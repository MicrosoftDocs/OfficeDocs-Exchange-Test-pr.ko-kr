---
title: '데이터베이스 가용성 그룹에 대 한 자동 다시 시드를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 데이터베이스 가용성 그룹에 대 한 자동 다시 시드를 구성 합니다.
ms:assetid: 4a8bd779-b52a-40ed-8040-4d76eabeb41e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ619303(v=EXCHG.150)
ms:contentKeyID: 50483043
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 가용성 그룹에 대 한 자동 다시 시드를 구성 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-04-15_

자동 다시 시드는 디스크 오류가 발생한 후 데이터베이스 중복성을 빠르게 복원하는 기능입니다. 디스크 오류가 발생하면 해당 디스크에 저장된 데이터베이스 복사본이 사서함 서버의 미리 구성된 예비용 디스크에 자동으로 다시 시드됩니다. 이 항목의 단계에 따라 DAG(데이터베이스 가용성 그룹)에 대해 자동 다시 시드를 구성할 수 있습니다.


> [!WARNING]
> 자동 다시 시드 기능은 필수 구성 작업을 수행하지 않습니다. 올바른 디스크 설치, 시스템에 예비용 디스크 추가, 불량 디스크 교체 및 새 디스크 포맷 작업은 관리자가 직접 수행해야 합니다.



DAG와 관련된 추가 관리 작업에 대한 자세한 내용은 [데이터베이스 가용성 그룹 관리](managing-database-availability-groups-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 10분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "데이터베이스 사용 가능 그룹" 항목

  - 실제 디스크당 하나의 논리 디스크/파티션을 만들어야 합니다.

  - 아래 단계에서 설명하는 특정 데이터베이스 및 로그 폴더 구조를 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 어떻게 해야 합니까?

## 1단계: 데이터베이스 및 볼륨의 루트 경로 구성

1단계에서는 DAG에 사용되는 데이터베이스(*AutoDagDatabasesRootFolderPath*) 및 볼륨(*AutoDagVolumesRootFolderPath*)의 루트 디렉터리를 구성합니다. 기본값은 각각 C:\\ExchangeDatabases와 C:\\ExchangeVolumes입니다. 기본 경로를 사용하는 경우 이 단계를 생략할 수 있습니다.

이 예에서는 데이터베이스의 루트 경로를 구성하는 방법을 보여줍니다.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabasesRootFolderPath "C:\ExchDbs"

이 예에서는 저장소 볼륨의 루트 경로를 구성하는 방법을 보여줍니다.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagVolumesRootFolderPath "C:\ExchVols"

## 이 단계의 작동 여부는 어떻게 확인합니까?

데이터베이스 및 볼륨의 루트 경로가 구성되었는지 확인하려면 다음 명령을 실행합니다.

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

*AutoDagDatabasesRootFolderPath* 및 *AutoDagVolumesRootFolderPath*의 출력에 구성된 경로가 반영되어야 합니다.

## 2단계: 볼륨당 데이터베이스 수 구성

다음으로, DAG에 대해 볼륨당 데이터베이스 수(*AutoDagDatabaseCopiesPerVolume*)를 구성합니다.

이 예에서는 볼륨당 4개의 데이터베이스가 구성된 DAG에 대해 이 자동 다시 시드 설정을 구성하는 방법을 보여줍니다.

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabaseCopiesPerVolume 4

## 이 단계의 작동 여부는 어떻게 확인합니까?

볼륨당 데이터베이스 수가 구성되었는지 확인하려면 다음 명령을 실행합니다.

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

*AutoDagDatabaseCopiesPerVolume*의 출력에 구성된 값이 반영되어야 합니다.

## 3단계: 데이터베이스 및 볼륨의 루트 디렉터리 만들기

다음으로, 1단계에서 구성한 루트 디렉터리에 해당하는 디렉터리를 만듭니다. 이 예에서는 명령 프롬프트를 사용하여 기본 디렉터리를 만드는 방법을 보여줍니다.

    md C:\ExchangeDatabases
    md C:\ExchangeVolumes

## 이 단계의 작동 여부는 어떻게 확인합니까?

데이터베이스 및 볼륨의 루트 디렉터리가 구성되었는지 확인하려면 다음 명령을 실행합니다.

    Dir C:\

만든 디렉터리가 출력 목록에 나타나야 합니다.

## 4단계: 볼륨 폴더 탑재

예비 볼륨을 포함하여 데이터베이스에 사용되는 모든 볼륨에 대해 Windows 디스크 관리 응용 프로그램(diskmgmt.msc)을 사용하여 각 볼륨을 C:\\ExchangeVolumes\\ 아래의 탑재된 폴더에 탑재합니다. 예를 들어, 데이터베이스가 포함된 두 개의 볼륨과 한 개의 예비 볼륨이 있는 경우 다음 탑재 폴더에 볼륨을 탑재합니다.

  - C:\\ExchangeVolumes\\Volume1

  - C:\\ExchangeVolumes\\Volume2

  - C:\\ExchangeVolumes\\Volume3

폴더가 루트 볼륨의 경로에서 탑재된 경우 탑재된 폴더의 이름은 아무 이름으로나 설정할 수 있습니다.

## 이 단계의 작동 여부는 어떻게 확인합니까?

볼륨 폴더가 탑재되었는지 확인하려면 다음 명령을 실행합니다.

    Dir C:\

탑재된 볼륨이 출력 목록에 나타나야 합니다.

## 5단계: 데이터베이스 폴더 만들기

다음으로, 루트 경로 C:\\ExchangeDatabases 아래에 데이터베이스 디렉터리를 만듭니다. 이 예에서는 각 볼륨에서 4개의 데이터베이스가 있는 저장소 구성에 대해 디렉터리를 만드는 방법을 보여줍니다.

    md c:\ExchangeDatabases\db001

    md c:\ExchangeDatabases\db002

    md c:\ExchangeDatabases\db003

    md c:\ExchangeDatabases\db004

## 이 단계의 작동 여부는 어떻게 확인합니까?

데이터베이스 폴더가 탑재되었는지 확인하려면 다음 명령을 실행합니다.

    Dir C:\ExchangeDatabases

만든 디렉터리가 출력 목록에 나타나야 합니다.

## 6단계: 데이터베이스 탑재 지점 만들기

각 데이터베이스에 대한 탑재 지점을 만들고 탑재 지점을 올바른 볼륨에 연결합니다. 예를 들어 db001에 대한 탑재된 폴더는 C:\\ExchangeDatabases\\db001에 있어야 합니다. 이렇게 하려면 diskmgmt.msc 또는 mountvol.exe를 사용합니다. 이 예에서는 mountvol.exe를 사용하여 db001을 C:\\ExchangeDatabases\\db001에 탑재하는 방법을 보여줍니다.

    Mountvol.exe c:\ExchangeDatabases\db001 \\?\Volume (GUID)

## 이 단계의 작동 여부는 어떻게 확인합니까?

데이터베이스 탑재 지점이 만들어졌는지 확인하려면 다음 명령을 실행합니다.

    Mountvol.exe C:\ExchangeDatabases\db001 /L

탑재된 볼륨이 탑재 지점 목록에 나타나야 합니다.

## 7단계: 데이터베이스 디렉터리 구조 만들기

다음으로, 5단계에서 만든 폴더 아래에 디렉터리를 두 개 만듭니다. 하나는 데이터베이스용이고 다른 하나는 같은 볼륨에 저장될 각 데이터베이스의 로그 스트림용입니다. 디렉터리 구조에 대해 다음 형식을 사용해야 합니다.

C:\\\< *DatabaseFolderName*\>\\*DatabaseName*\\\<*DatabaseName*\>.db

C:\\\< *DatabaseFolderName*\>\\*DatabaseName*\\\<*DatabaseName*\>.log

이 예에서는 볼륨 1에 저장될 4개의 데이터베이스에 대해 디렉터리를 만드는 방법을 보여줍니다.

    md c:\ExchangeDatabases\db001\db001.db

    md c:\ExchangeDatabases\db001\db001.log

    md c:\ExchangeDatabases\db002\db002.db

    md c:\ExchangeDatabases\db002\db002.log

    md c:\ExchangeDatabases\db003\db003.db

    md c:\ExchangeDatabases\db003\db003.log

    md c:\ExchangeDatabases\db004\db004.db

    md c:\ExchangeDatabases\db004\db004.log

모든 볼륨의 데이터베이스에 대해 위의 명령을 반복합니다.

## 이 단계의 작동 여부는 어떻게 확인합니까?

데이터베이스 디렉터리 구조가 만들어졌는지 확인하려면 다음 명령을 실행합니다.

    Dir C:\ExchangeDatabases /s

만든 디렉터리가 출력 목록에 나타나야 합니다.

## 8단계: 데이터베이스 만들기

적절한 폴더로 구성된 로그 및 데이터베이스 경로로 데이터베이스를 만듭니다. 이 예에서는 새로 만든 디렉터리 및 탑재 지점 구조에 저장될 데이터베이스를 만드는 방법을 보여줍니다.

    New-MailboxDatabase -Name db001 -Server MBX1 -LogFolderPath C:\ExchangeDatabases\db001\db001.log -EdbFilePath C:\ExchangeDatabases\db001\db001.db\db001.edb

## 이 단계의 작동 여부는 어떻게 확인합니까?

데이터베이스가 적절한 폴더에 만들어졌는지 확인하려면 다음 명령을 실행합니다.

    Get-MailboxDatabase db001 | Format List *path*

반환된 데이터베이스 속성은 데이터베이스 파일 및 로그 파일이 위의 폴더에 저장됨을 나타내야 합니다.

## 이 작업의 작동 여부는 어떻게 확인합니까?

DAG에 대해 자동 다시 시드가 구성되었는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행하여 DAG가 제대로 구성되었는지 확인합니다.
    
        Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

2.  다음 명령을 실행하여 디렉터리 구조가 제대로 구성되었는지 확인합니다. 여기에 사용된 경로는 기본 경로이며 필요한 경우 실제 사용하는 경로로 바꿉니다.
    
        Dir c:\ExchangeDatabases /s
    
        Dir c:\ExchangeVolumes /s

