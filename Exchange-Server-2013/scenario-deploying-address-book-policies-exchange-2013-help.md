---
title: '시나리오: 주소록 정책 배포: Exchange 2013 Help'
TOCTitle: '시나리오: 주소록 정책 배포'
ms:assetid: 6ac3c87d-161f-447b-afb2-149ae7e3f1dc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657455(v=EXCHG.150)
ms:contentKeyID: 50483390
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 시나리오: 주소록 정책 배포

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

## 배포 시나리오

다음 세 시나리오에서는 서로 다른 세 가지 조직 유형에 사용할 수 있는 배포 솔루션에 대해 설명합니다. 이외에도 많은 시나리오가 있지만 여기에서는 가장 일반적인 시나리오를 다룹니다. 이러한 시나리오에서 주소 목록과 GAL(전체 주소 목록)은 사용자 지정 특성과 같이 개체를 논리적으로 그룹화하는 필터를 기반으로 만들어졌습니다.

## 시나리오 1: 두 개의 별도 회사 - Exchange 조직 하나

이 시나리오는 인프라를 공유하지만 조직망과 일반 직원이 없는 정부 기관, 사업부 또는 부서에 적용할 수 있습니다. 또한 특별한 보안 문제나 개인 정보 관련 고려 사항이 없는 부서에 적용할 수도 있습니다. 이 시나리오에서는 직원이 GAL을 보거나 다른 메일 그룹의 구성원을 찾을 때 동일한 조직의 구성원만 볼 수 있는 두 개의 ABP(주소록 정책)가 만들어집니다. 또한 사용자는 조직 전체에 있는 메일 그룹의 구성원이 되지 않습니다.

![별도의 두 회사와 주소록 정책](images/JJ657455.b4fc82da-a659-4ade-ba33-d55d90dcf204(EXCHG.150).gif "별도의 두 회사와 주소록 정책")

Contoso 및 Humungous Insurance ABP는 다음과 같은 주소 목록, 전체 주소 목록, 방 목록 및 OAB를 사용하여 만들어졌으며 이러한 항목은 사용자 지정 특성과 같은 필터로 개체를 그룹화하는 받는 사람 필터를 사용하여 만들어졌습니다. 두 회사가 상호 작용 없이 분리되어 있기 때문에 공통 주소 목록이 없습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Contoso</p></td>
<td><p>Humongous Insurance</p></td>
</tr>
<tr class="even">
<td><p>주소 목록</p></td>
<td><p>AL_CON_Groups</p>
<p>AL_CON_Users</p>
<p>AL_CON_Contacts</p></td>
<td><p>AL_HI_Groups</p>
<p>AL_HI_Users</p>
<p>AL_HI_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>전체 주소 목록</p></td>
<td><p>GAL_CON</p></td>
<td><p>GAL_HI</p></td>
</tr>
<tr class="even">
<td><p>대화방 주소 목록</p></td>
<td><p>AL_CON_Rooms</p></td>
<td><p>AL_HI_Rooms</p></td>
</tr>
<tr class="odd">
<td><p>OAB(오프라인 주소록)</p></td>
<td><p>OAB_CON</p></td>
<td><p>OAB_HI</p></td>
</tr>
</tbody>
</table>


## 시나리오 2: 두 회사가 CEO 공유

이 시나리오에서는 Fabrikam 및 Tailspin Toys에서 동일한 Exchange 조직과 동일한 CEO를 공유합니다. CEO만 두 회사에서 동일한 사람입니다. 이 시나리오에서는 다음과 같은 특성이 있는 세 개의 ABP가 필요합니다.

  - Tailspin Toys의 사용자는 GAL을 찾아볼 때 Tailspin Toys 사용자만 볼 수 있습니다.

  - Fabrikam의 사용자는 GAL을 찾아볼 때 Fabrikam 사용자만 볼 수 있습니다.

  - 각 회사에는 회사의 임원과 CEO가 포함된 SeniorLeaders라는 메일 그룹이 있습니다.

  - CEO의 메일 그룹 구성원을 검색하는 사용자에게는 사용자 회사에 속해 있는 그룹만 표시됩니다. 이러한 사용자는 해당 회사에 속해 있지 않은 그룹은 볼 수 없습니다.

  - 만들어진 ABP는 각각 **Fab**, **Tail** 및 **CEO**입니다.

