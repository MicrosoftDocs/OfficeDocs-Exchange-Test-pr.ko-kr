---
title: '주소 목록 만들기: Exchange 2013 Help'
TOCTitle: 주소 목록 만들기
ms:assetid: e86ba1b7-c41c-4050-bc29-13996cf53c59
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125036(v=EXCHG.150)
ms:contentKeyID: 50484449
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewAddressListWizardForm.AddressListIntroductionPage
ms.translationtype: MT
---

# 주소 목록 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-12_

주소 목록은 받는 사람 및 기타 Active Directory 개체의 컬렉션입니다. 각 주소 목록에는 하나 이상의 유형의 개체 (예: 사용자, 연락처, 그룹, 공용 폴더, 회 및 기타 리소스를) 포함 될 수 있습니다. 주소 목록은 또한 사용자의 특정 그룹을 위해 Active Directory 메일 사용이 가능한 개체를 분할 하는 메커니즘을 제공 합니다.

주소 목록에 관련 된 다른 관리 작업을 [주소 목록 절차](address-list-procedures-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "주소 목록" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 주소 목록을 만들려면

1.  **조직** 으로 이동 \> **주소 목록**, 다음![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**추가** 클릭 하 고 있습니다.

2.  **주소 목록** 이름을 입력 하 고 목록에 포함할 받는 사람 유형을 지정 합니다.

3.  기본적으로 Exchange 조직의 모든 구성원이 포함 된 주소 목록을 만듭니다. 고유한 사용자 지정 주소 목록을 만들려면 **추가 하는 규칙을** 클릭 합니다.
    

    > [!IMPORTANT]
    > 규칙을 추가 하지 않으면, 기본 주소 목록 중 하 나와 함께 중복 된 주소 목록을 만들어야 합니다.



4.  목록에서 필터링 옵션 (예: **사용자 지정 특성 1** )을 선택 합니다.

5.  에 **지정 단어 또는 구를** 입력 단어 또는 구를 기준으로 필터링, **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭 한 다음 **확인** 을 클릭 합니다.
    
    4 단계를 반복 하 여 여러 구 또는 단어를 추가 하려면 계속 수 있습니다. 필터는 부울 **또는** 문입니다. 예, 주소 목록 사용자 정의 1 속성을 가진 equals **오리건**, **Idaho** 또는 **워싱턴** 사용자에 게 적용 되는 필터를 만들 수 있습니다.

6.  (선택 사항) 필터를 추가 하려면 다시 **규칙 추가** 클릭 합니다. 추가 필터는 부울 **및** 문을 만듭니다. 더 많은 필터 추가 이하의 수가 사용자가 주소 목록에 적용 됩니다.

7.  이 주소 목록에 적용 될 받는 사람을 참조 하려면 **주소 목록을 포함 하는 받는 사람 미리 보기** 를 클릭 합니다.

8.  **저장**을 클릭합니다.

9.  주소 목록 수 없습니다는 경고 메시지가 나타납니다 경우 업데이트할 때까지 적용 합니다. 조직 및 주소 목록에 추가 하는 필터의 크기에 따라 수천 또는 매우 많은 수의 받는 사람에 게 일부 주소 목록을 포함 될 수 있습니다. 주소 목록을 업데이트 영향을 줄 수에 리소스 사용량이 많지 않은 시간 동안에 주소를 업데이트 하는 것이 좋습니다.
    
    주소 목록을 업데이트 하는 방법에 대 한 자세한 내용은, [주소 목록 업데이트](update-an-address-list-exchange-2013-help.md)을 참조 하십시오.

## 셸을 사용 하 여 주소 목록을 만들려면

이 예에서는 *RecipientFilter* 매개 변수를 사용하여 주소 목록 MyAddressList를 만들고, 사서함 사용자인 받는 사람을 포함하고, `StateOrProvince`를 `Washington` 또는 `Oregon`으로 설정합니다.

    New-AddressList -Name MyAddressList -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

이 예에서는 기본 제공 조건을 사용하여 All Rooms 부모 컨테이너에 자식 주소 목록 Building 34 Meeting Rooms를 만듭니다.

    New-AddressList -Name "Building 34 Meeting Rooms" -Container "\All Rooms" -IncludedRecipients Resources -ConditionalCustomAttribute1 "Building 34"

구문과 매개 변수에 대한 자세한 내용은 [New-AddressList](https://technet.microsoft.com/ko-kr/library/aa996912\(v=exchg.150\))를 참조하십시오.

