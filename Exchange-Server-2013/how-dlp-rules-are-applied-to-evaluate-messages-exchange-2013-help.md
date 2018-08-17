---
title: '메시지를 평가 DLP 규칙을 적용 하는 방법: Exchange 2013 Help'
TOCTitle: 메시지를 평가 DLP 규칙을 적용 하는 방법
ms:assetid: 1ac77020-26ff-410c-ab09-4f28a99d67a1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn329050(v=EXCHG.150)
ms:contentKeyID: 56270201
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지를 평가 DLP 규칙을 적용 하는 방법

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange DLP(데이터 손실 방지) 정책 내에 중요한 정보 규칙을 설정하여 이메일 메시지에서 매우 구체적인 데이터를 검색할 수 있습니다. 이 항목은 이러한 규칙의 적용 방법과 메시지의 평가 방법을 이해하는 데 도움이 됩니다. 규칙이 적용되는 방법을 알면 DLP 검색 정확성을 높일 수 있을 뿐만 아니라 이메일 사용자에 대한 워크플로 중단을 방지할 수 있습니다. Microsoft에서 제공한 신용 카드 정보 규칙을 예로 사용합니다. 전송 규칙 또는 DLP 정책을 활성화하면 Exchange 전송 규칙 에이전트가 사용자가 보내는 모든 메시지를 만든 규칙 집합과 비교합니다.

## 요구의 정확한 파악

