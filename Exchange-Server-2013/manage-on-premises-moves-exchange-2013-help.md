---
title: '온-프레미스 이동 관리: Exchange 2013 Help'
TOCTitle: 온-프레미스 이동 관리
ms:assetid: 1691b658-f5af-49c6-9170-5c3cb66c7306
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150487(v=EXCHG.150)
ms:contentKeyID: 50482559
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 온-프레미스 이동 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-25_

이동 요청은 한 사서함 데이터베이스에서 다른 사서함 데이터베이스로 사서함을 이동하는 프로세스입니다. 로컬 이동 요청은 단일 포리스트 내에서 발생하는 사서함 이동입니다. Microsoft Exchange Server 2013에서 사서함 및 개인 보관 사서함은 별도의 데이터베이스에 있을 수 있습니다. 이동 요청 기능을 사용하면 기본 사서함 및 연관된 사서함을 같은 데이터베이스 또는 별도의 데이터베이스로 이동할 수 있습니다. 이 항목의 절차는 온-프레미스 사서함 이동에 도움이 됩니다.

다음 절차를 사용하면 온-프레미스 조직에서 사서함을 이동할 수 있습니다. 이 절차에서는 Exchange 관리 셸 및 EAC(Exchange 센터)를 사용합니다.

이동 요청을 사용하여 사서함을 이동하면 다음의 두 서비스에 의해 이동 요청이 처리됩니다.

  - Microsoft Exchange 사서함 복제 서비스

  - Microsoft Exchange 사서함 복제 프록시

사서함 복제 서버 및 프록시에 대한 자세한 내용은 [MRS 프록시에 대 한 자세한 내용은](https://technet.microsoft.com/ko-kr/library/jj156451\(v=exchg.150\))를 참조하십시오.

사서함 이동에 대한 자세한 내용은 [Exchange 2013 사서함 이동](mailbox-moves-in-exchange-2013-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 20분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 이동 및 마이그레이션 권한" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 사서함 이동 준비 여부 테스트

이 예에서는 *WhatIf* 스위치를 사용하여 Tony Smith의 사서함을 새로운 데이터베이스 DB01로 이동할 준비가 되었는지 여부와 명령 내에 오류가 있는지 여부를 테스트합니다. *WhatIf* 스위치를 사용하면 사서함에 대해 확인 작업이 수행됩니다. 사서함 이동 준비가 되지 않았으면 오류가 발생합니다.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase DB01 -WhatIf

구문과 매개 변수에 대한 자세한 내용은 [New-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219166\(v=exchg.150\)) 및 [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))을 참조하십시오.

## 로컬 이동 요청 만들기

## EAC를 사용하여 로컬 이동 요청 만들기

로컬 이동 요청을 만들려면 EAC에 로그인하고 다음 단계를 수행합니다.

1.  EAC에서 **받는 사람** \> **마이그레이션**으로 이동한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 로컬 사서함 이동** 마법사에서 이동할 사용자를 선택하고 **확인**을 클릭한 후 **다음**을 클릭합니다.

3.  **이동 구성** 페이지에서 새 배치의 이름을 구성합니다. 보관 사서함에 대해 원하는 옵션과 사서함 데이터베이스 위치를 선택하고 **새로 만들기**를 클릭합니다.

## 셸을 사용하여 로컬 이동 요청 만들기

로컬 이동 요청을 만드는 방법의 예를 보려면 [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))의 예 2를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

마이그레이션이 완료되었는지 확인하려면 다음을 수행합니다.

  - EAC에서 **받는 사람** \> **마이그레이션**으로 이동합니다.

  - EAC에서 **모든 배치에 대한 상태**를 클릭하여 이동에 성공했는지 확인합니다.

  - 셸에서 다음 명령을 실행하여 사서함 이동 정보를 검색합니다.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