![두 회사 한 CEO](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "두 회사 한 CEO")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Fabrikam</p></td>
<td><p>Tailspin Toys</p></td>
<td><p>CEO</p></td>
</tr>
<tr class="even">
<td><p>주소 목록</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p></td>
<td><p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p>
<p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>전체 주소 목록</p></td>
<td><p>GAL_FAB</p></td>
<td><p>GAL_TAIL</p></td>
<td><p>기본 GAL</p></td>
</tr>
<tr class="even">
<td><p>대화방 주소 목록</p></td>
<td><p>AL_FAB_Rooms</p></td>
<td><p>AL_TAIL_Rooms</p></td>
<td><p>기본 모든 장소</p></td>
</tr>
<tr class="odd">
<td><p>OAB(오프라인 주소록)</p></td>
<td><p>OAB_FAB</p></td>
<td><p>OAB_TAIL</p></td>
<td><p>기본 OAB</p></td>
</tr>
</tbody>
</table>


각 조직의 메일 그룹에 CEO를 추가하고 CEO가 각 회사의 ABP 범위에 속하는 경우 각 회사에서 CEO를 볼 수 있게 됩니다. CEO는 두 회사 모두에 있고 각 회사의 GAL 내에 표시되는 메일 그룹을 만들 수 있지만 메일 그룹의 구성원은 조직 내에 있는 그룹의 구성원만 볼 수 있습니다.

## 시나리오 3: 교육

이 시나리오는 학생 개인 정보를 보호하기 위해 학급 구분이 필요한 학교나 대학에 적용할 수 있습니다. 교육 시나리오는 다음과 같은 특징이 있습니다.

  - 각 학습의 학생은 해당 학습의 다른 학생, 해당 교사 및 교장만 볼 수 있습니다.

  - 교사는 해당 학급의 학생만 볼 수 있습니다.

  - 교사는 다른 모든 교사와 교장을 볼 수 있습니다.

  - 각 학급의 학부모와 교직원에 대한 메일 그룹을 만듭니다.

![주소록 정책 교육 시나리오](images/JJ657455.435f3b1a-9752-4c61-ab8a-80115c643d12(EXCHG.150).gif "주소록 정책 교육 시나리오")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Students_ClassA</p></td>
<td><p>Teachers_ClassA</p></td>
<td><p>교장 선생님</p></td>
</tr>
<tr class="even">
<td><p>주소 목록</p></td>
<td><p>AL_ClassAAL_Principal</p></td>
<td><p>AL_ClassAAL_AllTeachersAL_AllGroupsAL_Principal</p></td>
<td><p>AL_ClassA</p>
<p>AL_ClassB</p>
<p>AL_AllTeachers</p>
<p>AL_AllStudents</p>
<p>AL_AllGroups</p></td>
</tr>
<tr class="odd">
<td><p>전체 주소 목록</p></td>
<td><p>GAL_StudentsClassA</p></td>
<td><p>GAL_TeachersClassA</p></td>
<td><p>GAL_Everyone</p></td>
</tr>
<tr class="even">
<td><p>대화방 주소 목록</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>기본 모든 장소</p></td>
</tr>
<tr class="odd">
<td><p>OAB(오프라인 주소록)</p></td>
<td><p>OAB_StudentsClassA</p></td>
<td><p>OAB_TeachersClassA</p></td>
<td><p>기본 OAB</p></td>
</tr>
</tbody>
</table>


## 고려 사항 및 모범 사례

