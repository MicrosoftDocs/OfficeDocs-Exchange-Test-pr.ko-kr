---
title: '전송 규칙에 중요 한 정보 규칙 통합 (영문): Exchange 2013 Help'
TOCTitle: 전송 규칙에 중요 한 정보 규칙 통합 (영문)
ms:assetid: feb014a7-89dd-4f2d-a06d-52806ce435d4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150583(v=EXCHG.150)
ms:contentKeyID: 50482328
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전송 규칙에 중요 한 정보 규칙 통합 (영문)

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-01-14_

Microsoft Exchange 에서 뿐 아니라 일반적인 메시지 분류에 대 한 규칙 및 기존 전송 규칙을 포함 하지만 메시지 내에서 발견 되는 중요 한 정보에 대 한 규칙을 가진를 결합 하는 DLP 정책을 만들 수 있습니다. 기존 전송 규칙 프레임 워크는 전체 다양 하드 컨트롤에 부드러운 다루는 메시징 정책 정의를 다양 한 기능을 제공 합니다. 예는 다음과 같습니다.

  - 받는 사람 및 보낸사람, 조직 내의 부서 그룹 간의 상호작용을 포함 하 여 간의 상호작용을 제한 합니다.

  - 내에서 그리고 조직 외부의 통신에 대 한 별도 정책을 적용 합니다.

  - 입력 조직 내 / 외부에서 부적절 한 콘텐츠를 차단 합니다.

  - 기밀 정보를 필터링 합니다.

  - 추적 또는 전송 또는 특정 개인과에서 받은 메시지를 보관 합니다.

  - 배달 전에 검사에 대 한 인바운드 및 아웃 바운드 메시지를 리디렉션합니다.

  - 조직을 통해 전달 되 고 지 사항을 메시지에 적용 합니다.

전송 규칙을 사용 하면 전자 메일 메시지에 메시징 정책을 적용 하려면 전송 파이프라인을 통해 해당 흐름 Edge 전송 서버에서 사서함 서버의 전송 서비스에서. 이러한 규칙 메시징 정책 준수, 메시징 시스템을 보호 하기 위해 보다 안전한 도움말 메시지를 유지 하려면 시스템 관리자가 허용 하 고 실수로 정보 손실을 방지 합니다. 전송 규칙에 대 한 자세한 내용은 [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) ( Exchange Server 2013 ) 또는 [Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\)) (Exchange Online )를 참조 하십시오.

## 전송 규칙 프레임 워크 내에서 중요 한 정보 규칙

전송 규칙 프레임 워크와 중요 한 정보 규칙은 통합 하는 것이 사용자 지정할 수 있는 조건 소개: **메시지를 포함 하는 경우... 중요 한 정보** 합니다. 이 조건은 메시지 내에 포함 된 하나 이상의 중요 한 정보 유형으로 구성할 수 있습니다. 이러한 조건을 가진 여러 DLP 정책 또는 정책 내의 규칙 구성 된 경우 정책 또는 규칙 조건 중 하나라도 일치 하는 경우 충족 됩니다. Exchange 정책 규칙은 제목, 본문 및 메시지의 첨부 파일을 검사합니다. 규칙 이러한 메시지 구성 요소 중 하 나와 일치 하는 경우 규칙 동작을 적용 됩니다.

이미 존재 하는 전송 규칙을 메시징 정책을 정의 사용 하 여 중요 한 정보 조건을 함께 사용할 수 있습니다. 이 결합 하는 경우에 다른 규칙과 함께에서 작동 하는 조건과 AND 의미 체계를 제공 합니다. 예, 서로 다른 두 조건은 적용할 작업에 대 한 일치할 필요는 모두 되도록 AND 문인와 함께 추가 됩니다. 일치 하는 중요 한 정보 형식을 포함 하는 규칙에 따른 결과로 전송 규칙 작업 중 하나를 구성할 수 있습니다. 전송 규칙을 적용 하는 메시지를 검색 하는 전송 규칙 에이전트에 의해 다양 한 파일 형식으로 검색할 수 있습니다. 지원 되는 파일 형식에 대 한 자세한 내용은, [전송 규칙을 사용 하 여 메시지 첨부 파일을 검사 하려면](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013 ) 또는 [메일 흐름 규칙을 사용 하 여 Office 365의 메시지 첨부 파일을 검사 하려면](https://technet.microsoft.com/ko-kr/library/jj919236\(v=exchg.150\)) (Exchange Online )를 참조 하십시오.

규칙의 규칙 정의 예외 부분에도 사용할 수 있습니다. 예외 정의에서 사용은 규칙 내 조건으로 사용 관계가 없습니다. 조건 및 조건에도 서로 다른 정보 유형의 일부분으로 적용할 여러 정보 유형을 지정 하는 조건을 포함 하는 규칙을 정의 하는 유연성을 제공 합니다. 이렇게 하면 특정 기존 메시지 분류 규칙 일치 하는 있지만 정책 내에서 정의 하는 작업을 수행 하기 전에 다른 중요 한 정보 형식에 일치 하지 않는 같은 정책을 있습니다.

## 자세한 내용

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Exchange의 중요 한 정보 유형 찾아보십시오](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange Server 2013

[Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\)) Exchange Online

[사용자 지정 DLP 정책 만들기](create-a-custom-dlp-policy-exchange-2013-help.md)

