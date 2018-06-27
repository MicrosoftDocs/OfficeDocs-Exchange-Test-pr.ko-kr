---
title: '모든 사서함을 보류: Exchange 2013 Help'
TOCTitle: 모든 사서함을 보류
ms:assetid: 4c141604-3210-44cc-b98e-f3e0f15613b8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn767952(v=EXCHG.150)
ms:contentKeyID: 62486287
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 모든 사서함을 보류

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-01-18_


> [!NOTE]
> Exchange Online(Office 365 및 Exchange Online 독립 실행형 계획)에 새 원본 위치 유지 만들기에 대한 마감 날짜인 2017년 7월 1일을 연기했습니다. 하지만 올해 말 또는 내년 초에는 Exchange Online에 새 원본 위치 유지를 만들 수 없습니다. 원본 위치 유지를 사용하는 대신, Office 365 보안 및 준수 센터의 <A href="https://go.microsoft.com/fwlink/?linkid=780738">eDiscovery 사례</A> 또는 <A href="https://go.microsoft.com/fwlink/?linkid=827811">보존 정책</A>을 사용할 수 있습니다. 새 원본 위치 유지를 해제한 후에도 기존 원본 위치 유지를 계속 수정할 수 있으며 Exchange Server 2013 및 Exchange 하이브리드 배포에서 새 원본 위치 유지를 계속 만들 수 있습니다. 또한 사서함을 소송 보존 상태로 계속 유지할 수 있습니다.



조직의 모든 사서함 데이터를 특정 기간에 대 한 유지할지 필요할 수 있습니다. 이 요구 사항을 충족 하기 위해 소송 보존 또는 원본 위치 유지를 사용할 수 있습니다. 원본 위치 유지 또는 소송 보존으로 설정 된 사서함을 삽입 한 후 복구 가능한 항목 폴더에서 사서함 항목을 수정 하는 또는 영구적으로 삭제 하는 유지 됩니다. 자세한 내용은 [원본 위치 유지 및 소송 보존](in-place-hold-and-litigation-hold-exchange-2013-help.md)을 참조 하십시오.

조직의 모든 사서함을 소송 보존 또는 원본 위치 유지 상태로 두기 전에 다음을 고려하세요.

  - 보류에서 사서함을 배치할 때 (활성화 되어 있음) 하는 경우 사용자의 보관 사서함의 콘텐츠도 대기 상태로 설정 됩니다.

  - 대기 조직에서 모든 사서함을 배치 사서함 크기 큰 영향을 줄 수 있습니다. Exchange Server 2013 배포에서 조직의 보존 요구를 충족 하기 위해 적절 한 저장소를 계획 합니다. Exchange Online[사서함 저장소 제한](https://go.microsoft.com/fwlink/?linkid=403645) 사용자에 대 한 사용자의 구독 라이선스에 따라 달라 집니다.

  - 긴 기간에 대 한 사서함 데이터를 유지 한 사용자의 기본 사서함 및 보관 사서함의 복구 가능한 항목 폴더의 성장에 발생 합니다. 복구 가능한 항목 폴더는 폴더의 항목 사서함 저장소 제한에 가깝게 계산 하지 않도록 자체 저장 용량 제한을 있습니다. Exchange Server 2013 및 Exchange Online 에서 복구 가능한 항목 폴더에 대 한 기본 저장 용량 제한은 30GB입니다.
    
      - 복구 가능한 항목 폴더에 대 한 할당량 Exchange Online 자동으로 대기 사서함을 할 때 100GB로 증가 되었습니다.
    
      - Exchange Server 2013 정기적으로 제한에 도달 하지 것을 확인 하려면이 폴더의 크기를 모니터링 하는 것이 좋습니다. 자세한 내용은 [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)을 참조 하십시오.

## 소송 보존 하 고 전체 보류 간에 선택

다음은 보류 기능을 사용 하 여 조직의 모든 사서함에 배치를 보류를 결정할 때 고려 해야할 몇가지 요인입니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>수행하려는 작업</th>
<th>소송 보존 사용</th>
<th>원본 위치 유지 사용</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EAC를 사용하여 다음을 수행합니다.</p></td>
<td><p>예</p>
<p>소송 보존 설정, EAC는 빠른 일회용 작업 몇 사서함에 가장 적합 합니다. 셸을 사용 하 여 조직의 모든 사용자에 대 한 소송 보존을 설정 하기 위한 것이 좋습니다.</p></td>
<td><p>예</p>
<p>그렇지만 EAC에서는 소스가 500개를 초과하는 사서함을 선택할 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>셸 사용</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>10,000개를 초과하는 사서함 보류</p></td>
<td><p>예</p>
<p>소송 보존은 사서함 속성입니다. <strong>Set-Mailbox</strong> cmdlet을 사용 하 여 모든 사서함 보류에서 조직에 배치할 수 있습니다.</p></td>
<td><p>예; 여러 원본 위치 유지를 사용 하 여</p>
<p>단일 원본 위치 유지에 최대 10, 000 사서함을 지정 하려면 메일 그룹을 사용할 수 있습니다. 사서함을 추가로를 대기 시키려면 추가 원본 위치 유지 만들어야 합니다. 이 추가 관리 오버 헤드가 발생 합니다. 소송 보존 배치할 많은 수의 사서함에서이 더 간단 유지를 사용 합니다.</p></td>
</tr>
<tr class="even">
<td><p>다양한 기간 동안 여러 다른 사서함을 보류합니다.</p></td>
<td><p>예</p>
<p>소송 보존은 사서함 속성입니다. 각 사서함 또는 사서함 집합을 다른 기간 동안 보류할 수 있습니다.</p>
<p>자세한 내용 은 섹션을 소송 보존 사서함의 하위 집합에 배치할 수 있도록 하는 필터에 받는 사람 속성을 사용 하는 예제를 참조 하십시오.</p></td>
<td><p>예</p>
<p>수천 개의 사서함을 개별적으로 보존하려면 소송 보존을 사용하는 것이 좋습니다. 여러 사용자가 관여하는 특정 이벤트에 대해 원본 위치 유지를 만드는 경우 사용자 그룹에 대해 단일 원본 위치 유지를 사용합니다.</p>
<p>소송 보존을 포함 하 고 보다 관리 하기가 더 어려울 수 있는 여러 원본 위치 유지 쿼리를 만들고이 처럼 각 사서함에 대 한 별도 전체 보류를 만들려면 하지는 것이 좋습니다. 많은 수의 원본 위치 유지 개체도 새로 고칠 수 있습니다, 만들기 또는 대기 개체를 수정 하는 경우 EAC의 성능이 저하 될 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>새 사서함을 자동으로 원본 위치에 보류</p></td>
<td><p>아니요</p>
<p>만든 후 새 사서함 소송 보존에 배치 해야 합니다. 명령이 나 스크립트 필요한 만큼 자주 실행 하려면 동일한 효과 얻을 수를 예약할 수 있습니다.</p></td>
<td><p>아니요</p>
<p>원본 위치 유지를 만들 때 메일 그룹을 지정 하는 경우에 원본 위치 유지를 새 사서함을 추가 해야 합니다. 명령이 나 스크립트 필요한 만큼 자주 실행 하려면 동일한 효과 얻을 수를 예약할 수 있습니다. 것을 권장 하는 스크립트 검사 10, 000 사서함 제한에 이미 도달한 기존 원본 위치 유지 하는 경우 하 고 필요한 경우 새로운 원본 위치 유지를 만듭니다.</p></td>
</tr>
<tr class="even">
<td><p>보류에 배치 하는 모든 공용 폴더</p></td>
<td><p>아니요</p>
<p>Exchange Online 공용 폴더 사서함에 소송 보존을 배치할 수 없습니다. 원본 위치 유지를 사용 해야 합니다.</p></td>
<td><p>예</p></td>
</tr>
</tbody>
</table>


## 모든 사서함을 소송 보존으로 설정

쉽고 빠르게에 배치할 수 있습니다 모든 사서함 보류 무기한 또는 셸을 사용 하 여 지정 된 기간입니다. 이 명령은 2555 일 (약 7 년)에 대 한 보류에서 모든 사서함을 배치합니다.

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 2555

이 예제에서는 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) cmdlet 및 받는 사람 필터를 사용 하 여 조직에 있는 모든 사용자 사서함을 검색 한 다음 목록이 사서함을 소송 보존을 설정 하 고 보존 기간을 지정 하려면 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) cmdlet에 파이프 합니다. 자세한 내용은 [전체 사서함에 소송 보존으로 설정](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)를 참조 하십시오.

