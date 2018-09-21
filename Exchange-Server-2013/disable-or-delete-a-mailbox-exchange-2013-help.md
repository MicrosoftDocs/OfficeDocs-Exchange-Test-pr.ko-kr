---
title: '사용 하지 않거나 사서함 삭제: Exchange 2013 Help'
TOCTitle: 사용 하지 않거나 사서함 삭제
ms:assetid: 31ad25d6-2942-4fd9-aecb-cdf9654163d2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ863434(v=EXCHG.150)
ms:contentKeyID: 50555963
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 하지 않거나 사서함 삭제

 

_**적용 대상:** Exchange Server 2013 SP1_

_**마지막으로 수정된 항목:** 2015-03-09_

사용 하지 않도록 설정 하거나 삭제 된 사서함 Exchange 2013 EAC 또는 셸을 사용할 수 있습니다. 사서함을 사용 하지 않도록 설정 하거나 삭제 Exchange 사서함 데이터베이스에서 사서함을 유지 하 고 사서함을 비활성된 상태로 전환 합니다. 비활성화 및 삭제 된 사서함은 사서함 데이터베이스에서 삭제 된 사서함 보존 기간이 만료 되 면 30 일 때까지 기본적으로 유지 됩니다. 사서함 영구적으로 삭제 보존 기간이 만료 되 면 후 되거나 *제거*합니다.

