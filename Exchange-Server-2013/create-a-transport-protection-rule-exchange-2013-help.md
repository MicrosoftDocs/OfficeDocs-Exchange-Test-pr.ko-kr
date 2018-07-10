---
title: '전송 보호 규칙 만들기: Exchange 2013 Help'
TOCTitle: 전송 보호 규칙 만들기
ms:assetid: 3a857185-ee16-4ee7-9e57-8be95f7e753a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd302432(v=EXCHG.150)
ms:contentKeyID: 50482884
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전송 보호 규칙 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

전송 보호 규칙을 사용하면 보낸 사람, 받는 사람, 메시지 제목, 내용 같은 속성을 기반으로 메시지에 영구 권한 보호를 적용할 수 있습니다.


> [!WARNING]
> 프로덕션 환경에서 전공 규칙을 만들기 전에 먼저 테스트 환경에서 만들어 철저하게 테스트하는 것이 좋습니다. 이 항목에서 만드는 전송 규칙은 예입니다. 각자의 요구 사항을 기반으로 적절한 전송 규칙 조건자와 값을 사용하여 전송 규칙을 만들 수 있습니다.



IRM(정보 권한 관리) 관련 추가 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2 ~ 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "전송 규칙" 항목

  - [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) 를 실행 하는 서버는 조직에서 사용 가능 하 고 기존 RMS 서식 파일을 포함 해야 합니다.

  - IRM을 사용하여 메시지를 보호하도록 전송 보호 규칙을 구성하고 저널링도 사용하는 경우 저널링 에이전트가 메시지의 암호화되지 않은 복사본을 저널 서버에 저장할 수 있도록 저널 보고서 암호 해독을 사용하도록 설정하는 것이 좋습니다. 자세한 내용은 [저널 보고서 암호 해독](journal-report-decryption-exchange-2013-help.md) 항목을 참조하십시오.

  - 전송 보호 규칙을 만든 후 AD RMS 서버를 사용할 수 없기 때문에 규칙을 메시지에 적용할 수 없는 경우 사서함 서버의 전송 서비스에 의해 메시지가 큐에 대기됩니다. 이러한 메시지의 양에 따라 사서함 서버에서 추가 디스크 공간이 소비될 수 있습니다. Exchange에서는 메시지를 IRM으로 보호하려고 세 번 시도합니다. 세 번의 시도 후, AD RMS 서버에 액세스할 수 없거나 메시지에 IRM 보호를 적용할 수 없으면 보낸 사람에게 NDR(배달 못 함 보고서)이 전송됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 전송 보호 규칙 만들기

1.  **메일 흐름** \> **규칙**으로 이동합니다.

2.  목록 보기에서 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

3.  **새 규칙**에서 먼저 **기타 옵션**을 클릭하고 다음 필드를 완성합니다.
    
      - **이름**   전송 규칙의 이름을 입력합니다.
    
      - **다음 경우에 이 규칙 적용**   조건을 선택하고 조건의 필요한 값을 모두 입력합니다. 조건을 더 추가하려면 **조건 추가**를 클릭합니다.
        

        > [!IMPORTANT]
        > 전송 보호 규칙을 만들 때 조건을 선택하지 않으면 Exchange 2013 서버에서 조직의 전송 서비스를 사용하여 처리되는 모든 메시지가 IRM으로 보호됩니다. 모든 메시지에 IRM 보호를 적용하려면 더 많은 리소스가 필요합니다. 따라서 이를 고려하여 사서함 서버와 AD&nbsp;RMS 배포에 대한 계획을 수립하는 것이 좋습니다.

    
      - **다음 작업 실행**   **다음을 포함하는 메시지에 권한 보호 적용**을 선택한 다음 **RMS 템플릿 선택** 대화 상자를 사용하여 템플릿을 선택합니다.
    
      - **다음의 경우 제외**   (옵션) **예외 추가**를 클릭하여 규칙의 예외를 지정합니다.

4.  **저장**을 클릭하여 전송 규칙을 만듭니다.

## 셸을 사용하여 전송 보호 규칙 만들기

  - 전송 보호 규칙을 만들려면 AD RMS 배포에 기존 RMS 템플릿이 있어야 합니다. 다음은 AD RMS 클러스터에서 사용 가능한 템플릿을 검색하는 예입니다.
    
        Get-RMSTemplate | format-list
    
    구문과 매개 변수에 대한 자세한 내용은 [Get-RMSTemplate](https://technet.microsoft.com/ko-kr/library/dd297960\(v=exchg.150\))를 참조하십시오.

  - 다음은 전송 보호 규칙 BusinessCriticalProject를 만드는 예입니다. 이 규칙은 **전달하지 않음** 템플릿을 사용하여 제목 필드에 "Business Critical" 구를 포함하는 메시지에 IRM 보호를 적용합니다.
    

    > [!NOTE]
    > <CODE>SubjectContainsWords</CODE> 조건자가 이 예에서 사용됩니다. 전송 규칙 조건자의 어떠한 조합이라도 사용하여 규칙의 조건과 예외를 만들 수 있습니다. 사용할 수 있는 조건자에 대한 자세한 내용은 <A href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">전송 규칙 조건 (조건자)</A> 항목을 참조하십시오.

    
        New-TransportRule -Name "Protect-BusinessCriticalProject" -SubjectContainsWords "Business Critical" -ApplyRightsProtectionTemplate "Do Not Forward"
    
    구문과 매개 변수에 대한 자세한 내용은 [New-TransportRule](https://technet.microsoft.com/ko-kr/library/bb125138\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

전송 보호 규칙을 성공적으로 만들었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC를 사용하여 규칙이 만들어졌는지 확인한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하여 규칙의 속성을 확인합니다.

  - [Get-TransportRule](https://technet.microsoft.com/ko-kr/library/aa998585\(v=exchg.150\)) cmdlet을 사용하여 규칙을 검색합니다. 규칙을 검색하는 방법에 대한 예제를 보려면 **Get-TransportRule**에서 [Examples](https://technet.microsoft.com/ko-kr/aa998585\(exchg.150\)#examples) 항목을 참조하십시오.

  - Outlook, Outlook Web App 또는 모바일 장치를 사용하여 규칙 조건을 충족하는 테스트 메시지를 보낸 다음 받는 사람이 수신한 메시지가 IRM으로 보호되는지 여부를 확인합니다.

