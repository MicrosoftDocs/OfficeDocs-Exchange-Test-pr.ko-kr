---
title: '관리 역할 범위 필터 이해 (영문): Exchange 2013 Help'
TOCTitle: 관리 역할 범위 필터 이해 (영문)
ms:assetid: 6acc2922-ee9c-41f1-8a0f-10a541e8c273
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298043(v=EXCHG.150)
ms:contentKeyID: 50483320
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리 역할 범위 필터 이해 (영문)

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

관리 역할 범위 필터는 매우 자세하게 사용자 지정할 수 있는 관리 범위를 정의하는 데 사용할 수 있습니다. 범위 필터를 사용하여 받는 사람, 데이터베이스 및 서버를 조각화하는 방법과 일치하는 범위를 만들어서 관리자가 액세스해야 하는 해당 객체만 관리하도록 할 수 있습니다. 범위 필터에는 거의 모든 받는 사람, 데이터베이스 또는 서버 개체 속성을 사용할 수 있습니다.

관리 콘솔 범위 필터를 사용하려면 관리 역할 범위에 대해 잘 알고 있어야 합니다. 관리 역할 범위에 대한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

Microsoft Exchange Server 2013의 필터링된 사용자 지정 범위는 **New-ManagementScope** cmdlet을 사용하여 만듭니다. 필터링된 범위의 두 가지 유형인 받는 사람 및 구성(서버 및 데이터베이스 범위로 구성됨)은 일반 범위와 단독 범위로 나뉩니다. 다음 목록에서는 필터링된 범위의 각 유형을 만드는 데 사용하는 **New-ManagementScope** cmdlet의 매개 변수를 보여 줍니다.

  - **받는 사람 일반 필터링된 범위**   이 유형의 필터링된 범위를 만들려면 *RecipientRestrictionFilter* 매개 변수를 사용합니다.

  - **받는 사람 배타적 필터링된 범위**   이 유형의 필터링된 범위를 만들려면 *Exclusive* 스위치와 함께 *RecipientRestrictionFilter* 매개 변수를 사용합니다.

  - **서버 기반 구성 일반 필터링된 범위**   이 유형의 필터링된 범위를 만들려면 *ServerRestrictionFilter* 매개 변수를 사용합니다.

  - **서버 기반 구성 배타적 필터링된 범위**   이 유형의 필터링된 범위를 만들려면 *Exclusive* 스위치와 함께 *ServerRestrictionFilter* 매개 변수를 사용합니다.

  - **데이터베이스 기반 구성 일반 필터링된 범위**   이 유형의 필터링된 범위를 만들려면 *DatabaseRestrictionFilter* 매개 변수를 사용합니다.

  - **데이터베이스 기반 구성 단독 필터링된 범위**   이 유형의 필터링된 범위를 만들려면 *DatabaseRestrictionFilter* 매개 변수를 *Exclusive* 스위치와 함께 사용합니다.

필터링된 사용자 지정 범위를 만드는 경우 해당 범위는 관리 역할의 암시적 읽기 범위에서 액세스할 수 있는 모든 개체를 사용하여 필터와 일치시키려고 시도합니다. 개체가 발견되는 경우 해당 개체는 필터에서 반환한 결과에 포함되고 사용자 지정 범위별로 관리 역할에서 사용할 수 있게 됩니다. 필터는 관리 역할의 암시적 읽기 범위를 벗어난 결과를 반환할 수 없습니다.

*RecipientRestrictionFilter* 매개 변수를 사용하여 받는 사람 필터를 지정하는 경우 필터를 제한하기 위해 OU(조직 구성 단위)를 지정하는 데 *RecipientRoot* 매개 변수를 사용할 수 있습니다. *RecipientRoot* 매개 변수의 OU를 지정하는 경우 받는 사람 필터는 전체의 암시적 읽기 범위 내에서가 아닌 OU에 있는 받는 사람만 일치시키려고 시도합니다.

이 항목에 포함된 필터링할 수 있는 속성을 사용하여 관리 범위를 만들려면 [일반 또는 배타적 범위 만들기](create-a-regular-or-exclusive-scope-exchange-2013-help.md)를 참조하십시오.

## 필터 구문

