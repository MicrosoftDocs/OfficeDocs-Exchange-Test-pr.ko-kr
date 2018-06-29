---
title: '추가 또는 사서함에 대 한 전자 메일 주소를 제거 합니다.: Exchange 2013 Help'
TOCTitle: 추가 또는 사서함에 대 한 전자 메일 주소를 제거 합니다.
ms:assetid: 93e2d9a4-7558-4509-8641-8381a7eb674f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123794(v=EXCHG.150)
ms:contentKeyID: 50556041
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 추가 또는 사서함에 대 한 전자 메일 주소를 제거 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

동일한 사서함에 대 한 개 이상의 전자 메일 주소를 구성할 수 있습니다. 추가 주소에 *프록시 주소*라고 합니다. 프록시 주소에는 다른 전자 메일 주소로 전송 된 전자 메일을 수신 하는 사용자 수 있습니다. 사용자의 프록시 주소로 보내는 모든 전자 메일 메시지는 *기본 SMTP 주소* 또는 *기본 회신 주소*라고도 하는 자신의 기본 전자 메일 주소로 배달 됩니다.


> [!IMPORTANT]
> 비즈니스를 위한 Office 365를 사용 하는 경우이 추가 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=8347775">Office 365 관리 센터: Office 365에서 사용자에 게 추가 전자 메일 별칭 추가</A>



받는 사람 관리와 관련된 추가 관리 작업에 대한 자세한 내용은 [받는 사람](recipients-exchange-2013-help.md) 항목의 "받는 사람 설명서" 표를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

이 항목의 절차에서는 사용자 사서함의 전자 메일 주소를 추가하거나 제거하는 방법을 보여 줍니다. 다른 받는 사람 유형에 대해서도 비슷한 절차에 따라 전자 메일 주소를 추가하거나 제거할 수 있습니다.

## 무슨 작업을 하고 싶으십니까?

## 사용자 사서함에 전자 메일 주소 추가

## EAC를 사용하여 전자 메일 주소 추가

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 전자 메일 주소를 추가할 사서함을 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  사서함 속성 페이지에서 **전자 메일 주소**를 클릭합니다.
    

    > [!NOTE]
    > <STRONG>전자 메일 주소</STRONG> 페이지의 주소 목록에서 기본 SMTP 주소는 굵게 표시되며 <STRONG>유형</STRONG> 열에는 대문자로 된 <STRONG>SMTP</STRONG> 값이 표시됩니다.



4.  **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭한 다음 **SMTP**를 클릭하여 SMTP 전자 메일 주소를 이 사서함에 추가합니다.
    

    > [!NOTE]
    > SMTP는 기본 전자 메일 주소 유형입니다. EUM(Exchange 통합 메시징) 주소나 사용자 지정 주소를 사서함에 추가할 수도 있습니다. 자세한 내용은 <A href="manage-user-mailboxes-exchange-2013-help.md">사용자 사서함 관리</A> 항목의 "사용자 사서함 속성 변경"을 참조하십시오.



5.  **전자 메일 주소** 상자에 새 SMTP 주소를 입력하고 **확인**을 클릭합니다.
    
    선택한 사서함의 전자 메일 주소 목록에 새 주소가 표시됩니다.

6.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용하여 전자 메일 주소 추가

사서함과 연결된 전자 메일 주소는 사서함의 *EmailAddresses* 속성에 포함됩니다. *EmailAddresses* 속성은 전자 메일 주소를 둘 이상 포함할 수 있으므로 *다중값* 속성이라고 합니다. 다음 예에서는 다중값 속성을 수정하는 다양한 방법을 보여 줍니다.

이 예에서는 Dan Jump의 사서함에 SMTP 주소를 추가하는 방법을 보여 줍니다.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com"}

이 예에서는 사서함에 SMTP 주소를 여러 개 추가하는 방법을 보여 줍니다.

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com","danj@tailspintoys.com"}

이런 식으로 다중값 속성의 값을 추가 및 제거하는 방법에 대한 자세한 내용은 [다중값 속성 수정](modifying-multivalued-properties-exchange-2013-help.md) 항목을 참조하십시오.

이 예에서는 사서함과 연결된 모든 주소를 지정하여 사서함에 전자 메일 주소를 추가하는 또 다른 방법을 보여 줍니다. 이 예에서 danj@tailspintoys.com은 새로 추가하려는 전자 메일 주소이고 다른 두 전자 메일 주소는 기존 주소입니다. 대/소문자를 구분하는 한정자 `SMTP`가 포함된 주소는 기본 SMTP 주소입니다. 이 명령 구문을 사용할 때는 사서함의 모든 전자 메일 주소를 포함해야 합니다. 그러지 않으면 명령에 지정된 주소가 기존 주소를 덮어쓰게 됩니다.

    Set-Mailbox "Dan Jump" -EmailAddresses SMTP:dan.jump@contoso.com,dan.jump@northamerica.contoso.com,danj@tailspintoys.com

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

