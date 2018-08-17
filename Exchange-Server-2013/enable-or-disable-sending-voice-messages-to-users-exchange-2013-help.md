---
title: '사용 하도록 설정 하거나 사용자에 게 보내는 음성 메시지를 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: 사용 하도록 설정 하거나 사용자에 게 보내는 음성 메시지를 사용 하지 않도록 설정
ms:assetid: faa300d8-2534-40db-8ef9-428be8bb7934
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351277(v=EXCHG.150)
ms:contentKeyID: 52057990
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 하도록 설정 하거나 사용자에 게 보내는 음성 메시지를 사용 하지 않도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-12-13_

이렇게에서 금지 하거나 호출자가 UM (통합 메시징) 자동 전화 교환에서 사용자에 게 음성 메시지를 보낼 수를 설정할 수 있습니다. 기본적으로이 옵션을 사용할지 및 호출자가 UM 자동 전화 교환와 관련 된 UM 다이얼 플랜에 사용자에 게 음성 메시지를 보낼 수 있습니다. 이 옵션을 비활성화 하는 경우 자동 전화 교환 시스템 프롬프트 하는 동안 음성 메시지를 보내려고 발신자에 게 초대 하지 않습니다.

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

## EAC를 사용 하 여 발신자가 음성 메시지를 보내거나에서 작업을 금지를 사용 하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 자동 전화 교환** **UM 다이얼 플랜** 페이지에서 관리할 UM 자동 전화 교환 선택 하 고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 한 다음 키를 누릅니다.

3.  **UM 자동 전화 교환** 페이지에서 \> 호출자가 음성 메시지를 남길 수 있도록 **사용자에 대 한 음성 메시지를 남길 호출자가 허용** 옆에 있는 확인란을 선택 **주소록 및 연산자에 대 한 액세스를 주소** 를 **사용자에 게 문의 하는 것에 대 한 옵션** 아래 있습니다. 호출자가 음성 메시지를 남길 하지 못하도록 하려면 확인란의 선택을 취소 합니다.

4.  **저장**을 클릭합니다.


> [!NOTE]
> 이 옵션을 사용 하지 않도록 설정 하 고도 <STRONG>사용자가 전화를 걸려면 호출자가 허용</STRONG> 옵션을 사용 하지 않도록 설정 하는 경우 <STRONG>주소록을 검색 하기 위한 옵션</STRONG> 도 사용할 수 없습니다.



## 셸을 사용 하 여 호출자가 음성 메시지를 보내거나에서 작업을 금지을 사용 하도록 설정 하려면

호출자가 음성 메시지를 보내지 못하도록 `MyUMAutoAttendant` 라는 UM 자동 전화 교환에 전화를 해제 하는이 예제입니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $false

전화 건 사람이 전화를 UM 자동 전화 교환 `MyUMAutoAttendant` 라는 음성 메시지를 보낼 수를 설정 하는이 예제입니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $true