받는 사람과 구성 필터 모두는 동일한 구문을 사용하여 필터 쿼리를 만듭니다. 모든 필터 쿼리에는 최소한 다음과 같은 구성 요소가 있어야 합니다.

  - **여는 괄호**   여는 중괄호({)는 필터 쿼리의 시작을 나타냅니다.

  - **검사할 속성**   해당 속성은 테스트할 개체의 값입니다. 예를 들어 받는 사람 개체의 도시나 부서, 서버 구성 개체의 Active Directory 사이트 이름이나 서버 이름 또는 데이터베이스 구성 개체의 데이터베이스 이름이 여기에 해당합니다.

  - **비교 연산자**   비교 연산자는 속성에 저장된 값에 대해 지정하는 값을 쿼리가 평가해야 하는 방법을 지시합니다. 예를 들어 비교 연산자는 같음을 의미하는 **Eq**, 같지 않음을 의미하는 **Ne** 또는 비슷함을 의미하는 **Like** 등입니다. Exchange 관리 셸에서 사용할 수 있는 연산자의 전체 목록은 [비교 연산자](https://technet.microsoft.com/ko-kr/library/bb125229\(v=exchg.150\))를 참조하십시오.

  - **비교할 값**   쿼리 필터에서 지정하는 값은 지정한 속성에 저장된 값과 비교됩니다. 지정하는 값은 큰따옴표('')로 묶어야 합니다. 부분 문자열을 지정하려는 경우 입력하는 문자열을 와일드카드 문자(\*)로 묶고 **Like**와 같은 와일드카드 문자를 지원하는 비교 연산자를 사용할 수 있습니다. 부분 문자열이 포함된 문자열은 필터 쿼리와 일치합니다.

  - **닫는 괄호**   닫는 괄호(})는 필터 쿼리의 끝을 나타냅니다.

다음 구성 요소는 옵션이며 더 복잡한 필터 쿼리를 만들 수 있게 합니다.

  - **괄호**   수학에서와 같이 필터 쿼리의 괄호 ( )는 작업이 수행되는 순서를 지정할 수 있게 합니다. 가장 안쪽의 괄호가 첫 번째로 평가되고 필터 쿼리는 가장 바깥쪽 괄호 방향으로 수행됩니다.

  - **논리 연산자**   논리 연산자는 하나 이상의 비교 연산자를 묶고 필터 쿼리가 전체 문을 평가하게 합니다. 예를 들어, 논리 연산자에는 **And**, **Or** 및 **Not**이 포함됩니다.

종합하면 간단한 쿼리는 `{ City -Eq "Vancouver" }`와 같습니다. 이 필터는 속성 **City**의 값이 문자열 "Vancouver"와 같은 모든 받는 사람과 일치시킵니다.

다른 좀 더 복잡한 쿼리는 `{ ((City -Eq "Vancouver") -And (Department -Eq "Sales")) -Or (Title -Like "*Manager*") }`입니다. 필터 쿼리는 다음과 같은 순서로 평가됩니다.

1.  속성 **City** 및 **Department**가 평가됩니다. 각각의 값은 각 속성에 저장된 값에 따라 `True` 또는 `False`로 설정됩니다.

2.  그런 다음 **City** 및 **Department** 문의 결과가 평가됩니다. 둘 다 `True`인 경우 전체 **And** 문이 `True`가 됩니다. 하나 또는 둘 다 `False`인 경우 전체 **And** 문이 `False`가 됩니다. 다음 사항이 적용됩니다.
    
      - **And** 문이 `True`로 평가하는 경우 **Or** 연산자가 쿼리의 한쪽이나 다른 한쪽이 `True`임을 나타내기 때문에 전체 필터 쿼리는 `True`가 됩니다. 개체는 역할 할당에 노출됩니다.
    
      - **And** 문이 `False`인 경우 필터 쿼리는 계속 **Title** 속성을 평가합니다.

3.  그런 다음 **Title** 속성이 평가됩니다. **Title** 속성에 저장된 값에 따라 `True` 또는 `False`로 설정됩니다. 다음 사항이 적용됩니다.
    
      - **Title** 속성이 `True`로 평가하는 경우 **Or** 연산자가 쿼리의 한쪽이나 다른 한쪽이 `True`임을 나타내기 때문에 전체 필터 쿼리는 `True`가 됩니다. 개체는 역할 할당에 노출됩니다.
    
      - **Title** 속성이 `False`로 평가하는 경우 전체 필터 쿼리가 `False`로 평가하고 개체는 역할 할당에 노출되지 않습니다.

다음 표에서는 복잡한 쿼리가 `True`로 평가하는 경우 및 `False`로 평가하는 경우를 나타내는 값이 포함된 예를 보여 줍니다.

### 복잡한 쿼리

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>City</th>
<th>Department</th>
<th>Title</th>
<th>결과</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Sales (True)</p></td>
<td><p>CEO (False)</p></td>
<td><p><strong>City</strong> 및 <strong>Department</strong> 모두가 True로 평가되므로 True입니다. 필터 쿼리 조건이 이미 충족되었기 때문에 <strong>Title</strong>은 평가되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>Seattle (False)</p></td>
<td><p>Sales (True)</p></td>
<td><p>IT Manager (True)</p></td>
<td><p><strong>Title</strong>이 True로 평가되므로 True입니다. 필터 쿼리 조건을 충족하는 <strong>Title</strong>은 True로 평가되기 때문에 <strong>City</strong>와 <strong>Department</strong>의 비교 결과는 무시됩니다.</p>

> [!NOTE]
> 와일드카드 문자(*)가 필터 쿼리에서 사용되는 부분 문자열과 일치하는 <STRONG>Like</STRONG> 비교 연산자가 사용되기 때문에 IT Manager는 필터 쿼리와 일치됩니다.


</td>
</tr>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Marketing (False)</p></td>
<td><p>Writer (False)</p></td>
<td><p><strong>City</strong> 및 <strong>Department</strong> 둘 다 True로 평가하지 않고 <strong>Title</strong>도 True로 평가하지 않기 때문에 False입니다.</p></td>
</tr>
</tbody>
</table>


## 필터링할 수 있는 받는 사람 속성

받는 사람 필터를 만들 때 받는 사람 개체에서 거의 모든 속성을 사용할 수 있습니다. 필터링할 수 있는 받는 사람 속성 목록은 [-RecipientFilter 매개 변수에 대 한 필터링 할 수 있는 속성](https://technet.microsoft.com/ko-kr/library/bb738157\(v=exchg.150\))을 참조하십시오. 이 항목에서는 다른 cmdlet에서 *RecipientFilter* 매개 변수로 사용할 수 있는 속성에 대해 설명하지만 이러한 속성 대부분은 **New-ManagementScope** cmdlet에서 *RecipientRestrictionFilter* 매개 변수와도 작동할 수 있습니다.

## 필터링할 수 있는 서버 속성

*ServerRestrictionFilter* 매개 변수도 관리 범위를 만들 때 다음 서버 속성을 사용할 수 있습니다.

  - **CurrentServerRole**

  - **CustomerFeedbackEnabled**

  - **DataPath**

  - **DistinguishedName**

  - **ExchangeLegacyDN**

  - **ExchangeLegacyServerRole**

  - **ExchangeVersion**

  - **Fqdn**

  - **Guid**

  - **InternetWebProxy**

  - **Name**

  - **NetworkAddress**

  - **ObjectCategory**

  - **ObjectClass**

  - **ProductID**

  - **ServerRole**

  - **ServerSite**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

## 필터링할 수 있는 데이터베이스 속성

*DatabaseRestrictionFilter* 매개 변수로 관리 범위를 만드는 경우 다음 데이터베이스 속성을 사용할 수 있습니다.

  - **AdminDisplayName**

  - **AllowFileRestore**

  - **BackgroundDatabaseMaintenance**

  - **CircularLoggingEnabled**

  - **DatabaseCreated**

  - **DeletedItemRetention**

  - **Description**

  - **DistinguishedName**

  - **EdbFilePath**

  - **EventHistoryRetentionPeriod**

  - **ExchangeLegacyDN**

  - **ExchangeVersion**

  - **Guid**

  - **IssueWarningQuota**

  - **LogFilePrefix**

  - **LogFileSize**

  - **LogFolderPath**

  - **MasterServerOrAvailabilityGroup**

  - **MountAtStartup**

  - **Name**

  - **ObjectCategory**

  - **ObjectClass**

  - **RetainDeletedItemsUntilBackup**

  - **Server**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

