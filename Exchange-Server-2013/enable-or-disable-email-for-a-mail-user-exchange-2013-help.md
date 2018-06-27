---
title: '메일 사용자에 대 한 전자 메일을 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 메일 사용자에 대 한 전자 메일을 사용 하지 않도록 설정 하거나 사용
ms:assetid: 1e2571d4-ff84-4fda-bb1d-825e96e1bd26
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996598(v=EXCHG.150)
ms:contentKeyID: 50555956
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 사용자에 대 한 전자 메일을 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-11-14_

Exchange 조직의 기존 메일 사용자가 전자 메일을 사용할 수 없도록 설정할 수 있습니다. 메일 사용자가 전자 메일을 사용할 수 없도록 설정하면 Exchange 및 조직의 주소록에서 해당 전자 메일이 제거됩니다. 메일 사용자가 메일 그룹의 구성원인 경우에는 그룹으로 보내는 메일을 더 이상 받을 수 없습니다. 또한 Active Directory의 사용자 개체에서 Exchange 특성이 제거됩니다. 그러나 사용자 개체 및 Exchange 특성이 아닌 연락처나 조직 정보 등의 특성은 Active Directory에 보존됩니다.

메일 사용자가 전자 메일을 사용할 수 없도록 설정한 후 셸에서 **Enable-MailUser** cmdlet을 사용하여 해당 사용자가 다시 메일 사용이 가능하도록 설정할 수 있습니다. 또한 이 cmdlet을 사용하여 Active Directory 사용자가 메일 사용이 가능하도록 설정할 수도 있습니다.


> [!NOTE]
> 메일 사용자(<EM>메일 사용이 가능한 사용자</EM>라고도 함)는 조직에 사서함이 있는 사용자와는 다릅니다. 근본적인 차이점은 메일 사용자는 외부 전자 메일 주소를 가진 Exchange 조직 외부의 사용자를 나타낸다는 것입니다. 이러한 사용자는 조직에 사서함이 없습니다. 조직에 사서함이 있는 사용자와 메일 사용자의 차이점에 대한 자세한 내용은 <A href="recipients-exchange-2013-help.md">받는 사람</A>을 참조하십시오.



