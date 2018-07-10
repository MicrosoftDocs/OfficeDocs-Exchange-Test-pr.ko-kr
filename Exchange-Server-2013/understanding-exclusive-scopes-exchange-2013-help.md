---
title: '배타적 범위 이해 (영문): Exchange 2013 Help'
TOCTitle: 배타적 범위 이해 (영문)
ms:assetid: 32492622-3b01-4e3b-8288-ed39525eea75
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638110(v=EXCHG.150)
ms:contentKeyID: 50482797
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 배타적 범위 이해 (영문)

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

*단독 범위*는 관리 역할 할당에 연결할 수 있는 특수한 유형의 명시적 관리 범위입니다. 단독 범위는 CEO 사서함과 같이 매우 중요한 개체 그룹이 있고 이러한 개체를 관리할 수 있는 권한이 있는 사용자를 엄격하게 제어하려는 경우에 적합하도록 설계되었습니다.

단독 범위를 가질 수 있는 역할 할당을 *단독 역할 할당*이라고 합니다.

단독 범위를 만들 경우 해당 단독 범위 또는 동등한 단독 범위가 할당된 사용자만 이 범위에 일치하는 개체를 수정할 수 있습니다. 이 단독 범위 또는 동등한 단독 범위가 할당되지 않은 역할 담당자는 자신의 역할이 개체를 포함하는 범위를 가지더라도 범위에 일치하는 개체를 수정할 수 없습니다. 단독 범위는 단독이 아닌 다른 모든 일반 범위를 재정의합니다. 이 동작은 Active Directory ACL(액세스 제어 목록)에서 거부 ACE(액세스 제어 항목)가 작동하는 방식과 비슷합니다.

*동등한 단독 범위*는 다른 단독 범위와 일부 동일한 개체가 일치하는 또 다른 단독 범위를 나타냅니다. 이 범위는 동일한 개체 집합 전체가 일치할 필요는 없습니다. 두 범위는 모두 일치하는 개체의 일부 또는 전체를 수정할 수 있습니다.

## 단독 범위 만들기

단독 범위는 다른 명시적 범위와 같은 방법으로 만들 수 있습니다. 미리 만들어진 상대 범위, 받는 사람, 데이터베이스 또는 서버 필터, 데이터베이스 또는 서버 목록을 지정할 수 있습니다. 관리 역할 할당에 범위를 연결할 때까지 적용되지 않는 일반 범위와 달리 단독 범위의 거부 측면은 즉시 적용됩니다. 이는 단독 범위가 만들어지는 즉시 역할 할당이 만들어질 때까지 어떠한 사용자도 해당 범위에 포함된 개체에 더 이상 액세스할 수 없음을 의미합니다.

할당이 만들어진 후 단독 범위는 관리 역할 및 범위가 할당된 사용자에게 액세스 권한을 제공합니다. 다른 동등한 단독 범위에서 동일한 개체가 일치할 경우 해당 단독 범위에 연결된 역할 할당은 개체에 계속 액세스할 수 있습니다.

관리 범위 필터에 대한 자세한 내용은 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> 단독 범위를 포함하여 관리 역할 구성 요소를 변경할 때는 Active Directory 복제 시간을 고려해야 합니다.



두 개 이상의 단독 범위 내에 포함되는 개체가 있는 경우 이러한 단독 범위 중 하나에 할당되면 개체에 액세스할 수 있습니다. 자세한 내용은 이 항목 뒷부분의 Exclusive and regular scope interaction를 참조하십시오.

단독 범위는 역할 할당의 구성 쓰기 범위 또는 명시적 받는 사람만 제어합니다. 사용자 또는 그룹에 할당된 역할의 암시적 받는 사람 또는 구성 읽기 범위는 계속 적용됩니다. 이는 다음과 같은 사항이 적용됨을 의미합니다.

  - 역할이 할당된 사용자는 역할의 암시적 읽기 범위와 일치하는 개체를 계속 볼 수 있습니다.

  - 다른 역할이 할당된 사용자는 다른 역할의 읽기 범위에 해당 개체가 포함된 경우 단독 범위 내에 포함된 개체를 볼 수 있습니다. 단, 개체 수정은 단독 범위에 연결된 역할이 할당된 사용자만 수행할 수 있습니다.

단독 범위는 관리 또는 전문가 역할에서만 사용할 수 있으며 최종 사용자 역할에서는 사용할 수 없습니다. 역할에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하십시오.

## 단독 및 일반 범위 상호 작용

