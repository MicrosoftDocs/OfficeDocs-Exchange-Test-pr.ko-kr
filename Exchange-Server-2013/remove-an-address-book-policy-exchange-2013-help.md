---
title: '주소록 정책 제거: Exchange 2013 Help'
TOCTitle: 주소록 정책 제거
ms:assetid: c20c6f82-2f75-4116-9be1-c5af10113f71
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh529946(v=EXCHG.150)
ms:contentKeyID: 50484097
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주소록 정책 제거

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-03-25_

이 절차를 사용하여 ABP(주소록 정책)를 제거합니다.

ABP와 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 주소록 정책 절차](address-book-policy-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분 미만입니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md) 항목의 "주소록 정책" 항목

  - 사용자 사서함 또는 일시 삭제된 사서함에 할당된 ABP는 제거할 수 없습니다. 사용자에게 ABP가 할당되어 있는지 확인하려면 다음 셸 명령을 실행합니다.
    
    `Get-Mailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`
    
    일시 삭제된 사서함에 ABP가 할당되어 있는지 확인하려면 다음 명령을 실행합니다.
    
    `Get-Mailbox -SoftDeletedMailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`

  - 사용자의 사서함에서 ABP를 제거하려면 사서함의 속성의 **사서함 기능** 페이지 또는 **Set-Mailbox** cmdlet을 사용합니다.

  - ABP를 제거하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 ABP 제거

이 예에서는 ABP ABP\_TailspinToys를 제거합니다.

    Remove-AddressBookPolicy -Identity "ABP_TailspinToys"

구문과 매개 변수에 대한 자세한 내용은 [Remove-AddressBookPolicy](https://technet.microsoft.com/ko-kr/library/hh529929\(v=exchg.150\))를 참조하십시오.

