---
title: '삭제 된 사서함을 복원 또는 연결: Exchange 2013 Help'
TOCTitle: 삭제 된 사서함을 복원 또는 연결
ms:assetid: a5e6ac44-5901-4eab-9017-c6fae80a0f83
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ863438(v=EXCHG.150)
ms:contentKeyID: 50556049
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 삭제 된 사서함을 복원 또는 연결

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-05-04_

EAC 또는 셸을 사용하여 Active Directory 사용자 계정에 삭제된 사서함을 연결할 수 있습니다. 사서함을 삭제하면 해당 사서함이 사서함 데이터베이스에 보관되고 비활성 상태로 전환됩니다. 연결된 Active Directory 사용자 계정도 삭제됩니다. 사서함은 삭제된 사서함 보존 기간(기본값은 30일)이 만료될 때까지 보관되었다가 사서함 데이터베이스에서 영구적으로 삭제(또는 *제거*)됩니다.

삭제된 사서함이 Exchange 사서함 데이터베이스에서 영구적으로 삭제되기 전까지는 EAC 또는 셸을 사용하여 사서함을 Active Directory 사용자 계정에 연결할 수 있습니다. 또한 셸을 사용하여 삭제된 사서함의 내용을 기존 사서함으로 복원할 수도 있습니다.

