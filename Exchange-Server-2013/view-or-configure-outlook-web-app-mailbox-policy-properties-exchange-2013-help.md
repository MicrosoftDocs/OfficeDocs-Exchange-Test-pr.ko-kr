---
title: 'Outlook Web App 사서함 정책 속성 보기 또는 구성: Exchange 2013 Help'
TOCTitle: Outlook Web App 사서함 정책 속성 보기 또는 구성
ms:assetid: be012ffe-8fdb-4fb7-aebd-78b3a55593fa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351097(v=EXCHG.150)
ms:contentKeyID: 50484044
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App 사서함 정책 속성 보기 또는 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-04-13_

Outlook Web App 사서함 정책을 만든 후에는 Outlook Web App에서 사용할 수 있는 기능을 제어하는 다양한 옵션을 구성할 수 있습니다. 예를 들어 받은 편지함 규칙을 사용하거나 사용하지 않도록 설정하거나 또는 첨부 파일에 허용되는 파일 유형 목록을 만들 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "Outlook Web App 사서함 정책" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 Outlook Web App 사서함 정책 보기 또는 구성

1.  EAC에서 **사용 권한** \> **Outlook Web App 정책**을 클릭합니다.

2.  결과 창에서 보거나 구성할 사서함 정책을 클릭하여 선택합니다.

3.  **편집** 단추를 클릭합니다.

4.  
    
    **일반** 탭에서 정책 이름을 보거나 편집할 수 있습니다.

5.  
    
    **기능** 탭에서 확인란을 사용하여 기능을 사용하거나 사용하지 않도록 설정합니다. 기본적으로 가장 일반적인 기능이 표시됩니다. 사용하거나 사용하지 않도록 설정할 수 있는 모든 기능을 보려면 **기타 옵션**을 클릭합니다.
    

    > [!NOTE]
    > Outlook Web App 사서함 정책의 기능 설정은 Outlook Web App 가상 디렉터리 설정을 무시합니다. 셸에서 <STRONG>Set-CASMailbox</STRONG> cmdlet을 사용하여 개별 사용자에 대한 구분 설정을 변경할 수 있습니다.



6.  
    
    **파일 액세스** 탭에서 **직접 파일 액세스** 확인란 사용 하 여 파일 액세스 및 사용자에 대해 보기 옵션을 구성 합니다. 파일 액세스 사용자를 열거나 전자 메일 메시지에 첨부 된 파일의 내용을 볼 수 있습니다.
    
    파일 액세스는 사용자가 공용 컴퓨터에 로그인했는지 또는 개인 컴퓨터에 로그인했는지에 따라 제어할 수 있습니다. 사용자가 개인 컴퓨터 액세스와 공용 컴퓨터 액세스 중에서 선택할 수 있도록 하는 옵션은 폼 기반 인증을 사용 중인 경우에만 사용할 수 있습니다. 다른 모든 인증 형태는 기본적으로 개인 컴퓨터 액세스로 지정됩니다.

7.  **오프라인 액세스** 탭에서 옵션 단추를 사용하여 오프라인 액세스 가용성을 구성합니다.

8.  **저장**을 클릭하여 정책을 업데이트합니다.

## 셸을 사용하여 Outlook Web App 사서함 정책 구성

이 예에서는 기본 사서함 정책에서 일정에 액세스하도록 설정합니다.

    Set-OwaMailboxPolicy -Identity Default -CalendarEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-OwaMailboxPolicy](https://technet.microsoft.com/ko-kr/library/dd297989\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 Outlook Web App 사서함 정책 보기

이 예에서는 `Executives` 조직에 있는 Outlook Web App 사서함 정책 `Fabrikam`의 속성을 검색합니다.

    Get-OwaMailboxPolicy -Identity Fabrikam\Executives

구문과 매개 변수에 대한 자세한 내용은 [Get-OwaMailboxPolicy](https://technet.microsoft.com/ko-kr/library/dd351095\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

Outlook Web App 사서함 정책이 편집되었는지 확인하려면

1.  EAC에서 **사용 권한** \> **Outlook Web App 정책**을 클릭한 다음 특정 Outlook Web App 사서함 정책을 선택합니다.

2.  **편집** 단추를 클릭하여 사서함 정책의 속성을 봅니다.

3.  **저장** 또는 **취소**를 클릭하여 속성 페이지를 닫습니다.