조직에서 ABP를 사용할 때 다음을 고려하십시오.

  - ABP가 올바르게 작동하려면 ABP가 적용될 사용자 사서함이 Exchange 2010 SP3 또는 Exchange 2013 서버에 있어야 합니다.

  - 글로벌 카탈로그 서버에서 Exchange 2010 클라이언트 액세스 서버 역할을 실행하지 마십시오. 그렇게 하면 Microsoft Exchange 주소록 서비스 대신 Active Directory가 NSPI(Name Service Provider Interface)에 사용됩니다. 글로벌 카탈로그 서버에서는 Exchange 2013 서버 역할을 실행할 수 있고 ABP도 정상적으로 작동하지만, 도메인 컨트롤러에 Exchange를 설치하는 것은 권장되지 않습니다.

  - HAB(계층 구조 주소록)와 ABP는 동시에 사용할 수 없습니다. 자세한 내용은 [계층 구조 주소록](https://docs.microsoft.com/ko-kr/exchange/address-books/hierarchical-address-books/hierarchical-address-books)를 참조하십시오.

  - 사용자가 할당한 ABP는 사용자 고유의 GAL에 있어야 합니다.

  - 클라이언트 응용 프로그램이 LDAP를 통해 Active Directory에 직접 액세스하는 경우에는 ABP로 구성된 논리를 건너뛰게 됩니다. Outlook for Mac 2011 및 Entourage 2008에서는 직접 LDAP 쿼리를 사용하여 Active Directory에 액세스하므로, 자동 검색 서비스에 의해 도메인 컨트롤러나 글로벌 카탈로그 서버가 이러한 클라이언트 응용 프로그램에 지정되거나 제공되는 경우 해당 응용 프로그램에서 ABP가 제대로 작동하지 않게 됩니다. Outlook for Mac 2011은 EWS 또는 로컬 OAB를 사용하여 디렉터리 정보에 액세스합니다. 단, Outlook for Mac 2011이 LDAP 서비스에 직접 액세스할 수 있으면 액세스를 시도합니다.

  - ABP에 사용되는 GAL은 적어도 ABP에 정의되고 지정된 모든 주소 목록(대화방 주소 목록 포함)을 포함해야 합니다. 동일한 ABP에 포함된 주소 목록보다 적은 수의 개체를 포함하는 GAL을 만들지 마십시오.

  - 메일 그룹을 만들 때 가상 조직 경계를 벗어나지 않는 것이 좋습니다. 여러 가상 조직의 구성원을 포함하는 메일 그룹을 만들면 다음과 같은 문제가 발생합니다.
    
      - 그룹 구성원이 메일 그룹에 메일을 전송하면서 배달 확인이나 읽음 확인을 요청할 경우 다른 가상 조직의 그룹 구성원 전자 메일 주소를 확인할 수 있습니다.
    
      - 암호화된 메시지가 메일 그룹에 전송되었지만 일부 그룹 구성원에게 유효한 디지털 ID가 없으면 유효한 ID가 없는 구성원의 총 수와 해당 전자 메일 주소 목록이 포함된 경고 메시지가 보낸 사람에게 전달됩니다. 그러나 유효한 디지털 ID가 없는 일부 구성원이 보낸 사람과 다른 조직에 속하는 경우에는 이 경고 메시지에 구성원 수는 정확하게 포함되지만 다른 조직에 속하는 구성원의 전자 메일 주소는 포함되지 않습니다. 결과적으로, 총 구성원 수가 구성원 주소 목록과 일치하지 않게 됩니다.
        
        예를 들어, 메일 그룹에 Agency A 및 Agency B라는 두 조직의 구성원 총 다섯 명이 포함되어 있다고 가정해 보겠습니다. 그룹 구성원 중 셋이 Agency A에 속하고 그중 한 명이 잘못된 디지털 ID를 가지고 있습니다. 나머지 두 구성원은 Agency B에 속하고 둘 다 잘못된 ID를 가지고 있습니다. 이 경우 Agency A의 구성원이 암호화된 메시지를 메일 그룹에 보내면 받는 사람 중 총 세 명에게 유효한 디지털 ID가 없다는 경고 메시지를 받게 됩니다. 그러나 경고 메시지에는 Agency A에 속한 받는 사람의 전자 메일 주소만 나열됩니다.
    
      - ABP가 **Get-Group** cmdlet에 적용되지 않기 때문에 **Get-Group**을 실행할 수 있는 모든 사용자 또는 프로세스가 액세스 가능한 그룹의 모든 구성원을 볼 수 있습니다.
        
        사용자가 Outlook Web App를 사용하여 그룹을 관리할 수 없도록 OWA 옵션의 그룹 관리 설정을 수정하는 것이 좋습니다. 사용자가 OWA 옵션을 사용하여 그룹을 관리하지 못하게 하려면 MyDistributionGroupMembership RBAC 역할에서 해당 사용자를 제외하십시오. 자세한 내용은 [MyDistributionGroupMembership 역할](mydistributiongroupmembership-role-exchange-2013-help.md)을 참조하십시오.
    
      - 사용자가 Outlook 또는 Outlook Web App을 사용하여 그룹을 관리할 수 있도록 허용한 경우 그룹 소유자에게 그룹 구성원 목록을 볼 수 있는 전체 권한이 있어야 합니다.

  - 모든 ABP는 대화방 주소 목록을 포함해야 합니다. 조직에서 대화방 주소 목록을 사용하지 않는 경우에는 빈 대화방 주소 목록을 만들어 기본값으로 사용할 수 있습니다.

  - ABP 배포는 한 가상 조직의 사용자가 다른 가상 조직의 사용자에게 전자 메일을 보내지 못하도록 차단하지는 않습니다. 사용자가 다른 조직의 사용자에게 전자 메일을 보내지 못하게 하려면 전송 규칙을 만드는 것이 좋습니다. 예를 들어, Contoso 사용자가 Fabrikam 사용자의 메시지를 받지 못하게 하지만 Fabrikam의 임원진에서는 Contoso 사용자에게 메시지를 보내도록 허용하는 전송 규칙을 만들려면 다음 셸 명령을 실행하십시오.
    
      ```powershell
      New-TransportRule -Name "StopFabrikamtoContosoMail" -FromMemberOf "AllFabrikamEmployees" -SentToMemberOf "AllContosoEmployees" -DeleteMessage -ExceptIfFrom seniorleadership@fabrikam.com
      ```
  - Lync 클라이언트에 ABP와 유사한 기능을 적용 하려는 경우에 특정 사용자 개체에 `msRTCSIP-GroupingID` 특성을 설정할 수 있습니다. 자세한 내용은 [PartitionByOU가 Msrtcsip-groupingid로 대체 됨](https://go.microsoft.com/fwlink/p/?linkid=232306) 항목을 참조 합니다.

## 일반 배포 단계

## 주소 목록 조각화에서 ABP로 마이그레이션

Exchange 2007 주소 목록 격리 솔루션의 전체 [구성 가상 조직 및 Exchange 2007에서 주소 목록 분리](https://go.microsoft.com/fwlink/p/?linkid=109601)이 백서에는 지침을 사용 하 여 구성 하는 조직, [Exchange Server 2010 주소록 정책에서 Exchange Server 2007 주소 목록 분리 하 마이그레이션](https://go.microsoft.com/fwlink/p/?linkid=235967)에 설명 된 단계를 사용 하 여 Exchange Server 2010으로 마이그레이션할 먼저 해야 있습니다. 이 절차는 조직에 대 한 일부 중지 시간 필요 합니다 하 고 그에 따라 계획 따라서 갖추어야 합니다.

## 새로 ABP 배포

조직에서 Exchange 2013 ABP를 배포 중이고 Exchange 2007 주소 목록 조각화를 사용하지 않은 경우 이러한 지침을 사용하여 조직의 ABP를 배포할 수 있습니다.

이 섹션의 단계는 시나리오 2: Two companies sharing a CEO에 대해 단계별로 설정합니다. 이 시나리오에서 Fabrikam과 Tailspin Toys는 CEO와 임원진을 공유하는 별개의 회사입니다.

## 1단계: 주소록 정책 라우팅 에이전트 설치 및 구성

ABP를 사용하고 있고 서로 다른 가상 조직의 사용자가 서로의 개인 정보를 보지 못하도록 하려면 주소록 정책 라우팅 에이전트를 설정하면 됩니다. 주소록 정책 라우팅 에이전트는 받는 사람이 조직에서 확인되는 방식을 제어하는, 사서함 서버에서 실행되는 전송 에이전트입니다. 주소록 정책 라우팅 에이전트가 설치 및 구성되면 서로 다른 GAL이 할당된 사용자는 외부 받는 사람으로 표시되므로 외부 받는 사람의 대화 상대 카드를 볼 수 없습니다.

자세한 내용은 [주소 주소록 정책 라우팅 에이전트 설치 및 구성](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md)을 참조하십시오.

## 2단계: 가상 조직 나누기

조직을 나누는 방법을 마련해야 합니다. 다음과 같은 이유로 Company, Department 또는 StateOrProvince와 같은 미리 제공된 조건부 특성 대신 사서함, 연락처 및 그룹에 CustomAttribute1-15 속성을 사용하여 가상 조직을 나누는 것이 좋습니다.

  - 일부 개체의 받는 사람 유형에는 Active Directory에 미리 제공된 조건부 특성이 없을 수 있습니다. 예를 들어 매일 그룹 및 동적 메일 그룹에서는 회사, 부서 또는 상태 특성을 지원하지 않습니다.

  - 미리 제공된 조건부 특성 중에는 일부 받는 사람의 cmdlet에 노출되지 않는 것이 있습니다. 예를 들어 메일 사용자, 연락처, 메일 그룹 및 메일 사용 가능 공용 폴더에 대해 cmdlet에 노출되는 *Company*, *department* 및 *StateOrProvince* 매개 변수를 사용할 수 없습니다.

  - 미리 제공된 조건부 특성을 사용할 경우 받는 사람을 분리하려면 여러 cmdlet이 필요합니다. 예를 들어 **New-Mailbox** 또는 **Set-Mailbox** cmdlet을 실행한 후 UserMailbox에 대한 *Company*, *Department*, *StateOrProvince*에 태그를 지정하려면 Set-User를 실행해야 합니다.

  - *CustomAttributeX* 매개 변수는 각 받는 사람 유형에 대해 Set-\* cmdlet에 모두 노출되므로 단일 Set- cmdlet을 통해 해당 유형의 모든 조각화를 완료할 수 있습니다.

  - CustomAttributeX 특성은 조직의 사용자 지정을 위해 명시적으로 예약되어 있으며 조직 관리자만 제어할 수 있습니다.

조직을 나눌 때 구현해야 할 또 다른 모범 사례는 메일 그룹 및 동적 메일 그룹의 이름에 회사 식별자를 사용하는 것입니다. Exchange에는 그룹 명명 정책 기능이 있습니다. 이 기능은 메일 그룹의 Company, StateorProvince, Title 및 CustomAttribute1~CustomAttribute15 작성자를 포함하여 메일 그룹을 만드는 사용자의 여러 특성을 기반으로 메일 그룹의 이름에 접두사나 접미사를 자동으로 추가합니다. 그룹 명명 정책은 사용자가 고유한 메일 그룹을 만들 수 있도록 허용하는 경우 특히 중요합니다. 자세한 내용은 [메일 그룹 명명 정책을 만들려면](https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy)를 참조하십시오.

동적 메일 그룹에는 그룹 명명 정책이 적용되지 않으므로 수동으로 동적 메일 그룹을 나누고 명령 정책을 적용해야 합니다.

## 3단계: 주소 목록, GAL 및 OAB 만들기

주소 목록 및 전체 주소 목록을 만드는 경우에는 ConditionalCompany, ConditionalCustomAttribute5 등의 "IncludedRecipient" 및 "ConditionalX"를 사용하면 안 됩니다. 받는 사람 필터를 대신 사용해야 합니다. 받는 사람 필터를 만들려면 셸을 사용해야 합니다. 받는 사람 필터에 대한 자세한 내용은 [Edge 전송 서버의 받는 사람 필터링](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md)을 참조하십시오.

ABP를 만들 때 사용자의 Outlook 또는 Outlook Web App에 주소 목록을 표시하는 방식에 따라 여러 주소 목록을 만듭니다. 이 조직에는 다음 네 개의 주소 목록이 있습니다.

  - AL\_FAB\_Users\_DGs

  - AL\_FAB\_Contacts

  - AL\_TAIL\_Users\_DGs

  - AL\_TAIL\_Contacts

이 예에서는 주소 목록 AL\_TAIL\_Users\_DGs를 만듭니다. 주소 목록에는 CustomAttribute15가 TAIL인 모든 사용자 및 메일 그룹이 포함되어 있습니다.

  ```powershell
  New-AddressList -Name "AL_TAIL_Users_DGs" -RecipientFilter {((RecipientType -eq 'UserMailbox') -or (RecipientType -eq "MailUniversalDistributionGroup") -or (RecipientType -eq "DynamicDistributionGroup")) -and (CustomAttribute15 -eq "TAIL")}
  ```

받는 사람 필터를 사용한 주소 목록 만들기에 대한 자세한 내용은 [받는 사람 필터를 사용 하 여 주소 목록 만들기](https://docs.microsoft.com/ko-kr/exchange/address-books/address-lists/use-recipient-filters-to-create-an-address-list)를 참조하십시오.

ABP를 만들려면 대화방 주소 목록을 제공해야 합니다. 조직에 대화방 또는 장비 사서함 같은 리소스 사서함이 없는 경우에는 빈 대화방 주소 목록을 만드는 것이 좋습니다. 다음 예에서는 조직에 대화방 사서함이 없으므로 빈 대화방 주소 목록을 만듭니다.

  ```powershell
  New-AddressList -Name AL_BlankRoom -RecipientFilter {(Alias -ne $null) -and ((RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox'))}
  ```

그러나 이 시나리오에서는 Fabrikam 및 Contoso 모두에 대화방 사서함이 있습니다. 이 예에서는 받는 사람 필터를 사용하여 CustomAttribute15가 FAB인 Fabrikam의 대화방 목록을 만듭니다.

  ```powershell
  New-AddressList -Name AL_FAB_Room -RecipientFilter {(Alias -ne $null) -and (CustomAttribute15 -eq "FAB")-and (RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox')}
  ```
ABP에 사용되는 전체 주소 목록은 주소 목록의 부분 집합이어야 합니다. ABP의 주소 목록보다 개체 수가 적은 GAL을 만들지 마십시오. 이 예에서는 주소 목록 및 대화방 주소 목록에 있는 모든 받는 사람을 포함하는 Tailspin Toys의 전체 주소 목록을 만듭니다.

  ```powershell
  New-GlobalAddressList -Name "GAL_TAIL" -RecipientFilter {(CustomAttribute15 -eq "TAIL")}
  ```

자세한 내용은 [전체 주소 목록 만들기](https://docs.microsoft.com/ko-kr/exchange/address-books/address-lists/create-global-address-list)를 참조하십시오.

OAB를 만드는 경우 New- 또는 Set-OfflineAddressBook의 *AddressLists* 매개 변수를 제공할 때 적절한 GAL을 포함하여 항목이 예기치 않게 누락되지 않도록 할 수 있습니다. 기본적으로 사용자에게 표시되는 항목 집합을 사용자 지정하고 New/Set-OfflineAddressBook의 AddressLists에 AddressLists 목록을 지정하여 OAB의 다운로드 크기를 줄일 수 있습니다. 하지만 사용자가 OAB에서 전체 GAL 항목 집합을 볼 수 있게 하려면 AddressLists에 GAL을 포함해야 합니다.

이 예에서는 OAB\_FAB라는 Fabrikam 의 OAB를 만듭니다.

```powershell
New-OfflineAddressBook -Name "OAB_FAB" -AddressLists "GAL_FAB"
```

자세한 내용은 [오프 라인 주소록 만들기](https://docs.microsoft.com/ko-kr/exchange/address-books/offline-address-books/create-offline-address-book)를 참조하십시오.

## 4단계: ABP 만들기

필요한 모든 개체를 만든 후에는 ABP를 만들 수 있습니다. 이 예에서는 ABP\_TAIL이라는 이름의 ABP를 만듭니다.

  ```powershell
  New-AddressBookPolicy -Name "ABP_TAIL" -AddressLists "AL_TAIL_Users_DGs"," AL_TAIL_Contacts" -OfflineAddressBook "\OAB_TAIL" -GlobalAddressList "\GAL_TAIL" -RoomList "\AL_TAIL_Rooms"
  ```

자세한 내용은 [주소록 정책 만들기](https://docs.microsoft.com/ko-kr/exchange/address-books/address-book-policies/create-an-address-book-policy)를 참조하십시오.

## 5단계: 사서함에 ABP 할당

사용자에게 ABP를 할당하는 것이 프로세스의 마지막 단계입니다. ABP는 사용자의 응용 프로그램이 클라이언트 액세스 서버에서 실행되고 있는 Microsoft Exchange 주소록 서비스에 연결할 때 적용됩니다. 사용자 계정에 ABP가 적용될 때 사용자가 Outlook 또는 Outlook Web App에 연결되어 있다면 클라이언트 응용 프로그램을 닫고 다시 시작해야 새 주소 목록과 GAL을 볼 수 있습니다.

이 예에서는 CustomAttribute15가 "FAB"인 모든 사서함에 ABP\_FAB를 할당합니다.

  ```powershell
  Get-Mailbox -resultsize unlimited | where {$_.CustomAttribute15 -eq "TAIL"} | Set-Mailbox -AddressBookPolicy "ABP_TAIL"
  ```

자세한 내용은 [메일 사용자에 게 주소록 정책 할당](https://docs.microsoft.com/ko-kr/exchange/address-books/address-book-policies/assign-an-address-book-policy-to-mail-users)을 참조하십시오.

