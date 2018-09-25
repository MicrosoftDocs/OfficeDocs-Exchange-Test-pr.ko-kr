---
title: 'DLP 정책 템플릿 파일 개발: Exchange 2013 Help'
TOCTitle: DLP 정책 템플릿 파일 개발
ms:assetid: 4b263547-aef4-4ee8-aa4f-fa64a5863189
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ674703(v=EXCHG.150)
ms:contentKeyID: 50483051
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DLP 정책 템플릿 파일 개발

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

이 개요 문서에서는 DLP(데이터 손실 방지) 정책 템플릿 파일에 대한 XML 스키마 정의의 구성 요소에 대해 설명하고 XML 형식의 정책 파일 예를 제공합니다. 이 문서는 시작하기 전에 전반적인 DLP 아키텍처와 규칙 개발 프로세스를 이해하는 데 도움이 됩니다. 자세한 내용은 [데이터 손실 방지](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention) 및 [자체 DLP 템플릿 및 정보 유형 정의](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md) 항목을 참조하십시오.

데이터 손실 방지 솔루션을 쉽게 적용하고 관리할 수 있도록 Microsoft Exchange Server 2013에는 DLP 정책이라고 하는 개념 모델과 정책 템플릿이 도입되었습니다. DLP 정책 템플릿은 의도한 DLP 정책에 대한 예비 디자인을 제공합니다. DLP 정책 템플릿이 유용한 템플릿이 되기 위해서는 규정이나 비즈니스 요구 사항과 같은 구체적인 정책 목표를 충족하는 데 필요한 모든 지시문과 데이터 개체를 포함해야 합니다. DLP 정책 템플릿은 환경에 따라 달라지지 않습니다. DLP 정책 템플릿은 단순히 정책에 대한 정의 또는 모델이며 제품 구성의 일부로 제공하거나 독립 소프트웨어 공급업체 또는 파트너가 공급할 수 있습니다. 반면 DLP 정책은 템플릿이 런타임에 인스턴스화된 것으로, 배포 환경마다 고유합니다. 전송 규칙을 사용하여 기존 메시징 정책 프레임워크에 다양한 DLP 정책을 통합할 수 있습니다. 전송 규칙은 DLP 솔루션의 다양한 기능을 적용하고 표현하는 데 부족함이 없을 만큼 유연합니다.

## 정책 템플릿 원본 및 구조

DLP 정책 템플릿은 일반적으로 다음 그림에 나오는 서버 기반 처리 지시문, 클라이언트 컴퓨터 정책 또는 기타 정책 구문과 같은 여러 원본으로부터 영향을 받습니다.

![정책 템플릿에 영향을 주는 요인](images/JJ674703.12f48e4f-d7b8-4ddd-87e8-8477983252ec(EXCHG.150).gif "정책 템플릿에 영향을 주는 요인")

가져오기, 내보내기, 삭제 및 쿼리 기능이 있는 Exchange 관리 센터 등의 인터넷 기반 인터페이스와 Exchange 관리 셸 모두를 통해 DLP 정책 템플릿에 대한 단순한 관리 작업을 수행할 수 있습니다. DLP 정책은 생성 과정에서 DLP 정책 템플릿을 참조하여 만들어집니다. 참조되는 DLP 정책 템플릿은 시스템에 설치되고 Active Directory 도메인 서비스에 저장된 정책 템플릿에 대한 참조이거나 외부에서 제공한 정책에서 직접 입력으로 제공될 수 있습니다.

DLP 정책 템플릿은 XML 문서로 표현됩니다. Exchange 내에 제공된 정책과 외부에서 제공된 정책에는 모두 단일 XML 스키마가 사용됩니다. XML 문서의 개념 구조와 주요 요소는 아래 표에 나와 있습니다. 정책 구성 요소 정의 집합을 통해 규정 또는 비즈니스 요구 사항과 같은 구체적인 정책 목표를 쉽게 달성할 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>구조 요소</th>
<th>의미 또는 예</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>게시자</p></td>
<td><p>Microsoft 또는 파트너</p></td>
</tr>
<tr class="even">
<td><p>버전</p></td>
<td><p>15.0.1.0</p></td>
</tr>
<tr class="odd">
<td><p>정책 이름</p></td>
<td><p>PCI-DSS</p></td>
</tr>
<tr class="even">
<td><p>설명</p></td>
<td><p>PCI-DSS DLP 정책 PCI 데이터 보안 표준 (PCI DSS)에 따라 달라 집니다 정보의 신용 카드 또는 직불 카드 번호 등의 정보를 포함 하 여 현재 상태를 검색할 수 있습니다. 이 정책 사용 하 여 모든 규정 준수를 보장 하지 않습니다. 테스트가 완료 되 면 필요한 구성을 변경 Exchange 조직의 정책 준수 정보를 전송 하도록 합니다. 알려진된 비즈니스 파트너와 TLS를 구성 하거나이 유형의 데이터를 포함 하는 메시지에 권한 보호를 추가 하는 등 보다 제한적인 전송 규칙 동작 추가 (영문)을 예로 들 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>메타데이터</p></td>
<td><p>국가별 규정, 국가 또는 지역, 키워드 등을 설명하는 태그</p></td>
</tr>
<tr class="even">
<td><p>정책 구문 집합</p></td>
<td><ol>
<li><p>조건 및 작업 같은 전송 규칙 정의</p></li>
<li><p>대화형 알림을 통해 클라이언트 환경을 제어하는 전자 메일 클라이언트 동작 정의</p></li>
<li><p>필요한 경우, 클라이언트 환경 관련 설정과 통합되어야 하는 구성 참조</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>데이터 분류 집합</p></td>
<td><ol>
<li><p>분류 엔터티 또는 선호도를 지정합니다.</p></li>
<li><p>엔터티는 횟수와 신뢰도를 포함하고 선호도는 신뢰도만 포함합니다.</p></li>
<li><p>자체 속성 집합과 분류 스키마를 함께 제공합니다.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## 정책 템플릿 형식 정의

