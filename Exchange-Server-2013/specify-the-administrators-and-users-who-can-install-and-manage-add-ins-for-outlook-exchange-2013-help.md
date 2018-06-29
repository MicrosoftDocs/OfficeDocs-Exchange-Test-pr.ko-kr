---
title: '관리자 및 설치 하 고 Outlook 용 추가 기능을 관리할 수 있는 사용자 지정: Exchange 2013 Help'
TOCTitle: 관리자 및 설치 하 고 Outlook 용 추가 기능을 관리할 수 있는 사용자 지정
ms:assetid: 7ee4302d-b8bb-40a0-9810-10d3a0271bcb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ943754(v=EXCHG.150)
ms:contentKeyID: 52058098
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리자 및 설치 하 고 Outlook 용 추가 기능을 관리할 수 있는 사용자 지정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2017-02-08_

설치 및 Outlook 용 추가 기능을 관리 하는 관리자가 조직에서 사용 권한이 지정할 수 있습니다. 설치 하 여 자신의 사용에 대 한 추가 기능 관리 권한이 있는 사용자 조직에서 지정할 수 있습니다.

이 할당 하거나 추가 기능을 특정 관리 역할을 제거 하 여 수행 됩니다. 다섯 가지 기본 제공 역할을 사용할 수 있습니다.

관리 역할

  - **Org 마켓플레이스 앱**   관리자가 설치 하 고 조직에 대 한 Office 스토어에서 사용할 수 있는 추가 기능을 관리할 수 있습니다.

  - **조직 사용자 지정 앱**   관리자가 설치 하 고 조직에 대 한 사용자 지정 추가 기능을 관리할 수 있습니다.

사용자 역할

  - **내 마켓플레이스 앱**   설치 하 고 자신의 사용에 대 한 Office 스토어 추가 기능을 관리할 수 있습니다.

  - **내 사용자 지정 응용 프로그램**   설치 하 고 자신의 용도 대 한 사용자 지정 추가 기능을 관리할 수 있습니다.

  - **내 ReadWriteMailbox 앱**   설치 하 고 자신의 매니페스트에 ReadWriteMailbox 사용 권한 수준을 요청 하는 추가 기능을 관리할 수 있습니다.

기본적으로 **조직 관리** 역할 그룹을 가진 모든 관리자에 게 사용 하도록 설정 하는 위의 관리 역할을 모두. 기본적으로 최종 사용자에 게 권한도 부여 사용 하도록 설정 하는 위의 사용자 역할을 합니다.

이러한 각 역할에 대 한 정보를 [Org 마켓플레이스 앱 역할](org-marketplace-apps-role-exchange-2013-help.md), [조직 사용자 지정 앱 역할](org-custom-apps-role-exchange-2013-help.md), [내 마켓플레이스 앱 역할](my-marketplace-apps-role-exchange-2013-help.md), [사용자 지정 앱의 역할](my-custom-apps-role-exchange-2013-help.md)및 [내 ReadWriteMailbox 앱 역할](my-readwritemailbox-apps-role-exchange-2013-help.md)를 참조 하십시오.

추가 기능에 대 한 정보를 [Outlook용 앱](add-ins-for-outlook-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이 cmdlet을 실행하려면 먼저 사용 권한을 할당받아야 합니다. 이 cmdlet의 모든 매개 변수가 이 항목에 나열되지만 사용자에게 할당된 사용 권한에 포함되지 않은 일부 매개 변수에는 액세스할 수 없습니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md) 항목의 "역할 할당" 항목.

  - Office 스토어에 대 한 액세스는 사서함 또는 특정 지역에서 조직에 대 한 지원 되지 않습니다. **조직** 에서 **Exchange 관리 센터** 에서 옵션으로 **Office 스토어에서 추가** 하는 경우 표시 되지 않으면 \> **추가 기능** \> ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")있습니다 시킬 수 있는 URL 또는 파일 위치에서 Outlook 용 추가 기능을 설치 합니다. 자세한 내용은 서비스 공급자에 게 문의 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 관리자를 설치 하 고 조직에 대 한 추가 기능을 관리 하는 데 필요한 사용 권한 할당

## EAC를 사용하여 관리자에게 사용 권한 할당

관리자 설치 및 추가 기능을 사용할 수 있는 조직에 대 한 Office 스토어에서 관리 하는 데 필요한 사용 권한을 할당 하려면 EAC를 사용할 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)를 참조 하십시오.

## 사용자를 설치 하 고 자신의 사용에 대 한 추가 기능을 관리 하는 데 필요한 사용 권한 할당

## EAC를 사용하여 사용자에게 사용 권한 할당

사용자가 보고 하 고 자신의 용도 대 한 사용자 지정 추가 기능을 수정 하는 데 필요한 사용 권한을 할당 하려면 EAC를 사용할 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)을 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

사용자에게 사용 권한이 할당되었는지 확인하려면 `Get-ManagementRoleAssignment -Role <Role Name> -GetEffectiveUsers` 형식을 사용하여 셸 명령을 실행합니다. 여기서 `Role Name`은 할당된 사용 권한을 확인할 역할입니다.

이 예제는 누구에 게 할당 했을 때 확인 하는 방법을 보여주는 조직에 대 한 Office 스토어에서 추가 기능을 설치할 수 있는 권한이 있습니다.

1.  `Get-ManagementRoleAssignment -Role "Org Marketplace Apps" -GetEffectiveUsers`를 실행합니다.

2.  결과에서 **유효 사용자** 열의 항목을 확인합니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

