---
title: '사용자에 대 한 음성 메일 미리 보기 파트너 서비스를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 사용자에 대 한 음성 메일 미리 보기 파트너 서비스를 구성 합니다.
ms:assetid: 7bb914ca-5502-4e64-bae5-555034138d8a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff630920(v=EXCHG.150)
ms:contentKeyID: 51407710
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자에 대 한 음성 메일 미리 보기 파트너 서비스를 구성 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

UM(통합 메시징) 사서함 정책에서 음성 메일 미리 보기 파트너를 구성할 수 있습니다. UM 사서함 정책에서 음성 메일 미리 보기 파트너 ID 및 음성 메일 미리 보기 파트너 주소와 같은 음성 메일 미리 보기 파트너 설정을 구성하면, UM 사용 가능하며 해당 사서함 정책과 연결된 모든 사용자에게 이러한 설정이 적용됩니다.


> [!NOTE]
> 음성 메일 미리 보기 파트너를 구성하려면 셸을 사용해야 합니다.



UM 사서함 정책에 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 사서함 정책 절차](um-mailbox-policy-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 어떻게 해야 합니까?

## 1단계: 파트너 서비스에 등록

인증 된 파트너 및 등록 하는 방법에 대 한 자세한 내용은 목록이 찾으려고 [음성 메일 미리 보기 advisor](voice-mail-preview-advisor-exchange-2013-help.md) 를 참조 하거나 [Microsoft 적절치](https://go.microsoft.com/fwlink/p/?linkid=281966) 웹사이트를 참조 합니다. 등록 된 계정이 후 파트너 id와 SMTP 주소 음성 메시지를 전달를 사용 하 여 음성 메일 미리 보기 파트너를 제공 합니다.

2단계에서는 1단계에서 얻은 파트너 ID 및 SMTP 주소를 필수 UM 사서함 정책에 적용합니다.

## 2단계: 음성 메일 미리 보기 파트너 주소 및 ID 설정

이 예에서는 *MyUMMailboxPolicy*라는 UM 사서함 정책에서 음성 메일 미리 보기 파트너 주소를 exumvmp@fabrikam.com으로 설정하고 음성 메일 미리 보기 파트너 ID를 CON123-2010으로 설정합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com
    -VoiceMailPreviewPartnerAssignedID CON123-2010

## 3단계: 고급 음성 메일 미리 보기 파트너 설정 구성

파트너가 사용자 지정 설정을 요구하는 경우 음성 메일 미리 보기 파트너에 대해 다음과 같은 두 개의 매개 변수를 추가로 설정해야 할 수도 있습니다.

  - *VoiceMailPreviewPartnerMaxMessageDuration*

  - *VoiceMailPreviewPartnerMaxDeliveryDelay*

이 예에서는 *MyUMMailboxPolicy*라는 UM 사서함 정책에서 최대 메시지 기간을 300초(5분)로 설정하고 최대 배달 지연 시간을 600초(10분)로 설정합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300 -VoiceMailPreviewPartnerMaxDeliveryDelay 600

## 4단계: UM 사용 가능 사용자를 음성 메일 미리 보기 파트너용 UM 사서함 정책에 할당

UM 다이얼 플랜에서 UM 사용 가능 사용자 중 일부에 대해서만 음성 메일 미리 보기 파트너 서비스를 구성하려면 새 UM 사서함 정책을 만들고 파트너 설정을 구성해야 합니다. 구성이 완료되면 UM 사용 가능한 선택된 사용자에게 새 정책을 적용할 수 있습니다. UM 사용 가능 사용자를 UM 사서함 정책에 할당하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [UM 사서함 정책 할당](assign-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/ko-kr/library/bb124893\(v=exchg.150\))

음성 메일 미리 보기 파트너 프로그램에 대한 자세한 내용은 [음성 메일 미리 보기 advisor](voice-mail-preview-advisor-exchange-2013-help.md)를 참조하십시오.

