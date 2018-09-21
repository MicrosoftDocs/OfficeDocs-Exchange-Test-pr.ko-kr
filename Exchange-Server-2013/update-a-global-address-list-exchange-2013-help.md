---
title: '전체 주소 목록 업데이트: Exchange 2013 Help'
TOCTitle: 전체 주소 목록 업데이트
ms:assetid: 236e8530-62dd-4c43-8a5d-8465623252e6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb266966(v=EXCHG.150)
ms:contentKeyID: 50482730
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전체 주소 목록 업데이트

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-12-16_

셸을 사용하여 GAL(전체 주소 목록)을 업데이트할 수 있습니다. GAL은 조직에서 구현된 Microsoft Exchange 내의 모든 그룹, 사용자 및 연락처에 대한 항목이 포함된 디렉터리입니다.

주소 목록과 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 목록 절차](address-list-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "주소 목록" 항목

  - Exchange Online에서는 기본적으로 주소 목록 역할이 어떤 역할 그룹에도 할당되지 않습니다. 주소 목록 역할이 필요한 cmdlet을 사용하려면 역할 그룹에 이 역할을 추가해야 합니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 항목의 "역할 그룹에 역할 추가" 섹션을 참조하세요.

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 GAL 업데이트

다음은 Fourth Coffee 회사의 GAL을 업데이트하는 예입니다.


> [!NOTE]
> 이 명령을 실행하면 업데이트 프로세스만 시작됩니다. GAL을 업데이트하는 데는 몇 시간 정도 걸릴 수 있습니다.



```powershell
Update-GlobalAddressList -Identity "Fourth Coffee"
```

구문과 매개 변수에 대한 자세한 내용은 [Update-GlobalAddressList](https://technet.microsoft.com/ko-kr/library/aa998806\(v=exchg.150\))를 참조하십시오.

