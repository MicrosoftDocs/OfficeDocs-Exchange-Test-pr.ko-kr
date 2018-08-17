---
title: '주소 목록 이동: Exchange 2013 Help'
TOCTitle: 주소 목록 이동
ms:assetid: c843bbd5-6c0e-41e1-b749-7ae87c1beb25
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124534(v=EXCHG.150)
ms:contentKeyID: 50484132
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주소 목록 이동

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-14_

이 항목에서는 기존 주소 목록을 루트 주소 목록 아래의 새 컨테이너로 이동하는 방법에 대해 설명합니다.

주소 목록과 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 목록 절차](address-list-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "주소 목록" 항목

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 주소 목록 이동

이 예에서는 주소 목록의 GUID를 사용하여 주소 목록을 All Users\\Sales 컨테이너에 있는 Building 4 컨테이너로 이동합니다.

    Move-AddressList -Identity c3fffd8e-026b-41b9-88c4-8c21697ac8ac -Target "\All Users\Sales\Building4"

**Y**를 입력하여 해당 주소 목록 이동을 확인하고 Enter 키를 누릅니다.

구문과 매개 변수에 대한 자세한 내용은 [Move-AddressList](https://technet.microsoft.com/ko-kr/library/bb124520\(v=exchg.150\))를 참조하십시오.

