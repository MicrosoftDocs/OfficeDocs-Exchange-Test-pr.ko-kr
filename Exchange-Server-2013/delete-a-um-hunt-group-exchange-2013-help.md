---
title: 'UM 헌트 그룹 삭제: Exchange 2013 Help'
TOCTitle: UM 헌트 그룹 삭제
ms:assetid: 11ac102d-b58d-486c-85b6-e096428e556d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996318(v=EXCHG.150)
ms:contentKeyID: 50555942
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 헌트 그룹 삭제

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-05_

UM(통합 메시징) 헌트 그룹을 삭제하면 해당 UM 헌트 그룹과 연결된 UM IP 게이트웨이는 더 이상 수신 전화를 처리하거나 응답하지 않습니다. UM 헌트 그룹을 삭제하면 UM IP 게이트웨이에 구성된 헌트 그룹이 없게 되고, UM IP 게이트웨이는 UM 통화를 처리할 수 없습니다.

UM 헌트 그룹과 관련된 추가 작업에 대한 자세한 내용은 [UM 헌트 그룹 절차](um-hunt-group-procedures-exchange-2013-help.md)를 참조하십시오.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UM 헌트 그룹 설정을 변경하려면 헌트 그룹을 삭제한 다름 적절한 설정이 포함된 다른 헌트 그룹을 만들어야 합니다.</td>
</tr>
</tbody>
</table>


## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 헌트 그룹" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM IP 게이트웨이를 만들었는지 확인하십시오. 자세한 단계는 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 헌트 그룹을 만들었는지 확인합니다. 자세한 단계는 [UM 헌트 그룹 만들기](create-a-um-hunt-group-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 헌트 그룹 삭제

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경할 UM 다이얼 플랜을 클릭하고, 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지에 있는 **UM 헌트 그룹**에서 삭제할 헌트 그룹을 선택하고, 도구 모음에서 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭합니다.

3.  **경고** 페이지에서 **예**를 클릭합니다.

## 셸을 사용하여 UM 헌트 그룹 삭제

이 예에서는 `MyUMHuntGroup`이라는 UM 헌트 그룹을 삭제합니다.

    Remove-UMHuntGroup -identity MyUMHuntGroup

