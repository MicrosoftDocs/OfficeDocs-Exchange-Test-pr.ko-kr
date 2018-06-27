---
title: 'Exchange eDiscovery 사용 권한 할당: Exchange 2013 Help'
TOCTitle: Exchange eDiscovery 사용 권한 할당
ms:assetid: 729e09d8-614b-431f-ae04-ae41fb4c628e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298059(v=EXCHG.150)
ms:contentKeyID: 50483420
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange eDiscovery 사용 권한 할당

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-10-02_

사용자가 Microsoft Exchange Server 2013 In-place eDiscovery를 사용 하 여 수을 하려는 경우 먼저 권한을 부여 해야 해당 검색 관리 역할 그룹에 추가 하 여 합니다. 검색 관리 역할 그룹의 구성원에 게 Exchange 설치를 통해 만들어진 검색 사서함에 대 한 전체 액세스 사서함 권한이 합니다.


> [!WARNING]
> 검색 관리 역할 그룹의 구성원에는 중요 한 메시지 콘텐츠에 액세스할 수 있습니다. 특히, 이러한 구성원 <A href="in-place-ediscovery-exchange-2013-help.md">원본 위치 eDiscovery</A> 을 사용 하 여 Exchange 조직, 미리 보기 메시지 (및 기타 사서함 항목)의 모든 사서함을 검색 하 고 검색 사서함에 복사할 복사 된 메시지를.pst 파일로 내보낼를 수 있습니다. 대부분의 조직에서 법적, 규정 준수, 또는 인사 담당자가이 권한이 부여 됩니다.<BR>



검색 관리 역할 그룹에 대 한 자세한 내용은, [검색 관리](discovery-management-exchange-2013-help.md)를 참조 하십시오. 자세한 내용은 대 한 액세스 제어 RBAC (역할 기반), [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참조 하십시오.

이 절차가 사용된 시나리오에 관심이 있으면 다음 항목을 참조하십시오.

  - [원본 위치 eDiscovery 검색 만들기](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [만들기 또는 In-place Hold 제거](create-or-remove-an-in-place-hold-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md) 항목의 "역할 그룹" 항목.

  - 기본적으로 검색 관리 역할 그룹 구성원이 포함 되지 않습니다. 또한 조직 관리 역할을 가진 관리자가를 만들거나 검색 관리 역할 그룹에 추가 되지 않고 검색 검색을 관리할 수 없습니다.

  - Exchange 2013 조직 관리 역할 그룹의 구성원 모든 사서함 콘텐츠를 대기 시키려면는 [원본 위치 유지 및 소송 보존](in-place-hold-and-litigation-hold-exchange-2013-help.md) 를 만들 수 있습니다. 그러나는 쿼리 기반 원본 위치 유지를 만들려면 사용자 검색 관리 역할 그룹의 구성원 이어야 해야 하거나는 사서함 검색 역할이 할당 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## EAC를 사용 하 여 검색 관리 역할 그룹에 사용자를 추가 하려면

1.  **사용 권한 관리** 로 이동 \> **관리자 역할로** 합니다.

2.  목록 보기에서 **검색 관리** 를 선택 하 고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘") 를 클릭 한 다음

3.  **역할 그룹** **구성원** 을 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭 합니다.

4.  **구성원 선택** 하나 이상의 사용자를 선택 하 고 **추가** 클릭 한 다음 **확인** 을 클릭 합니다.

5.  **역할 그룹** **저장** 을 클릭 합니다.

## 셸을 사용 하 여 검색 관리 역할 그룹에 사용자를 추가 하려면

검색 관리 역할 그룹에 Bsuneja 사용자를 추가 하는이 예제입니다.

    Add-RoleGroupMember -Identity "Discovery Management" -Member Bsuneja

구문과 매개 변수에 대한 자세한 내용은 [Add-RoleGroupMember](https://technet.microsoft.com/ko-kr/library/dd638207\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

검색 관리 역할 그룹에 사용자를 추가 했을 때 있는지를 확인 하려면 다음을 수행 합니다.

1.  EAC에서 **사용 권한 관리** 로 이동 \> **관리자 역할로** 합니다.

2.  목록 보기에서 **검색 관리** 를 선택 합니다.

3.  세부 정보 창에서 사용자가 **구성원** 아래에 나열 되었는지 확인 합니다.

검색 관리 역할 그룹의 구성원 목록을 표시 하려면이 명령을 실행할 수도 있습니다.

    Get-RoleGroupMember -Identity "Discovery Management"


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


