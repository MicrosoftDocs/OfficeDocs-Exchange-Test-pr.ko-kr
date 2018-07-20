---
title: 'Outlook 보호 규칙 만들기: Exchange 2013 Help'
TOCTitle: Outlook 보호 규칙 만들기
ms:assetid: da64750d-faaf-44de-ad8c-888eba7fbdbf
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638196(v=EXCHG.150)
ms:contentKeyID: 50484268
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook 보호 규칙 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Outlook 보호 규칙을 사용 하는 메시지 전송 하기 전에 Outlook 2010 에서 Active Directory 권한 관리 서비스 (AD RMS) 서식 파일을 적용 하 여 정보 권한 관리 (IRM)와 메시지를 보호할 수 있습니다.

IRM과 관련된 추가 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "권한 보호" 항목

  - Microsoft Exchange Server 2013 를 실행 하는 서버와 동일한 Active Directory 포리스트에 배포 된 [AD RMS](https://technet.microsoft.com/en-us/library/hh831364.aspx) 서버를 있어야 합니다.

  - 메시지를 IRM으로 보호 하도록 Outlook 보호 규칙을 구성 하는 경우에 암호를 해독 하 고 메시지에 액세스 하는 전송 규칙 에이전트를 포함 하 여 전송 에이전트를 허용 하도록 전송 암호 해독을 사용 하도록 설정 하는 것이 좋습니다. 저널링을 사용 하는 경우 저널 보고서에는 암호화 되지 않은 메시지 복사본을 저장 하려면 저널링 에이전트를 허용 하도록 저널 보고서 암호 해독을 사용 하도록 설정 고려해 야 합니다. 자세한 내용은 [저널 보고서 암호 해독](journal-report-decryption-exchange-2013-help.md)를 참조 하십시오.

  - Exchange 관리 센터 (EAC)를 사용 하 여 Outlook 보호 규칙을 만들 수 없습니다. 셸을 사용 해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용 하 여 Outlook 보호 규칙 만들기

이 예제에서는 Outlook 보호 규칙 Project Contoso를 만듭니다. 중요 한 비즈니스 AD RMS 템플릿 사용 하 여 ContosoPMs 메일 그룹에 보낸 메시지를 보호 하는 규칙입니다.

    New-OutlookProtectionRule -Name "Project Contoso" -SentTo "DL-ContosoPMs@contoso.com" -ApplyRightsProtectionTemplate "Business Critical"


> [!NOTE]
> Outlook 보호 규칙에 대 한 <CODE>SentTo</CODE> 조건자를 사용 하는 경우 및 메일 그룹을 지정 메시지만 주소가 지정 된 받는 사람, 사람, 참조 또는 숨은 참조에 메일 그룹에 필드 IRM으로 보호 된 됩니다. 메일 그룹의 개별 구성원에 게 보내는 메시지에 IRM 보호 적용 되지 않습니다.



지정 된 부서 또는 지정된 된 범위 (내부 메시지에 대 한`InOrganization` , 모든 받는 사람에 게 `All` )에 게 보내는 메시지에 사용자가 보낸 메시지에 IRM 보호 기능을 적용 하려면 `FromDepartment` 및 `SentToScope` 조건자를 사용할 수도 있습니다.

자세한 구문 및 매개 변수 정보에 대 한 [New-OutlookProtectionRule](https://technet.microsoft.com/ko-kr/library/dd298182\(v=exchg.150\))를 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

Outlook 보호 규칙 성공적으로 만들었습니다을 확인 하려면 다음을 수행 합니다.

  - 규칙을 만들었는지 확인 하 고 해당 규칙의 속성을 보려면 [Get-OutlookProtectionRule](https://technet.microsoft.com/ko-kr/library/dd298004\(v=exchg.150\)) cmdlet을 실행 합니다. Outlook 보호 규칙을 검색 하는 방법의 예 **Get-OutlookProtectionRule**에서 [예](https://technet.microsoft.com/ko-kr/dd298004\(exchg.150\)#examples) 를 참조 하십시오.

  - Outlook 2010 를 사용 하 여 규칙의 조건을 충족 하는 테스트 메시지를 만들고 클라이언트에서 규칙이 트리거되는 있는지 확인 합니다.
    

    > [!NOTE]
    > Outlook에서 사용할 수 있도록 Outlook 보호 규칙에 대 한 다소 시간이 걸릴 수 있습니다.


