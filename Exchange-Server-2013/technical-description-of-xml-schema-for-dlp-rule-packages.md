---
title: '중요 한 정보 규칙 패키지 개발 (영문): Exchange 2013 Help'
TOCTitle: 중요 한 정보 규칙 패키지 개발 (영문)
ms:assetid: c4ab8707-0839-4855-9390-3dbcb43475a7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ674704(v=EXCHG.150)
ms:contentKeyID: 50484107
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 중요 한 정보 규칙 패키지 개발 (영문)

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-07-28_

이 항목의 XML 스키마 및 지침은 분류 규칙 패키지에서 중요한 정보 유형을 정의하는 기본 DLP(데이터 손실 방지) XML 파일을 직접 만들어 보는 데 도움이 됩니다. 잘 구성된 XML 파일을 만들면 Microsoft Exchange Server 2013 DLP 솔루션을 만드는 데 사용할 수 있도록 Exchange 관리 센터 또는 Exchange 관리 셸을 통해 해당 파일을 가져올 수 있습니다. 사용자 지정 DLP 정책 템플릿인 XML 파일에는 분류 규칙 패키지인 XML이 포함될 수 있습니다. 자신의 DLP 템플릿을 XML 파일로 정의하는 방법에 대한 개요는 [자체 DLP 템플릿 및 정보 유형 정의](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)를 참조하십시오.

**목차**

Overview of the rule authoring process

Rule description

Basic rule structure

Using local languages in your XML file

Classification rule pack XML schema definition

For more information

## 규칙 작성 프로세스의 개요

규칙 작성 프로세스는 다음과 같은 일반적인 단계로 구성됩니다.

1.  대상 환경의 테스트 문서 대표 집합을 준비합니다. 테스트 문서 집합에 대해 고려해야 할 주요 사항은 규칙이 작성되는 엔터티나 선호도를 포함하는 문서의 하위 집합 그리고 규칙이 작성되는 엔터티나 선호도를 포함하지 않는 문서의 하위 집합입니다.

2.  적격 콘텐츠를 식별하기 위해 수용 요구 사항(정밀도 및 회수)을 충족하는 규칙을 확인합니다. 이를 위해서는 대상 문서를 식별하기 위한 최소 일치 요구 사항을 함께 충족하는 규칙 내 여러 조건(부울 논리를 사용하여 바인딩)의 개발이 필요할 수 있습니다.

3.  수용 요구 사항(정밀도 및 회수)을 기반으로 규칙에 대한 권장 신뢰 수준을 설정합니다. 권장 신뢰도 요소가 규칙의 기본 신뢰 수준으로 간주될 수 있습니다.

4.  규칙을 사용하여 정책을 인스턴스화하고 샘플 테스트 콘텐츠를 모니터링하여 규칙의 유효성을 검사합니다. 결과를 기반으로 규칙 또는 신뢰 수준을 조정하여 가양성 및 가음성을 최소화하는 동시에 검색되는 콘텐츠를 최대화합니다. 양성 및 음성 샘플 모두에 대해 만족스러운 콘텐츠 검색 수준에 도달할 때까지 유효성 검사 및 규칙 조정을 계속합니다.

정책 템플릿 파일의 XML 스키마 정의에 대한 자세한 내용은 [DLP 정책 템플릿 파일 개발](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)을 참조하십시오.

## 규칙 설명

DLP 중요한 정보 검색 엔진에 대해 두 가지 주요 규칙 유형인 엔터티 및 선호도를 작성할 수 있습니다. 선택된 규칙 유형은 앞 섹션에서 설명한 대로 콘텐츠 처리에 적용해야 할 처리 논리 유형을 기반으로 합니다. 규칙 정의는 표준화된 규칙 XSD에서 설명하는 형식으로 XML 문서에 구성됩니다. 규칙은 일치시킬 콘텐츠 유형과 설명된 일치가 대상 콘텐츠를 나타내는 신뢰 수준을 모두 설명합니다. 신뢰 수준은 콘텐츠에서 패턴이 검색될 경우 엔터티가 나타날 가능성 또는 콘텐츠에서 증거가 검색될 경우 선호도가 나타날 가능성을 지정합니다.

## 기본 규칙 구조

규칙 정의는 세 가지 주요 구성 요소로 구성됩니다.

1.  **엔터티**   해당 규칙에 대한 일치 및 계산 논리 정의

