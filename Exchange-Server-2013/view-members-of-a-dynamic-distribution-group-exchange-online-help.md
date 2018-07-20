---
title: '동적 메일 그룹의 구성원 보기: Exchange 2013 Help'
TOCTitle: 동적 메일 그룹의 구성원 보기
ms:assetid: 40b100c6-864e-4c82-9f98-08dd5c83e378
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232019(v=EXCHG.150)
ms:contentKeyID: 50482211
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 동적 메일 그룹의 구성원 보기

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2018-03-02_

동적 메일 그룹은 구성원 자격의 기준이 정의된 받는 사람 집합이 아닌 특정 받는 사람 필터인 메일 그룹입니다. MicrosoftExchange의 미리 만든 필터를 사용하여 동적 메일 그룹의 받는 사람 필터를 보다 쉽게 만들 수 있습니다. *미리 만든 필터*는 일반적으로 사용되는 필터로, 다양한 받는 사람 필터링 기준을 충족합니다. 동적 메일 그룹에 포함할 받는 사람 유형을 지정할 수 있습니다. 또한 받는 사람이 충족해야 하는 조건 목록을 지정할 수도 있습니다. 미리 만든 필터를 사용하는 동적 메일 그룹의 받는 사람 목록을 미리 볼 때 셸을 사용할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "동적 메일 그룹" 항목입니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 동적 메일 그룹의 구성원 목록 미리 보기

이 예제에서는 전체 시간 employees 동적 메일 그룹에 대 한 팀 구성원의 목록을 반환 합니다. 첫번째 명령은 변수 `$FTE`에서 동적 메일 그룹 개체를 저장합니다. 두번째 명령은 **Get-Recipient** cmdlet를 사용 하 여 동적 메일 그룹에 대해 정의 된 조건과 일치 하는 받는 사람 목록을 합니다.

  ```
  $FTE = Get-DynamicDistributionGroup "Full Time Employees"
  ```

  ```
  Get-Recipient -RecipientPreviewFilter $FTE.RecipientFilter -OrganizationalUnit $FTE.RecipientContainer
  ```

구문과 매개 변수에 대한 자세한 내용은 [Get-DynamicDistributionGroup](https://technet.microsoft.com/ko-kr/library/bb124762\(v=exchg.150\)) 및 [Get-Recipient](https://technet.microsoft.com/ko-kr/library/aa996921\(v=exchg.150\))를 참조하십시오.


> [!NOTE]
> EAC를 사용 하 여 동적 메일 그룹의 구성원을 볼 수 없습니다.



## 작동 여부는 어떻게 확인합니까?

동적 메일 그룹의 구성원을 볼 성공적으로 했는지를 확인 하려면 다음을 수행 합니다.

  - 셸에서 이전 명령을 실행하여 동적 메일 그룹 구성원의 목록을 미리 본 후 구성원의 목록이 반환됩니다. 예를 들어 동적 메일 그룹에 대한 받는 사람 필터와 일치하는 속성을 사용하여 새로운 사용자 사서함을 만든 경우 이 새로운 사용자가 그룹 구성원의 목록에 표시되어야 합니다.

