---
title: '사서함 데이터베이스 복사본 속성 구성: Exchange 2013 Help'
TOCTitle: 사서함 데이터베이스 복사본 속성 구성
ms:assetid: cf186561-ab2c-45c0-90f5-8d3ecfabeeac
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351151(v=EXCHG.150)
ms:contentKeyID: 50484187
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 데이터베이스 복사본 속성 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-01_

각 사서함 데이터베이스 복사본에는 사용자가 구성할 수 있는 자체 속성이 있습니다. 이러한 속성으로는 재생 지연 시간과 자르기 지연 시간 및 활성화 기본 설정 수가 포함됩니다. 재생 지연, 자르기 지연 및 활성화 기본 설정 수에 대한 자세한 내용은 [사서함 데이터베이스 복사본 관리](managing-mailbox-database-copies-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 데이터베이스 복사본 속성 구성

1.  EAC에서 **서버** \> **데이터베이스**로 이동합니다.

2.  구성할 데이터베이스를 선택합니다.

3.  세부 정보 창의 **데이터베이스 복사본** 아래에서 원하는 데이터베이스 복사본의 **세부 정보 보기**를 클릭한 후 다음 내용을 보거나 구성합니다.
    
      - **데이터베이스**   선택한 데이터베이스의 이름을 표시합니다.
    
      - **사서함 서버**   선택한 데이터베이스 복사본을 호스트하는 사서함 서버의 이름을 표시합니다.
    
      - **콘텐츠 인덱스 상태** 선택한 데이터베이스 복사본에 대한 콘텐츠 인덱스의 현재 상태를 표시합니다.
    
      - **상태**   선택한 데이터베이스 복사본의 현재 상태를 표시합니다.
    
      - **복사 큐 길이**   선택한 데이터베이스 복사본에 복사되기 위해 대기 중인 로그 파일 수를 나타냅니다. 이 필드는 수동 데이터베이스 복사본에만 해당합니다.
    
      - **재생 큐 길이**   선택한 데이터베이스 복사본으로 재생되기 위해 대기 중인 로그 파일 수를 나타냅니다. 이 필드는 수동 데이터베이스 복사본에만 해당합니다.
    
      - **오류 메시지**   `Failed` 또는 `Failed and Suspended` 상태인 데이터베이스 복사본에 대한 모든 오류 메시지를 표시합니다.
    
      - **사용 가능한 최신 로그 시간**   데이터베이스의 활성 복사본에 가장 최근에 생성된 로그 파일의 날짜 및 시간 스탬프를 표시합니다. 이 필드는 수동 데이터베이스 복사본에만 해당합니다. 활성 데이터베이스 복사본(복제된 데이터베이스 복사본 및 독립 실행형 데이터베이스 복사본)의 경우 이 필드에 **사용 안 함**이 표시됩니다.
    
      - **마지막으로 로그를 검사한 시간**   선택한 데이터베이스 복사본에서 LogInspector가 검사한 마지막 로그 파일의 날짜 및 시간 스탬프를 표시합니다. 이 필드는 수동 데이터베이스 복사본에만 해당합니다. 활성 데이터베이스 복사본(복제된 데이터베이스 복사본 및 독립 실행형 데이터베이스 복사본)의 경우 이 필드에 **사용 안 함**이 표시됩니다.
    
      - **마지막으로 로그를 복사한 시간**   선택한 데이터베이스 복사본에서 LogInspector가 검사한 마지막 로그 파일의 날짜 및 시간 스탬프를 표시합니다. 이 필드는 수동 데이터베이스 복사본에만 해당합니다. 활성 데이터베이스 복사본(복제된 데이터베이스 복사본 및 독립 실행형 데이터베이스 복사본)의 경우 이 필드에 **사용 안 함**이 표시됩니다.
    
      - **마지막으로 로그를 재생한 시간**   선택한 데이터베이스 복사본에 LogInspector가 재생한 마지막 로그 파일의 날짜 및 시간 스탬프를 표시합니다. 이 필드는 수동 데이터베이스 복사본에만 해당합니다. 활성 데이터베이스 복사본(복제된 데이터베이스 복사본 및 독립 실행형 데이터베이스 복사본)의 경우 이 필드에 **사용 안 함**이 표시됩니다.
    
      - **활성화 기본 설정 번호**   활성화 기본 설정 번호를 표시합니다. 이 번호는 Active Manager의 최상의 복사본 선택 프로세스의 일부로서 사용되어 RedistributeActiveDatabases.ps1 스크립트로 DAG 전체에 활성 사서함 데이터베이스를 다시 배포함으로써 DAG의 균형을 유지합니다. 활성화 기본 설정의 값이 1보다 크거나 같은 수이며, 1이 기본 설정 순서에서 맨 위입니다. 사서함 데이터베이스의 복사본 수보다 클 수 없습니다.
    
      - **재생 지연 시간(일)**   Microsoft Exchange Replication Service에서 복사한 로그 파일을 수동 데이터베이스 복사본으로 재생하기까지 Microsoft Exchange Information Store 서비스가 대기해야 할 시간을 표시합니다. 이 매개 변수를 0보다 큰 값으로 설정하면 지연된 데이터베이스 복사본이 만들어집니다. 이 값의 기본 설정은 0일입니다. 이 설정에 허용되는 최대 값은 14일이며, 최소 값은 0일입니다. 이 값을 0으로 설정하면 재생 지연이 사용되지 않습니다.

## 셸을 사용하여 사서함 데이터베이스 복사본 속성 구성

이 예에서는 3이라는 활성화 기본 설정 수를 사용하여 사서함 데이터베이스 복사본을 구성합니다.

    Set-MailboxDatabaseCopy -Identity DB3\EX3 -ActivationPreference 3

이 예에서는 재생 지연 시간과 자르기 지연 시간이 1일이고 활성화 기본 설정 수가 2인 Server1에서 호스팅하는 데이터베이스 DB1의 복사본을 구성합니다.

    Set-MailboxDatabaseCopy -Identity DB1\Server1 -ReplayLagTime 1.0:0:0 -TruncationLagTime 1.0:0:0 -ActivationPreference 2

## 작동 여부는 어떻게 확인합니까?

사서함 데이터베이스 복사본이 성공적으로 구성되었는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 **서버** \> **데이터베이스**로 이동합니다. 적절한 데이터베이스를 선택하고 세부 정보 창에서 **세부 정보 보기**를 클릭하여 데이터베이스 복사 속성을 봅니다.

  - 셸에서 다음 명령을 실행하여 데이터베이스 복사본에 대한 구성 정보를 표시합니다.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## 자세한 내용

[Set-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd298104\(v=exchg.150\))

[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ko-kr/library/dd298044\(v=exchg.150\))

[Get-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb124924\(v=exchg.150\))