메시지의 신용 카드 정보에 대한 작업을 수행해야 한다고 가정합니다. 수행해야 하는 작업이 이 항목의 주제가 아니더라도 [Exchange Online 흐름 규칙 동작을 메일](https://technet.microsoft.com/ko-kr/library/jj919237\(v=exchg.150\))에서 해당 내용을 자세히 알아볼 수 있습니다. 가능한 한 최대한 확실하게, 메시지에서 검색되는 내용이 진짜 신용 카드 데이터이고, 단순히 신용 카드 데이터와 유사한 숫자 그룹(예: 예약 코드 또는 차량 식별 번호)을 적당히 사용한 것일 수 있는 그 외 데이터가 아님을 확인해야 합니다. 이 요구를 충족하기 위해 다음 정보가 신용 카드로 확실히 분류되어야 합니다.

**    Margie’s Travel 귀하,  
    Spencer씨의 업데이트된 신용 카드 정보를 받았습니다.  
    Spencer Badillo  
    Visa: 4111 1111 1111 1111  
    만료 날짜: 2/2012  
    Spencer씨의 여행 프로필을 업데이트해 주시기 바랍니다.**

또한 다음 정보가 신용 카드로 확실히 분류되지 않도록 해야합니다.

**    안녕 Alex,  
    나도 하와이에 갈 거야. 내 예약 코드는 1234 1234 1234 1234이고 3/2012에 하와이에 갈 거야.  
    그럼 안녕, Lisa**

다음 XML 조각은 Exchange와 함께 제공되며 제공된 DLP 정책 템플릿 중 하나에 포함되어 있는 것으로, 앞에서 설명한 요구가 현재 중요한 정보 규칙에 어떻게 정의되어 있는지를 보여 줍니다.

    <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>

## 솔루션의 패턴 일치

앞에 표시된 XML 규칙 정의에는 규칙이 중요한 정보만 검색하고 모호한 관련 정보는 검색하지 않는 확률을 향상시키는 패턴 일치가 포함되어 있습니다. DLP 규칙 및 템플릿의 XML 스키마에 대한 자세한 내용은 [자체 DLP 템플릿 및 정보 유형 정의](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)를 참조하세요.

신용 카드 규칙에는 패턴에 대한 XML 코드 섹션이 있는데 여기에는 기본 식별자 일치 및 몇 가지 확증적인 추가 증거가 포함되어 있습니다. 여기에 이러한 세 가지 요구 사항이 모두 설명되어 있습니다.

1.  `<IdMatch idRef="Func_credit_card" />  ` — 내부적으로 정의된 credit card라는 이름의 함수 일치가 필요합니다. 이 함수에는 포함된 몇 가지 유효성 검사는 다음과 같습니다.
    
    1.  정규식(이 예에서는 16자리)을 일치시키는데, 이러한 정규식은 **4111 1111 1111 1111**도 일치시키도록 공백 구분 기호와 같은 변형이나 **4111-1111-1111-1111**도 일치시키도록 하이픈 구분 기호와 같은 변형을 포함할 수도 있습니다.
    
    2.  이 16자리 숫자가 신용 카드 번호일 확률을 높이기 위해 이 숫자에 대해 Lhun의 체크섬 알고리즘을 평가합니다.
    
    3.  필수 일치가 필요하며, 이후 확증적인 증거가 평가됩니다.

2.  `<Any minMatches="1">  ` — 이 섹션은 증거의 다음 항목 중 하나 이상이 있어야 함을 나타냅니다.

3.  확증적인 증거는 다음 세 가지 중 한 개의 일치일 수 있습니다.
    
    `<Match idRef="Keyword_cc_verification" />`
    
    `<Match idRef="Keyword_cc_name" />`
    
    `<Match idRef="Func_expiration_date" />`
    
    이러한 세 가지는 신용 카드에 대한 키워드 목록, 신용 카드의 이름 또는 만료 날짜가 필요함을 의미할 뿐입니다. 만료 날짜는 내부적으로 다른 함수로 정의 및 평가됩니다.

## 규칙에 대한 콘텐츠 평가 프로세스

이 5단계는 Exchange가 이메일 메시지와 규칙을 비교하기 위해 수행하는 작업을 나타냅니다. 여기서 사용하는 신용 카드 규칙 예에서는 다음 단계가 수행됩니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>단계</th>
<th>작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1. 콘텐츠 얻기</p></td>
<td><p>Spencer Badillo</p>
<p>Visa: 4111 1111 1111 1111</p>
<p>만료 날짜: 2/2012</p></td>
</tr>
<tr class="even">
<td><p>2. 정규식 분석</p></td>
<td><p>4111 1111 1111 1111 -&gt; 16자리 숫자가 검색됨</p></td>
</tr>
<tr class="odd">
<td><p>3. 함수 분석</p></td>
<td><ul>
<li><p>4111 1111 1111 1111 -&gt; 체크섬과 일치</p></li>
<li><p>1234 1234 1234 1234 -&gt; 일치하지 않음</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>4. 추가 증거</p></td>
<td><ol>
<li><p>키워드 Visa가 해당 숫자에 가까움</p></li>
<li><p>날짜(2012년 2월)에 대한 정규식이 해당 숫자에 가까움</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>5. 결과</p></td>
<td><ol>
<li><p>체크섬과 일치하는 정규식이 있음</p></li>
<li><p>추가 증거로 신뢰 수준 증가</p></li>
</ol>
<p></p></td>
</tr>
</tbody>
</table>


Microsoft에서 이 규칙을 설정한 방식에서는 규칙과 일치하기 위해서는 키워드와 같은 확증적인 증거가 반드시 이메일 메시지 콘텐츠의 일부여야 한다고 규정합니다. 따라서 다음 이메일 콘텐츠는 신용 카드를 포함한 것으로 검색되지 않습니다.

**    Margie’s Travel 귀하,  
    Spencer의 업데이트된 정보를 받았습니다.  
    Spencer Badillo  
    4111 1111 1111 1111  
    Spencer씨의 여행 프로필을 업데이트해 주시기 바랍니다.**

다음 예에 표시된 대로 추가 증거 없이 패턴을 정의하는 사용자 지정 규칙을 사용할 수 있습니다. 이 규칙에서는 신용 카드 번호만 있고 확증적인 증거가 없는 메시지를 검색합니다.

``` 
      <Pattern confidenceLevel="85">
         <IdMatch idRef="Func_credit_card" />
      </Pattern>
    </Entity>
```

이 문서의 신용 카드 예를 다른 중요한 정보 규칙으로도 확장할 수 있습니다. Exchange에서 Microsoft가 제공한 규칙의 전체 목록을 보려면 다음 방법으로 Exchange 관리 셸에서 [Get-ClassificationRuleCollection](https://technet.microsoft.com/ko-kr/library/jj218696\(v=exchg.150\)) cmdlet을 사용하세요.

```
$rule_collection = Get-ClassificationRuleCollection
```

```
$rule_collection[0].SerializedClassificationRuleCollection | Set-Content oob_classifications.xml -Encoding byte
```

## 자세한 내용

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\))

[PowerShell을 사용 하 여 Exchange 2013 (Exchange 관리 셸)](https://technet.microsoft.com/ko-kr/library/bb123778\(v=exchg.150\))

[Exchange Online PowerShell](https://technet.microsoft.com/ko-kr/library/jj200677\(v=exchg.150\))

