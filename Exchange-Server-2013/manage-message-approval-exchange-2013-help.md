﻿---
title: '메시지 승인 관리: Exchange 2013 Help'
TOCTitle: 메시지 승인 관리
ms:assetid: 43a89f71-8002-4cb0-b3c8-1c2b2597f227
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd297936(v=EXCHG.150)
ms:contentKeyID: 50482980
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지 승인 관리

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-05-04_

때때로 메시지를 전달 하기 전에 메시지에서 렌즈의 두번째 집합을 것이 좋습니다. Exchange 관리자로이 설정할 수 있습니다. 이 프로세스를 *중재*호출 하 고 승인자 *중재자*라고 합니다. 어떤 메시지 승인 필요를 따라 두 방법 중 하나를 사용할 수 있습니다.

  - 메일 그룹 속성 변경

  - 메일 흐름 규칙 만들기

이 문서에 설명 합니다.

  - 사용 하 여 승인 방법을 결정 하는 방법

  - 승인 프로세스의 작동 방식

일반적인 시나리오를 구현 하는 방법을 알아보려면 [일반적인 메시지 승인 시나리오](common-message-approval-scenarios-exchange-2013-help.md)를 참조 하십시오.

## 사용 하 여 승인 방법을 결정 하는 방법

여기에서는 메시지 승인 하는 두 방법의 비교 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>무슨 작업을 하고 싶으십니까?</th>
<th>방식</th>
<th>1 단계</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>그룹에 모든 메시지를 승인 해야 살펴본된 메일 그룹을 만듭니다.</p></td>
<td><p>메일 그룹에 대 한 메시지 승인을 설정 합니다.</p></td>
<td><p>Exchange 관리 센터 (EAC) 이동 &gt; <strong>받는 사람</strong> &gt; <strong>그룹</strong>, 메일 그룹을 편집 하 고 다음 <strong>메시지 승인</strong> 를 선택 합니다.</p></td>
</tr>
<tr class="even">
<td><p>특정 조건에 일치 하는 또는 특정 사람에 게 전송 되는 메시지에 대 한 승인이 필요 합니다.</p></td>
<td><p><strong>승인을 위해 메시지 전달</strong> 동작을 사용 하 여 전송 규칙을 만듭니다.</p>
<p>받는 사람, 보낸사람, 및 텍스트 패턴을 포함 한 메시지 조건을 지정할 수 있습니다. 조건에는 예외를 포함할 수도 있습니다.</p></td>
<td><p>EAC를 이동 &gt; <strong>메일 흐름</strong> &gt; <strong>규칙</strong> 입니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 승인 프로세스의 작동 방식

사용자 또는 그룹 Outlook Web Access 사용 하 여 하는 경우 승인을 필요로 하는 메시지를 보내면 다른 사용자가 메시지를 지연 될 수 있습니다 알림을 받으면 있습니다.

![메시지 승인 알림을 보여주는 메시지](images/Dd297936.80e2e5f1-0a1e-4c37-9076-794581155405(EXCHG.150).png "메시지 승인 알림을 보여주는 메시지")

중재자에 요청을 승인 하거나 거부 하는 메시지와 전자 메일을 받습니다. 단추를 승인 하거나 거부 하는 메시지를 포함 하는 메시지의 텍스트 및 첨부 파일을 검토 하려면 원본 메시지를 포함 합니다.

![첨부 파일을 포함한 승인 요청 메시지](images/Dd297936.bf517f5a-b10e-40df-a48a-403b395b5962(EXCHG.150).png "첨부 파일을 포함한 승인 요청 메시지")

중재자 세 작업 중 하나를 사용할 수 있습니다.

![메시지 승인 옵션을 보여주는 워크플로](images/Dd297936.dc7a6ca9-c67d-487a-8713-4d628e07f4b3(EXCHG.150).png "메시지 승인 옵션을 보여주는 워크플로")

1.  승인 하는 경우 원래 의도 한 받는 사람에 게 메시지가 전달 합니다. 원래 보낸사람에 게 통보 되지 않습니다.

2.  거부 하는 경우 거부 메시지 보낸사람에 게 전송 됩니다. 중재자에 대 한 설명을 추가할 수 있습니다.
    
    ![중재자의 설명이 포함된 거부 알림](images/Dd297936.a663d36a-c67d-4155-b8f6-4b5dc8e105d9(EXCHG.150).png "중재자의 설명이 포함된 거부 알림")  

3.  승인자 중 하나를 삭제 또는 승인 메시지를 무시 하는 경우 만료 메시지 보낸사람에 게 전송 됩니다. Exchange Online 2 일 후 그리고 Exchange Server 2013 에서 5 일 후에 발생합니다. ( Exchange Server 2013 변경할 수 있습니다이 기간).

