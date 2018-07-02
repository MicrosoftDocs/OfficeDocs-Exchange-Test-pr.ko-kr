---
title: 'Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync
ms:assetid: 5fafaff3-eb37-4fdb-95f0-e56c45ea5884
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998357(v=EXCHG.150)
ms:contentKeyID: 50483238
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange Server 2013용 Exchange ActiveSync 클라이언트 프로토콜에 대해 알아봅니다. 보안 기능, 관리 가능한 항목, 안전하게 만드는 방법, Windows Phone 7과의 동기화 문제를 방지하는 방법 등 Exchange ActiveSync의 기능에 대해 알아봅니다.


> [!TIP]
> 이 항목은 관리자용입니다. Windows Phone, iOS 또는 Android 장치를 설정하여 Office 365 또는 Exchange Server 사서함에 액세스하기를 원하시나요? 다음 항목을 확인하세요. 
> <UL>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=615415">Windows Phone에서 전자 메일 설정</A></P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=615414">IPhone, iPad 또는 iPod Touch에서 전자 메일 설정</A></P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/?linkid=615417">Android 전화 또는 태블릿에서 전자 메일 설정</A></P></LI></UL>



Exchange ActiveSync는 모바일 장치를 Exchange 사서함과 동기화하는 데 사용할 수 있는 클라이언트 프로토콜입니다. Exchange ActiveSync는 Microsoft Exchange 2013을 설치할 때 기본적으로 설정됩니다.

**목차**

Exchange ActiveSync 개요

Exchange ActiveSync의 기능

Exchange ActiveSync 관리

Windows Phone 7 동기화

## Exchange ActiveSync 개요

Exchange ActiveSync는 대기 시간이 길고 대역폭이 낮은 네트워크에서 작동하도록 최적화된 Microsoft Exchange 동기화 프로토콜입니다. HTTP와 XML을 기반으로 한 이 프로토콜을 사용하면 휴대폰에서 Microsoft Exchange가 실행되는 서버의 조직 정보에 액세스할 수 있습니다. 휴대폰 사용자는 Exchange ActiveSync를 통해 전자 메일, 일정, 연락처, 작업에 액세스할 수 있으며 오프라인 작업 시에도 계속해서 이 정보에 액세스할 수 있습니다.


> [!NOTE]
> Exchange ActiveSync는 공유 사서함 또는 대리인 액세스를 지원하지 않습니다.




> [!IMPORTANT]
> Windows Phone 7 휴대폰은 모든 Exchange ActiveSync 사서함 정책 설정 중 일부만 지원합니다. 전체 목록을 보려면 Windows Phone 7 동기화를 참조하십시오.



## Exchange ActiveSync의 기능

Exchange ActiveSync는 다음과 같은 기능을 제공합니다.

  - HTML 메시지 지원

  - 추가 작업 플래그 지원

  - 전자 메일 메시지의 대화 그룹화

  - 전체 대화를 동기화 또는 동기화하지 않는 기능

  - SMS(문자 서비스) 메시지와 사용자의 Exchange 사서함 동기화

  - 메시지 회신 상태 보기 지원

  - 빠른 메시지 검색 지원

  - 모임 참석자 정보

  - 향상된 Exchange 검색

  - PIN 재설정

  - 암호 정책을 통한 향상된 장치 보안

  - 무선 프로비전을 위한 자동 검색

  - 사용자가 자리를 비운 경우, 휴가 중 또는 부재 중인 경우 자동 회신 설정 지원

  - 작업 동기화 지원

  - Direct Push

  - 연락처 가용성 정보 지원

## Exchange ActiveSync 관리

기본적으로 Exchange ActiveSync는 사용하도록 설정되어 있습니다. Exchange 사서함이 있는 모든 사용자는 모바일 장치를 Microsoft Exchange 서버와 동기화할 수 있습니다.

다음과 같은 Exchange ActiveSync 작업을 수행할 수 있습니다.

  - 사용자가 Exchange ActiveSync를 사용하거나 사용하지 못하도록 설정합니다.

  - 최소 암호 길이, 장치 잠금, 최대 암호 입력 실패 횟수 등의 정책을 설정합니다.

  - 분실 또는 도난 당한 휴대폰에서 데이터를 모두 지울 수 있는 원격 지우기 기능 시작

  - 다양한 형식으로 보거나 내보내기 위한 다양한 보고서 실행

  - 장치 액세스 규칙을 통해 조직과 동기화되는 모바일 장치 유형 제어

## Exchange ActiveSync의 보안 기능

Exchange 서버와 모바일 장치 간의 통신에 SSL(Secure Sockets Layer) 암호화를 사용하도록 Exchange ActiveSync를 구성할 수 있습니다.

## Exchange ActiveSync에서 모바일 장치 액세스 관리

