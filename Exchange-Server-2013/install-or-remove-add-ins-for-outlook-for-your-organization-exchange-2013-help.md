---
title: '설치 또는 제거 하는 조직에 대 한 Outlook 용: Exchange 2013 Help'
TOCTitle: 설치 또는 제거 하는 조직에 대 한 Outlook 용
ms:assetid: 112f3ef7-9943-4a1e-8a42-e08e8e9f67f4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ943752(v=EXCHG.150)
ms:contentKeyID: 52058054
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 설치 또는 제거 하는 조직에 대 한 Outlook 용

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2017-02-03_

설치 하거나 EAC 또는 셸을 사용 하 여 조직에 대 한 Outlook 용 추가 기능을 제거할 수 있습니다.


> [!NOTE]
> 기본적으로 조직에 대 한 추가 기능을 설치한 후 추가 기능에 조직에서 모든 사용자에 대해 사용할 수 있습니다. 설치 후 사용자에 게 추가 기능에 선택적 또는 필요한 확인 하 고 추가 기능에 사용 또는 사용 하지 않도록 설정 하 여부를 지정 하려면 EAC 또는 셸을 사용할 수 있습니다. 추가 기능에 대 한 기본 설정을 변경 하는 방법에 대 한 정보를 <A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Outlook 용 앱에 대 한 사용자 액세스 관리</A>을 참조 하십시오. 조직에서 특정 사용자에 게 사용할 수 있는 추가 기능 사용 가능 시간을 제한 하려면 셸을 사용 해야 합니다. 자세한 내용은 <A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Outlook 용 앱에 대 한 사용자 액세스 관리</A>을 참조 하십시오.



추가 관리 작업에 대 한 [Outlook용 앱](add-ins-for-outlook-exchange-2013-help.md)를 참조 합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "Outlook 용 앱" 항목.

  - 관리자를 설치 하 여 조직에 대 한 추가 기능 관리 권한을 할당할 수 있습니다. 설치 하 고 자신의 용도 대 한 추가 기능을 관리할 수 있는 권한이 사용자를 할당할 수도 있습니다. 자세한 내용은 [관리자 및 설치 하 고 Outlook 용 추가 기능을 관리할 수 있는 사용자 지정](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md)을 참조 하십시오.

  - Office 스토어에 대 한 액세스는 사서함 또는 특정 지역에서 조직에 대 한 지원 되지 않습니다. **조직** 에서 **Exchange 관리 센터** 에서 옵션으로 **Office 스토어에서 추가** 하는 경우 표시 되지 않으면 \> **추가 기능** \> ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")있습니다 시킬 수 있는 URL 또는 파일 위치에서 Outlook 용 추가 기능을 설치 합니다. 자세한 내용은 서비스 공급자에 게 문의 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## Outlook 용 추가 기능을 설치 합니다.

## EAC를 사용 하 여 추가 기능을 추가 하려면

1.  EAC에서 **조직** 으로 이동 \> **추가 기능** 입니다.

2.  **새로 만들기** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭 하 고에서 추가 기능을 설치 하려는 위치를 선택 합니다.
    
      - **Office 스토어에서 추가** 합니다. Office 스토어에서 앱을 설치 하려면 선택한 다음 **추가** 클릭 합니다. 앱 Outlook Web App 을 사용 하는 **Office 및 SharePoint에 대 한 추가 기능** 에 나열 된 \> **Outlook** 합니다.
        

        > [!NOTE]
        > Office 저장소에 대 한 액세스는 사서함 또는 특정 지역에서 조직에 대 한 지원 되지 않습니다. <STRONG>조직</STRONG> 에서 <STRONG>Exchange 관리 센터</STRONG> 에서 옵션으로 <STRONG>Office 스토어에서 추가</STRONG> 하는 경우 표시 되지 않으면 &gt; <STRONG>추가 기능</STRONG> &gt; <IMG title="아이콘 추가" alt="아이콘 추가" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">있습니다 시킬 수 있는 URL 또는 파일 위치에서 Outlook 용 추가 기능을 설치 합니다. 자세한 내용은 서비스 공급자에 게 문의 합니다.

    
      - **URL에서 추가** 합니다. **URL** 추가 기능에서 매니페스트 파일을 설치 하려면 전체 URL을 입력 합니다.
    
      - **파일에서 추가** 합니다. **찾아보기**, 선택한 다음 추가 기능에서 매니페스트 파일의 설치 하려는 위치로 이동 합니다.

3.  **저장**을 클릭합니다.

## 셸을 사용 하 여 추가 기능을 추가 하려면

이 예제에서는 URL에서 추가 기능을 추가 하는 방법을 보여줍니다.

    New-App -OrganizationApp -Url <URL location for add-in manifest file>

이 예제에서는 파일에서 추가 기능을 추가 하는 방법을 보여줍니다.

    New-App -OrganizationApp -FileData <File location for add-in manifest file>


> [!TIP]
> 셸을 사용 하 여 조직에 대 한 추가 기능을 설치 하는 추가 기능에 설치 하 고 동시에 것에 대 한 설정을 구성 수 있습니다.



구문과 매개 변수는 [New-App](https://technet.microsoft.com/ko-kr/library/jj218722\(v=exchg.150\))을 참조하십시오.

## Outlook 용 추가 기능을 제거 합니다.

## EAC를 사용 하 여 추가 기능을 제거 하려면

1.  EAC에서 **조직** 으로 이동 \> **추가 기능** 입니다.

2.  목록 보기에서 제거할 앱을 선택하고 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭합니다.

## 셸을 사용 하 여 추가 기능을 제거 하려면

셸을 사용 하 여 조직에서 추가 기능을 제거할 수 있습니다.


> [!NOTE]
> Outlook이 조직에 대 한 설치에 대 한 표시 이름 및 모든 추가 기능에 대 한 응용 프로그램 Id를 조회 하려면 다음 명령을 실행 합니다.



    Get-App -OrganizationApp |FL DisplayName,AppID

조직에서 사용자 지정 추가 기능에서 금융 테스트에서는 추가 기능을 제거 하려면 다음 명령을 실행 합니다.

    Remove-App -OrganizationApp -Identity <GUID for Finance Test Add-in>

구문과 매개 변수에 대해서는 [Remove-App](https://technet.microsoft.com/ko-kr/library/jj218709\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

조직에 설치 된 추가 기능을 보려면 다음을 수행 하나.

  - EAC에서 **조직** 으로 이동 \> **추가 기능** 및 다음 검토 설치 된 추가 기능 목록입니다.

  - 셸에서 `Get-App`실행 하 고 설치 된 추가 기능의 목록을 검토 합니다.

