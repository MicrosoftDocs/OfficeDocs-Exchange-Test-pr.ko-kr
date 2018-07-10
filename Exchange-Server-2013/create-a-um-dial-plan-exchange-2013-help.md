---
title: 'UM 다이얼 플랜 만들기: Exchange 2013 Help'
TOCTitle: UM 다이얼 플랜 만들기
ms:assetid: 963ff2e1-515d-439a-953a-664174e5e283
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123819(v=EXCHG.150)
ms:contentKeyID: 50483702
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMDialPlanWizardForm.CreateUMDialPlanWizardPage
ms.translationtype: MT
---

# UM 다이얼 플랜 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-04-16_

UM(통합 메시징) 다이얼 플랜에는 전화 통신 네트워크와 관련된 구성 정보가 포함되어 있습니다. UM 다이얼 플랜은 음성 메일에 사용할 수 있는 사용자의 내선 전화 번호에서 자신의 사서함으로의 연결을 설정합니다. UM 다이얼 플랜을 만들 때 다이얼 플랜에 대한 내선 번호 자릿수, URI(Uniform Resource Identifier) 유형 및 VoIP(Voice over IP) 보안 설정을 구성할 수 있습니다.

UM 다이얼 플랜을 만들 때마다 UM 사서함 정책도 만들어집니다. UM 사서함 정책은 \<*DialPlanName*\> 기본 정책이라고 합니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 다이얼 플랜 만들기

1.  
    
    EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동한 다음 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 UM 다이얼 플랜** 페이지에서 다음 상자에 해당 정보를 입력합니다.
    
      - **이름**   다이얼 플랜의 이름을 입력합니다. UM 다이얼 플랜 이름은 필수이며 고유해야 합니다. 하지만 이 이름은 EAC와 셸에 표시되는 용도로만 사용됩니다. 다이얼 플랜을 만든 후 표시 이름을 변경해야 하는 경우 먼저 기존 UM 다이얼 플랜을 삭제한 다음 적합한 이름으로 다른 다이얼 플랜을 만들어야 합니다. 조직에서 여러 개의 UM 다이얼 플랜을 사용하는 경우 UM 다이얼 플랜에 대해 의미 있는 이름을 사용하는 것이 좋습니다. UM 다이얼 플랜 이름의 최대 길이는 64자이며 공백을 포함할 수 있습니다. 하지만 다음 문자는 사용할 수 없습니다. " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        UM 다이얼 플랜 이름에 공백을 포함할 수는 있지만, 통합 메시징과 Office Communications Server 2007 R2 또는 Microsoft Lync Server를 통합하는 경우에는 다이얼 플랜의 이름에 공백을 포함할 수 없습니다. 따라서 표시 이름에 공백이 포함된 다이얼 플랜을 만든 후에 Office Communications Server 2007 R2 또는 Lync Server와 통합할 경우 먼저 해당 다이얼 플랜을 삭제한 다음 표시 이름에 공백이 포함되지 않은 다른 다이얼 플랜을 만들어야 합니다.
        

        > [!IMPORTANT]
        > 다이얼 플랜의 이름 상자에는 64자까지 입력할 수 있지만 다이얼 플랜 이름은 49자보다 길 수 없습니다. 49자보다 많은 문자를 포함하는 다이얼 플랜 이름을 만들려고 하면 오류 메시지가 나타납니다. 메시지에는 UM 다이얼 플랜 이름이 너무 길어 UM 사서함 정책을 생성할 수 없다는 내용이 표시됩니다. 이 문제는 앞서 설명했듯이 다이얼 플랜을 만들 때 이름이 <EM>&lt;DialPlanName&gt;</EM> 기본 정책인 기본 UM 사서함 정책도 만들어지기 때문에 발생합니다. 기본 정책의 15자가 다이얼 플랜 이름에 추가되면 총 문자 수가 제한을 초과합니다. UM 다이얼 플랜과 UM 사서함 정책에 대한 <EM>name</EM> 매개 변수는 모두 64자일 수 있습니다. 하지만 다이얼 플랜의 이름이 49자보다 길면 기본 UM 사서함 정책의 이름이 64자보다 길어지므로 시스템에서 허용되지 않습니다.

    
      - **내선 번호 길이(자릿수)**   다이얼 플랜의 자릿수를 입력합니다. 내선 번호 자릿수는 PBX(Private Branch eXchange) 또는 IP PBX에 만들어진 전화 통신 다이얼 플랜을 기반으로 합니다. 예를 들어 전화 통신 다이얼 플랜과 연결된 사용자가 4자리 내선 번호를 돌려 동일한 전화 통신 다이얼 플랜의 다른 사용자에게 전화하는 경우 내선 번호 자릿수로 4를 선택합니다.
        
        이 입력란은 필수이며 값 범위는 1에서 20까지입니다. 일반적인 내선 번호 길이는 3에서 7까지입니다. 기존 전화 통신 환경에서 내선 번호를 포함하는 경우 해당 내선 번호의 자릿수와 일치하는 자릿수를 지정해야 합니다.
        
        SIP(Session Initiation Protocol) 또는 E.164 다이얼 플랜을 만들고 UM 사용 가능 사용자를 다이얼 플랜에 연결할 때도 사용자가 사용할 내선 번호를 입력해야 합니다. 이 번호는 Outlook Voice Access 사용자가 자신의 사서함에 액세스할 때 사용합니다.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_URI 형식)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_VoIP 보안)
    
      - **오디오 언어**   이 목록에서 Outlook Voice Access 사용자가 사용할 기본 언어를 지정합니다. 이 설정은 UM 자동 전화 교환의 언어 설정에는 적용되지 않습니다. Outlook Voice Access에 사용되는 언어를 UM 자동 전화 교환에 사용되는 언어와 동일하게 또는 다르게 설정할 수 있습니다. 사용자가 다이얼 플랜과 연결된 사용자에게 전화를 걸 때의 오디오 언어는 음성 녹음 교환원이 사용하는 기본 언어입니다. 해당 발신자가 듣게 되는 시스템 음성 안내는 같은 언어로 재생됩니다. UM 다이얼 플랜에서 선택한 언어는 전자 메일, 음성 메일 및 일정 항목을 읽고, 개인 인사말이 녹음되지 않은 경우 사용자 이름을 말하고, 음성 메일 미리 보기 기능을 사용하여 음성 메시지를 복사하고, ASR(자동 음성 인식)이 적절히 작동할 수 있도록 설정하는 데 사용됩니다.
    
      - **국가/지역 코드**   이 상자에 발신 전화에 사용될 국가/지역 번호를 입력합니다. 이 번호는 전화를 거는 번호 앞에 표시됩니다. 이 상자에는 1~4자리 숫자를 입력할 수 있습니다. 예를 들어 미국 국가/지역 번호는 1이고, 영국 국가/지역 번호는 44입니다.

3.  **저장**을 클릭합니다.

## 셸을 사용하여 UM 다이얼 플랜 만들기

이 예에서는 4자리 내선 번호를 사용하는 `MyUMDialPlan`이라는 새 UM 다이얼 플랜을 만듭니다.

    New-UMDialplan -Name MyUMDialPlan -NumberofDigits 4

이 예에서는 SIP URI를 지원하고 5자리 내선 번호를 사용하는 `MyUMDialPlan`이라는 새 UM 다이얼 플랜을 만듭니다.

    New-UMDialplan -Name MyUMDialPlan -UriType SIPName -NumberofDigits 5

