---
title: '메일 연락처에 대 한 전자 메일을 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 메일 연락처에 대 한 전자 메일을 사용 하지 않도록 설정 하거나 사용
ms:assetid: ca47441f-1aa4-4958-aba5-18d51e59837e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124552(v=EXCHG.150)
ms:contentKeyID: 50556085
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 연락처에 대 한 전자 메일을 사용 하지 않도록 설정 하거나 사용

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2012-12-05_

Exchange 조직의 기존 메일 연락처에 대해 전자 메일을 사용하지 않도록 설정할 수 있습니다. 메일 연락처에 대해 전자 메일을 사용하지 않도록 설정하면 메일 연락처가 Exchange 및 조직의 주소록에서 제거됩니다. 메일 연락처가 메일 그룹의 구성원일 경우 해당 연락처는 이제 메일 그룹으로 전송되는 메일을 수신하지 않습니다. 또한, Exchange 특성은 Active Directory의 메일 사용 가능 연락처 개체에서 제거되지만 연락처 및 Exchange 이외의 특성(예: 연락처 정보 및 조직 정보)은 Active Directory에 유지됩니다.

메일 연락처에 대한 전자 메일을 사용하지 않도록 설정한 후에는 셸에서 <strong>Enable-MailContact</strong> cmdlet을 사용하여 해당 메일 연락처를 메일 사용 가능한 상태로 되돌릴 수 있습니다. 이 cmdlet을 사용하면 어떠한 Active Directory 연락처도 메일 사용 가능한 상태로 만들 수 있습니다.

