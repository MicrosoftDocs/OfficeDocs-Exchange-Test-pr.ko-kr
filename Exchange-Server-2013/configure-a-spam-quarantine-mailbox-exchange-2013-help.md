---
title: '스팸 격리 사서함 구성: Exchange 2013 Help'
TOCTitle: 스팸 격리 사서함 구성
ms:assetid: 907d2f90-2a62-4d59-a4cf-945fef2e963f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123746(v=EXCHG.150)
ms:contentKeyID: 50483662
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 스팸 격리 사서함 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-19_

콘텐츠 필터 에이전트에서 스팸으로 확인된 메시지를 스팸 격리 사서함으로 보낼 수 있습니다. SCL(스팸 지수) 격리 임계값을 사용하는 경우에는 격리된 모든 메시지가 NDR(배달 못 함 보고서)로서 래핑되며 스팸 격리 사서함으로 지정한 SMTP 주소로 전송됩니다. 격리된 메시지를 검토하고 Microsoft Outlook의 다시 보내기 기능을 사용해 원래 받는 사람에게 보낼 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 45분

  - 기본적으로 스팸 방지 기능은 사서함 서버의 전송 서비스에서 사용되지 않도록 설정되어 있습니다. 일반적으로 Exchange 조직에서 들어오는 메시지를 수락하기 전에 스팸 방지 필터링을 미리 수행하지 않은 경우에만 사서함 서버에서 스팸 방지 기능을 사용하도록 설정할 수 있습니다. 자세한 내용은 [사서함 서버에서 스팸 방지 기능을 사용 하도록 설정](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)을 참조하세요.

  - 스팸 격리 사서함의 담당자는 잠재적으로 개인적이며 중요한 메시지를 본 다음 Exchange 조직의 모든 사람을 대신하여 메일을 보낼 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 콘텐츠 필터링이 사용하도록 설정되었는지 확인

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)의 "스팸 방지 기능" 항목

1.  다음 명령을 실행하여 콘텐츠 필터 에이전트가 Exchange 서버에 설치되어 있고 사용하도록 설정되어 있는지 확인합니다.
    
        Get-TransportAgent "Content Filter Agent"

2.  다음 명령을 실행하여 콘텐츠 필터링이 사용하도록 설정되어 있는지 확인합니다.
    
        Get-ContentFilterConfig | Format-List Enabled

자세한 내용은 [콘텐츠 필터링 관리](manage-content-filtering-exchange-2013-help.md)을 참조하십시오.

## 2단계: 스팸 격리를 위한 전용 사서함 만들기

전용 스팸 격리 사서함을 만들려면 다음 단계를 수행해야 합니다.

  - **전용 Exchange 데이터베이스 만들기**   스팸 격리 사서함에 대한 전용 데이터베이스를 만드는 것이 좋습니다. 저장소 할당량 제한에 도달할 경우 메시지가 손실되므로 스팸 격리 사서함은 큰 데이터베이스를 가져야 합니다. 자세한 내용은 [Exchange 2013의 사서함 데이터베이스를 관리 합니다.](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)를 참조하십시오.

  - **전용 사서함 및 사용자 계정 만들기**   이 스팸 격리 사서함에 대한 전용 사서함과 Active Directory 사용자 계정을 만드는 것이 좋습니다. 자세한 내용은 [사용자 사서함 만들기](create-user-mailboxes-exchange-2013-help.md)를 참조하십시오.
    
    조직의 규정 준수 정책과 요구 사항에 따라 메시징 레코드 관리, 사서함 할당량, 위임 권한 등과 같은 받는 사람 정책을 적용할 수 있습니다. 자세한 내용은 [메시징 레코드 관리](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/messaging-records-management/messaging-records-management)를 참조하십시오.
    

    > [!NOTE]
    > 저장소 할당량 때문에 격리된 메시지가 거부되는 경우 해당 메시지가 손실됩니다. 격리된 메시지가 NDR로 래핑되기 때문에 격리된 메시지에 대해서는 NDR이 생성되지 않습니다.



  - **Outlook 구성**   조직의 요구 사항을 충족하도록 Outlook 위임 액세스 권한을 구성해야 합니다. 또한 **메시지** 보기에 원래 `Sender[#0x0069001E]`, `Recipient[#0x0E04001E]` 및 `Bcc[#0x0E02001E]` 필드를 표시하도록 Outlook 프로필을 구성하는 것이 좋습니다. 자세한 내용은 [릴리스 스팸 격리 사서함에서 메시지를 격리](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md)을 참조하십시오.

