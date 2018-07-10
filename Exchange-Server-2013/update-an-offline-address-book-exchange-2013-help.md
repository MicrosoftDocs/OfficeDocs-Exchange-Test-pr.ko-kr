---
title: '오프 라인 주소록 업데이트: Exchange 2013 Help'
TOCTitle: 오프 라인 주소록 업데이트
ms:assetid: 448a207e-41b4-4cef-9fe9-a68b81e2ec4e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997684(v=EXCHG.150)
ms:contentKeyID: 50482994
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 오프 라인 주소록 업데이트

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-11-15_

OAB를 만들거나 OAB 설정을 수정한 후에도 OAB 생성(OABGen) 프로세스가 완료될 때까지는 사용자가 해당 변경 내용을 사용할 수 없습니다.

OAB와 관련된 추가 관리 작업에 대한 자세한 내용은 [오프 라인 주소록 절차](offline-address-book-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "오프라인 주소록" 항목

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 OAB 업데이트

이 예에서는 My OAB라는 OAB를 업데이트합니다.

    Update-OfflineAddressBook -Identity "My OAB"

구문과 매개 변수에 대한 자세한 내용은 [Update-OfflineAddressBook](https://technet.microsoft.com/ko-kr/library/aa995979\(v=exchg.150\))을 참조하십시오.

