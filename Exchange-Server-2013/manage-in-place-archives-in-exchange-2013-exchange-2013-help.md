---
title: 'Exchange 2013에서 원본 위치 보관 관리: Exchange 2013 Help'
TOCTitle: Exchange 2013에서 원본 위치 보관 관리
ms:assetid: 49ef4a3e-d209-4fb2-80a3-6132b0f69bd0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ651146(v=EXCHG.150)
ms:contentKeyID: 50483039
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013에서 원본 위치 보관 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-02-01_

원본 위치 보관 개인 저장소 (.pst) 파일에 대 한 필요성을 제거 하 고 조직의 메시지 보존 및 eDiscovery 요구 사항을 충족할 수 있도록 하 여 조직의 메시징 데이터의 제어를 잠금을 해제 하는데 도움이 됩니다. 보관 활성화, 사용자가 MicrosoftOutlook 및 Outlook Web App 를 사용 하 여 액세스할 수 있는 보관 사서함에 있는 메시지를 저장할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "원본 위치 보관함" 항목

  - 사용자의 기본 사서함 사용자의 보관 보다 이전 Exchange 버전에는 지원 되지 않습니다. Exchange 2010에서 여전히 사용자의 기본 사서함이 있는 경우 Exchange 2013으로 보관 사서함을 이동 하는 동시에 Exchange 2013으로 이동 해야 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 사서함을 만들고 온-프레미스 보관 사서함 사용

## EAC를 사용하여 다음을 수행합니다.

1.  **받는 사람** \> **사서함**으로 이동합니다.

2.  **새로 만들기** \> **사용자 사서함**을 클릭합니다.

3.  **새 사용자 사서함** 페이지의 **별칭** 텍스트 상자에 사용자의 별칭을 입력합니다.
    

    > [!NOTE]
    > 이 텍스트 상자를 비워 두면 <STRONG>사용자 로그온 이름</STRONG> 텍스트 상자에 입력한 값이 별칭에 사용됩니다.



4.  
    
    다음 옵션 중 하나를 선택합니다.
    
      - **기존 사용자**   **사용자 선택 – 전체 포리스트** 대화 상자를 열려면 이 단추를 클릭한 후 **찾아보기**를 클릭합니다. 이 대화 상자에는 메일을 사용할 수 없거나 Exchange 사서함이 없는 포리스트의 Active Directory 사용자 계정 목록이 표시됩니다. 메일을 사용할 수 있도록 설정할 사용자 계정을 선택하고 **확인**을 클릭합니다. 이 옵션을 선택할 경우 사용자 계정 정보가 Active Directory에도 있으므로 이 정보를 제공할 필요가 없습니다.
    
      - **새 사용자**   Active Directory에서 새 사용자 계정을 만들고 이 사용자의 사서함을 만들려면 이 단추를 클릭합니다. 이 옵션을 선택하면 필요한 사용자 계정 정보를 제공해야 합니다.
    

    > [!NOTE]
    > 사용자 사서함에 연결된 Active Directory&nbsp;계정은 Exchange&nbsp;서버와 동일한 포리스트에 있어야 합니다. 신뢰할 수 있는 포리스트에 있는 사용자 계정의 사서함을 만들려면 연결된 사서함을 만들어야 합니다. 자세한 내용은 <A href="manage-linked-mailboxes-exchange-2013-help.md">연결 된 사서함 관리</A>를 참조하십시오.



