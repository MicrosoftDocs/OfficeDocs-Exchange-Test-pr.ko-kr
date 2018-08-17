---
title: 'UM 자동 전화 교환 만들기: Exchange 2013 Help'
TOCTitle: UM 자동 전화 교환 만들기
ms:assetid: 773f53fb-d80f-4a79-8bd3-bd753942489f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998875(v=EXCHG.150)
ms:contentKeyID: 50483450
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.CreateAutoAttendantWizardForm.CreateAutoAttendantWizardPage
ms.translationtype: MT
---

# UM 자동 전화 교환 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-03-08_

UM (통합 메시징) 자동 전화 교환을 만든 후 교환원 응답할에서는 일반적으로 외부 전화번호로 수신 전화 자동 전화 교환에서 응답 합니다. 달리 다른 통합 메시징 구성 요소와 UM 다이얼 플랜 및 UM IP 게이트웨이 같은 필요가 UM 자동 전화 교환 만들기. 그러나 자동 전화 교환 도움말 내부 및 외부 발신자에 게 사용자 또는 조직에 존재 하 고 자신에 게 전화를 전송 하는 부서를 찾습니다.

UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 UM 자동 전화 교환을 만들려면

1.  
    
    EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동하고 자동 전화 교환을 추가할 UM 다이얼 플랜을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지에서 **UM 자동 전화 교환**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**새로 만들기** 클릭 합니다.

3.  **새 UM 자동 전화 교환** 페이지에서 다음 정보를 입력 합니다.
    
      - **이름**   이 상자에 UM 자동 전화 교환의 표시 이름을 입력합니다. UM 자동 전화 교환 이름은 필수이며 고유해야 합니다. 하지만 이 이름은 EAC와 셸에 표시되는 용도로만 사용됩니다.
        
        자동 전화 교환을 만든 후 표시 이름을 변경해야 하는 경우 먼저 기존 UM 자동 전화 교환을 삭제한 다음 적합한 이름으로 다른 자동 전화 교환을 만들어야 합니다. 조직에서 여러 개의 UM 자동 전화 교환을 사용하고 있는 경우 UM 자동 전화 교환에 대해 의미 있는 이름을 사용하는 것이 좋습니다. UM 자동 전화 교환 이름의 최대 길이는 64자이며 공백이 포함될 수 있습니다.
        
        새 UM 자동 전화 교환 공백을 포함 하도록 Office Communications Server 2007 R2 또는 Microsoft Lync Server와 통합 메시징를 통합 하는 경우 이름을 지정할 수 있지만 자동 전화 교환 이름에 공백을 포함할 수 없습니다. 따라서 표시 이름에 공백이 포함 된 자동 전화 교환을 만들고 Office Communications Server 2007 R2 또는 Lync Server와 통합 하려는 경우 먼저 해당 자동 전화 교환을 삭제 하 고 생성 해야 표시 이름에 공백이 포함 되지 않은 다른 자동 전화 교환 합니다.
    
      - **사용 하도록 설정 하는 대로이 자동 전화 교환 만들기**    새 UM 자동 전화 교환 마법사를 완료 하면 걸려오는 전화에 응답 하도록 자동 전화 교환을 사용 하도록 설정 하려면이 확인란을 선택 합니다. 기본적으로 새 자동 전화 교환은 사용 안함으로 만들어집니다.
        
        을 사용할 수 없음으로 UM 자동 전화 교환을 만들기로 결정 하는 경우 마법사를 완료 한 후 자동 전화 교환을 사용 하도록 설정 하려면 EAC 또는 셸을 사용할 수 있습니다.
    
      - **음성 명령에 응답하도록 자동 전화 교환 설정**   UM 자동 전화 교환에 음성을 사용하도록 설정하려면 이 확인란을 선택합니다. 자동 전화 교환에서 음성을 사용하도록 설정하면 발신자가 터치톤이나 음성 입력을 사용하여 UM 자동 전화 교환에서 사용하는 시스템 또는 사용자 지정 음성 안내에 응답할 수 있습니다. 기본적으로 자동 전화 교환이 만들어질 때는 음성을 사용할 수 없습니다.
        
        음성 사용이 가능한 자동 전화 교환을 사용 하 여 발신자의 경우에 대 한 음성 인식 ASR (자동) 지원이 포함 된 적절 한 UM 언어 팩을 설치 하 고이 언어를 사용 하 여 자동 전화 교환의 속성을 구성 해야 합니다.
    
      - **액세스 번호**    이 상자를 사용 하 여 발신자에 게 자동 전화 교환에 도달 하기 위해 사용할 전화번호는 내선 번호를 입력 합니다. 상자에는 내선 번호 또는 전화번호를 입력 하 고 목록에 번호를 추가 하려면 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 를 클릭 합니다. 자릿수 제공한 전화번호는 내선 번호에 연결 된 UM 다이얼 플랜에 구성 하는 내선 번호에 대 한 자릿수와 일치 필요가 없습니다. UM 자동 전화 교환에 대 한 직접 호출 됨 때문입니다.
        
        내선 번호 또는 전화번호 입력 한 수를 제한 됩니다. 그러나 나열 된 내선 번호를 하지 않고 새 자동 전화 교환을 만들 수 있습니다. 내선 번호 또는 전화번호는 필요 하지 않습니다.
        
        편집 또는 기존 내선 번호 또는 전화번호를 제거할 수 있습니다. 기존 내선 번호 또는 전화번호를 편집 하려면 **편집**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭 합니다. 목록에서 기존 내선 번호 또는 전화번호를 제거 하려면 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭 합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용 하 여 UM 자동 전화 교환 만들기

이 예에서는 들어오는 호출을 받을 수 있지만 음성을 사용할 수 없는 `MyUMAutoAttendant`라는 UM 자동 전화 교환을 만듭니다.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 55000 -Enabled $false

이 예에서는 음성 사용이 가능한 `MyUMAutoAttendant`라는 UM 자동 전화 교환을 만듭니다.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true

