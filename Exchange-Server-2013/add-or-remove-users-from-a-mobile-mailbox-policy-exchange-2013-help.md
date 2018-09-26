---
title: '추가 또는 모바일 사서함 정책에서 사용자 제거: Exchange 2013 Help'
TOCTitle: 추가 또는 모바일 사서함 정책에서 사용자 제거
ms:assetid: 4ca8e395-c074-4165-b788-16fae3e2ccab
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997929(v=EXCHG.150)
ms:contentKeyID: 50483063
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 추가 또는 모바일 사서함 정책에서 사용자 제거

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-07-16_

모바일 장치 사서함 정책을 사용하면 보안 및 모바일 장치 설정의 공통된 집합을 사용자 그룹에 적용할 수 있습니다. 여러 모바일 장치 사서함 정책을 만들 수 있습니다.


> [!WARNING]
> Microsoft Exchange Server 2013을 설치하면 기본 모바일 장치 사서함 정책이 생성되고 모든 사용자에게 자동으로 이 정책이 할당됩니다.



모바일 장치 사서함 정책과 관련된 추가 관리 작업에 대한 자세한 내용은 [모바일 장치 사서함 정책](mobile-device-mailbox-policies-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 주제의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "모바일 장치 사서함 정책" 항목.

  - EAC의 **모바일** \> **모바일 장치 사서함 정책**에서 모바일 장치 사서함 정책 하나를 사용 가능한 상태로 설정해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 사용자의 모바일 장치 사서함 정책 변경

EAC 또는 셸을 사용하여 사용자의 모바일 장치 사서함 정책을 변경할 수 있습니다.

## EAC를 사용하여 사용자의 모바일 장치 사서함 정책 변경

EAC를 사용하여 단일 사용자의 모바일 장치 사서함 정책을 변경할 수 있습니다.

1.  EAC에서 **받는 사람** \> **사서함**을 클릭하고 사서함을 선택합니다.

2.  세부 정보 창에서 **전화 및 음성 기능**으로 스크롤한 다음 **세부 정보 보기**를 선택하여 **모바일 장치 세부 정보** 화면을 표시합니다.

3.  현재 할당되어 있는 모바일 장치 사서함 정책이 표시됩니다. 모바일 장치 사서함 정책을 변경하려면 **찾아보기**를 클릭합니다.

4.  목록에서 적절한 모바일 장치 사서함 정책을 선택하고 **확인**을 클릭한 다음 **저장**을 클릭합니다.

## 셸을 사용하여 모바일 장치 사서함 정책에 사용자 추가

셸에서 **Set-CASMailbox** cmdlet을 사용 하 여 단일 사용자의 모바일 장치 사서함 정책을 변경할 수 있습니다.

1.  셸에서 다음 명령을 실행합니다.

    ```powershell
    Set-CASMailbox -Identity tony@contoso.com -ActiveSyncMailboxPolicy "Sales" 
    ```

## 작동 여부는 어떻게 확인합니까?

사용자의 모바일 장치 사서함 정책을 성공적으로 변경했는지 확인하려면 다음 중 하나를 수행하십시오.

1.  EAC에서 **받는 사람** \> **사서함**을 클릭하고 특정 받는 사람을 선택합니다. 세부 정보 창에서 **전화 및 음성 기능**으로 스크롤하여 **세부 정보 보기**를 클릭합니다.

2.  셸에서 다음 명령을 실행합니다.

    ```powershell    
    Get-CASMailbox -Identity tony@contoso.com 
    ```

## 동시에 여러 사용자의 모바일 장치 사서함 정책 변경

동시에 여러 사용자의 모바일 장치 사서함 정책을 변경하려면 EAC의 대량 편집 기능을 사용하거나 셸을 사용하여 필터링된 사용자 집합에 대해 모바일 장치 사서함 정책을 변경합니다.

## EAC의 대량 편집 도구를 사용하여 여러 사용자의 모바일 장치 사서함 정책 변경

대량 편집 기능을 사용하여 한 번에 여러 사용자의 모바일 장치 사서함 정책을 업데이트할 수 있습니다.

1.  EAC에서 **받는 사람** \> **사서함**을 클릭합니다.

2.  여러 사용자를 선택합니다.

3.  세부 정보 창에서 **Exchange ActiveSync**로 스크롤하여 **정책 업데이트**를 클릭합니다.

4.  **찾아보기**를 클릭하고 모바일 장치 사서함 정책을 선택합니다.

5.  **확인**을 클릭한 다음 **저장**을 클릭합니다.

## 셸을 사용하여 필터링된 사용자 집합에 대해 모바일 장치 사서함 정책 변경

셸을 사용하여 필터링된 사용자 집합에 대해 모바일 장치 사서함 정책을 변경할 수 있습니다. 다양한 특성을 기준으로 사용자를 필터링할 수 있습니다.

1.  셸에서 다음 명령을 실행합니다.

    ```powershell    
    Get-Mailbox | where { $_.CustomAttribute1 -match "Manager"
     } | Set-CASMailbox -activesyncmailboxpolicy(Get-ActiveSyncMailboxPolicy "Contoso").Identity
    ````

    > [!NOTE]
    > <CODE>CustomAttribute1</CODE>을 <STRONG>Get-Mailbox</STRONG> 개체의 속성 중 하나로 대체할 수 있습니다. 전체 목록을 보려면 다음을 입력합니다. <CODE>Get-Mailbox username |fl</CODE>.



## 작동 여부는 어떻게 확인합니까?

사용자의 모바일 장치 사서함 정책을 성공적으로 변경했는지 확인하려면 다음 중 하나를 수행하십시오.

1.  EAC에서 **받는 사람** \> **사서함**을 클릭하고 특정 받는 사람을 선택합니다. 세부 정보 창에서 **전화 및 음성 기능**으로 스크롤하여 **세부 정보 보기**를 클릭합니다.

2.  셸에서 다음 명령을 실행합니다.
    
    ```powershell
    Get-CASMailbox -Identity tony@contoso.com
    ```