5.  
    
    **기타 옵션**을 클릭하여 다음 설정을 구성합니다.
    
      - **사서함 데이터베이스**   **찾아보기**를 클릭하여 사서함을 저장할 사서함 데이터베이스를 선택합니다. 데이터베이스를 선택하지 않으면 Exchange에서 자동으로 데이터베이스를 할당합니다.
    
      - **보관**   사서함의 보관 사서함을 만들려면 이 확인란을 선택합니다. 보관 사서함을 만들면 기본 보존 정책 설정이나 정의한 설정에 따라 기본 사서함에서 보관 사서함으로 사서함 항목이 자동으로 이동합니다.
        
        **찾아보기**를 클릭하여 보관 사서함을 저장할 로컬 포리스트의 데이터베이스를 선택합니다.
        
        자세한 내용은 [전체에서 Exchange 2013의 보관](in-place-archiving-in-exchange-2013-exchange-2013-help.md)을 참조하십시오.
    
      - **주소록 정책**   사서함에 대한 ABP(주소록 정책)를 선택하려면 이 목록을 사용합니다. ABP에는 GAL(전체 주소 목록), OAB(오프라인 주소록), 방 목록 및 일련의 주소 목록이 들어 있습니다. 사서함 사용자에게 할당되면 ABP는 할당된 사용자에게 Outlook 및 Outlook Web App의 사용자 지정된 GAL에 대한 액세스 권한을 제공합니다. 자세한 내용은 [주소록 정책](address-book-policies-exchange-2013-help.md)를 참조하십시오.

6.  
    
    작업이 끝나면 **저장**을 클릭하여 사서함을 만듭니다.

## 셸 사용

이 예에서는 Active Directory에 Chris Ashton이라는 사용자를 만들고 사서함 데이터베이스 DB01에 사서함을 만든 다음 보관함을 사용하도록 설정합니다. 다음 로그온할 때 암호를 다시 설정해야 합니다. 초기 암호 값을 설정하기 위해 이 예에서는 변수($password)를 만들고, 암호를 입력하라는 메시지를 표시하고, SecureString 개체로 변수에 해당 암호를 할당합니다.

    $password = Read-Host "Enter password" -AsSecureString
    New-Mailbox -UserPrincipalName chris@contoso.com -Alias chris -Archive -Database "DB01" -Name ChrisAshton -OrganizationalUnit Users -Password $password -FirstName Chris -LastName Ashton -DisplayName "Chris Ashton" 