전자 메일 주소가 사서함에 추가되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람** \> **사서함**으로 이동하여 사서함을 클릭한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

  - 사서함 속성 페이지에서 **전자 메일 주소**를 클릭합니다.

  - 사서함의 전자 메일 주소 목록에 새 전자 메일 주소가 포함되어 있는지 확인합니다.

또는

  - 셸에서 다음 명령을 실행합니다.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - 결과에 새 전자 메일 주소가 포함되어 있는지 확인합니다.

## 사용자 사서함에서 전자 메일 주소 제거

## EAC를 사용하여 전자 메일 주소 제거

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 전자 메일 주소를 제거할 사서함을 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  사서함 속성 페이지에서 **전자 메일 주소**를 클릭합니다.

4.  전자 메일 주소 목록에서 제거할 주소를 선택하고 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭합니다.

5.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용하여 전자 메일 주소 제거

이 예에서는 Janet Schorr의 사서함에서 전자 메일 주소를 제거하는 방법을 보여 줍니다.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janets@corp.contoso.com"}

이 예에서는 사서함에서 여러 주소를 제거하는 방법을 보여 줍니다.

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janet.schorr@corp.contoso.com","janets@tailspintoys.com"}

이런 식으로 다중값 속성의 값을 추가 및 제거하는 방법에 대한 자세한 내용은 [다중값 속성 수정](modifying-multivalued-properties-exchange-2013-help.md) 항목을 참조하십시오.

사서함의 전자 메일 주소를 설정할 때 명령에서 특정 전자 메일 주소를 생략하는 방법으로 전자 메일 주소를 제거할 수도 있습니다. 예를 들어 Janet Schorr의 사서함에 janets@contoso.com(기본 SMTP 주소), janets@corp.contoso.com 및 janets@tailspintoys.com이라는 세 개의 전자 메일 주소가 있는 경우 janets@corp.contoso.com 주소를 제거하려면 다음 명령을 실행합니다.

    Set-Mailbox "Janet Schorr" -EmailAddresses SMTP:janets@contoso.com,janets@tailspintoys.com

위 명령에서 janets@corp.contoso.com을 생략했으므로 이 주소가 사서함에서 제거됩니다.

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

전자 메일 주소가 사서함에서 제거되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람** \> **사서함**으로 이동하여 사서함을 클릭한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

  - 사서함 속성 페이지에서 **전자 메일 주소**를 클릭합니다.

  - 사서함의 전자 메일 주소 목록에 전자 메일 주소가 포함되어 있지 않은지 확인합니다.

또는

  - 셸에서 다음 명령을 실행합니다.
    
        Get-Mailbox <identity> | fl EmailAddresses

  - 결과에 전자 메일 주소가 포함되어 있지 않은지 확인합니다.

## 셸을 사용하여 여러 사서함에 전자 메일 주소 추가

셸과 CSV(쉼표로 구분된 값) 파일을 사용하여 한 번에 여러 사서함에 새 전자 메일 주소를 추가할 수 있습니다.

이 예에서는 다음과 같은 형식으로 C:\\Users\\Administrator\\Desktop\\AddEmailAddress.csv에서 데이터를 가져옵니다.

    Mailbox,NewEmailAddress
    Dan Jump,danj@northamerica.contoso.com
    David Pelton,davidp@northamerica.contoso.com
    Kim Akers,kima@northamerica.contoso.com
    Janet Schorr,janets@northamerica.contoso.com
    Jeffrey Zeng,jeffreyz@northamerica.contoso.com
    Spencer Low,spencerl@northamerica.contoso.com
    Toni Poe,tonip@northamerica.contoso.com
    ...

다음 명령을 실행하여 CSV 파일의 데이터로 CSV 파일에 지정된 각 사서함에 전자 메일 주소를 추가합니다.

    Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Set-Mailbox $_.Mailbox -EmailAddresses @{add=$_.NewEmailAddress}}


> [!NOTE]
> 이 CSV 파일의 첫 행에 있는 열 이름(<CODE>Mailbox,NewEmailAddress</CODE>)은 임의적입니다. 어떤 열 이름을 사용하건 간에 셸 명령에서 동일한 열 이름을 사용해야 합니다.



## 작동 여부는 어떻게 확인합니까?

전자 메일 주소가 여러 사서함에 추가되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람** \> **사서함**으로 이동하여 주소를 추가한 사서함을 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

  - 사서함 속성 페이지에서 **전자 메일 주소**를 클릭합니다.

  - 사서함의 전자 메일 주소 목록에 새 전자 메일 주소가 포함되어 있는지 확인합니다.

또는

  - 새 전자 메일 주소를 추가할 때 사용한 것과 동일한 CSV 파일을 사용하여 셸에서 다음 명령을 실행합니다.
    
        Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Get-Mailbox $_.Mailbox | fl Name,EmailAddresses}

  - 각 사서함의 결과에 새 전자 메일 주소가 포함되어 있는지 확인합니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


