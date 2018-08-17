---
title: 'UM 헌트 그룹 만들기: Exchange 2013 Help'
TOCTitle: UM 헌트 그룹 만들기
ms:assetid: 43ecb1ec-5f82-4516-9010-de8f954d3758
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997679(v=EXCHG.150)
ms:contentKeyID: 50555975
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMHuntGroupWizardForm.CreateUMHuntGroupWizardPage1
ms.translationtype: MT
---

# UM 헌트 그룹 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-04-16_

UM(통합 메시징) 헌트 그룹은 PBX(Private Branch eXchange) 또는 IP PBX 헌트 그룹을 논리적으로 나타낸 것입니다. UM 헌트 그룹은 UM IP 게이트웨이와 UM 다이얼 플랜 간의 연결 또는 링크 역할을 합니다.


> [!NOTE]
> UM IP 게이트웨이를 만들 때 UM IP 게이트웨이와 UM 다이얼 플랜을 연결하면 UM 헌트 그룹도 만들어집니다.




> [!NOTE]
> UM 헌트 그룹 설정을 변경하려면 헌트 그룹을 삭제한 다름 적절한 설정이 포함된 다른 헌트 그룹을 만들어야 합니다.



UM 헌트 그룹과 관련된 다른 관리 작업에 대한 자세한 내용은 [UM 헌트 그룹 절차](um-hunt-group-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 헌트 그룹" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM IP 게이트웨이를 만들었는지 확인하십시오. 자세한 단계는 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 헌트 그룹 만들기

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 헌트 그룹**에서 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

3.  **새 UM 헌트 그룹** 페이지에서 다음 정보를 입력합니다.
    
      - **이름**   이 입력란에 UM 헌트 그룹의 표시 이름을 입력합니다. UM 헌트 그룹 이름은 필수 항목이며 고유해야 하지만, EAC와 셸에 표시되는 용도로만 사용됩니다. 헌트 그룹을 만든 후 표시 이름을 변경해야 하는 경우에는 기존 헌트 그룹을 먼저 삭제한 다음 적합한 이름으로 다른 헌트 그룹을 만들어야 합니다.
        
        조직에서 여러 개의 헌트 그룹을 사용하고 있는 경우 헌트 그룹에 대해 의미 있는 이름을 사용하는 것이 좋습니다. UM 헌트 그룹 이름의 최대 길이는 64자이며 공백을 포함할 수 있습니다. 하지만 다음 문자는 사용할 수 없습니다. " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **UM IP 게이트웨이**   이 텍스트 상자에, 사용할 UM IP 게이트웨이를 지정합니다. **찾아보기**를 클릭하여 UM IP 게이트웨이를 선택한 후 **확인**을 클릭합니다.
    
      - **파일럿 식별자**   이 상자에 PBX 또는 IP PBX에 구성된 파일럿 식별자를 고유하게 식별하는 문자열을 지정합니다.
        
        이 입력란에는 내선 번호나 SIP(Session Initiation Protocol) URI(Uniform Resource Identifier)를 사용할 수 있고, 영숫자 문자를 입력할 수 있습니다. 레거시 PBX의 경우 숫자 값이 파일럿 식별자로 사용됩니다. 그러나 일부 IP PBX는 SIP URI를 사용할 수 있습니다.

4.  
    
    **저장**을 클릭합니다.

## 셸을 사용하여 UM 헌트 그룹 만들기

이 예에서는 파일럿 식별자가 12345인 `MyUMHuntGroup`이라는 UM 헌트 그룹을 만듭니다.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 12345 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

이 예에서는 파일럿 식별자가 여러 개 있는 `MyUMHuntGroup`이라는 UM 헌트 그룹을 만듭니다.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

