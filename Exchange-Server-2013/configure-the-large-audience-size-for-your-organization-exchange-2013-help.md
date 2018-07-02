---
title: '조직에 대 한 큰 대상 그룹 크기를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 조직에 대 한 큰 대상 그룹 크기를 구성 합니다.
ms:assetid: 8a37911c-4339-4921-b5d3-0a5a774d4517
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ659068(v=EXCHG.150)
ms:contentKeyID: 50483606
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 조직에 대 한 큰 대상 그룹 크기를 구성 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

Exchange 관리 셸을 사용하여 조직에서 메일 설명을 사용하는 방법을 정의하는 다양한 설정을 구성할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "메일 설명" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 조직에 대해 큰 대상 크기 구성

**Set-OrganizationConfig** cmdlet을 사용하여 조직에 대해 큰 대상 크기를 구성합니다. 보낸 사람이 메시지에 주소를 지정한 받는 사람 수가 구성된 크기보다 많으면 큰 대상 메일 설명이 표시됩니다. 큰 대상 크기는 기본적으로 25로 설정되어 있습니다. 이 예에서는 조직의 큰 대상 크기를 50으로 구성합니다.

    Set-OrganizationConfig -MailTipsLargeAudienceThreshold 50

구문과 매개 변수에 대한 자세한 내용은 [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\))를 참조하십시오.

