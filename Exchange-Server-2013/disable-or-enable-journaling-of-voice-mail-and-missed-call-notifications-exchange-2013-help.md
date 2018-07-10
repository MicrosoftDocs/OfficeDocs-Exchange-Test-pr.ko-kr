---
title: '사용 하지 않거나 음성 메일 및 부재중된 전화 알림의 저널링을 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 사용 하지 않거나 음성 메일 및 부재중된 전화 알림의 저널링을 사용 하도록 설정
ms:assetid: 5164a92e-69e6-4339-b80c-0cfbf0dc0198
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201690(v=EXCHG.150)
ms:contentKeyID: 50483093
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 하지 않거나 음성 메일 및 부재중된 전화 알림의 저널링을 사용 하도록 설정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

Microsoft Exchange Server 2013에서는 Exchange 조직의 받는 사람이나 보낸 사람과 주고받는 전자 메일 메시지를 저널링하기 위해 저널 규칙을 만들 때 UM(통합 메시징) 서비스에서 생성된 음성 메일과 부재 중 전화 알림이 포함됩니다. 이 항목의 절차에 따라 전체 조직에 대해 이 기능을 설정하거나 해제할 수 있습니다.

저널링과 관련된 다른 관리 작업에 대한 자세한 내용은 [저널링 관리](manage-journaling-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "저널링" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 음성 메일과 부재 중 전화 알림에 대해 저널링 설정 또는 해제

이 예에서는 *VoicemailJournalingEnabled* 매개 변수를 `$false`로 설정하여 음성 메일과 부재 중 전화 알림의 저널링을 사용하지 않도록 설정합니다.

    Set-TransportConfig -VoicemailJournalingEnabled $false

이 예에서는 이 매개 변수를 `$true`로 설정하여 음성 메일과 부재 중 전화 알림의 저널링을 사용하도록 설정합니다.

    Set-TransportConfig -VoicemailJournalingEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-TransportConfig](https://technet.microsoft.com/ko-kr/library/bb124151\(v=exchg.150\))를 참조하십시오.

## 자세한 내용

[저널링](journaling-exchange-2013-help.md)

[저널링 관리](manage-journaling-exchange-2013-help.md)

