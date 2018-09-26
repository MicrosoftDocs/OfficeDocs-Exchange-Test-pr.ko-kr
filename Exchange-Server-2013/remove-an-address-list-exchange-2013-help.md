---
title: '주소 목록을 제거합니다: Exchange 2013 Help'
TOCTitle: 주소 목록을 제거합니다
ms:assetid: 39a313f3-41d4-4c8f-af67-df2316f3687f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997294(v=EXCHG.150)
ms:contentKeyID: 50482891
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주소 목록을 제거합니다

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-14_

이 항목에서는 주소 목록을 제거하는 방법을 설명합니다. 기본 GAL(전체 주소 목록)은 제거할 수 없습니다.

주소 목록과 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 목록 절차](address-list-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md) 항목의 "주소 목록" 항목

  - 하위 주소 목록을 포함하는 상위 주소 목록은 제거할 수 없습니다. 그러나 키보드에서 Ctrl 키를 누른 채로 상위 및 하위 주소 목록을 선택하여 한꺼번에 제거할 수 있습니다. 하위 주소 목록은 그대로 두고 상위 주소 목록만 제거하려고 할 경우 오류 메시지가 표시됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 주소 목록 제거

1.  **조직** \> **주소록**으로 이동합니다.

2.  목록 보기에서 제거하려는 주소 목록을 선택하고 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭합니다.

3.  경고에서 **예**를 클릭하여 주소 목록을 제거합니다.

## 셸을 사용하여 주소 목록 제거

다음은 하위 주소록을 포함하지 않는 주소 목록 Sales Department를 제거하는 예입니다.

```powershell
Remove-AddressList -Identity "Sales Department"
```

해당 주소 목록을 제거하려면 **Y**를 입력한 다음 Enter 키를 누릅니다.

구문과 매개 변수에 대한 자세한 내용은 [Remove-AddressList](https://technet.microsoft.com/ko-kr/library/bb124342\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 하위 주소 목록을 포함하는 주소 목록 제거

다음은 상위 주소 목록 Departments와 모든 하위 주소 목록을 제거하는 예입니다.

```powershell
Remove-AddressList -Identity Departments -Recursive
```

**Y**를 입력하여 상위 주소 목록과 해당 하위 주소 목록을 제거할 것인지를 확인한 후 Enter 키를 누릅니다.

구문과 매개 변수에 대한 자세한 내용은 [Remove-AddressList](https://technet.microsoft.com/ko-kr/library/bb124342\(v=exchg.150\))를 참조하십시오.

