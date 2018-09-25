---
title: '관리 되는 폴더에서 마이그레이션: Exchange 2013 Help'
TOCTitle: 관리 되는 폴더에서 마이그레이션
ms:assetid: 6796a79d-501e-4216-9370-77965bc5835d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298032(v=EXCHG.150)
ms:contentKeyID: 52058095
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리 되는 폴더에서 마이그레이션

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

Microsoft Exchange Server 2013에서 MRM(메시징 레코드 관리)은 보존 태그 및 보존 정책을 사용하여 수행됩니다. 보존 정책은 사서함에 적용할 수 있는 보존 태그의 그룹입니다. 자세한 내용은 [보존 태그 및 보존 정책](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/messaging-records-management/retention-tags-and-policies)을 참조하십시오. Exchange Server 2007에 도입된 MRM 기술인 관리되는 폴더는 지원되지 않습니다.

관리되는 폴더 사서함 정책이 적용된 사서함을 마이그레이션하여 보존 정책을 사용할 수 있습니다. 이렇게 하려면 사용자의 관리되는 폴더 사서함 정책에 연결된 관리되는 폴더에 해당하는 보존 태그를 만들어야 합니다.


> [!IMPORTANT]
> 프로덕션 환경에서 관리되는 폴더에서 보존 정책으로 마이그레이션하기 전에 테스트 환경에서 프로세스를 테스트하는 것이 좋습니다.




> [!TIP]
> 사서함을 보존 설정하여 보존 정책이나 관리되는 폴더 사서함 정책의 처리를 중단할 수 있습니다. 사서함을 보존 설정하면 마이그레이션 시나리오에서 새 정책 설정이 테스트 사서함이나 소량의 프로덕션 사서함에서 테스트될 때까지 이 메시지가 삭제되거나 옮겨지는 것을 방지하는 데 도움이 됩니다. 자세한 내용은 <A href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold">사서함 보존에 원본 위치 유지</A>를 참조하십시오.



MRM과 관련된 기타 관리 작업에 대한 자세한 내용은 [메시징 레코드 관리 절차](messaging-records-management-procedures-exchange-2013-help.md)를 참조하십시오.

## 관리되는 폴더와 보존 태그 비교

사용자가 보존 설정을 기반으로 항목을 관리되는 폴더로 이동해야 하는 관리되는 폴더와 달리, 보존 태그는 사서함의 폴더 또는 개별 항목에 적용할 수 있습니다. 이 프로세스는 사용자의 워크플로 및 전자 메일 조직 방법에 최소의 영향을 미칩니다. 폴더에 보존 태그가 적용된 경우 해당 폴더에 있는 모든 항목은 보존 설정을 상속합니다. 사용자는 해당 폴더의 개별 항목에 서로 다른 보존 태그를 적용하여 보존 설정을 자세히 지정할 수 있습니다.

관리되는 폴더는 폴더에 대해 다양한 관리되는 콘텐츠 설정을 지원하며 메시지 클래스(예: 전자 메일 항목 또는 일정 항목)마다 서로 다른 관리되는 콘텐츠 설정이 지원됩니다. 보존 태그의 속성에는 보존 설정이 지정되어 있으므로 보존 태그에는 별도의 관리되는 콘텐츠 설정 개체가 필요하지 않습니다. 특정 메시지 클래스에 대해서는 보존 태그를 만들 수 없으며, 음성 메일 메시지의 경우 DPT(기본 정책 태그) 예외가 있습니다. 또한 보존 태그에서는 관리되는 폴더 도우미에서 수행된 저널링을 사용할 수 없습니다.


> [!NOTE]
> 저널 보고서가 포함된 메시지 복사본을 저널링 사서함으로 전송하는 데 사용되는 저널 규칙은 저널링 에이전트에 의해 전송 파이프라인에서 적용되며, MRM과는 별개입니다. 자세한 내용은 <A href="journaling-exchange-2013-help.md">저널링</A>을 참조하십시오.



다음 표에서는 보존 태그 또는 관리되는 폴더를 사용할 때 사용할 수 있는 MRM 기능을 비교합니다.

