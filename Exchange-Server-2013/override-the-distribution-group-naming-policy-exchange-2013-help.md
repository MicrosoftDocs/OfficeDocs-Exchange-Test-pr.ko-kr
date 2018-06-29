---
title: '메일 그룹 명명 정책을 무시합니다: Exchange 2013 Help'
TOCTitle: 메일 그룹 명명 정책을 무시합니다
ms:assetid: 9eb23fc9-3f59-4d09-9077-85c89a051ee0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ218685(v=EXCHG.150)
ms:contentKeyID: 50482266
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 그룹 명명 정책을 무시합니다

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-13_

메일 그룹에 대한 그룹 명명 정책은 사용자가 만드는 그룹에만 적용됩니다. 관리자가 EAC(Exchange 관리 센터)를 사용하여 메일 그룹을 만들면 그룹 명명 정책이 무시되고 그룹 이름에 적용되지 않습니다.

그러나 Exchange 관리 셸을 사용하여 메일 그룹을 만들거나 그룹 이름을 바꾸는 경우, *IgnoreNamingPolicy* 매개 변수를 사용하여 그룹 명명 정책을 재정의하지 않으면 그룹 명명 정책이 관리자가 만든 그룹에도 적용됩니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "메일 그룹" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 새 그룹을 만들 때 그룹 명명 정책 재정의

그룹 명명 정책을 재정의하려면 다음 명령을 실행합니다.

    New-DistributionGroup -Name <Group Name> -IgnoreNamingPolicy

예를 들어 조직의 그룹 명명 정책이 **DG\_\<그룹 이름\>\_Users**인 경우 다음 명령을 실행하면 이름이 **All Administrators**인 그룹이 만들어집니다.

    New-DistributionGroup -Name "All Administrators" -IgnoreNamingPolicy

Microsoft Exchange에서는 이 그룹을 만들 때 *Name* 및 *DisplayName* 매개 변수 둘 다에 **All Administrators**를 사용합니다.

## 그룹 이름 변경 시 셸을 사용하여 그룹 명명 정책 재정의

셸을 사용하여 기존 그룹의 이름을 바꿀 때 그룹 명명 정책을 재정의하려면 다음 명령을 실행합니다.

    Set-DistributionGroup -Identity <Old Group Name> -Name <New Group Name> -DisplayName <New Group Name> -IgnoreNamingPolicy

예를 들어 밤늦게 그룹 명명 정책을 만들었는데 다음날 아침에 확인해 보니 접두사의 텍스트 문자열 철자가 잘못된 경우를 가정해 보겠습니다. 철자가 잘못된 접두사를 사용하여 새 그룹을 이미 만들었더라도 EAC에서 그룹 명명 정책을 수정할 수 있습니다. 단, 철자가 잘못된 이름이 지정된 그룹 이름을 바꾸려면 셸을 사용해야 합니다. 다음 명령을 실행합니다.

    Set-DistributionGroup -Identity "Goverment_Contracts_NWRegion" -Name "Government_ContractEstimates_NWRegion" -DisplayName "Government_ContractEstimates_NWRegion" -IgnoreNamingPolicy


> [!IMPORTANT]
> 그룹 이름을 바꿀 때는 <EM>DisplayName</EM> 매개 변수를 포함하십시오. 그렇게 하지 않으면 공유 주소록과 전자 메일 메시지의 받는 사람:, 참조: 및 보낸 사람: 필드에 이전 이름이 계속 표시됩니다.



## 작동 여부는 어떻게 확인합니까?

그룹 명명 정책을 무시하는 배포 그룹을 성공적으로 만들거나 이름을 변경했는지 확인하려면 다음 명령을 실행합니다.

    Get-DistributionGroup <Name> | FL DisplayName

    Get-OrganizationConfig | FL DistributionGroupNamingPolicy

그룹의 표시 이름 형식이 조직의 그룹 명명 정책에서 지정하는 형식과 다르면 정상적으로 수행된 것입니다.

