---
title: 'Exchange 관리 센터에 대 한 액세스를 해제: Exchange 2013 Help'
TOCTitle: Exchange 관리 센터에 대 한 액세스를 해제
ms:assetid: 49f4fa77-1722-4703-81c9-8724ae0334fb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ218639(v=EXCHG.150)
ms:contentKeyID: 50483035
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 관리 센터에 대 한 액세스를 해제

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-05-20_

보안을 위해 일부 조직에서는 인터넷 사용자에 대해 EAC(Exchange 관리 센터)에 대한 액세스를 제한할 수도 있습니다. 이 절차에서는 EAC에 대한 액세스를 해제하는 방법을 보여줍니다. 이 절차를 통해 사용자가 Outlook Web App의 옵션에 액세스하지 못하게 할 수는 없습니다.


> [!NOTE]
> 이 절차는 이 단계가 적용된 CAS 서버에 대해 EAC 관리자 액세스를 전체적으로 해제합니다. 내부 사용자에 대해 EAC 관리자를 사용하도록 설정하려면 별도의 CAS 서버를 설치하고 다음 명령을 사용하여 내부 요청만 처리하도록 서버를 구성해야 합니다.<BR><CODE>Set-ECPVirtualDirectory -Identity "InternalCAS\ecp (default web site)" -AdminEnabled $True</CODE>




> [!WARNING]
> 이 절차는 온-프레미스 Exchange Server 2013 배포에만 적용됩니다.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "Exchange 관리 센터 연결" 항목

  - 이 절차를 수행하는 데 EAC를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 EAC에 대한 인터넷 액세스 해제

이 예에서는 CAS01 서버의 EAC에 대한 액세스를 해제합니다.

    Set-ECPVirtualDirectory -Identity "CAS01\ecp (default web site)" -AdminEnabled $false

구문과 매개 변수에 대한 자세한 내용은 [Set-EcpVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dd297991\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

EAC에 대한 액세스가 해제되었는지 확인하려면 다음을 수행합니다.

1.  인터넷 브라우저에 조직에서 Outlook Web App 액세스용으로 사용하는 내부 또는 외부 URL을 입력합니다. 이때 **/owa** 식별자를 **/ecp**로 바꿉니다. 예를 들어, Outlook Web App 액세스용 외부 URL이 https://primary.tailspintoys.com/owa이면 https://primary.tailspintoys.com/ecp를 사용합니다.

2.  액세스가 해제되었으면 **404 - 웹 사이트를 찾을 수 없음** 오류가 표시됩니다.