### 보존 태그와 관리되는 폴더 비교

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>보존 태그</th>
<th>관리되는 폴더</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 폴더(예: 받은 편지함)에 대한 보존 설정 지정</p></td>
<td><p>RPT(보존 정책 태그) 사용</p></td>
<td><p>관리되는 기본 폴더 사용</p></td>
</tr>
<tr class="even">
<td><p>전체 사서함에 대한 보존 설정 지정</p></td>
<td><p>DPT(기본 정책 태그) 사용</p></td>
<td><p>관리되는 기본 폴더 사용</p></td>
</tr>
<tr class="odd">
<td><p>사용자 지정 폴더에 대한 보존 설정 사용</p></td>
<td><p>개인 태그 사용</p></td>
<td><p>관리되는 사용자 지정 폴더 사용</p></td>
</tr>
<tr class="even">
<td><p>관리되는 콘텐츠 설정 필요</p></td>
<td><p>아니요(보존 태그에 포함된 보존 설정)</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>다양한 메시지 클래스(예: 전자 메일 메시지, 음성 메일 또는 일정 항목)에 대한 보존 설정 사용</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>항목을 사용자의 보관 사서함으로 이동하는 보관함으로 이동 동작 지원</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>관리되는 폴더로 이동 작업 지원</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>관리되는 폴더 도우미를 사용한 저널링 허용</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>사용자에게 적용된 정책</p></td>
<td><p>보존 정책</p></td>
<td><p>관리되는 폴더 사서함 정책</p></td>
</tr>
<tr class="even">
<td><p>사서함 사용자에게 적용할 수 있는 최대 정책 수</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>관리되는 폴더 도우미에 의해 처리</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>클라이언트 지원</p></td>
<td><p>Microsoft Outlook 2010 및 OfficeOutlook Web App</p></td>
<td><p>Outlook 2010, Office Outlook 2007 및 Outlook Web App</p></td>
</tr>
</tbody>
</table>


## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 20분

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - EAC(Exchange 관리 센터)를 사용하여 보존 정책을 기반으로 보존 태그를 만들 수는 없습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

## 관리되는 폴더의 사서함 사용자 마이그레이션

다음은 이 관리되는 폴더 사서함 정책에서 보존 정책으로 사용자를 마이그레이션하기 위한 일반적인 단계입니다. 각 단계에 대해서는 이 항목 뒷부분에서 자세하게 설명합니다.

1.  모든 Exchange 2010 및 Exchange 2007 사서함에 적용 된, 관리 되는 각 정책에는 폴더 및 관리 되는 각 폴더에 대 한 콘텐츠 설정을 관리 하는 관리 되는 폴더 사서함 정책에 대 한 정보를 수집 합니다. 이 정보를 가져올 Exchange 2010 또는 Exchange 2007 서버의 EMC 또는 셸을 사용할 수 있습니다.

2.  마이그레이션을 위한 보존 태그를 만듭니다.

3.  보존 정책을 만들고 새로 만든 보존 태그를 해당 정책에 연결합니다.

4.  관리되는 폴더 사서함 정책을 제거한 후 사용자 사서함에 보존 정책을 적용합니다.
    

    > [!IMPORTANT]
    > 보존 정책을 사용자에 적용하고 관리되는 폴더 도우미가 실행된 후에 사용자 사서함에 있는 관리되는 폴더는 관리되지 않는 상태가 됩니다.



다음 절차의 경우 Contoso 사서함에는 다음 관리되는 폴더가 포함된 관리되는 폴더 사서함 정책이 적용되어 있습니다.

### Contoso에 대한 관리되는 폴더

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>관리되는 폴더</th>
<th>관리되는 콘텐츠 설정</th>
<th>보존 사용</th>
<th>보존 기간</th>
<th>보존 작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Corp-DeletedItems</p></td>
<td><p>CS-Corp-DeletedItems</p></td>
<td><p>예</p></td>
<td><p>30일</p></td>
<td><p>삭제 및 복구 허용</p></td>
</tr>
<tr class="even">
<td><p>Corp-SentItems</p></td>
<td><p>CS-Corp-SentItems</p></td>
<td><p>예</p></td>
<td><p>1,825일</p></td>
<td><p>지운 편지함으로 이동</p></td>
</tr>
<tr class="odd">
<td><p>Corp-JunkMail</p></td>
<td><p>CS-Corp-JunkMail</p></td>
<td><p>예</p></td>
<td><p>30일</p></td>
<td><p>영구 삭제</p></td>
</tr>
<tr class="even">
<td><p>Corp-EntireMailbox</p></td>
<td><p>CS-Corp-EntireMailbox</p></td>
<td><p>예</p></td>
<td><p>365일</p></td>
<td><p>지운 편지함으로 이동</p></td>
</tr>
<tr class="odd">
<td><p>30일</p></td>
<td><p>CS-30Days</p></td>
<td><p>예</p></td>
<td><p>30일</p></td>
<td><p>지운 편지함으로 이동</p></td>
</tr>
<tr class="even">
<td><p>5년</p></td>
<td><p>CS-5Years</p></td>
<td><p>예</p></td>
<td><p>1,825일</p></td>
<td><p>지운 편지함으로 이동</p></td>
</tr>
<tr class="odd">
<td><p>사용 기간 제한 없음</p></td>
<td><p>CS-NeverExpire</p></td>
<td><p>아니요</p></td>
<td><p>365일</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


