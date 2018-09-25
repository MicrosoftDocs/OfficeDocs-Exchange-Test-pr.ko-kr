---
title: '사용자 정의 특성: Exchange 2013 Help'
TOCTitle: 사용자 정의 특성
ms:assetid: 2b043878-0b34-4563-a9c2-28a9efa7447e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423541(v=EXCHG.150)
ms:contentKeyID: 50482763
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자 정의 특성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-17_

Microsoft Exchange Server 2013에는 15개의 확장 특성이 있습니다. 이러한 특성을 사용하여 직원 ID, OU(조직 구성 단위) 또는 기존 특성이 없는 다른 사용자 지정 값 등의 받는 사람과 관련된 정보를 추가할 수 있습니다. Active Directory에서는 이러한 사용자 지정 특성에 **ms-Exch-Extension-Attribute1**부터 **ms-Exch-Extension-Attribute15**까지의 레이블이 지정됩니다. Exchange 관리 셸에서 여기에 해당되는 매개 변수는 *CustomAttribute1*부터 *CustomAttribute15*까지입니다. 이러한 특성은 Exchange 구성 요소에서 사용되지 않습니다. 이러한 특성을 사용하면 Active Directory 스키마를 확장하지 않고도 Active Directory 데이터를 저장할 수 있습니다.

Exchange Server 2003 이하 버전에서는 이 정보를 Active Directory에 저장하려면 Active Directory 스키마를 확장하여 특성을 만들어야 했습니다. 스키마를 확장하려면 프로덕션 환경에 구현하기 전에 계획, OID(개체 ID) 확보, 테스트 환경에서의 확장 프로세스 테스트 과정을 거쳐야 합니다. Exchange 2013에서는 주소 목록, 전자 메일 주소 정책 및 동적 메일 그룹에 스키마 확장을 사용할 수 없습니다.

**목차**

Advantages of custom attributes

Custom attributes examples

Custom attributes example with the ConditionalCustomAttributes parameter

Custom attribute example with ExtensionCustomAttributes parameter

## 사용자 지정 특성의 이점

사용자 지정 특성의 이점에는 다음이 포함됩니다.

  - Active Directory 스키마를 확장하지 않아도 됩니다.

  - Exchange 설치에서 특성이 만들어집니다.

  - EAC(Exchange 관리 센터) 또는 Exchange 관리 셸을 사용하여 특성을 관리할 수 있습니다. 사용자 지정 컨트롤이나 스크립트를 작성하여 이러한 특성을 입력하고 표시할 필요가 없습니다.

  - 특성은 **Get-Mailbox** 등의 받는 사람 cmdlet에서 *Filter* 매개 변수에 사용할 수 있으며 필터링이 가능한 속성입니다. EAC 및 셸에서 사용하여 전자 메일 주소 정책, 주소 목록 및 동적 메일 그룹에 대한 필터를 만들 수도 있습니다.

## 다중값 사용자 지정 특성

