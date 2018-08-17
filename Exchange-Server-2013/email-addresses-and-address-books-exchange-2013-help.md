---
title: '전자 메일 주소 및 주소록: Exchange 2013 Help'
TOCTitle: 전자 메일 주소 및 주소록
ms:assetid: b97d0f68-691a-42af-9a6c-4dcc37b28a42
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657488(v=EXCHG.150)
ms:contentKeyID: 50484003
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전자 메일 주소 및 주소록

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

받는 사람(사용자, 리소스, 연락처 및 그룹 포함)은 Microsoft Exchange가 메시지를 배달하거나 라우팅할 수 있는 Active Directory에서 메일 사용이 가능한 개체입니다. 받는 사람이 전자 메일 메시지를 보내거나 받으려면 받는 사람에게 전자 메일 주소가 있어야 합니다. 주소록은 사용자가 전자 메일을 보내기 위해 서로를 찾는 방법입니다. 주소록을 구성하는 방법은 아주 다양합니다. Exchange Server 2013의 주소록 기능에 대한 자세한 정보는 Key terminology를 참조하십시오.

## 주요 용어

다음 용어는 Exchange 2013에서 전자 메일 주소 및 주소록과 연관된 핵심 구성 요소를 설명합니다.

  - **주소록 정책**  
    ABP(주소록 정책)를 사용하면 사용자를 특정 그룹으로 분할하여 조직의 GAL(전체 주소 목록)에 대한 사용자 지정 보기를 제공할 수 있습니다. ABP를 만들 때 GAL, OAB(오프라인 주소록), 방 목록 및 하나 이상의 주소 목록을 정책에 할당합니다. 그런 다음 ABP를 사서함 사용자에게 할당하여 사서함 사용자에게 Outlook과 Outlook Web App에서 사용자 지정된 GAL에 액세스할 수 있는 권한을 제공할 수 있습니다. 여러 개의 GAL이 필요한 온-프레미스 조직에서 보다 간단하게 GAL 조각화를 수행할 수 있는 메커니즘을 제공하는 것이 목표입니다.

<!-- end list -->

  - **주소 목록**  
    주소 목록은 GAL의 하위 집합입니다. 각 주소 목록은 메일 사용이 가능한 하나 이상의 받는 사람 유형(예: 사용자, 연락처, 그룹, 공용 폴더, 회의 및 기타 리소스)을 모은 것입니다. 주소 목록을 사용하여 받는 사람 및 리소스를 구성하면 사용자가 필요한 받는 사람 및 리소스를 보다 쉽게 찾을 수 있습니다. 주소 목록은 동적으로 업데이트됩니다. 따라서 조직에 받는 사람이 새로 추가되면 해당 주소 목록에 자동으로 추가됩니다.

<!-- end list -->

  - **전자 메일 주소 정책**  
    전자 메일 주소 정책이 받는 사람의 기본 및 보조 전자 메일 주소를 생성하므로 받는 사람이 전자 메일을 받거나 보낼 수 있습니다. 기본적으로 Exchange에는 메일 사용이 가능한 모든 사용자에 대한 전자 메일 주소 정책이 있습니다.

<!-- end list -->

  - **계층 구조 주소록**  
    HAB(계층 구조 주소록)를 사용하면 최종 사용자가 연공서열 또는 관리 구조 등의 조직 계층 구조를 사용하여 주소록에서 받는 사람을 찾을 수 있습니다. 일반적으로 사용자는 기본 GAL 및 관련 받는 사람 속성만 사용할 수 있습니다. 또한 GAL의 구조가 조직 내 받는 사람의 관리 또는 연공서열 관계를 정확하게 반영하지 않을 때도 있습니다. 조직의 고유 비즈니스 구조에 매핑되는 HAB를 사용자 지정할 수 있게 되면 사용자는 내부에서 받는 사람을 효과적으로 찾을 수 있습니다.

<!-- end list -->

  - **오프라인 주소록**  
    OAB(오프라인 주소록)는 Microsoft Outlook 사용자가 서버 연결이 끊긴 동안 OAB에 포함된 정보에 액세스할 수 있도록 다운로드한 주소 목록 모음의 복사본입니다.

## 전자 메일 주소 및 주소록 설명서

다음 표에는 Exchange 2013에서 전자 메일 주소 및 주소록에 대해 알아보고 이를 관리하는 데 도움이 되는 항목에 대한 링크가 나와 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="address-lists-exchange-2013-help.md">주소 목록</a></p></td>
<td><p>최종 사용자가 쉽게 액세스할 수 있도록 받는 사람을 구성하는 방법으로 주소 목록 및 GAL에 대해 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="address-book-policies-exchange-2013-help.md">주소록 정책</a></p></td>
<td><p>가상 조직별로 주소 목록과 GAL을 구분하는 방법에 대해 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="details-templates-exchange-2013-help.md">세부 항목 템플릿</a></p></td>
<td><p>Outlook에서 주소 카드를 사용자 지정하는 방법에 대해 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="email-address-policies-exchange-2013-help.md">전자 메일 주소 정책</a></p></td>
<td><p>받는 사람이 더 잘 검색될 수 있도록 하는 프록시 전자 메일 주소에 대해 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hierarchical-address-books-exchange-2013-help.md">계층 구조 주소록</a></p></td>
<td><p>조직의 고유한 비즈니스 구조에 맞도록 GAL과 주소 목록을 사용자 지정하는 방법에 대해 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="offline-address-books-exchange-2013-help.md">오프라인 주소록</a></p></td>
<td><p>사용자에게 조직의 주소 목록에 대한 오프라인 액세스를 제공하는 것에 대해 알아봅니다.</p></td>
</tr>
</tbody>
</table>

