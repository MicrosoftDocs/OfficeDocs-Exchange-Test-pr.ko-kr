---
title: '사서함 데이터베이스 를 제거할 수 없습니다.: Exchange 2013 Help'
TOCTitle: 사서함 데이터베이스 를 제거할 수 없습니다.
ms:assetid: 5881e4c0-c2e2-48db-84b4-7f9ce3cf46a7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.unwillingtoremovemailboxdatabase(v=EXCHG.150)
ms:contentKeyID: 50483167
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 데이터베이스 [UnwillingToRemoveMailboxDatabase]를 제거할 수 없습니다.

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2012-11-08_

잠재적인 데이터 손실 없이는 로컬 서버에서 사용자 사서함 데이터베이스를 제거할 수 없기 때문에 Microsoft Exchange Server 2013 설치를 계속할 수 없습니다.

Exchange 2013 설치 프로그램은 사서함 서버 역할을 제거하기 전에 서버에서 모든 사서함 데이터베이스가 제거되었는지 확인합니다. 그러나 사용자 사서함이 서버에 남아 있을 수 있습니다.

이 문제를 해결하려면 서버의 모든 사서함을 다른 Exchange 서버로 옮기거나 사서함과 그 안에 담긴 데이터가 더 이상 필요하지 않다면 해당 사서함을 사용하지 않도록 설정하십시오. 그런 다음 Exchange 2013 설치 프로그램을 다시 실행합니다.

  - 데이터베이스의 사서함을 식별하는 방법에 대한 자세한 내용은 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))를 참조하십시오.

  - 사서함을 이동하는 방법에 대한 자세한 내용은 [Exchange 2013 사서함 이동](mailbox-moves-in-exchange-2013-exchange-2013-help.md)을 참조하십시오.

  - 사서함을 사용하지 않도록 설정하는 방법에 대한 자세한 내용은 [Disable-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997210\(v=exchg.150\))를 참조하십시오.

  - 사서함 데이터베이스를 제거하는 방법에 대한 자세한 내용은 [Exchange 2013의 사서함 데이터베이스를 관리 합니다.](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)를 참조하십시오.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