2.  **선호도**   규칙에 대한 일치 논리 정의

3.  **지역화된 문자열**   규칙 이름 및 설명에 대한 지역화

처리의 세부 사항을 정의하는 데 사용되고 이러한 주요 구성 요소에서 참조되는 세 가지 추가 지원 요소는 키워드, regex 및 함수입니다. 참조를 사용하면 주민등록번호 같은 지원 요소의 단일 정의를 여러 엔터티 또는 선호도 규칙에 사용할 수 있습니다. XML 형식의 기본 규칙 구조는 다음과 같이 나타날 수 있습니다.

    <?xml version="1.0" encoding="utf-8"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
    
      <RulePack id="DAD86A92-AB18-43BB-AB35-96F7C594ADAA">
        <Version major="1" minor="0" build="0" revision="0"/>
        <Publisher id="619DD8C3-7B80-4998-A312-4DF0402BAC04"/>
        <Details defaultLangCode="en-us">
          <LocalizedDetails langcode="en-us">
            <PublisherName>DLP by EPG</PublisherName>
            <Name>CSO Custom Rule Pack</Name>
            <Description>This is a rule package for a EPG demo.</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
    
      <Rules>
    
        <!-- Employee ID -->
        <Entity id="E1CC861E-3FE9-4A58-82DF-4BD259EAB378" patternsProximity="300" recommendedConfidence="75">
          <Pattern confidenceLevel="75">
            <IdMatch idRef="Regex_employee_id" />
            <Match idRef="Keyword_employee" />
          </Pattern>
        </Entity>
    
        <Regex id="Regex_employee_id">(\s)(\d{9})(\s)</Regex>
        <Keyword id="Keyword_employee">
          <Group matchStyle="word">
            <Term>Identification</Term>
            <Term>Contoso Employee</Term>
          </Group>
        </Keyword>
    
    
        <LocalizedStrings>
    
          <Resource idRef="E1CC861E-3FE9-4A58-82DF-4BD259EAB378">
            <Name default="true" langcode="en-us">
              Employee ID
            </Name>
            <Description default="true" langcode="en-us">
              A custom classification for detecting Employee ID's
            </Description>
          </Resource>
    
        </LocalizedStrings>
      </Rules>
    </RulePackage>

## 엔터티 규칙

엔터티 규칙은 잘 정의된 식별자(예: 주민등록번호)를 대상으로 하며 계산할 수 있는 패턴의 모음으로 나타냅니다. 엔터티 규칙은 일치의 개수와 신뢰 수준을 반환합니다. 여기서 개수는 검색된 엔터티 인스턴스의 총 수이고 신뢰 수준은 지정된 엔터티가 지정된 문서에 있을 가능성입니다. 엔터티는 "id" 특성을 고유한 식별자로 포함합니다. 식별자는 지역화, 버전 관리 및 쿼리에 사용됩니다. 엔터티 id는 GUID여야 하고 다른 엔터티나 선호도에서 중복되어서는 안 되며, 지역화된 문자열 섹션에서 참조됩니다.

엔터티 규칙은 선택 사항인 patternsProximity 특성(기본값 = 300)을 포함합니다. 이 특성은 일치 조건을 만족시키는 데 필요한 여러 패턴의 인접성을 지정하기 위해 부울 논리를 적용할 때 사용됩니다. 엔터티 요소에는 하나 이상의 하위 패턴 요소가 포함되며, 여기서 각 패턴은 신용카드 엔터티 또는 운전면허 엔터티 등 개별적인 엔터티 표현입니다. 패턴 요소에는 샘플 데이터 집합을 기반으로 패턴의 정밀도를 나타내는 필수 특성인 confidenceLevel이 있습니다. 패턴 요소는 세 개의 자식 요소를 가질 수 있습니다.

1.  IdMatch - 필수 항목입니다.

2.  Match

3.  모두

임의의 패턴 요소가 \&quot;true\&quot;를 반환하면 패턴이 충족됩니다. 엔터티 요소의 수는 검색된 모든 패턴 수의 합과 같습니다.

![엔터티 개수에 대한 수식](images/JJ674704.25309939-98bc-4460-8f89-8560bbad7981(EXCHG.150).gif "엔터티 개수에 대한 수식")

여기서 k는 엔터티의 패턴 요소 수입니다.