승인을 위해 대기 하는 메시지 *중재 사서함*을 호출 하는 시스템 사서함에 저장 일시적으로 가져옵니다. 메뉴 또는 도구 모음을 중재자 승인 하거나 거부 하는 메시지를 하기로 승인 메시지를 삭제 하는 승인 메시지 만료 수 있도록 때까지 원본 메시지는 중재 사서함에 저장 됩니다.

맨 위로 이동

## 질문 및 답변

**승인자 및 메일 그룹의 소유자 간의 차이 무엇입니까?**

메일 그룹의 소유자 메일 그룹 구성원 자격을 관리 하는 일을 담당 이지만 자신이 하 여 전송 된 메시지를 보통 할 수 있습니다. 사람 등 IT 수 메일 그룹의 소유자를 호출할 수 모든 직원 하지만 인사 관리자만 중재자도 설정할 수 있습니다.

**중재자 또는 승인자는 메일 그룹에 메시지를 보낼 때 수행 하는 작업**

메시지 승인 프로세스를 무시 하는 그룹에 직접 이동 합니다.

**받는 사람 중 일부만 할 때 수행 하는 작업 승인 해야 합니까?**

받는 사람 중 일부만 승인이 필요한 여기에서 받는 사람 그룹에 메시지를 보낼 수 있습니다. 그 중 하나는 중재 받는 메일 그룹으로 12 받는 사람에 게 보낸 메시지를 고려 합니다. 메시지에서 두 복사본 자동으로 분할 합니다. 승인 필요 하지 않은 11 받는 사람에 게 하나의 메시지를 즉시 배달 하 고 살펴본된 메일 그룹에 대 한 승인 프로세스에는 두번째 메시지는 전송 합니다. 메시지는 둘 이상의 중재 된 받는 사람에 대 한 있으며, 각 중재 된 받는 사람에 대 한 메시지의 별도 복사본을 자동으로 만들어집니다 하 고 적절 한 승인 프로세스를 통해 각 복사본 이동 합니다.

**승인이 필요한 받는 사람을 중재 내 메일 그룹에 포함 하는 경우에 어떻게 합니까?**

메일 그룹 승인에도 필요 하는 중재 된 받는 사람을 포함할 수 있습니다. 이 경우 메일 그룹에 메시지를 승인 되 면 메일 그룹의 구성원 인 각 중재 된 받는 사람에 대해 별도 승인 프로세스 발생 합니다. 그러나 살펴본된 메일 그룹에 메시지 승인 된 후 메일 그룹 구성원의 자동 승인을 설정할 수도 있습니다. 이 작업을 수행 하려면 [Set-DistributionGroup](https://technet.microsoft.com/ko-kr/library/bb124955\(v=exchg.150\)) cmdlet에서 *BypassNestedModerationEnabled* 매개 변수를 사용 합니다.

**자사 Exchange 서버가 있는 경우이 프로세스를 서로 다른가?**

기본적으로 각 Exchange 조직에 대해 하나의 중재 사서함 사용 됩니다. 사용자 고유의 Exchange 서버가 있는 부하 분산에 대 한 자세한 중재 사서함 필요 하는 경우 [관리 하 고 메시지 승인 문제를 해결합니다](manage-and-troubleshoot-message-approval-exchange-2013-help.md)에서 중재 사서함을 추가 하기 위한 지침을 따릅니다. 중재 사서함 시스템 사서함과 Exchange 라이선스가 필요 하지 않습니다.


> [!NOTE]
> <STRONG>Exchange 2007 있는 경우:</STRONG> Microsoft Exchange Server 2007 중재 된 받는 사람을 지원 하지 않습니다. 살펴본된 메일 그룹에 게 보낸 메시지는 Exchange 2007 허브 전송 서버에서 확장 되 면 하는 경우 메시지 중재를 무시 하 고 메일 그룹의 모든 구성원에 게 배달 됩니다. Exchange 조직에서 Exchange 2007 허브 전송 서버를 포함 하는 경우 살펴본된 메일 그룹에 대 한 확장 서버로 Exchange Server 2013 사서함 서버를 지정 하는 경우이 해야 합니다. 이렇게 하면 메일 그룹에 보내는 모든 메시지가 중재 됩니다.



맨 위로 이동

## 자세한 정보가 필요 하십니까?

[메일 흐름 규칙 관리](manage-mail-flow-rules-exchange-2013-help.md)

[Exchange 2013에 대 한 Exchange 관리 셸 빠른 참조](exchange-management-shell-quick-reference-for-exchange-2013-exchange-2013-help.md)

[Exchange Online PowerShell](https://technet.microsoft.com/ko-kr/library/jj200677\(v=exchg.150\))
