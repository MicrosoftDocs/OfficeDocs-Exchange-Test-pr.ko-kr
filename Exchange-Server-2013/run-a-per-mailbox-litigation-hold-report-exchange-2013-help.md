---
title: '사서함 단위 소송 보존 보고서 실행: Exchange 2013 Help'
TOCTitle: 사서함 단위 소송 보존 보고서 실행
ms:assetid: 98c46226-2f48-42c6-a741-34bb5944f519
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150542(v=EXCHG.150)
ms:contentKeyID: 50482308
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 단위 소송 보존 보고서 실행

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-13_

조직이 법적 소송에 관련되어 있는 경우 증거로 사용될 가능성이 있는 전자 메일 메시지와 같은 관련 데이터를 보존해야 할 수 있습니다. 이와 같은 경우 소송 보존을 사용하면 특정 인물과 주고받은 모든 전자 메일을 보관하거나 특정 기간 동안 조직 내에서 주고받은 모든 전자 메일을 보관할 수 있습니다. 사서함이 소송 보존 중인 경우 어떤 상황이 발생하는지와 소송 보존을 사용하거나 사용하지 않도록 설정하는 방법에 대한 자세한 내용은 [사용자 사서함 관리](manage-user-mailboxes-exchange-2013-help.md)의 "사서함 기능" 섹션을 참조하십시오.

소송 보존 보고서를 사용하면 지정된 기간 동안 사서함에 대해 수행된 다음 유형의 변경을 추적할 수 있습니다.

  - 소송 보존이 사용할 수 있도록 설정되었습니다.

  - 소송 보존이 사용할 수 없도록 설정되었습니다.

보고서에는 이러한 변경 유형마다 변경한 사용자와 변경한 시간 및 날짜가 포함됩니다.

## 시작하기 전에 알아야 할 내용

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 항목의 "관리자 감사 로깅만 보기" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## EAC를 사용하여 소송 보존 보고서 실행

1.  EAC에서 **규정 준수 관리** \> **감사**로 이동합니다.

2.  **사서함 단위 소송 보존 보고서 실행**을 클릭합니다.
    
    지난 2주 이내에 사서함에 대해 수행된 소송 보존 변경 사항에 대한 보고서가 실행됩니다.

3.  특정 사서함에 대한 변경 내용을 보려면 검색 결과 창에서 사서함을 선택합니다. 세부 정보 창에서 검색 결과를 확인합니다.


> [!TIP]
> 검색 결과를 좁히려면 시작 날짜, 종료 날짜 또는 둘 다를 선택하고 검색할 특정 사서함을 선택합니다. <STRONG>검색</STRONG>을 클릭하여 보고서를 다시 실행합니다.



## 작동 여부는 어떻게 확인합니까?

소송 보존 보고서가 성공적으로 실행되면 날짜 범위 내에 소송 보존이 변경된 사서함이 검색 결과 창에 표시됩니다. 결과가 없으면 날짜 범위 내에 수행된 소송 보존 변경 내용이 없거나 최신 변경 내용이 아직 적용되지 않은 것입니다.


> [!NOTE]
> 사서함을 소송 보존 상태로 설정하면 보존이 적용되는 데 최대 60분까지 걸릴 수 있습니다.


