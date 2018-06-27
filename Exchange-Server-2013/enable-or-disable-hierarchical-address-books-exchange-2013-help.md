---
title: '계층 구조 주소록을 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 계층 구조 주소록을 사용 하지 않도록 설정 하거나 사용
ms:assetid: b4c3a175-ce5e-4bfb-a4a0-92d25f3644b3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff607473(v=EXCHG.150)
ms:contentKeyID: 50483969
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 계층 구조 주소록을 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Outlook 2010 이상에서 최종 사용자에게 제공되는 기능인 HAB(계층 구조 주소록)를 구성할 수 있습니다. HAB를 사용하면 연공서열 또는 관리 구조를 기반으로 하는 조직의 계층 구조를 사용하여 Exchange 조직에서 받는 사람을 찾을 수 있습니다. HAB에 대한 자세한 내용은 [계층 구조 주소록](hierarchical-address-books-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1시간입니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "메일 그룹" 항목

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 시작하기 전에 [계층 구조 주소록](hierarchical-address-books-exchange-2013-help.md) 항목을 읽어 보십시오. HAB가 Exchange 조직에 적합한지 이해하고 있어야 합니다.

  - 현재 Exchange 조직의 OU(조직 단위), 그룹, 사용자, 연락처 구성 방식을 이해합니다.

  - HAB를 구성하는 데 필요한 다음 표의 cmdlet과 관련 매개 변수를 이해합니다.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>cmdlet</th>
    <th>매개 변수</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/ko-kr/library/aa997443(v=exchg.150)">Set-OrganizationConfig</a></p></td>
    <td><p><em>HierarchicalAddressBookRoot</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/ko-kr/library/bb123770(v=exchg.150)">Set-Group</a></p></td>
    <td><p><em>IsHierarchicalGroup</em></p>
    <p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/ko-kr/library/aa998221(v=exchg.150)">Set-User</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/ko-kr/library/bb124535(v=exchg.150)">Set-Contact</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    </tbody>
    </table>


  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 HAB를 사용하도록 설정


> [!NOTE]
> HAB를 사용하도록 설정할 때 EAC를 사용할 수 없었더라도 일단 HAB가 사용되도록 설정되면 EAC를 통해 조직 계층 구조에서 그룹의 구성원 자격을 관리할 수 있습니다.



이 예에서는 HAB에 대해 HAB라는 OU를 만듭니다. 조직의 도메인 이름은 Contoso-dom이며 Contoso,Ltd는 계층 구조의 최상위 조직(*루트 조직*)의 이름이 됩니다. 회사 사무실, 제품 지원 조직, 판매 및 마케팅 조직이라는 하위 그룹이 Contoso,Ltd 아래에 하위 조직으로 생성됩니다. 또한 인사, 회계 그룹, 관리 그룹이 회사 사무실 아래에 하위 조직으로 생성됩니다.

메일 그룹 만들기에 대한 자세한 내용은 [메일 그룹 만들기 및 관리](create-and-manage-distribution-groups-exchange-2013-help.md)를 참조하십시오.

1.  Contoso 조직에 HAB라는 OU를 만듭니다. Active Directory 사용자 및 컴퓨터를 사용하거나 명령 프롬프트에 다음을 입력할 수 있습니다.
    

    > [!NOTE]
    > 또는 Exchange 포리스트의 기존 OU를 사용할 수 있습니다.

    
        dsadd ou "OU=HAB,DC=Contoso-dom,DC=Contoso,DC=com"
    

    > [!NOTE]
    > 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=198986">새 조직 구성 단위 만들기</A>를 참조 합니다.



2.  HAB에 대해 루트 메일 그룹 Contoso,Ltd를 만듭니다.
    

    > [!NOTE]
    > 이 항목에서는 셸 예제가 제공됩니다. 그러나 EAC를 사용하여 메일 그룹을 만들 수도 있습니다. 자세한 내용은 <A href="create-and-manage-distribution-groups-exchange-2013-help.md">메일 그룹 만들기 및 관리</A>를 참조하십시오.

    
        New-DistributionGroup -Name "Contoso,Ltd" -DisplayName "Contoso,Ltd" -Alias "ContosoRoot" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "ContosoRoot" -Type "Distribution"

3.  Contoso,Ltd를 HAB의 루트 조직으로 지정
    
        Set-OrganizationConfig -HierarchicalAddressBookRoot "Contoso,Ltd"

4.  HAB의 다른 계층에 대해 메일 그룹 만들기 이 예에서는 회사 사무실, 제품 지원 조직, 판매 및 마케팅 조직, 인사, 회계 그룹 및 관리 그룹과 같은 그룹을 만듭니다. 이 예에서는 회사 사무실 메일 그룹을 만듭니다.
    

    > [!NOTE]
    > 이 항목에서는 셸 예제가 제공됩니다. 그러나 EAC를 사용하여 메일 그룹을 만들 수도 있습니다. 자세한 내용은 <A href="create-and-manage-distribution-groups-exchange-2013-help.md">메일 그룹 만들기 및 관리</A>를 참조하십시오.

    
        New-DistributionGroup -Name "Corporate Office" -DisplayName "Corporate Office" -Alias "CorporateOffice" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "CorporateOffice" -Type "Distribution"

5.  각 그룹을 HAB의 구성원으로 지정합니다. 이 예에서는 Contoso,Ltd, 회사 사무실, 제품 지원 조직, 판매 및 마케팅 조직, 인사, 회계 그룹 및 관리 그룹을 계층 구조 그룹으로 지정합니다. 이 예에서는 Contoso,Ltd 메일 그룹을 HAB의 구성원으로 지정합니다.
    
        Set-Group -Identity "Contoso,Ltd" -IsHierarchicalGroup $true

6.  각 하위 그룹을 루트 조직의 구성원으로 추가합니다. 이 예에서는 회사 사무실, 제품 지원 조직, 판매 및 마케팅 조직 메일 그룹이 HAB의 루트 조직인 Contoso,Ltd의 구성원으로 추가됩니다. 이 예에서는 회사 사무실 메일 그룹을 Contoso,Ltd 루트 메일 그룹의 구성원으로 추가합니다.
    

    > [!NOTE]
    > 이 예에서는 메일 그룹의 별칭을 사용합니다.

    
        Add-DistributionGroupMember -Identity "ContosoRoot" -Member "CorporateOffice"

7.  각 하위 그룹을 회사 사무실 메일 그룹에 구성원으로 추가합니다. 이 예에서는 메일 그룹인 인사, 회계 그룹 및 관리 그룹이 회사 사무실 메일 그룹의 구성원으로 추가됩니다. 이 예에서는 인사 메일 그룹을 회사 사무실 메일 그룹의 구성원으로 추가합니다.
    

    > [!NOTE]
    > 이 예에서는 메일 그룹의 별칭을 사용하고 인사 메일 그룹의 별칭을 HumanResources로 간주합니다.

    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "HumanResources"

8.  사용자를 HAB의 그룹에 추가합니다. 이 예에서는 David Hamilton(SMTP 주소 DHamilton@contoso.com)이 OU Contoso-dom.Contoso.com/Users의 기존 사용자이며 회사 사무실 그룹에 추가됩니다. 다른 사용자를 HAB의 그룹에 추가하려면 이 단계를 반복합니다.
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "DHamilton"

9.  HAB에 포함된 그룹의 *SeniorityIndex* 매개 변수를 설정합니다. 이 예에서는 회사 사무실 그룹에 인사, 회계 그룹 및 관리 그룹의 세 가지 하위 그룹이 포함됩니다. 그룹을 기본 설정인 사전 순서에 따라 오름차순으로 나열하는 대신 인사(*SeniorityIndex* = 100), 회계 그룹(*SeniorityIndex* = 50), 관리 그룹(*SeniorityIndex* = 25) 순으로 정렬합니다. 이 예에서는 인사 그룹의 *SeniorityIndex* 매개 변수를 100으로 설정합니다.
    
        Set-Group -Identity "Human Resources" -SeniorityIndex 100
    

    > [!NOTE]
    > <EM>SeniorityIndex</EM> 매개 변수는 HAB의 그룹 또는 사용자를 숫자 순서에 따라 내림차순으로 정렬하는 데 사용되는 숫자 값입니다. <EM>SeniorityIndex</EM> 매개 변수가 설정되지 않았거나 2명 이상의 사용자에 대해 동일할 경우 HAB 정렬 순서가 <EM>PhoneticDisplayName</EM> 매개 변수 값을 사용하여 사용자를 사전 순서에 따라 오름차순으로 나열합니다. <EM>PhoneticDisplayName</EM> 값이 설정되지 않은 경우 HAB 정렬 순서가 <EM>DisplayName</EM> 매개 변수 값을 기본값으로 사용하여 사용자를 사전 순서에 따라 오름차순으로 나열합니다.



10. HAB 그룹에 포함된 사용자의 *SeniorityIndex* 매개 변수를 설정합니다. 이 예에서는 회사 사무실 그룹에 세 명의 사용자인 Amy Alberts, David Hamilton, Rajesh M. Patel이 포함됩니다. 사용자를 기본 설정인 사전 순서에 따라 오름차순으로 나열하는 대신 David Hamilton(*SeniorityIndex* = 100), Rajesh M. Patel(*SeniorityIndex* = 50), Amy Alberts(*SeniorityIndex* = 25) 순으로 정렬합니다. 이 예에서는 David Hamilton 사용자의 *SeniorityIndex* 매개 변수를 100으로 설정합니다.
    
        Set-User -Identity "DHamilton@contoso.com" -SeniorityIndex 100

앞의 단계를 완료하면 HAB가 Outlook에 표시됩니다. HAB를 보려면 Outlook을 열고 **주소록**을 클릭합니다. 다음과 같이 HAB가 **조직** 탭에 표시됩니다.

**Contoso,Ltd의 HAB 예**

![계층 구조 주소록 대화 상자](images/Ff607473.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "계층 구조 주소록 대화 상자")

HAB를 만든 후 EAC를 사용하여 조직 계층 구조에서 그룹의 구성원을 관리할 수 있습니다. 그러나 셸을 사용하여 새 그룹 또는 사용자의 *SeniorityIndex* 매개 변수를 수정해야 합니다.

구문과 매개 변수 정보에 대한 자세한 내용은 다음을 참조하십시오.

  - [New-DistributionGroup](https://technet.microsoft.com/ko-kr/library/aa998856\(v=exchg.150\))

  - [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\))

  - [Set-Group](https://technet.microsoft.com/ko-kr/library/bb123770\(v=exchg.150\))

  - [Add-DistributionGroupMember](https://technet.microsoft.com/ko-kr/library/bb124340\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/ko-kr/library/aa998221\(v=exchg.150\))

## 셸을 사용하여 계층 구조 주소록을 사용하지 않도록 설정

이 예에서는 HAB에 사용된 루트 조직을 사용하지 않도록 설정합니다.

    Set-OrganizationConfig -HierarchicalAddressBookRoot $null


> [!NOTE]
> 이 명령으로는 HAB 구조에 사용된 루트 조직 또는 하위 그룹을 삭제하거나 그룹 또는 사용자의 <EM>SeniorityIndex</EM> 값을 다시 설정할 수 없습니다. 이 명령으로는 HAB가 Outlook에 표시되지 않도록 설정하는 것만 가능합니다. 구성 설정이 동일한 HAB를 다시 사용하려면 루트 조직만 다시 사용하도록 설정하면 됩니다.



구문과 매개 변수 정보에 대한 자세한 내용은 [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\))를 참조하십시오.