패턴 요소에는 IdMatch 요소가 하나만 있어야 합니다. IdMatch는 신용카드 번호 또는 ITIN 번호 등, 패턴과 일치될 식별자를 나타냅니다. 패턴의 수는 패턴 요소와 일치되는 IdMatch의 수입니다. IdMatch 요소는 Match 요소에 대한 근접성 윈도우를 연결합니다.

패턴 요소의 다른 선택적 하위 요소는 IdMatch 요소 찾기 (영문)를 지원 하기 위해 일치 하는 데 필요한 확증 적 인증 거 나타내는 일치 하는 요소입니다. 예, 찾기 (영문) 신용 카드 번호, 외에도 추가 아티팩트에에서 존재 하는 주소와 이름이 같은 신용 카드의 근접성 창 내에서 문서를 더 높은 신뢰도 규칙이 필요할 수 있습니다. 일치 하는 요소 또는 (이러한 메서드 일치 하는 방법과 기술을 섹션에서 자세하게에서 설명 된) 모든 요소를 통해 이러한 추가 아티팩트를 나타낼 수 합니다. 패턴 요소에 직접 포함 될 수 또는 Any 요소를 사용 하 여 일치 하는 의미를 정의할 수 결합 하는 패턴 정의에 여러 일치 하는 요소를 포함할 수 있습니다. IdMatch 콘텐츠 주위의 고정 근접 창에서 일치 하는 경우 true를 반환 합니다.

IdMatch 및 Match 요소는 일치시킬 콘텐츠의 세부 사항을 정의하는 대신 idRef 특성을 통해 콘텐츠를 참조합니다. 이에 따라 여러 패턴 구성체에서 정의를 다시 사용할 수 있는 기회가 많아집니다.

    <Entity id="..." patternsProximity="300" > 
        <Pattern confidenceLevel="85">
            <IdMatch idRef="FormattedSSN" />
            <Any minMatches="1">
                <Match idRef="SSNKeyword" />
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>  
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Match idRef="SSNKeyword" />
            <Any minMatches="1">        
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity> 

앞의 XML에서 \&quot;…\&quot;로 나타낸 Entity id 요소는 GUID여야 하며 지역화된 문자열 섹션에서 참조됩니다.

## 엔터티 패턴 근접성 윈도우

엔터티에는 패턴을 찾는 데 사용되는 선택 사항인 patternsProximity 특성 값(정수, 기본값 = 300)이 있습니다. 각 패턴의 경우 특성 값은 해당 패턴에 대해 지정된 다른 모든 Match의 IdMatch 위치로부터 거리를 (유니코드 문자로) 정의합니다. 근접성 윈도우는 IdMatch 위치에 의해 IdMatch의 좌우로 확장되는 윈도우와 연결됩니다.

![일치하는 요소가 호출된 텍스트 패턴](images/JJ674704.65d52989-f50f-4097-b39a-9612f860d727(EXCHG.150).gif "일치하는 요소가 호출된 텍스트 패턴")

아래 예에서는 SSN IdMatch 요소가 적어도 하나의 주소, 이름 또는 날짜 보강 일치를 필요로 하는 일치 알고리즘에 근접성 윈도우가 어떻게 영향을 주는지 보여줍니다. SSN2와 SSN3의 경우 근접성 윈도우 내에 보강 증거의 일부만 있거나, 전혀 없으므로 SSN1과 SSN4만 일치합니다.

![근접 규칙 일치/비일치 예제](images/JJ674704.8117deb3-d8c8-4d4e-a011-ac5f9990b08e(EXCHG.150).gif "근접 규칙 일치/비일치 예제")

참고 메시지 본문 및 각 첨부 파일 독립 항목으로 처리 됩니다. 즉, 이러한 각 항목의 끝을 지 나 근접 창을 확장 합니다. 각 항목 (첨부 파일 또는 본문) idMatch와 확증 적 인증 거 각 내에 있는 해야 합니다.

## 엔터티 신뢰 수준

엔터티 요소의 신뢰 수준은 충족되는 모든 패턴의 신뢰 수준을 조합한 것입니다. 충족되는 패턴의 신뢰 수준은 다음 수식을 사용하여 결합됩니다.

![엔터티 신뢰 수준에 대한 수식](images/JJ674704.9b8bb9c8-3ded-4ea5-a609-71d8034b1017(EXCHG.150).gif "엔터티 신뢰 수준에 대한 수식")

