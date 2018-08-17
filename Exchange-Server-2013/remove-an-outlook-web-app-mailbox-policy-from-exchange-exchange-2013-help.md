---
title: 'Exchange에서 Outlook Web App 사서함 정책 제거: Exchange 2013 Help'
TOCTitle: Exchange에서 Outlook Web App 사서함 정책 제거
ms:assetid: edab7bac-b62c-4b82-8f21-dcac77cf0e8f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351239(v=EXCHG.150)
ms:contentKeyID: 50484453
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange에서 Outlook Web App 사서함 정책 제거

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-03-15_

EAC 또는 셸을 사용 하 여 Exchange 조직에서 MicrosoftOutlook Web App 사서함 정책을 제거할 수 있습니다.

Outlook Web App 사서함 정책에 관련 된 추가 관리 작업을 [Outlook Web App 사서함 정책](outlook-web-app-mailbox-policies-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "Outlook Web App 사서함 정책" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 Outlook Web App 사서함 정책 제거

1.  EAC에서 **사용 권한** \> **Outlook Web App 정책**을 클릭합니다.

2.  결과 창에서 제거 하려는 사서함 정책을 선택 하려면 클릭 합니다.

3.  **삭제** 단추를 클릭합니다.

4.  확인 창에서 **예** 를 사서함 정책 제거를 클릭 하거나 취소 하려면 **아니요** 클릭 합니다.

## 셸을 사용하여 Outlook Web App 사서함 정책 제거

이 예제에서는 `Policy1`라는 Outlook Web App 사서함 정책을 제거 합니다.

    Remove-OwaMailboxPolicy -Name Policy1 

구문과 매개 변수에 대 한 자세한 내용은 [Remove-OwaMailboxPolicy](https://technet.microsoft.com/ko-kr/library/dd298103\(v=exchg.150\))을 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

Outlook Web App 사서함 정책의 성공적으로 제거 했는지 확인.

  - EAC에서 **사용 권한** 을 클릭 \> **Outlook Web App 정책을** 합니다. 제거한 정책 목록에 더이상 표시 되어야 합니다.

