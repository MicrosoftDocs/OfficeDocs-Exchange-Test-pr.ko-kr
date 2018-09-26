---
title: '주소 목록 업데이트: Exchange 2013 Help'
TOCTitle: 주소 목록 업데이트
ms:assetid: 163e7099-cf14-4bb0-a84c-1401e9db670e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996375(v=EXCHG.150)
ms:contentKeyID: 50482538
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.UpdateAddressListWizardForm.ScheduleWizardPage
ms.translationtype: MT
---

# 주소 목록 업데이트

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-14_

주소 목록은 받는 사람 및 기타 Active Directory 개체의 모음입니다. 주소 목록 필터 규칙이 편집된 경우 주소 목록을 적용합니다. 새 받는 사람을 포함시키고 필터링 기준에 더 이상 만족하지 않는 받는 사람을 제거하도록 주소 목록의 구성원을 업데이트하려면 주소 목록을 적용해야 합니다.

주소 목록과 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 목록 절차](address-list-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 주소 목록의 받는 사람 수에 따라 이 프로세스가 완료되는 데 오래 걸릴 수 있습니다.

  - 조직의 크기 및 주소 목록에 추가한 필터에 따라 일부 주소 목록에는 수천 명이나 수만 명의 받는 사람이 포함되어 있습니다. 주소 목록 업데이트에는 컴퓨터 리소스가 많이 사용될 수 있습니다. 따라서 사용량이 적은 시간 동안 주소 목록을 업데이트해야 합니다.

  - 주소 목록에 3,000명 이상의 받는 사람이 포함되어 있는 경우 Exchange 관리 셸을 사용하여 주소 목록을 업데이트하는 것이 좋습니다.

이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 주소 목록 업데이트

1.  **조직** \> **주소록**으로 이동합니다.

2.  목록 보기에서 업데이트할 주소 목록을 선택합니다.

3.  세부 정보 창에서 **업데이트**를 클릭합니다.

## 셸을 사용하여 주소 목록 업데이트

이 예에서는 주소 목록 Washington State를 업데이트합니다.

```powershell
Update-AddressList "Washington State"
```

이름이 같은 주소 목록이 여러 개 있는 경우 업데이트할 주소 목록의 전체 경로를 지정해야 합니다. 예를 들어 North America 아래에 있는 주소 목록 Sales를 업데이트하려고 하는데 Europe 아래에도 Sales 주소 목록이 있는 경우 다음 명령을 사용합니다.

```powershell
Update-AddressList "North America\Sales"
```

구문과 매개 변수에 대한 자세한 내용은 [Update-AddressList](https://technet.microsoft.com/ko-kr/library/aa997982\(v=exchg.150\))를 참조하십시오.