여기서 k는 엔터티에 대한 패턴 요소의 수이며, 일치하지 않는 패턴은 신뢰 수준 0을 반환합니다.

엔터티 요소 구조 코드 샘플의 예로 다시 돌아가, 두 패턴이 모두 일치하는 경우 엔터티의 신뢰 수준은 다음 계산에 따라 94.75%입니다.

CLEntity= 1-\[(1-CLPattern1) x (1-CLPattern1)\]

*= 1-\[(1-0.85) x (1-0.65)\]*

*= 1-(0.15 x 0.35)*

*= 94.75%*

이와 유사하게 두 번째 패턴만 일치하는 경우 엔터티의 신뢰 수준은 다음 계산에 따라 65%입니다.

CLEntity= 1 – \[(1 – CLPattern1) X (1 – CLPattern1)\]

*= 1 – \[(1 – 0) X (1 – 0.65)\]*

*= 1 – (1 X 0.35)*

*= 65%*

이러한 신뢰도 값은 규칙 작성 프로세스의 일부로 유효성이 검사된 테스트 문서 집합을 기반으로 개별 패턴에 대한 규칙에 할당됩니다.

## 선호도 규칙

선호도 규칙은 Sarbanes-Oxley나 회사 재무 콘텐츠와 같이 잘 정의된 식별자가 없는 콘텐츠를 대상으로 합니다. 이러한 콘텐츠의 경우 일관된 단일 식별자를 찾을 수 없으므로, 분석에서 증거 모음이 있는지 확인해야 합니다. 선호도 규칙은 수를 반환하지 않는 대신 관련된 신뢰 수준이 있으면 이를 반환합니다. 선호도 콘텐츠는 개별 증거의 모음으로 나타냅니다. 증거는 일정한 근접 내에 있는 필요한 일치 항목의 집합입니다. 선호도 규칙의 경우 근접성은 evidencesProximity 특성(기본 값 600)에 의해 정의되고 최소 신뢰 수준은 thresholdConfidenceLevel 특성에 의해 정의됩니다.

선호도 규칙은 지역화, 버전 관리 및 쿼리에 사용되는 고유 식별자의 id 특성을 포함합니다. 선호도 규칙은 잘 정의된 식별자를 사용하지 않으므로, 엔터티 규칙과는 달리 IdMatch 요소는 포함하지 않습니다.

각 선호도 규칙에는 검색할 증거와 해당 선호도 규칙에 기여하는 신뢰 수준을 정의하는 하나 이상의 자식 증거 요소가 있습니다. 선호도는 결과 신뢰 수준이 임계값 수준 미만이면 검색된 것으로 간주되지 않습니다. 각 Evidence는 논리적으로 이 문서 "형식"에 대한 보강 증거를 나타내며 confidenceLevel 특성은 테스트 데이터 집합에서 해당 증거에 대한 정밀도입니다.

증거 요소에는 하나 이상의 Match 또는 Any 자식 요소가 있습니다. 자식 Match 요소와 Any 요소가 일치하면 증거가 검색되고 신뢰 수준은 규칙 신뢰 수준 계산에 반영됩니다. 엔터티 규칙과 마찬가지로 선호도 규칙에 대해서도 Match 또는 Any 요소에 동일한 설명이 적용됩니다.

    <Affinity id="..." 
              evidencesProximity="1000"
              thresholdConfidenceLevel="65">
        <Evidence confidenceLevel="40">
            <Any> 
                <Match idRef="AssetsTerms" /> 
                <Match idRef="BalanceSheetTerms" /> 
                <Match idRef="ProfitAndLossTerms" /> 
            </Any> 
        </Evidence>
        <Evidence confidenceLevel="40">
            <Any minMatches="2"> 
                <Match idRef="TaxTerms" /> 
                <Match idRef="DollarAmountTerms" /> 
                <Match idRef="SECTerms" /> 
                <Match idRef="SECFilingFormTerms" /> 
                <Match idRef="DollarTotalRegex" /> 
            </Any> 
        </Evidence>
    </Affinity>

## 선호도 근접성 윈도우

선호도에 대한 근접성 윈도우는 엔터티 패턴과는 다르게 계산됩니다. 선호도 근접성은 슬라이딩 윈도우 모델을 따릅니다. 선호도 근접성 알고리즘은 지정된 윈도우에서 최대 일치 증거 수 검색을 시도합니다. 근접성 윈도우의 증거는 검색할 선호도 규칙에 대해 정의된 임계값보다 높은 신뢰 수준을 가져야 합니다.