연결이 끊어진 사서함에 대해 자세히 알아보고 관련 관리 작업을 수행하려면 다음 항목을 참조하십시오.

  - [연결이 끊어진 사서함](disconnected-mailboxes-exchange-2013-help.md)

  - [사용 하지 않거나 사서함 삭제](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [비활성화 된 사서함에 연결](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [사서함을 영구적으로 삭제](permanently-delete-a-mailbox-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 삭제된 사서함을 연결할 새 사용자 계정을 Active Directory에 만듭니다. 또는 셸에서 **Get-User** cmdlet을 사용하여 삭제된 사서함을 연결할 Active Directory 사용자 계정이 있으며 이미 다른 사서함에 연결되어 있지는 않은지 확인합니다. 삭제된 사서함을 사용자 계정에 연결하려면 해당 계정이 있어야 하고 *RecipientType* 속성의 값이 `User`여야 합니다. 이 값은 해당 계정이 아직 사서함을 사용하는 계정이 아님을 나타냅니다.
    
    온-프레미스 Exchange 조직의 경우 Active Directory 사용자 및 컴퓨터에서도 이 정보를 확인할 수 있습니다.
    

    > [!IMPORTANT]
    > 연결된 사서함, 리소스 사서함 또는 공유 사서함을 삭제한 후 이러한 삭제된 사서함에 연결할 때는 사서함을 연결하려는 Active Directory 사용자 계정이 비활성 상태여야 합니다.



  - 사용자 계정을 연결할 삭제된 사서함이 사서함 데이터베이스에 있으며 일시 삭제된 사서함이 아닌지 확인하려면 다음 명령을 실행합니다.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    삭제된 사서함이 사서함 데이터베이스에 있고 *DisconnectReason* 속성의 값이 `Disabled`여야 합니다. 사서함이 데이터베이스에서 제거된 경우에는 명령에서 어떤 결과도 반환되지 않습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

  - 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## 무슨 작업을 하고 싶으십니까?

## 삭제된 사서함 연결

삭제된 사서함을 연결할 때는 메일 사용 가능 상태가 아닌 사용자 계정, 즉 기존 사서함이 없는 사용자 계정에 연결합니다. 이미 사서함이 있는 사용자 계정에 삭제된 사서함을 연결하려면 삭제된 사서함을 복원해야 합니다. 자세한 내용은 이 항목 뒷부분의 Restore a deleted mailbox을 참조하십시오.

## EAC를 사용하여 삭제된 사서함 연결

다음 절차에서는 삭제된 사용자 사서함을 사용자 계정에 연결하는 방법을 보여줍니다. 삭제된 사서함이 연결된 사서함, 리소스 사서함 및 공유 사서함인 경우에도 이 절차에 따라 삭제된 사서함을 사용자 계정에 연결할 수 있습니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  **자세히** ![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘")를 클릭하고 **사서함 연결**을 클릭합니다.
    
    Exchange 조직의 선택한 Exchange 서버에서 연결이 끊어진 사서함이 목록으로 표시됩니다.
    

    > [!NOTE]
    > 연결이 끊어진 사서함 목록에는 비활성 사서함, 삭제된 사서함 및 일시 삭제된 사서함이 포함됩니다.



3.  삭제된 사서함 중 사용자를 연결할 사서함을 클릭하고 **연결**을 클릭합니다.

4.  사서함을 연결할지 묻는 창이 표시되면 **예**를 클릭합니다.
    
    메일을 사용할 수 없는 사용자 계정의 목록이 표시됩니다.

5.  삭제된 사서함을 연결할 사용자를 클릭하고 **확인**을 클릭합니다.
    
    삭제된 사서함이 선택한 사용자 계정에 연결됩니다.

## 셸을 사용하여 삭제된 사서함 연결

셸에서 **Connect-Mailbox** cmdlet을 사용하여 메일을 사용할 수 없는 사용자 계정에 삭제된 사서함을 연결할 수 있습니다. 연결하려는 사서함의 유형을 지정해야 합니다. 다음 예에서는 사용자 사서함, 대화방 사서함, 장비 사서함 및 공유 사서함을 다시 연결하기 위한 구문을 보여줍니다. 모든 예에서 선택적 매개 변수인 *Alias*는 전자 메일 주소에서 @ 기호 왼쪽 부분에 해당하는 전자 메일 별칭을 지정하는 데 사용됩니다. *Alias* 매개 변수를 포함하지 않을 경우 *User* 또는 *LinkedMasterAccount* 매개 변수에 지정된 값을 사용하여 다시 연결할 사서함의 전자 메일 주소 별칭이 만들어집니다.


> [!NOTE]
> 앞서 설명한 것처럼 연결된 사서함, 리소스 사서함 또는 공유 사서함을 연결할 때는 사서함을 연결할 Active Directory 사용자 계정이 비활성 상태여야 합니다.



이 예에서는 사용자 사서함을 연결합니다. *Identity* 매개 변수는 MBXDB01이라는 사서함 데이터베이스에 보관된 삭제된 사서함의 표시 이름을 지정합니다. *User* 매개 변수는 사서함을 연결할 Active Directory 사용자 계정을 지정합니다.

    Connect-Mailbox -Identity "Paul Cannon" -Database MBXDB01 -User "Robin Wood" -Alias robinw


> [!NOTE]
> <CODE>LegacyDN</CODE> 또는 <CODE>MailboxGuid</CODE> 속성의 값을 사용하여 삭제된 사서함을 식별할 수도 있습니다.



이 예에서는 연결된 사서함을 연결합니다. *Identity* 매개 변수는 MBXDB02라는 사서함 데이터베이스에 있는 삭제된 사서함을 지정합니다. *LinkedMasterAccount* 매개 변수는 사서함을 연결할 계정 포리스트의 Active Directory 사용자 계정을 지정합니다. *LinkedDomainController* 매개 변수는 계정 포리스트에 있는 도메인 컨트롤러를 지정합니다.

    Connect-Mailbox -Identity "Temp User" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount danpark@fabrikam.com -Alias dpark

이 예에서는 대화방 사서함을 연결합니다.

    Connect-Mailbox -Identity "rm2121" -Database "MBXResourceDB" -User "Conference Room 2121" -Alias ConfRm2121 -Room

이 예에서는 장비 사서함을 연결합니다.

    Connect-Mailbox -Identity "MotorPool01" -Database "MBXResourceDB" -User "Van01 (12 passengers)" -Alias van01 -Equipment

이 예에서는 공유 사서함을 연결합니다.

    Connect-Mailbox -Identity "Printer Support" -Database MBXDB01 -User "Corp Printer Support" -Alias corpprint -Shared


> [!NOTE]
> <CODE>LegacyDN</CODE> 또는 <CODE>MailboxGuid</CODE> 값을 사용하여 삭제된 사서함을 식별할 수도 있습니다.



구문과 매개 변수에 대한 자세한 내용은 [Connect-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997878\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

삭제된 사서함이 사용자 계정에 연결되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람**을 클릭하고 연결한 사서함 유형에 해당하는 페이지로 이동한 다음 **새로 고침**![새로 고침 아이콘](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "새로 고침 아이콘")을 클릭하여 사서함이 나열되는지 확인합니다.

  - Active Directory 사용자 및 컴퓨터에서 사서함을 연결한 사용자 계정을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. **일반** 탭에서 **전자 메일** 상자가 연결된 사서함의 전자 메일 주소로 채워져 있는지 확인합니다.

  - 셸에서 다음 명령을 실행합니다.
    
        Get-User <identity>
    
    *RecipientType* 속성의 **UserMailbox** 값은 사용자 계정과 사서함이 연결되었음을 나타냅니다. **Get-Mailbox \<identity\>** 명령을 실행하여 사서함이 연결되었는지 확인할 수도 있습니다.

## 삭제된 사서함 복원

셸에서 **New-MailboxRestoreRequest** cmdlet을 사용하여 삭제된 사서함을 기존 사서함으로 복원할 수 있습니다. 삭제된 사서함을 복원하면 해당 내용이 기존 사서함, 즉 *대상 사서함*에 복사됩니다. 삭제된 사서함은 복원된 후에도 관리자가 영구적으로 삭제하거나 삭제된 사서함 보존 기간이 만료되어 제거될 때까지 사서함 데이터베이스에 보관됩니다.

사서함 복원 요청이 완료된 후 기본적으로 30일 동안 보관되었다가 제거됩니다. **Remove-StoreMailbox** cmdlet을 사용하여 그 전에 제거할 수도 있습니다.


> [!NOTE]
> EAC를 사용하여 삭제된 사서함을 복원할 수는 없습니다.



## 셸을 사용하여 삭제된 사서함 복원

사서함 복원을 요청하려면 삭제된 사서함의 표시 이름, 레거시 DN(고유 이름) 또는 사서함 GUID를 사용해야 합니다. **Get-MailboxStatistics** cmdlet을 사용하여 복원하려는 삭제된 사서함의 `DisplayName`, `MailboxGuid` 및 `LegacyDN` 속성 값을 표시합니다. 예를 들어 다음 명령을 실행하여 조직의 모든 비활성 사서함 및 삭제된 사서함에 대해 이 정보를 반환합니다.

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "Disabled"} | fl DisplayName,MailboxGuid,LegacyDN,Database

이 예에서는 *SourceStoreMailbox* 매개 변수로 식별되며 MBXDB01 사서함 데이터베이스에 있는 삭제된 사서함을 대상 사서함인 Debra Garcia로 복원합니다. 원본 사서함을 다른 사서함, 즉 레거시 DN 값 동일하지 않은 사서함으로 복원할 수 있도록 *AllowLegacyDNMismatch* 매개 변수가 사용됩니다.

    New-MailboxRestoreRequest -SourceStoreMailbox e4890ee7-79a2-4f94-9569-91e61eac372b -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

이 예에서는 Pilar Pinilla의 삭제된 보관 사서함을 현재 보관 사서함으로 복원합니다. 기본 사서함과 해당 보관 사서함의 레거시 DN이 동일하므로 *AllowLegacyDNMismatch* 매개 변수는 필요하지 않습니다.

    New-MailboxRestoreRequest -SourceStoreMailbox "Personal Archive - Pilar Pinilla" -SourceDatabase "MDB01" -TargetMailbox pilarp@contoso.com -TargetIsArchive

구문과 매개 변수에 대한 자세한 내용은 [New-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829875\(v=exchg.150\))를 참조하십시오.

## 셸을 사용 하 여 삭제 된 공용 폴더 사서함을 복원 하려면

하드 복원 하려는 및 사서함이 삭제 된 항목 보존 제한 내에 있는 공용 폴더 사서함 삭제 한 경우 ( [삭제 된 항목 보존 및 복구 가능한 항목 할당량 구성](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)참조) `Update-StoreMailboxState` cmdlet은 앞에 오는 `Connect-Mailbox` cmdlet을 사용할 수 있습니다. 자세한 구문 및 매개 변수 정보에 대 한 [Connect-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997878\(v=exchg.150\)) 및 [Update-StoreMailboxState](https://technet.microsoft.com/ko-kr/library/jj860462\(v=exchg.150\))를 참조 하십시오.

공용 폴더 사서함을 포함 하는 사서함 데이터베이스의 이름 또는 삭제 된 공용 폴더 사서함으로 GUID의 GUID를 만들어야 합니다. 이 정보를 설치 하지 않은 경우 다음 단계를 수행 수 있습니다.

1.  다음 cmdlet를 실행 하 여 Active Directory 포리스트 및 도메인 컨트롤러의 정규화 된 도메인 이름을 (FQDN)을 가져옵니다.
    
        Get-OrganizationConfig | fl OriginatingServer

2.  1 단계에서 반환 되는 정보를 사용 하 고 삭제 된 공용 폴더 사서함에 포함 된 사서함 데이터베이스의 이름 또는 GUID에 대 한 공용 폴더 사서함의 GUID에 대 한 Deleted Objects 컨테이너 Active Directory에서 검색 합니다.
    

    > [!TIP]
    > 사용자 지정 스크립트를 사용 하 여 삭제 된 개체를 검색할 수 또는 Powershell 프롬프트에 <STRONG>ldp.exe</STRONG> 를 입력 하 여 열 수 있는 Ldp 유틸리티를 사용 하 여 합니다.



삭제 된 공용 폴더 사서함 GUID를 알고 있는 시점과 이름 또는 GUID는 사서함의 데이터베이스는 공용 폴더 사서함을 복원 하려면 다음 명령을 실행 하는 공용 폴더 사서함을 포함 합니다.

1.  (수 하 라는 메시지가 적절 한 자격 증명을 제공)에서 다음 명령을 실행 하 여 새 Active Directory 개체를 만듭니다.
    
        New-MailUser <mailUserName> -ExternalEmailAddress <emailAddress> 
        
        Get-MailUser <mailUserName> | Disable-MailUser
    
    `<mailUserName>`, `<emailAddress>`및 `<mailUserName>` 는 값에 다음을 수행 하려는 합니다. 다음 단계에서 동일한 `<mailUserName>` 값을 사용 해야 합니다.

2.  다음 명령을 실행 하 여 방금 만든 Active Directory 개체를 삭제 된 공용 폴더 사서함을 연결 합니다.
    
        Connect-Mailbox -Identity <public folder mailbox GUID> -Database <database name or GUID> -User <mailUserName>
    

    > [!NOTE]
    > <CODE>Identity</CODE> 매개 변수는 Active Directory 사용자 개체에 연결 하는 Exchange 데이터베이스에서 사서함 개체를 지정 합니다. 위의 예제에서는 공용 폴더 사서함에 대 한 GUID를 지정 하지만 표시 이름 값 이나 LegacyExchangeDN 값을 사용할 수도 있습니다.



3.  다음 예제에 따라 공용 폴더 사서함에서 `Update-StoreMailboxState` 를 실행 합니다.
    
        Update-StoreMailboxState -Identity <public folder mailbox GUID> -Database <database name or GUID>
    
    2 단계와 같이 `Identity` 매개 변수는 GUID, 표시 이름 또는 공용 폴더 사서함에 대 한 LegacyExchangeDN 값을 수락 합니다.

## 작동 여부는 어떻게 확인합니까?

삭제 된 공용 폴더 사서함을 성공적으로 복원 했는지를 확인 하려면 **Get-PublicFolder -GetChildren -\<public folder mailbox GUID\>** cmdlet을 실행 합니다. 복원에 성공 하면이 cmdlet이 작동할 수 있습니다.

자세한 내용은 다음 항목을 참조하십시오.

  - [Connect-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997878\(v=exchg.150\))

  - [Update-StoreMailboxState](https://technet.microsoft.com/ko-kr/library/jj860462\(v=exchg.150\))

