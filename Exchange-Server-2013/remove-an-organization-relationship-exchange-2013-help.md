---
title: '조직 관계 제거: Exchange 2013 Help'
TOCTitle: 조직 관계 제거
ms:assetid: ff211394-f58b-4da7-bb3a-df6abcb5950e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657513(v=EXCHG.150)
ms:contentKeyID: 50484618
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 조직 관계 제거

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-04_

조직 관계는 Exchange 조직의 사용자가 일정 약속 있음/없음 정보를 Office 365 조직 또는 다른 Exchange 온-프레미스 조직과 공유할 수 있도록 하는 기능입니다. 조직 관계를 제거하여 다른 조직과의 일정 공유를 사용하지 않도록 설정할 수 있습니다.

다른 조직과 일정을 공유할 수 있습니다, 전에 Azure Active Directory 인증 시스템과 (로 알려져: "페더레이션")의 인증 관계를 설정 해야 하며 최소 소프트웨어 요구 사항을 충족 해야 합니다. 페더레이션 공유 하는 방법에 대 한 자세한 내용은, [공유](sharing-exchange-2013-help.md)를 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "일정 및 공유 사용 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 조직 관계 제거

1.  온-프레미스 조직의 Exchange 2013 서버에서 **조직** \> **공유**로 이동합니다.

2.  **조직 공유**에서 조직 관계를 선택한 다음 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")을 클릭하여 조직 관계를 제거합니다.

3.  나타나는 경고에서 **예**를 클릭합니다.

## 셸을 사용하여 조직 관계 제거

이 예에서는 Exchange 조직에서 조직 관계 Contoso를 제거합니다.

```powershell
Remove-OrganizationRelationship -Identity "Contoso"
```

구문과 매개 변수에 대한 자세한 내용은 [Remove-OrganizationRelationship](https://technet.microsoft.com/ko-kr/library/ee332362\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

조직 관계가 제거되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **조직** \> **공유**로 이동한 다음 조직 관계가 **조직 공유** 아래의 목록 보기에 표시되지 않는지 확인합니다.

  - 다음 셸 명령을 실행하여 조직 관계 정보가 제거되었는지 확인합니다.
    
    ```powershell
Get-OrganizationRelationship | Format-List
```


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