![선호도 규칙 일치의 근접성 텍스트](images/JJ674704.2601ec86-0094-43fa-8d22-9d97f7465942(EXCHG.150).gif "선호도 규칙 일치의 근접성 텍스트")

## 선호도 신뢰 수준

선호도의 신뢰 수준은 선호도 규칙에 대한 근접성 윈도우 내에서 검색한 증거의 조합과 같습니다. 엔터티 규칙의 신뢰 수준과 유사하지만 주요 차이점은 근접성 윈도우의 응용 프로그램입니다. 엔터티 규칙과 유사하게, 선호도 요소의 신뢰 수준은 충족되는 모든 증거 신뢰 수준의 조합이지만 선호도 규칙의 경우 근접성 윈도우 내에서 검색한 증거 요소의 최고 조합만을 나타냅니다. 증거 신뢰 수준은 다음 수식을 사용하여 결합됩니다.

![선호도 규칙 신뢰도에 대한 수식](images/JJ674704.8a5da4ca-af02-4c5a-ab60-0072dc7e7a0f(EXCHG.150).gif "선호도 규칙 신뢰도에 대한 수식")

여기서 k는 근접성 윈도우 내에서 일치된 선호도에 대한 증거 요소의 수입니다.

그림 4 선호도 규칙 구조 예로 다시 돌아가서, 근접성 슬라이딩 윈도우 내에서 세 개의 증거가 모두 일치하는 경우 선호도 수준은 아래 계산에 따라 85.6%입니다. 이 값은 규칙 일치의 결과인 선호도 규칙 임계값 65를 초과합니다.

CL선호도= 1 – \[(1 – CL증거 1) X (1 – CL증거 2) X (1 – CL증거 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0.4) X (1 – 0.4)\]*

*= 1 – (0.4 X 0.6 X 0.6)*

*= 85.6%*

![신뢰도가 높은 선호도 규칙 일치 예제](images/JJ674704.e17b2e22-18c3-40c4-8f19-0993bb556675(EXCHG.150).gif "신뢰도가 높은 선호도 규칙 일치 예제")

동일한 규칙 정의 예에서 두 번째 증거가 근접성 윈도우의 외부에 있어 첫 번째 증거만 일치하는 경우 가장 높은 선호도 신뢰 수준은 아래 계산에 따라 60%이며 임계값 65를 충족하지 않으므로 선호도 규칙이 일치하지 않습니다.

CL선호도= 1 – \[(1 – CL증거 1) X (1 – CL증거 2) X (1 – CL증거 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0) X (1 – 0)\]*

*= 1 – (0.4 X 1 X 1)*

*= 60%*

![신뢰도가 낮은 선호도 규칙 일치 예제](images/JJ674704.077095b1-6eb0-40df-b254-f33437725720(EXCHG.150).gif "신뢰도가 낮은 선호도 규칙 일치 예제")

## 신뢰 수준 조정

규칙 작성 프로세스의 핵심 단계 중 하나는 엔터티 및 선호도 규칙 둘 다에 대한 신뢰 수준을 조정하는 것입니다. 규칙 정의를 만든 다음 대표 콘텐츠에 대해 규칙을 실행하고 정확성 데이터를 수집합니다. 각 패턴 또는 증거에 대한 반환 결과와 테스트 문서의 예상 결과를 비교합니다.

![규칙 일치 증거 비교 테이블](images/JJ674704.25a7d9a1-d02f-447e-a88b-8e78bdc0413a(EXCHG.150).gif "규칙 일치 증거 비교 테이블")

규칙이 수용 요구 사항을 충족할 경우, 다시 말해 패턴이나 증거의 신뢰 수준이 설정된 임계값(예: 75%)보다 높으면 일치 식이 완료되고 다음 단계로 이동할 수 있습니다.

패턴이나 증거가 신뢰 수준을 충족하지 못하면 이를 다시 작성(보강 증거 추가, 추가 패턴/증거 제거 또는 추가)하고 이 단계를 반복합니다.

