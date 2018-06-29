---
title: 'UM IP 게이트웨이 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: UM IP 게이트웨이 사용 하지 않도록 설정
ms:assetid: fe3a8797-1230-49cb-a839-ccec238266b6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125257(v=EXCHG.150)
ms:contentKeyID: 50484605
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM IP 게이트웨이 사용 하지 않도록 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-11-13_

UM (통합 메시징) IP 게이트웨이 만들 때에 기본적으로 UM IP 게이트웨이 상태의 활성화 됩니다. UM IP 게이트웨이 만든 후에 해당 상태 사용 안함으로 설정 하 여 게이트웨이의 작업을 비활성화할 수 있습니다. UM IP 게이트웨이, (VoIP) IP 게이트웨이 통해 음성을 해제 한 후 IP Private Branch eXchange (PBX) 또는 사용 하도록 구성 된 세션 테두리 컨트롤러 (SBC) 들어오는 통합 메시징 호출 더이상 처리할 수 없습니다.

UM IP 게이트웨이와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM IP 게이트웨이 절차](um-ip-gateway-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM IP 게이트웨이" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행 하기 전에 UM IP 게이트웨이 만들어진 및 수 있는지 확인 합니다. 자세한 단계 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md) 및 [UM IP 게이트웨이 사용 하도록 설정](enable-a-um-ip-gateway-exchange-2013-help.md)를 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 UM IP 게이트웨이 사용 하지 않도록 설정 하려면

1.  EAC에서 **통합** 메시징으로 이동 \> **UM IP 게이트웨이** 사용 하지 않도록 설정할 UM IP 게이트웨이 선택 하 고 다음![아래쪽 화살표 아이콘](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "아래쪽 화살표 아이콘")의 **아래쪽 화살표** 클릭 합니다.

2.  **경고** 페이지에서 **예**를 클릭합니다.

## 셸을 사용 하 여 UM IP 게이트웨이 사용 하지 않도록 설정 하려면

이 예제에서는 `MyUMIPGateway` 라는 UM IP 게이트웨이 사용 하지 않도록 설정 하 고 VoIP 게이트웨이, IP PBX 또는 SBC 들어오는 호출을 수락 하 여이 중지 합니다.

    Disable-UMIPGateway -Identity MyUMIPGateway

이 예제에서는 `MyUMIPGateway` 라는 UM IP 게이트웨이 사용 하지 않도록 설정 하 고 즉시 모든 현재 호출의 연결을 끊습니다.

    Disable-UMIPGateway -Identity MyUMIPGateway -Immediate $true