동기화가 가능한 모바일 장치를 제어할 수 있습니다. 조직에 새로 연결되는 모바일 장치를 모니터링하거나 연결이 허용되는 모바일 장치 유형을 결정하는 규칙을 설정하면 됩니다. 동기화가 가능한 모바일 장치를 지정하는 데 어떤 방법을 사용하든 언제든지 특정 장치 및 사용자에 대해 액세스를 승인 또는 거부할 수 있습니다.

## Exchange ActiveSync의 장치 보안 기능

Exchange ActiveSync에서는 Exchange 서버와 모바일 장치 간의 통신 보안 옵션을 구성하는 기능을 비롯하여 다음과 같은 기능을 제공함으로써 모바일 장치의 보안을 강화합니다.

  - **원격 지우기**   모바일 장치가 분실 또는 도난되었거나 손상된 경우 Exchange Server 컴퓨터 또는 웹 브라우저에서 Outlook Web App을 사용하여 원격 지우기 명령을 실행할 수 있습니다. 이 명령은 모바일 장치에서 모든 데이터를 지웁니다.

  - **장치 암호 정책**   Exchange ActiveSync에서는 여러 장치 암호 옵션을 구성할 수 있습니다.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>iOS7 지문 판독기 기술은 장치 암호로 사용할 수 없습니다. iOS7 지문 판독기를 사용하기로 선택한 경우에도 조직의 모바일 장치 사서함 정책에서 장치 암호를 필요로 하는 경우 장치 암호를 만들고 입력해야 합니다.</td>
    </tr>
    </tbody>
    </table>
    
    장치 암호 옵션은 다음과 같습니다.
    
      - **최소 암호 길이(문자)**   모바일 장치 암호의 길이를 지정하는 옵션입니다. 기본 길이는 4자이며 최대 길이는 18자입니다.
    
      - **최소 문자 집합 수**   이 텍스트 상자를 사용하여 영숫자 암호의 복잡성을 지정하고 사용자가 소문자, 대문자, 기호 및 숫자 중에서 다양한 여러 가지 문자 집합을 사용하도록 합니다.
    
      - **영숫자 암호 필요**   암호 보안 수준을 결정하는 옵션입니다. 이 옵션을 통해 암호에 숫자 외에 문자나 기호를 사용하도록 적용할 수 있습니다.
    
      - **비활성화 시간(초)**   사용자에게 암호를 입력하여 모바일 장치의 잠금을 해제하라는 메시지가 표시되기 전에 모바일 장치가 비활성화된 상태로 있어야 하는 시간을 지정합니다.
    
      - **암호 기록 적용**   사용자가 휴대폰에서 이전 암호를 다시 사용하지 못하도록 하려면 이 확인란을 선택합니다. 설정하는 숫자로 사용자가 다시 사용할 수 없는 이전 암호의 수가 결정됩니다.
    
      - **암호 복구 사용**   모바일 장치에 대해 암호 복구를 사용하도록 설정하려면 이 확인란을 선택합니다.  관리자는 **Get-ActiveSyncDeviceStatistics** cmdlet을 사용하여 사용자 복구 암호를 조회할 수 있습니다.
    
      - **장치 지우기 시도 횟수**   이 옵션을 사용하면 여러 번 암호를 입력하는 데 실패하는 경우 휴대폰의 메모리를 지워지게 할지 여부를 지정할 수 있습니다.

  - **장치 암호화 정책**   사용자 그룹에 대해 적용할 수 있는 다양한 모바일 장치 암호화 정책이 있습니다. 다음과 같은 정책이 포함됩니다.
    
      - **장치에서 암호화 필요**   모바일 장치에서 암호화가 필요한 경우 이 확인란을 선택합니다. 모바일 장치에 있는 모든 정보를 암호화하여 보안이 강화됩니다.
    
      - **저장소 카드에서 암호화 필요**   모바일 장치의 이동식 저장소 카드에서 암호화가 필요한 경우 이 확인란을 선택합니다. 이를 통해 모바일 장치의 저장소 카드에 대한 모든 정보를 암호화하여 보안을 강화합니다.

## Windows Phone 7 동기화

조직에 Windows Phone 7 모바일 장치가 있는 경우 특정 모바일 장치 사서함 정책 속성이 구성되어 있으면 장치에 동기화 문제가 생깁니다. Windows Phone 7 휴대폰이 Exchange 사서함과 동기화되도록 하려면 **AllowNonProvisionableDevices** 속성을 True로 설정하거나 다음과 같은 모바일 장치 사서함 정책 속성만 구성합니다.

  - PasswordRequired

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - DeviceWipeThreshold

  - AllowSimplePassword

  - PasswordExpiration

  - PasswordHistory

  - DisableRemovableStorage

  - DisableIrDA

  - DisableDesktopSync

  - BlockRemoteDesktop

  - BlockInternetSharing