다음으로 이전 단계의 결과를 기반으로 규칙에서 각 패턴 또는 증거의 신뢰 수준을 조정합니다. 각 패턴 또는 증거에 대해 규칙이 작성되고 있는 엔터티 또는 선호도를 포함하고 일치를 반환한 문서의 하위 집합인 TP(진양성)의 수와 규칙이 작성되고 있는 엔터티 또는 선호도를 포함하지 않고 일치를 반환한 문서의 하위 집합인 FP(가양성)의 수를 집계합니다. 다음 계산을 사용하여 각 패턴/증거에 대한 신뢰 수준을 설정합니다.

*신뢰 수준 = 진양성 / (진양성 + 가양성)*


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>패턴 또는 증거</th>
<th>진양성</th>
<th>가양성</th>
<th>신뢰 수준</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>P1또는 E1</p></td>
<td><p>4</p></td>
<td><p>1</p></td>
<td><p>80%</p></td>
</tr>
<tr class="even">
<td><p>P2또는 E2</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>Pn또는 En</p></td>
<td><p>9</p></td>
<td><p>10</p></td>
<td><p>47%</p></td>
</tr>
</tbody>
</table>


## XML 파일에 현지 언어 사용

규칙 스키마는 각 엔터티 및 선호도 요소의 지역화된 이름과 설명을 저장하도록 지원합니다. 각 엔터티 및 선호도 요소의 LocalizedStrings 섹션에는 해당 요소가 포함되어야 합니다. 각 요소를 지역화하려면 각 요소의 다양한 로캘에 대한 이름과 설명을 저장하도록 리소스 요소를 LocalizedStrings 요소의 자식으로 포함하십시오. 리소스 요소는 지역화되는 각 요소에 대한 해당 idRef 특성과 일치하는 필수 idRef 특성을 포함합니다. 리소스 요소의 로캘 자식 요소는 지정된 각 로캘에 대한 지역화된 이름과 설명을 포함합니다.

    <LocalizedStrings>
        <Resource idRef="guid">
            <Locale langcode="en-US" default="true"> 
                <Name>affinity name en-us</Name> 
                <Description>
                    affinity description en-us
                </Description> 
            </Locale> 
            <Locale langcode="de"> 
                <Name>affinity name de</Name> 
                <Description>
                    affinity description de
                </Description> 
            </Locale> 
        </Resource>
    </LocalizedStrings>

