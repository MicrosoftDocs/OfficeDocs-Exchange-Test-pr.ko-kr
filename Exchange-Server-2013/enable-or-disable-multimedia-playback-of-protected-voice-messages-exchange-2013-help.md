---
title: '보호 된 음성 메시지의 멀티미디어 재생을 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 보호 된 음성 메시지의 멀티미디어 재생을 사용 하지 않도록 설정 하거나 사용
ms:assetid: 3c33370c-4262-42b1-8d83-d61fc7c426cd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423543(v=EXCHG.150)
ms:contentKeyID: 52057910
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보호 된 음성 메시지의 멀티미디어 재생을 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

보호된 음성 메일 메시지를 받는 사용자가 전화에서 재생 기능을 통해 메시지를 듣도록 강제 적용할 수 있습니다. 클라이언트 소프트웨어에서 권한 관리를 지원하지 않는 경우 사용자는 Outlook Voice Access를 사용하여 메시지를 들어야 합니다.

음성 메시지를 들으려는 UM(통합 메시징) 사용 가능 사용자는 컴퓨터나 모바일 장치의 멀티미디어 소프트웨어 또는 전화에서 재생 기능을 사용할 수 있습니다. UM 사용 가능 사용자는 멀티미디어 재생을 통해 미디어 플레이어를 사용해 컴퓨터 스피커로 음성 메시지를 듣거나, 모바일 장치에서 미디어 플레이어를 사용해 음성 메시지를 들을 수 있습니다.


> [!NOTE]
> 보호된 음성 메일은 권한 관리를 지원하는 Outlook 버전을 사용 중인 클라이언트에서만 사용 가능합니다. 클라이언트 소프트웨어에서 권한 관리를 지원하지 않는 경우 사용자는 Outlook Voice Access를 사용하여 통화 내용을 들어야 합니다.



기본적으로, UM 사서함 정책에서 **RequireProtectedPlayOnPhone** 속성 값은 False로 설정됩니다. 즉, 해당 UM 사서함 정책에 연결된 UM 사용 가능 사용자는 다음 방법을 통해 보호된 음성 메시지를 들을 수 있습니다.

  - Outlook Voice Access 사용

  - Outlook 2010 이상 버전의 기본 제공 미디어 플레이어 또는 전화에서 재생 단추 사용

  - Outlook Web App의 기본 제공 미디어 플레이어 또는 전화에서 재생 단추 사용

이 값이 true로 설정되어 있으면 보호된 음성 메일의 멀티미디어 재생은 허용되지 않습니다. 이 값이 true로 설정된 UM 사서함 정책에 연결된 UM 사용 가능 사용자는 다음 방법을 통해서만 보호된 음성 메시지를 들을 수 있습니다.

  - Outlook Voice Access 사용

  - Outlook 2010 이상 버전의 전화에서 재생 단추 사용

  - Outlook Web App의 전화에서 재생 단추 사용

이 설정은 UM 사용 가능 사용자가 공용 컴퓨터, 공공 장소의 랩톱 또는 모바일 장치의 미디어 플레이어를 사용하여 개인 정보를 포함할 수 있는 보호된 음성 메일을 듣는 경우 특히 유용합니다.

보호된 음성 메일 절차와 관련된 추가 관리 작업에 대한 자세한 내용은 [보호 된 음성 메일 절차](protected-voice-mail-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 보호된 음성 메시지의 멀티미디어 재생을 사용하거나 사용하지 않도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 사서함 정책** 아래에서 관리할 UM 사서함 정책을 선택한 후 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지 \> **보호된 음성 메일**에서 **보호된 음성 메시지에 대해 전화에서 재생 요구** 옆의 확인란을 선택하여 이 설정을 사용하도록 설정합니다. 이 설정을 사용하지 않도록 설정하려면 확인란의 선택을 취소합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 보호된 음성 메시지의 멀티미디어 재생을 사용하거나 사용하지 않도록 설정

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책에 연결된 사용자가 미디어 플레이어를 사용하여 보호된 음성 메시지를 재생하도록 허용합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $false

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책에 연결된 사용자가 미디어 플레이어를 사용하여 보호된 음성 메시지를 재생하지 못하게 합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $true