이 섹션의 끝에 있는 그림에서는 단독 범위 간 그리고 단독 범위와 일반 범위 간의 상호 작용 방식을 보여 줍니다. 그림의 모든 사용자는 사용자와 연결된 다음 특성을 가집니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>User</th>
<th>City</th>
<th>Title</th>
<th>Department</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Terry</p></td>
<td><p>Vancouver</p></td>
<td><p>Accountant</p></td>
<td><p>Accounting</p></td>
</tr>
<tr class="even">
<td><p>David</p></td>
<td><p>Vancouver</p></td>
<td><p>Writer</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="odd">
<td><p>Walter</p></td>
<td><p>Vancouver</p></td>
<td><p>Manager</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="even">
<td><p>Bob</p></td>
<td><p>Vancouver</p></td>
<td><p>CEO</p></td>
<td><p>Board</p></td>
</tr>
<tr class="odd">
<td><p>Christine</p></td>
<td><p>Vancouver</p></td>
<td><p>President</p></td>
<td><p>Board</p></td>
</tr>
<tr class="even">
<td><p>Fred</p></td>
<td><p>Vancouver</p></td>
<td><p>CFO</p></td>
<td><p>Executives</p></td>
</tr>
<tr class="odd">
<td><p>Martin</p></td>
<td><p>Vancouver</p></td>
<td><p>CIO</p></td>
<td><p>Executives</p></td>
</tr>
<tr class="even">
<td><p>Kim</p></td>
<td><p>Vancouver</p></td>
<td><p>Vice President, Operations</p></td>
<td><p>Executives</p></td>
</tr>
<tr class="odd">
<td><p>Jennifer</p></td>
<td><p>Vancouver</p></td>
<td><p>Vice President, Technology</p></td>
<td><p>Executives</p></td>
</tr>
</tbody>
</table>


그림에서 다음 세 개의 관리 역할 할당은 앞 표의 사용자를 관리합니다. 각각에는 연결된 범위가 있으며, 그 일부는 단독 범위입니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>역할 할당</th>
<th>범위 필터</th>
<th>단독 또는 일반</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Recipient Administrators</p></td>
<td><p>City = Vancouver</p></td>
<td><p>일반</p></td>
</tr>
<tr class="even">
<td><p>VIP Administrators</p></td>
<td><p>Title = CEO or CFO or CIO or President</p></td>
<td><p>단독</p></td>
</tr>
<tr class="odd">
<td><p>Executive Administrators</p></td>
<td><p>Department = Executives</p></td>
<td><p>단독</p></td>
</tr>
</tbody>
</table>


모든 사용자가 Vancouver에 위치하므로 받는 Recipient Administrators 역할 할당은 모든 사용자와 일치하는 범위를 가집니다. 단독 범위가 없다면 이는 Recipient Administrators 역할 할당이 모든 사용자를 관리할 수 있음을 의미합니다. 그러나 이 조직은 두 개의 단독 범위로 VIP Administrators와 Executive Administrators를 만들었습니다. 이 두 단독 범위는 각각의 범위 필터와 일치하는 사용자를 관리할 수 있는 사람을 제한합니다. VIP Administrators 역할 할당은 직책이 CEO, CFO, CIO 또는 President인 모든 사용자와 일치하는 범위 필터를 가집니다. Executive Administrators 역할 할당은 Executives 부서에 속한 모든 사용자와 일치하는 범위 필터를 가집니다.

일반 및 단독 범위에 대한 평가 결과는 다음과 같습니다.

  - Recipient Administrators 역할 할당은 사용자 Terry, David 및 Walter를 관리할 수 있습니다. 그 외의 다른 사용자는 VIP Administrators 및 Executive Administrators 역할 할당의 단독 범위 필터와 일치하므로 이 역할 할당에서 관리할 수 없습니다.

  - VIP Administrators 역할 할당은 사용자 Bob, Christine, Fred 및 Martin을 관리할 수 있습니다. 이 역할 할당과 연결된 단독 범위 필터가 이러한 개체의 특성과 일치하기 때문입니다. 사용자 Kim과 Jennifer의 경우 특성이 이 단독 범위와 일치하지 않으므로 이 역할 할당에서 관리할 수 없습니다.

  - Executive Administrators 역할 할당은 사용자 Kim, Jennifer, Fred 및 Martin을 관리할 수 있습니다. 이 역할 할당과 연결된 단독 범위 필터가 이러한 개체의 특성과 일치하기 때문입니다. 사용자 Bob과 Christine의 경우 특성이 이 단독 범위와 일치하지 않으므로 이 역할 할당에서 관리할 수 없습니다.

Fred와 Martin은 두 단독 범위에서 모두 액세스할 수 있습니다. 이 두 사용자의 특성이 두 단독 범위의 필터와 모두 일치하기 때문입니다.

**단독 범위와 일반 범위 간의 상호 작용**

![단독 및 일반 범위 상호 작용](images/Dd638110.0aa26d1d-1fa6-44d8-802d-83d75cd2624c(EXCHG.150).jpg "단독 및 일반 범위 상호 작용")

관리 범위에 대한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