메일 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [메일 사용자 관리](manage-mail-users-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "메일 사용자" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 메일 사용자가 전자 메일을 사용할 수 없도록 설정

앞서 언급한 것처럼 메일 사용자가 전자 메일을 사용할 수 없도록 설정하면 Exchange 특성은 해당 Active Directory 메일 사용자 개체에서 제거되지만 사용자는 보존됩니다. EAC의 메일 사용자 목록에서 메일 사용자를 제거하더라도 Active Directory 사용자 및 컴퓨터를 사용하거나 셸에서 **Get-MailUser** 및 **Set-Set-MailUser** cmdlet을 사용하여 해당 Active Directory 연락처 개체를 보고 관리할 수 있습니다.

## EAC를 사용하여 메일 사용자가 전자 메일을 사용할 수 없도록 설정

1.  EAC에서 **받는 사람** \> **연락처**로 이동합니다.

2.  연락처 목록에서 전자 메일을 사용할 수 없도록 설정할 메일 사용자를 클릭합니다.

3.  **기타** ![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘")를 클릭한 다음 **사용 안 함**을 클릭합니다.

4.  선택한 메일 사용자를 사용하지 않을 것인지 묻는 경고가 표시됩니다. **예**를 클릭하여 사용하지 않도록 설정합니다.

메일 사용자가 연락처 목록에서 제거됩니다.

## 셸을 사용하여 메일 사용자가 전자 메일을 사용할 수 없도록 설정

이 예에서는 메일 사용자 Yan Li가 전자 메일을 사용할 수 없도록 설정합니다.

    Disable-MailUser -Identity "Yan Li"

구문과 매개 변수에 대한 자세한 내용은 [Disable-MailUser](https://technet.microsoft.com/ko-kr/library/aa998578\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

메일 사용자가 전자 메일을 사용할 수 없도록 성공적으로 설정되었는지 확인하려면 다음 중 하나를 수행하십시오.

1.  EAC에서 **받는 사람** \> **연락처**로 이동하고 메일 사용자가 더 이상 목록에 없는지 확인합니다.

2.  Active Directory 사용자 및 컴퓨터에서 사용자를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **일반** 탭에서 **전자 메일** 상자가 비어 있는지 확인합니다. 비어 있으면 메일 사용자가 메일을 사용할 수 없는 것입니다.

3.  셸에서 다음 명령을 실행합니다.
    
        Get-MailUser
    
    이 cmdlet은 메일 사용이 가능한 사용자만 반환하므로 전자 메일을 사용할 수 없도록 설정한 메일 사용자는 결과에 반환되지 않습니다.

4.  셸에서 다음 명령을 실행합니다.
    
        Get-User
    
    이 cmdlet은 모든 Active Directory 사용자 개체를 반환하므로 전자 메일을 사용할 수 없도록 설정한 메일 사용자가 결과에 반환됩니다.

## 셸을 사용하여 사용자가 메일 사용이 가능하도록 설정

**Enable-MailUser** cmdlet을 사용하면 기존 Active Directory 사용자가 메일 사용이 가능하도록 설정할 수 있습니다. 단일 사용자가 메일 사용이 가능하도록 설정하거나, CSV 파일을 사용하여 여러 사용자에 대해 메일 사용이 가능하도록 설정할 수 있습니다.

## 셸을 사용하여 단일 사용자가 메일을 사용할 수 있도록 설정

이 예에서는 사용자 Sanjay Shah가 메일 사용이 가능하도록 설정합니다. 이를 위해서는 외부 전자 메일 주소를 제공해야 합니다.

    Enable-MailUser -Identity "Sanjay Shah" -ExternalEmailAddress renev@tailspintoys.com

## 셸 및 CSV 파일을 사용하여 여러 사용자에 대해 메일 사용이 가능하도록 설정

여러 사용자에 대해 메일 사용이 가능하도록 일괄적으로 설정하는 경우 먼저 메일을 사용할 수 없는 사용자 목록을 CSV(쉼표로 구분된 값 파일)로 내보낸 다음 메모장 같은 텍스트 편집기나 Microsoft Excel 같은 스프레드시트 응용 프로그램을 사용하여 이 CSV 파일에 외부 전자 메일 주소를 추가합니다. 그런 다음 셸 명령에서 업데이트된 CSV 파일을 사용하여 CSV 파일에 있는 사용자가 메일 사용이 가능하도록 설정합니다.

1.  메일을 사용할 수 없거나 조직에 사서함이 없는 기존 사용자 목록을 관리자의 데스크톱에 UsersToMailEnable.csv라는 파일로 내보내려면 다음 명령을 실행합니다.
    
        Get-User | Where { $_.RecipientType -eq "User" } | Out-File "C:\Users\Administrator\Desktop\UsersToMailEnable.csv"
    
    결과 파일은 다음과 같습니다.
    
        Name            RecipientType
        ----            -------------
        Guest           User
        krbtgt          User
        RMS_SERVICE     User
        David Pelton    User
        Kim Akers       User
        Janet Schorr    User
        Jeffrey Zang    User
        Spencer Low     User
        Toni Poe        User
        ...

2.  CSV 파일을 다음과 같이 변경합니다.
    
      - 메일 사용이 가능하지 않도록 할 사용자를 CSV 파일에서 삭제합니다. 예를 들어, 이전 예에서는 기본 시스템 계정인 첫 세 항목을 삭제합니다.
    
      - **RecipientType** 열과 모든 `User` 인스턴스를 삭제합니다.
    
      - **EmailAddress**라는 열 제목을 추가한 다음 파일의 각 사용자에 대해 전자 메일 주소를 추가합니다. 각 사용자의 이름과 외부 주소는 쉼표로 구분해야 합니다.
    
    업데이트된 CSV 파일은 다음과 같습니다.
    
        Name,EmailAddress
        David Pelton,davidp@contoso.com
        Kim Akers,kakers@tailspintoys.com
        Janet Schorr,janet.schorr@adatum.com
        Jeffrey Zang,jzang@tailspintoys.com
        Spencer Low,spencerl@fouthcoffee.com
        Toni Poe,tonip@contoso.com
        ...

3.  CSV 파일의 데이터를 사용하여 파일에 있는 사용자가 메일 사용이 가능하도록 설정하려면 다음 명령을 실행합니다.
    
        Import-CSV "C:\Users\Administrator\Desktop\UsersToMailEnable.csv" | ForEach-Object {Enable-MailUser -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    명령 결과에는 메일 사용이 가능한 새 사용자에 대한 정보가 표시됩니다.

## 작동 여부는 어떻게 확인합니까?

Active Directory 사용자가 메일 사용이 가능하도록 성공적으로 설정되었는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 **받는 사람** \> **연락처**로 이동합니다. 새 메일 사용자가 연락처 목록에 표시됩니다. **연락처 유형**에 유형이 **메일 사용자**로 표시됩니다.
    

    > [!NOTE]
    > 새 메일 사용자를 표시하려면 <STRONG>새로 고침</STRONG><IMG title="새로 고침 아이콘" alt="새로 고침 아이콘" src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif">을 클릭해야 합니다.



  - 셸에서 다음 명령을 실행하여 새 메일 사용자에 대한 정보를 표시합니다.
    
        Get-MailUser | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

