---
title: 'Active Directory 에 존재 하는 중복 된 Microsoft Exchange System Objects 컨테이너: Exchange 2013 Help'
TOCTitle: Active Directory 에 존재 하는 중복 된 Microsoft Exchange System Objects 컨테이너
ms:assetid: cd0f45ab-89de-4653-b50d-c1157c2329d5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.adiniterrorrule(v=EXCHG.150)
ms:contentKeyID: 50484180
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory [AdInitErrorRule]에 존재 하는 중복 된 Microsoft Exchange System Objects 컨테이너

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2013-02-18_

Active Directory 도메인 이름 지정 컨텍스트에 중복 Microsoft Exchange System Objects 컨테이너가 있어서 Microsoft Exchange Server 2013 설치를 계속할 수 없습니다. 중복 Microsoft Exchange System Objects 컨테이너가 발견되는 경우 설치를 계속하려면 중복 컨테이너를 삭제해야 합니다. 중복 Microsoft Exchange System Objects 컨테이너가 있으면 **DomainPrep**을 다시 실행하여 문제를 해결할 수 없습니다. 중복 Microsoft Exchange System Objects 컨테이너를 식별하여 삭제해야 합니다.

이 문제를 해결하려면 다음을 수행합니다.

1.  관리 자격 증명을 사용하여 도메인 컨트롤러에 로그온합니다.

2.  **관리 도구**에서 **Active Directory 사용자 및 컴퓨터**를 클릭합니다.

3.  **Active Directory 사용자 및 컴퓨터** 관리 콘솔 창의 도구 모음 메뉴에서 **보기**를 클릭하고 **고급 기능**을 선택합니다.

4.  중복 Microsoft Exchange System Objects 컨테이너를 찾습니다.

5.  중복 Microsoft Exchange System Objects 컨테이너에 유효한 Active Directory 개체가 들어 있지 않은지 확인합니다.

6.  중복 Microsoft Exchange System Objects 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.

7.  Active Directory 대화 상자에서 **예**를 클릭하여 삭제를 확인합니다.


> [!NOTE]
> 변경 내용을 즉시 복제하려면 도메인 컨트롤러 사이에서 복제를 수동으로 시작해야 합니다.



문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

