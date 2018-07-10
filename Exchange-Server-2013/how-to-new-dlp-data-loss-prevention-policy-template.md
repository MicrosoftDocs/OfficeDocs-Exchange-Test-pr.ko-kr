---
title: '템플릿에서 DLP 정책 만들기: Exchange 2013 Help'
TOCTitle: 템플릿에서 DLP 정책 만들기
ms:assetid: 4432ef8b-6108-48d3-b2af-43ef5b40d2bc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150515(v=EXCHG.150)
ms:contentKeyID: 50482208
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 템플릿에서 DLP 정책 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-14_

Microsoft Exchange Server 2013에서는 DLP(데이터 손실 방지) 정책 템플릿을 사용하여 조직의 메시징 정책 및 규정 준수 요구 사항을 쉽게 충족할 수 있습니다. 이러한 템플릿에는 일반적인 여러 법적 및 규정 요구 사항과 연결된 메시지 데이터를 관리하는 데 유용한 미리 만들어진 규칙 집합이 포함됩니다. Microsoft에서 제공하는 모든 템플릿의 목록을 보려면 [Exchange에서 제공 하는 DLP 정책 템플릿](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)을 참조하십시오. 제공되는 DLP 템플릿 예는 다음을 관리하는 데 유용할 수 있습니다.

  - GLBA(Gramm-Leach-Bliley Act) 데이터

  - PCI-DSS(Payment Card Industry Data Security Standard)

  - U.S. PII(United States Personally Identifiable Information)

으로를 사용 하거나 이러한 DLP 서식 파일 중 하나를 사용자 지정할 수 있습니다-됩니다. DLP 정책 템플릿 새 조건 또는 조건자 및 작업을 포함 하는 전송 규칙을 기반으로 합니다. DLP 정책이 기존 전송 규칙의 전체 범위를 지원 하 고 DLP 정책 설정 된 후에 추가 규칙을 추가할 수 있습니다. 정책 서식 파일에 대 한 자세한 내용은 [DLP 정책 템플릿](dlp-policy-templates-exchange-2013-help.md)을 참조 하십시오. 전송 규칙 기능에 대 한 자세한 내용은, [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013 ) 또는 [Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\)) (Exchange Online )를 참조 하십시오. 일단 정책을 적용 (영문)를 시작 다음 항목을 검토 하 여 결과 확인 하는 방법에 대 한 자세한 수 있습니다.

Exchange 2013: [DLP 정책 검색 보고서 보기](view-dlp-policy-detection-reports-exchange-2013-help.md)

Exchange Online: [DLP 정책 검색 보고서 보기](https://technet.microsoft.com/ko-kr/library/dn904484\(v=exchg.150\))


> [!WARNING]
> DLP 정책을 프로덕션 환경에서 실행하기 전에 테스트 모드에서 실행해야 합니다. 그러한 테스트 중에, 샘플 사용자 사서함을 구성한 다음 결과 확인을 위해 테스트 정책을 호출하는 테스트 메시지를 전송해보는 것이 좋습니다.



템플릿에서 DLP 정책 만들기 (영문)와 관련 된 추가 관리 작업을 [DLP 절차](dlp-procedures-exchange-2013-help.md)Exchange Server 2013 또는 [DLP 절차](https://technet.microsoft.com/ko-kr/library/jj938003\(v=exchg.150\))Exchange Online 을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 30분

  - 해당 Exchange 2013[계획 및 배포](planning-and-deployment-for-exchange-2013-installation-instructions.md)의 설명에 따라 설정 되었는지 확인 합니다.

  - 조직 내의 관리자 및 사용자 계정을 모두 구성하고 기본 메일 흐름의 유효성을 검사합니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "데이터 손실 방지(DLP)" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 템플릿에서 DLP 정책 구성

1.  EAC에서 **규정 준수 관리** \> **데이터 손실 방지**로 이동한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.
    

    > [!NOTE]
    > <STRONG>추가</STRONG><IMG title="아이콘 추가" alt="아이콘 추가" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> 아이콘 옆의 화살표를 클릭하고 드롭다운 메뉴에서 <STRONG>템플릿에서 새 DLP 정책 만들기</STRONG>를 선택한 경우에도 이 작업을 선택할 수 있습니다.



2.  **템플릿에서 새 DLP 정책 만들기** 페이지에서 다음 필드에 값을 입력합니다.
    
    1.  **이름**   이 정책을 다른 정책과 구분하는 이름을 추가합니다.
    
    2.  **설명**   이 정책을 요약하는 선택적 설명을 추가합니다.
    
    3.  **템플릿 선택**   새 정책을 만드는 데 기초로 사용할 적절한 템플릿을 선택합니다.
    
    4.  **기타 옵션**   모드 또는 상태를 선택합니다. 새 정책은 지정할 사항을 지정하기 전까지는 완전하게 사용할 수 없습니다. 정책에 대한 기본 모드는 알림이 없는 테스트 모드입니다.
    
    5.  **저장**을 클릭하여 정책 만들기를 마칩니다.


> [!NOTE]
> 조직에서는 특정 템플릿 내의 규칙 외에도 메시징 환경 내의 규정된 데이터에 적용되는 추가 회사 정책이나 추가로 필요한 사항이 있을 수 있습니다. Exchange 2013에서는 기본 템플릿을 손쉽게 변경하여 Exchange 메시징 환경이 사용자 고유의 요구 사항을 준수할 수 있도록 작업을 추가할 수 있습니다.



정책을 Exchange 2013 환경에 저장한 후에는 정책 내의 규칙을 편집하여 정책을 수정할 수 있습니다. 규칙 변경의 예로는 특정 사용자를 정책에서 제외하거나 알림을 보내거나 메시지에 중요한 내용이 있는 경우 메시지 배달을 차단하는 작업이 있습니다. 정책 및 규칙 편집에 대한 자세한 내용은 [DLP 정책 관리](manage-dlp-policies-exchange-2013-help.md)를 참조하십시오.

Exchange 2013에서 이미 만든 DLP 정책을 변경하려면 **DLP 정책 편집** 페이지에서 특정 정책의 규칙 집합으로 이동하고 해당 페이지에서 사용할 수 있는 도구를 사용해야 합니다.

일부 정책에서는 메시지에 대한 RMS를 호출하는 규칙을 추가할 수 있습니다. 이러한 유형의 규칙을 사용하려면 작업을 추가하기 전에 Exchange 서버에서 RMS를 구성해야 합니다.

DLP 정책의 경우 규칙, 작업, 예외, 적용 기간 또는 정책 내의 다른 규칙이 적용되는지 여부를 변경하고 각 정책에 대한 사용자 지정 조건을 추가할 수 있습니다.

## 자세한 내용

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[DLP 정책 템플릿](dlp-policy-templates-exchange-2013-help.md)

