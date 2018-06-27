---
title: '역할 항목 보기: Exchange 2013 Help'
TOCTitle: 역할 항목 보기
ms:assetid: d9bb0d14-db59-456c-8f50-a8d7f7323df9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351179(v=EXCHG.150)
ms:contentKeyID: 50484356
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 항목 보기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-03_

각 관리 역할 항목에는 단일 cmdlet 또는 스크립트를 나타냅니다. 역할 항목에 포함 된 매개 변수는 사용자가 액세스할 수 있는 cmdlet 또는 스크립트 매개 변수를 결정 합니다.

역할 항목을 참조 하는 스크립트 또는 역할 항목 연관 된 관리 역할 이름 및 cmdlet의 역할 항목의 id 구성 됩니다. Microsoft Exchange Server 2013 의 역할 항목에 대 한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)을 참조 하십시오.

역할 항목에 관련 된 다른 관리 작업에 대 한 자세한 내용은? [고급 사용 권한](advanced-permissions-exchange-2013-help.md)확인할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 역할" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목 파이프라인의 사용, **Format-List** cmdlet, 개체 및 속성을 사용 하면 됩니다. 이러한 개념에 대 한 자세한 내용은 다음 항목을 참조 하십시오.
    
      - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))
    
      - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)
    
      - [구조적 데이터](https://technet.microsoft.com/ko-kr/library/aa996386\(v=exchg.150\))

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 역할 항목의 목록 보기

역할 항목의 목록을 검색 하려면 **Get-ManagementRoleEntry** cmdlet을 사용할 수 있습니다. **Get-ManagementRoleEntry** cmdlet을 사용 하는 경우에 모두 목록 하려는 역할 항목을 포함 하는 역할 이름을 cmdlet의 이름과 표시 하려는 역할 항목을 포함 하는 값을 지정 해야 합니다. 역할 이름 및 cmdlet 이름 (\*) 와일드 카드 문자를 결합 하 여 역할 항목의 특정 또는 광범위 한 목록을 반환할 수 있습니다.

자세한 구문 및 매개 변수 정보에 대 한 [Get-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd335210\(v=exchg.150\))를 참조 하십시오.

## 역할에서 모든 역할 항목의 목록을 보려면

특정 역할 중 하나를 역할 항목의 목록을 보려면 다음 구문을 사용 합니다.

    Get-ManagementRoleEntry <role name>\*

이 예제에서는 `Recipient Administrators` 역할에 대해 모든 역할 항목을 검색 합니다.

    Get-ManagementRole "Recipient Administrators\*"

자세한 구문 및 매개 변수 정보에 대 한 [Get-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd335210\(v=exchg.150\))를 참조 하십시오.

## 특정 역할 항목을 포함 하는 역할의 목록을 보려면

특정 역할 항목을 포함 하는 모든 역할의 목록을 보려면 다음 구문을 사용 합니다.

    Get-ManagementRoleEntry *\<cmdlet name>

이 예에서는 **Set-Mailbox** 역할 항목을 포함 하는 모든 역할을 검색 합니다.

    Get-ManagementRoleEntry *\Set-Mailbox

자세한 구문 및 매개 변수 정보에 대 한 [Get-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd335210\(v=exchg.150\))를 참조 하십시오.

## 비슷한 역할 항목을 포함 하는 역할의 대상된 목록 보기

이름이 비슷한 cmdlet을 포함 하는 대상으로 지정 된 역할의 목록을 보려면 다음 구문을 사용 합니다.

    Get-ManagementRoleEntry *<partial role name>*\*<partial cmdlet name>*

이 예제에서는 이름에 문자열 `Tier 1` 를 포함 하는 역할에 있는 `Mailbox` 문자열 포함 하는 역할 항목의 목록을 반환 합니다.

    Get-ManagementRoleEntry "*Tier 1*\*Mailbox*"

자세한 구문 및 매개 변수 정보에 대 한 [Get-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd335210\(v=exchg.150\))를 참조 하십시오.

## 단일 역할 항목을 보려면

단일 역할 항목의 세부 정보를 보려면 다음 구문을 사용 합니다.

    Get-ManagementRoleEntry <role name>\<cmdlet name> | Format-List

이 예제에서는 `Recipient Administrators` 역할에서 **Set-Mailbox** 역할 항목의 세부 정보를 검색합니다.

    Get-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" | Format-List

보면 역할 항목 **Format-List** cmdlet을 사용 하 여 목록에 너무 많은 매개 변수가 있으면이 항목 뒷부분에 나오는 "단일 역할 항목에서 매개 변수 보기"를 참조 합니다.

자세한 구문 및 매개 변수 정보에 대 한 [Get-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd335210\(v=exchg.150\))를 참조 하십시오.

## 단일 역할 항목에서 매개 변수를 보려면

일부 역할 항목 결과 **Format-List** cmdlet에 **Get-ManagementRoleEntry** cmdlet에 파이프 하 여 볼 수 있는 것 보다 더 많은 매개 변수를 포함 합니다. 역할 항목에서 모든 매개 변수를 보려면 해야하는 경우에 직접 역할 항목 개체의 **Parameters** 속성에 액세스 해야 합니다.

역할 항목 개체의 **Parameters** 속성에 저장 된 매개 변수를 보려면 다음 구문을 사용 합니다.

    (Get-ManagementRoleEntry <role name>\<cmdlet name>).Parameters

편지 병합 받는 사람 역할에 **Set-Mailbox** 역할 항목에서 매개 변수를 검색 하는이 예제입니다.

    (Get-ManagementRoleEntry "Mail Recipients\Set-Mailbox").Parameters

자세한 구문 및 매개 변수 정보에 대 한 [Get-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd335210\(v=exchg.150\))를 참조 하십시오.

