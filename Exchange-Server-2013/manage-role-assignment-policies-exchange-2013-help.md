---
title: '역할 할당 정책 관리: Exchange 2013 Help'
TOCTitle: 역할 할당 정책 관리
ms:assetid: f93d502e-5df4-4ba0-b68d-01a17ccffb4d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657511(v=EXCHG.150)
ms:contentKeyID: 50484531
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 할당 정책 관리

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-09_

최종 사용자의 그룹에 할당 된 사용 권한을 사용자 지정 하려는 경우에 새 사용자 지정 관리 역할 할당 정책을 만듭니다. 만들 할당 정책은 최종 사용자에 게 특정 요구 사항에 맞게 사용자 지정할 수 있습니다. Microsoft Exchange Server 2013 에 할당 정책에 대 한 자세한 내용은 [관리 역할 할당 정책 이해 (영문)](understanding-management-role-assignment-policies-exchange-2013-help.md)을 참조 하십시오.

사용 권한 관리와 관련된 다른 관리 작업에 대한 자세한 내용은 [사용 권한](permissions-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md) 항목의 "할당 정책" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 할당 정책을 추가 합니다.

새 할당 정책을 만든 후 여기에 사용자를 지정합니다. 자세한 내용은 [사서함에 할당 정책 변경](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)을 참조하십시오.

## EAC를 사용 하 여 새 할당 정책을 만들려면


> [!NOTE]
> Exchange 관리 센터 (EAC)를 사용 하 여 명시적 할당 정책에만 만들 수 있습니다. 새 기본 할당 정책을 만들려는 경우 Exchange 관리 셸을 사용 해야 합니다. 자세한 내용은이 항목 뒷부분에 나오는 "은 셸을 사용 하 여 기본 할당 정책 만들기" 섹션을 참조 하십시오.



1.  EAC에서 **사용 권한 관리** 로 이동 \> **사용자 역할** 한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭 합니다.

2.  역할 할당 정책 창에서 새 할당 정책에 대 한 이름을 제공 합니다.

3.  할당 정책에 추가할 역할 옆의 확인란을 선택합니다. 추가한 최종 사용자 역할을 비롯한 여러 역할을 선택할 수 있습니다. 하위 역할이 있는 역할을 선택할 경우 하위 역할이 자동으로 선택됩니다.

4.  **저장**을 클릭하여 할당 정책에 대한 변경 내용을 저장합니다.

## 셸을 사용하여 명시적 할당 정책 만들기

사서함에 수동으로 할당할 수 있는 명시적 할당 정책을 만들려면 다음 구문을 사용합니다.

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign>

이 예에서는 명시적 할당 정책 Limited Mailbox Configuration을 만들고 여기에 `MyBaseOptions`, `MyAddressInformation` 및 `MyDisplayName` 역할을 할당합니다.

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName

구문과 매개 변수에 대한 자세한 내용은 [New-RoleAssignmentPolicy](https://technet.microsoft.com/ko-kr/library/dd638101\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 기본 할당 정책 만들기

새 사서함에 할당할 기본 할당 정책을 만들려면 다음 구문을 사용합니다.

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign> -IsDefault

이 예에서는 기본 할당 정책 Limited Mailbox Configuration을 만들고 여기에 `MyBaseOptions`, `MyAddressInformation` 및 `MyDisplayName` 역할을 할당합니다.

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName -IsDefault

구문과 매개 변수에 대한 자세한 내용은 [New-RoleAssignmentPolicy](https://technet.microsoft.com/ko-kr/library/dd638101\(v=exchg.150\))를 참조하십시오.

## 할당 정책을 제거 합니다.

관리 역할 할당 정책을 더이상 해야하는 경우에이 제거할 수 없습니다.

## 시작하기 전에 알아야 할 내용

  - 할당 정책이 할당된 모든 사용자는 다른 할당 정책으로 변경되어야 합니다. 사서함의 할당 정책을 변경하는 방법에 대한 자세한 내용은 [사서함에 할당 정책 변경](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)을 참조하십시오.

  - 할당 된 관리 역할 할당 정책 사이의 관리 역할 할당을 모두 제거 해야 합니다. 할당 정책을에서 역할 할당을 제거 하는 방법에 대 한 자세한 내용은이 항목 뒷부분에 나오는 할당 정책에서 역할을 제거 하려면 셸 사용 하 여 섹션을 참조 하십시오.

  - 기본 할당 정책을 제거 하려면 Exchange 2013 조직에서 마지막 할당 정책을 이어야 합니다.

## EAC를 사용 하 여 할당 정책을 제거 하려면

1.  EAC에서 **사용 권한 관리** 로 이동 \> **사용자 역할** 입니다.

2.  제거 하려는 할당 정책을 선택한 다음 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭 합니다.

## 셸을 사용하여 할당 정책 제거

할당 정책을 제거하려면 다음 구문을 사용합니다.

    Remove-RoleAssignmentPolicy <role assignment policy>

이 예에서는 New York Temporary Users 할당 정책을 제거합니다.

    Remove-RoleAssignmentPolicy "New York Temporary Users"

구문과 매개 변수에 대한 자세한 내용은 [Remove-RoleAssignmentPolicy](https://technet.microsoft.com/ko-kr/library/dd638190\(v=exchg.150\))를 참조하십시오.

## 할당 정책 또는 배정 정책 세부 정보를 보려면

관리 역할 할당 정책에서 다양 한 방식으로 원하는 정보 및 EAC 또는 셸을 사용 하는 여부에 따라 볼 수 있습니다.

EAC에서 할당 정책 및 자신에 게 할당 된 역할의 목록을 볼 수 있습니다. 셸에서 조직의 모든 할당 정책 보기, 등 특정 정책이 할당 된 사서함을 나열할 수 있습니다.

## EAC를 사용 하 여 할당 정책 목록을 보려면

1.  EAC에서 **사용 권한 관리** 로 이동 \> **사용자 역할** 입니다. 모든 조직에서 할당 정책을 여기에 나열 됩니다.

2.  특정 할당 정책의 세부 정보를 보려면 보려는 할당 정책을 선택합니다. 할당 정책에 할당된 역할과 설명이 세부 정보 창에 표시됩니다.

## 셸을 사용하여 할당 정책 목록 보기

**Get-RoleAssignmentPolicy** cmdlet을 실행할 때 할당 정책을 지정하지 않으면 조직에 있는 모든 할당 정책의 목록을 볼 수 있습니다.

이 절차에서는 파이프라이닝과 **Format-Table** cmdlet을 사용합니다. 이 개념에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))

  - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)

