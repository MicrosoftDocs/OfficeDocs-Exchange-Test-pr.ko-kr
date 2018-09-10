---
title: '자체 DLP 템플릿 및 정보 유형 정의: Exchange 2013 Help'
TOCTitle: 자체 DLP 템플릿 및 정보 유형 정의
ms:assetid: f4622dba-3347-4758-b4a2-f01b043c908c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ674310(v=EXCHG.150)
ms:contentKeyID: 50484543
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 자체 DLP 템플릿 및 정보 유형 정의

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-14_

Microsoft Exchange Server 2013과는 별도로 DLP(데이터 손실 방지) 정책 템플릿을 XML 파일로 개발한 다음 Exchange 관리 센터나 Exchange 관리 셸을 사용하여 가져올 수 있습니다. 이 섹션에서는 DLP 솔루션 내에서 사용할 수 있도록 DLP XML 파일을 제작하고 튜닝하는 프로세스 및 세부 정보에 대해 설명합니다. Exchange 관리 센터는 기존 DLP 정책 템플릿 및 전송 규칙으로 메시지를 빠르게 검색하는 방법을 제공하므로 자체 DLP XML 파일을 개발할 필요가 없습니다.

DLP 정책 템플릿에 관련 된 관리 작업을 찾고 있습니까? [DLP 절차](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013 ) 또는 [DLP 절차](https://technet.microsoft.com/ko-kr/library/jj938003\(v=exchg.150\)) (Exchange Online )를 참조 하십시오.


> [!NOTE]
> Exchange 2013: DLP는 CAL(Exchange Enterprise Client) 액세스 라이선스가 필요한 고급 기능입니다. CAL 및 서버 라이선스에 대한 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 라이선스</A>를 참조하세요.<BR>Exchange Online: DLP는 Exchange Online 계획 2 구독이 필요한 고급 기능입니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online 라이선스</A>를 참조하세요.




> [!IMPORTANT]
> 이 설명서에서는 중요한 정보 규칙에 대한 파일 패키징 또는 배포 지침에 대한 비즈니스 모델이나 정보를 권장하거나 이러한 규칙이 배포되는 방식을 논의하지는 않습니다. 뿐만 아니라 사용자 개발 규칙에 대한 암호화 같은 보호 메커니즘을 다루거나 이러한 메커니즘이 사용되는 방식을 논의하지도 않습니다.



## 필요에 맞게 정보 형식 확장

다음 섹션에서는 Exchange 2013으로 가져오고 DLP 정책으로 사용할 수 있는 중요한 정보 규칙 패키지 및 DLP 정책 템플릿에 대한 자체 XML 파일을 생성하기 위해 이해해야 하는 개념 및 XML 스키마 정의에 대해 설명합니다.

Microsoft Exchange의 DLP는 조직별 정책을 중요한 정보에 적용하는 데 도움을 줍니다. DLP 솔루션의 가장 핵심 장점은 조직, 규정 요구, 지리적 위치 또는 비즈니스의 기타 측면에 고유할 수 있는 기밀 또는 중요한 정보를 올바르게 식별하는 능력입니다. Microsoft에서 제품 내에 업무 시작을 위한 정책 템플릿과 중요한 정보 유형을 제공하고 있지만 비즈니스 요구에 따라 사용자 지정 데이터 손실 방지 솔루션이 필요할 수도 있습니다. 따라서 Microsoft는 자체 DLP 정책 템플릿이나 중요한 정보 정의를 만든 후 분류 규칙 패키지로 가져오는 방법을 제공합니다. DLP 솔루션이 정확하려면 가양성 및 거짓 부정을 최소화하면서 높은 수준의 보호를 제공하는 적절한 중요한 정보 검색 엔진용 규칙 집합을 구성할 수 있어야 합니다.

## 자체 DLP 정책 템플릿 개발

자체 DLP 정책 템플릿 XML 파일을 작성한 후 가져올 수 있습니다. 이러한 Exchange에 제공된 DLP 솔루션 확장 방법을 통해 DLP 요구 사항에 잘 맞는 DLP 정책을 구축할 수 있습니다.

사용자 지정 템플릿 및 해당 관련 정책을 관리하는 일은 Microsoft-제공 템플릿을 기반으로 만든 DLP 정책을 관리하는 것과 비슷합니다. 일반적인 DLP 정책 수명 주기에서는 다음을 수행합니다.

1.  자체의 DLP 정책 템플릿인 사용자 지정 XML 파일을 만듭니다. 자세한 내용은 [DLP 정책 템플릿 파일 개발](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)을 참조하세요.

2.  사용자 지정 템플릿을 가져옵니다. 자세한 내용은 [파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)를 참조하세요.

3.  사용자 지정 템플릿을 기반으로 하는 DLP 정책을 만듭니다. 자세한 내용은 [템플릿에서 DLP 정책 만들기](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/create-dlp-policy-from-template)를 참조하세요.

4.  1~2단계를 반복하여 사용자 지정 템플릿을 업데이트합니다.

5.  사용자 지정 템플릿을 제거합니다. 자세한 내용은 [Remove-DlpPolicyTemplate](https://technet.microsoft.com/ko-kr/library/jj215739\(v=exchg.150\))을 참조하세요.

XML 스키마 정의 및 자체 템플릿 개발과 관련된 개념에 대한 자세한 내용은 [DLP 정책 템플릿 파일 개발](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)을 참조하십시오.

## 분류 규칙 패키지 형태의 자체 중요한 정보 유형 및 일치 논리 개발

XML 파일에 해당하는 분류 규칙 패키지로 자체 중요한 정보 정의를 작성한 다음 DLP 솔루션의 일부로 가져올 수 있습니다. 중요한 정보 검색 엔진은 신용 카드 번호, 주민 등록 번호 및 회사 지적 재산권과 같은 중요한 정보를 식별하기 위한 심도 깊은 콘텐츠 분석 기능을 제공합니다. 이 엔진은 콘텐츠를 검색하고 분석하기 위한 구성 가능한 지침 또는 규칙 집합을 통해 제어됩니다. 이러한 규칙은 함께 결합되어 표준화된 규칙 패키지 XML 스키마 정의를 준수하는 XML 문서에 해당하는 분류 규칙 패키지가 됩니다. 자체 스키마 정의 개발 방법은 다음과 같습니다.

1.  중요한 정보 유형인 사용자 지정 XML 파일을 직접 만듭니다. 자세한 내용은 [중요 한 정보 규칙 패키지 개발 (영문)](technical-description-of-xml-schema-for-dlp-rule-packages.md)을 참조하세요.

2.  중요한 정보 유형을 가져옵니다. 자세한 내용은 [New-ClassificationRuleCollection](https://technet.microsoft.com/ko-kr/library/jj218619\(v=exchg.150\))을 참조하십시오.

3.  정보 유형에 따라 사용자 지정 템플릿을 만듭니다. 자세한 내용은 [중요 한 정보 규칙 패키지 개발 (영문)](technical-description-of-xml-schema-for-dlp-rule-packages.md)을 참조하세요.

4.  1~2단계를 반복하여 사용자 지정 템플릿을 업데이트합니다.

5.  사용자 지정 템플릿을 제거합니다. 자세한 내용은 [Remove-ClassificationRuleCollection](https://technet.microsoft.com/ko-kr/library/jj218670\(v=exchg.150\))을 참조하세요.

규칙 패키지에 대한 자세한 내용은 [중요 한 정보 규칙 패키지 개발 (영문)](technical-description-of-xml-schema-for-dlp-rule-packages.md) 및 [일치 하는 방법 및 규칙 패키지에 대 한 기술](technical-description-of-xsd-rule-matching-for-dlp-rule-packages.md)를 참조하십시오.

## 패키지 규칙의 규칙 유형 이해

규칙 패키지 내의 규칙은 잘 정의된 콘텐츠 특성을 검색하기 위한 프로세스를 구성합니다(예: 운전 면허 번호를 찾기 위한 규칙). 다음 두 가지 주요 규칙 유형을 사용할 수 있습니다. 엔터티 및 선호도입니다.

*엔터티* 규칙은 주민 등록 번호와 같은 잘 정의된(규제되는) 식별자를 대상으로 합니다. 엔터티는 셀 수 있는 패턴의 모음으로 나타냅니다. 패턴은 명시적인 기본 일치 식별자를 기준으로 하는 일치 항목 모음입니다. 엔터티의 예로 운전 면허증을 들 수 있습니다.

*선호도* 규칙은 회사 재무 제표와 같은 특정 유형의 문서를 대상으로 합니다. 선호도는 독립적인 증거의 모음으로 나타냅니다. 증거는 일정한 근접 내에 있는 필요한 일치 항목의 집합입니다. 선호도의 예로 미국 Sarbanes-Oxley Act를 들 수 있습니다.

## 자세한 내용

[데이터 손실 방지](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

[New-ClassificationRuleCollection](https://technet.microsoft.com/ko-kr/library/jj218619\(v=exchg.150\))

[메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange Server 2013

[Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\)) Exchange Online

[Exchange의 중요 한 정보 유형 찾아보십시오](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