DLP 정책 템플릿은 다음 스키마를 따르는 XML 문서로 표현됩니다. XML은 대/소문자를 구분합니다. 예를 들어 `dlpPolicyTemplates`는 작동하지만 `DlpPolicyTemplates`는 작동하지 않습니다.

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <dlpPolicyTemplates>
    <dlpPolicyTemplate id="F7C29AEC-A52D-4502-9670-141424A83FAB" mode="Audit" state="Enabled" version="15.0.2.0">
      <contentVersion>4</contentVersion>
      <publisherName>Microsoft</publisherName>
      <name>
        <localizedString lang="en">PCI-DSS</localizedString>
      </name>
      <description>
        <localizedString lang="en">Detects the presence of information subject to Payment Card Industry Data Security Standard (PCI-DSS) compliance requirements.</localizedString>
      </description>
      <keywords></keywords>
      <ruleParameters></ruleParameters>
      <ruleParameters/>
      <policyCommands>
        <!-- The contents below are applied/executed as rules directly in PS - -->
        <commandBlock>
          <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP Policy."]]>
        </commandBlock>
        <commandBlock>
          <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "%%DlpPolicyName%%" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP Policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]>
        </commandBlock>
      </policyCommands>
      <policyCommandsResources></policyCommandsResources>
    </dlpPolicyTemplate>
  </dlpPolicyTemplates>
  ```

모든 요소에 대해 XML 파일에 포함된 매개 변수에 공백이 있는 경우 매개 변수를 큰따옴표로 묶어야 합니다. 그렇지 않으면 제대로 작동하지 않습니다. 아래 예에서 `-SentToScope` 다음에 오는 매개 변수는 허용 가능하며, 공백이 없는 연속 문자열이므로 큰따옴표가 포함되지 않습니다. 하지만 –`Comments`에 대해 제공된 매개 변수는 큰따옴표가 없고 공백을 포함하므로 Exchange 관리 센터에 표시되지 않습니다.

  ```xml
  <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments Monitors payment card information sent inside the organization -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
  ```

## localizedString 요소

템플릿 형식은 예를 들어 설치할 DLP 정책 템플릿을 선택할 때 최종 사용자에게 표시될 수 있는 템플릿 내 문자열을 지역화하는 기능을 제공합니다. localizedString 요소를 사용하여 Name 및 Description 필드에 대한 여러 개의 정의를 제공할 수 있습니다.

## ruleParameters 노드

배포 관련 개체에 매핑할 DLP 정책을 만들 때 템플릿 인스턴스화 단계에서 제공해야 하는 선택적 매개 변수 집합입니다. 배포에 사용할 수 있는 실제 메일 그룹을 예로 들 수 있습니다.

## dlpPolicyTemplate 요소

DLP 정책 템플릿의 루트 요소로서 모든 템플릿에 필요합니다. 다음 표에는 사용 가능한 특성이 나와 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>특성 이름</th>
<th>필수 여부</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>예</p></td>
<td><p>이 DLP 정책 템플릿 문서에 사용된 버전 번호입니다.</p></td>
</tr>
<tr class="even">
<td><p>상태</p></td>
<td><p>아니요</p></td>
<td><p>정책 상태에 대한 선택적 기본 구성입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Mode</p></td>
<td><p>아니요</p></td>
<td><p>정책 모드에 대한 선택적 기본 구성입니다.</p></td>
</tr>
<tr class="even">
<td><p>Id</p></td>
<td><p>아니요</p></td>
<td><p>&quot;A29C69BF-4F98-47F1-9A99-5771DFD2C27F&quot;와 같은 형식으로 이 DLP 정책 템플릿 정의를 고유하게 식별하는 GUID입니다.</p></td>
</tr>
</tbody>
</table>


하위 요소는 다음 요소를 순서대로 포함합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>하위 요소</th>
<th>(최소, 최대)</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PublisherName</p></td>
<td><p>(1, 1)</p></td>
<td><p>템플릿 게시자에 대한 메타데이터입니다.</p></td>
</tr>
<tr class="even">
<td><p>이름</p></td>
<td><p>(1, 1)</p></td>
<td><p>이 템플릿에 대한 지역화 가능한 이름입니다.</p></td>
</tr>
<tr class="odd">
<td><p>설명</p></td>
<td><p>(1, 1)</p></td>
<td><p>이 템플릿에 대한 지역화 가능한 설명입니다.</p></td>
</tr>
<tr class="even">
<td><p>키워드</p></td>
<td><p>(1, 1)</p></td>
<td><p>이 템플릿에 적용되는 키워드 목록입니다. 템플릿의 키워드 목록을 비워 둘 수도 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>RuleParameters</p></td>
<td><p>(0, 1)</p></td>
<td><p>정책 정의에 사용된 템플릿 매개 변수 목록입니다.</p></td>
</tr>
<tr class="even">
<td><p>PolicyCommands</p></td>
<td><p>(0, 1)</p></td>
<td><p>이 정책에 대한 전송 규칙 정의 목록입니다. 이 요소는 선택적 요소입니다.</p></td>
</tr>
</tbody>
</table>


## DLP 정책 템플릿: PolicyCommands

정책 템플릿의 이 부분은 정책 정의를 인스턴스화하는 데 사용되는 Exchange 관리 셸 명령 목록을 포함합니다. 인스턴스화 프로세스의 일부로 가져오기 프로세스에서 각 명령이 실행됩니다. 다음은 샘플 정책 명령입니다.

  ```xml
  <PolicyCommands>
      <!-- The contents below are applied/executed as rules directly in PS - -->
        <CommandBlock> <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "PCI-DSS" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP policy."]]></CommandBlock>
        <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
    </PolicyCommands> 
  ```

cmdlet 형식은 사용되는 cmdlet에 대한 표준 Exchange 관리 셸 cmdlet 구문입니다. 명령은 순서대로 실행됩니다. 각 명령 노드는 여러 명령으로 이루어진 스크립트 블록을 포함할 수 있습니다. 다음은 DLP 정책 템플릿 내에 분류 규칙 팩을 포함하는 방법과 정책 생성 프로세스의 일부로 규칙 팩을 설치하는 방법을 보여 주는 예입니다. 분류 규칙 팩은 정책 템플릿에 포함되고 나중에 템플릿에서 cmdlet에 매개 변수로 전달됩니다.

```powershell 
<CommandBlock>
  <![CDATA[
$rulePack = [system.Text.Encoding]::Unicode.GetBytes('<?xml version="1.0" encoding="utf-16"?>
<rulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">

  <RulePack id="c3f021a3-c265-4dc2-b3a7-41a1800bf518">
    <Version major="1" minor="0" build="0" revision="0"/>
    <Publisher id="e17451d3-9648-4117-a0b1-493a6d5c73ad"/>
    <Details defaultLangCode="en-us">
      <LocalizedDetails langcode="en-us">
        <PublisherName>Contoso</PublisherName>
        <Name>Contoso Sample Rule Pack</Name>
        <Description>This is a sample rule package</Description>
      </LocalizedDetails>
    </Details>
  </RulePack>

  <Rules>
    <Entity id="7cc35258-6b35-4415-baff-a76d1a018980" patternsProximity="300" recommendedConfidence="85" workload="Exchange">     

      <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_Contoso" />
        <Any minMatches="1">
          <Match idRef="Regex_conf" />
        </Any>
      </Pattern>
    </Entity>

    <Regex id="Regex_Contoso">(?i)(\bContoso\b)</Regex>
    <Regex id="Regex_conf">(?i)(\bConfidential\b)</Regex>

    <LocalizedStrings>
      <Resource idRef="7cc35258-6b35-4415-baff-a76d1a018980">
        <Name default="true" langcode="en-us">
          Confidential Information Rule
        </Name>
        <Description default="true" langcode="en-us">
          Sample rule pack - Detects Contoso confidential information
        </Description>
      </Resource>
    </LocalizedStrings>
  </Rules>

</RulePackage>

')


New-ClassificationRuleCollection -FileData $rulePack 
New-TransportRule -name "customEntity" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -MessageContainsDataClassifications @{Name="Confidential Information Rule"} -SetAuditSeverity High]]>
</CommandBlock> 
```

하위 요소는 다음 요소를 순서대로 포함합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>하위 요소</th>
<th>(최소, 최대)</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CommandBlock</p></td>
<td><p>(1, n)</p></td>
<td><p>PowerShell에서 실행되는 명령 블록입니다. 명령 블록은 각각 순서대로 실행됩니다.</p></td>
</tr>
</tbody>
</table>


## 자세한 내용

[데이터 손실 방지](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[자체 DLP 템플릿 및 정보 유형 정의](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

