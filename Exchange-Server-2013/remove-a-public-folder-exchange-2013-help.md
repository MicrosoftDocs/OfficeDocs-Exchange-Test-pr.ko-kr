---
title: '공용 폴더를 제거 합니다.: Exchange 2013 Help'
TOCTitle: 공용 폴더를 제거 합니다.
ms:assetid: 334b831d-e372-4d85-a407-5c8a5d0e78de
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997202(v=EXCHG.150)
ms:contentKeyID: 50482823
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공용 폴더를 제거 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-11-16_

조직에서 더 이상 사용되지 않는 공용 폴더를 제거해야 할 수 있습니다. 어떤 공용 폴더를 제거해야 할지 확인하려면 [공용 폴더 및 공용 폴더 항목에 대 한 통계 보기](view-statistics-for-public-folders-and-public-folder-items-exchange-2013-help.md)를 참조하십시오.

공용 폴더 관리와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [Office 365 및 Exchange Online의 절차에서는 공용 폴더](https://technet.microsoft.com/ko-kr/library/jj966272\(v=exchg.150\))를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md) 항목의 "공용 폴더" 항목

  - 메일 사용 가능 공용 폴더는 삭제할 수 없습니다. 공용 폴더를 삭제하려면 먼저 공용 폴더에 대해 전자 메일을 사용하지 않도록 설정해야 합니다. 자세한 내용은 [메일 사용이 가능한 또는 공용 폴더 메일-사용 안함](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md) 항목을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 공용 폴더 제거

1.  **공용 폴더** \> **공용 폴더**로 이동합니다.

2.  목록 보기에서 삭제 하려는 공용 폴더를 선택 합니다. Note 내용이 있으면 폴더 이름을 클릭 하면 해당 폴더 내에 하위 폴더 표시 됩니다. 이때 제거할 특정 하위 폴더를 선택 하려면 클릭 수 있습니다.
    
    폴더나 하위 폴더를 삭제를 차례로 아무곳 이나 클릭 하 여 폴더의 이름에 밑줄이 제외 하 고 폴더의 행에 다음![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")**삭제** 를 클릭 합니다. 폴더의 이름에 밑줄이 클릭 하면 **삭제** 옵션을 선택 하는 사용할 수 있는 되지 않습니다.
    
    ![제거할 공용 폴더 선택](images/Aa997202.8666290d-3f19-4c70-afe3-45569762718b(EXCHG.150).png "제거할 공용 폴더 선택")  

3.  공용 폴더를 삭제할지 묻는 경고 상자가 표시됩니다. 계속하려면 **예**를 클릭합니다.

## 셸을 사용하여 공용 폴더 삭제

다음은 Help Desk\\Resolved 공용 폴더를 삭제하는 예입니다. 다음 명령은 Resolved 공용 폴더에 하위 폴더가 없다고 가정합니다.

    Remove-PublicFolder -Identity "\Help Desk\Resolved"

다음은 위 명령을 수정하지 않고 테스트하는 예입니다.

    Remove-PublicFolder -Identity "\HelpDesk\Resolved" -WhatIf

이 예에서는 명령이 재귀적으로 실행되므로 Marketing 공용 폴더와 모든 하위 폴더가 제거됩니다.

    Remove-PublicFolder -Identity "\Marketing" -Recurse:$True

구문과 매개 변수에 대한 자세한 내용은 [Remove-PublicFolder](https://technet.microsoft.com/ko-kr/library/bb124894\(v=exchg.150\))를 참조하십시오.