Exchange Online으로 사서함 삭제 해야하는 경우 [Exchange Online의 사용자 사서함을 복원 또는 삭제](https://technet.microsoft.com/ko-kr/library/dn186233\(v=exchg.150\))를 참조 하십시오.


> [!NOTE]
> 비활성화 또는 삭제 된 사서함은 <EM>사서함 연결을 끊은</EM>으로 이라고 합니다.



삭제 하 고 사서함을 사용 하지 않도록 설정 간의 주요 차이점 때는 사서함을 사용 하지 않도록 설정, Exchange 특성 해당 Active Directory 사용자 계정에서 제거 되지만 사용자 계정이 그대로 유지 됩니다. 사서함을 삭제 하는 경우에 Exchange 특성 및 Active Directory 사용자 계정을 모두 삭제 됩니다. 이 차이 다시 연결 하거나 비활성화 및 삭제 된 사서함을 복원 하도록 옵션을 결정 합니다.

다음 표에 Exchange 사서함의 형식을 사용 하지 않도록 설정 하거나 삭제할 수 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>사서함 유형</th>
<th>사용 하지 않습니까?</th>
<th>삭제 하 시겠습니까?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>보관 사서함</p></td>
<td><p>예</p></td>
<td><p>더 *</p></td>
</tr>
<tr class="even">
<td><p>연결된 사서함</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>리소스 사서함 (회의실 또는 장비)</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>공유 사서함</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>사용자 사서함</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
</tbody>
</table>


\* 보관 사서함을 사용 하는 경우 기본 사서함 삭제 될 때 삭제 될 됩니다. 보관 사서함을 사용 하지 않도록 설정 하는 방법에 대 한 정보를 [Exchange 2013에서 원본 위치 보관 관리](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)을 참조 하십시오.

사서함을 보유 하는 사용자 계정을 삭제 하는 관리자, 사서함 사용자 계정에 연결 되어있지 않습니다 해당 사서함을 삭제 하도록 표시, 사서함의 경우에 유지 하는 Exchange 정보 저장소 검색 결국 것입니다. 사서함을 유지 하려는 경우 다음을 수행 해야 합니다.

1.  사용자 계정을 삭제 하는 대신 사용자 계정을 사용 하지 않도록 설정 합니다.

2.  해당 사용을 제한 하 고 사서함에 액세스 하는 사서함의 속성을 변경 합니다. 예, 집합 보내고 할당량 1, 사서함에 액세스할 수 있는 사용자 제한 및 사서함에 메시지를 보낼 수 있는 블록으로 받습니다.

3.  대기는 더 이상 필요 하거나 모든 데이터를 expunged 되었는지, 될 때까지 사서함을 유지 합니다.

연결이 끊어진 사서함과 관련된 추가 관리 작업에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [연결이 끊어진 사서함](disconnected-mailboxes-exchange-2013-help.md)

  - [비활성화 된 사서함에 연결](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [삭제 된 사서함을 복원 또는 연결](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [사서함을 영구적으로 삭제](permanently-delete-a-mailbox-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 사서함을 사용 하지 않도록 설정

듯이 사서함을 사용 하지 않도록 설정, Exchange 특성은 해당 Active Directory 사용자 계정에서 제거 된 하지만 사용자 계정이 그대로 유지 됩니다.

## EAC를 사용 하 여 사서함을 사용 하지 않도록 설정 하려면

다음 절차에서는 사용자 사서함을 사용 하지 않도록 설정 하는 방법을 보여줍니다. 동일한 절차를 사용 하 여 EAC에서 적절 한 페이지로 이동한 후 다른 사서함 유형을 사용 하지 않도록 설정 합니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 사용 하지 않도록 설정 하려는 사서함을 클릭 합니다.

3.  **자세히** ![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘")를 클릭한 후 **사용 안 함**을 클릭합니다.

4.  사서함을 사용 하지 않도록 설정 하려면 확실 한 경우 경고를 묻는 나타납니다. **예** 를 눌러 사서함을 사용 하지 않도록 설정 합니다.

사서함은 사서함 목록에서 제거 됩니다.

## 셸을 사용하여 사서함을 사용하지 않도록 설정

다음 명령을 사용 하 여 사용자 사서함, 연결 된 사서함, 리소스 사서함 및 공유 사서함을 사용 하지 않도록 설정 합니다.

```powershell
Disable-Mailbox <identity>
```

이 명령을 실행 하면 사서함을 사용 하지 않도록 설정 하려면 확인을 요청 하는 메시지가 표시 됩니다.

다음은 사서함을 사용 하지 않도록 설정 하는 것에 대 한 명령의 예입니다.

```
Disable-Mailbox danj
```

```
Disable-Mailbox "Conf Room 31/1234 (12)"
```

```
Disable-Mailbox sharedmbx@contoso.com
```

## 작동 여부는 어떻게 확인합니까?

성공적으로 사서함을 사용 하지 않도록 했을 때를 확인 하려면 다음 중 하나를 수행 합니다.

  - EAC에서 **받는 사람** 을 클릭 하 고 사용 하지 않도록 설정한 사서함 형식에 대 한 적절 한 페이지로 이동 사서함 더이상 나타나는지 확인 합니다.

  - Active Directory 사용자 및 컴퓨터에서 사용자 계정을 사용 하지 않도록 설정 하면 사서함을 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 클릭 합니다. **일반** 탭에서 **전자 메일** 필드가 비어 있는지 확인 합니다. 사서함을 사용 하지 않도록 설정 하지만 사용자 계정이 여전히 존재 하는 것을 확인 합니다.

  - 셸에서 다음 명령을 실행합니다.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    *DisconnectReason* 속성에 `Disabled` 값 사서함 비활성화 되어 있음을 나타냅니다.
    

    > [!NOTE]
    > 사서함을 삭제 하는 경우 <EM>DisconnectReason</EM> 속성에 값 <CODE>Disabled</CODE>이기도 합니다. 그러나 해당 Active Directory 사용자 계정이 삭제 됩니다.



  - 셸에서 다음 명령을 실행합니다.
    
    ```powershell
Get-User <identity>
```
    
    *RecipientType* 속성에 대 한 값이 있는 메모는 `User`, `UserMailbox`하는 대신 활성화 된 사서함이 있는 사용자에 대 한 값입니다. 이 확인 하는 사서함을 사용 하지 않도록 설정 하지만 사용자 계정이 그대로 유지 됩니다.

## 사서함 삭제

앞서 설명한 것 처럼 사서함을 삭제 하는 경우 Exchange 특성 및 Active Directory 사용자 계정을 모두 삭제 됩니다. 사서함 (및 보관 사서함에 설정 된 경우)가 영구적으로 삭제 됩니다 사서함 데이터베이스에서 사서함 보존 기간이 만료 후 합니다.

## EAC를 사용 하 여 사서함을 삭제 하려면

다음 절차에서는 사용자 사서함을 삭제 하는 방법을 보여줍니다. EAC에서 적절 한 페이지로 이동한 후 다른 사서함 종류를 삭제 하려면 동일한 절차를 사용 합니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 삭제 하려는 사서함을 클릭 하 고![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")**삭제** 를 클릭 합니다.

3.  사서함을 삭제 하려면 확실 한 경우 경고를 묻는 나타납니다. **예** 를 클릭 사서함을 삭제 합니다.

사서함은 사서함 목록에서 제거 됩니다.

## 셸을 사용하여 사서함 삭제

사용자 사서함, 연결 된 사서함, 리소스 사서함 및 공유 사서함을 삭제 하려면 다음 명령을 사용 합니다.

```powershell
Remove-Mailbox <identity>
```

이 명령을 실행 하면 사서함 및 해당 Active Directory 사용자 계정을 제거 하려면 확인을 요청 하는 메시지가 표시 됩니다.

다음은 사서함 삭제 명령의 예입니다.

```
Remove-Mailbox pilarp@contoso.com
```

```
Remove-Mailbox "Fleet Van (16)"
```

```
Remove-Mailbox corpprint
```

## 작동 여부는 어떻게 확인합니까?

사서함을 삭제 성공적으로 했는지를 확인 하려면 확인 절차의 다음 설정 중 하나를 수행 합니다.

1.  EAC에서 **받는 사람** 을 클릭 하 고 삭제 하는 사서함 형식에 대 한 적절 한 페이지로 이동 및 사서함 더이상 나열 되는지 확인 합니다.

2.  Active Directory 사용자 및 컴퓨터에서 해당 사용자 계정을 더 이상 나타나는지 확인 합니다.

또는

1.  사서함 삭제 되었는지 확인 하려면 다음 명령을 실행 합니다.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    *DisconnectReason* 속성에 `Disabled` 값은 사서함 삭제 된 것을 나타냅니다.
    

    > [!NOTE]
    > 사서함 사용 하지 않는 경우 <EM>DisconnectReason</EM> 속성에 값 <CODE>Disabled</CODE>이기도 합니다. 그러나 해당 Active Directory 사용자 계정이 그대로 유지 됩니다.



2.  Active Directory 사용자 계정이 삭제 되었는지 확인 하려면 다음 명령을 실행 합니다.
    
    ```powershell
Get-User <identity>
```
    
    명령은은 계정이 삭제 되었는지 확인 (영문), 해당 사용자를 찾을 수 없는 되었다는 오류를 반환 합니다.

