---
title: 'UM 헌트 그룹 보기: Exchange 2013 Help'
TOCTitle: UM 헌트 그룹 보기
ms:assetid: f038f7b4-4de9-4373-bd58-09d49e37a3ed
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125167(v=EXCHG.150)
ms:contentKeyID: 50556109
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 헌트 그룹 보기

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-05_

UM (통합 메시징) 헌트 그룹에 대 한 속성을 볼 때 단일 UM 헌트 그룹 또는 단일 UM IP 게이트웨이에 연결 된 모든 UM 헌트 그룹과 연결 된 속성을 볼 수 있습니다. 두 매개 변수를 지정 하는 경우 모든 UM 헌트 그룹이 반환 됩니다. 속성을 보려면 UM 헌트 그룹; EAC를 사용할 수 없습니다. 셸을 사용 해야 합니다.

UM 헌트 그룹을 만든 후에 구성 된 설정은 변경할 수 없습니다. 파일럿 식별자에서 UM 헌트 그룹 등 구성 설정을 변경 하려는 경우에 기존 UM 헌트 그룹을 삭제 하 고 올바른 설정이 있는 새 UM 헌트 그룹을 생성 해야 합니다.

UM 헌트 그룹과 관련된 추가 작업에 대한 자세한 내용은 [UM 헌트 그룹 절차](um-hunt-group-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1 분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 헌트 그룹" 항목

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 절차를 수행 하기 전에 UM 게이트웨이 만들었는지 확인 합니다. 자세한 단계 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)을 참조 하십시오.

  - 이 절차를 수행 하기 전에 UM 헌트 그룹을 만들었는지 확인 합니다. 자세한 단계 [UM 헌트 그룹 만들기](create-a-um-hunt-group-exchange-2013-help.md)을 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용 하 여 UM 헌트 그룹의 속성을 보려면

이 예에서는 Active Directory 포리스트의 모든 UM 헌트 그룹을 표시합니다.

    Get-UMHuntGroup

서식이 지정 된 목록에서 `MyUMHuntGroup` 라는 UM 헌트 그룹의 세부 정보를 표시 하는이 예제입니다.

    Get-UMHuntGroup -identity MyUMIPGateway\MyUMHuntGroup | Format-List


> [!NOTE]
> <STRONG>Get-UMHuntGroup</STRONG> cmdlet을 사용 하는 경우에 UM 헌트 그룹의 이름을 입력할 수 없습니다. UM 헌트 그룹과 연결 된 UM IP 게이트웨이의 이름을 포함 해야 합니다.