## 모든 사서함을 원본 위치 유지 상태로 설정

EAC를 사용하여 최대 500개의 사서함을 선택하고 보류할 수 있습니다. 자세한 내용은 [만들기 또는 In-place Hold 제거](create-or-remove-an-in-place-hold-exchange-2013-help.md)을 참조하세요.


> [!TIP]
> 원본 위치 유지를 500 명 이상의 사용자를 시키려면 셸을 사용 합니다. <A href="https://technet.microsoft.com/ko-kr/library/dd298064(v=exchg.150)">New-MailboxSearch</A>를 참조 하십시오.



## 추가 정보

  - 보류에 조직의 모든 사서함을 배치 하는 경우 명령을 실행 하는 시간에 존재 하는 사서함만 보류에 배치 됩니다. 만들 새 사서함 나중에 다시 하 게 유지에서 명령을 실행 유지 합니다. 새 사서함을 자주 만들어야 하는 경우 필요에 따라 자주 명령으로 예약 된 작업을 실행할 수 있습니다.

  - 지정한 끝나기 전에 삭제를 방지 하 고를 수정 하기 전에 메시지의 원래 버전을 저장 하 여 데이터를 유지 대기 사서함을 배치 합니다. 지정 된 기간 이후에 메시지 자동으로 삭제 되지 않습니다. 조직의 전자 메일 보존 요구를 충족 하기 위해 소송 보존으로 설정 또는 지정 된 기간 후 메시지를 자동으로 삭제할 수, 하는 보존 정책을 사용 하 여 원본 위치 유지를 결합 합니다. 자세한 내용 은 [보존 태그 및 보존 정책](retention-tags-and-retention-policies-exchange-2013-help.md) 참조 하십시오.

  - 이 항목에서 사용 하 여 모든 사서함에 소송 보존을 배치 하는 PowerShell 명령을 모든 사용자 사서함을 반환 하는 받는 사람 필터를 사용 합니다. 다음에 연결할 수 **Set-Mailbox** cmdlet에 해당 사서함에 소송 보존을 배치 하는 특정 사서함의 목록을 반환 하려면 다른 받는 사람 속성을 사용할 수 있습니다.
    
    다음은 일반적인 사용자 또는 사서함 속성을 기준으로 사서함의 하위 집합을 반환 하려면 **Get-Mailbox** 및 **Get-Recipient** cmdlet을 사용 하 여 몇가지 예입니다. 이 예제에서는 관련 사서함 속성 (예: *CustomAttributeN* 또는 *Department*) 채워지고 가정 합니다.
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    
    포함 하거나 사서함을 제외 하는 필터에 다른 사용자 사서함 속성을 사용할 수 있습니다. 자세한 내용은 [필터링 할 수 있는 속성에-Filter 매개 변수](https://technet.microsoft.com/ko-kr/library/bb738155\(v=exchg.150\))를 참조 합니다.