조직에 있는 모든 할당 정책의 목록을 반환하려면 다음 명령을 사용합니다.

    Get-RoleAssignmentPolicy

조직에 있는 모든 할당 정책에 대해 특정 속성의 목록을 반환하고 싶은 경우에는 결과를 **Format-Table** cmdlet으로 파이프하고 결과 목록에 표시할 속성을 지정합니다. 다음 구문을 사용합니다.

    Get-RoleAssignmentPolicy | Format-Table <property 1>, <property 2...>

이 예는 조직에 있는 모든 할당 정책의 목록을 반환하며 **Name** 및 **IsDefault** 속성을 포함합니다.

    Get-RoleAssignmentPolicy | Format-Table Name, IsDefault

구문과 매개 변수에 대한 자세한 내용은 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) 또는 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/ko-kr/library/dd638195\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 단일 할당 정책의 세부 정보 보기

**Get-RoleAssignmentPolicy** cmdlet을 사용하고 출력을 **Format-List** cmdlet으로 파이프하여 특정 할당 정책의 세부 정보를 볼 수 있습니다.

이 절차에서는 파이프라이닝과 **Format-List** cmdlet을 사용합니다. 이 개념에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))

  - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)

특정 할당 정책의 세부 정보를 보려면 다음 구문을 사용합니다.

    Get-RoleAssignmentPolicy <assignment policy name> | Format-List

이 예에서는 Redmond Users - no Text Messaging 할당 정책에 대한 세부 정보를 봅니다.

    Get-RoleAssignmentPolicy "Redmond Users - no Text Messaging" | Format-List

구문과 매개 변수에 대한 자세한 내용은 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) 또는 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/ko-kr/library/dd638195\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 기본 할당 정책 찾기

**Get-RoleAssignmentPolicy** cmdlet의 출력을 **Where** cmdlet으로 파이프하여 기본 할당 정책을 찾을 수 있습니다. **Where** cmdlet을 사용하면 반환된 데이터를 필터링하여 *IsDefault* 속성이 `$True`로 설정된 할당 정책만 표시할 수 있습니다.

이 절차에서는 파이프라이닝과 **Where** cmdlet을 사용합니다. 이 개념에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))

  - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)

이 예에서는 기본 할당 정책이 반환됩니다.

    Get-RoleAssignmentPolicy | Where { $_.IsDefault -eq $True }

구문과 매개 변수에 대한 자세한 내용은 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) 또는 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/ko-kr/library/dd638195\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 특정 정책이 할당된 사서함 보기

모든 사서함 **Where** cmdlet에 **Get-Mailbox** cmdlet의 출력을 파이프 하 여 특정 할당 정책 할당을 찾을 수 있습니다. **Where** cmdlet를 사용 하 여의 *RoleAssignmentPolicy* 속성은 지정한 할당 정책 이름으로 설정 하는 사서함만 표시를 반환 하는 데이터를 필터링 합니다.

이 절차에서는 파이프라이닝과 **Where** cmdlet을 사용합니다. 이 개념에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))

  - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)

다음 구문을 사용합니다.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<role assignment policy>" }

이 예에서는 Vancouver End Users 정책이 할당된 모든 사서함을 찾습니다.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Vancouver End Users" }

