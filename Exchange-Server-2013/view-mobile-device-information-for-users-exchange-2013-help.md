---
title: '사용자에 대 한 모바일 장치 정보 보기: Exchange 2013 Help'
TOCTitle: 사용자에 대 한 모바일 장치 정보 보기
ms:assetid: 4fd263c0-ad61-416c-bd68-339bf66605cf
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997974(v=EXCHG.150)
ms:contentKeyID: 50483086
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자에 대 한 모바일 장치 정보 보기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-11-29_

사용자는 여러 개의 모바일 장치를 구성하여 MicrosoftExchange Server 2013과 동기화할 수 있습니다. EAC 또는 셸을 사용하여 특정 사용자와 연결된 모바일 장치 목록을 볼 수 있습니다.

모바일 장치와 관련된 추가 관리 작업은 [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 주제의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "모바일 장치 사서함 정책" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사용자의 모바일 장치 정보 보기

EAC에는 현재 사용자 사서함과 동기화되고 있는 모바일 장치의 목록이 표시됩니다. 제품군, 모델, 전화 번호 또는 상태별로 모바일 장치를 볼 수 있습니다.

1.  EAC에서 **받는 사람** \> **사서함**을 클릭하고 사서함을 선택합니다.

2.  세부 정보 창에서 **전화 및 음성 기능**으로 스크롤한 다음 **세부 정보 보기**를 클릭하여 **모바일 장치 세부 정보** 화면을 표시합니다.

## 셸을 사용하여 사용자의 모바일 장치 정보 보기

**Get-MobileDevice** cmdlet을 사용하여 특정 사용자의 모바일 장치 목록을 볼 수 있습니다.

1.  다음 명령을 실행합니다.
    
        Get-MobileDevice -Mailbox useralias

