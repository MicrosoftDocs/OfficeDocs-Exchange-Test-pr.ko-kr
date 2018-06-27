---
title: '휴대폰 원격 초기화: Exchange 2013 Help'
TOCTitle: 휴대폰 원격 초기화
ms:assetid: 67ba838e-031d-4a98-b277-170683b6f520
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998614(v=EXCHG.150)
ms:contentKeyID: 52057988
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 휴대폰 원격 초기화

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2013-02-06_

사용자들은 매일 중요한 회사 정보를 지니고 다닙니다. 사용자 중 한 명이 휴대폰을 분실할 경우 이러한 데이터가 다른 사람의 손에 넘어갈 수 있습니다. 사용자 중 한 명이 휴대폰을 분실할 경우 EAC(Exchange 관리 센터)나 Exchange 관리 셸을 사용하여 휴대폰에서 모든 회사 정보 및 사용자 정보를 지울 수 있습니다.


> [!NOTE]
> 이 항목에서는 MicrosoftOutlook Web App을 사용하여 휴대폰에서 원격 지우기를 수행하는 방법에 대한 지침도 제공합니다. 원격 지우기를 수행하려면 사용자가 Outlook Web App에 로그인해야 합니다.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "모바일 장치" 항목

  - 이 절차에서는 설치된 응용 프로그램, 사진 및 개인 정보 등을 비롯하여 휴대폰의 모든 데이터를 지웁니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사용자 휴대폰 내용 지우기

EAC를 사용하여 사용자 휴대폰의 내용을 지우거나 아직 완료되지 않은 원격 지우기를 취소할 수 있습니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자를 선택하고 **모바일 장치**에서 **자세히 보기**를 선택합니다.

3.  **모바일 장치 세부 정보** 페이지에서 분실한 모바일 장치를 선택한 후 **데이터 지우기**를 선택합니다.

4.  **저장**을 선택합니다.

## 셸을 사용하여 사용자 휴대폰 내용 지우기

셸에서 **Clear-MobileDevice** cmdlet을 사용하여 사용자 휴대폰 내용을 지울 수 있습니다.

다음 명령은 WM\_TonySmith라는 장치의 내용을 지우고 admin@contoso.com으로 확인 메시지를 보냅니다.

    Clear-MobileDevice -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"

## Outlook Web App을 사용하여 사용자 휴대폰 내용 지우기

사용자는 Outlook Web App을 사용하여 자신의 휴대폰의 내용을 지울 수 있습니다.

1.  Outlook Web App에서 **설정 \> 전화 \> 모바일 장치**를 선택합니다.

2.  휴대폰을 선택합니다.

3.  **장치 지우기** 아이콘을 클릭하거나 누릅니다.

## 작동 여부는 어떻게 확인합니까?

여러 가지 방법으로 원격 지우기가 완료되었는지 확인할 수 있습니다.

  - 구성된 *–NotificationEmailAddresses* 매개 변수와 함께 **Clear-MobileDevice** cmdlet을 실행합니다. 원격 지우기가 완료되면 메시지가 제공된 전자 메일 주소로 전송됩니다.

  - EAC에서 모바일 장치의 상태를 확인합니다. 상태가 **보류 중인 데이터 지움**에서 **지우기 완료**로 바뀝니다.

  - Outlook Web App에서 모바일 장치의 상태를 확인합니다. 상태가 **보류 중인 데이터 지움**에서 **지우기 완료**로 바뀝니다.

