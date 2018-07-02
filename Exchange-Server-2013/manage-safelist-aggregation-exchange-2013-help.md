---
title: '수신 허용 목록 집계 관리: Exchange 2013 Help'
TOCTitle: 수신 허용 목록 집계 관리
ms:assetid: 5ac17168-f411-4cb7-ae98-ebefb865b210
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998280(v=EXCHG.150)
ms:contentKeyID: 50483189
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 수신 허용 목록 집계 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

*수신 허용 목록 집계*는 Microsoft Outlook과 Microsoft Exchange Server 2013 간에 공유되는 스팸 방지 기능입니다. 이 기능은 수신 허용 - 받는 사람 목록, 수신 허용 - 보낸 사람 목록, 수신 거부 목록 및 Outlook 사용자가 구성한 연락처 데이터에서 데이터를 수집하여 Exchange 스팸 방지 에이전트에 제공합니다. 수신 허용 목록 집계를 사용하면 스팸 방지 에이전트를 실행 중인 Exchange 서버에서 수행한 스팸 방지 필터링의 가양성 수를 줄일 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "받는 사람의 프로비전 권한" 섹션 및 [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) 항목의 "스팸 방지 기능" 섹션

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 기본적으로 스팸 방지 기능은 사서함 서버의 전송 서비스에서 사용되지 않도록 설정되어 있습니다. 일반적으로 Exchange 조직에서 들어오는 메시지를 수락하기 전에 스팸 방지 필터링을 미리 수행하지 않은 경우에만 사서함 서버에서 스팸 방지 기능을 사용하도록 설정할 수 있습니다. 자세한 내용은 [사서함 서버에서 스팸 방지 기능을 사용 하도록 설정](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)을 참조하세요.

  - **Update-SafeList** cmdlet을 실행할 때 발생할 수 있는 네트워크 및 복제 트래픽을 고려해야 합니다. 수신 허용 목록 사용량이 많은 여러 사서함에서 이 명령을 실행하면 과도한 트래픽이 발생할 수 있습니다. 여러 사서함에서 이 명령을 실행할 때는 사용량이 적은 업무 외 시간에 실행하는 것이 좋습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 사서함 수신 허용 목록 모음 제한 구성

사용자가 구성할 수 있는 수신 허용 - 보낸 사람 및 수신 거부의 최대 개수를 구성할 수 있습니다. 기본적으로 사용자는 최대 5,000개의 수신 허용 - 보낸 사람 및 500개의 수신 거부를 구성할 수 있습니다.

수신 허용 - 보낸 사람 및 수신 거부의 최대 개수를 구성하려면 다음 명령을 실행합니다.

    Set-Mailbox <MailboxIdentity> -MaxSafeSenders <Integer> -MaxBlockedSenders <Integer>

이 예에서는 수신 허용 - 보낸 사람 최대 2,000개, 수신 거부 최대 200개가 되도록 사서함 john@contoso.com을 구성합니다.

    Set-Mailbox john@contoso.com -MaxSafeSenders 2000 -MaxBlockedSenders 200

## 작동 여부는 어떻게 확인합니까?

사서함 수신 허용 목록 모음 제한이 구성되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-Mailbox <Identity> | Format-List Name,Max*Senders

2.  표시된 값이 구성한 값과 일치하는지 확인합니다.

## 셸을 사용하여 Update-Safelist 명령 실행

Exchange 2013에서는 수신 허용 목록 집계가 자동으로 수행되므로 별도로 예약하거나 수동으로 **Update-Safelist** cmdlet을 실행할 필요가 없습니다. 하지만 수신 허용 목록 집계를 테스트하기 위해 이 cmdlet을 실행해야 할 경우가 있습니다.

이 예에서는 사서함 john@contoso.com에 대한 수신 허용 - 보낸 사람 목록을 Active Directory에 씁니다.

    Update-Safelist john@contoso.com -Type SafeSenders

