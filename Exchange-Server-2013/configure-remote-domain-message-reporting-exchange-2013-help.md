---
title: '원격 도메인 메시지 보고 구성: Exchange 2013 Help'
TOCTitle: 원격 도메인 메시지 보고 구성
ms:assetid: 73dc686a-e7a3-44c7-b82f-f52ff9273199
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ649325(v=EXCHG.150)
ms:contentKeyID: 50483426
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원격 도메인 메시지 보고 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

원격 도메인을 통해 전자 메일을 주고받는 방법을 구성하려면 Exchange 관리 셸을 사용할 수 있습니다. 아래에서는 Exchange 관리 셸을 사용하여 Exchange에서 배달 및 배달 못 함 보고서가 처리되는 방식을 구성하는 방법을 보여 줍니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "원격 도메인" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 메시지 보고 구성

**Set-RemoteDomain** cmdlet을 사용하여 원격 도메인의 속성을 구성할 수 있습니다.

이 예에서는 Contoso라는 원격 도메인에 대한 배달 보고서를 사용하지 않도록 설정합니다. 기본적으로 이 설정은 사용하도록 설정되어 있습니다.

    Set-RemoteDomain Contoso -DeliveryReportEnabled $false

이 예에서는 원격 도메인에 대한 배달 못 함 보고서를 사용하지 않도록 설정합니다. 기본적으로 이 설정은 사용하도록 설정되어 있습니다.

    Set-RemoteDomain Contoso -NDREnabled $false

