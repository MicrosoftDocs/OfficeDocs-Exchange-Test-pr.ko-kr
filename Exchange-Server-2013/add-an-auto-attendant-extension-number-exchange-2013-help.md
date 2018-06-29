---
title: '자동 전화 교환 내선 번호를 추가 합니다.: Exchange 2013 Help'
TOCTitle: 자동 전화 교환 내선 번호를 추가 합니다.
ms:assetid: f2bd62ba-1e01-4cb7-862c-c750752e20e0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232200(v=EXCHG.150)
ms:contentKeyID: 50484522
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 자동 전화 교환 내선 번호를 추가 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-11-05_

UM (통합 메시징) 자동 전화 교환에 내선 번호 또는 여러 내선 번호를 구성할 수 있습니다. UM 자동 전화 교환에 내선 번호를 추가 하는 경우 해당 번호 하는데 사용할 수 호출자에 의해 자동 전화 교환으로 호출 합니다. 또한 발신자에 게 자동 전화 교환에 액세스 하는데 사용할 수 있는 둘 이상의 내선 번호 있기 때문에 내선 번호를 추가 해야할 수 있습니다. 기본적으로 없음 내선 번호는 자동 전화 교환을 만들 때 구성 됩니다.

자동 전화 교환에 대 한 내선 번호를 설정 하지 않고 새 자동 전화 교환을 만들 수 있습니다. 또한 단일 자동 전화 교환으로 둘 이상의 전화 또는 내선 번호를 연결할 수 있습니다. UM 자동 전화 교환 만들기 또는 자동 전화 교환을 구성한 후이 추가 하는 경우에 하거나 내선 번호를 추가할 수 있습니다. UM 자동 전화 교환에 구성 된 내선 번호의 자릿수 UM 자동 전화 교환와 연결 된 UM 다이얼 플랜에 구성 된 내선 번호에 대 한 자릿수를 일치 해야 합니다.


> [!NOTE]
> 내선 번호를 추가 하는 대신 세션 SIP (Initiation Protocol) 주소를 추가할 수 있습니다. 일부 IP Private Branch Exchange (Pbx) 하 여 SIP 주소를 사용 하는 Office Communications Server 2007 R2 또는 Microsoft Lync Server 및 합니다.



UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 UM 자동 전화 교환에 대 한 확장 또는 전화 번호를 사용 하는 추가 하려면

1.  EAC에서 **통합** 메시징으로 이동 \> **UM 다이얼 플랜** 합니다. 목록 보기에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 하 고 편집 하려는 UM 다이얼 플랜을 선택 합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환** 확장 또는 전화 번호를 추가 하려는 UM 자동 전화 교환을 선택 합니다.

3.  도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

4.  **UM 자동 전화 교환** 페이지에서 \> **일반액세스 번호**, 텍스트 상자에![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**추가** 클릭 하 고 사용 하려는 확장 또는 전화 번호를 입력 합니다.

5.  번호를 추가 하려면 **저장** 을 클릭 합니다.

## 셸을 사용 하 여 UM 자동 전화 교환에 내선 번호를 구성 하려면

이 예에서는 여러 내선 번호를 사용 하 여 `MyUMAutoAttendant` 라는 UM 자동 전화 교환을 구성 합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -PilotIdentifierList "12345, 72000, 75000"

