---
title: '큐 관리: Exchange 2013 Help'
TOCTitle: 큐 관리
ms:assetid: 37f11378-a884-4aff-ab55-689f40a46321
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997263(v=EXCHG.150)
ms:contentKeyID: 51407682
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 큐 관리

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-01-31_

Microsoft Exchange Server 2013에서는 Exchange 도구 상자 또는 Exchange 관리 셸의 큐 뷰어를 사용하여 큐를 관리할 수 있습니다. Exchange 관리 셸에서 큐 관리 cmdlet을 사용하는 방법에 대한 자세한 내용은 [Exchange 관리 셸을 사용 하 여 큐를 관리](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "큐" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 큐 보기

## Exchange 도구 상자의 큐 뷰어를 사용하여 큐 보기

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange 2013** \> **Exchange 도구 상자**를 클릭합니다.

2.  **메일 흐름 도구** 섹션에서 **큐 뷰어**를 두 번 클릭하여 도구를 새 창에서 엽니다.

3.  큐 뷰어에서 **큐** 탭을 클릭합니다. 연결된 서버의 모든 큐 목록이 표시됩니다.

4.  작업 창의 **목록 내보내기** 링크를 사용하여 큐 목록을 내보낼 수 있습니다. 자세한 내용은 [큐 뷰어에서 목록 내보내기](export-lists-from-queue-viewer-exchange-2013-help.md)을 참조하십시오.

## 셸을 사용하여 큐 보기

큐를 보려면 다음 구문을 사용합니다.

    Get-Queue [-Filter <Filter> -Server <ServerIdentity> -Include <Internal | External | Empty | DeliveryType> -Exclude <Internal | External | Empty | DeliveryType>]

이 예에서는 Exchange 2013 사서함 서버 Mailbox01에서 비어 있지 않은 모든 큐에 대한 기본 정보를 표시합니다.

    Get-Queue -Server Mailbox01 -Exclude Empty

이 예에서는 명령이 실행되는 사서함 서버에서 포함된 메시지 수가 100개를 초과하는 모든 큐에 대한 자세한 정보를 표시합니다.

    Get-Queue -Filter {MessageCount -gt 100} | Format-List

## 셸을 사용하여 여러 Exchange 서버에 대한 큐 요약 정보 보기

**Get-QueueDigest** cmdlet은 DAG, Active Directory 사이트, 서버 목록, 전체 Active Directory 포리스트 등의 특정 범위 내에 있는 모든 서버의 큐 상태에 대한 간략한 집계 보기를 제공합니다. 경계 네트워크에서 구독된 Edge 전송 서버의 큐는 결과에 포함되지 않습니다. 또한 **Get-QueueDigest**는 Edge 전송 서버에서 제공되기는 하지만 결과는 Edge 전송 서버의 큐로 제한됩니다.


> [!NOTE]
> 기본적으로 <STRONG>Get-QueueDigest</STRONG> cmdlet은 메시지가 10개 이상 포함된 배달 큐를 표시하고 1~2분 후에 결과를 반환합니다. 이러한 기본값을 변경하는 방법에 대한 지침은 <A href="configure-get-queuedigest-exchange-2013-help.md">Get-QueueDigest 구성</A>을 참조하세요.



여러 Exchange 서버의 큐에 대한 요약 정보를 보려면 다음 명령을 실행합니다.

    Get-QueueDigest <-Server <ServerIdentity1,ServerIdentity2,..> | -Dag <DagIdentity1,DagIdentity2...> | -Site <ADSiteIdentity1,ADSiteIdentity2...> | -Forest> [-Filter <Filter>]

이 예에서는 FirstSite라는 Active Directory 사이트의 모든 Exchange 2013 사서함 서버에서 메시지 수가 100개를 초과하는 큐에 대한 요약 정보를 표시합니다.

    Get-QueueDigest -Site FirstSite -Filter {MessageCount -gt 100}

이 예에서는 DAG01이라는 DAG(데이터베이스 사용 가능 그룹)의 모든 Exchange 2013 사서함 서버에서 큐 상태 값이 **Retry**인 큐에 대한 요약 정보를 표시합니다.

    Get-QueueDigest -Dag DAG01 -Filter {Status -eq "Retry"}

## 큐 다시 시작

큐를 다시 시작하면 Suspended 상태의 큐에서 나가는 작업이 다시 시작됩니다. 이 작업을 적용하려면 큐 상태가 Suspended여야 합니다. 큐를 다시 시작하더라도 큐의 메시지 상태는 변경되지 않습니다. Suspended 상태의 메시지는 일시 중단된 상태로 유지되고 큐에서 나가지 않습니다.

## Exchange 도구 상자의 큐 뷰어를 사용하여 큐 다시 시작

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange 2013** \> **Exchange 도구 상자**를 클릭합니다.

2.  **메일 흐름 도구** 섹션에서 **큐 뷰어**를 두 번 클릭하여 도구를 새 창에서 엽니다.

3.  큐 뷰어에서 **큐** 탭을 클릭합니다. 연결된 서버의 모든 큐 목록이 표시됩니다.

4.  **필터 만들기**를 클릭하고 필터 식을 다음과 같이 입력합니다.
    
    1.  큐 속성 드롭다운 목록에서 **상태**를 선택합니다.
    
    2.  비교 연산자 드롭다운 목록에서 **같음**을 선택합니다.
    
    3.  값 드롭다운 목록에서 **Suspended**를 선택합니다.

5.  **필터 적용**을 클릭합니다. 현재 일시 중단된 서버의 큐가 모두 표시됩니다.

6.  목록에서 큐를 한 개 이상 선택하고 마우스 오른쪽 단추를 클릭한 다음 **다시 시작**을 선택합니다.

## 셸을 사용하여 큐 다시 시작

큐를 다시 시작하려면 다음 구문을 사용합니다.

    Resume-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

이 예에서는 로컬 서버에서 상태가 Suspended인 모든 큐를 다시 시작합니다.

    Resume-Queue -Filter {Status -eq "Suspended"}

이 예에서는 Mailbox01 서버에서 contoso.com이라는 일시 중단된 배달 큐를 다시 시작합니다.

    Resume-Queue -Identity Mailbox01\contoso.com

## 작동 여부는 어떻게 확인합니까?

큐가 다시 시작되었는지 확인하려면 다음을 수행합니다.

1.  큐 뷰어 또는 **Get-Queue** cmdlet을 사용하여 다시 시작하려고 한 큐를 찾습니다.

2.  큐 **Status** 속성에 `Suspended` 값이 없는지 확인합니다.

## 큐 다시 시도

전송 서버가 다음 홉에 연결할 수 없으면 배달 큐가 다시 시도 상태가 됩니다. 큐 뷰어나 셸을 사용하여 배달 큐를 다시 시도하면 즉시 연결 시도가 강제 적용되고 예약된 다음 다시 시도 시간이 재정의됩니다. 연결이 실패하면 다시 시도 간격 타이머가 재설정됩니다. 이 기능을 사용하려면 배달 큐가 다시 시도 상태여야 합니다.

## Exchange 도구 상자의 큐 뷰어를 사용하여 큐 다시 시도

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange 2013** \> **Exchange 도구 상자**를 클릭합니다.

2.  **메일 흐름 도구** 섹션에서 **큐 뷰어**를 두 번 클릭하여 도구를 새 창에서 엽니다.

3.  큐 뷰어에서 **큐** 탭을 클릭합니다. 연결된 서버의 모든 큐 목록이 표시됩니다.

4.  **필터 만들기**를 클릭하고 필터 식을 다음과 같이 입력합니다.
    
    1.  큐 속성 드롭다운 목록에서 **상태**를 선택합니다.
    
    2.  비교 연산자 드롭다운 목록에서 **같음**을 선택합니다.
    
    3.  값 드롭다운 목록에서 **다시 시도**를 선택합니다.

5.  **필터 적용**을 클릭합니다. 현재 **다시 시도** 상태인 모든 큐가 표시됩니다.

6.  목록에서 하나 이상의 큐를 선택합니다. 마우스 오른쪽 단추를 클릭한 다음 **큐 다시 시도**를 선택합니다. 연결 시도가 성공하면 큐 상태가 **활성**으로 변경됩니다. 연결할 수 없는 경우 큐는 **다시 시도** 상태로 유지되며 다음 다시 시도 시간이 업데이트됩니다.

## 셸을 사용하여 큐 다시 시도

큐를 다시 시도하려면 다음 구문을 사용합니다.

    Retry-Queue <-Identity QueueIdentity | -Filter QueueFilter [-Server ServerIdentity]>

이 예에서는 로컬 서버에서 상태가 다시 시도인 모든 큐를 다시 시도합니다.

    Retry-Queue -Filter {status -eq "retry"}

이 예에서는 Mailbox01 서버에서 `Retry` 상태인 contoso.com이라는 큐를 다시 시도합니다.

    Retry-Queue -Identity Mailbox01\contoso.com

## 작동 여부는 어떻게 확인합니까?

큐가 다시 시도되었는지 확인하려면 다음을 수행합니다.

1.  큐 뷰어 또는 **Get-Queue** cmdlet을 사용하여 다시 시도하려고 한 큐를 찾습니다.

2.  큐의 **LastRetryTime** 속성이 큐를 다시 시도한 시간과 일치하는지 확인합니다.

## 큐의 메시지 다시 전송

큐를 다시 전송하는 것은 큐를 다시 시도하는 것과 비슷합니다. 단, 다시 전송 시에는 분류기가 다시 처리할 수 있도록 메시지를 전송 큐로 다시 보냅니다. 다음 상태의 메시지를 다시 전송할 수 있습니다.

  - 다시 시도 상태의 배달 큐. 큐의 메시지가 Suspended 상태여서는 안 됩니다.

  - Suspended 상태가 아닌 연결할 수 없는 큐의 메시지

  - 포이즌 메시지 큐에 있는 메시지

## 셸을 사용하여 메시지 다시 전송

메시지를 다시 전송하려면 다음 구문을 사용합니다.

    Retry-Queue <-Identity QueueIdentity | -Filter {Status -eq "Retry"} -Server ServerIdentity> -Resubmit $true

이 예에서는 Mailbox01 서버에서 상태가 다시 시도인 모든 배달 큐에 있는 모든 메시지를 다시 전송합니다.

    Retry-Queue -Filter {Status -eq "Retry"} -Server Mailbox01 -Resubmit $true

이 예에서는 Mailbox01 서버의 연결할 수 없는 큐에 있는 모든 메시지를 다시 전송합니다.

    Retry-Queue -Identity Mailbox01\Unreachable -Resubmit $true

## 포이즌 메시지 큐의 메시지 다시 전송

메시지를 다시 시작하여 포이즌 메시지 큐의 메시지를 다시 전송합니다. 큐 뷰어 또는 셸을 사용하여 포이즌 메시지 큐의 메시지를 다시 전송할 수 있습니다. 포이즌 메시지 큐에 메시지가 있을 때만 큐 뷰어에서 포이즌 메시지 큐를 볼 수 있습니다.


> [!NOTE]
> 포이즌 메시지 큐에는 서버 오류가 발생한 후 Exchange 시스템에 유해한 것으로 판명된 메시지가 들어 있습니다. 이 메시지의 콘텐츠 또는 형식이 실제로 유해할 수도 있고 잘못된 메시지를 처리하는 동안 잘못 작성된 에이전트로 인해 Exchange 서버의 작동이 중단되어 생성된 것일 수도 있습니다. 포이즌 메시지 큐에 포함된 메시지의 안전성이 확실치 않으면 해당 메시지를 검사할 수 있도록 파일로 내보내야 합니다. 자세한 내용은 <A href="export-messages-from-queues-exchange-2013-help.md">큐에서 메시지 내보내기</A>를 참조하십시오.



## Exchange 도구 상자의 큐 뷰어를 사용하여 포이즌 메시지 큐의 메시지 다시 전송

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange 2013** \> **Exchange 도구 상자**를 클릭합니다.

2.  **메일 흐름 도구** 섹션에서 **큐 뷰어**를 두 번 클릭하여 도구를 새 창에서 엽니다.

3.  큐 뷰어에서 **큐** 탭을 클릭합니다. 연결된 서버의 모든 큐 목록이 표시됩니다.

4.  포이즌 메시지 큐를 클릭합니다. 작업 창에서 **메시지 보기**를 선택합니다.

5.  목록에서 하나 이상의 메시지를 클릭하고 마우스 오른쪽 단추로 누른 다음 **다시 시작**을 선택합니다.

## 셸을 사용하여 포이즌 메시지 큐의 메시지 다시 전송

포이즌 메시지 큐의 메시지를 다시 전송하려면 다음 단계를 수행합니다.

1.  다음 명령을 실행하여 메시지 ID를 확인합니다.
    
        Get-Message -Queue Poison | Format-Table Identity

2.  이전 단계의 메시지 ID를 사용하여 다음 명령을 실행합니다.
    
        Resume-Message <PoisonMessageIdentity>
    
    이 예에서는 포이즌 메시지 큐에서 메시지 ID 값이 222인 메시지를 다시 시작합니다.
    
        Resume-Message 222

## 작동 여부는 어떻게 확인합니까?

포이즌 메시지 큐의 메시지가 다시 전송되었는지 확인하려면 다음을 수행합니다.

1.  큐 뷰어 또는 **Get-Queue** cmdlet을 사용하여 메시지를 다시 전송하려고 한 포이즌 메시지 큐를 확인합니다.

2.  포이즌 메시지 큐에 더 이상 메시지가 없는지 확인합니다. 빈 포이즌 메시지 큐는 큐 뷰어 또는 **Get-Queue** cmdlet에 표시되지 않습니다. 따라서 다시 전송한 메시지만 포함되어 있었던 포이즌 메시지 큐가 더 이상 표시되지 않으면 메시지가 정상적으로 다시 전송된 것입니다.

## 큐 일시 중단

큐를 일시 중단하면 메시지가 큐에서 나갈 수 없지만 큐의 메시지 상태는 변경되지 않습니다. SMTP 송신을 통해 배달 중인 메시지는 작업을 마치게 됩니다. 큐를 일시 중단하여 메일 흐름을 중지한 다음 큐에 있는 하나 이상의 메시지를 일시 중단할 수 있습니다. 큐를 다시 시작하면 일시 중단된 메시지는 큐에서 나가지 않습니다.

상태가 Active 또는 Retry인 큐를 일시 중단할 수 있습니다. 연결할 수 없는 큐와 전송 큐도 일시 중단할 수 있습니다.

연결할 수 없는 큐를 일시 중단할 경우 큐를 다시 시작해야만 전송 서버에 구성 업데이트가 수신될 때 항목이 분류기로 다시 전송됩니다. 전송 큐를 일시 중단할 경우 큐를 다시 시작해야만 분류기에서 메시지를 선택합니다.

## Exchange 도구 상자의 큐 뷰어를 사용하여 큐 일시 중단

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange 2013** \> **Exchange 도구 상자**를 클릭합니다.

2.  **메일 흐름 도구** 섹션에서 **큐 뷰어**를 두 번 클릭하여 도구를 새 창에서 엽니다.

3.  큐 뷰어에서 **큐** 탭을 클릭합니다. 연결된 서버의 모든 큐 목록이 표시됩니다. 특정 조건을 충족하는 큐만 표시되도록 필터를 만들 수 있습니다.

4.  큐를 하나 이상 선택하고 마우스 오른쪽 단추를 클릭한 다음 **일시 중단**을 선택합니다.

## 셸을 사용하여 큐 일시 중단

큐를 일시 중단하려면 다음 구문을 사용합니다.

    Suspend-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

이 예에서는 로컬 서버에서 메시지 수가 1,000개 이상이고 상태가 다시 시도인 모든 큐를 일시 중단합니다.

    Suspend-Queue -Filter {MessageCount -ge 1000 -and Status -eq "Retry"}

이 예에서는 Mailbox01 서버에서 contoso.com이라는 큐를 일시 중단합니다.

    Suspend-Queue -Identity Mailbox01\contoso.com

## 작동 여부는 어떻게 확인합니까?

큐를 일시 중단되었는지 확인하려면 다음을 수행합니다.

1.  큐 뷰어 또는 **Get-Queue** cmdlet을 사용하여 일시 중단하려고 한 큐를 찾습니다.

2.  큐 **Status** 속성에 `Suspended` 값이 있는지 확인합니다.

