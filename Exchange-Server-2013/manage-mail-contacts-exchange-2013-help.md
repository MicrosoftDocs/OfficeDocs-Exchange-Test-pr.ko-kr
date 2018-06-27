---
title: '메일 연락처 관리: Exchange 2013 Help'
TOCTitle: 메일 연락처 관리
ms:assetid: 74c72aed-e9ff-4927-8eb7-c08a86e79ae0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998858(v=EXCHG.150)
ms:contentKeyID: 50482250
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailContactWizardForm.NewMailContactIntroductionWizardPage
ms.translationtype: MT
---

# 메일 연락처 관리

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-10-04_

메일 연락처는 Exchange 또는 Exchange Online 조직의 외부 사람 또는 외부 조직에 대한 정보를 포함하는 메일 사용이 가능한 디렉터리 서비스 개체입니다. 각 메일 연락처에는 외부 전자 메일 주소가 있습니다. 메일 연락처에 대한 자세한 내용은 [받는 사람](recipients-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 메일 연락처 만들기

## EAC를 사용하여 메일 연락처 만들기

1.  EAC에서 **받는 사람** \> **연락처**로 이동합니다.

2.  **새로 만들기** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") \> **메일 연락처**를 클릭합니다.

3.  **새 메일 연락처** 페이지의 다음 상자에 값을 지정합니다.
    
      - **이름**   이 상자에 연락처의 이름을 입력합니다.
    
      - **이니셜**   이 상자에 연락처의 이니셜을 입력합니다.
    
      - **성**   이 상자에 연락처의 성을 입력합니다.
    
      - **\* 표시 이름**   이 상자를 사용하여 연락처의 표시 이름을 입력합니다. EAC의 연락처 목록 및 조직의 주소록에 표시되는 이름입니다. 기본적으로 이 상자에는 **이름**, **이니셜** 및 **성** 상자에 입력한 이름이 채워집니다. 해당 입력란을 사용하지 않은 경우에도 이 입력란은 필수이므로 이름을 입력해야 합니다. 이름은 64자를 초과할 수 없습니다.
    
      - **\* 이름**   이 상자를 사용하여 연락처의 이름을 입력합니다. 이 이름은 디렉터리 서비스에 나열된 이름입니다. 표시 이름과 마찬가지로 이 상자에는 기본적으로 **이름**, **이니셜** 및 **성** 상자에 입력한 이름이 채워집니다. 해당 입력란을 사용하지 않은 경우에도 이 입력란은 필수이므로 이름을 입력해야 합니다. 이름은 64자를 초과할 수 없습니다.
    
      - **\* 별칭** 이 상자를 사용 하 여 별칭을 입력 (64 자 이하의) 대화 상대에 대 한 합니다. 이 상자는 필요 합니다.
    
      - **\* 외부 전자 메일 주소**   이 상자를 사용하여 연락처의 외부 전자 메일 계정을 입력합니다. 이 입력란은 필수입니다. 이 연락처로 보낸 전자 메일은 이 전자 메일 주소로 전달됩니다.
    
      - **조직 구성 단위**   기본값(받는 사람 범위) 이외의 OU(조직 구성 단위)를 선택할 수 있습니다. 받는 사람 범위가 포리스트로 설정되어 있으면 기본값은 EAC를 실행 중인 컴퓨터가 포함된 도메인의 사용자 컨테이너로 설정됩니다. 받는 사람 범위가 특정 도메인으로 설정되어 있으면 해당 도메인의 사용자 컨테이너가 기본적으로 선택됩니다. 받는 사람 범위가 특정 OU로 설정되어 있으면 해당 OU가 기본적으로 선택됩니다.
        
        다른 OU를 선택하려면 **찾아보기**를 클릭합니다. 이 대화 상자에는 지정된 범위 내에 있는 포리스트의 모든 OU가 표시됩니다. 원하는 OU를 선택한 다음 **확인**을 클릭합니다.
        

        > [!NOTE]
        > <STRONG>조직 구성 단위</STRONG> 상자는 Exchange Server 2013에서만 사용할 수 있습니다. Exchange Online에서는 사용할 수 없습니다.



4.  작업을 마친 후 **저장**을 클릭합니다.

## 셸을 사용하여 메일 연락처 만들기

이 예에서는 Exchange Server 2013에서 Debra Garcia의 메일 연락처를 만듭니다.

    New-MailContact -Name "Debra Garcia" -ExternalEmailAddress dgarcia@tailspintoys.com -OrganizationalUnit Users

이 예에서는 Exchange Online에서 Alan Shen의 메일 연락처를 만듭니다.

    New-MailContact -Name "Alan Shen" -ExternalEmailAddress alans@fourthcoffee.com

이 예에서는 Exchange Server 2013에서 Karen Toh라는 기존 연락처가 메일을 사용할 수 있도록 설정합니다.

    Enable-MailContact -Identity "Karen Toh" -ExternalEmailAddress ktoh@tailspintoys.com

## 작동 여부는 어떻게 확인합니까?

메일 연락처가 만들어졌는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람** \> **연락처**로 이동합니다. 새 메일 연락처는 연락처 목록에 표시됩니다. **연락처 유형**에서는 유형이 **메일 연락처**로 표시됩니다.

  - 셸에서 다음 명령을 실행하여 새 메일 연락처에 대한 정보를 표시합니다.
    
        Get-MailContact <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## 메일 연락처 속성 변경

## EAC를 사용하여 메일 연락처 속성 변경

1.  EAC에서 **받는 사람** \> **연락처**로 이동합니다.

2.  메일 연락처 및 메일 사용자 목록에서 속성을 변경하려는 메일 연락처를 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  메일 연락처 속성 페이지에서 다음 섹션 중 하나를 클릭하여 속성을 보거나 변경합니다.
    
      - General
    
      - Contact Information
    
      - Organization
    
      - Email Options(Exchange Online에서 사용할 수 없음)
    
      - MailTip

## 일반

메일 연락처에 대한 기본 정보를 보거나 변경하려면 **일반** 섹션을 사용합니다.

  - **이름**, **이니셜**, **성**

  - **\* 이름**   Active Directory에 표시되는 이름입니다. 이 이름을 변경하는 경우 64자를 초과할 수 없습니다.

  - **\* 표시 이름**   이 이름은 조직의 주소록, 전자 메일의 받는 사람 및 보낸 사람 줄, 사서함 목록에 표시됩니다. 표시 이름 앞뒤에는 빈 공간을 포함할 수 없습니다.

  - **\* 별칭**   메일 연락처의 별칭입니다. 별칭을 변경할 경우 조직에서 고유한 64자 이하의 별칭을 사용해야 합니다.

  - **\* 외부 전자 메일 주소**   메일 연락처의 기본 SMTP 주소와 외부 전자 메일 계정입니다. 이 연락처로 보낸 전자 메일은 이 전자 메일 주소로 전달됩니다.

  - **기타 옵션**을 클릭하여 메일 연락처 계정이 포함된 OU를 표시합니다. 연락처를 다른 OU로 이동하려면 Active Directory 사용자 및 컴퓨터를 사용해야 합니다.

## 연락처 정보

**연락처 정보** 섹션을 사용하면 우편물 주소나 전화 번호 등 받는 사람의 연락처 정보를 보거나 변경할 수 있습니다. 이 정보는 주소록에 표시됩니다.

## 조직

**조직** 섹션을 사용하면 조직에서의 연락처 역할에 대한 자세한 정보를 기록할 수 있습니다. 이 정보는 주소록에 표시됩니다. 또한 Outlook과 같은 전자 메일 클라이언트에서 액세스할 수 있는 가상 조직도를 만들 수 있습니다.

  - **직함**   이 상자를 사용하여 연락처의 직함을 보거나 변경합니다.

  - **부서**   이 상자를 사용하여 연락처의 근무 부서를 보거나 변경합니다. 이 상자를 사용하여 동적 메일 그룹과 주소 목록에 대한 받는 사람 조건을 만들 수 있습니다.

  - **회사**   이 상자를 사용하여 연락처의 근무 회사를 보거나 변경합니다. 이 상자를 사용하여 동적 메일 그룹에 대한 받는 사람 조건을 만들 수도 있습니다.

  - **관리자** 관리자를 추가하려면 **찾아보기**를 클릭합니다. **관리자 선택**에서 사람을 선택하고 **확인**을 클릭합니다.

  - **부하 직원**   이 입력란은 수정할 수 없습니다. *부하 직원*은 특정 관리자에게 보고하는 받는 사람입니다. 받는 사람에 대한 관리자를 지정한 경우 해당 받는 사람은 관리자 사서함의 세부 정보에 부하 직원으로 나타납니다. 예를 들어 Toby가 메일 연락처인 Ann과 Spencer를 관리하는 경우 Ann과 Spencer의 조직 속성에 있는 **관리자** 상자에는 Toby가 지정되고, Toby의 사서함 속성에 있는 **부하 직원** 상자에는 Ann과 Spencer가 표시됩니다.

## 전자 메일 옵션

**전자 메일 옵션** 섹션을 사용하면 메일 연락처의 프록시 주소를 추가 또는 제거하거나 기존 프록시 주소를 편집할 수 있습니다. 메일 연락처의 기본 SMPT 주소도 이 섹션에 표시되지만 변경할 수는 없습니다. 변경하려면 **일반** 섹션에서 연락처의 외부 전자 메일 주소를 변경해야 합니다.


> [!NOTE]
> <STRONG>전자 메일 옵션</STRONG> 섹션은 Exchange Server 2013에서만 사용할 수 있습니다. Exchange Online에서는 사용할 수 없습니다.



## 메일 설명

**메일 설명** 섹션에서는 메일 설명을 추가하여 이 받는 사람에게 메시지를 보낼 경우 발생할 수 있는 문제를 사용자에게 알릴 수 있습니다. 메일 설명은 새 전자 메일 메시지의 받는 사람, 참조 또는 숨은 참조 필드에 이 받는 사람이 추가될 때 정보 표시줄에 표시되는 텍스트입니다.


> [!NOTE]
> 메일 설명은 HTML 태그를 포함할 수 있지만 스크립트는 사용할 수 없습니다. 표시되는 사용자 지정 메일 설명의 길이는 175자를 초과할 수 없습니다. 단, HTML 태그는 길이 제한 계산에 포함되지 않습니다.



## 셸을 사용하여 메일 연락처 속성 변경

메일 연락처의 속성은 Active Directory와 Exchange 모두에 저장됩니다. 일반적으로 조직 및 연락처 정보 속성을 보고 변경하려면 **Get-Contact** 및 **Set-Contact** cmdlet을 사용합니다. 전자 메일 주소와 메일 설명 같은 메일 관련 속성과 사용자 지정 특성을 보거나 변경하고 주소 목록에서 연락처를 숨길지 여부를 지정하려면 **Get-MailContact** 및 **Set-MailContact** cmdlet을 사용합니다.

자세한 내용은 다음 항목을 참조하십시오.

  - [Get-Contact](https://technet.microsoft.com/ko-kr/library/aa998258\(v=exchg.150\))

  - [Set-Contact](https://technet.microsoft.com/ko-kr/library/bb124535\(v=exchg.150\))

  - [Get-MailContact](https://technet.microsoft.com/ko-kr/library/bb124717\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/ko-kr/library/aa995950\(v=exchg.150\))

다음은 셸을 사용하여 메일 연락처 속성을 변경하는 몇 가지 예입니다.

이 예에서는 메일 연락처 Kai Axford의 직함, 부서, 회사 및 관리자 속성을 구성합니다.

    Set-Contact "Kai Axford" _-Title Consultant -Department "Public Relations" -Company Fabrikam -Manager "Karen Toh"

이 예에서는 모든 메일 연락처에 대해 CustomAttribute1 속성을 PartTime 값으로 설정하고 해당 메일 연락처를 조직의 주소록에서 숨깁니다.

    Get-MailContact | Set-MailContact -CustomAttribute1 PartTime -HiddenFromAddressListsEnabled $true

이 예에서는 Public Relations 부서의 모든 메일 연락처에 대해 CustomAttribute15 속성을 TemporaryEmployee 값으로 설정합니다.

    Get-Contact -Filter "Department -eq 'Public Relations'" | Set-MailContact -CustomAttribute15 TemporaryEmployee

## 작동 여부는 어떻게 확인합니까?

메일 연락처의 속성이 변경되었는지 확인하려면 다음을 수행합니다.

  - EAC에서 메일 연락처를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하여 변경한 속성을 봅니다.

  - 셸에서 **Get-Contact** 및 **Get-MailContact** cmdlet을 사용하여 변경 내용을 확인합니다. 셸을 사용할 때 얻을 수 있는 한 가지 이점은 여러 메일 연락처의 여러 속성을 볼 수 있다는 것입니다. 모든 메일 연락처가 CustomAttribute1 속성 값 PartTime으로 설정되고 주소록에서 숨겨진 위 예의 경우 다음 명령을 실행하여 변경 내용을 확인합니다.
    
        Get-MailContact | Fl Name,CustomAttribute1,HiddenFromAddressListsEnabled
    
    Public Relations 부서의 모든 메일 연락처에 대해 CustomAttribute15가 설정된 위 예의 경우 다음 명령을 실행하여 변경 내용을 확인합니다.
    
        Get-Contact -Filter "Department -eq 'Public Relations'" | Get-MailContact | FL Name,CustomAttribute15

## 메일 연락처 대량 편집

EAC를 사용하여 여러 메일 연락처에 대해 선택한 속성을 변경할 수 있습니다. EAC에서 연락처 목록의 메일 연락처를 둘 이상 선택하면 대량 편집할 수 있는 속성이 세부 정보 창에 표시됩니다. 이러한 속성 중 하나를 변경하면 변경 내용이 선택된 모든 받는 사람에게 적용됩니다.

메일 연락처를 대량 편집할 경우 다음 속성 영역을 변경할 수 있습니다.

  - **연락처 정보**   주소, 우편 번호 및 구/군/시 이름과 같은 공유 속성을 변경합니다.

  - **조직**   부서 이름, 회사 이름 및 선택한 메일 연락처나 메일 사용자가 보고하는 관리자 등의 공유 속성을 변경합니다.

## EAC를 사용하여 메일 연락처 대량 편집

1.  EAC에서 **받는 사람** \> **연락처**로 이동합니다.

2.  연락처 목록에서 두 개 이상의 메일 연락처를 선택합니다. 메일 연락처 및 메일 사용자의 조합을 대량으로 편집할 수 없습니다.
    

    > [!TIP]
    > 인접한 여러 메일 연락처를 선택하려면 Shift 키를 누른 상태로 편집하려는 첫 번째 메일 연락처를 클릭한 다음 마지막 메일 연락처를 클릭합니다. Ctrl 키를 누른 상태로 편집할 각 연락처를 클릭하여 여러 메일 연락처를 선택할 수도 있습니다.



3.  세부 정보 창의 **대량 편집**에서 **연락처** 또는 **조직** 아래의 **업데이트**를 클릭합니다.

4.  속성 페이지에서 필요한 사항을 변경하고 변경 내용을 저장합니다.

## 작동 여부는 어떻게 확인합니까?

메일 연락처가 대량 편집되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 대량 편집한 각 메일 연락처를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하여 변경한 속성을 봅니다.

  - 셸에서 **Get-Contact** cmdlet을 사용하여 변경 내용을 확인합니다. 예를 들어 EAC의 대량 편집 기능을 사용하여 A. Datum Corporation이라는 공급 회사의 모든 메일 연락처에 대해 관리자 및 사무실을 변경한 경우 이러한 변경 내용을 확인하려면 셸에서 다음 명령을 실행할 수 있습니다.
    
        Get-Contact -ResultSize unlimited -Filter {(Company -eq 'Adatum')} | fl Name,Office,Manager


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning용 단축 아이콘" alt="LinkedIn Learning용 단축 아이콘" /> <strong>Office 365를 처음 사용하시나요?</strong><br />
LinkedIn Learning에서 제공하는 <a href="https://support.office.com/en-us/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>의 무료 비디오 과정을 확인해보세요.</p></td>
</tr>
</tbody>
</table>