구문과 매개 변수에 대한 자세한 내용은 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) 또는 [Get-RoleAssignmentPolicy](https://technet.microsoft.com/ko-kr/library/dd638195\(v=exchg.150\))를 참조하십시오.

## 기본 할당 정책 변경

만들어지는 새 사서함에 할당 된 관리 역할 할당 정책을 변경할 수 있습니다. 기본 역할 할당 정책을 변경 하면 기존 사서함에 할당 된 할당 정책을 변경 되지 않습니다. 기존 사서함에 할당 된 할당 정책을 변경 하려면 [사서함에 할당 정책 변경](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)를 참조 하십시오.


> [!NOTE]
> EAC를 사용 하 여 기본 할당 정책을 변경 하려면 수는 없습니다. 셸을 사용 하 여 해야 합니다.



## 셸을 사용하여 기본 할당 정책 변경

기본 할당 정책을 변경하려면 다음 구문을 사용합니다.

    Set-RoleAssignmentPolicy <assignment policy name> -IsDefault

이 예에서는 Vancouver End Users 할당 정책을 기본 할당 정책으로 설정합니다.

    Set-RoleAssignmentPolicy "Vancouver End Users" -IsDefault


> [!IMPORTANT]
> 정책 관리 역할 할당 하지 않은 경우에 새 사서함은 기본 할당 정책을 할당 됩니다. 없는 할당 된 관리 역할 할당 정책에 할당 된 사서함 Microsoft Outlook Web App에서 모든 사서함 구성 기능에 액세스할 수 없습니다.



구문과 매개 변수에 대한 자세한 내용은 [Set-RoleAssignmentPolicy](https://technet.microsoft.com/ko-kr/library/dd638090\(v=exchg.150\))를 참조하십시오.

## 역할 할당 정책에 추가

## EAC를 사용 하 여 역할 할당 정책에 추가 하려면

1.  EAC에서 **사용 권한 관리** 로 이동 \> **사용자 역할** 입니다.

2.  하나 이상의 역할을 추가 하려면 할당 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

3.  할당 정책에 추가할 역할 옆의 확인란을 선택합니다. 추가한 최종 사용자 역할을 비롯한 여러 역할을 선택할 수 있습니다. 하위 역할이 있는 역할을 선택할 경우 하위 역할이 자동으로 선택됩니다.

4.  할당 정책의 변경 내용을 저장하려면 **저장**을 클릭합니다.

## 셸을 사용하여 할당 정책에 역할 추가

역할과 할당 정책 간에 관리 역할 할당을 만들려면 다음 구문을 사용합니다.

    New-ManagementRoleAssignment -Name <role assignment name> -Role <role name> -Policy <assignment policy name>

이 예에서는 MyVoicemail 역할 및 Seattle Users 할당 정책 간에 Seattle Users - Voicemail 역할 할당을 만듭니다.

    New-ManagementRoleAssignment -Name "Seattle Users - Voicemail" -Role MyVoicemail -Policy "Seattle Users"

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 역할 할당 정책에서 제거

최종 사용자가 자신의 사서함 또는 메일 그룹의 특정 기능을 관리 하는 권한을 갖도록 하지 않을 경우에 사용자가 할당 된 관리 역할 할당 정책에서 사용 권한을 부여 하는 관리 역할을 제거할 수 있습니다. 다른 사용자가 동일한 할당 정책의 할당 하는 경우 해당 기능을 관리 하는 기능을 사라집니다.

## EAC를 사용 하 여 역할 할당 정책에서 제거 하려면

1.  EAC에서 **사용 권한 관리** 로 이동 \> **사용자 역할** 입니다.

2.  에서 하나 이상의 역할을 제거 하려면 할당 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘") 를 클릭 합니다.

3.  할당 정책에서 제거 하려면 원하는 역할 또는 역할 옆에 있는 확인란 확인란의 선택을 취소 합니다. 하위 역할이 있는 역할에 대 한 확인란의 선택을 취소 하는 경우 하위 역할에 대 한 확인란 지워집니다.

4.  **저장**을 클릭하여 할당 정책에 대한 변경 내용을 저장합니다.

## 셸을 사용 하 여 역할 할당 정책에서 제거 하려면

**Get-ManagementRoleAssignment** cmdlet 및 다음 파이핑 **Remove-ManagementRoleAssignment** cmdlet에 반환 되는 역할 할당을 사용 하 여 관련 된 관리 역할 할당을 검색 하 여 역할 할당 정책에서 제거할 수 있습니다.

일반 및 위임 역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참조하십시오.

이 절차에서는 파이프라이닝을 사용합니다. 파이프라이닝에 대한 자세한 내용은 [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))을 참조하십시오.

역할을 할당 정책에서 제거 하려면 다음 구문을 사용 합니다.

    Get-ManagementRoleAssignment -RoleAssignee <assignment policy name> -Role <role name> | Remove-ManagementRoleAssignment

이 예제에서는 사용자가 시애틀 사용자 할당 정책에서 자신의 음성 메일 옵션을 관리할 수 있도록 하는 MyVoicemail 관리 역할을 제거 합니다.

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Users" -Role MyVoicemail | Remove-ManagementRoleAssignment

구문과 매개 변수에 대한 자세한 내용은 [Remove-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351205\(v=exchg.150\))를 참조하십시오.

