---
title: 'UM 사서함 정책 만들기: Exchange 2013 Help'
TOCTitle: UM 사서함 정책 만들기
ms:assetid: 7f20874b-c46c-4505-9a78-f63eacb578ff
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123510(v=EXCHG.150)
ms:contentKeyID: 50556020
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMMailboxPolicyWizardForm.CreateUMMailboxPolicyWizardPage
ms.translationtype: MT
---

# UM 사서함 정책 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-03-08_

UM(통합 메시징) 사서함 정책을 만들어 PIN 정책 설정 또는 전화 걸기 제한과 같은 공통 UM 정책 설정 집합을 UM 사용 가능 사서함 모음에 적용할 수 있습니다. UM 사서함 정책은 UM 사용 가능 사용자와 UM 다이얼 플랜을 연결하여 공통 정책 집합이나 보안 설정을 UM 사용 가능 사서함 모음에 적용할 수 있습니다. UM 사서함 정책은 UM 사용 가능 사용자에 대해 UM 구성 설정을 적용하고 표준화하는 데 유용합니다.

기본적으로 UM 다이얼 플랜을 만들 때 UM 사서함 정책도 만들어집니다. 조직에 통합 메시징을 배포한 후 추가 UM 사서함 정책을 만들거나 기존 UM 사서함 정책을 수정해야 할 수 있습니다.

UM 사서함 정책에 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 사서함 정책 절차](um-mailbox-policy-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 사서함 정책 만들기

1.  
    
    EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 **새로 만들기** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

3.  **새 UM 사서함 정책** 페이지의 **이름** 상자에 새 UM 사서함 정책의 이름을 입력합니다.
    
    이 상자에 UM 사서함 정책의 고유 이름을 지정합니다. 이 이름은 EAC에 나타나는 표시 이름입니다. UM 사서함 정책을 만든 후 표시 이름을 변경해야 하는 경우 기존 UM 사서함 정책을 먼저 삭제한 다음 적합한 이름으로다른 UM 사서함 정책을 만들어야 합니다. UM 사용 가능 사용자가 연결되어 있는 UM 사서함 정책은 삭제할 수 없습니다.
    
    UM 사서함 정책 이름은 필수 항목이지만 표시 목적으로만 사용됩니다. 조직에서 여러 개의 UM 사서함 정책을 사용할 수 있기 때문에 UM 사서함 정책에 대해 의미 있는 이름을 사용하는 것이 좋습니다. UM 사서함 정책 이름의 최대 길이는 64자이며 공백을 포함할 수 있습니다. 그러나 다음 문자는 사용할 수 없습니다. " / \\ \[ \] : ; | = , + \* ? \< \>.

4.  **저장**을 클릭하여 새 UM 사서함 정책을 저장합니다. UM 사서함 정책을 저장할 때 PIN 정책, 음성 사서함 기능 및 보호된 음성 사서함 설정을 비롯한 모든 기본 설정이 사용되도록 설정됩니다. 기본 설정을 사용자 지정하거나 변경하려면 **Set-UMMailbox** cmdlet을 사용하여 방금 만든 UM 사서함 정책의 설정을 변경합니다.

## 셸을 사용하여 UM 사서함 정책 만들기

이 예에서는 UM 다이얼 플랜 `MyUMDialPlan`에 연결된 `MyUMMailboxPolicy`라는 UM 사서함 정책을 만듭니다.

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