## 어떻게 해야 합니까?

## 1단계: 마이그레이션을 위한 보존 태그 만들기

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "메시징 레코드 관리" 항목

이 단계에 사용할 수 있는 두 가지 방법은 다음과 같습니다.

  - **관리되는 폴더 및 해당 관리되는 콘텐츠 설정을 기반으로 보존 태그 만들기**   이 방법을 사용할 경우 *ManagedFolderToUpgrade* 매개 변수와 함께 **New-RetentionPolicyTag** cmdlet을 사용합니다. 이 매개 변수를 지정할 경우 해당 보존 태그가 자동으로 관리되는 폴더에 적용됩니다.
    

    > [!IMPORTANT]
    > 이식할 관리되는 폴더에 다른 메시지 클래스의 여러 관리되는 콘텐츠 설정이 있는 경우, 보존 태그만이 만들어지며 관리되는 모든 콘텐츠 설정의 더 긴 보존 기간이 관리되는 콘텐츠 설정의 메시지 클래스에 관계 없이 이식된 태그의 보존 기간으로 사용됩니다.<BR>예를 들어 관리되는 폴더 Corp-DeletedItems의 관리되는 다음 콘텐츠 설정을 검토합니다.



  - **보존 설정을 수동으로 지정하여 보존 태그 만들기**   이 방법을 사용할 경우 *ManagedFolderToUpgrade* 매개 변수 없이 **New-RetentionPolicyTag** cmdlet을 사용합니다. 이 매개 변수를 지정하지 않으면 정책에 추가하는 보존 정책 태그가 기본 폴더에 적용되고 기본 정책 태그는 전체 사서함에 적용됩니다. 그러나 정책에 추가하는 개인 태그는 관리되는 폴더에 자동으로 적용되지 않습니다.


> [!NOTE]
> Exchange 2013 및 Exchange 2010 서버와 혼합된 환경을 사용 하는 경우에 쉽게 포트 관리 되는 폴더를 Exchange 2010 서버에서 Exchange 관리 콘솔 (EMC)에서 <STRONG>관리 되는 폴더 포트</STRONG> 마법사를 사용할 수 없으며 보존 태그를 콘텐츠 설정을 관리 하는 해당 합니다.



**관리되는 폴더를 기반으로 보존 태그 만들기**

이 예에서는 Contoso 관리되는 폴더 사서함 정책에 표시된 해당 관리되는 콘텐츠 설정을 기반으로 하여 보존 태그를 만듭니다.

```powershell
New-RetentionPolicyTag Corp-DeletedItems -ManagedFolderToUpgrade Corp-DeletedItems
New-RetentionPolicyTag Corp-SentItems -ManagedFolderToUpgrade Corp-SentItems
New-RetentionPolicyTag Corp-JunkMail -ManagedFolderToUpgrade Corp-JunkMail
New-RetentionPolicyTag Corp-EntireMailbox -ManagedFolderToUpgrade Corp-EntireMailbox
New-RetentionPolicyTag 30Days -ManagedFolderToUpgrade 30Days
New-RetentionPolicyTag 5Years -ManagedFolderToUpgrade 5Years
New-RetentionPolicyTag NeverExpire -ManagedFolderToUpgrade NeverExpire
```

