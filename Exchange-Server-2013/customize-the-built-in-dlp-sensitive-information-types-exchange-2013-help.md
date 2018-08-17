---
title: '기본 제공 DLP 중요 한 정보 유형 사용자 지정: Exchange 2013 Help'
TOCTitle: 기본 제공 DLP 중요 한 정보 유형 사용자 지정
ms:assetid: 3f8bf141-2e7c-4ea7-b102-dfd6c41539da
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn781122(v=EXCHG.150)
ms:contentKeyID: 62757534
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 기본 제공 DLP 중요 한 정보 유형 사용자 지정

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-05-26_

전자 메일에 중요 한 정보를 찾고 때 *규칙*이라는 것에 해당 정보를 제공 해야 합니다. 데이터 손실 방지 (DLP) 바로 사용할 수 있는 가장 일반적인 중요 한 정보 형식에 대 한 51 규칙의 팩이 포함 됩니다. 이러한 규칙을 사용 하려면 정책에이 포함 해야 합니다. 조직의 특정 요구를 충족 하기 위해 이러한 기본 제공 규칙을 조정 하려면 하 고 있는 사용자 지정 중요 한 정보 유형 만들기 (영문) 하 여 수행할 수 있습니다를 찾을 수 있습니다. 이 항목에서는 광범위 한 잠재적 신용 카드 정보를 검색 하는 기존 규칙 컬렉션이 포함 된 XML 파일을 사용자 지정 하는 방법을 보여줍니다.

이 예제에서는 걸릴 수 있으며 다른 중요 한 정보를 기본 제공 형식에 적용할 수 있습니다. 기본 목록에 대 한 중요 한 정보 유형 및 XML 정의 [Exchange의 중요 한 정보 유형 찾아보십시오](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) 항목을 참조 합니다.

이 항목에서는 XML 규칙 사용자 지정 내용에 대 한 다음 섹션을 안내합니다.

  - 현재 규칙의 XML 내보내기

  - XML에서 수정할 규칙 찾기

  - XML을 수정 하 고 새 중요 한 정보 유형 만들기

  - 추가 증거 덜 필요

  - 조직에만 적용 되는 키워드를 찾습니다.

  - 규칙을 업로드 합니다.

규칙의 다양 한 부분은 사항에 대해 설명 하 고 기능 자신이 체크아웃이 항목의 끝에 용어 용어집 .

## 현재 규칙의 XML 파일 내보내기

