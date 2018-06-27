---
title: '관리 하 고 메시지 승인 문제를 해결합니다: Exchange 2013 Help'
TOCTitle: 관리 하 고 메시지 승인 문제를 해결합니다
ms:assetid: 860df43f-a05b-4da3-83f1-68d3123a923d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298110(v=EXCHG.150)
ms:contentKeyID: 52058093
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리 하 고 메시지 승인 문제를 해결합니다

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

중재 사서함을 제거 하려고 하면 다음과 같은 오류가 나타날 수 있습니다.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>멤버 자격 제한 또는 중재 기능이 사용 하는 기존 받는 사람에 대 한 승인 워크플로 사용 되 고 되기 때문에 &lt;<em>mailbox</em>&gt; 중재 사서함을 제거할 수 없습니다. 선택 된 받는 사람에 승인 기능을 사용 하지 않도록 설정 해야 하거나이 중재 사서함을 제거 하기 전에 해당 받는 사람에 대 한 다른 중재 사서함을 지정 합니다.</p></td>
</tr>
</tbody>
</table>


중재 된 받는 사람 및 메일 그룹 멤버 자격 승인에 대 한 승인 워크플로 처리 하는 중재 사서함을 사용할 수 있습니다. PowerShell을 사용 하 여 중재 사서함을 사용 하도록 구성 된 모든 받는 사람을 찾을 수 있습니다. 받는 사람을 파악 한 후 다른 중재 사서함을 사용 하도록 구성할 수 있습니다 또는 해당 중재를 사용 하지 않도록 설정할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "Aribtration" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 1 단계: 셸을 사용 하 여 삭제 하려는 중재 사서함을 사용 하는 모든 받는 사람을 찾을 수

다음 명령을 실행합니다.

    $AM = Get-Mailbox "<arbitration mailbox>" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

예, 중재 mailbox01 중재 사서함을 사용 하는 모든 받는 사람을 찾으려면 다음 명령을 실행 합니다.

    $AM = Get-Mailbox "Arbitration Mailbox01" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}


> [!NOTE]
> 중재 사서함의 DN (고유 이름)을 사용 하 여 지정 됩니다. 중재 사서함의 DN을 알고 있는 경우에 단일 명령을 실행할 수 있습니다: <CODE>Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq &lt;DN&gt;}</CODE>합니다.



## 2 단계: 셸을 사용 하 여 다른 중재 사서함을 지정 하거나 받는 사람에 대 한 중재를 사용 하지 않도록 설정 하려면

삭제 하려는 중재 사서함을 사용 하 여에서 중재 된 받는 사람을 중지 하려면 다른 중재 사서함을 지정 하거나 또는 받는 사람에 대 한 중재를 사용 하지 않도록 설정할 수 있습니다.

받는 사람에 대 한 다른 중재 사서함을 지정 하려는 경우 다음 명령을 실행 합니다.

    Set-<RecipientType> <Identity> -ArbitrationMailbox <different arbitration mailbox>

예 구성원 승인에 대 한 중재 mailbox02 중재 사서함을 사용 하 여 모든 직원 라는 메일 그룹을 다시 구성 하려면 다음 명령을 실행 합니다.

    Set-DistributionGroup "All Employees" -ArbitrationMailbox "Arbitration Mailbox02"

받는 사람에 대 한 중재를 사용 하지 않도록 설정 하려는 경우 다음 명령을 실행 합니다.

    Set-<RecipientType> <Identity> -ModerationEanbled $false

예, Human Resources 라는 사서함에 대 한 중재를 사용 하지 않으려면 다음 명령을 실행 합니다.

    Set-Mailbox "Human Resources" -ModerationEanbled $false

## 작동 여부는 어떻게 확인합니까?

프로시저 성공적으로 완료 하는 경우 사용 되는 오류 메시지를 수신 하지 않고 중재 사서함을 삭제할 수 있습니다.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

