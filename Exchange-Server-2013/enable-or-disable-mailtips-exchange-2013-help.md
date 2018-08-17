---
title: '사용 또는 사용 안함 메일 설명: Exchange 2013 Help'
TOCTitle: 사용 또는 사용 안함 메일 설명
ms:assetid: 11ad3848-f303-4ad5-a21d-9b0883db4bda
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ649321(v=EXCHG.150)
ms:contentKeyID: 50482507
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 또는 사용 안함 메일 설명

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

Exchange 관리 셸을 사용하여 조직에서 메일 설명을 사용하는 방법을 정의하는 다양한 설정을 구성할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "메일 설명" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 메일 설명을 사용하거나 사용하지 않도록 설정

**Set-OrganizationConfig** cmdlet을 사용하여 조직에서 메일 설명을 사용하거나 사용하지 않도록 설정합니다. 새 Exchange 조직을 설치하면 기본적으로 메일 설명이 사용되도록 설정됩니다. 이 예에서는 조직에서 메일 설명을 사용하도록 설정하는 방법을 보여 줍니다.

    Set-OrganizationConfig -MailTipsAllTipsEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\)) 항목을 참조하십시오.

