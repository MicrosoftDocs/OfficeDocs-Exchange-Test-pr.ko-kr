---
title: '일치 하는 방법 및 규칙 패키지에 대 한 기술: Exchange 2013 Help'
TOCTitle: 일치 하는 방법 및 규칙 패키지에 대 한 기술
ms:assetid: 09fe9278-d077-452c-b7e5-729b3dc70b1b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ674702(v=EXCHG.150)
ms:contentKeyID: 50482474
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 일치 하는 방법 및 규칙 패키지에 대 한 기술

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-07-28_

이 항목에서는 사용자 자신의 사용자 지정 중요한 정보 유형 규칙 패키지를 포함하도록 설계된 DLP(데이터 손실 방지) XML 파일 내의 Pattern 및 Evidence 요소 일치 방법에 대해 설명합니다. 올바른 형식의 XML 파일을 만든 후 EAC(Exchange 관리 센터)나 Exchange 관리 셸을 사용하여 파일을 가져오면 Microsoft Exchange Server 2013 DLP 솔루션을 만드는 데 도움이 될 수 있습니다. 여기에 설명된 일치 방법을 사용하려면 먼저 DLP XML 파일이 이미 시작된 상태여야 합니다. 사용자 자신의 DLP 템플릿 및 XML 파일 정의에 대한 자세한 내용은 [자체 DLP 템플릿 및 정보 유형 정의](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)를 참조하십시오.

## Match 요소

`Match` 요소는 `Pattern` 및 `Evidence` 요소 내에서 일치시킬 기본 키워드, regex 또는 함수를 나타내는 데 사용됩니다. 일치 자체에 대한 정의는 `Rule` 요소 외부에 저장되고 `idRef` 필수 특성을 통해 참조됩니다. 여러 `Match` 요소가 일치 의미 체계를 정의하기 위해 `Pattern` 요소에 직접 포함되거나 `Any` 요소를 사용하여 결합될 수 있는 Pattern 정의에 포함될 수 있습니다.

    <?xml version="1.0" encoding="utf-8"?>
    <Rules packageId="...">
            ...
    <Entity id="...">
      <Pattern confidenceLevel="85">
                 <IdMatch idRef="FormattedSSN" />
                 <Match idRef="USDate" />
                 <Match idRef="USAddress" />
      </Pattern>
    </Entity>
            ...
             <Keyword id="FormattedSSN "> ... </Keyword>
             <Regex id=" USDate "> ... </Regex>
             <Regex id="USAddress"> ... </Regex>
            ...
    
    </Rules>

## 키워드 기반 일치 정의

일반적인 규칙 요구 사항은 잘 알려진 키워드 문자열 식을 기반으로 일치시키는 것입니다. 이 작업은 `Keyword` 요소를 사용하여 수행됩니다. Keyword 요소에는 해당 Entity 또는 Affinity 규칙에서 참조로 사용되는 "id" 특성이 있습니다. 여러 Entity 및 Affinity 규칙에서 단일 Keyword 요소를 참조할 수 있습니다.

일치 하는 정확 하 게 일치 하는 값 또는 word 기반 일치 하는 알고리즘을 사용 하 여 수행할 수 있습니다. 지정 된 언어로 텍스트를 검색 하는 대/소문자 구분 알고리즘을 사용 하는 정확 하 게 일치 합니다. 단어 경계를 기초로 일치 하는 알고리즘을 적용 하는 일치 하는 항목. 일치 시킬 용어 용어 하위 요소를 사용 하 여 키워드 정의에서 인라인에 포함된 될 수 있습니다.


> [!TIP]
> 효율성 및 성능을 높이려면 regex보다는 상수 기반 일치 스타일을 사용하십시오. regex 일치는 상수 기반 일치로 충분하지 않으며 정규식의 유연성이 필요한 경우에만 사용하십시오.



    <Keyword id="Word_Example">
        <Group matchStyle="word">
           <Term>card verification</Term>
           <Term>cvn</Term>
           <Term>cid</Term>
           <Term>cvc2</Term>
           <Term>cvv2</Term>
           <Term>pin block</Term>
           <Term>security code</Term>
        </Group>
    </Keyword>
    ...
    <Keyword id="String_Example">
        <Group matchStyle="string">
           <Term>card</Term>
           <Term>pin</Term>
           <Term>security</Term>
        </Group>
    </Keyword>

## 정규식 기반 일치 정의

