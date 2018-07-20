---
title: '역할 그룹 구성원 관리: Exchange 2013 Help'
TOCTitle: 역할 그룹 구성원 관리
ms:assetid: c064729d-7cda-47fc-b105-acf4b300d430
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657492(v=EXCHG.150)
ms:contentKeyID: 50484067
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 그룹 구성원 관리

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-08_

이 항목에서는 추가, 제거 및 Microsoft Exchange Server 2013 에서 관리 역할 그룹의 구성원을 확인 하는 방법을 보여줍니다. Exchange 2013 의 역할 그룹에 대 한 자세한 내용은 [관리 역할 그룹 이해 (영문)](understanding-management-role-groups-exchange-2013-help.md)을 참조 하십시오.

역할 그룹에 관련된 추가 관리 작업은 [사용 권한](permissions-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "역할 그룹" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 역할 그룹에 구성원을 추가 합니다.

사용자 역할 그룹에 의해 부여 된 사용 권한 부여, 사용자 또는 USG (), 유니버설 보안 그룹 또는 사용자 역할 그룹의 구성원으로,의 구성원 인지 다른 역할 그룹을 추가 해야 합니다.

## EAC를 사용 하 여 역할 그룹에 구성원을 추가 하려면

1.  Exchange 관리 센터 (EAC), **사용 권한 관리** 로 이동 \> **관리자 역할로** 합니다.

2.  구성원을 추가 하려는 역할 그룹을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

3.  **구성원** 섹션에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭 합니다.

4.  사용자, Usg, 또는 역할 그룹에 추가 하 고 **추가** 클릭 한 다음 **확인** 을 클릭 하 고 원하는 다른 역할 그룹을 선택 합니다.

5.  **저장**을 클릭하여 역할 그룹에 대한 변경 내용을 저장합니다.

## 셸을 사용 하 여 역할 그룹에 구성원을 추가 하려면

역할 그룹 구성원을 추가 하려면 [Add-RoleGroupMember](https://technet.microsoft.com/ko-kr/library/dd638207\(v=exchg.150\))의 [예제](https://technet.microsoft.com/ko-kr/dd638207\(exchg.150\)#examples) 섹션을 참조 하십시오.

여러 역할 그룹 구성원을 추가 하거나 역할 그룹 구성원 자격을 완전히 교체 하 [Update-RoleGroupMember](https://technet.microsoft.com/ko-kr/library/dd638116\(v=exchg.150\))의 [예제](https://technet.microsoft.com/ko-kr/dd638116\(exchg.150\)#examples) 섹션을 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

을 역할 그룹에 하나 이상의 구성원을 성공적으로 추가 되었는지 확인 하려면 다음을 수행 합니다.

1.  EAC에서 **사용 권한** \> **관리 역할**로 이동합니다.

2.  구성원을 추가 하 여 역할 그룹을 선택 합니다.

3.  역할 그룹 세부 정보 창에서 추가한 구성원 나열 되어있는지 확인 합니다.

## 역할 그룹에서 구성원 제거

유니버설 보안 그룹 (USG)는 사용자의 멤버가, 역할 그룹의 멤버 자격에서 또는 사용자에 게 서 역할 그룹에 의해 부여 된 권한을 제거 하려면 해당 사용자를 제거 해야 합니다.

## EAC를 사용 하 여 역할 그룹에서 구성원을 제거 하려면

1.  EAC에서 **사용 권한** \> **관리 역할**로 이동합니다.

2.  역할 그룹에서 구성원을 제거 하려면 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

3.  **구성원** 섹션에서 제거, **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭 한 다음 **저장** 을 클릭 하 고 원하는 구성원을 선택 합니다.

## 셸을 사용 하 여 역할 그룹에서 구성원 제거

역할 그룹 구성원을 제거 하려면 [Remove-RoleGroupMember](https://technet.microsoft.com/ko-kr/library/dd638208\(v=exchg.150\))의 [예제](https://technet.microsoft.com/ko-kr/dd638208\(exchg.150\)#examples) 섹션을 참조 하십시오.

여러 역할 그룹 구성원을 제거 하거나 역할 그룹 구성원 자격을 완전히 교체 하 [Update-RoleGroupMember](https://technet.microsoft.com/ko-kr/library/dd638116\(v=exchg.150\))의 [예제](https://technet.microsoft.com/ko-kr/dd638116\(exchg.150\)#examples) 섹션을 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

역할 그룹에 하나 이상의 구성원을 성공적으로 제거 했는지를 확인 하려면 다음을 수행 합니다.

1.  EAC에서 **사용 권한** \> **관리 역할**로 이동합니다.

2.  역할 그룹에서 구성원 제거를 선택 합니다.

3.  역할 그룹 세부 정보 창에서 제거한 구성원 더이상 나열 되어 있는지를 확인 합니다.

## 역할 그룹의 구성원 보기

역할 그룹의 구성원은 역할 그룹에 할당 하는 관리 역할에 의해 제공 되는 사용 권한은 부여 됩니다. 사용자가 지정한 역할 그룹에서 사용자, 유니버설 보안 그룹 (USG) 또는 기타 역할 그룹에는 사용 권한을 부여 받습니다를 참조 하는 역할 그룹의 구성원을 볼 수 있습니다.

## EAC를 사용 하 여 역할 그룹의 구성원을 보려면

1.  EAC에서 **사용 권한** \> **관리 역할**로 이동합니다.

2.  구성원을 보려는 역할 그룹을 선택합니다.

3.  역할 그룹 세부 정보 창에서 역할 그룹 세부 정보 창에서 구성원을 봅니다.

## 셸을 사용하여 역할 그룹의 구성원 보기

역할 그룹의 구성원을 보려면 [Get-RoleGroupMember](https://technet.microsoft.com/ko-kr/library/dd638093\(v=exchg.150\))에서 "예" 섹션을 참조 하십시오.

