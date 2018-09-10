---
title: '사용자 그룹에 대 한 팩스를 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 사용자 그룹에 대 한 팩스를 사용 하도록 설정
ms:assetid: b8d9f54d-ff06-4942-83e1-fc6c4ad02178
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423556(v=EXCHG.150)
ms:contentKeyID: 52058028
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자 그룹에 대 한 팩스를 사용 하도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

UM(통합 메시징) 사서함 정책과 연결된 사용자에 대해 인바운드 팩스를 사용하도록 설정할 수 있습니다. 기본적으로 사용자가 통합 메시징을 사용하도록 설정해도 팩스 파트너 서버의 URI를 지정하고, 조직의 팩스 파트너 서버를 배포하고, UM 사서함 정책에서 팩스를 사용하도록 설정할 때까지는 사용자가 팩스 메시지를 받을 수 없습니다. UM 다이얼 플랜에서 수신 팩스 허용 옵션을 사용하지 않도록 설정하면 UM 사서함 정책과 연결된 사용자는 계속 팩스를 받을 수 없습니다. 마찬가지로 개별 사용자에 대해 수신 팩스 허용 옵션을 사용하지 않도록 설정해도 해당 사용자는 팩스를 받을 수 없습니다.

팩스 파트너에 대 한 자세한 내용은 [팩스 파트너에 대 한 Microsoft 적절치](https://go.microsoft.com/fwlink/?linkid=190238)를 참조 하십시오.

팩스와 관련된 추가 관리 작업에 대한 자세한 내용은 [절차를 팩스](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/faxing-procedures)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 인바운드 팩스를 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 수정하려는 사서함 정책을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지 \> **일반**에서 **인바운드 팩스 허용** 옆에 있는 확인란을 선택합니다.

4.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용하여 인바운드 팩스를 사용하도록 설정

이 예에서는 UM 사서함 정책 `MyUMMailboxPolicy`와 연결된 사용자가 인바운드 팩스를 사용하도록 허용합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $true

