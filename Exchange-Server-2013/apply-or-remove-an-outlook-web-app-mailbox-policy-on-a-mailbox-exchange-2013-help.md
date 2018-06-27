---
title: '사서함에는 Outlook Web App 사서함 정책 적용 또는 제거: Exchange 2013 Help'
TOCTitle: 사서함에는 Outlook Web App 사서함 정책 적용 또는 제거
ms:assetid: 51d8e269-b0d5-4bc7-9b3d-0460871e54fa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876884(v=EXCHG.150)
ms:contentKeyID: 50483099
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에는 Outlook Web App 사서함 정책 적용 또는 제거

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-12_

하나 이상의 사서함에 Outlook Web App 사서함 정책을 적용하거나 EAC나 셸을 사용하여 정책을 제거할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "Outlook Web App 사서함 정책" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## Outlook Web App 사서함 정책 적용

## EAC를 사용하여 Outlook Web App 사서함 정책 적용

1.  EAC에서 **받는 사람** \> **사서함**을 클릭합니다.

2.  작업 창에서 Outlook Web App 사서함 정책을 적용할 사서함을 클릭하여 선택합니다. 사서함을 여러 개 선택할 수도 있습니다.

3.  **사서함을 하나 선택한 경우:**
    
    1.  세부 정보 창에서 **전자 메일 연결**로 스크롤하여 **세부 정보 보기**를 클릭합니다.
    
    2.  **찾아보기**를 클릭하여 사용 가능한 사서함 정책을 보고 원하는 정책을 선택합니다.
    
    3.  **저장**을 클릭하여 선택한 정책을 선택한 사서함에 할당합니다.
    
    **사서함을 하나 이상 선택한 경우:**
    
    1.  세부 정보 창에서 **Outlook Web App**으로 스크롤하여 **정책 할당**을 클릭합니다.
    
    2.  **찾아보기**를 클릭하여 사용 가능한 사서함 정책을 보고 원하는 정책을 선택합니다.
    
    3.  **저장**을 클릭하여 선택한 정책을 선택한 사서함에 할당합니다.

## 셸을 사용하여 기존 사서함에 Outlook Web App 사서함 정책 적용

이 예에서는 이름이 "Calendar"인 Outlook Web App 사서함 정책을 사용자 tony@contoso.com의 사서함에 적용합니다.

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:Calendar

구문과 매개 변수에 대한 자세한 내용은 [Set-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb125264\(v=exchg.150\))를 참조하십시오.

## Outlook Web App 사서함 정책 제거

## EAC를 사용하여 Outlook Web App 사서함 정책 제거

1.  EAC에서 **받는 사람** \> **사서함**을 클릭합니다.

2.  작업 창에서 Outlook Web App 사서함 정책을 제거할 사서함을 선택합니다.

3.  세부 정보 창에서 **전자 메일 연결**로 스크롤하여 **세부 정보 보기**를 클릭합니다.
    
    사서함 정책이 할당되어 있으면 **지우기**를 클릭하여 사서함에서 제거합니다.

4.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용하여 기존 사서함에서 Outlook Web App 사서함 정책 제거

이 예에서는 사용자 tony@contoso.com의 사서함에서 Outlook Web App 사서함 정책을 제거합니다.

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:$null

구문과 매개 변수에 대한 자세한 내용은 [Set-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb125264\(v=exchg.150\))를 참조하십시오.