또 다른 일반적인 일치 방법은 정규식을 기반으로 합니다. 정규식 일치의 유연성으로 인해 이 방법은 운전 면허 번호, 주소 등의 데이터에 대한 일치를 구현할 때 일반적으로 선택됩니다. 일반적인 정규식 구문이 regex 패턴을 정의하는 데 사용됩니다. 다음 표는 가장 일반적으로 사용할 수 있는 정규식 토큰의 몇 가지 예를 보여줍니다.


> [!TIP]
> 효율성 및 성능을 높이려면 regex보다는 상수 기반 일치 스타일을 사용하십시오. regex 일치는 상수 기반 일치로 충분하지 않으며 정규식의 유연성이 필요한 경우에만 사용하십시오.




<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기호</th>
<th>의미</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>c</p></td>
<td><p>특수 문자 중 하나가 아닌 경우 리터럴 문자 c를 한 번 일치시킵니다.</p></td>
</tr>
<tr class="even">
<td><p>^</p></td>
<td><p>줄의 시작 부분을 일치시킵니다.</p></td>
</tr>
<tr class="odd">
<td><p>.</p></td>
<td><p>줄 바꿈 문자가 아닌 모든 문자를 일치시킵니다.</p></td>
</tr>
<tr class="even">
<td><p>$</p></td>
<td><p>줄의 끝 부분을 일치시킵니다.</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>식 사이의 논리적 OR입니다.</p></td>
</tr>
<tr class="even">
<td><p>()</p></td>
<td><p>하위 식을 그룹화합니다.</p></td>
</tr>
<tr class="odd">
<td><p>[]</p></td>
<td><p>문자 클래스를 정의합니다.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>앞의 식을 0회 이상 일치시킵니다.</p></td>
</tr>
<tr class="odd">
<td><p>+</p></td>
<td><p>앞의 식을 1회 이상 일치시킵니다.</p></td>
</tr>
<tr class="even">
<td><p>?</p></td>
<td><p>앞의 식을 0회 또는 1회 일치시킵니다.</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n</em>}</p></td>
<td><p>앞의 식을 <em>n</em>회 일치시킵니다.</p></td>
</tr>
<tr class="even">
<td><p>{<em>n,</em>}</p></td>
<td><p>앞의 식을 <em>n</em>회 이상 일치시킵니다.</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n, m</em>}</p></td>
<td><p>앞의 식을 <em>n</em>~<em>m</em>회 일치시킵니다.</p></td>
</tr>
<tr class="even">
<td><p>\d</p></td>
<td><p>숫자를 일치시킵니다.</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>숫자가 아닌 문자를 일치시킵니다.</p></td>
</tr>
<tr class="even">
<td><p>\w</p></td>
<td><p>밑줄을 포함하여 영문자를 일치시킵니다.</p></td>
</tr>
<tr class="odd">
<td><p>\W</p></td>
<td><p>영문자가 아닌 문자를 일치시킵니다.</p></td>
</tr>
<tr class="even">
<td><p>\s</p></td>
<td><p>공백 문자(\t, \n, \r 또는 \f)를 일치시킵니다.</p></td>
</tr>
<tr class="odd">
<td><p>\S</p></td>
<td><p>공백이 아닌 문자를 일치시킵니다.</p></td>
</tr>
<tr class="even">
<td><p>\t</p></td>
<td><p>탭입니다.</p></td>
</tr>
<tr class="odd">
<td><p>\n</p></td>
<td><p>줄 바꿈입니다.</p></td>
</tr>
<tr class="even">
<td><p>\r</p></td>
<td><p>캐리지 리턴입니다.</p></td>
</tr>
<tr class="odd">
<td><p>\f</p></td>
<td><p>FF(Form Feed)입니다.</p></td>
</tr>
<tr class="even">
<td><p>\<em>m</em></p></td>
<td><p><em>m</em>을 이스케이프합니다. 여기서 <em>m</em>은 위에 설명된 메타 문자 중 하나(^, ., $, |, (), [], *, +, ?, \, 또는 /)입니다.</p></td>
</tr>
</tbody>
</table>