## 분류 규칙 팩 XML 스키마 정의

    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:mce="http://schemas.microsoft.com/office/2011/mce"
               targetNamespace="http://schemas.microsoft.com/office/2011/mce" 
               xmlns:xs="http://www.w3.org/2001/XMLSchema"
               elementFormDefault="qualified"
               attributeFormDefault="unqualified"
               id="RulePackageSchema">
      <xs:simpleType name="LangType">
        <xs:union memberTypes="xs:language">
          <xs:simpleType>
            <xs:restriction base="xs:string">
              <xs:enumeration value=""/>
            </xs:restriction>
          </xs:simpleType>
        </xs:union>
      </xs:simpleType>
      <xs:simpleType name="GuidType" final="#all">
        <xs:restriction base="xs:token">
          <xs:pattern value="[0-9a-fA-F]{8}\-([0-9a-fA-F]{4}\-){3}[0-9a-fA-F]{12}"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulePackageType">
        <xs:sequence>
          <xs:element name="RulePack" type="mce:RulePackType"/>
          <xs:element name="Rules" type="mce:RulesType">
            <xs:key name="UniqueRuleId">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueProcessorId">
              <xs:selector xpath="mce:Regex|mce:Keyword"></xs:selector>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueResourceIdRef">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:key>        
            <xs:keyref name="ReferencedRuleMustExist" refer="mce:UniqueRuleId">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:keyref>
            <xs:keyref name="RuleMustHaveResource" refer="mce:UniqueResourceIdRef">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:keyref>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="RulePackType">
        <xs:sequence>
          <xs:element name="Version" type="mce:VersionType"/>
          <xs:element name="Publisher" type="mce:PublisherType"/>
          <xs:element name="Details" type="mce:DetailsType">
            <xs:key name="UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="mce:LocalizedDetails"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:keyref name="DefaultLangCodeMustExist" refer="mce:UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="."/>
              <xs:field xpath="@defaultLangCode"/>
            </xs:keyref>
          </xs:element>
          <xs:element name="Encryption" type="mce:EncryptionType" minOccurs="0" maxOccurs="1"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="VersionType">
        <xs:attribute name="major" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="minor" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="build" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="revision" type="xs:unsignedShort" use="required"/>
      </xs:complexType>
      <xs:complexType name="PublisherType">
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="LocalizedDetailsType">
        <xs:sequence>
          <xs:element name="PublisherName" type="mce:NameType"/>
          <xs:element name="Name" type="mce:RulePackNameType"/>
          <xs:element name="Description" type="mce:OptionalNameType"/>
        </xs:sequence>
        <xs:attribute name="langcode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="DetailsType">
        <xs:sequence>
          <xs:element name="LocalizedDetails" type="mce:LocalizedDetailsType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="defaultLangCode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="EncryptionType">
        <xs:sequence>
          <xs:element name="Key" type="xs:normalizedString"/>
          <xs:element name="IV" type="xs:normalizedString"/>
        </xs:sequence>
      </xs:complexType>
      <xs:simpleType name="RulePackNameType">
        <xs:restriction base="xs:token">
          <xs:minLength value="1"/>
          <xs:maxLength value="64"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="NameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="1"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="OptionalNameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="0"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="RestrictedTermType">
        <xs:restriction base="xs:string">
          <xs:minLength value="1"/>
          <xs:maxLength value="512"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulesType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Entity" type="mce:EntityType"/>
            <xs:element name="Affinity" type="mce:AffinityType"/>
          </xs:choice>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Regex" type="mce:RegexType"/>
            <xs:element name="Keyword" type="mce:KeywordType"/>
          </xs:choice>
          <xs:element name="LocalizedStrings" type="mce:LocalizedStringsType"/>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="EntityType">
        <xs:sequence>
          <xs:element name="Pattern" type="mce:PatternType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="patternsProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="recommendedConfidence" type="mce:ProbabilityType"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="PatternType">
        <xs:sequence>
          <xs:element name="IdMatch" type="mce:IdMatchType"/>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="AffinityType">
        <xs:sequence>
          <xs:element name="Evidence" type="mce:EvidenceType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="evidencesProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="thresholdConfidenceLevel" type="mce:ProbabilityType" use="required"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="EvidenceType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="IdMatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="MatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="AnyType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="minMatches" type="xs:nonNegativeInteger" default="1"/>
        <xs:attribute name="maxMatches" type="xs:nonNegativeInteger" use="optional"/>
      </xs:complexType>
      <xs:simpleType name="ProximityType">
        <xs:restriction base="xs:positiveInteger">
          <xs:minInclusive value="1"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="ProbabilityType">
        <xs:restriction base="xs:integer">
          <xs:minInclusive value="1"/>
          <xs:maxInclusive value="100"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="WorkloadType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Exchange"/>
          <xs:enumeration value="Outlook"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RegexType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="id" type="xs:token" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="KeywordType">
        <xs:sequence>
          <xs:element name="Group" type="mce:GroupType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="xs:token" use="required"/>
      </xs:complexType>
      <xs:complexType name="GroupType">
        <xs:sequence>
          <xs:choice>
            <xs:element name="Term" type="mce:TermType" maxOccurs="unbounded"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="matchStyle" default="word">
          <xs:simpleType>
            <xs:restriction base="xs:NMTOKEN">
              <xs:enumeration value="word"/>
              <xs:enumeration value="string"/>
            </xs:restriction>
          </xs:simpleType>
        </xs:attribute>
      </xs:complexType>
      <xs:complexType name="TermType">
        <xs:simpleContent>
          <xs:extension base="mce:RestrictedTermType">
            <xs:attribute name="caseSensitive" type="xs:boolean" default="false"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="LocalizedStringsType">
        <xs:sequence>
          <xs:element name="Resource" type="mce:ResourceType" maxOccurs="unbounded">
            <xs:key name="UniqueLangCodeUsedInNamePerResource">
              <xs:selector xpath="mce:Name"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:key name="UniqueLangCodeUsedInDescriptionPerResource">
              <xs:selector xpath="mce:Description"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="ResourceType">
        <xs:sequence>
          <xs:element name="Name" type="mce:ResourceNameType" maxOccurs="unbounded"/>
          <xs:element name="Description" type="mce:DescriptionType" minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="idRef" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="ResourceNameType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="DescriptionType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
    </xs:schema>

## 자세한 내용

[데이터 손실 방지](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[자체 DLP 템플릿 및 정보 유형 정의](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

