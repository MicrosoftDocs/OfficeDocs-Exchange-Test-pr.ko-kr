---
title: '데이터 손실 방지: Exchange 2013 Help'
TOCTitle: 데이터 손실 방지
ms:assetid: 7c8ed3c1-ca91-4d9b-b16b-0a2b8ac89730
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150527(v=EXCHG.150)
ms:contentKeyID: 50482290
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 데이터 손실 방지

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

포함된 DLP 정책 및 테스트 방법을 비롯하여 Exchange Server에 2013 및 Exchange Online의 DLP 정책에 대해 자세히 알아봅니다. 또한 Exchange DLP의 새 기능에 대해서도 알아봅니다.

엔터프라이즈 메시지 시스템의 경우 전자 메일은 중요한 데이터를 포함하는 업무상 통신에 광범위하게 사용되므로 DLP(데이터 손실 방지)가 중요한 역할을 합니다. 작업자의 생산성을 저해하지 않으면서 이러한 데이터에 규정 준수 요구 사항을 적용하고 전자 메일에서의 데이터 사용을 관리하기 위해 DLP 기능은 중요한 데이터를 이전보다 쉽게 관리할 수 있게 해줍니다. DLP의 대략적인 개념을 알아보려면 다음 비디오를 시청하세요.

> [!VIDEO https://www.microsoft.com/ko-kr/videoplayer/embed/31f2b48e-93ed-4be3-b46d-e7230c0fed8f]

DLP 정책은 일련의 조건을 포함하는 간단한 패키지로 전자 메일 메시지 및 첨부 파일을 필터링하기 위해 EAC(Exchange 관리 센터)에서 만들어 활성화하는 전송 규칙, 작업 및 예외로 구성됩니다. DLP 정책을 만들되 활성화하지는 않도록 선택할 수도 있습니다. 그러면 메일 흐름에 영향을 주지 않고 정책을 테스트할 수 있습니다. DLP 정책은 기존 전송 규칙의 모든 기능을 사용할 수 있습니다. 사실상 Microsoft Exchange Server 2013과 Exchange Online에는 새로운 DLP 기능을 구현하기 위해 새로운 유형의 전송 규칙이 다양하게 생성되어 있습니다. 전송 규칙의 중요한 새로운 기능 중 하나는 메일 흐름 프로세싱에 통합될 수 있는 중요한 정보를 분류하기 위한 새로운 접근 방식입니다. 이 새로운 DLP 기능은 키워드 일치, 사전 일치, 정규식 평가 및 기타 콘텐츠 검사를 통해 깊이 있는 콘텐츠 분석을 수행하여 조직의 DLP 정책을 위반하는 콘텐츠를 검색합니다. 최신 버전의 Exchange Online 및 Exchange 2013 SP1은 표준 양식의 중요한 정보를 검색하는 데 도움이 되는 [문서 지문](overview-of-document-fingerprinting-in-exchange.md)을 추가적으로 제공합니다. 전송 규칙에 대한 자세한 내용은 [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)(Exchange 2013) 또는 [Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\))(Exchange Online) 및 [전송 규칙에 중요 한 정보 규칙 통합 (영문)](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)을 참조하세요. Exchange 관리 셸 cmdlet을 사용하여 DLP 정책을 관리할 수도 있습니다. 정책 및 준수 cmdlet에 대한 자세한 내용은 [정책 및 규정 준수 Cmdlet](https://technet.microsoft.com/ko-kr/library/dd298082\(v=exchg.150\))을 참조하세요.

사용자 지정 가능한 DLP 정책 자체 외에도, 규칙 위반 메시지를 보내기 전일지라도 정책 중 하나를 위반할 수 있음을 전자 메일 보낸 사람에게 알릴 수 있습니다. 이렇게 하려면 정책 설명을 구성할 수 있습니다. 정책 팁은 메일 설명과 비슷하며, 정책 팁을 구성하여 메시지를 작성하는 사람에게 발생할 수 있는 정책 위반에 대한 정보를 제공하는 간략한 메모를 Microsoft Outlook 2013 클라이언트에 표시할 수 있습니다. Exchange Online 최신 릴리스 및 Exchange 2013 SP1에서는 Outlook Web App 및 장치용 OWA에 정책 설명도 표시됩니다. 자세한 내용은 [정책 팁](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)을 참조하십시오.


> [!NOTE]
> Exchange Online: DLP는 Exchange Online 계획 2 구독이 필요한 고급 기능입니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online 라이선스</A>를 참조하세요.<BR>Exchange 2013: DLP는 CAL(Exchange Enterprise Client) 액세스 라이선스가 필요한 고급 기능입니다. CAL 및 서버 라이선스에 대한 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 라이선스</A>를 참조하세요.<BR><STRONG>Exchange Enterprise CAL(서비스 포함):</STRONG> 일부 사서함은 온-프레미스에 있고 일부 사서함은 Exchange Online에 있는 하이브리드 배포에서 Exchange Enterprise CAL(서비스 포함) 고객일 경우 주의해야 할 동작 차이점이 있습니다. Exchange Online에서는 DLP 정책이 적용됩니다. 따라서 특정 온-프레미스 사용자로부터 다른 온-프레미스 사용자에게 전송된 메시지에는 DLP 정책이 적용되지 않습니다. 이 메시지는 온-프레미스 인프라를 벗어나지 않기 때문입니다.



데이터 손실 방지와 관련된 관리 작업에 대한 자세한 내용은 [DLP 절차](dlp-procedures-exchange-2013-help.md)(Exchange 2013) 또는 [DLP 절차](https://technet.microsoft.com/ko-kr/library/jj938003\(v=exchg.150\))(Exchange Online)를 참조하세요.

**목차**

중요한 데이터를 보호하기 위한 정책 수립

DLP 정책의 중요한 정보 유형

일반적인 메시지 분류를 사용하여 중요한 정보 검색

문서 지문을 사용하여 표준 형식 데이터 검색

정책 팁에서는 중요한 콘텐츠와 관련한 기대 사항에 대해 사용자에게 알립니다.

DLP를 통해 처리된 메시지에 대한 정보

설치 필수 구성 요소

자세한 내용

## 중요한 데이터를 보호하기 위한 정책 수립

데이터 손실 방지 기능은 개인 식별 번호나 신용 카드 번호 같이 정책의 조건 내에서 정의한 다양한 범주의 중요한 정보를 식별하고 모니터링하는 데 유용합니다. 사용자 지정 정책과 전송 규칙을 직접 정의하거나, 빠른 시작을 위해 Microsoft에서 제공하는 미리 정의된 DLP 정책 템플릿을 사용할 수 있습니다. 포함된 정책 템플릿에 대한 자세한 내용은 [Exchange에서 제공 하는 DLP 정책 템플릿](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)을 참조하십시오. *정책 템플릿*에는 다양한 조건, 규칙 및 작업이 포함되어 있으므로 이 중에서 선택하여 메시지를 검사하는 데 유용한 실제 DLP를 만들어 저장할 수 있습니다. 정책 템플릿을 모델로 하여 상황에 맞는 규칙을 선택하거나 작성하면 데이터 손실 방지에 필요한 요건을 충족하는 정책을 쉽게 만들 수 있습니다.

다음과 같은 세 가지 방법으로 DLP를 사용하기 시작할 수 있습니다.

1.  **Microsoft의 기본 제공 템플릿 적용**   DLP 정책을 사용하기 시작하는 가장 빠른 방법은 템플릿을 사용하여 새 정책을 만들고 구현하는 것입니다. 그러면 템플릿을 사용하지 않을 때에 비해 간편하게 새 규칙 집합을 작성할 수 있습니다. 이때 확인할 데이터의 유형이나 처리하려는 준수 규정을 알고 있어야 합니다. 이러한 데이터를 처리하는 데 있어 조직에서 바라는 사항도 알고 있어야 합니다. 자세한 내용은 [Exchange에서 제공 하는 DLP 정책 템플릿](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md) 및 [템플릿에서 DLP 정책 만들기](how-to-new-dlp-data-loss-prevention-policy-template.md)를 참조하십시오.

2.  **조직 외부에서 미리 작성된 정책 파일 가져오기**   ISV(Independent Software Vendor)에서 메시징 환경의 외부에 이미 만든 정책을 가져올 수 있습니다. 이 방법을 사용하면 비즈니스 요구 사항에 맞게 DLP 솔루션을 확장할 수 있습니다. 자세한 내용은 [Microsoft 파트너 로부터 정책 서식 파일](policy-templates-from-microsoft-partners-exchange-2013-help.md), [자체 DLP 템플릿 및 정보 유형 정의](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md) 및 [파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)를 참조하십시오.

3.  **기존 조건을 사용하지 않고 사용자 지정 정책 만들기**   기업에는 메시징 시스템 내에 존재하는 것으로 알려진 특정 유형의 데이터를 모니터링하기 위한 고유한 요구 사항이 있을 수 있습니다. 고유한 메시지 데이터에 대한 확인 및 작업을 시작하기 위해 전적으로 사용자가 직접 사용자 지정 정책을 만들 수 있습니다. 이러한 사용자 지정 정책을 만들려면 DLP 정책이 적용될 환경의 요구 사항 및 제약 조건을 알고 있어야 합니다. 자세한 내용은 [사용자 지정 DLP 정책 만들기](create-a-custom-dlp-policy-exchange-2013-help.md)를 참조하십시오.

정책을 추가한 후에는 정책의 규칙을 검토 및 변경하거나 정책을 비활성화하거나 완전히 제거할 수 있습니다. 이러한 작업 절차는 [DLP 정책 관리](manage-dlp-policies-exchange-2013-help.md)를 참조하십시오.

## DLP 정책의 중요한 정보 유형

DLP 정책을 만들거나 변경할 때 중요한 정보에 대한 검사가 포함된 규칙을 포함할 수 있습니다. [Exchange의 중요 한 정보 유형 찾아보십시오](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) 항목에 나열된 중요한 정보 유형을 정책에 사용할 수 있습니다. 특정 정책 요구 사항을 충족하기 위해 정책 내에서 설정하는 조건(조치 작업을 수행하기 전에 특정 항목이 발견되어야 하는 횟수나 작업에 대한 정확한 정보 등)을 새 사용자 지정 정책 내에서 사용자 지정할 수 있습니다. DLP 정책 만들기에 대한 자세한 내용은 [사용자 지정 DLP 정책 만들기](create-a-custom-dlp-policy-exchange-2013-help.md)를 참조하십시오. 전체 전송 규칙에 대한 자세한 내용은 [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)(Exchange 2013) 또는 [Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\))(Exchange Online)을 참조하세요.

중요한 정보와 관련된 규칙을 쉽게 사용할 수 있도록 Microsoft에서는 중요한 정보 유형의 일부가 이미 포함된 정책 템플릿을 제공합니다. 여기에 나열된 모든 중요한 정보 유형에 대한 조건을 정책 템플릿에 추가할 수는 없지만, 이러한 템플릿을 사용하면 조직 내에서 규정 준수와 관련된 가장 일반적인 유형의 데이터에 초점을 맞추는 데 도움이 됩니다. 미리 작성된 템플릿에 대한 자세한 내용은 [Exchange에서 제공 하는 DLP 정책 템플릿](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)을 참조하십시오. 조직에서 사용할 다양한 DLP 정책을 만들고 이러한 정책을 모두 사용하도록 설정하여 매우 다양한 유형의 정보를 검사할 수 있습니다. 기존 템플릿을 기반으로 하지 않는 DLP 정책을 만들 수도 있습니다. 이러한 정책을 만들려면 [사용자 지정 DLP 정책 만들기](create-a-custom-dlp-policy-exchange-2013-help.md)를 참조하십시오. 중요한 정보 유형에 대한 자세한 내용은 [Exchange의 중요 한 정보 유형 찾아보십시오](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)를 참조하십시오.

## 문서 지문을 사용하여 표준 형식 데이터 검색

Exchange 2013 SP1 및 최신 Exchange Online 릴리스에서는 [문서 지문](overview-of-document-fingerprinting-in-exchange.md)를 사용하여 표준 형식을 기준으로 중요한 정보 유형을 쉽게 만들 수 있습니다. 양식 데이터를 보호하는 방법에 대한 자세한 내용은 [문서 지문을 사용 하 여 양식 데이터를 보호 합니다.](protect-form-data-with-document-fingerprinting-exchange-2013-help.md)를 참조하세요.

## 정책 팁에서는 중요한 콘텐츠와 관련한 기대 사항에 대해 사용자에게 알립니다.

정책 팁 알림 메시지를 사용하여 전자 메일 메시지를 작성할 때 발생할 수 있는 규정 준수 문제를 전자 메일을 보낸 사람에게 알릴 수 있습니다. DLP 정책에서 정책 팁을 구성하면 보낸 사람의 전자 메일 메시지에 포함된 요소가 정책에 설명된 조건을 충족할 경우에만 알림 메시지가 나타납니다. 정책 팁은 메일 설명과 유사한 기능으로, Exchange 2010에서 도입되었습니다. 자세한 내용은 [정책 팁](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)을 참조하십시오.

## 일반적인 메시지 분류를 사용하여 중요한 정보 검색

Exchange 2013과 Exchange Online에서는 일반적인 메시지 분류에 비해 메시지 및 첨부 파일 데이터 관리에 유용한 새로운 방법을 제공합니다. DLP 솔루션이 강력한 기능을 발휘할 수 있게 하는 주요 요인은 조직의 고유한 기밀 또는 중요 콘텐츠, 규제 요구 사항, 지리적 요건 또는 기타 비즈니스 요구 사항을 올바르게 식별하는 기능입니다. Exchange 2013에서는 깊이 있는 콘텐츠 분석을 위한 새로운 아키텍처와 DLP 정책의 규칙을 통해 설정하는 검색 조건을 함께 사용하여 이를 달성할 수 있습니다. Exchange 2013에서 데이터 손실을 효과적으로 방지하려면 높은 수준의 보호 기능을 제공하면서 가양성 및 거짓 부정으로 인한 부적절한 메일 흐름 중단을 최소화할 수 있도록 중요한 정보 규칙 집합을 올바르게 구성해야 합니다. DLP 정보 전체에서 중요한 정보 검색이라고 하는 이러한 유형의 규칙은 DLP 기능을 사용하기 위해 전송 규칙이 제공하는 프레임워크 내에서 작동합니다.

이러한 새 기능에 대한 자세한 내용은 [전송 규칙에 중요 한 정보 규칙 통합 (영문)](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)을 참조하세요. 일반적인 메시지 분류 필드를 Exchange의 메시지에 적용할 수도 있으며, 이러한 필드와 새로운 중요한 정보 검색 기능을 단일 DLP 정책 내에서 함께 사용하거나 동시에 실행하여 Exchange 내에서 독립적으로 평가되도록 할 수 있습니다. 기존의 Exchange 2010 메시지 분류에 대한 자세한 내용은 TechNet 라이브러리의 [메시지 분류 이해](https://go.microsoft.com/fwlink/?linkid=266612)를 참조하세요.

## DLP를 통해 처리된 메시지에 대한 정보

Exchange 2013에서 사용 중인 환경의 메시지 및 DLP 정책 검색에 대한 정보를 얻으려면 [DLP 정책 검색 보고서 보기](view-dlp-policy-detection-reports-exchange-2013-help.md) 및 [DLP 정책 감지에 대 한 문제 보고서 만들기](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)를 참조하세요. DLP 검색과 관련된 데이터는 Exchange 2013의 메시지 추적 도구인 배달 보고서에 통합되어 있습니다.

Exchange Online의 경우 [DLP 정책 검색 보고서 보기](https://technet.microsoft.com/ko-kr/library/dn904484\(v=exchg.150\)) 및 [\[Exchange Online\] DLP 정책 검색에 대 한 문제 보고서 만들기](https://technet.microsoft.com/ko-kr/library/dn904486\(v=exchg.150\))를 참조하세요.

## 설치 필수 구성 요소

DLP 기능을 사용하려면 Exchange 2013 또는 Exchange Online에 적어도 하나의 보낸 사람 사서함이 구성되어 있어야 합니다. DLP(데이터 손실 방지)는 CAL(클라이언트 액세스 라이선스)이 필요한 고급 기능입니다. Exchange 2013을 시작하는 방법에 대한 자세한 내용은 [계획 및 배포](planning-and-deployment-for-exchange-2013-installation-instructions.md)를 참조하십시오. Exchange Online을 시작하는 방법에 대한 자세한 내용은 [Exchange Online](https://technet.microsoft.com/ko-kr/library/jj200580\(v=exchg.150\))를 참조하십시오.

## 자세한 내용

Exchange 2013

  - [메시징 정책 및 규정 준수](messaging-policy-and-compliance-exchange-2013-help.md)

  - [DLP 절차](dlp-procedures-exchange-2013-help.md)

  - [DLP 정책 검색 보고서 보기](view-dlp-policy-detection-reports-exchange-2013-help.md)

  - [문서 지문](overview-of-document-fingerprinting-in-exchange.md)

  - [정책 및 규정 준수 Cmdlet](https://technet.microsoft.com/ko-kr/library/dd298082\(v=exchg.150\))

Exchange Online

  - [보안 및 Exchange Online에 대 한 규정 준수](https://technet.microsoft.com/ko-kr/library/jj200706\(v=exchg.150\))

  - [DLP 절차](https://technet.microsoft.com/ko-kr/library/jj938003\(v=exchg.150\))

  - [DLP 정책 검색 보고서 보기](https://technet.microsoft.com/ko-kr/library/dn904484\(v=exchg.150\))

  - [문서 지문](overview-of-document-fingerprinting-in-exchange.md)

