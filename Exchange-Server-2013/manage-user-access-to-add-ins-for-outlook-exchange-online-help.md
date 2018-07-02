---
title: 'Outlook 용 앱에 대 한 사용자 액세스 관리: Exchange 2013 Help'
TOCTitle: Outlook 용 앱에 대 한 사용자 액세스 관리
ms:assetid: e5833dec-a23a-439e-ac03-92671817bff8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ943757(v=EXCHG.150)
ms:contentKeyID: 52058127
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook 용 앱에 대 한 사용자 액세스 관리

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2018-04-17_

Outlook 용 추가 기능에 대 한 사용자 액세스를 관리 하는 EAC 또는 Exchange Online PowerShell을 사용할 수 있습니다.

  - Exchange 관리 센터 (EAC)를 사용 하 여 사용자는 조직 수준에 대 한 access 추가 기능에서 기본 설정을 관리할 수 있습니다. 예, 추가 기능을 사용 가능 여부가 사용자에 게 있는지 여부를 구성할 수 있습니다. 추가 기능에 적용 되는지 필수 또는 사용자를 위한 옵션을 지정할 수 있습니다.

  - Exchange Online PowerShell을 사용한 작업 EAC를 함께 사용할 수 있는 모든 설정으로 다른 설정을 관리할 수 있습니다. 예, 조직에서 특정 사용자에 게 가용성을 제한할 수 있습니다.

추가 관리 작업 [Outlook용 앱](add-ins-for-outlook-exchange-2013-help.md)를 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - Windows PowerShell을 사용하여 Exchange Online에 연결하는 방법을 알아보려면 [Exchange Online PowerShell에 연결](https://go.microsoft.com/fwlink/p/?linkid=396554)을 참조하세요.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "추가 기능 Outlook에 대 한" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 여부를 지정할 추가 기능을 사용할 수 있는, 사용 또는 사용 하지 않도록 설정

## 이 옵션을 설정 하거나 사용 하지 않도록 지 여부를 지정할 추가 기능을 사용할 수 있는, EAC를 사용

1.  EAC에서 **조직** 으로 이동 \> **추가 기능** 입니다.

2.  목록 보기에서에 대 한 설정을 변경 하려는 추가 기능에 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

3.  추가 기능에 사용 하 여 사용자가 사용 하지 않으려면 **이 추가 기능을 사용 하면 조직에서 사용자에 게 확인** 확인란의 선택을 취소 한 다음 **저장** 을 클릭 합니다.

4.  추가 기능을 사용할 수 있도록 사용자가 원할 경우 **이 추가 기능을 사용 하면 조직에서 사용자에 게 확인** 을 선택 하 고 원하는 옵션을 선택 합니다.
    
      - **이 단계는 선택적 기본적으로 활성화**    사용자가 추가 기능을 해제 하도록 하려는 경우이 설정을 사용 합니다.
    
      - **이 단계는 선택적 기본적으로 사용 하지 않도록 설정**    사용자가 추가 기능에서 설정 하도록 하려는 경우이 설정을 사용 합니다.
    
      - **필수, 항상 사용 하도록 설정 합니다. 사용자가이 추가 기능을 비활성화할 수 없습니다** 에서는 추가 기능을 해제 하려면 사용자가 하지 않을 경우이 설정을 사용 합니다.

5.  **저장**을 클릭합니다.

## 이 옵션을 설정 하거나 사용 하지 않도록 지 여부를 지정할 추가 기능을 사용할 수 있는 Exchange Online PowerShell을 사용 하 여

Exchange Online PowerShell 여부를 지정할 추가 기능을 사용할 수 있는, 사용 가능 여부를 사용할 수 있습니다.


> [!NOTE]
> Outlook이 조직에 대 한 설치에 대 한 표시 이름 및 모든 추가 기능에 대 한 추가 기능에서 Id를 조회 하려면 다음 명령을 실행 합니다.



    Get-app -Organizationadd-in | Format-List DisplayName,add-inID

추가 기능을 사용 하지 않도록 설정 하 고 모든 사용자에 게에서 숨겨진를 원하는 경우에 다음 명령을 실행 합니다.

    Set-app <add-in ID> -Organizationadd-in -Enabled $false

기본적으로 사용할 수 있는 추가 기능의 싶지만 사용자가 끌 수 있도록 하는 경우에 다음 명령을 실행 합니다.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Enabled

추가 기능에 기본적으로 사용 하지 않도록 설정할 싶지만 사용자가 켤 수 있도록 하는 경우에 다음 명령을 실행 합니다.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Disabled

추가 기능에 사용자를 위해 필요한 것으로 표시 하려는 경우에 다음 명령을 실행 합니다.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser AlwaysEnabled

자세한 구문 및 매개 변수 [Set-App](https://technet.microsoft.com/ko-kr/library/jj218630\(v=exchg.150\))를 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

1.  EAC에서 **조직** 으로 이동 \> **추가 기능** 입니다.

2.  **사용자 기본값** 및 **제공 대상** 열에서 값을 검토합니다.

또는

1.  Exchange Online PowerShell에서 `Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*`를 실행 합니다.

2.  **DefaultStateForUser** 및 **Enabled**의 값을 검토합니다.

## 특정 사용자만 사용할 수 있도록 제한

## Exchange Online PowerShell를 사용 하 여 특정 사용자에 게 사용 가능 시간을 제한 하려면

LinkedIn 추가 기능을 사용할 수 있도록 Marketing 팀 메일 그룹의 구성원만을 하려는 경우에 다음 명령을 실행 합니다.

    $a = Get-DistributionGroupMember Marketing

    Set-app <add-in ID for the LinkedIn add-in> -Organizationadd-in -ProvidedTo SpecificUsers -UserList $a.Identity -DefaultStateForUser Enabled}

자세한 구문 및 매개 변수 [Set-App](https://technet.microsoft.com/ko-kr/library/jj218630\(v=exchg.150\))를 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

특정 사용자만 액세스하도록 제한되었는지 확인하려면 다음을 수행합니다.

1.  Exchange Online PowerShell에서 `Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*,ProvidedTo,UserList`를 실행 합니다.

2.  **ProvidedTo**의 값을 검토합니다.