구문과 매개 변수에 대한 자세한 내용은 [New-RetentionPolicyTag](https://technet.microsoft.com/ko-kr/library/dd335226\(v=exchg.150\))를 참조하십시오.

**수동으로 보존 태그 만들기**


> [!NOTE]
> EAC를 사용하여 수동으로 보존 태그를 만들 수도 있습니다(관리되는 폴더의 설정을 기반으로 하지 않음). 자세한 내용은 <A href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">보존 정책 만들기</A>를 참조하십시오.



이 예에서는 Contoso 관리되는 폴더 사서함 정책에 표시된 관리되는 폴더 및 해당 관리되는 콘텐츠 설정을 기반으로 하여 보존 태그를 만듭니다. 보존 설정은 *ManagedFolderToUpgrade* 매개 변수를 사용하지 않고 수동으로 지정합니다.

```powershell
New-RetentionPolicyTag Corp-DeletedItems -Type DeletedItems -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction DeleteAndAllowRecovery
New-RetentionPolicyTag Corp-SentItems -Type SentItems -RetentionEnabled $true -AgeLimitforRetention 1825 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag Corp-JunkMail -Type JunkMail -RetentionEnabled $true -AgeLimitforRetention 30 -RetentionAction PermanentlyDelete
New-RetentionPolicyTag Corp-EntireMailbox -Type All -RetentionEnabled $true -AgeLimitForRetention 365 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag 30Days -Type Personal -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag 5Years -Type Personal -RetentionEnabled $true -AgeLimitForRetention 1825 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag NeverExpire -Type Personal -RetentionEnabled $false
```

구문과 매개 변수에 대한 자세한 내용은 [New-RetentionPolicyTag](https://technet.microsoft.com/ko-kr/library/dd335226\(v=exchg.150\))를 참조하십시오.

## 2단계: 보존 정책 만들기

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "메시징 레코드 관리" 항목


> [!NOTE]
> EAC를 사용하여 보존 정책을 만들고 보존 태그를 정책에 추가할 수도 있습니다. 자세한 내용은 <A href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">보존 정책 만들기</A>를 참조하십시오.



이 예에서는 보존 정책 RP-Corp를 만들고 새로 만든 보존 태그를 정책에 연결합니다.

```powershell
New-RetentionPolicy RP-Corp -RetentionPolicyTagLinks Corp-DeletedItems,Corp-SentItems,Corp-JunkMail,Corp-EntireMailbox,30Days,NeverExpire
```

구문과 매개 변수에 대한 자세한 내용은 [New-RetentionPolicy](https://technet.microsoft.com/ko-kr/library/dd297970\(v=exchg.150\))를 참조하십시오.

## 3단계: 사용자 사서함에서 관리되는 폴더 사서함 정책 제거

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "보존 정책 적용" 항목

이 예에서는 Ken Kwok 사서함에서 관리되는 폴더 사서함 정책 및 모든 관리되는 폴더를 제거합니다. 메시지가 있는 관리되는 폴더는 제거되지 않습니다.

```powershell
Set-Mailbox -Identity Kwok -RemoveManagedFolderAndPolicy RP-Corp
```

## 4단계: 사용자 사서함에 보존 정책 적용

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "보존 정책 적용" 항목


> [!NOTE]
> EAC를 사용하여 보존 정책을 사용자에게 적용할 수도 있습니다. 자세한 내용은 <A href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/messaging-records-management/apply-retention-policy">사서함에 보존 정책 적용</A>을 참조하십시오.



이 예에서는 새로 만든 보존 정책 RP-Corp를 사서함 사용자 Ken Kwok에 적용합니다.

```powershell
Set-Mailbox -Identity Kwok -RetentionPolicy RP-Corp
```

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 이 작업의 작동 여부는 어떻게 확인합니까?

관리되는 폴더에서 보전 정책으로 마이그레이션되었는지 확인하려면 다음을 수행합니다.

  - 모든 사용자 사서함 및 이러한 사서함에 적용된 보존 정책에 대한 보고서를 생성합니다.
    
    이 명령은 조직에서 모든 사서함에 적용된 보존 정책 및 해당 보존 상태를 검색합니다.
    
    ```powershell
    Get-Mailbox -ResultSize unlimited -Filter {Name -NotLike "DiscoverySearch*�?} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto
    ```

  - 관리되는 폴더 도우미가 보존 정책을 포함한 사서함을 처리하고 나면 [Get-RetentionPolicyTag](https://technet.microsoft.com/ko-kr/library/dd298009\(v=exchg.150\)) cmdlet을 사용하여 사용자 사서함에서 프로비전된 보존 태그를 검색할 수 있습니다.
    
    이 명령은 April Stewart의 사서함에 실제로 적용된 보존 태그를 검색합니다.
    
    ```powershell
    Get-RetentionPolicyTag -Mailbox astewart
    ```

