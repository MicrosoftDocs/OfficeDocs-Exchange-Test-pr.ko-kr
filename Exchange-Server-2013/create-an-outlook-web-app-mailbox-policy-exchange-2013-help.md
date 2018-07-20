---
title: 'Outlook Web App 사서함 정책 만들기: Exchange 2013 Help'
TOCTitle: Outlook Web App 사서함 정책 만들기
ms:assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335191(v=EXCHG.150)
ms:contentKeyID: 50482834
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App 사서함 정책 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-05-30_

일련의 공용 정책 설정을 적용할 Outlook Web App 사서함 정책을 만들 수 있습니다. Outlook Web App 사서함 정책은 특정 사용자 그룹에 대한 설정(예: 첨부 파일 설정)을 적용하고 표준화하는 데 유용합니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이 cmdlet을 실행하려면 먼저 사용 권한을 할당받아야 합니다. 이 cmdlet의 모든 매개 변수가 이 항목에 나열되지만 사용자에게 할당된 사용 권한에 포함되지 않은 일부 매개 변수에는 액세스할 수 없습니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "Outlook Web App 사서함 정책" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 Outlook Web App 사서함 정책 만들기

1.  EAC에서 **사용 권한** \> **Outlook Web App 정책**을 클릭합니다.

2.  **새로 만들기** 단추를 클릭합니다.

3.  
    
    정책의 이름을 입력합니다.

4.  
    
    확인란을 사용하여 기능을 사용하거나 사용하지 않도록 설정합니다. 기본적으로 가장 일반적인 기능이 표시됩니다. 사용하거나 사용하지 않도록 설정할 수 있는 모든 기능을 보려면 **기타 옵션**을 클릭합니다.
    

    > [!NOTE]
    > Outlook Web App 사서함 정책의 기능 설정은 Outlook Web App 가상 디렉터리 설정을 무시합니다. 셸에서 <STRONG>Set-CASMailbox</STRONG> cmdlet을 사용하여 개별 사용자에 대한 구분 설정을 변경할 수 있습니다.



5.  **저장**을 클릭하여 정책을 저장합니다.

## 셸을 사용하여 Outlook Web App 사서함 정책 만들기

이 예에서는 `Policy1`이라는 Outlook Web App 사서함 정책을 만듭니다.

  - 셸에서 다음 명령을 실행합니다.
    
        New-OwaMailboxPolicy -Name Policy1

구문과 매개 변수에 대한 자세한 내용은 [New-OwaMailboxPolicy](https://technet.microsoft.com/ko-kr/library/dd351067\(v=exchg.150\))를 참조하십시오. 셸을 사용하여 Outlook Web App 사서함 정책을 구성하는 방법에 대한 자세한 내용은 [Set-OwaMailboxPolicy](https://technet.microsoft.com/ko-kr/library/dd297989\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

Outlook Web App 사서함 정책을 만들었는지 확인하려면

  - EAC에서 **사용 권한** \> **Outlook Web App 정책**을 클릭하고 새로운 사서함 정책을 찾습니다.

