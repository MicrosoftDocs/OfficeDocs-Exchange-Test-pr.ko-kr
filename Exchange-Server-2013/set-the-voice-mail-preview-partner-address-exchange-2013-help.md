---
title: '음성 메일 미리 보기 파트너 주소 설정: Exchange 2013 Help'
TOCTitle: 음성 메일 미리 보기 파트너 주소 설정
ms:assetid: 57fbed1e-1b14-4939-95e6-ef7c072f32a9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff630917(v=EXCHG.150)
ms:contentKeyID: 51407700
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메일 미리 보기 파트너 주소 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-13_

UM(통합 메시징) 사서함 정책에 대해 음성 메일 미리 보기 파트너 주소를 설정할 수 있습니다. UM 사서함 정책에 대한 음성 메일 미리 보기 파트너 주소를 설정하면 설정이 해당 사서함 정책과 연결된 모든 UM 사용 가능 사용자에게 적용됩니다.


> [!NOTE]
> 음성 메일 미리 보기 파트너 주소는 셸을 사용하여 설정해야 합니다.



음성 메일 미리 보기 파트너 프로그램에 대한 자세한 내용은 [음성 메일 미리 보기 advisor](voice-mail-preview-advisor-exchange-2013-help.md)를 참조하십시오.

음성 메일 미리 보기와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 미리 보기 절차](voice-mail-preview-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 UM 사서함 정책에서 음성 메일 미리 보기 파트너 주소 설정

이 예에서는 *MyUMMailboxPolicy*로 명명된 UM 사서함 정책에서 음성 메일 미리 보기 파트너 주소를 exumvmp@fabrikam.com으로 설정합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com

