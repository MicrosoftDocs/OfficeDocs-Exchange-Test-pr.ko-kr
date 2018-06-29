---
title: '역할 범위 보기: Exchange 2013 Help'
TOCTitle: 역할 범위 보기
ms:assetid: 0bb3a434-6651-473a-94eb-4eb9a34e6f70
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335084(v=EXCHG.150)
ms:contentKeyID: 50482478
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 범위 보기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-03_

관리 역할 범위에서는 개체에 할당된 cmdlet과 매개 변수를 사용하여 개체를 변경할 수 있도록 사용자가 사용할 수 있는 개체를 결정합니다. 범위를 보고 조직에 추가된 범위, 특정 범위의 구성 또는 분리된 범위를 확인할 수 있습니다.

Microsoft Exchange Server 2013의 관리 역할 범위에 대한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

역할 범위와 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 범위" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목에서는 파이프라이닝과 **Format-List** cmdlet을 사용합니다. 이 개념에 대한 자세한 내용은 다음 항목을 참조하십시오.
    
      - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))
    
      - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 특정 범위 보기

**Get-ManagementScope** cmdlet의 출력을 **Format-List** cmdlet으로 파이프하여 범위의 세부 정보를 볼 수 있습니다.

특정 범위의 세부 정보를 보려면 다음 구문을 사용합니다.

    Get-ManagementScope <scope name> | Format-List

이 예에서는 Seattle Servers 범위의 세부 정보를 검색합니다.

    Get-ManagementScope "Seattle Servers" | Format-List

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd298180\(v=exchg.150\))를 참조하십시오.

## 모든 범위 표시

이 예에서는 조직의 범위 목록을 검색합니다.

    Get-ManagementScope

이 cmdlet은 배타적 범위와 일반 범위를 모두 검색합니다. 배타적 범위나 일반 범위만 반환하려면 이 항목의 뒷부분에 있는 "배타적 범위 또는 일반 범위만 모두 표시"를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd298180\(v=exchg.150\))를 참조하십시오.

## 분리된 범위 모두 표시

*분리된 범위*는 관리 역할 할당에 연결되지 않은 범위입니다.

이 예에서는 분리된 범위 목록을 검색합니다.

    Get-ManagementScope -Orphan

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd298180\(v=exchg.150\))를 참조하십시오.

## 배타적 범위 또는 일반 범위만 모두 표시

기본적으로 **Get-ManagementScope** cmdlet은 배타적 범위와 일반 범위가 모두 포함된 범위 목록을 반환합니다. 배타적 범위나 일반 범위만 반환하려는 경우 다음 구문을 사용합니다.

    Get-ManagementScope -Exclusive < $true | $false >

이 예에서는 배타적 범위만 반환합니다.

    Get-ManagementScope -Exclusive $true

이 예에서는 일반 범위 목록만 반환합니다.

    Get-ManagementScope -Exclusive $false

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd298180\(v=exchg.150\))를 참조하십시오.