## 3단계: 스팸 격리 사서함 지정

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)의 "스팸 방지 기능" 항목

다음 명령을 실행합니다.

    Set-ContentFilterConfig -QuarantineMailbox <SmtpAddress>

이 예에서는 스팸 격리 임계값을 초과하는 모든 메시지를 spamQ@contoso.com으로 보냅니다.

    Set-ContentFilterConfig -QuarantineMailbox spamQ@contoso.com

## 이 단계의 작동 여부는 어떻게 확인합니까?

스팸 격리 사서함이 지정되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-ContentFilterConfig | Format-List QuarantineMailbox

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 4단계: SCL 격리 임계값 구성

SCL 격리 임계값은 잠재적 스팸으로 식별된 특정 메시지가 스팸 격리 사서함에 배달되는 값입니다. SCL 격리 임계값은 0-9 사이의 값으로 설정할 수 있으며 0은 스팸일 가능성이 낮고 9는 스팸일 가능성이 가장 높은 것으로 간주됩니다.

조직의 요구 사항에 맞도록 SCL 임계값을 조정하는 방법과 받는 사람별 SCL 임계값을 조정하는 방법은 [콘텐츠 필터링 관리](manage-content-filtering-exchange-2013-help.md)을 참조하십시오.

## 5단계: 스팸 격리 사서함 관리

스팸 격리 사서함을 관리할 때는 다음 지침을 따릅니다.

  - 원본 메시지를 다시 보내려면 Outlook의 다시 보내기 기능을 사용하여 스팸 격리 사서함으로 전송된 항목을 보냅니다.
    
    자세한 내용은 [릴리스 스팸 격리 사서함에서 메시지를 격리](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md)을 참조하십시오.

  - 스팸 격리 사서함의 크기가 허용되는 범위로 유지되도록 스팸 격리 사서함을 모니터링합니다. 더 큰 받는 사람 집합, 더 큰 메시지의 자연적 추세 또는 SCL 격리 작업에 대한 임계값으로 인해 전자 메일 메시지의 볼륨이 변경될 수 있습니다.

  - 스팸 격리 사서함에서 가양성을 모니터링합니다. 스팸 격리 사서함에 가양성이 많이 포함되어 있으면 SCL 격리 임계값을 조정합니다. 가양성이 스팸 격리 사서함에 배달되는 이유를 확인하는 방법에 대한 자세한 내용은 [스팸 방지 스탬프](anti-spam-stamps-exchange-2013-help.md)를 참조하십시오.

  - 스팸 격리 사서함에서 격리된 메시지를 복구하려면 동일한 Outlook 프로필을 사용하십시오. 메시지를 복구하기 위해 다른 Outlook 프로필에 사용 권한을 적용할 수 없습니다. 다른 Outlook 프로필을 사용하여 스팸 격리 사서함으로부터 메시지를 복구하거나 전달할 수 없습니다.


> [!IMPORTANT]
> 스팸으로 식별된 NDR은 해당 SCR 등급에서 격리되어야 한다는 것을 나타내더라도 삭제됩니다. NDR은 스팸 격리 사서함에 배달되지 않습니다. 이러한 메시지를 추적하려면 에이전트 로그나 메시지 추적 로그를 사용합니다. 자세한 내용은 <A href="anti-spam-agent-logging-exchange-2013-help.md">스팸 방지 에이전트 로깅</A>을 참조하십시오.



## 6단계: SCL 격리 임계값 조정

SCL 격리 임계값을 구성한 후 설정을 주기적으로 모니터링하고 조직의 요구 사항에 기초하여 조정합니다. 예를 들어 너무 많은 가양성이 스팸 격리 사서함에 필터링될 경우 SCL 격리 임계값을 더 큰 수로 올립니다. SCL 격리 임계값을 조정하는 방법에 대한 자세한 내용은 [스팸 지수 임계값](spam-confidence-level-threshold-exchange-2013-help.md)을 참조하십시오.