메일 연락처와 관련된 추가 관리 작업에 대한 자세한 내용은 [메일 연락처 관리](manage-mail-contacts-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "메일 연락처" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 메일 연락처에 대해 전자 메일을 사용하지 않도록 설정

앞서 설명한 것처럼 메일 연락처에 대해 전자 메일을 사용하지 않도록 설정하면 Exchange 특성이 해당 Active Directory 연락처 개체에서 제거되지만 연락처는 유지됩니다. 메일 연락처는 EAC의 메일 연락처 목록에서 제거되지만 Active Directory 사용자 및 컴퓨터를 사용하거나 셸에서 <strong>Get-Contact</strong> 및 <strong>Set-Contact</strong> cmdlet을 사용하면 해당 Active Directory 연락처 개체를 보고 관리할 수 있습니다.

## EAC를 사용하여 메일 연락처에 대한 전자 메일을 사용하지 않도록 설정

1.  EAC에서 <strong>받는 사람</strong> \> <strong>연락처</strong>로 이동합니다.

2.  연락처 목록에서 전자 메일을 사용하지 않도록 설정할 메일 연락처를 클릭합니다.

3.  <strong>자세히</strong> ![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘")를 클릭한 후 <strong>사용 안 함</strong>을 클릭합니다.

4.  선택한 메일 연락처를 사용하지 않도록 설정할 것인지 묻는 경고 메시지가 나타납니다. <strong>예</strong>를 클릭하여 사용하지 않도록 설정합니다.

메일 연락처가 연락처 목록에서 제거됩니다.

## 셸을 사용하여 메일 연락처에 대한 전자 메일을 사용하지 않도록 설정

이 예에서는 메일 연락처 Neil Black에 대한 전자 메일을 사용하지 않도록 설정합니다.

    Disable-MailContact -Identity "Neil Black"

구문과 매개 변수에 대한 자세한 내용은 [Disable-MailContact](https://technet.microsoft.com/ko-kr/library/aa997465\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

메일 연락처에 대한 전자 메일을 사용하지 않도록 설정했는지 확인하려면 다음 중 하나를 수행합니다.

1.  EAC에서 <strong>받는 사람</strong> \> <strong>연락처</strong>로 이동한 후 해당 메일 연락처가 목록에서 제거되었는지 확인합니다.

2.  Active Directory 사용자 및 컴퓨터에서 연락처를 마우스 오른쪽 단추로 클릭한 후 <strong>속성</strong>을 클릭합니다. <strong>일반</strong> 탭에서 <strong>전자 메일</strong> 상자가 비어있는지 확인합니다. 비어있으면 연락처가 메일 사용 가능한 상태가 아닙니다.

3.  셸에서 다음 명령을 실행합니다.
    
        Get-MailContact
    
    이 cmdlet은 메일 사용 가능한 연락처만 반환하므로 전자 메일을 사용하지 않도록 설정한 연락처는 결과에 반환되지 않습니다.

4.  셸에서 다음 명령을 실행합니다.
    
        Get-Contact
    
    이 cmdlet은 모든 Active Directory 연락처 개체를 반환하므로 전자 메일을 사용하지 않도록 설정한 연락처가 결과에 반환됩니다.

## 셸을 사용하여 연락처를 메일 사용 가능 상태로 설정

<strong>Enable-MailContact</strong> cmdlet을 사용하여 기존 Active Directory 연락처를 메일 사용 가능한 상태로 설정할 수 있습니다. 단일 연락처를 메일 사용 가능하도록 설정하거나 CSV 파일을 사용하여 여러 연락처를 메일 사용 가능하도록 설정할 수 있습니다.

## 셸을 사용하여 단일 연락처를 메일 사용 가능 상태로 설정

이 예에서는 연락처 Rene Valdes를 메일 사용 가능한 상태로 설정합니다. 외부 전자 메일 주소를 제공해야 합니다.

    Enable-MailContact -Identity "Rene Valdes" -ExternalEmailAddress renev@tailspintoys.com

## 셸 및 CSV 파일을 사용하여 여러 개의 연락처를 메일 사용 가능 상태로 설정

여러 개의 연락처를 메일 사용 가능 상태로 설정하려면 먼저 메일 사용 가능 상태가 아닌 연락처의 목록을 CSV(쉼표로 구분된 값) 파일로 내보낸 후 메모장 같은 텍스트 편집기나 Microsoft Excel 같은 스프레드시트 응용 프로그램을 사용하여 외부 전자 메일 주소를 추가해야 합니다. 그런 다음 셸 명령에 업데이트된 CSV 파일을 사용해 CSV 파일에 나열된 연락처를 메일 사용 가능한 상태로 설정합니다.

1.  다음 명령을 실행하여 메일 사용 가능 상태가 아닌 기존 연락처의 목록을 관리자 데스크톱의 Contacts.csv로 내보냅니다.
    
        Get-Contact | Where { $_.RecipientType -eq "Contact" } | Out-File "C:\Users\Administrator\Desktop\Contacts.csv"
    
    결과 파일은 다음 파일과 유사합니다.
    
        Name
        Walter Harp
        James Alvord
        Rainer Witt
        Susan Burk
        Ian Tien
        ...

2.  이름이 <strong>EmailAddress</strong>인 열 제목을 추가한 후 파일에서 각 연락처에 대한 전자 메일 주소를 추가합니다. 각 연락처에 대한 이름과 외부 전자 메일 주소는 쉼표로 구분해야 합니다. 업데이트된 CSV 파일은 다음 파일과 유사합니다.
    
        Name,EmailAddress
        James Alvord,james@contoso.com
        Susan Burk,sburk@tailspintoys.com
        Walter Harp,wharp@tailspintoys.com
        Ian Tien,iant@tailspintoys.com
        Rainer Witt,rainerw@fourthcoffee.com
        ...

3.  다음 명령을 실행하여 CSV 파일의 데이터를 사용해 파일 내 나열된 연락처를 메일 사용 가능한 상태로 설정합니다.
    
        Import-CSV C:\Users\Administrator\Desktop\Contacts.csv | ForEach-Object {Enable-MailContact -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    메일 사용 가능한 상태로 설정된 새 연락처의 정보가 명령 결과에 표시됩니다.

## 작동 여부는 어떻게 확인합니까?

Active Directory 연락처가 성공적으로 메일 사용 가능한 상태로 설정되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 <strong>받는 사람</strong> \> <strong>연락처</strong>로 이동합니다. 새 메일 연락처가 연락처 목록에 표시됩니다. <strong>연락처 유형</strong>에서는 유형이 <strong>메일 연락처</strong>로 표시됩니다.
    

    > [!NOTE]
    > 새 메일 연락처를 표시하려면 <STRONG>새로 고침</STRONG><IMG title="새로 고침 아이콘" alt="새로 고침 아이콘" src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif">을 클릭해야 할 수 있습니다.



  - 셸에서 다음 명령을 실행하여 새 메일 연락처에 대한 정보를 표시합니다.
    
        Get-MailContact | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

