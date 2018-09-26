---
title: '비활성화 된 사서함에 연결: Exchange 2013 Help'
TOCTitle: 비활성화 된 사서함에 연결
ms:assetid: a8abd399-75fd-4ee2-b2e4-634b55e4f79f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ863439(v=EXCHG.150)
ms:contentKeyID: 50556059
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 비활성화 된 사서함에 연결

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-13_

EAC 또는 셸을 사용하여 Active Directory 사용자 계정에 사용되지 않는 사서함을 연결할 수 있습니다. 사서함을 사용하지 않도록 설정하면 해당 사서함이 사서함 데이터베이스에 보관되고 비활성 상태로 전환됩니다. Exchange 특성도 해당 Active Directory 사용자 계정에서 제거되지만 사용자 계정은 유지됩니다. 사서함은 삭제된 사서함 보존 기간(기본값은 30일)이 만료될 때까지 보관되었다가 사서함 데이터베이스에서 영구적으로 삭제(또는 *제거*)됩니다.

사용되지 않는 사서함이 Exchange 사서함 데이터베이스에서 영구적으로 삭제되기 전까지는 EAC 또는 셸을 사용하여 사서함을 원래 Active Directory 사용자 계정에 다시 연결할 수 있습니다.

연결이 끊어진 사서함에 대해 자세히 알아보고 관련 관리 작업을 수행하려면 다음 항목을 참조하십시오.

  - [연결이 끊어진 사서함](disconnected-mailboxes-exchange-2013-help.md)

  - [사용 하지 않거나 사서함 삭제](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [삭제 된 사서함을 복원 또는 연결](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [사서함을 영구적으로 삭제](permanently-delete-a-mailbox-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 셸에서 **Get-User** cmdlet을 실행하여 사용되지 않는 사서함을 연결할 Active Directory 사용자 계정이 있으며 이미 다른 사서함에 연결되어 있지는 않은지 확인합니다. 사용되지 않는 사서함을 사용자 계정에 연결하려면 해당 계정이 있어야 하고 *RecipientType* 속성의 값이 `User`여야 합니다. 이 값은 해당 계정이 아직 사서함을 사용하는 계정이 아님을 나타냅니다.
    
    온-프레미스 Exchange 조직의 경우 Active Directory 사용자 및 컴퓨터에서도 이 정보를 확인할 수 있습니다.

  - 다음 명령을 실행하여 사용자 계정을 연결하려는 사용되지 않는 사서함이 사서함 데이터베이스에 있으며 일시 삭제된 사서함이 아닌지 확인합니다.
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    ```    
    사용되지 않는 사서함을 연결하려면 사서함이 사서함 데이터베이스에 있고 *DisconnectReason* 속성의 값이 `Disabled`여야 합니다. 사서함이 데이터베이스에서 제거된 경우에는 명령에서 어떤 결과도 반환되지 않습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사용되지 않는 사서함 연결

다음 절차에서는 사용되지 않는 사용자 사서함을 연결하는 방법을 보여 줍니다. 연결된 사서함과 공유 사서함을 사용하지 않도록 설정한 후 이를 해당 사용자 계정에 다시 연결할 수도 있습니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  **자세히** ![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘")를 클릭하고 **사서함 연결**을 클릭합니다.
    
    Exchange 조직의 선택한 Exchange 서버에서 연결이 끊어진 사서함이 목록으로 표시됩니다.
    

    > [!NOTE]   
    > 연결이 끊어진 사서함 목록에는 비활성 사서함, 삭제된 사서함 및 일시 삭제된 사서함이 포함됩니다.


3.  다시 연결하려는 사용되지 않는 사서함을 클릭하고 **연결**을 클릭합니다.

4.  사서함을 다시 연결할지 묻는 창이 표시되면 **예**를 클릭합니다.
    
    사용되지 않는 사서함이 해당 사용자 계정에 다시 연결됩니다.

## 셸을 사용하여 사용되지 않는 사서함 연결

셸에서 **Connect-Mailbox** cmdlet을 사용하여 사용자 계정을 사용되지 않는 사서함에 연결할 수 있습니다. 연결하려는 사서함의 유형을 지정해야 합니다. 다음 예에서는 사용자 사서함, 연결된 사서함 및 공유 사서함을 다시 연결하기 위한 구문을 보여 줍니다.

이 예에서는 사용자 사서함을 연결합니다. *Identity* 매개 변수는 Exchange 데이터베이스에 있는 연결이 끊어진 사서함을 지정합니다. *User* 매개 변수는 사서함을 다시 연결할 Active Directory 사용자 계정을 지정합니다.

```powershell
Connect-Mailbox -Identity "Jeffrey Zeng" -Database MBXDB01 -User "Jeffrey Zeng"
```

이 예에서는 연결된 사서함을 연결합니다. *Identity* 매개 변수는 Exchange 데이터베이스에 있는 연결이 끊어진 사서함을 지정합니다. *LinkedMasterAccount* 매개 변수는 사서함을 다시 연결할 계정 포리스트의 Active Directory 사용자 계정을 지정합니다. *Alias* 매개 변수는 다시 연결된 사서함의 별칭, 즉 전자 메일 주소에서 @ 기호의 왼쪽 부분을 지정합니다.

```powershell
Connect-Mailbox -Identity "Kai Axford" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount kai.axford@fabrikam.com -Alias kaia
```

이 예에서는 공유 사서함을 연결합니다.

```powershell
Connect-Mailbox -Identity "Corporate Shared Mailbox" -Database "Mailbox Database 03" -User "Corporate Shared Mailbox" -Alias corpshared -Shared
```

> [!NOTE]
> <STRONG>Connect-Mailbox</STRONG> cmdlet을 실행할 때 <EM>Alias</EM> 매개 변수를 포함하지 않을 경우 <EM>User</EM> 또는 <EM>LinkedMasterAccount</EM> 매개 변수에 지정된 값을 사용하여 다시 연결할 사서함의 전자 메일 주소 별칭이 만들어집니다.



구문과 매개 변수에 대한 자세한 내용은 [Connect-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997878\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사용되지 않는 사서함이 사용자 계정에 연결되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람**을 클릭하고 다시 연결한 사서함 유형에 해당하는 페이지로 이동한 다음 **새로 고침**![새로 고침 아이콘](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "새로 고침 아이콘")을 클릭하여 사서함이 표시되는지 확인합니다.

  - Active Directory 사용자 및 컴퓨터에서 사서함을 사용하지 않도록 설정했던 원래 사용자 계정을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. **일반** 탭에서 **전자 메일** 상자가 다시 연결된 사서함의 전자 메일 주소로 채워져 있는지 확인합니다.

  - 셸에서 다음 명령을 실행합니다.
    
    ```powershell
    Get-User <identity>
    ```
    
    *RecipientType* 속성의 **UserMailbox** 값은 사용자 계정과 사서함이 연결되었음을 나타냅니다. **Get-Mailbox** cmdlet을 실행하여 사서함이 있는지 확인할 수도 있습니다.