자세한 내용은 [Get-MigrationUserStatistics](https://technet.microsoft.com/ko-kr/library/jj218695\(v=exchg.150\))를 참조하십시오.

## 일괄 이동 요청 만들기

## EAC를 사용하여 일괄 이동 요청 만들기

EAC에 로그인하고 다음 단계를 수행합니다.

1.  EAC에서 **받는 사람** \> **마이그레이션**으로 이동한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 로컬 사서함 이동** 마법사에서 이동할 사용자를 선택하고 **확인**을 클릭한 후 **다음**을 클릭합니다.

3.  **이동 구성** 페이지에서 새 배치의 이름을 구성합니다. 보관 사서함에 대해 원하는 옵션과 사서함 데이터베이스 위치를 선택하고 **새로 만들기**를 클릭합니다.

> [!CAUTION]
> 잘못된 항목 제한을 50개 항목보다 많이 설정하지 않도록 하십시오. 이렇게 설정하는 경우에는 이동이 실패할 수 있습니다. 잘못된 항목 제한을 50개 항목보다 많이 설정하려면 Exchange 관리 셸을 사용하여 –<em>AcceptLargeDataLoss</em> 매개 변수를 true로 설정해야 합니다.


## 셸을 사용하여 일괄 이동 요청 만들기

이 예에서는 지정된 .csv 파일의 사서함이 다른 사서함 데이터베이스로 이동되는 로컬 이동을 위한 마이그레이션 일괄 처리를 만듭니다. 이 .csv 파일에는 이동될 각 사서함의 전자 메일 주소가 있는 단일 열이 포함되어 있습니다. 이 열의 헤더 이름은 **EmailAddress**로 지정해야 합니다. 이 예의 마이그레이션 일괄 처리는 **Start-MigrationBatch** cmdlet이나 EAC(Exchange 관리 센터)를 사용하여 수동으로 시작해야 합니다. 또는 *AutoStart* 매개 변수를 사용하여 마이그레이션 일괄 처리를 자동으로 시작할 수 있습니다.

```
New-MigrationBatch -Local -Name LocalMove1 -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\LocalMove1.csv")) -TargetDatabases MBXDB2 -TimeZone "Pacific Standard Time"
```

```
Start-MigrationBatch -Identity LocalMove1
```

구문과 매개 변수에 대한 자세한 내용은 [New-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219166\(v=exchg.150\)) 및 [Start-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219165\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

마이그레이션이 완료되었는지 확인하려면 다음을 수행합니다.

  - EAC에서 **모든 배치에 대한 상태**를 클릭하여 이동에 성공했는지 확인합니다.

  - 셸에서 다음 명령을 실행하여 사서함 이동 정보를 검색합니다.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

자세한 내용은 [Get-MigrationUserStatistics](https://technet.microsoft.com/ko-kr/library/jj218695\(v=exchg.150\))를 참조하십시오.

## 마이그레이션 일괄 처리 표시

셸을 사용하여 마이그레이션 일괄 처리를 표시하는 방법에 대한 예를 보려면 [Get-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219164\(v=exchg.150\))의 예 2를 참조하십시오.

## 사용자의 기본 사서함만 이동

## EAC를 사용하여 사용자의 기본 사서함만 이동

1.  EAC에서 **받는 사람** \> **마이그레이션**으로 이동한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 로컬 사서함 이동** 마법사에서 기본 사서함을 이동할 사용자를 선택하고 **확인**을 클릭한 후 **다음**을 클릭합니다.

3.  **이동 구성** 페이지에서 새 배치의 이름을 구성합니다. **기본 사서함만 이동**을 선택하고 사서함 데이터베이스 위치에 대한 옵션을 선택한 다음 **새로 만들기**를 클릭합니다.

## 셸을 사용하여 사용자의 기본 사서함만 이동

이 예에서는 Tony Smith의 기본 사서함만 DB01로 이동합니다. 보관 데이터는 이동되지 않습니다.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -PrimaryOnly -TargetDatabase "DB01"

구문과 매개 변수에 대한 자세한 내용은 [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

마이그레이션이 완료되었는지 확인하려면 다음을 수행합니다.

  - EAC에서 **모든 일괄 처리에 대한 상태**를 클릭합니다.

  - 셸에서 다음 명령을 실행하여 사서함 이동 정보를 검색합니다.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

자세한 내용은 [Get-MigrationUserStatistics](https://technet.microsoft.com/ko-kr/library/jj218695\(v=exchg.150\))를 참조하십시오.

## .csv 일괄 처리 파일을 사용하여 포리스트 간 이동 만들기

이 예에서는 마이그레이션 끝점을 구성한 다음 .csv 파일을 사용하여 원본 포리스트에서 대상 포리스트로의 포리스트 간 일괄 이동을 만듭니다.

```
New-MigrationEndpoint -Name Fabrikam -ExchangeRemote -Autodiscover -EmailAddress tonysmith@fabrikam.com -Credentials (Get-Credential fabrikam\tonysmith) 
```

```
$csvData=[System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\batch.csv")
New-MigrationBatch -CSVData $csvData -Timezone "Pacific Standard Time" -Name FabrikamMerger -SourceEndpoint Fabrikam -TargetDeliveryDomain "mail.contoso.com"
```

포리스트 간 이동을 위한 포리스트 준비에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [크로스 포리스트 이동 요청에 대 한 사서함을 준비](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [예제 코드를 사용 하 여 크로스 포리스트 이동에 대 한 사서함을 준비](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

  - [셸에서 준비 MoveRequest.ps1 스크립트를 사용 하 여 크로스 포리스트 이동에 대 한 준비 사서함](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

구문과 매개 변수에 대한 자세한 내용은 [New-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219166\(v=exchg.150\)) 및 [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

마이그레이션이 완료되었는지 확인하려면 다음을 수행합니다.

  - 셸에서 다음 명령을 실행하여 사서함 이동 정보를 검색합니다.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

자세한 내용은 [Get-MigrationUserStatistics](https://technet.microsoft.com/ko-kr/library/jj218695\(v=exchg.150\))를 참조하십시오.

## 보관 사서함만 이동

## EAC를 사용하여 보관 사서함만 이동

1.  EAC에서 **받는 사람** \> **마이그레이션**으로 이동한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 로컬 사서함 이동** 마법사에서 보관 사서함을 이동할 사용자를 선택하고 **확인**을 클릭한 후 **다음**을 클릭합니다.

3.  **이동 구성** 페이지에서 새 배치의 이름을 구성합니다. **보관 사서함만 이동**을 선택하고 사서함 데이터베이스 위치에 대한 옵션을 선택한 다음 **새로 만들기**를 클릭합니다.

## 셸을 사용하여 보관 사서함만 이동

이 예에서는 Tony Smith의 보관 사서함만 DB03으로 이동합니다. 기본 사서함은 이동되지 않습니다.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -ArchiveOnly -ArchiveTargetDatabase "DB03"

구문과 매개 변수에 대한 자세한 내용은 [New-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219166\(v=exchg.150\)) 및 [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

마이그레이션이 완료되었는지 확인하려면 다음을 수행합니다.

  - 셸에서 다음 명령을 실행하여 사서함 이동 정보를 검색합니다.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

자세한 내용은 [Get-MigrationUserStatistics](https://technet.microsoft.com/ko-kr/library/jj218695\(v=exchg.150\))를 참조하십시오.

## 사용자의 기본 사서함 및 보관 사서함을 별도의 데이터베이스로 이동

이 예에서는 Ayla의 기본 사서함 및 보관 사서함을 별도의 데이터베이스로 이동합니다. 기본 데이터베이스는 DB01로 이동되고 보관 사서함은 DB03으로 이동됩니다.

    New-MoveRequest -Identity 'ayla@humongousinsurance.com' -TargetDatabase DB01 -ArchiveTargetDatabase -DB03

구문과 매개 변수에 대한 자세한 내용은 [New-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219166\(v=exchg.150\)) 및 [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

마이그레이션이 완료되었는지 확인하려면 다음을 수행합니다.

  - 셸에서 다음 명령을 실행하여 사서함 이동 정보를 검색합니다.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

자세한 내용은 [Get-MigrationUserStatistics](https://technet.microsoft.com/ko-kr/library/jj218695\(v=exchg.150\))를 참조하십시오.

## 사용자의 기본 사서함을 이동하고 잘못된 항목 제한을 더 많이 허용

## EAC를 사용하여 사용자의 기본 사서함을 이동하고 잘못된 항목 제한을 더 많이 허용

1.  EAC에서 **받는 사람** \> **마이그레이션**으로 이동한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 로컬 사서함 이동** 마법사에서 기본 사서함을 이동할 사용자를 선택하고 **확인**을 클릭한 후 **다음**을 클릭합니다.

3.  **이동 구성** 페이지에서 새 배치의 이름을 구성합니다. **기본 사서함만 이동**을 선택하고 사서함 데이터베이스 위치에 대한 옵션을 선택합니다.

4.  **기타 옵션** ![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘")을 클릭하고 잘못된 항목 제한을 입력한 다음 **확인**을 클릭합니다.

## 셸을 사용하여 사용자의 기본 사서함을 이동하고 잘못된 항목 제한을 더 많이 허용

이 예에서는 Lisa의 기본 사서함을 사서함 데이터베이스 DB01로 이동하고 잘못된 항목 제한을 `100`으로 설정합니다. 잘못된 항목 제한을 더 많이 설정하려면 *AcceptLargeDataLoss* 매개 변수를 사용해야 합니다.

    New-MoveRequest -Identity 'Lisa' -PrimaryOnly -TargetDatabase "DB01" -BadItemLimit 100 -AcceptLargeDataLoss

구문과 매개 변수에 대한 자세한 내용은 [New-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219166\(v=exchg.150\)) 및 [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

마이그레이션이 완료되었는지 확인하려면 다음을 수행합니다.

  - 셸에서 다음 명령을 실행하여 사서함 이동 정보를 검색합니다.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

자세한 내용은 [Get-MigrationUserStatistics](https://technet.microsoft.com/ko-kr/library/jj218695\(v=exchg.150\))를 참조하십시오.

