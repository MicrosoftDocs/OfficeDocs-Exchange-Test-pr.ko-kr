---
title: '전자 메일 주소 정책 편집: Exchange 2013 Help'
TOCTitle: 전자 메일 주소 정책 편집
ms:assetid: cc8b36a0-95f4-43e9-bc64-87646d2e14e4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124580(v=EXCHG.150)
ms:contentKeyID: 50484177
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.EditEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# 전자 메일 주소 정책 편집

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-12-10_

전자 메일 주소 정책은 받는 사람(사용자, 연락처, 그룹 등)이 전자 메일을 보내고 받을 수 있도록 받는 사람의 기본 및 보조 전자 메일 주소를 생성합니다.

전자 메일 주소 정책에 관련된 추가 관리 작업은 [전자 메일 주소 정책 절차](email-address-policy-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 사항은 무엇입니까?

  - 예상 완료 시간: 5분

  - 셸을 사용하여 정책을 만든 경우 전자 메일 주소 정책을 편집하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다.

  - 받는 사람 필터를 사용하여 전자 메일 주소 정책을 만든 경우 셸을 사용하여 전자 메일 주소 정책을 편집해야 합니다. 자세한 내용은 [받는 사람 필터를 사용 하 여 전자 메일 주소 정책 만들기](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [전자 메일 주소 및 주소록](email-addresses-and-address-books-exchange-2013-help.md)의 "전자 메일 주소 정책" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

> [!CAUTION]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, 또는 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>


## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 정책이 적용되는 받는 사람 변경

1.  **메일 흐름** \> **전자 메일 주소 정책**으로 이동합니다.

2.  목록 보기에서 변경하려는 전자 메일 주소 정책을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **전자 메일 주소 정책**에서 **적용 대상**을 클릭하고 설정을 수정합니다.

## EAC를 사용하여 전자 메일 주소 정책의 우선 순위 변경

사용자는 동일한 전자 메일 주소 계정에 대해 여러 프록시 전자 메일 주소를 가질 수 있습니다(예: ayla@exchange.mail.contoso.com 또는 ayla@contoso.com). 그리고 이러한 전자 메일 주소는 우선 순위에 따라 적용될 수 있습니다. 예를 들어, 다음 시나리오를 살펴봅시다. 전자 메일 주소 정책이 두 개이고, 이 정책에 우선 순위 1과 2를 할당합니다. 그 후 다른 정책을 만들면 자동으로 우선 순위 3이 할당됩니다. 그러나 전자 메일 주소 정책이 두 개이고 둘 중 하나에 우선 순위 1을 할당할 경우 또 다른 정책을 만들면 기본 우선 순위 2가 할당됩니다. 이 경우 다음에 만든 정책은 기본적으로 우선 순위 2 정책이 됩니다. 이전의 우선 순위 2 정책에는 우선 순위 3이 할당됩니다.

1.  **메일 흐름** \> **전자 메일 주소 정책**으로 이동합니다.

2.  우선 순위를 변경할 전자 메일 주소 정책을 선택한 다음 **우선 순위 높이기**![위쪽 화살표 아이콘](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "위쪽 화살표 아이콘") 또는 **우선 순위 낮추기**![아래쪽 화살표 아이콘](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "아래쪽 화살표 아이콘")을 클릭합니다.

## 셸을 사용하여 전자 메일 주소 정책 편집

이 예에서는 현재 조지아 주, 앨라배마 주 및 루이지애나 주에 있는 받는 사람을 포함하는 South East Offices 전자 메일 주소 정책을 편집하여 텍사스 주에 있는 받는 사람도 포함하도록 합니다.

```powershell
Set-EmailAddressPolicy -Identity "South East Offices" -ConditionalStateorProvince "Georgia","Alabama","Louisiana","Texas"
```

> [!NOTE]
> 전자 메일 주소 정책이 조지아 주, 앨라배마 주 및 루이지애나 주의 받는 사람에게 이미 적용되어 있더라도 매개 변수가 기존 값에 값을 추가하지 않고 덮어쓰기 때문에 매개 변수에 해당하는 받는 사람을 포함해야 합니다.



구문과 매개 변수에 대한 자세한 내용은 [Set-EmailAddressPolicy](https://technet.microsoft.com/ko-kr/library/bb124517\(v=exchg.150\))를 참조하십시오.