Exchange 관리 셸 를 사용 하 여 필요한 XML를 내보내려면 또는 합니다. Exchange Server 2013[PowerShell을 사용 하 여 Exchange 2013 (Exchange 관리 셸)](https://technet.microsoft.com/ko-kr/library/bb123778\(v=exchg.150\))을 참조 하십시오. Exchange Online[원격 PowerShell을 사용하여 Exchange Online에 연결](https://technet.microsoft.com/ko-kr/library/jj984289\(v=exchg.150\))을 참조 하십시오.

1.  Exchange 관리 셸 또는 Exchange Online PowerShell에서 조직의 규칙 화면에 표시 하려면 **Get-classificationrulecollection** 입력 합니다. 기본, 기본 제공 규칙, "Microsoft 규칙 패키지." 라는 표시 됩니다 만들지 않은 경우 직접,

2.  조직의 규칙에서 저장을 입력 하 여 변수에 <strong>$ruleCollections Get-classificationrulecollection =</strong>합니다. 변수에 저장 하는 것을 사용 하면 원격 PowerShell 명령을 사용할 수 있는 형식으로 나중에 쉽게 사용할 수 있습니다.

3.  모든 데이터와 서식이 지정 된 XML 파일을 입력 하 여 확인 **집합-콘텐츠-경로 "C:\\custompath\\exportedRules.xml"-인코딩 바이트-$ruleCollections.SerializedClassificationRuleCollection 값이**. (**Set-content** XML 파일에 기록 cmdlet의 일부입니다.)
    

    > [!IMPORTANT]
    > 규칙 팩 실제로 저장 된 파일 위치를 사용 하 고 있는지 확인 합니다. <strong>C:\custompath\ </strong> 자리 표시자입니다.



## XML에서 수정할 규칙을 찾기

위의 cmdlet 내보낸 전체 *규칙 컬렉션*을 제공 하 여 51 기본 규칙을 포함 합니다. 그런 다음 신용 카드 번호 규칙을 수정 하려면을 구체적으로 찾이 필요 합니다.

1.  텍스트 편집기를 사용 하 여 이전 섹션에서 내보낸 XML 파일을 엽니다.

2.  DLP 규칙 포함 된 섹션의 시작 되는 **\<Rules\>** 태그까지 아래로 스크롤하십시오. (이 XML 파일의 전체 규칙 컬렉션에 대 한 정보를 포함 하므로 포함 된 규칙을 가져올 과거의 스크롤 하는 맨 위쪽에 다른 정보.)

3.  신용 카드 번호 규칙 정의를 찾을 **Func\_credit\_card** 찾습니다. (Xml에서 규칙 이름은 공백을 포함할 수 없습니다, 공백을 밑줄로, 일반적으로 대체 되 고 규칙 이름은 줄여서 경우도 있으므로 합니다. 이 예는 미국 주민등록 번호 규칙 "SSN입니다." 약어로 표시 되는 신용 카드 번호 규칙 XML 다음 코드 예제와 같습니다.
    
        <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085"
               patternsProximity="300" recommendedConfidence="85">
              <Pattern confidenceLevel="85">
               <IdMatch idRef="Func_credit_card" />
                <Any minMatches="1">
                  <Match idRef="Keyword_cc_verification" />
                  <Match idRef="Keyword_cc_name" />
                  <Match idRef="Func_expiration_date" />
                </Any>
              </Pattern>
            </Entity>

XML에서 신용 카드 번호 규칙 정의 찾은 했으므로 요구 사항에 맞게 규칙의 XML을 사용자 지정할 수 있습니다. (XML 정의에서 세부 정보를이 항목의 끝에 용어 용어집 참조).

## XML을 수정 하 고 새 중요 한 정보 형식 만들기

첫째, 만들어야 하는 새 중요 한 정보 유형 기본 규칙을 직접 수정할 수는 없습니다. [중요 한 정보 규칙 패키지 개발 (영문)](technical-description-of-xml-schema-for-dlp-rule-packages.md)에서 설명 하는 중요 한 정보를 사용자 지정 종류와 다양 한 작업을 수행할 수 있습니다. 이 예는 표시 됩니다 단순하게 유지 하 고만 확증 적 인증 거 제거한 신용 카드 번호 규칙에 키워드를 추가 합니다.

모든 XML 규칙 정의 다음과 같은 일반 서식 파일을 기반으로 합니다. 에 복사 / 붙여넣기 신용 카드 번호 정의 XML 서식 파일을 일부 값 (다음 예제에서는 "잡혀" 자리 표시자 확인)를 수정 및 하 다음 정책에서 사용할 수 있는 새 규칙으로 수정 된 XML을 업로드 합니다.

    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id=". . .">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id=". . ." /> 
        <Details defaultLangCode=". . .">
          <LocalizedDetails langcode=" . . . ">
             <PublisherName>. . .</PublisherName>
             <Name>. . .</Name>
             <Description>. . .</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
       <!-- Paste the Credit Card Number rule definition here.--> 
    
          <LocalizedStrings>
             <Resource idRef=". . .">
               <Name default="true" langcode=" . . . ">. . .</Name>
               <Description default="true" langcode=". . ."> . . .</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>

이제 해야 된 항목은 다음과 같은 XML와 비슷합니다. 규칙 패키지와 규칙은 해당 고유 Guid에 의해 식별 됩니다, 때문에 두 Guid를 생성 해야 합니다: 규칙 패키지 및 신용 카드 번호 규칙에 대 한 GUID를 교체할 수 하나에 대 한 하나입니다. (다음 코드 예제에서 엔터티 ID에 대 한 GUID는 새 대체할 필요가 있는 기본 제공 규칙 정의 대 한.) 다양 한 방법을 Guid를 생성할 수 있지만 PowerShell <strong>\[guid\]::NewGuid()</strong>을 입력 하 여 쉽게 수행할 수 있습니다.

    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id="8aac8390-e99f-4487-8d16-7f0cdee8defc">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id="8d34806e-cd65-4178-ba0e-5d7d712e5b66" />
        <Details defaultLangCode="en">
          <LocalizedDetails langcode="en">
            <PublisherName>Contoso Ltd.</PublisherName>
            <Name>Financial Information</Name>
            <Description>Modified versions of the Microsoft rule package</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f"
           patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    
          <LocalizedStrings>
             <Resource idRef="db80b3da-0056-436e-b0ca-1f4cf7080d1f"> 
    <!-- This is the GUID for the preceding Credit Card Number entity because the following text is for that Entity. -->
               <Name default="true" langcode="en-us">Modified Credit Card Number</Name>
               <Description default="true" langcode="en-us">Credit Card Number that looks for additional keywords, and another version of Credit Card Number that doesn't require keywords (but has a lower confidence level)</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>

## 중요 한 정보 형식에서 확증 적 인증 거 요구 사항을 제거합니다

이제 Exchange 환경에 업로드할 수 있도록 하 고 있는 새 중요 한 정보 유형을 했으므로 다음 단계를 규칙을 보다 구체적인 만드는 것입니다. 만 체크섬을 전달 하지만 추가 (확증) 증거 (예: 키워드)를 필요로 하지 않습니다 16 자리 숫자를 찾고 규칙을 수정 합니다. 이 작업을 수행 확증 적 인증 거 찾는 XML의 일부를 제거 해야 합니다. 확증 적 인증 거 있기 때문에 일반적으로 특정 키워드 또는 신용 카드 번호 근처 만료 날짜 가양성을 줄일 수 있는 매우 유용 합니다. 해당 증거를 제거 하는 경우 낮춰 **confidenceLevel**,이 예제의 85은 신용 카드 번호를 발견 하는 방법을 판단는 조정 해야 합니다.

    <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="300"
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
          </Pattern>
        </Entity>

## 조직에만 적용 되는 키워드를 찾습니다.

확증 적 인증 거 필요 하지만 다른 또는 추가 키워드를 원하는 해야할 수 및 해당 증거를 검색할 위치를 변경할 수도 있습니다. 확장 하거나 축소 창 확증 적 인증 거 16 자리 숫자가 주위에 **patternsProximity** 를 조정할 수 있습니다. 직접 키워드를 추가 하려면 키워드 목록을 정의 하 고 규칙 내에서 참조 해야 합니다. 다음 XML 키워드 "회사 카드" 및 "Contoso 카드"를 추가 하 고 신용 카드 번호의 150 자 내에서 이러한 구가 포함 된 메시지 신용 카드 번호로 식별 됩니다.

    <Rules>
    <! -- Modify the patternsProximity to be "150" rather than "300." -->
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="150" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
    <!-- Add the following XML, which references the keywords at the end of the XML sample. -->
              <Match idRef="My_Additional_Keywords" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    <!-- Add the following XML, and update the information inside the <Term> tags with the keywords that you want to detect. -->
        <Keyword id="My_Additional_Keywords">
          <Group matchStyle="word">
            <Term caseSensitive="false">company card</Term>
            <Term caseSensitive="false">Contoso card</Term>
          </Group>
        </Keyword>

## 규칙을 업로드 합니다.

규칙을 업로드 하려면 다음을 수행 해야 합니다.

1.  유니코드 인코딩을 사용 하 여.xml 파일을 저장 합니다. 이 서로 다른 인코딩을 사용 하 여 파일을 저장 하는 경우 규칙이 작동 하지 않음 중요 합니다.

2.  Exchange 관리 셸 또는 Exchange Online PowerShell에 연결 합니다. Exchange Server 2013[PowerShell을 사용 하 여 Exchange 2013 (Exchange 관리 셸)](https://technet.microsoft.com/ko-kr/library/bb123778\(v=exchg.150\))를 참조 하십시오. Exchange Online[원격 PowerShell을 사용하여 Exchange Online에 연결](https://technet.microsoft.com/ko-kr/library/jj984289\(v=exchg.150\))를 참조 하십시오.

3.  Exchange 관리 셸 또는 Exchange Online PowerShell 입력 **New-classificationrulecollection FileData (Get-content-경로 "C:\\custompath\\MyNewRulePack.xml"-인코딩 바이트)**.
    

    > [!IMPORTANT]
    > 규칙 팩 실제로 저장 된 파일 위치를 사용 하 고 있는지 확인 합니다. <STRONG>C:\custompath\</STRONG> 자리 표시자입니다.



4.  를 확인 하기 위해 **Y** 를 입력 하 고 **Enter** 키를 누릅니다.

5.  **Get 자세한**는 이제 표시 하 여 규칙의 이름을 입력 하 여 새 규칙에 업로드 한 있는지 확인 하십시오.

중요 한 정보를 검색 하는 새 규칙을 사용 하 여를 시작 하려면 DLP 정책 규칙을 추가 해야 합니다. 정책에 규칙을 추가 하는 방법을 알아보려면 [DLP 정책 관리](manage-dlp-policies-exchange-2013-help.md)를 참조 하십시오.

## 용어 용어집

이 절차는 동안 발생 한 용어에 대 한 정의.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>용어</th>
<th>정의</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Entity</p></td>
<td><p>엔터티는 신용 카드 번호와 같은 중요 한 정보 유형, 호출 기능입니다. 각 엔터티에 ID와 고유 GUID는 XML에 GUID 및 그에 대 한 검색을 복사 하는 경우 XML 규칙 정의 하 고 해당 XML 규칙의 지역화 된 모든 번역을 찾을 수 있습니다. 변환에 대 한 GUID를 검색 하 고 해당 GUID를 검색 하 여이 정의 찾을 수도 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>함수</p></td>
<td><p>XML 파일 컴파일된 코드에서 함수를은 <strong>Func_credit_card</strong>참조 합니다. 함수는 복잡 한 regex를 실행 하 고 기본 제공 된 규칙에 대 한 체크섬과 일치 하는지 확인 하는데 사용 됩니다.) 코드에서 이런 때문에 XML 파일에 나타나지 변수 중 일부는 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p>IdMatch</p></td>
<td><p>패턴과 일치 하는 동안에 식별자-예: 신용 카드 번호입니다. <a href="technical-description-of-xml-schema-for-dlp-rule-packages.md">엔터티 규칙</a>에서 <strong>Match</strong> 태그 및이 대 한 자세한를 읽을 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>키워드 목록</p></td>
<td><p>XML 파일 목록이 있는 우리는 일치 항목을 찾습니다 <strong>patternsProximity</strong> 내에서 엔터티에 대 한 키워드는 <strong>keyword_cc_verification</strong> 및 <strong>keyword_cc_name</strong>도 참조 합니다. 이러한 XML에 현재 표시 되지 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p>패턴</p></td>
<td><p>패턴에 대 한 자세한 내용은 중요 한 형식 목록이 들어 있습니다. 키워드, regex, 내부 (수행 하는 함수와 체크섬을 확인 하는 등의 작업)이 포함 됩니다. 중요 한 정보 유형 고유 confidences 있는 여러 패턴을 가질 수 있습니다. 발견 되는 거의 없거나 전혀 없는 확증 적 인증 거는 경우 확증 적 인증 거 발견 되는 경우 높은 정확도 및 낮은 신뢰를 반환 하는 중요 한 정보 형식을 만들 때 유용 합니다.</p></td>
</tr>
<tr class="even">
<td><p>패턴 confidenceLevel</p></td>
<td><p>DLP 엔진 일치 하는 항목이 발견 하는 신뢰 수준을입니다. 패턴의 요구 사항이 충족 하는 경우이 수준의 신뢰 패턴에 대 한 일치 하는와 연결 됩니다. 경우 (ETRs) 규칙 Exchange 전송 사용을 고려해 야 신뢰 측정값입니다.</p></td>
</tr>
<tr class="odd">
<td><p>patternsProximity</p></td>
<td><p>신용 카드 번호 패턴의 모습을 찾을 때 <strong>patternsProximity</strong> 는 번호를 중심으로 근접 확증 적 인증 거에 살펴볼입니다.</p></td>
</tr>
<tr class="even">
<td><p>recommendedConfidence</p></td>
<td><p>이 규칙에 대 한 것이 좋습니다 신뢰 수준입니다. 권장된 신뢰 엔터티 및 선호도에 적용 됩니다. 엔터티,이 번호는 패턴에 대 한 <strong>confidenceLevel</strong> 에 대해 평가 되지 않습니다. 것이 단순히 추천 단어를 하나를 적용 하려는 경우에 신뢰도 선택할 수 있도록 지원 합니다. 선호도에 대 한 패턴의 <strong>confidenceLevel</strong> 를 호출할 수는 ETR 동작에 대 한 <strong>recommendedConfidence</strong> 번호 보다 길어야 합니다. <strong>recommendedConfidence</strong> 기본 신뢰 수준을 ETRs에서 사용 되는 작업을 호출 하는 경우 원할 경우 수동으로 변경할 수 있습니다를 호출할 수 ETR을 기반으로 패턴의 신뢰 수준 대신 합니다.</p></td>
</tr>
</tbody>
</table>


## 자세한 내용

  - [메시지를 평가 DLP 규칙을 적용 하는 방법](how-dlp-rules-are-applied-to-evaluate-messages-exchange-2013-help.md)

  - [사용자 지정 DLP 정책 만들기](create-a-custom-dlp-policy-exchange-2013-help.md)

  - [Exchange의 중요 한 정보 유형 찾아보십시오](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

