---
title: '큐 뷰어 옵션 설정: Exchange 2013 Help'
TOCTitle: 큐 뷰어 옵션 설정
ms:assetid: 03a9134c-0714-4c13-b286-92bccc7ec05e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa995934(v=EXCHG.150)
ms:contentKeyID: 50482404
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 큐 뷰어 옵션 설정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

큐 뷰어의 옵션을 설정하여 페이지에 표시되는 항목 수와 자동 새로 고침 간격을 조정할 수 있습니다. 자동 새로 고침 간격은 큐 뷰어에서 결과가 업데이트되는 빈도를 결정합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "큐" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, 또는 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a></td>
</tr>
</tbody>
</table>


## Exchange 도구 상자를 사용하여 큐 뷰어 옵션 설정

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange Server 2013** \> **Exchange 도구 상자**를 클릭합니다.

2.  **메일 흐름 도구** 섹션에서 **큐 뷰어**를 두 번 클릭합니다.

3.  큐 뷰어에서 **보기** \> **옵션**을 클릭하고 **큐 뷰어 옵션** 대화 상자에서 다음 설정을 구성합니다.
    
    1.  **새로 고침 간격(초)** 필드에 큐 뷰어의 화면 표시가 업데이트되는 빈도를 입력합니다.
        

        > [!NOTE]
        > 기본 자동 새로 고침 간격은 30초이며 더 짧게 설정할 수 없습니다. <STRONG>큐 뷰어 옵션</STRONG> 페이지에서 <STRONG>화면 자동 새로 고침</STRONG> 확인란의 선택을 해제하여 자동 새로 고침 기능을 사용하지 않도록 설정하면 <STRONG>새로 고침</STRONG>을 클릭하여 큐 뷰어에 표시된 결과를 수동으로 업데이트해야 합니다.

    
    2.  **각 페이지에 표시할 항목 수** 필드에 큐 뷰어에 표시할 최대 항목 수를 입력합니다. 이 개수는 1에서 10,000 사이여야 합니다. 제한보다 더 많은 항목이 있는 경우 최대 항목 수의 그룹으로 항목이 표시됩니다. 예를 들어 다음 그림은 각 페이지에 10개의 항목을 표시하도록 구성된 큐 뷰어에 14개의 메시지가 있는 큐를 보여 줍니다. 페이지에 있는 개체 수는 오른쪽 상단에 표시됩니다. 페이지 맨 아래에서 큐에 있는 항목의 총 수를 볼 수 있습니다. 탐색 컨트롤을 사용하여 큐에 있는 추가 항목을 볼 수 있습니다.

4.  작업을 마치면 **확인**을 클릭합니다.
    
    **큐 뷰어**
    
    ![항목 수가 항목 제한을 초과한 큐 뷰어](images/Aa995934.e82196e6-002a-4e9e-823d-b244b0bd25e2(EXCHG.150).gif "항목 수가 항목 제한을 초과한 큐 뷰어")  

## 작동 여부는 어떻게 확인합니까?

큐 뷰어에서 새로 고침 간격 및 페이지당 항목 수 설정을 사용하면 이 절차가 제대로 작동한 것입니다.

