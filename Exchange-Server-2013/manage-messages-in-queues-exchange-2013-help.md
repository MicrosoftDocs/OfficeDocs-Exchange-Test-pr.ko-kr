---
title: '큐에서 메시지 관리: Exchange 2013 Help'
TOCTitle: 큐에서 메시지 관리
ms:assetid: 83358884-6036-4e91-87a8-35200541874d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123535(v=EXCHG.150)
ms:contentKeyID: 51407718
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 큐에서 메시지 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-05-07_

Microsoft Exchange Server 2013의 Exchange 관리 셸이나 Exchange 도구 상자의 큐 뷰어를 사용하여 큐의 메시지를 관리할 수 있습니다. Exchange 관리 셸에서 메시지 관리 cmdlet을 사용하는 방법에 대한 자세한 내용은 [Exchange 관리 셸을 사용 하 여 큐를 관리](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "큐" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 큐에서 메시지 제거

받는 사람이 여러 명인 메시지의 경우 둘 이상의 큐에 위치할 수 있습니다. 둘 이상의 큐에서 메시지를 한 번에 제거하려면 필터를 사용해야 합니다. 큐에서 메시지를 제거할 때 배달 못 함 보고서(NDR)를 보낼지 여부를 선택할 수 있습니다. 전송 큐의 메시지는 제거할 수 없습니다.

## Exchange 도구 상자의 큐 뷰어를 사용하여 메시지 제거

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange 2013** \> **Exchange 도구 상자**를 클릭합니다.

2.  **메일 흐름 도구** 섹션에서 **큐 뷰어**를 두 번 클릭하여 도구를 새 창에서 엽니다.

3.  큐 뷰어에서 **메시지** 탭을 클릭합니다. 연결된 서버에 있는 모든 메시지의 목록이 표시됩니다. 큐를 하나만 표시하도록 조정하려면 **큐** 탭을 클릭하고 해당 큐 이름을 두 번 클릭한 다음 표시되는 *Server\\Queue* 탭을 클릭합니다.

4.  목록에서 메시지를 하나 이상 선택하고 마우스 오른쪽 단추로 클릭한 다음 **메시지 제거(NDR 있음)** 또는 **메시지 제거(NDR 보내지 않음)**를 선택합니다. 선택한 작업을 확인한 후 **계속하시겠습니까?**라고 묻는 대화 상자가 나타납니다. **예**를 클릭합니다.

5.  특정 큐에서 메시지를 모두 제거하려면 **큐** 탭을 클릭합니다. 큐 하나를 선택하여 마우스 오른쪽 단추로 클릭한 다음 **메시지 제거(NDR 있음)** 또는 **메시지 제거(NDR 보내지 않음)**를 선택합니다. 선택한 작업을 확인한 후 **계속하시겠습니까?**라고 묻는 대화 상자가 나타납니다. **예**를 클릭합니다.
    

    > [!NOTE]
    > 필터링된 목록에서 작업할 경우 필터의 항목이 모두 표시되지 않을 수도 있습니다. 이 경우 <STRONG>이 작업은 이 페이지의 모든 항목에 영향을 줍니다. 이 필터의 모든 항목을 포함하도록 이 작업의 범위를 확장하려면 다음 확인란을 선택한 다음 [확인]을 클릭하십시오.</STRONG>라는 메시지가 표시됩니다.



## 셸을 사용하여 메시지 제거

큐에서 메시지를 제거하려면 다음 구문을 사용합니다.

    Remove-Message <-Identity MessageIdentity | -Filter {MessageFilter}> -WithNDR <$true | $false>

이 예에서는 NDR을 보내지 않고 제목이 "Win Big"인 메시지를 큐에서 제거합니다.

    Remove-Message -Filter {Subject -eq "Win Big"} -WithNDR $false

이 예에서는 Mailbox01이라는 서버의 연결할 수 없는 큐에서 메시지 ID가 3인 메시지를 제거하고 NDR을 보냅니다.

    Remove-Message -Identity Mailbox01\Unreachable\3 -WithNDR $true

## 작동 여부는 어떻게 확인합니까?

큐에서 메시지가 제거되었는지 확인하려면 다음 중 하나를 수행합니다.

  - 큐 뷰어에서 큐를 선택하거나 필터를 만들어 메시지가 더 이상 존재하지 않는지 확인합니다.

  - *Queue* 또는 *Filter* 매개 변수와 함께 **Get-Message** cmdlet을 사용하여 메시지가 더 이상 존재하지 않는지 확인할 수 있습니다. 자세한 내용은 [Get-Message](https://technet.microsoft.com/ko-kr/library/bb124738\(v=exchg.150\))를 참조하십시오.

## 큐의 메시지 다시 시작

현재 Suspended 상태에 있는 메시지를 다시 시작할 수 있습니다. 메시지를 다시 시작하면 메시지를 배달할 수 있습니다. 포이즌 메시지 큐에 있는 메시지를 다시 시작하면 메시지는 분류기로 전송되어 처리됩니다. 받는 사람이 여러 명인 메시지는 여러 큐에 위치할 수 있습니다. 여러 큐에 있는 메시지를 한 번의 작업으로 다시 시작하려면 필터를 사용해야 합니다.

## Exchange 도구 상자의 큐 뷰어를 사용하여 메시지 다시 시작

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange 2013** \> **Exchange 도구 상자**를 클릭합니다.

2.  **메일 흐름 도구** 섹션에서 **큐 뷰어**를 두 번 클릭하여 도구를 새 창에서 엽니다.

3.  큐 뷰어에서 **메시지** 탭을 클릭합니다. 연결된 서버에 있는 모든 메시지의 목록이 표시됩니다. 단일 큐에 대한 작업을 조정하려면 **큐** 탭을 클릭하고 큐 이름을 두 번 클릭한 다음 나타나는 *Server\\Queue* 탭을 클릭합니다.

4.  **필터 만들기**를 클릭하고 필터 식을 다음과 같이 입력합니다.
    
    1.  메시지 속성 드롭다운 목록에서 **상태**를 선택합니다.
    
    2.  비교 연산자 드롭다운 목록에서 **같음**을 선택합니다.
    
    3.  값 드롭다운 목록에서 **Suspended**를 선택합니다.

5.  **필터 적용**을 클릭합니다. Suspended 상태의 모든 메시지가 표시됩니다.

6.  목록에서 하나 이상의 메시지를 클릭하고 마우스 오른쪽 단추로 누른 다음 **다시 시작**을 선택합니다.

## 셸을 사용하여 메시지 다시 시작

메시지를 다시 시작하려면 다음 구문을 사용합니다.

    Resume-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

이 예에서는 Contoso.com 도메인에 있는 보낸 사람이 전송한 모든 메시지를 다시 시작합니다.

    Resume-Message -Filter {FromAddress -eq "*contoso.com"}

이 예에서는 서버 Hub01의 연결할 수 없는 큐에서 메시지 ID가 3인 메시지를 다시 시작합니다.

    Resume-Message -Identity Hub01\Unreachable\3

포이즌 메시지 큐에서 메시지를 다시 전송하려면 다음 단계를 수행합니다.

## 작동 여부는 어떻게 확인합니까?

큐에서 메시지가 다시 시작되었는지 확인하려면 다음 중 하나를 수행합니다.

  - 큐 뷰어에서 큐를 선택하거나 필터를 만들어 메시지가 더 이상 Suspended 상태가 아닌지 확인합니다.

  - *Queue* 또는 *Filter* 매개 변수와 함께 **Get-Message** cmdlet을 사용하여 메시지가 더 이상 Suspended 상태가 아닌지 확인할 수 있습니다. 자세한 내용은 [Get-Message](https://technet.microsoft.com/ko-kr/library/bb124738\(v=exchg.150\))를 참조하십시오.

서버의 큐에서 메시지를 찾을 수 없는 경우 이는 메시지가 다음 홉으로 배달되었음을 나타낼 수 있습니다.

## 큐의 메시지 일시 중단

메시지를 일시 중단하면 메시지를 배달할 수 없습니다. 큐에 표시되지만 이미 배달 중인 메시지는 일시 중단되지 않습니다. 배달은 계속되고 메시지 상태는 **PendingSuspend**가 됩니다. 그러나 배달이 실패하면 메시지는 큐를 다시 입력한 다음 일시 중단됩니다. 전송 큐나 포이즌 메시지 큐에 있는 메시지는 일시 중단할 수 없습니다.

받는 사람이 여러 명인 메시지는 여러 큐에 위치할 수 있습니다. 단일 작업에서 여러 큐에 있는 메시지를 일시 중단하려면 필터를 사용해야 합니다.

## Exchange 도구 상자의 큐 뷰어를 사용하여 메시지 일시 중단

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange 2013** \> **Exchange 도구 상자**를 클릭합니다.

2.  **메일 흐름 도구** 섹션에서 **큐 뷰어**를 두 번 클릭하여 도구를 새 창에서 엽니다.

3.  큐 뷰어에서 **메시지** 탭을 클릭합니다. 연결된 서버에 있는 모든 메시지의 목록이 표시됩니다. 보기에서 큐를 하나만 표시하도록 제한하려면 **큐** 탭을 클릭하고 큐 이름을 두 번 클릭한 다음 표시되는 *Server\\Queue* 탭을 클릭합니다.

4.  하나 이상의 메시지를 선택하고 마우스 오른쪽 단추로 클릭한 다음 **Suspended**를 선택합니다.

## 셸을 사용하여 메시지 일시 중단

메시지를 일시 중단하려면 다음 구문을 사용합니다.

    Suspend-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

이 예에서는 큐에서 보낸 사람 도메인이 contoso.com인 모든 메시지를 일시 중단합니다.

    Suspend-Message -Filter {FromAddress -eq "*contoso.com"}

이 예에서는 Mailbox01이라는 서버의 연결할 수 없는 큐에서 메시지 ID가 3인 메시지를 일시 중단합니다.

    Suspend-Message -Identity Mailbox01\Unreachable\3

## 작동 여부는 어떻게 확인합니까?

큐에서 메시지가 일시 중단되었는지 확인하려면 다음 중 하나를 수행합니다.

  - 큐 뷰어에서 큐를 선택하거나 필터를 만들어 메시지가 Suspended 상태인지 확인합니다.

  - *Queue* 또는 *Filter* 매개 변수와 함께 **Get-Message** cmdlet을 사용하여 메시지가 Suspended 상태인지 확인할 수 있습니다. 자세한 내용은 [Get-Message](https://technet.microsoft.com/ko-kr/library/bb124738\(v=exchg.150\))를 참조하십시오.