구문과 매개 변수에 대한 자세한 내용은 [Update-SafeList](https://technet.microsoft.com/ko-kr/library/bb125034\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

수신 허용 목록 집계가 구성되었는지 확인하려면 다음 단계를 수행합니다.

## 1단계: 셸을 사용하여 Exchange 서버에서 콘텐츠 필터 에이전트를 사용하는지 확인

1.  다음 명령을 실행합니다.
    
        Get-ContentFilterConfig | Format-List Enabled

2.  출력에서 *Enabled* 매개 변수가 `True`로 표시되는 경우 콘텐츠 필터링을 사용하는 것입니다. 그렇지 않은 경우 다음 명령을 실행하여 Exchange 서버에서 콘텐츠 필터링 및 콘텐츠 필터 에이전트를 사용하도록 설정합니다.
    
        Set-ContentFilterConfig -Enabled $true

## 2단계: (선택 사항) ADSI 편집을 사용하여 수신 허용 목록 집계 데이터가 Edge 전송 서버로 복제되었는지 확인합니다.

이 단계는 주변 네트워크에 있는 Edge 전송 서버에서 콘텐츠 필터 에이전트를 실행하는 경우에만 필요합니다.

Edge 전송 서버의 AD LDS(Active Directory Lightweight Directory Services) 인스턴스에서 사용자 개체를 보고 사용자 개체에 대해 수신 허용 목록 모음 데이터가 업데이트되었는지와 Microsoft Exchange EdgeSync 서비스가 데이터를 AD LDS 인스턴스에 복제했는지 확인합니다.

각 사용자 개체에 대한 세 가지 수신 허용 목록 컬렉션 특성은 다음과 같습니다.

  - **msExchSafeRecipientsHash**   이 특성은 사용자에 대한 수신 허용 - 받는 사람 목록의 해시를 저장합니다.

  - **msExchSafeSendersHash**   이 특성은 사용자에 대한 수신 허용 - 보낸 사람 목록의 해시를 저장합니다.

  - **msExchBlockedSendersHash**   이 특성은 사용자에 대한 수신 거부 목록 컬렉션의 해시를 저장합니다.

특성에 16진수 문자열(예: `0xac 0xbd 0x03 0xca`)이 있으면 해당 사용자 개체가 업데이트된 것입니다. 특성의 값이 `<Not Set>`이면 특성이 업데이트되지 않은 것입니다.

AD LDS ADSI(Active Directory 서비스 인터페이스) 스냅인을 사용하여 특성을 검색하고 볼 수 있습니다.

## 3단계: 테스트 메시지를 보내 수신 허용 목록 집계가 작동하는지 확인

수신 허용 목록 집계가 작동하는지 테스트하려면 수신 허용 - 보낸 사람을 통해 메시지를 보냅니다. 수신 허용 목록 집계가 작동하지 않을 경우 이 메시지는 콘텐츠 필터링으로 차단됩니다. 수신 허용 목록 집계가 작동하는 경우 해당 메시지는 받은 편지함에 도착합니다.

1.  기존 외부 전자 메일 계정을 찾아서 사용하거나 Microsoft Hotmail 같은 무료 웹 기반 전자 메일 공급자에서 전자 메일 계정을 만듭니다.

2.  Microsoft Outlook의 수신 허용 - 보낸 사람 목록에 계정을 추가합니다.

3.  **Update-SafeList** cmdlet을 사용하여 해당 사서함의 수신 허용 목록 모음을 Active Directory에 복사합니다.

4.  옵션: 주변 네트워크에 있는 Edge 전송 서버에서 콘텐츠 필터 에이전트를 실행 중인 경우 **Start-EdgeSynchronization** cmdlet을 실행하여 EdgeSync 복제를 강제 실행합니다.

5.  차단된 구와 같은 특정 단어를 콘텐츠 필터링 구성에 추가합니다. 자세한 단계는 [콘텐츠 필터링 관리](manage-content-filtering-exchange-2013-help.md)를 참조하십시오.

6.  1단계의 외부 전자 메일 계정에서 5단계에서 구성한 차단된 구가 포함된 Exchange 사서함으로 메시지를 보냅니다.
    
    메시지가 받은 편지함으로 배달되면 수신 허용 목록 집계가 제대로 작동하는 것입니다.

