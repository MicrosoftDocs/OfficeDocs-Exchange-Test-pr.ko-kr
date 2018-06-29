---
title: '사용자 지정 DLP 정책 만들기: Exchange 2013 Help'
TOCTitle: 사용자 지정 DLP 정책 만들기
ms:assetid: b3299a39-9663-41e4-b76e-9d2f7879d486
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150550(v=EXCHG.150)
ms:contentKeyID: 50482284
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자 지정 DLP 정책 만들기

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-03-18_

사용자 지정 데이터 손실 방지 (DLP) 정책을 사용 하면 기존 DLP 서식 파일 중 하나에 조건, 규칙 및 작업을 사용 하 여 조직의 특정 요구를 충족 도움이 되 고 설명 되어있지 수를 설정할 수 있습니다.

단일 정책에서 제공 하는 규칙 조건을 [Exchange의 중요 한 정보 유형 찾아보십시오](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)에 제공 된 중요 한 정보 유형 외에도 모든 기존 전송 규칙을 포함 합니다. 전송 규칙에 대 한 자세한 내용은 [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013 ) 또는 [Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\)) (Exchange Online )를 참조 하십시오.


> [!WARNING]
> 프로덕션 환경에서이 실행 하기 전에 테스트 모드에서 DLP 정책을 사용 해야 합니다. 이러한 테스트 하는 동안 샘플 사용자 사서함을 구성 하 고 결과 확인 하기 위해 테스트 정책을 호출 하는 테스트 메시지를 보낼 것이 좋습니다. 테스트 하는 방법에 대 한 자세한 내용은 <A href="test-a-mail-flow-rule-exchange-2013-help.md">메일 흐름 규칙을 테스트 합니다.</A>을 참조 하십시오.



사용자 지정 DLP 정책을 만드는데 관련 된 추가 관리 작업을 [DLP 절차](dlp-procedures-exchange-2013-help.md)(Exchange 2013 ) 또는 [DLP 절차](https://technet.microsoft.com/ko-kr/library/jj938003\(v=exchg.150\)) (Exchange Online )를 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 60분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "데이터 손실 방지(DLP)" 항목을 참조하십시오.

  - 새 사용자 지정 DLP 정책을 만들려면 Exchange 2013 에 대 한 설치 지침을 수행 해야 합니다. 배포에 대 한 자세한 내용은 [계획 및 배포](planning-and-deployment-for-exchange-2013-installation-instructions.md)을 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!NOTE]
> 고객 환경에서 차이가, 있기 때문에 Microsoft 고객 지원 서비스 (CSS)는 개발 또는 사용자 지정 정규식 스크립트 ("RegEx 스크립트")의 테스트에 참여할 수 없습니다. RegEX 사용자 지정 스크립트 개발에 대 한 테스트 및 디버깅, 내부 IT 리소스 사용을 Office 365 고객 해야 합니다. 또는 Office 365 고객 외부 컨설팅 리소스와 같은 Microsoft Consulting Services MCS ()를 사용 하도록 선택할 수 있습니다. 스크립트 개발 리소스에 관계 없이 CSS EXO 및 EOP 지원 엔지니어는 사용자 지정 RegEx 스크립트 문의에 대 한 고객 지원 하기 위해 사용할 수 없습니다.




> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용 하 여 기존의 모든 규칙 없이 사용자 지정 DLP 정책을 만들려면

1.  EAC에서 **규정 준수 관리** 로 이동 \> **데이터 손실 방지** 합니다. 구성한 상태 여야 하는 모든 기존 정책 목록에 표시 됩니다.

2.  **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 아이콘 옆에 있는 화살표를 클릭 하 고 **새 사용자 지정 정책** 을 선택 합니다.
    

    > [!IMPORTANT]
    > 화살표 대신 <STRONG>추가</STRONG><IMG title="아이콘 추가" alt="아이콘 추가" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> 아이콘을 클릭 하는 경우에 서식 파일을 기반으로 새 정책을 만들어집니다. 서식 파일을 사용 하는 방법에 대 한 자세한 내용은 <A href="how-to-new-dlp-data-loss-prevention-policy-template.md">템플릿에서 DLP 정책 만들기</A>을 참조 하십시오.



3.  **새 사용자 지정 정책** 페이지에서 다음 필드에 입력 합니다.
    
    1.  **이름**   이 정책을 다른 정책과 구분하는 이름을 추가합니다.
    
    2.  **설명**   이 정책을 요약하는 선택적 설명을 추가합니다.
    
    3.  **선택 된 상태**    이 정책에 대 한 상태 확인 하는 모드를 선택 합니다. 새 정책 수를 지정할 때까지 완벽 하 게 사용 되지 않습니다. 정책에 대 한 기본 모드는 알림 없이 테스트입니다.

4.  새 정책 참조 정보 만들기를 종료 하려면 **저장** 을 클릭 합니다. 정책을 구성 하 고 있지만 되지 않은 값이 있는 모든 정책을 아직 모든 규칙 또는이 새 사용자 지정 정책에 연결 된 작업의 목록에 추가 됩니다.

5.  방금 만든 정책을 두번클릭 하거나 선택한![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")**편집** 을 클릭 합니다.

6.  **편집 DLP 정책** 페이지에서 **규칙** 을 클릭 합니다.
    
    새 빈 규칙을 추가 하려면 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 를 클릭 합니다. 중요 한 정보 유형 외에도 모든 기존 전송 규칙을 사용 하 여 상태를 설정할 수 있습니다.
    
    혼란을 방지 하기 위해 고유한 문자열을 제공 하는 옵션을 사용 하는 경우 정책 또는 규칙의 각 부분에 대 한 고유 이름을 제공 합니다. 여러 옵션 추가 옵션은 수 있습니다.
    
    1.  보낸사람 알림 또는 재정의 허용 하는 방법에 대 한 규칙을 추가 하려면 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 아이콘 옆에 있는 화살표를 클릭 합니다.
    
    2.  규칙을 제거 하려면 규칙을 강조 표시 하 고 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭 합니다.
    
    3.  추가 조건 및 적용 또는 다른 규칙에 미치는 영향의 시간 제한이 범위를 포함 하 여이 정책에이 규칙에 대 한 작업을 추가 하려면 **기타 옵션**![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘") 을 클릭 합니다.

7.  정책 수정을 완료 하려면 **저장** 을 클릭 하 고 변경 내용을 저장 합니다.

DLP 정책 템플릿은 한 가지 유형의 하는데 도움이 되는 Microsoft Exchange를 디자인 하는 기능 및 메시징 환경에 대 한 강력한 정책 및 규정 준수 시스템을 적용 합니다. 규정 준수 기능에 대 한 자세한 내용은 [메시징 정책 및 규정 준수](messaging-policy-and-compliance-exchange-2013-help.md) (Exchange 2013 ) 또는 [보안 및 Exchange Online에 대 한 규정 준수](https://technet.microsoft.com/ko-kr/library/jj200706\(v=exchg.150\))를 참조 하십시오.

## 자세한 내용

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange 2013

[Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\)) Exchange Online

[전송 규칙에 중요 한 정보 규칙 통합 (영문)](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