Regex 요소에는 해당 Entity 또는 Affinity 규칙에서 참조로 사용되는 "id" 특성이 있습니다. 여러 Entity 및 Affinity 규칙에서 단일 Regex 요소를 참조할 수 있습니다. Regex 식은 Regex 요소의 값으로 정의됩니다.

    <Regex id="CCRegex">
         \bcc\#\s|\bcc\#\:\s
    </Regex>
    ...
    <Regex id="ItinFormatted">
        (?:^|[\s\,\:])(?:9\d{2})[- ](?:[78]\d[-  
         ]\d{4})(?:$|[\s\,]|\.\s)
    </Regex>
    ...
    <Regex id="NorthCarolinaDriversLicenseNumber">
        (^|\s|\:)(\d{1,8})($|\s|\.\s)
    </Regex>

## 여러 Match 요소 결합

일반적인 일치 신뢰도 향상 방법은 일치 항목이 하나 이상 발생해야 한다는 등의 의미 체계를 여러 Match 요소 간에 정의하는 것입니다. Any 요소를 사용하면 여러 일치 항목 간에 기반이 되는 논리를 정의할 수 있습니다. Any 요소를 Pattern 요소의 하위 요소로 사용할 수 있습니다. 이 요소는 Match 하위 요소를 하나 이상 포함하며 해당 Match 하위 요소 간의 일치 논리를 정의합니다. 논리가 "아닌" 모든 일치 항목 및 정확히 일치하는 항목 개수가 있는 Any 요소에 대한 XML 코드 예는 아래를 참조하십시오.

선택적 특성인 minMatches(기본값 = 1)를 사용하여 성공적으로 일치시키기 위해 충족해야 하는 최소 Match 요소 수를 정의할 수 있습니다. 마찬가지로 선택적 특성인 maxMatches(기본값 = 하위 Match 요소 수)를 사용하여 성공적으로 일치시키기 위해 충족해야 하는 최대 Match 요소 수를 정의할 수 있습니다. 이러한 조건은 minMatches 및 maxMatches 특성 사용을 기반으로 논리 연산자를 통해 결합되어 다음 의미 체계를 허용합니다.

  - 모든 하위 Match 요소 일치
    
    하위 Match 요소 일치 안 함
    
    하위 Match 요소의 정확한 하위 집합 일치

<!-- end list -->

    <Any minMatches="3" maxMatches="3">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any maxMatches="0">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any minMatches="1" maxMatches="1">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

## 더 많은 증거로 신뢰 수준 향상

엔터티 기반 규칙의 경우 또 다른 신뢰도 향상 옵션은 확증적인 증거 수를 각각 늘리면서 Pattern 요소를 여러 개 정의하는 것입니다. 이 작업은 Any 요소에 minMatches와 maxMatches를 사용하여 늘어나는 확증적인 증거 수를 기반으로 신뢰 수준을 향상시키는 독립 패턴을 만드는 방법으로 수행됩니다. 예를 들면 다음과 같습니다.

  - 확증적인 증거 한 조각이 발견된 경우: 신뢰 수준 65%

  - 두 조각이 발견된 경우: 신뢰 수준 75%

  - 세 조각이 발견된 경우: 신뢰 수준 85%

<!-- end list -->

    <Entity id="..." patternsProximity="300" >
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Any maxMatches="1">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="75">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="2" maxMatches="2">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="85">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="3">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity>

## 예: 미국 사회 보장 규칙

이 섹션에서는 미국 사회 보장 번호를 일치시키는 규칙을 작성하기 위한 소개 정보를 제공합니다. 먼저 사회 보장 번호가 포함된 콘텐츠를 식별하는 방법에 대한 설명으로 시작하겠습니다. 사회 보장 번호는 다음과 같은 경우에 발견됩니다.

1.  Regex가 서식이 지정된 SSN과 일치하고 유효한 SSN 범위에 속하는 경우

2.  확증적인 증거   다음 중 하나가 근처에서 발생해야 합니다.
    
    1.  키워드 일치 {Social Security, Soc Sec, SSN, SSNS, SSN\#, SS\#, SSID}
    
    2.  미국 주소를 나타내는 텍스트
    
    3.  날짜를 나타내는 텍스트
    
    4.  이름을 나타내는 텍스트

그런 다음 설명을 규칙 스키마 표현으로 변환합니다.

    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77"
             patternsProximity="300" RecommendedConfidence="85">
        <Pattern confidenceLevel="85">
          <IdMatch idRef="FormattedSSN" />
          <Any minMatches="1">
              <Match idRef="SSNKeywords" />
              <Match idRef="USDate" />
              <Match idRef="USAddress" />
              <Match idRef="Name" />
          </Any>
        </Pattern>
    </Entity>

## 자세한 내용

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[자체 DLP 템플릿 및 정보 유형 정의](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