구문과 매개 변수에 대한 자세한 내용은 [New-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997663\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

온-프레미스 보관 사서함이 있는 사용자 사서함이 만들어졌는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람** \> **사서함**으로 이동한 다음 목록에서 새 사용자 사서함을 선택합니다. 세부 정보 창의 **원본 위치 보관함**이 **사용**으로 설정되어 있는지 확인합니다. **세부 정보 보기**를 클릭하여 보관 상태와 보관이 만들어진 사서함 데이터베이스를 포함하는 보관 속성을 확인합니다.

  - 셸에서 다음 명령을 실행하여 새 사용자 사서함 및 보관함에 대한 정보를 표시합니다.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress,*Archive*

  - 셸에서 **Test-ArchiveConnectivity** cmdlet을 사용하여 보관함에 대한 연결을 테스트합니다. 보관함 연결 테스트 방법의 예를 보려면 [Test-ArchiveConnectivity](https://technet.microsoft.com/ko-kr/library/hh529914\(v=exchg.150\))의 예 섹션을 참조하십시오.

## 기존 사서함에 온-프레미스 보관 사서함 사용

사서함이 있지만 보관함을 사용하지 않도록 설정한 기존 사용자에 대한 보관함을 만들 수도 있습니다. 이러한 작업을 기존 사서함에 대한 *보관함 사용*이라고 합니다.

## EAC를 사용하여 다음을 수행합니다.

1.  **받는 사람** \> **사서함**으로 이동합니다.

2.  사서함을 선택합니다.

3.  세부 정보 창의 **원본 위치 보관함**에서 **사용**을 클릭합니다.
    

    > [!TIP]
    > Shift 또는 Ctrl 키를 사용해 여러 사서함을 선택하여 보관함을 대량으로 사용하도록 설정할 수도 있습니다. 여러 사서함을 선택한 후 세부 정보 창에서 <STRONG>기타 옵션</STRONG>을 클릭합니다. 그런 후에 <STRONG>보관함</STRONG>에서 <STRONG>사용</STRONG>을 클릭합니다.



4.  **원본 위치 보관함 만들기** 페이지에서 **확인**을 클릭하여 Exchange에서 보관함에 대한 사서함 데이터베이스를 자동으로 선택하도록 하거나 **찾아보기**를 클릭하여 데이터베이스를 지정합니다.

## 셸 사용

이 예에서는 Tony Smith의 사서함에 대해 보관함을 사용하도록 설정합니다.

    Enable-Mailbox "Tony Smith" -Archive

이 예에서는 DB01 데이터베이스에서 온-프레미스 또는 클라우드 기반 보관함이 사용하도록 설정되어 있지 않고 이름이 DiscoverySearchMailbox로 시작하지 않는 사서함을 검색합니다. 결과를 **Enable-Mailbox** cmdlet으로 파이프하여 사서함 데이터베이스 DB01의 모든 사서함에 대한 보관함을 사용하도록 설정합니다.

    Get-Mailbox -Database DB01 -Filter {ArchiveGuid -Eq $null -AND ArchiveDomain -eq $null -AND Name -NotLike "DiscoverySearchMailbox*"} | Enable-Mailbox -Archive

구문과 매개 변수에 대한 자세한 내용은 [Enable-Mailbox](https://technet.microsoft.com/ko-kr/library/aa998251\(v=exchg.150\)) 및 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

기존 사서함에 대해 온-프레미스 보관 사서함을 사용하도록 설정되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람** \> **사서함**으로 이동하여 목록에서 사서함을 선택합니다. 세부 정보 창의 **원본 위치 보관함**이 **사용**으로 설정되어 있는지 확인합니다. **세부 정보 보기**를 클릭하여 보관 상태와 보관이 만들어진 사서함 데이터베이스를 포함하는 보관 속성을 확인합니다.

  - 셸에서 다음 명령을 실행하여 새 보관함에 대한 정보를 표시합니다.
    
        Get-Mailbox <Name> | FL Name,*Archive*

  - 셸에서 **Test-ArchiveConnectivity** cmdlet을 사용하여 보관함에 대한 연결을 테스트합니다. 보관 연결 테스트 방법의 예제를 보려면 [Test-ArchiveConnectivity](https://technet.microsoft.com/ko-kr/library/hh529914\(v=exchg.150\))의 예제를 참조하십시오.

## 온-프레미스 보관 사서함을 사용하지 않도록 설정

문제 해결을 위해서나 또는 원본 보관함을 지원하지 않는 Exchange 버전으로 사서함을 이동할 경우 사용자의 보관함을 사용하지 않도록 설정할 수 있습니다. 온-프레미스 보관 사서함을 사용하지 않도록 설정하면 보관함에 있는 모든 정보는 사서함 보존 기간이 지나 보관함이 영구적으로 삭제될 때까지 사서함 데이터베이스에 보관됩니다. 기본적으로 Exchange 에서는 보관 사서함을 포함해 연결이 끊어진 사서함을 30일 동안 보관합니다.


> [!IMPORTANT]
> 보관함을 사용하지 않도록 설정하면 사서함에서 보관함이 제거되고 사서함 데이터베이스에서 삭제하도록 표시됩니다.



온-프레미스 보관함을 해당 사서함에 다시 연결하려면 [Connect-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997878\(v=exchg.150\)) cmdlet을 *Archive* 매개 변수와 함께 사용합니다.

## EAC를 사용하여 다음을 수행합니다.

1.  **받는 사람** \> **사서함**으로 이동합니다.

2.  사서함을 선택합니다.

3.  세부 정보 창의 **원본 위치 보관함**에서 **사용 안 함**을 클릭합니다.
    

    > [!TIP]
    > Shift 또는 Ctrl 키를 사용해 여러 사서함을 선택하여 보관함을 대량으로 사용하지 않도록 설정할 수도 있습니다. 여러 사서함을 선택한 후 세부 정보 창에서 <STRONG>기타 옵션</STRONG>을 클릭합니다. 그런 후에 <STRONG>보관함</STRONG>에서 <STRONG>사용 안 함</STRONG>을 클릭합니다.



## 셸 사용

이 예에서는 Chris Ashton의 사서함에 대해 보관함을 사용하지 않도록 설정합니다. 사서함을 사용하지 않도록 설정하지는 않습니다.

    Disable-Mailbox -Identity "Chris Ashton" -Archive

구문과 매개 변수에 대한 자세한 내용은 [Disable-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997210\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

보관함이 사용하지 않도록 설정되었는지 확인하려면 다음을 수행합니다.

  - EAC에서 사서함을 선택합니다. 그런 다음 세부 정보 창의 **원본 위치 보관함**에서 보관 상태를 확인합니다.

  - 셸에서 다음 명령을 실행하여 사서함 사용자의 보관 속성을 확인합니다.
    
        Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*
    
    보관함이 사용하지 않도록 설정된 경우 보관 관련 속성에 대해 다음 값이 반환됩니다.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>속성</th>
    <th>값</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ArchiveDatabase(온-프레미스 보관 사서함의 경우)</p></td>
    <td><p>&lt;공백&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>ArchiveState</p></td>
    <td><p><code>None</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>DisabledArchiveDatabase(온-프레미스 보관 사서함의 경우)</p></td>
    <td><p>&lt;사서함 데이터베이스 이름&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>DisabledArchiveGuid</p></td>
    <td><p>&lt;사용하지 않도록 설정된 보관함의 GUID&gt;</p></td>
    </tr>
    </tbody>
    </table>


## 온-프레미스 보관 사서함 연결

보관 사서함을 사용하지 않도록 설정하면 해당 보관 사서함의 연결이 끊어집니다. 연결이 끊어진 보관 사서함은 지정된 기간 동안 사서함 데이터베이스에 보존됩니다. 기본적으로 Exchange에서는 연결이 끊어진 보관함을 30일 동안 보존합니다. 이 기간 동안에는 보관함을 기존 사서함에 연결하여 복구할 수 있습니다. 삭제된 사서함 보존 기간을 수정하여 삭제된 사서함이나 보관함을 보존하는 기간을 늘리거나 줄일 수 있습니다.


> [!WARNING]
> 사용자의 보관함을 사용하지 않도록 설정한 다음 동일한 사용자의 보관함을 사용하도록 설정하면 새 보관함이 만들어집니다. 새 보관함에는 사용자의 연결이 끊어진 보관함에 있던 데이터가 포함되지 않습니다. 사용자를 연결이 끊어진 해당 보관함에 다시 연결하려면 다음 절차를 사용해야 합니다.




> [!NOTE]
> 연결이 끊어진 보관함을 사서함 사용자에 연결하는 데 EAC를 사용할 수 없습니다.



## 셸 사용

1.  보관함의 이름을 모르는 경우 셸에서 다음 명령을 실행하여 이름을 확인할 수 있습니다. 이 예에서는 사서함 데이터베이스 DB01을 검색하고 이 데이터베이스를 **Get-MailboxStatistics** cmdlet으로 파이프하여 데이터베이스의 모든 사서함에 대한 사서함 통계를 검색한 후 **Where-Object** cmdlet을 사용하여 결과를 필터링한 다음 연결이 끊어진 보관함의 목록을 검색합니다. 이 명령은 GUID 및 항목 수와 같은 각 보관함에 대한 추가 정보를 표시합니다.
    
        Get-MailboxDatabase "DB01" | Get-MailboxStatistics | Where {($_.DisconnectDate -ne $null) -and ($_.IsArchiveMailbox -eq $true)} | Format-List

2.  보관함을 기본 사서함에 연결합니다. 이 예에서는 Chris Ashton의 보관함을 Chris Ashton의 기본 사서함에 연결하고 GUID를 보관함의 ID로 사용합니다.
    
        Enable-Mailbox -ArchiveGuid "8734c04e-981e-4ccf-a547-1c1ac7ebf3e2" -ArchiveDatabase "DB01" -Identity "Chris Ashton"

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Get-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb124924\(v=exchg.150\))

  - [Get-MailboxStatistics](https://technet.microsoft.com/ko-kr/library/bb124612\(v=exchg.150\))

  - [Enable-Mailbox](https://technet.microsoft.com/ko-kr/library/aa998251\(v=exchg.150\))

## 작동 여부는 어떻게 확인합니까?

연결이 끊어진 보관함이 사서함 사용자에게 연결되었는지 확인하려면 다음 셸 명령을 사용하여 사서함 사용자의 보관함 속성을 검색하고 *ArchiveGuid* 및 *ArchiveDatabase* 속성에 대해 반환된 값을 확인합니다.

    Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*

