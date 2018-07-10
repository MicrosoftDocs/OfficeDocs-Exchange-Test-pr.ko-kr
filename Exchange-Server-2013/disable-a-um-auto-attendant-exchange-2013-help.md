---
title: 'UM 자동 전화 교환을 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: UM 자동 전화 교환을 사용 하지 않도록 설정
ms:assetid: ad79f374-f68f-430b-8b9c-2c841e1c55ae
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124228(v=EXCHG.150)
ms:contentKeyID: 50483855
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 자동 전화 교환을 사용 하지 않도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-05_

기본적으로 UM (통합 메시징) 자동 전화 교환 만들어지면 해당 상태 사용 안함으로 설정 됩니다. UM 자동 전화 교환을 만든 후에 걸려오는 전화를 받을 수 있는지 여부를 제어를 해당 상태를 변경할 수 있습니다. 예, 다음 다시 사용자 지정된 음성 안내 하 고 메시지를 녹음/녹화 또는 녹음/녹화 중인 때 UM 자동 전화 교환을 사용 하지 않도록 설정 하는 것이 좋습니다.

UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행 하기 전에 UM 자동 전화 교환이 만들어졌는지 확인 합니다. 자세한 단계 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)을 참조 하십시오. 또한 UM 자동 전화 교환의 상태가 사용으로 설정 되었는지 확인 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 UM 자동 전화 교환을 사용 하지 않으려면

1.  EAC에서 **통합** 메시징으로 이동 \> **UM 다이얼 플랜** 합니다. 목록 보기에서 변경할 다이얼 플랜을 선택 하 고 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

2.  **UM 다이얼 플랜** 페이지에서 **UM 자동 전화 교환** 사용 하지 않도록 설정할 UM 자동 전화 교환을 선택 합니다. 도구 모음에서 **아래쪽 화살표**![아래쪽 화살표 아이콘](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "아래쪽 화살표 아이콘") 를 클릭 합니다.

3.  **경고** 페이지에서 **예**를 클릭합니다.

## 셸을 사용 하 여 UM 자동 전화 교환을 사용 하지 않도록 설정 하려면

이 예제에서는 `MyUMAutoAttendant`라는 UM 자동 전화 교환 사용 하지 않도록 설정 합니다.

    Disable-UMAutoAttendant -Identity MyUMAutoAttendant