Exchange 2010 SP2(서비스 팩 2)에서는 기존 사용자 지정 특성이 필요를 충족하지 못할 경우 메일 받는 사람에 대한 추가적인 정보를 저장할 수 있는 다섯 개의 사용자 지정 특성이 Exchange에 추가되었습니다. *ExtensionCustomAttribute1* - *ExtensionCustomAttribute5* 매개 변수는 각각 최대 1,300개의 값을 저장할 수 있습니다. 쉼표로 구분된 목록으로 여러 값을 지정할 수 있습니다. 이러한 새 매개 변수를 지원하는 cmdlet은 다음과 같습니다.

  - [Set-DistributionGroup](https://technet.microsoft.com/ko-kr/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/ko-kr/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/ko-kr/library/aa995950\(v=exchg.150\))

  - [Set-MailPublicFolder](https://technet.microsoft.com/ko-kr/library/bb123707\(v=exchg.150\))

  - [Set-RemoteMailbox](https://technet.microsoft.com/ko-kr/library/ff607302\(v=exchg.150\))

다중값 속성에 대한 자세한 내용은 [다중값 속성 수정](modifying-multivalued-properties-exchange-2013-help.md) 항목을 참조하십시오.

## 사용자 지정 특성 예

OU에 있는 모든 받는 사람에 대해 전자 메일 주소 정책을 만드는 경우는 Exchange 배포에서 흔히 일어납니다. OU는 전자 메일 주소 정책이나 주소 목록의 *RecipientFilter* 매개 변수에 사용할 수 있는 필터링 가능한 속성이 아닙니다.


> [!NOTE]
> 동적 메일 그룹에는 특정 OU 또는 컨테이너에서 받는 사람을 제한할 때 사용할 수 있는 추가 매개 변수가 있습니다.



OU에 있는 받는 사람이 부서 또는 위치와 같이 필터링 기준으로 사용할 수 있는 일반 속성을 공유하지 않을 경우에는 이 예와 같이 사용자 지정 특성 중 하나에 일반 값을 넣을 수 있습니다.

```powershell
Get-Mailbox -OrganizationalUnit Sales | Set-Mailbox CustomAttribute1 "SalesOU"
```

이제 다음 예와 같이 *CustomAttribute1* 속성이 SalesOU인 모든 받는 사람에 대해 전자 메일 주소 정책을 만들 수 있습니다.

```powershell
New-EmailAddressPolicy -Name "Sales" -RecipientFilter { CustomAttribute1 -eq "SalesOU"} -EnabledEmailAddressTemplates "SMTP:%s%2g@sales.contoso.com"
```

## ConditionalCustomAttributes 매개 변수를 사용한 사용자 지정 특성 예

동적 메일 그룹, 전자 메일 주소 정책 또는 주소 목록을 만들 때 *RecipeintFilter* 매개 변수를 사용하여 사용자 지정 특성을 지정할 필요가 없습니다. *ConditionalCustomAttribute1*부터 *ConditionalCustomAttribute15*까지의 매개 변수를 대신 사용하면 됩니다.

이 예에서는 *CustomAttribute1*이 SalesOU로 설정된 받는 사람에 기반하여 동적 배포 그룹을 만듭니다.

```powershell
New-DynamicDistributionGroup -Name "Sales Users and Contacts" -IncludedRecipients "MailboxUsers,MailContacts" -ConditionalCustomAttribute1 "SalesOU"
```


> [!NOTE]
> <EM>Conditional</EM> 매개 변수를 사용할 경우에는 <EM>IncludedRecipients</EM> 매개 변수를 사용해야 합니다. 또한 <EM>RecipientFilter</EM> 매개 변수를 사용하면 <EM>Conditional</EM> 매개 변수를 사용할 수 없습니다. 추가 필터를 포함하여 동적 메일 그룹, 전자 메일 주소 정책 또는 주소 목록을 만들려는 경우에는 <EM>RecipientFilter</EM> 매개 변수를 사용해야 합니다.



## ExtensionCustomAttributes 매개 변수를 사용한 사용자 지정 특성 예

이 예에서 Kweku의 사서함의 *ExtensionCustomAttribute1*은 그가 교육 강좌 MATH307, ECON202 및 ENGL300에 등록했음을 반영하여 업데이트됩니다.

```powershell
Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 MATH307,ECON202,ENGL300
```

다음으로 MATH307에 등록한 모든 학생의 동적 배포 그룹이 *RecipientFilter* 매개 변수를 사용하여 생성됩니다. 여기서 *ExtensionCustomAttribute1*은 MATH307입니다. *ExtentionCustomAttributes* 매개 변수를 사용할 때는 `-like` 연산자 대신 `-eq` 연산자를 사용할 수 있습니다.

```powershell
New-DynamicDistributionGroup -Name Students_MATH307 -RecipientFilter {ExtensionCustomAttribute1 -eq "MATH307"}
```

이 예에서 Kweku의 *ExtensionCustomAttribute1* 값은 강좌 ENGL210을 추가하고 강좌 ECON202를 제거했음을 반영하여 업데이트됩니다.

```powershell
Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 @{Add="ENGL210"; Remove="ECON202"}
```

