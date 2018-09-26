---
title: 'Exchange의 중요 한 정보 유형 찾아보십시오: Exchange 2013 Help'
TOCTitle: 중요 한 정보 형식을 찾습니다.
ms:assetid: 98b81f9c-87bb-4905-8e53-04621c3ae74d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150541(v=EXCHG.150)
ms:contentKeyID: 50482264
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange의 중요 한 정보 유형 찾아보십시오

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2018-05-03_

Exchange에서 데이터 손실 방지 (DLP)에 DLP 정책에서 사용 하 여 사용할 수 있는 80 중요 한 정보 유형을 포함 합니다. 이 항목 모두 이러한 중요 한 정보 유형 및 각 종류를 감지 하는 경우의 DLP 정책을 찾아 나와 있습니다. 중요 한 정보 유형 정규식 또는 함수를 식별할 수 있는 패턴에 의해 정의 됩니다. 또한 확증 적 인증 거 키워드 및 체크섬와 같은 중요 한 정보 형식을 식별 하기 위해 사용할 수 있습니다. 신뢰 수준 및 근접성 평가 프로세스에도 사용 됩니다.

## ABA 라우팅 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>서식 있는 패턴 또는 서식 없는 패턴으로 표시될 수 있는 9자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>서식 있음:</p>
<ul>
<li><p>0, 1, 2, 3, 6, 7 또는 8로 시작하는 4자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>4자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>1자리 숫자</p></li>
</ul>
<p>서식 없음:</p>
<ul>
<li><p>0, 1, 2, 3, 6, 7 또는 8로 시작하는 9자리 연속 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_aba_routing</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_ABA_Routing</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- ABA Routing Number -->
<Entity id="cb353f78-2b72-4c3c-8827-92ebe4f69fdf" patternsProximity="300" recommendedConfidence="75">
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_aba_routing" />
        <Match idRef="Keyword_ABA_Routing" />
      </Pattern>
 </Entity>
 ```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-1"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ABA_Routing</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>aba</p>
<p>aba #</p>
<p>aba routing #</p>
<p>aba routing number</p>
<p>aba #</p>
<p>abarouting#</p>
<p>aba number</p>
<p>abaroutingnumber</p>
<p>american bank association routing #</p>
<p>american bank association routing number</p>
<p>americanbankassociationrouting#</p>
<p>americanbankassociationroutingnumber</p>
<p>bank routing number</p>
<p>bankrouting#</p>
<p>bankroutingnumber</p>
<p>routing transit number</p>
<p>RTN</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 아르헨티나 국가 ID(DNI) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>마침표로 구분된 8자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>8자리 숫자:</p>
<ul>
<li><p>2자리 숫자</p></li>
<li><p>마침표</p></li>
<li><p>3자리 숫자</p></li>
<li><p>마침표</p></li>
<li><p>3자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_argentina_national_id</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_argentina_national_id</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Argentina National Identity (DNI) Number -->
<Entity id="eefbb00e-8282-433c-8620-8f1da3bffdb2" recommendedConfidence="75" patternsProximity="300">
   <Pattern confidenceLevel="75">
      <IdMatch idRef="Regex_argentina_national_id"/>
      <Match idRef="Keyword_argentina_national_id"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-3"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_argentina_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Argentina National Identity number</p>
<p>ID</p>
<p>Identification National Identity Card</p>
<p>DNI</p>
<p>NIC National Registry of Persons</p>
<p>Documento Nacional de Identidad</p>
<p>Registro Nacional de las Personas</p>
<p>Identidad</p>
<p>Identificación</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 호주 은행 계좌 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>6-10자리 숫자(은행 지점 번호 포함 또는 제외)</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>계좌 번호는 6-10자리 숫자입니다.</p>
<p>호주 은행 지점 번호:</p>
<ul>
<li><p>3자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>3자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_australia_bank_account_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_australia_bank_account_number</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Regex_australia_bank_account_number_bsb</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_australia_bank_account_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_australia_bank_account_number</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Australia Bank Account Number -->
<Entity id="74a54de9-2a30-4aa0-a8aa-3d9327fc07c7" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_australia_bank_account_number" />
        <Match idRef="Keyword_australia_bank_account_number" />
        <Match idRef="Regex_australia_bank_account_number_bsb" />
  </Pattern>
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_australia_bank_account_number" />
        <Match idRef="Keyword_australia_bank_account_number" />
  </Pattern>
 </Entity>
 ```
 </td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-5"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_australia_bank_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>swift bank code</p>
<p>correspondent bank</p>
<p>base currency</p>
<p>usa account</p>
<p>holder address</p>
<p>bank address</p>
<p>information account</p>
<p>fund transfers</p>
<p>bank charges</p>
<p>bank details</p>
<p>banking information</p>
<p>full names</p>
<p>iaea</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 호주 운전 면허 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>9개의 문자 및 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>9개의 문자 및 숫자:</p>
<ul>
<li><p>2자리 숫자 또는 문자(대/소문자 구분 안 함)</p></li>
<li><p>2자리 숫자</p></li>
<li><p>5자리 숫자 또는 문자(대/소문자 구분 안 함)</p></li>
<li><p>또는</p></li>
<li><p>1-2개의 선택적 문자(대/소문자 구분 안 함)</p></li>
<li><p>4-9자리 숫자</p></li>
<li><p>또는</p></li>
<li><p>9자리 숫자 또는 문자(대/소문자 구분 안 함)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_australia_drivers_license_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_australia_drivers_license_number</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_australia_drivers_license_number_exclusions</code>의 키워드가 발견되지 않았습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Australia Drivers License Number -->
<Entity id="1cbbc8f5-9216-4392-9eb5-5ac2298d1356" patternsProximity="300" recommendedConfidence="75">
   <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_australia_drivers_license_number" />
        <Match idRef="Keyword_australia_drivers_license_number" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_australia_drivers_license_number_exclusions" />
        </Any>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-7"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_australia_drivers_license_number</p></th>
<th><p>Keyword_australia_drivers_license_number_exclusions</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>international driving permits</p>
<p>australian automobile association</p>
<p>sydney nsw</p>
<p>international driving permit</p>
<p>DriverLicence</p>
<p>DriverLicences</p>
<p>Driver Lic</p>
<p>Driver Licence</p>
<p>Driver Licences</p>
<p>DriversLic</p>
<p>DriversLicence</p>
<p>DriversLicences</p>
<p>Drivers Lic</p>
<p>Drivers Lics</p>
<p>Drivers Licence</p>
<p>Drivers Licences</p>
<p>Driver'Lic</p>
<p>Driver'Lics</p>
<p>Driver'Licence</p>
<p>Driver'Licences</p>
<p>Driver'Lic</p>
<p>Driver' Lics</p>
<p>Driver' Licence</p>
<p>Driver'Licences</p>
<p>Driver'sLic</p>
<p>Driver'sLics</p>
<p>Driver'sLicence</p>
<p>Driver'sLicences</p>
<p>Driver's Lic</p>
<p>Driver's Lics</p>
<p>Driver's Licence</p>
<p>Driver's Licences</p>
<p>DriverLic#</p>
<p>DriverLics#</p>
<p>DriverLicence#</p>
<p>DriverLicences#</p>
<p>Driver Lic#</p>
<p>Driver Lics#</p>
<p>Driver Licence#</p>
<p>Driver Licences#</p>
<p>DriversLic#</p>
<p>DriversLics#</p>
<p>DriversLicence#</p>
<p>DriversLicences#</p>
<p>Drivers Lic#</p>
<p>Drivers Lics#</p>
<p>Drivers Licence#</p>
<p>Drivers Licences#</p>
<p>Driver'Lic#</p>
<p>Driver'Lics#</p>
<p>Driver'Licence#</p>
<p>Driver'Licences#</p>
<p>Driver' Lic#</p>
<p>Driver' Lics#</p>
<p>Driver' Licence#</p>
<p>Driver' Licences#</p>
<p>Driver'sLic#</p>
<p>Driver'sLics#</p>
<p>Driver'sLicence#</p>
<p>Driver'sLicences#</p>
<p>Driver's Lic#</p>
<p>Driver's Lics#</p>
<p>Driver's Licence#</p>
<p>Driver's Licences#</p></td>
<td><p>aaa</p>
<p>DriverLicense</p>
<p>DriverLicenses</p>
<p>Driver License</p>
<p>Driver Licenses</p>
<p>DriversLicense</p>
<p>DriversLicenses</p>
<p>Drivers License</p>
<p>Drivers Licenses</p>
<p>Driver'License</p>
<p>Driver'Licenses</p>
<p>Driver' License</p>
<p>Driver' Licenses</p>
<p>Driver'sLicense</p>
<p>Driver'sLicenses</p>
<p>Driver's License</p>
<p>Driver's Licenses</p>
<p>DriverLicense#</p>
<p>DriverLicenses#</p>
<p>Driver License#</p>
<p>Driver Licenses#</p>
<p>DriversLicense#</p>
<p>DriversLicenses#</p>
<p>Drivers License#</p>
<p>Drivers Licenses#</p>
<p>Driver'License#</p>
<p>Driver'Licenses#</p>
<p>Driver' License#</p>
<p>Driver' Licenses#</p>
<p>Driver'sLicense#</p>
<p>Driver'sLicenses#</p>
<p>Driver's License#</p>
<p>Driver's Licenses#</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 호주 의료 계좌 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>10-11자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10-11자리 숫자:</p>
<ul>
<li><p>첫 번째 숫자는 2-6 범위에 있습니다.</p></li>
<li><p>9번째 숫자는 검사 숫자입니다.</p></li>
<li><p>10번째 숫자는 문제 숫자입니다.</p></li>
<li><p>11번째 숫자(선택 사항)는 개인 번호입니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 95% 신뢰합니다.</p>
<ul>
<li><p><code>Func_australian_medical_account_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_Australia_Medical_Account_Number</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_australian_medical_account_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Australia Medical Account Number -->
<Entity id="104a99a0-3d3b-4542-a40d-ab0b9e1efe63" recommendedConfidence="85" patternsProximity="300">
    <Pattern confidenceLevel="95">
     <IdMatch idRef="Func_australian_medical_account_number"/>
     <Any minMatches="1">
     <Match idRef="Keyword_Australia_Medical_Account_Number"/>
     </Any>
  </Pattern>
<Pattern confidenceLevel="85">
     <IdMatch idRef="Func_australian_medical_account_number"/>
     <Any minMatches="0" maxMatches="0">
  <Match idRef="Keyword_Australia_Medical_Account_Number"/>
     </Any>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-9"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_Australia_Medical_Account_Number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>bank account details</p>
<p>medicare payments</p>
<p>mortgage account</p>
<p>bank payments</p>
<p>information branch</p>
<p>credit card loan</p>
<p>department of human services</p>
<p>local service</p>
<p>medicare</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 호주 여권 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>문자와 7자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>1개의 문자(대/소문자 구분 안 함)와 7자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_australia_passport_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_passport</code> 또는 <code>Keyword_australia_passport_number</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Australia Passport Number -->
<Entity id="29869db6-602d-4853-ab93-3484f905df50" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_australia_passport_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_passport" />
          <Match idRef="Keyword_australia_passport_number" />
        </Any>
   </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-11"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_passport</p></th>
<th><p>Keyword_australia_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Passport Number</p>
<p>Passport No</p>
<p>Passport #</p>
<p>Passport#</p>
<p>PassportID</p>
<p>Passportno</p>
<p>passportnumber</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート ＃</p>
<p>Numéro de passeport</p>
<p>Passeport n °</p>
<p>Passeport Non</p>
<p>Passeport #</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
<td><p>passport</p>
<p>passport details</p>
<p>immigration and citizenship</p>
<p>commonwealth of australia</p>
<p>department of immigration</p>
<p>residential address</p>
<p>department of immigration and citizenship</p>
<p>visa</p>
<p>national identity card</p>
<p>passport number</p>
<p>travel document</p>
<p>issuing authority</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 호주 세금 파일 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>8-9자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>일반적으로 다음과 같이 공백과 함께 표시되는 8-9자리 숫자:</p>
<ul>
<li><p>3자리 숫자</p></li>
<li><p>선택적 공백 1개</p></li>
<li><p>3자리 숫자</p></li>
<li><p>선택적 공백 1개</p></li>
<li><p>마지막 숫자가 검사 숫자인 2-3자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 95% 신뢰합니다.</p>
<ul>
<li><p><code>Func_australian_tax_file_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_Australia_Tax_File_Number</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_number_exclusions</code>의 키워드가 발견되지 않았습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_australian_tax_file_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_Australia_Tax_File_Number</code> 또는 <code>Keyword_number_exclusions</code>의 키워드가 발견되지 않았습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
    <!-- Australia Tax File Number -->
<Entity id="e29bc95f-ff70-4a37-aa01-04d17360a4c5" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="95">
        <IdMatch idRef="Func_australian_tax_file_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_Australia_Tax_File_Number" />
        </Any>
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_number_exclusions" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_australian_tax_file_number" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_Australia_Tax_File_Number" />
          <Match idRef="Keyword_number_exclusions" />
        </Any>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-13"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_Australia_Tax_File_Number</p></th>
<th><p>Keyword_number_exclusions</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>australian business number</p>
<p>marginal tax rate</p>
<p>medicare levy</p>
<p>portfolio number</p>
<p>service veterans</p>
<p>withholding tax</p>
<p>individual tax return</p>
<p>tax file number</p></td>
<td><p>00000000</p>
<p>11111111</p>
<p>22222222</p>
<p>33333333</p>
<p>44444444</p>
<p>55555555</p>
<p>66666666</p>
<p>77777777</p>
<p>88888888</p>
<p>99999999</p>
<p>000000000</p>
<p>111111111</p>
<p>222222222</p>
<p>333333333</p>
<p>444444444</p>
<p>555555555</p>
<p>666666666</p>
<p>777777777</p>
<p>888888888</p>
<p>999999999</p>
<p>0000000000</p>
<p>1111111111</p>
<p>2222222222</p>
<p>3333333333</p>
<p>4444444444</p>
<p>5555555555</p>
<p>6666666666</p>
<p>7777777777</p>
<p>8888888888</p>
<p>9999999999</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 벨기에 국가 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>11자리 숫자와 구분 기호</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>11자리 숫자와 구분 기호:</p>
<ul>
<li><p>생년월일을 나타내는 YY.MM.DD 형식의 6자리 숫자와 마침표 2개</p></li>
<li><p>하이픈</p></li>
<li><p>세 개의 순차적 숫자(남성의 경우 홀수, 여성의 경우 짝수)</p></li>
<li><p>마침표</p></li>
<li><p>검사 숫자에 해당하는 두 자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_belgium_national_number</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_belgium_national_number</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Belgium National Number -->
  <Entity id="fb969c9e-0fd1-4b18-8091-a2123c5e6a54" recommendedConfidence="75" patternsProximity="300">
   <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_belgium_national_number"/>
     <Match idRef="Keyword_belgium_national_number"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-15"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_belgium_national_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Identity</p>
<p>Registration</p>
<p>Identification</p>
<p>ID</p>
<p>Identiteitskaart</p>
<p>Registratie nummer</p>
<p>Identificatie nummer</p>
<p>Identiteit</p>
<p>Registratie</p>
<p>Identificatie</p>
<p>Carte d’identité</p>
<p>numéro d'immatriculation</p>
<p>numéro d'identification</p>
<p>identité</p>
<p>inscription</p>
<p>Identifikation</p>
<p>Identifizierung</p>
<p>Identifikationsnummer</p>
<p>Personalausweis</p>
<p>Registrierung</p>
<p>Registrationsnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 브라질 법인 번호(CNPJ)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>등록 번호, 지점 번호, 검사 숫자 및 구분 기호를 포함하는 14자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>14자리 숫자와 구분 기호:</p>
<ul>
<li><p>2자리 숫자</p></li>
<li><p>마침표</p></li>
<li><p>3자리 숫자</p></li>
<li><p>마침표</p></li>
<li><p>3자리 숫자(처음 8자리 숫자는 등록 번호임)</p></li>
<li><p>정방향 슬래시</p></li>
<li><p>4자리 지점 번호</p></li>
<li><p>하이픈</p></li>
<li><p>검사 숫자에 해당하는 2자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_brazil_cnpj</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_brazil_cnpj</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_brazil_cnpj</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Brazil Legal Entity Number (CNPJ) -->
<Entity id="9b58b5cd-5e90-4df6-b34f-1ebcc88ceae4" recommendedConfidence="85" patternsProximity="300">
   <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_brazil_cnpj"/>
     <Match idRef="Keyword_brazil_cnpj"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_brazil_cnpj"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-17"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_brazil_cnpj</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CNPJ</p>
<p>CNPJ/MF</p>
<p>CNPJ-MF</p>
<p>National Registry of Legal Entities</p>
<p>Taxpayers Registry</p>
<p>Legal entity</p>
<p>Legal entities</p>
<p>Registration Status</p>
<p>Business</p>
<p>Company</p>
<p>CNPJ</p>
<p>Cadastro Nacional da Pessoa Jurídica</p>
<p>Cadastro Geral de Contribuintes</p>
<p>CGC</p>
<p>Pessoa jurídica</p>
<p>Pessoas jurídicas</p>
<p>Situação cadastral</p>
<p>Inscrição</p>
<p>Empresa</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 브라질 CPF 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>서식이 있거나 서식이 없을 수 있는 검사 숫자를 포함하는 11자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>서식 있음:</p>
<ul>
<li><p>3자리 숫자</p></li>
<li><p>마침표</p></li>
<li><p>3자리 숫자</p></li>
<li><p>마침표</p></li>
<li><p>3자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>검사 숫자에 해당하는 2자리 숫자</p></li>
</ul>
<p>서식 없음:</p>
<ul>
<li><p>마지막 2자리 숫자가 검사 숫자인 11자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_brazil_cpf</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_brazil_cpf</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_brazil_cpf</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Brazil CPF Number -->
<Entity id="78e09124-f2c3-4656-b32a-c1a132cd2711" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_brazil_cpf"/>
     <Match idRef="Keyword_brazil_cpf"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_brazil_cpf"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-19"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_brazil_cpf</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPF</p>
<p>Identification</p>
<p>Registration</p>
<p>Revenue</p>
<p>Cadastro de Pessoas Físicas</p>
<p>Imposto</p>
<p>Identificação</p>
<p>Inscrição</p>
<p>Receita</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 브라질 국가 ID 카드(RG)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>Registro Geral(이전 형식)</p>
<dl>
<dd><p>9자리 숫자</p>
</dd>
</dl>
<p>Registro de Identidade(RIC)(새로운 형식)</p>
<dl>
<dd><p>11자리 숫자</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>Registro Geral(이전 형식):</p>
<ul>
<li><p>2자리 숫자</p></li>
<li><p>마침표</p></li>
<li><p>3자리 숫자</p></li>
<li><p>마침표</p></li>
<li><p>3자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>검사 숫자에 해당하는 1자리 숫자</p></li>
</ul>
<p>Registro de Identidade(RIC)(새로운 형식)</p>
<ul>
<li><p>10자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>검사 숫자에 해당하는 1자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_brazil_rg</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_brazil_rg</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_brazil_rg</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Brazil National ID Card (RG) -->
<Entity id="486de900-db70-41b3-a886-abdf25af119c" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_brazil_rg"/>
     <Match idRef="Keyword_brazil_rg"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_brazil_rg"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-21"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_brazil_rg</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cédula de identidade</p>
<p>identity card</p>
<p>national id</p>
<p>número de rregistro</p>
<p>registro de Iidentidade</p>
<p>registro geral</p>
<p>RG(이 키워드는 대/소문자를 구분함)</p>
<p>RIC(이 키워드는 대/소문자를 구분하지 않음)</p>
<p></p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 캐나다 은행 계좌 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>7 또는 12자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>캐나다 은행 계좌 번호는 7 또는 12자리 숫자입니다.</p>
<p>캐나다 은행 계좌 송금 번호:</p>
<ul>
<li><p>5자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>3자리 숫자</p>
<p>또는</p></li>
<li><p>"0"</p>
<p>8자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_canada_bank_account_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_canada_bank_account_number</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Regex_canada_bank_account_transit_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_canada_bank_account_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_canada_bank_account_number</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Canada Bank Account Number -->
<Entity id="552e814c-cb50-4d94-bbaa-bb1d1ffb34de" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_canada_bank_account_number" />
        <Match idRef="Keyword_canada_bank_account_number" />
        <Match idRef="Regex_canada_bank_account_transit_number" />
   </Pattern>
   <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_bank_account_number" />
        <Match idRef="Keyword_canada_bank_account_number" />
   </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-23"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_bank_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>canada savings bonds</p>
<p>canada revenue agency</p>
<p>canadian financial institution</p>
<p>direct deposit form</p>
<p>canadian citizen</p>
<p>legal representative</p>
<p>notary public</p>
<p>commissioner for oaths</p>
<p>child care benefit</p>
<p>universal child care</p>
<p>canada child tax benefit</p>
<p>income tax benefit</p>
<p>harmonized sales tax</p>
<p>social insurance number</p>
<p>income tax refund</p>
<p>child tax benefit</p>
<p>territorial payments</p>
<p>institution number</p>
<p>deposit request</p>
<p>banking information</p>
<p>direct deposit</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 캐나다 운전 면허 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>지역마다 다름</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>앨버타, 브리티시 콜롬비아, 매니토바, 뉴브런즈윅, 뉴펀들랜드/래브라도, 노바스코샤, 온타리오, 프린스에드워드아일랜드, 퀘벡 및 서스캐처원을 포함하는 다양한 패턴</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_[province_name]_drivers_license_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_[province_name]_drivers_license_name</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_canada_drivers_license</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Canada Driver's License Number -->
    <Entity id="37186abb-8e48-4800-ad3c-e3d1610b3db0" patternsProximity="300" recommendedConfidence="75">
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_alberta_drivers_license_number" />
        <Match idRef="Keyword_alberta_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_british_columbia_drivers_license_number" />
        <Match idRef="Keyword_british_columbia_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_manitoba_drivers_license_number" />
        <Match idRef="Keyword_manitoba_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_new_brunswick_drivers_license_number" />
        <Match idRef="Keyword_new_brunswick_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_newfoundland_labrador_drivers_license_number" />
        <Match idRef="Keyword_newfoundland_labrador_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_nova_scotia_drivers_license_number" />
        <Match idRef="Keyword_nova_scotia_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_ontario_drivers_license_number" />
        <Match idRef="Keyword_ontario_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_prince_edward_island_drivers_license_number" />
        <Match idRef="Keyword_prince_edward_island_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_quebec_drivers_license_number" />
        <Match idRef="Keyword_quebec_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_saskatchewan_drivers_license_number" />
        <Match idRef="Keyword_saskatchewan_drivers_license_name" />
        <Match idRef="Keyword_canada_drivers_license" />
      </Pattern>
    </Entity>
  ```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-25"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_[province_name]_drivers_license_name</p></th>
<th><p>Keyword_canada_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>시/도 약어(예: AB)</p>
<p>시/도 이름(예: 앨버타)</p></td>
<td><p>DL</p>
<p>DL</p>
<p>CDL</p>
<p>CDLS</p>
<p>DriverLic</p>
<p>DriverLics</p>
<p>DriverLicense</p>
<p>DriverLicenses</p>
<p>DriverLicence</p>
<p>DriverLicences</p>
<p>Driver Lic</p>
<p>Driver Lics</p>
<p>Driver License</p>
<p>Driver Licenses</p>
<p>Driver Licence</p>
<p>Driver Licences</p>
<p>DriversLic</p>
<p>DriversLics</p>
<p>DriversLicence</p>
<p>DriversLicences</p>
<p>DriversLicense</p>
<p>DriversLicenses</p>
<p>Drivers Lic</p>
<p>Drivers Lics</p>
<p>Drivers License</p>
<p>Drivers Licenses</p>
<p>Drivers Licence</p>
<p>Drivers Licences</p>
<p>Driver'Lic</p>
<p>Driver'Lics</p>
<p>Driver'License</p>
<p>Driver'Licenses</p>
<p>Driver'Licence</p>
<p>Driver'Licences</p>
<p>Driver'Lic</p>
<p>Driver'Lics</p>
<p>Driver'License</p>
<p>Driver'Licenses</p>
<p>Driver'Licence</p>
<p>Driver'Licences</p>
<p>Driver'sLic</p>
<p>Driver'sLics</p>
<p>Driver'sLicense</p>
<p>Driver'sLicenses</p>
<p>Driver'sLicence</p>
<p>Driver'sLicences</p>
<p>Driver's Lic</p>
<p>Driver's Lics</p>
<p>Driver's License</p>
<p>Driver's Licenses</p>
<p>Driver's Licence</p>
<p>Driver's Licences</p>
<p>Permis de Conduire</p>
<p>id</p>
<p>ids</p>
<p>idcard number</p>
<p>idcard numbers</p>
<p>idcard #</p>
<p>idcard #s</p>
<p>idcard card</p>
<p>idcard cards</p>
<p>idcard</p>
<p>identification number</p>
<p>identification numbers</p>
<p>identification #</p>
<p>identification #s</p>
<p>identification card</p>
<p>identification cards</p>
<p>identification</p>
<p>DL#</p>
<p>DLS#</p>
<p>CDL#</p>
<p>CDLS#</p>
<p>DriverLic#</p>
<p>DriverLics#</p>
<p>DriverLicense#</p>
<p>DriverLicenses#</p>
<p>DriverLicence#</p>
<p>DriverLicences#</p>
<p>Driver Lic#</p>
<p>Driver Lics#</p>
<p>Driver License#</p>
<p>Driver Licenses#</p>
<p>Driver License#</p>
<p>Driver Licences#</p>
<p>DriversLic#</p>
<p>DriversLics#</p>
<p>DriversLicense#</p>
<p>DriversLicenses#</p>
<p>DriversLicence#</p>
<p>DriversLicences#</p>
<p>Drivers Lic#</p>
<p>Drivers Lics#</p>
<p>Drivers License#</p>
<p>Drivers Licenses#</p>
<p>Drivers Licence#</p>
<p>Drivers Licences#</p>
<p>Driver'Lic#</p>
<p>Driver'Lics#</p>
<p>Driver'License#</p>
<p>Driver'Licenses#</p>
<p>Driver'Licence #</p>
<p>Driver'Licences#</p>
<p>Driver' Lic#</p>
<p>Driver' Lics#</p>
<p>Driver' License#</p>
<p>Driver' Licenses#</p>
<p>Driver' Licence#</p>
<p>Driver' Licences#</p>
<p>Driver'sLic#</p>
<p>Driver'sLics#</p>
<p>Driver'sLicense#</p>
<p>Driver'sLicenses#</p>
<p>Driver'sLicence#</p>
<p>Driver'sLicences#</p>
<p>Driver's Lic#</p>
<p>Driver's Lics#</p>
<p>Driver's License#</p>
<p>Driver's Licenses#</p>
<p>Driver's Licence#</p>
<p>Driver's Licences#</p>
<p>Permis de Conduire#</p>
<p>id#</p>
<p>ids#</p>
<p>idcard card#</p>
<p>idcard cards#</p>
<p>idcard#</p>
<p>identification card#</p>
<p>identification cards#</p>
<p>identification#</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 캐나다 건강 서비스 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>10자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_canada_health_service_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_canada_health_service_number</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Canada Health Service Number -->
<Entity id="59c0bf39-7fab-482c-af25-00faa4384c94" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_health_service_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_canada_health_service_number" />
        </Any>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-27"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_health_service_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>personal health number</p>
<p>patient information</p>
<p>health services</p>
<p>speciality services</p>
<p>automobile accident</p>
<p>patient hospital</p>
<p>psychiatrist</p>
<p>workers compensation</p>
<p>disability</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 캐나다 여권 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>2개의 대문자와 6자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>2개의 대문자와 6자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_canada_passport_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_canada_passport_number</code> 또는 <code>Keyword_passport</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
 <!-- Canada Passport Number -->
<Entity id="14d0db8b-498a-43ed-9fca-f6097ae687eb" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_passport_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_canada_passport_number" />
          <Match idRef="Keyword_passport" />
        </Any>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-29"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_passport_number</p></th>
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>canadian citizenship</p>
<p>canadian passport</p>
<p>passport application</p>
<p>passport photos</p>
<p>certified translator</p>
<p>canadian citizens</p>
<p>processing times</p>
<p>renewal application</p></td>
<td><p>Passport Number</p>
<p>Passport No</p>
<p>Passport #</p>
<p>Passport#</p>
<p>PassportID</p>
<p>Passportno</p>
<p>passportnumber</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n °</p>
<p>Passeport Non</p>
<p>Passeport #</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 캐나다 PHIN(개인 건강 식별 번호)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>9자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>9자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_canada_phin</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_canada_phin</code> 또는 <code>Keyword_canada_provinces</code>의 2개 이상의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Canada PHIN -->
<Entity id="722e12ac-c89a-4ec8-a1b7-fea3469f89db" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_canada_phin" />
        <Any minMatches="2">
          <Match idRef="Keyword_canada_phin" />
          <Match idRef="Keyword_canada_provinces" />
        </Any>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-31"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_canada_phin</p></th>
<th><p>Keyword_canada_provinces</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>social insurance number</p>
<p>health information act</p>
<p>income tax information</p>
<p>manitoba health</p>
<p>health registration</p>
<p>prescription purchases</p>
<p>benefit eligibility</p>
<p>personal health</p>
<p>power of attorney</p>
<p>registration number</p>
<p>personal health number</p>
<p>practitioner referral</p>
<p>wellness professional</p>
<p>patient referral</p>
<p>health and wellness</p></td>
<td><p>Nunavut</p>
<p>Quebec</p>
<p>Northwest Territories</p>
<p>Ontario</p>
<p>British Columbia</p>
<p>Alberta</p>
<p>Saskatchewan</p>
<p>Manitoba</p>
<p>Yukon</p>
<p>Newfoundland and Labrador</p>
<p>New Brunswick</p>
<p>Nova Scotia</p>
<p>Prince Edward Island</p>
<p>Canada</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 캐나다 사회 보험 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>선택적 하이픈 또는 공백을 포함하는 9자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>서식 있음:</p>
<ul>
<li><p>3자리 숫자</p></li>
<li><p>하이픈 또는 공백</p></li>
<li><p>3자리 숫자</p></li>
<li><p>하이픈 또는 공백</p></li>
<li><p>3자리 숫자</p></li>
</ul>
<p>서식 없음:</p>
<ul>
<li><p>9자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_canadian_sin</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>2개 이상의 다음 항목 조합:</p>
<ul>
<li><p><code>Keyword_sin</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_sin_collaborative</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Func_eu_date</code> 함수가 올바른 날짜 형식의 날짜를 찾습니다.</p></li>
</ul></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_unformatted_canadian_sin</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_sin</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Canada Social Insurance Number -->
<Entity id="a2f29c85-ecb8-4514-a610-364790c0773e" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_canadian_sin" />
        <Any minMatches="2">
          <Match idRef="Keyword_sin" />
          <Match idRef="Keyword_sin_collaborative" />
          <Match idRef="Func_eu_date" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_unformatted_canadian_sin" />
        <Match idRef="Keyword_sin" />
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-33"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_sin</p></th>
<th><p>Keyword_sin_collaborative</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>sin</p>
<p>social insurance</p>
<p>numero d'assurance sociale</p>
<p>sins</p>
<p>ssn</p>
<p>ssn</p>
<p>social security</p>
<p>numero d'assurance social</p>
<p>national identification number</p>
<p>national id</p>
<p>sin#</p>
<p>soc ins</p>
<p>social ins</p></td>
<td><p>driver's license</p>
<p>drivers license</p>
<p>driver's licence</p>
<p>drivers licence</p>
<p>DOB</p>
<p>Birthdate</p>
<p>Birthday</p>
<p>Date of Birth</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 칠레 ID 카드 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>7-8자리 숫자와 구분 기호, 검사 숫자 또는 문자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>7-8자리 숫자와 구분 기호:</p>
<ul>
<li><p>1-2자리 숫자</p></li>
<li><p>마침표</p></li>
<li><p>3자리 숫자</p></li>
<li><p>마침표</p></li>
<li><p>3자리 숫자</p></li>
<li><p>대시 1개</p></li>
<li><p>검사 숫자에 해당하는 1자리 숫자 또는 문자(대/소문자 구분 안 함)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_chile_id_card</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_chile_id_card</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_chile_id_card</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Chile Identity Card Number -->
<Entity id="4e979794-49a0-407e-a0b9-2c536937b925" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_chile_id_card"/>
     <Match idRef="Keyword_chile_id_card"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_chile_id_card"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-35"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_chile_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>National Identification Number</p>
<p>Identity card</p>
<p>ID</p>
<p>Identification</p>
<p>Rol Único Nacional</p>
<p>RUN</p>
<p>Rol Único Tributario</p>
<p>RUT</p>
<p>Cédula de Identidad</p>
<p>Número De Identificación Nacional</p>
<p>Tarjeta de identificación</p>
<p>Identificación</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 중국 주민 ID 카드(PRC) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>18자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>18자리 숫자:</p>
<ul>
<li><p>주소 코드에 해당하는 6자리 숫자</p></li>
<li><p>생년월일에 해당하는 YYYYMMDD 형식의 8자리 숫자</p></li>
<li><p>주문 코드에 해당하는 3자리 숫자</p></li>
<li><p>검사 숫자에 해당하는 1자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_china_resident_id</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_china_resident_id</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_china_resident_id</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- China Resident Identity Card (PRC) Number -->
<Entity id="c92daa86-2d16-4871-901f-816b3f554fc1" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_china_resident_id"/>
     <Match idRef="Keyword_china_resident_id"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_china_resident_id"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-37"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_china_resident_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Resident Identity Card</p>
<p>PRC</p>
<p>National Identification Card</p>
<p>身份证</p>
<p>居民 身份证</p>
<p>居民身份证</p>
<p>鉴定</p>
<p>身分證</p>
<p>居民 身份證</p>
<p>鑑定</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 신용 카드 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>서식을 지정할 수는 16 자리 또는 서식이 지정 되지 않은 (dddddddddddddddd) Luhn 테스트로 전달 해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>Visa, MasterCard, Discover Card, JCB, American Express, 상품권 및 식사권을 비롯하여 전 세계 모든 주요 브랜드 카드를 검색하는 매우 복잡하고 강력한 패턴입니다.</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>있음(Luhn 체크섬)</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_credit_card</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>다음 중 하나가 충족됩니다.</p>
<ul>
<li><p><code>Keyword_cc_verification</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_cc_name</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Func_expiration_date</code> 함수가 올바른 날짜 형식의 날짜를 찾습니다.</p></li>
</ul></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 65% 신뢰합니다.</p>
<ul>
<li><p><code>Func_credit_card</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Credit Card Number -->
<Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_credit_card" />
        <Any minMatches="1">
          <Match idRef="Keyword_cc_verification" />
          <Match idRef="Keyword_cc_name" />
          <Match idRef="Func_expiration_date" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="65">
        <IdMatch idRef="Func_credit_card" />
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-39"> </h3>
<div>
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_cc_verification</p></th>
<th><p>Keyword_cc_name</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>card verification</p>
<p>card identification number</p>
<p>cvn</p>
<p>cid</p>
<p>cvc2</p>
<p>cvv2</p>
<p>pin block</p>
<p>security code</p>
<p>security number</p>
<p>security no</p>
<p>issue number</p>
<p>issue no</p>
<p>cryptogramme</p>
<p>numéro de sécurité</p>
<p>numero de securite</p>
<p>kreditkartenprüfnummer</p>
<p>kreditkartenprufnummer</p>
<p>prüfziffer</p>
<p>prufziffer</p>
<p>sicherheits Kode</p>
<p>sicherheitscode</p>
<p>sicherheitsnummer</p>
<p>verfalldatum</p>
<p>codice di verifica</p>
<p>cod. sicurezza</p>
<p>cod sicurezza</p>
<p>n autorizzazione</p>
<p>código</p>
<p>codigo</p>
<p>cod. seg</p>
<p>cod seg</p>
<p>código de segurança</p>
<p>codigo de seguranca</p>
<p>codigo de segurança</p>
<p>código de seguranca</p>
<p>cód. segurança</p>
<p>cod. seguranca cod. segurança</p>
<p>cód. seguranca</p>
<p>cód segurança</p>
<p>cod seguranca cod segurança</p>
<p>cód seguranca</p>
<p>número de verificação</p>
<p>numero de verificacao</p>
<p>ablauf</p>
<p>gültig bis</p>
<p>gültigkeitsdatum</p>
<p>gultig bis</p>
<p>gultigkeitsdatum</p>
<p>scadenza</p>
<p>data scad</p>
<p>fecha de expiracion</p>
<p>fecha de venc</p>
<p>vencimiento</p>
<p>válido hasta</p>
<p>valido hasta</p>
<p>vto</p>
<p>data de expiração</p>
<p>data de expiracao</p>
<p>data em que expira</p>
<p>validade</p>
<p>valor</p>
<p>vencimento</p>
<p>Venc</p></td>
<td><p>amex</p>
<p>american express</p>
<p>americanexpress</p>
<p>Visa</p>
<p>mastercard</p>
<p>master card</p>
<p>mc</p>
<p>mastercards</p>
<p>master cards</p>
<p>diner's Club</p>
<p>diners club</p>
<p>dinersclub</p>
<p>discover card</p>
<p>discovercard</p>
<p>discover cards</p>
<p>JCB</p>
<p>japanese card bureau</p>
<p>carte blanche</p>
<p>carteblanche</p>
<p>credit card</p>
<p>cc#</p>
<p>cc#:</p>
<p>expiration date</p>
<p>exp date</p>
<p>expiry date</p>
<p>date d’expiration</p>
<p>date d'exp</p>
<p>date expiration</p>
<p>bank card</p>
<p>bankcard</p>
<p>card number</p>
<p>card num</p>
<p>cardnumber</p>
<p>cardnumbers</p>
<p>card numbers</p>
<p>creditcard</p>
<p>credit cards</p>
<p>creditcards</p>
<p>ccn</p>
<p>card holder</p>
<p>cardholder</p>
<p>card holders</p>
<p>cardholders</p>
<p>check card</p>
<p>checkcard</p>
<p>check cards</p>
<p>checkcards</p>
<p>debit card</p>
<p>debitcard</p>
<p>debit cards</p>
<p>debitcards</p>
<p>atm card</p>
<p>atmcard</p>
<p>atm cards</p>
<p>atmcards</p>
<p>enroute</p>
<p>en route</p>
<p>card type</p>
<p>carte bancaire</p>
<p>carte de crédit</p>
<p>carte de credit</p>
<p>numéro de carte</p>
<p>numero de carte</p>
<p>nº de la carte</p>
<p>nº de carte</p>
<p>kreditkarte</p>
<p>karte</p>
<p>karteninhaber</p>
<p>karteninhabers</p>
<p>kreditkarteninhaber</p>
<p>kreditkarteninstitut</p>
<p>kreditkartentyp</p>
<p>eigentümername</p>
<p>kartennr</p>
<p>kartennummer</p>
<p>kreditkartennummer</p>
<p>kreditkarten-nummer</p>
<p>carta di credito</p>
<p>carta credito</p>
<p>n. carta</p>
<p>n carta</p>
<p>nr. carta</p>
<p>nr carta</p>
<p>numero carta</p>
<p>numero della carta</p>
<p>numero di carta</p>
<p>tarjeta credito</p>
<p>tarjeta de credito</p>
<p>tarjeta crédito</p>
<p>tarjeta de crédito</p>
<p>tarjeta de atm</p>
<p>tarjeta atm</p>
<p>tarjeta debito</p>
<p>tarjeta de debito</p>
<p>tarjeta débito</p>
<p>tarjeta de débito</p>
<p>nº de tarjeta</p>
<p>no. de tarjeta</p>
<p>no de tarjeta</p>
<p>numero de tarjeta</p>
<p>número de tarjeta</p>
<p>tarjeta no</p>
<p>tarjetahabiente</p>
<p>cartão de crédito</p>
<p>cartão de credito</p>
<p>cartao de crédito</p>
<p>cartao de credito</p>
<p>cartão de débito</p>
<p>cartao de débito</p>
<p>cartão de debito</p>
<p>cartao de debito</p>
<p>débito automático</p>
<p>debito automatico</p>
<p>número do cartão</p>
<p>numero do cartão</p>
<p>número do cartao</p>
<p>numero do cartao</p>
<p>número de cartão</p>
<p>numero de cartão</p>
<p>número de cartao</p>
<p>numero de cartao</p>
<p>nº do cartão</p>
<p>nº do cartao</p>
<p>nº. do cartão</p>
<p>no do cartão</p>
<p>no do cartao</p>
<p>no. do cartão</p>
<p>no. do cartao</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 크로아티아 ID 카드 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>9자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>9자리 연속 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_croatia_id_card</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_croatia_id_card</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!--Croatia Identity Card Number-->
<Entity id="ff12f884-c20a-4189-b185-34c8e7258d47" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_croatia_id_card"/>
     <Match idRef="Keyword_croatia_id_card"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-41"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_croatia_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Croatian identity card</p>
<p>Osobna iskaznica</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 크로아티아 개인 식별(OIB) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>10자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10자리 숫자:</p>
<ul>
<li><p>생년월일에 해당하는 DDMMYY 형식의 6자리 숫자</p></li>
<li><p>마지막 숫자가 검사 숫자인 4자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_croatia_oib_number</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_croatia_oib_number</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_croatia_oib_number</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Croatia Personal Identification (OIB) Number -->
<Entity id="31983b6d-db95-4eb2-a630-b44bd091968d" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_croatia_oib_number"/>
     <Match idRef="Keyword_croatia_oib_number"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_croatia_oib_number"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-43"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_croatia_oib_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Personal Identification Number</p>
<p>Osobni identifikacijski broj</p>
<p>OIB</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 체코 국가 ID 카드 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>정방향 슬래시를 포함하는 10자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10자리 숫자:</p>
<ul>
<li><p>생년월일에 해당하는 6자리 숫자</p></li>
<li><p>정방향 슬래시</p></li>
<li><p>마지막 숫자가 검사 숫자인 4자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_czech_id_card</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_czech_id_card</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Czech National Identity Card Number -->
<Entity id="60c0725a-4eb6-455b-9dda-05d8a7396497" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_czech_id_card"/>
     <Match idRef="Keyword_czech_id_card"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-45"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_czech_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Czech national identity card</p>
<p>Občanský průka</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 덴마크 개인 식별 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>하이픈을 포함하는 10자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10자리 숫자:</p>
<ul>
<li><p>생년월일에 해당하는 DDMMYY 형식의 6자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>마지막 숫자가 검사 숫자인 4자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_denmark_id</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_denmark_id</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Denmark Personal Identification Number -->
<Entity id="6c4f2fef-56e1-4c00-8093-88d7a01cf460" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_denmark_id"/>
     <Match idRef="Keyword_denmark_id"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-47"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_denmark_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Personal Identification Number</p>
<p>CPR</p>
<p>Det Centrale Personregister</p>
<p>Personnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## DEA(약물 집행 기구) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>2개 문자와 7자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>패턴에는 다음이 모두 포함되어야 합니다.</p>
<ul>
<li><p>등록 코드에 해당하는 abcdefghjklmnprstux 중 한 문자(대/소문자 구분 안 함)</p></li>
<li><p>등록자 성의 첫 문자에 해당하는 한 문자(대/소문자 구분 안 함)</p></li>
<li><p>검사 숫자의 마지막 7개 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_dea_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- DEA Number -->
<Entity id="9a5445ad-406e-43eb-8bd7-cac17ab6d0e4" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_dea_number"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><p>없음</p></td>
</tr>
</tbody>
</table>


## 유럽 직불 카드 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>16자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>매우 복잡하고 강력한 패턴</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_eu_debit_card</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>다음 중 하나 이상이 충족됩니다.</p>
<ul>
<li><p><code>Keyword_eu_debit_card</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_card_terms_dict</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_card_security_terms_dict</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_card_expiration_terms_dict</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Func_expiration_date</code> 함수가 올바른 날짜 형식의 날짜를 찾습니다.</p></li>
</ul></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
    <!-- EU Debit Card Number -->
    <Entity id="0e9b3178-9678-47dd-a509-37222ca96b42" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_eu_debit_card" />
        <Any minMatches="1">
          <Match idRef="Keyword_eu_debit_card" />
          <Match idRef="Keyword_card_terms_dict" />
          <Match idRef="Keyword_card_security_terms_dict" />
          <Match idRef="Keyword_card_expiration_terms_dict" />
          <Match idRef="Func_expiration_date" />
        </Any>
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-50"> </h3>
<div>
<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_eu_debit_card</p></th>
<th> </th>
<th><p>Keyword_card_terms_dict</p></th>
<th><p>Keyword_card_security_terms_dict</p></th>
<th><p>Keyword_card_expiration_terms_dict</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>account number</p>
<p>card number</p>
<p>card no.</p>
<p>security number</p>
<p>cc#</p></td>
<td> </td>
<td><p>acct nbr</p>
<p>acct num</p>
<p>acct no</p>
<p>american express</p>
<p>americanexpress</p>
<p>americano espresso</p>
<p>amex</p>
<p>atm card</p>
<p>atm cards</p>
<p>atm kaart</p>
<p>atmcard</p>
<p>atmcards</p>
<p>atmkaart</p>
<p>atmkaarten</p>
<p>bancontact</p>
<p>bank card</p>
<p>bankkaart</p>
<p>card holder</p>
<p>card holders</p>
<p>card num</p>
<p>card number</p>
<p>card numbers</p>
<p>card type</p>
<p>cardano numerico</p>
<p>cardholder</p>
<p>cardholders</p>
<p>cardnumber</p>
<p>cardnumbers</p>
<p>carta bianca</p>
<p>carta credito</p>
<p>carta di credito</p>
<p>cartao de credito</p>
<p>cartao de crédito</p>
<p>cartao de debito</p>
<p>cartao de débito</p>
<p>carte bancaire</p>
<p>carte blanche</p>
<p>carte bleue</p>
<p>carte de credit</p>
<p>carte de crédit</p>
<p>carte di credito</p>
<p>carteblanche</p>
<p>cartão de credito</p>
<p>cartão de crédito</p>
<p>cartão de debito</p>
<p>cartão de débito</p>
<p>cb</p>
<p>ccn</p>
<p>check card</p>
<p>check cards</p>
<p>checkcard</p>
<p>checkcards</p>
<p>chequekaart</p>
<p>cirrus</p>
<p>cirrus-edc-maestro</p>
<p>controlekaart</p>
<p>controlekaarten</p>
<p>credit card</p>
<p>credit cards</p>
<p>creditcard</p>
<p>creditcards</p>
<p>debetkaart</p>
<p>debetkaarten</p>
<p>debit card</p>
<p>debit cards</p>
<p>debitcard</p>
<p>debitcards</p>
<p>debito automatico</p>
<p>diners club</p>
<p>dinersclub</p>
<p>discover</p>
<p>discover card</p>
<p>discover cards</p>
<p>discovercard</p>
<p>discovercards</p>
<p>débito automático</p>
<p>edc</p>
<p>eigentümername</p>
<p>european debit card</p>
<p>hoofdkaart</p>
<p>hoofdkaarten</p>
<p>in viaggio</p>
<p>japanese card bureau</p>
<p>japanse kaartdienst</p>
<p>jcb</p>
<p>kaart</p>
<p>kaart num</p>
<p>kaartaantal</p>
<p>kaartaantallen</p>
<p>kaarthouder</p>
<p>kaarthouders</p>
<p>karte</p>
<p>karteninhaber</p>
<p>karteninhabers</p>
<p>kartennr</p>
<p>kartennummer</p>
<p>kreditkarte</p>
<p>kreditkarten-nummer</p>
<p>kreditkarteninhaber</p>
<p>kreditkarteninstitut</p>
<p>kreditkartennummer</p>
<p>kreditkartentyp</p>
<p>maestro</p>
<p>master card</p>
<p>master cards</p>
<p>mastercard</p>
<p>mastercards</p>
<p>mc</p>
<p>mister cash</p>
<p>n carta</p>
<p>n. carta</p>
<p>no de tarjeta</p>
<p>no do cartao</p>
<p>no do cartão</p>
<p>no. de tarjeta</p>
<p>no. do cartao</p>
<p>no. do cartão</p>
<p>nr carta</p>
<p>nr. carta</p>
<p>numeri di scheda</p>
<p>numero carta</p>
<p>numero de cartao</p>
<p>numero de carte</p>
<p>numero de cartão</p>
<p>numero de tarjeta</p>
<p>numero della carta</p>
<p>numero di carta</p>
<p>numero di scheda</p>
<p>numero do cartao</p>
<p>numero do cartão</p>
<p>numéro de carte</p>
<p>nº carta</p>
<p>nº de carte</p>
<p>nº de la carte</p>
<p>nº de tarjeta</p>
<p>nº do cartao</p>
<p>nº do cartão</p>
<p>nº. do cartão</p>
<p>número de cartao</p>
<p>número de cartão</p>
<p>número de tarjeta</p>
<p>número do cartao</p>
<p>scheda dell'assegno</p>
<p>scheda dell'atmosfera</p>
<p>scheda dell'atmosfera</p>
<p>scheda della banca</p>
<p>scheda di controllo</p>
<p>scheda di debito</p>
<p>scheda matrice</p>
<p>schede dell'atmosfera</p>
<p>schede di controllo</p>
<p>schede di debito</p>
<p>schede matrici</p>
<p>scoprono la scheda</p>
<p>scoprono le schede</p>
<p>solo</p>
<p>supporti di scheda</p>
<p>supporto di scheda</p>
<p>switch</p>
<p>tarjeta atm</p>
<p>tarjeta credito</p>
<p>tarjeta de atm</p>
<p>tarjeta de credito</p>
<p>tarjeta de debito</p>
<p>tarjeta debito</p>
<p>tarjeta no</p>
<p>tarjetahabiente</p>
<p>tipo della scheda</p>
<p>ufficio giapponese della</p>
<p>scheda</p>
<p>v pay</p>
<p>v-pay</p>
<p>visa</p>
<p>visa plus</p>
<p>visa electron</p>
<p>visto</p>
<p>visum</p>
<p>vpay</p></td>
<td><p>card identification number</p>
<p>card verification</p>
<p>cardi la verifica</p>
<p>cid</p>
<p>cod seg</p>
<p>cod seguranca</p>
<p>cod segurança</p>
<p>cod sicurezza</p>
<p>cod. seg</p>
<p>cod. seguranca</p>
<p>cod. segurança</p>
<p>cod. sicurezza</p>
<p>codice di sicurezza</p>
<p>codice di verifica</p>
<p>codigo</p>
<p>codigo de seguranca</p>
<p>codigo de segurança</p>
<p>crittogramma</p>
<p>cryptogram</p>
<p>cryptogramme</p>
<p>cv2</p>
<p>cvc</p>
<p>cvc2</p>
<p>cvn</p>
<p>cvv</p>
<p>cvv2</p>
<p>cód seguranca</p>
<p>cód segurança</p>
<p>cód. seguranca</p>
<p>cód. segurança</p>
<p>código</p>
<p>código de seguranca</p>
<p>código de segurança</p>
<p>de kaart controle</p>
<p>geeft nr uit</p>
<p>issue no</p>
<p>issue number</p>
<p>kaartidentificatienummer</p>
<p>kreditkartenprufnummer</p>
<p>kreditkartenprüfnummer</p>
<p>kwestieaantal</p>
<p>no. dell'edizione</p>
<p>no. di sicurezza</p>
<p>numero de securite</p>
<p>numero de verificacao</p>
<p>numero dell'edizione</p>
<p>numero di identificazione della</p>
<p>scheda</p>
<p>numero di sicurezza</p>
<p>numero van veiligheid</p>
<p>numéro de sécurité</p>
<p>nº autorizzazione</p>
<p>número de verificação</p>
<p>perno il blocco</p>
<p>pin block</p>
<p>prufziffer</p>
<p>prüfziffer</p>
<p>security code</p>
<p>security no</p>
<p>security number</p>
<p>sicherheits kode</p>
<p>sicherheitscode</p>
<p>sicherheitsnummer</p>
<p>speldblok</p>
<p>veiligheid 번호:</p>
<p>veiligheidsaantal</p>
<p>veiligheidscode</p>
<p>veiligheidsnummer</p>
<p>verfalldatum</p></td>
<td><p>ablauf</p>
<p>data de expiracao</p>
<p>data de expiração</p>
<p>data del exp</p>
<p>data di exp</p>
<p>data di scadenza</p>
<p>data em que expira</p>
<p>data scad</p>
<p>data scadenza</p>
<p>date de validité</p>
<p>datum afloop</p>
<p>datum van exp</p>
<p>de afloop</p>
<p>espira</p>
<p>espira</p>
<p>exp date</p>
<p>exp datum</p>
<p>expiration</p>
<p>만료</p>
<p>expires</p>
<p>expiry</p>
<p>fecha de expiracion</p>
<p>fecha de venc</p>
<p>gultig bis</p>
<p>gultigkeitsdatum</p>
<p>gültig bis</p>
<p>gültigkeitsdatum</p>
<p>la scadenza</p>
<p>scadenza</p>
<p>valable</p>
<p>validade</p>
<p>valido hasta</p>
<p>valor</p>
<p>venc</p>
<p>vencimento</p>
<p>vencimiento</p>
<p>verloopt</p>
<p>vervaldag</p>
<p>vervaldatum</p>
<p>vto</p>
<p>válido hasta</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 핀란드 국가 ID


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>세기를 나타내는 6자리 숫자와 문자, 3자리 숫자와 검사 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>패턴에는 다음이 모두 포함되어야 합니다.</p>
<ul>
<li><p>생년월일에 해당하는 DDMMYY 형식의 6자리 숫자</p></li>
<li><p>세기 표시('-', '+' 또는 'a')</p></li>
<li><p>3자리 개인 ID 번호</p></li>
<li><p>검사 숫자에 해당하는 1자리 숫자 또는 문자(대/소문자 구분 안 함)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_finnish_national_id</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_finnish_national_id</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Finnish National ID-->
<Entity id="338FD995-4CB5-4F87-AD35-79BD1DD926C1" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_finnish_national_id" />
          <Match idRef="Keyword_finnish_national_id" />
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-52"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_finnish_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sosiaaliturvatunnus</p>
<p>SOTU Henkilötunnus HETU</p>
<p>Personbeteckning</p>
<p>Personnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 핀란드 여권 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>9개의 문자와 숫자의 조합</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>9개의 문자와 숫자의 조합:</p>
<ul>
<li><p>2문자(대/소문자 구분 안 함)</p></li>
<li><p>7자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_finland_passport_number</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_finland_passport_number</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Finland Passport Number -->
<Entity id="d1685ac3-1d3a-40f8-8198-32ef5669c7a5" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_finland_passport_number"/>
     <Match idRef="Keyword_finland_passport_number"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-54"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_finland_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Passport</p>
<p>Passi</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 프랑스 운전 면허 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>12자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>비슷한 패턴(예: 프랑스 전화 번호)을 무시하기 위한 유효성 검사 기능을 포함하는 12자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_french_drivers_license</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>다음 중 하나 이상이 충족됩니다.</p>
<ul>
<li><p><code>Keyword_french_drivers_license</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Func_eu_date</code> 함수가 올바른 날짜 형식의 날짜를 찾습니다.</p></li>
</ul></li>
</ul>


```Command&nbsp;Line
<!-- France Driver's License Number -->
<Entity id="18e55a36-a01b-4b0f-943d-dc10282a1824" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_french_drivers_license" />
        <Any minMatches="1">
          <Match idRef="Keyword_french_drivers_license" />
          <Match idRef="Func_eu_date" />
        </Any>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-56"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_french_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>drivers licence</p>
<p>drivers license</p>
<p>driving licence</p>
<p>driving license</p>
<p>permis de conduire</p>
<p>licence number</p>
<p>license number</p>
<p>licence numbers</p>
<p>license numbers</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 프랑스 국가 ID 카드(CNI)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>12자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>12자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 65% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_france_cni</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- France CNI -->
<Entity id="f741ac74-1bc0-4665-b69b-f0c7f927c0c4" patternsProximity="300" recommendedConfidence="65">
  <Pattern confidenceLevel="65">
        <IdMatch idRef="Regex_france_cni" />
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><p>없음</p></td>
</tr>
</tbody>
</table>


## 프랑스 여권 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>9자리 숫자 및 문자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>9자리 숫자 및 문자:</p>
<ul>
<li><p>2자리 숫자</p></li>
<li><p>2문자(대/소문자 구분 안 함)</p></li>
<li><p>5자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_fr_passport</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_passport</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- France Passport Number -->
<Entity id="3008b884-8c8c-4cd8-a289-99f34fc7ff5d" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_fr_passport" />
        <Match idRef="Keyword_passport" />
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-59"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Passport Number</p>
<p>Passport No</p>
<p>Passport #</p>
<p>Passport#</p>
<p>PassportID</p>
<p>Passportno</p>
<p>passportnumber</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート ＃</p>
<p>Numéro de passeport</p>
<p>Passeport n °</p>
<p>Passeport Non</p>
<p>Passeport #</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 프랑스 사회 보장 번호(INSEE)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>15자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>다음 두 패턴 중 하나가 일치해야 합니다.</p>
<ul>
<li><p>13자리 숫자와 공백 1개, 2자리 숫자 또는</p></li>
<li><p>15자리 연속 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 95% 신뢰합니다.</p>
<ul>
<li><p><code>Func_french_insee</code> 또는 <code>Func_fr_insee</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_fr_insee</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_french_insee</code> 또는 <code>Func_fr_insee</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_fr_insee</code>의 키워드가 발견되지 않았습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- France INSEE -->
<Entity id="71f62b97-efe0-4aa1-aa49-e14de253619d" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="95">
        <IdMatch idRef="Func_french_insee" />
        <Match idRef="Func_fr_insee" />
        <Any minMatches="1">
          <Match idRef="Keyword_fr_insee" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_french_insee" />
        <Match idRef="Func_fr_insee" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_fr_insee" />
        </Any>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-61"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_fr_insee</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>insee</p>
<p>securité sociale</p>
<p>securite sociale</p>
<p>national id</p>
<p>national identification</p>
<p>numéro d'identité</p>
<p>no d'identité</p>
<p>no. d'identité</p>
<p>numero d'identite</p>
<p>no d'identite</p>
<p>no. d'identite</p>
<p>social security number</p>
<p>social security code</p>
<p>social insurance number</p>
<p>le numéro d'identification nationale</p>
<p>d'identité nationale</p>
<p>numéro de sécurité sociale</p>
<p>le code de la sécurité sociale</p>
<p>numéro d'assurance sociale</p>
<p>numéro de sécu</p>
<p>code sécu</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 독일 운전 면허 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>11자리 숫자와 문자 조합</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>11자리 숫자와 문자(대/소문자 구분 안 함):</p>
<ul>
<li><p>1자리 숫자 또는 문자</p></li>
<li><p>2자리 숫자</p></li>
<li><p>6자리 숫자 또는 문자</p></li>
<li><p>1자리 숫자</p></li>
<li><p>1자리 숫자 또는 문자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_german_drivers_license</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>다음 중 하나 이상이 충족됩니다.</p>
<ul>
<li><p><code>Keyword_german_drivers_license_number</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_german_drivers_license_collaborative</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_german_drivers_license</code>의 키워드가 발견되었습니다.</p></li>
</ul></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- German Driver's License Number -->
<Entity id="91da9335-1edb-45b7-a95f-5fe41a16c63c" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_german_drivers_license" />
        <Any minMatches="1">
          <Match idRef="Keyword_german_drivers_license_number" />
          <Match idRef="Keyword_german_drivers_license_collaborative" />
          <Match idRef="Keyword_german_drivers_license" />
        </Any>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-63"> </h3>
<div>
<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_german_drivers_license_number</p></th>
<th> </th>
<th><p>Keyword_german_drivers_license_collaborative</p></th>
<th><p>Keyword_german_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Führerschein</p>
<p>Fuhrerschein</p>
<p>Fuehrerschein</p>
<p>Führerscheinnummer</p>
<p>Fuhrerscheinnummer</p>
<p>Fuehrerscheinnummer</p>
<p>Führerschein-</p>
<p>Fuhrerschein-</p>
<p>Fuehrerschein-</p>
<p>FührerscheinnummerNr</p>
<p>FuhrerscheinnummerNr</p>
<p>FuehrerscheinnummerNr</p>
<p>FührerscheinnummerKlasse</p>
<p>FuhrerscheinnummerKlasse</p>
<p>FuehrerscheinnummerKlasse</p>
<p>Führerschein- Nr</p>
<p>Fuhrerschein- Nr</p>
<p>Fuehrerschein- Nr</p>
<p>Führerschein- Klasse</p>
<p>Fuhrerschein- Klasse</p>
<p>Fuehrerschein- Klasse</p>
<p>FührerscheinnummerNr</p>
<p>FuhrerscheinnummerNr</p>
<p>FuehrerscheinnummerNr</p>
<p>FührerscheinnummerKlasse</p>
<p>FuhrerscheinnummerKlasse</p>
<p>FuehrerscheinnummerKlasse</p>
<p>Führerschein- Nr</p>
<p>Fuhrerschein- Nr</p>
<p>Fuehrerschein- Nr</p>
<p>Führerschein- Klasse</p>
<p>Fuhrerschein- Klasse</p>
<p>Fuehrerschein- Klasse</p>
<p>DL</p>
<p>DLS</p>
<p>Driv Lic</p>
<p>Driv Licen</p>
<p>Driv License</p>
<p>Driv Licenses</p>
<p>Driv Licence</p>
<p>Driv Licences</p>
<p>Driv Lic</p>
<p>Driver Licen</p>
<p>Driver License</p>
<p>Driver Licenses</p>
<p>Driver Licence</p>
<p>Driver Licences</p>
<p>Drivers Lic</p>
<p>Drivers Licen</p>
<p>Drivers License</p>
<p>Drivers Licenses</p>
<p>Drivers Licence</p>
<p>Drivers Licences</p>
<p>Driver's Lic</p>
<p>Driver's Licen</p>
<p>Driver's License</p>
<p>Driver's Licenses</p>
<p>Driver's Licence</p>
<p>Driver's Licences</p>
<p>Driving Lic</p>
<p>Driving Licen</p>
<p>Driving License</p>
<p>Driving Licenses</p>
<p>Driving Licence</p>
<p>Driving Licences</p></td>
<td> </td>
<td><p>Nr-Führerschein</p>
<p>Nr-Fuhrerschein</p>
<p>Nr-Fuehrerschein</p>
<p>No-Führerschein</p>
<p>No-Fuhrerschein</p>
<p>No-Fuehrerschein</p>
<p>N-Führerschein</p>
<p>N-Fuhrerschein</p>
<p>N-Fuehrerschein</p>
<p>Nr-Führerschein</p>
<p>Nr-Fuhrerschein</p>
<p>Nr-Fuehrerschein</p>
<p>No-Führerschein</p>
<p>No-Fuhrerschein</p>
<p>No-Fuehrerschein</p>
<p>N-Führerschein</p>
<p>N-Fuhrerschein</p>
<p>N-Fuehrerschein</p></td>
<td><p>ausstellungsdatum</p>
<p>ausstellungsort</p>
<p>ausstellende behöde</p>
<p>ausstellende behorde</p>
<p>ausstellende behoerde</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 독일 ID 카드 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>2010년 11월 1일 이후</p>
<dl>
<dd><p>9개의 문자 및 숫자</p>
</dd>
</dl>
<p>1987년 4월 1일부터 2010년 10월 31일까지</p>
<dl>
<dd><p>10자리 숫자</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>2010년 11월 1일 이후:</p>
<ul>
<li><p>1개 문자(대/소문자 구분 안 함)</p></li>
<li><p>8자리 숫자</p></li>
</ul>
<p>1987년 4월 1일부터 2010년 10월 31일까지</p>
<ul>
<li><p>10자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 65% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_germany_id_card</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_germany_id_card</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Germany Identity Card Number -->
<Entity id="e577372f-c42e-47a0-9d85-bebed1c237d4" recommendedConfidence="65" patternsProximity="300">
  <Pattern confidenceLevel="65">
     <IdMatch idRef="Regex_germany_id_card"/>
     <Match idRef="Keyword_germany_id_card"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-65"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_germany_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Identity Card</p>
<p>ID</p>
<p>Identification</p>
<p>Personalausweis</p>
<p>Identifizierungsnummer</p>
<p>Ausweis</p>
<p>Identifikation</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 독일 여권 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>10자리 숫자 또는 문자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>패턴에는 다음이 모두 포함되어야 합니다.</p>
<ul>
<li><p>첫 번째 문자는 숫자 또는 (C, F, G, H, J, K) 집합의 문자임</p></li>
<li><p>3자리 숫자</p></li>
<li><p>5자리 숫자 또는 (C, -H, J-N, P, R, T, V-Z) 집합의 문자</p></li>
<li><p>1자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_german_passport</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>5개의 키워드 목록 중에 포함된 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_german_passport_data</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>5개의 키워드 목록 중에 포함된 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- German Passport Number -->
<Entity id="2e3da144-d42b-47ed-b123-fbf78604e52c" patternsProximity="300" recommendedConfidence="75">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_german_passport" />
        <Any minMatches="1">
          <Match idRef="Keyword_german_passport" />
          <Match idRef="Keyword_german_passport_collaborative" />
          <Match idRef="Keyword_german_passport_number" />
          <Match idRef="Keyword_german_passport1" />
          <Match idRef="Keyword_german_passport2" />
        </Any>
  </Pattern>
  <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_german_passport_data" />
        <Any minMatches="1">
          <Match idRef="Keyword_german_passport" />
          <Match idRef="Keyword_german_passport_collaborative" />
          <Match idRef="Keyword_german_passport_number" />
          <Match idRef="Keyword_german_passport1" />
          <Match idRef="Keyword_german_passport2" />
        </Any>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-67"> </h3>
<div>
<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_german_passport</p></th>
<th> </th>
<th><p>Keyword_german_passport_collaborative</p></th>
<th><p>Keyword_german_passport_number</p></th>
<th><p>Keyword_german_passport1</p></th>
<th><p>Keyword_german_passport2</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>reisepass</p>
<p>reisepasse</p>
<p>reisepassnummer</p>
<p>passport</p>
<p>passports</p></td>
<td> </td>
<td><p>geburtsdatum</p>
<p>ausstellungsdatum</p>
<p>ausstellungsort</p></td>
<td><p>No-Reisepass</p>
<p>Nr-Reisepass</p></td>
<td><p>Reisepass-Nr</p></td>
<td><p>bnationalit.t</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 그리스 국가 ID 카드


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>7-8자리 문자 및 숫자와 대시의 조합</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>7자리 문자 및 숫자(이전 형식):</p>
<ul>
<li><p>1개 문자(그리스어 알파벳의 임의 문자)</p></li>
<li><p>대시 1개</p></li>
<li><p>6자리 숫자</p></li>
</ul>
<p>8자리 문자와 숫자(새로운 형식):</p>
<ul>
<li><p>그리스어 및 라틴어 알파벳 둘 다에 해당 대문자가 포함된 2개 문자(ABEZHIKMNOPTYX)</p></li>
<li><p>대시 1개</p></li>
<li><p>6자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_greece_id_card</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_greece_id_card</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Greece National ID Card -->
<Entity id="82568215-1da1-46d3-874a-d2294d81b5ac" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_greece_id_card"/>
     <Match idRef="Keyword_greece_id_card"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-69"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_greece_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Greek identity Card</p>
<p>Tautotita</p>
<p>Δελτίο αστυνομικής ταυτότητας</p>
<p>Ταυτότητα</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## HKID(홍콩 ID 카드) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>8-9자리 문자 및 숫자와 마지막 문자를 선택적 괄호로 묶어서 조합</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>8-9자리 문자 조합:</p>
<ul>
<li><p>1-2개 문자(대/소문자 구분 안 함)</p></li>
<li><p>6자리 숫자</p></li>
<li><p>검사 숫자에 해당하고 선택적으로 괄호로 묶는 마지막 문자(임의 숫자 또는 문자 A)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_hong_kong_id_card</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_hong_kong_id_card</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 65% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_hong_kong_id_card</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Hong Kong Identity Card (HKID) number -->
<Entity id="e63c28a7-ad29-4c17-a41a-3d2a0b70fd9c" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_hong_kong_id_card"/>
     <Match idRef="Keyword_hong_kong_id_card"/>
  </Pattern>
  <Pattern confidenceLevel="65">
     <IdMatch idRef="Func_hong_kong_id_card"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-71"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_hong_kong_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Hong Kong Identity Card</p>
<p>HKID</p>
<p>ID card</p>
<p>香港身份證</p>
<p>香港永久性居民身份證</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 인도 PAN(영구 계정 번호)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>10자리 문자 또는 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10자리 문자 또는 숫자:</p>
<ul>
<li><p>5개 문자(대/소문자 구분 안 함)</p></li>
<li><p>4자리 숫자</p></li>
<li><p>알파벳 검사 숫자에 해당하는 문자 1개</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_india_permanent_account_number</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_india_permanent_account_number</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- India Permanent Account Number -->
<Entity id="2602bfee-9bb0-47a5-a7a6-2bf3053e2804" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_india_permanent_account_number"/>
     <Match idRef="Keyword_india_permanent_account_number"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-73"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_india_permanent_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Permanent Account Number</p>
<p>PAN</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 인도 고유 ID(Aadhaar) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>선택적 공백 또는 대시를 포함하는 12자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>12자리 숫자:</p>
<ul>
<li><p>4자리 숫자</p></li>
<li><p>선택적 공백 또는 대시</p></li>
<li><p>4자리 숫자</p></li>
<li><p>선택적 공백 또는 대시</p></li>
<li><p>검사 숫자에 해당하는 마지막 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_india_aadhaar</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_india_aadhar</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_india_aadhaar</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- India Unique Identification (Aadhaar) number -->
<Entity id="1ca46b29-76f5-4f46-9383-cfa15e91048f" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_india_aadhaar"/>
     <Match idRef="Keyword_india_aadhar"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_india_aadhaar"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-75"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_india_aadhar</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aadhar</p>
<p>Aadhaar</p>
<p>UID</p>
<p>आधार</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 인도네시아 ID 카드(KTP) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>선택적으로 마침표를 포함하는 16자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>16자리 숫자:</p>
<ul>
<li><p>2자리 시/도 코드</p></li>
<li><p>마침표(옵션)</p></li>
<li><p>2자리 지역 또는 구/군/시 코드</p></li>
<li><p>2자리 소구역 코드</p></li>
<li><p>마침표(옵션)</p></li>
<li><p>생년월일에 해당하는 DDMMYY 형식의 6자리 숫자</p></li>
<li><p>마침표(옵션)</p></li>
<li><p>4자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_indonesia_id_card</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_indonesia_id_card</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_indonesia_id_card</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Indonesia Identity Card (KTP) Number -->
<Entity id="da68fdb0-f383-4981-8c86-82689d3b7d55" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_indonesia_id_card"/>
     <Match idRef="Keyword_indonesia_id_card"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_indonesia_id_card"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-77"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_indonesia_id_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KTP</p>
<p>Kartu Tanda Penduduk</p>
<p>Nomor Induk Kependudukan</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## IBAN(국제 은행 계좌 번호)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>국가 코드 (처음 두) 더하기 bban 번호 (최대 30 개의 문자) plus 자리 숫자 (두 자리 숫자) 확인</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>패턴에는 다음이 모두 포함되어야 합니다.</p>
<ul>
<li><p>두 문자로 된 국가 코드</p></li>
<li><p>두 검사 자리 숫자 (선택 사항 공간을 앞에 오는)</p></li>
<li><p>1-7 그룹 4 개의 문자 또는 숫자 (공백으로 구분 수)</p></li>
<li><p>1-3 문자 또는 숫자</p></li>
</ul>
<p>각 국가 대 한 형식은 약간 다릅니다. IBAN 중요 한 정보 유형에서는 이러한 60 국가 설명 합니다.</p>
<dl>
<dd><p>ad, ae, a에서에서 달리 ba, 배경, bh, 채널, cr, cy, cz, de, 진한, do, ee, es, 무선, 중, fr, gb, ge, gi, gl가, hr, 될 hu, 즉, 일리노이은 그, kw, kz, 파운드, li, lt, lu, lv, mc, md, me, mk, mr, 체, 뮤 nl, 아니요 pl, pt, 되는, rs, sa, se, si, sk, sm, 조지아 주, tr, vg</p>
</dd>
</dl></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_iban</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<Entity id="e7dc4711-11b7-4cb0-b88b-2c394a771f0e" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_iban" />
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><p>없음</p></td>
</tr>
</tbody>
</table>


## IP 주소


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>IPv4:</p>
<ul>
<li><p>IPv4 주소의 서식 있는 버전(마침표 있음) 및 서식 없는 버전(마침표 없음)으로 구성된 복잡한 패턴</p></li>
</ul>
<p>IPv6:</p>
<ul>
<li><p>서식 있는(콜론 포함) IPv6 번호로 구성된 복잡한 패턴</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>IPv6의 경우 DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_ipv6_address</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_ipaddress</code>의 키워드가 발견되지 않았습니다.</p></li>
</ul>
<p>IPv4의 경우 DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 95% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_ipv4_address</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_ipaddress</code>의 키워드가 발견되었습니다.</p></li>
</ul>
<p>IPv6의 경우 DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 95% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_ipv6_address</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_ipaddress</code>의 키워드가 발견되지 않았습니다.</p></li>
</ul>


```Command&nbsp;Line  
    <!-- IP Address -->
    <Entity id="1daa4ad5-e2dd-4ca4-a788-54722c09efb2" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_ipv6_address" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_ipaddress" />
        </Any>
      </Pattern>
      <Pattern confidenceLevel="95">
        <IdMatch idRef="Regex_ipv4_address" />
        <Any minMatches="1">
          <Match idRef="Keyword_ipaddress" />
        </Any>
      </Pattern>
      <Pattern confidenceLevel="95">
        <IdMatch idRef="Regex_ipv6_address" />
        <Any minMatches="1">
          <Match idRef="Keyword_ipaddress" />
        </Any>
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-80"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ipaddress</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IP(이 키워드는 대/소문자를 구분함)</p>
<p>ip address</p>
<p>ip addresses</p>
<p>internet protocol</p>
<p>IP-כתובת ה</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 아일랜드 PPS(개인 공공 서비스) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>이전 형식(2012년 12월 31일까지)</p>
<dl>
<dd><p>7자리 숫자와 1-2개 문자</p>
</dd>
</dl>
<p>새 형식(2013년 1월 1일 이후)</p>
<dl>
<dd><p>7자리 숫자와 2개 문자</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>이전 형식(2012년 12월 31일까지)</p>
<ul>
<li><p>7자리 숫자</p></li>
<li><p>1-2개 문자(대/소문자 구분 안 함)</p></li>
</ul>
<p>새 형식(2013년 1월 1일 이후)</p>
<ul>
<li><p>7자리 숫자</p></li>
<li><p>알파벳 검사 숫자에 해당하는 문자 1개(대/소문자 구분 안 함)</p></li>
<li><p>문자 "A" 또는 "H"(대/소문자 구분 안 함)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_ireland_pps</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>다음 중 하나가 충족됩니다.</p>
<ul>
<li><p><code>Keyword_ireland_pps</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p><code>Func_eu_date</code> 함수가 올바른 날짜 형식의 날짜를 찾습니다.</p></li>
</ul></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 65% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_ireland_pps</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Ireland Personal Public Service (PPS) Number -->
<Entity id="1cdb674d-c19a-4fcf-9f4b-7f56cc87345a" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_ireland_pps"/>
     <Any minMatches="1">
  <Match idRef="Keyword_ireland_pps"/>
  <Match idRef="Func_eu_date"/>
     </Any>
  </Pattern>
  <Pattern confidenceLevel="65">
     <IdMatch idRef="Func_ireland_pps"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-82"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ireland_pps</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Personal Public Service Number</p>
<p>PPS Number</p>
<p>PPS Num</p>
<p>PPS No.</p>
<p>PPS #</p>
<p>PPS#</p>
<p>PPSN</p>
<p>Public Services Card</p>
<p>Uimhir Phearsanta Seirbhíse Poiblí</p>
<p>Uimh. PSP</p>
<p>PSP</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 이스라엘 은행 계좌 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>13자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>서식 있음:</p>
<ul>
<li><p>2자리 숫자</p></li>
<li><p>대시 1개</p></li>
<li><p>3자리 숫자</p></li>
<li><p>대시 1개</p></li>
<li><p>8자리 숫자</p></li>
</ul>
<p>서식 없음:</p>
<ul>
<li><p>13자리 연속 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_israel_bank_account_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_israel_bank_account_number</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Israel Bank Account Number -->
<Entity id="7d08b2ff-a0b9-437f-957c-aeddbf9b2b25" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_israel_bank_account_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_israel_bank_account_number" />
        </Any>
    </Pattern>
</Entity>

```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-84"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_israel_bank_account_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bank Account Number</p>
<p>Bank Account</p>
<p>Account Number</p>
<p>מספר חשבון בנק</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 이스라엘 국가 ID


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>9자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>9자리 연속 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_israeli_national_id_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_Israel_National_ID</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Israel National ID Number -->
<Entity id="e05881f5-1db1-418c-89aa-a3ac5c5277ee" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_israeli_national_id_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_Israel_National_ID" />
        </Any>
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-86"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_Israel_National_ID</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>מספר זהות</p>
<p>National ID Number</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 이탈리아 운전 면허 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>10개의 문자 및 숫자 조합</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10개의 문자 및 숫자 조합:</p>
<ul>
<li><p>1개 문자(대/소문자 구분 안 함)</p></li>
<li><p>문자 "A" 또는 "V"(대/소문자 구분 안 함)</p></li>
<li><p>7개 문자(대/소문자 구분 안 함), 숫자 또는 밑줄 문자</p></li>
<li><p>1개 문자(대/소문자 구분 안 함)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_italy_drivers_license_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_italy_drivers_license_number</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Italy Driver's license Number -->
<Entity id="97d6244f-9157-41bd-8e0c-9d669a5c4d71" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_italy_drivers_license_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_italy_drivers_license_number" />
        </Any>
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-88"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_italy_drivers_license_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>numero di patente di guida</p>
<p>patente di guida</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 일본 은행 계좌 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>7 또는 8자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>은행 계좌 번호:</p>
<ul>
<li><p>7 또는 8자리 숫자</p></li>
</ul>
<p>은행 계좌 지점 코드:</p>
<ul>
<li><p>4자리 숫자</p></li>
<li><p>공백 또는 대시(선택 사항)</p></li>
<li><p>3자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_jp_bank_account</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_jp_bank_account</code>의 키워드가 발견되었습니다.</p></li>
<li><p>다음 중 하나가 충족됩니다.</p>
<ul>
<li><p><code>Func_jp_bank_account_branch_code</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_jp_bank_branch_code</code>의 키워드가 발견되었습니다.</p></li>
</ul></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_jp_bank_account</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_jp_bank_account</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Japan Bank Account Number -->
<Entity id="d354f95b-96ee-4b80-80bc-4377312b55bc" patternsProximity="300" recommendedConfidence="75">
  <Version minEngineVersion="15.01.0131.000">
    <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_jp_bank_account" />
          <Match idRef="Keyword_jp_bank_account" />
          <Any minMatches="1">
            <Match idRef="Func_jp_bank_account_branch_code" />
            <Match idRef="Keyword_jp_bank_branch_code" />
          </Any>
      </Pattern>
  </Version>    
     <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_bank_account" />
        <Match idRef="Keyword_jp_bank_account" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-90"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_bank_account</p></th>
<th> </th>
<th><p>Keyword_jp_bank_branch_code</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Checking Account Number</p>
<p>Checking Account</p>
<p>Checking Account #</p>
<p>Checking Acct Number</p>
<p>Checking Acct #</p>
<p>Checking Acct No.</p>
<p>Checking Account No.</p>
<p>Bank Account Number</p>
<p>Bank Account</p>
<p>Bank Account #</p>
<p>Bank Acct Number</p>
<p>Bank Acct #</p>
<p>Bank Acct No.</p>
<p>Bank Account No.</p>
<p>Savings Account Number</p>
<p>Savings Account</p>
<p>Savings Account #</p>
<p>Savings Acct Number</p>
<p>Savings Acct #</p>
<p>Savings Acct No.</p>
<p>Savings Account No.</p>
<p>Debit Account Number</p>
<p>Debit Account</p>
<p>Debit Account #</p>
<p>Debit Acct Number</p>
<p>Debit Acct #</p>
<p>Debit Acct No.</p>
<p>Debit Account No.</p>
<p>口座番号を当座預金口座の確認</p>
<p># アカウントの確認、勘定番号の確認</p>
<p>#勘定の確認</p>
<p>勘定番号の確認</p>
<p>口座番号の確認</p>
<p>銀行口座番号</p>
<p>銀行口座</p>
<p>銀行口座 #</p>
<p>銀行の勘定番号</p>
<p>銀行のacct #</p>
<p>銀行の勘定いいえ</p>
<p>銀行口座番号</p>
<p>普通預金口座番号</p>
<p>預金口座</p>
<p>貯蓄口座 #</p>
<p>貯蓄勘定の数</p>
<p>貯蓄勘定 #</p>
<p>貯蓄勘定番号</p>
<p>普通預金口座番号</p>
<p>引き落とし口座番号</p>
<p>口座番号</p>
<p>口座番号 #</p>
<p>デビットのacct番号</p>
<p>デビット勘定 #</p>
<p>デビットACCTの番号</p>
<p>デビット口座番号</p></td>
<td> </td>
<td><p>Otemachi</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 일본 운전 면허 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>12자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>12자리 연속 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_jp_drivers_license_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_jp_drivers_license_number</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Japan Driver's License Number -->
<Entity id="c6011143-d087-451c-8313-7f6d4aed2270" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_drivers_license_number" />
        <Match idRef ="Keyword_jp_drivers_license_number" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-92"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_drivers_license_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>드라이버 라이선스</p>
<p>운전 면허</p>
<p>드라이버의 라이선스</p>
<p>드라이버 라이선스</p>
<p>드라이버의 라이선스</p>
<p>드라이버 라이선스</p>
<p>dl #</p>
<p>dl #</p>
<p>lic #</p>
<p>lics #</p>
<p>運転免許証</p>
<p>運転免許</p>
<p>免許証</p>
<p>免許</p>
<p>運転免許証番号</p>
<p>運転免許番号</p>
<p>免許証番号</p>
<p>免許番号</p>
<p>運転免許証ナンバー</p>
<p>運転免許ナンバー</p>
<p>免許証ナンバー</p>
<p>運転免許証No 합니다.</p>
<p>運転免許No 합니다.</p>
<p>免許証No 합니다.</p>
<p>免許No 합니다.</p>
<p>運転免許証 #</p>
<p>運転免許 #</p>
<p>免許証 #</p>
<p>免許 #</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 일본 여권 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>2개 문자와 7자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>2개의 문자(대/소문자 구분 안 함)와 7자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_jp_passport</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_jp_passport</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Japan Passport Number -->
<Entity id="75177310-1a09-4613-bf6d-833aae3743f8" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_passport" />
        <Match idRef="Keyword_jp_passport" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-94"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート #</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 일본 주민 등록 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>11자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>11자리 연속 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_jp_resident_registration_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_jp_resident_registration_number</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Japan Resident Registration Number -->
<Entity id="01c1209b-6389-4faf-a5f8-3f7e13899652" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_resident_registration_number" />
        <Match idRef ="Keyword_jp_resident_registration_number" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-96"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_resident_registration_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Resident Registration Number</p>
<p>Resident Register Number</p>
<p>Residents Basic Registry Number</p>
<p>Resident Registration No.</p>
<p>Resident Register No.</p>
<p>Residents Basic Registry No.</p>
<p>Basic Resident Register No.</p>
<p>住民登録番号、登録番号をレジデント</p>
<p>住民基本登録番号、登録番号</p>
<p>住民基本レジストリ番号を常駐</p>
<p>登録番号を常駐住民基本台帳登録番号</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 일본 SIN(사회 보험 번호)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>7-12자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>7-12자리 숫자:</p>
<ul>
<li><p>4자리 숫자</p></li>
<li><p>하이픈 1개(선택 사항)</p></li>
<li><p>6자리 숫자</p></li>
<li><p>또는</p></li>
<li><p>7-12자리 연속 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_jp_sin</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_jp_sin</code>의 키워드가 발견되었습니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_jp_sin_pre_1997</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_jp_sin</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Japan Social Insurance Number -->
<Entity id="c840e719-0896-45bb-84fd-1ed5c95e45ff" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_jp_sin" />
        <Match idRef="Keyword_jp_sin" />
    </Pattern>
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_jp_sin_pre_1997" />
        <Match idRef="Keyword_jp_sin" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-98"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_jp_sin</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Social Insurance No.</p>
<p>Social Insurance Num</p>
<p>Social Insurance Number</p>
<p>社会保険のテンキー</p>
<p>社会保険番号</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 말레이시아 ID 카드 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>선택적으로 하이픈을 포함하는 12자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>12자리 숫자:</p>
<ul>
<li><p>생년월일에 해당하는 YYMMDD 형식의 6자리 숫자</p></li>
<li><p>대시(옵션)</p></li>
<li><p>2개 문자로 이루어진 출생지 코드</p></li>
<li><p>대시(옵션)</p></li>
<li><p>임의의 3자리 숫자</p></li>
<li><p>1자리 성별 코드</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_malaysia_id_card_number</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_malaysia_id_card_number</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Malaysia ID Card Number -->
</Entity>
      <Entity id="7f0e921c-9677-435b-aba2-bb8f1013c749" patternsProximity="300" recommendedConfidence="85">
        <Pattern confidenceLevel="85">
            <IdMatch idRef="Regex_malaysia_id_card_number" />
            <Match idRef="Keyword_malaysia_id_card_number" />
        </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-100"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_malaysia_id_card_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyKad</p>
<p>Identity Card</p>
<p>ID Card</p>
<p>Identification Card</p>
<p>Digital Application Card</p>
<p>Kad Akuan Diri</p>
<p>Kad Aplikasi Digital</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 네덜란드 시민 서비스(BSN) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>선택적으로 공백을 포함하는 8-9자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>8-9자리 숫자:</p>
<ul>
<li><p>3자리 숫자</p></li>
<li><p>공백 1개(선택 사항)</p></li>
<li><p>3자리 숫자</p></li>
<li><p>공백 1개(선택 사항)</p></li>
<li><p>2-3자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_netherlands_bsn</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_netherlands_bsn</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p><code>Func_eu_date2</code> 함수가 올바른 날짜 형식의 날짜를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Netherlands Citizen&#39;s Service (BSN) Number -->
<Entity id="c5f54253-ef7e-44f6-a578-440ed67e946d" patternsProximity="300" recommendedConfidence="85">
  <Pattern confidenceLevel="85">
       <IdMatch idRef="Func_netherlands_bsn" /> 
       <Match idRef="Keyword_netherlands_bsn" /> 
       <Match idRef="Func_eu_date2" /> 
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-102"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_netherlands_bsn</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Citizen service number</p>
<p>BSN</p>
<p>Burgerservicenummer</p>
<p>Sofinummer</p>
<p>Persoonsgebonden nummer</p>
<p>Persoonsnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 뉴질랜드 보건부 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>3개 문자, 공백 1개(선택 사항) 및 4자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>3개 문자(대/소문자 구분 안 함), 공백 1개(선택 사항), 4자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_new_zealand_ministry_of_health_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_nz_terms</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- New Zealand Health Number -->
<Entity id="2b71c1c8-d14e-4430-82dc-fd1ed6bf05c7" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_new_zealand_ministry_of_health_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_nz_terms" />
        </Any>
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-104"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_nz_terms</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NHI</p>
<p>New Zealand</p>
<p>Health</p>
<p>treatment</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## Norway Identification Number


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>11자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>11자리 숫자:</p>
<ul>
<li><p>생년월일에 해당하는 DDMMYY 형식의 6자리 숫자</p></li>
<li><p>3자리 개인 번호</p></li>
<li><p>2개의 검사 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_norway_id_number</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_norway_id_number</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_norway_id_numbe</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Norway Identification Number -->
<Entity id="d4c8a798-e9f2-4bd3-9652-500d24080fc3" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_norway_id_number"/>
     <Match idRef="Keyword_norway_id_number"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_norway_id_number"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-106"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_norway_id_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Personal identification number</p>
<p>Norwegian ID Number</p>
<p>ID Number</p>
<p>Identification</p>
<p>Personnummer</p>
<p>Fødselsnummer</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 필리핀 통합 다목적 ID 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>하이픈으로 구분된 12자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>12자리 숫자:</p>
<ul>
<li><p>4자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>7자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>1자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_philippines_unified_id</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_philippines_id</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Philippines Unified Multi-Purpose ID number -->
<Entity id="019b39dd-8c25-4765-91a3-d9c6baf3c3b3" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_philippines_unified_id"/>
     <Match idRef="Keyword_philippines_id"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-108"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_philippines_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Unified Multi-Purpose ID</p>
<p>UMID</p>
<p>Identity Card</p>
<p>Pinag-isang Multi-Layunin ID</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 폴란드 ID 카드


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>3개의 문자 및 6자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>3개의 문자(대/소문자 구분 안 함)와 6자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_polish_national_id</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_polish_national_id_passport_number</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Poland Identity Card-->
<Entity id="25E64989-ED5D-40CA-A939-6C14183BB7BF" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_polish_national_id" />
          <Match idRef="Keyword_polish_national_id_passport_number" />
      </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-110"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_polish_national_id_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nazwa i nr dowodu tożsamości</p>
<p>Dowód Tożsamości</p>
<p>dow. os.</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 폴란드 국가 ID(PESEL)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>11자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>11자리 연속 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_pesel_identification_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_pesel_identification_number</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Poland National ID (PESEL) -->      
<Entity id="E3AAF206-4297-412F-9E06-BA8487E22456" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_pesel_identification_number" />
          <Match idRef="Keyword_pesel_identification_number" />
      </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-112"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_pesel_identification_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nr PESEL</p>
<p>PESEL</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 폴란드 여권


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>2개 문자와 7자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>2개의 문자(대/소문자 구분 안 함)와 7자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_polish_passport_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_polish_national_id_passport_number</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Poland Passport Number -->
<Entity id="03937FB5-D2B6-4487-B61F-0F8BFF7C3517" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_polish_passport_number" />
          <Match idRef="Keyword_polish_national_id_passport_number" />
      </Pattern>
</Entity>
</Version>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-114"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_polish_national_id_passport_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nazwa i nr dowodu tożsamości</p>
<p>Dowód Tożsamości</p>
<p>dow. os.</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 포르투갈 시민 카드 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>8자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>8자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_portugal_citizen_card</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_portugal_citizen_card</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Portugal Citizen Card Number -->
<Entity id="91a7ece2-add4-4986-9a15-c84544d81ecd" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_portugal_citizen_card"/>
     <Match idRef="Keyword_portugal_citizen_card"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-116"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_portugal_citizen_card</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Citizen Card</p>
<p>National ID Card</p>
<p>CC</p>
<p>Cartão de Cidadão</p>
<p>Bilhete de Identidade</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 사우디 아라비아 국가 ID


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>10자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10자리 연속 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_saudi_arabia_national_id</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_saudi_arabia_national_id</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Saudi Arabia National ID -->
<Entity id="8c5a0ba8-404a-41a3-8871-746aa21ee6c0" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_saudi_arabia_national_id" />
        <Any minMatches="1">
          <Match idRef="Keyword_saudi_arabia_national_id" />
        </Any>
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-118"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_saudi_arabia_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Identification Card</p>
<p>I card number</p>
<p>ID number</p>
<p>الوطنية الهوية بطاقة رقم</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 싱가포르 NRIC(국가 등록 ID 카드) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>9개의 문자 및 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>9개의 문자 및 숫자:</p>
<ul>
<li><p>문자 "F", "G", "S" 또는 "T"(대/소문자 구분 안 함)</p></li>
<li><p>7자리 숫자</p></li>
<li><p>알파벳 검사 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_singapore_nric</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_singapore_nric</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_singapore_nric</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Singapore National Registration Identity Card (NRIC) Number -->
<Entity id="cead390a-dd83-4856-9751-fb6dc98c34da" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Regex_singapore_nric"/>
     <Match idRef="Keyword_singapore_nric"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_singapore_nric"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-120"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_singapore_nric</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>National Registration Identity Card</p>
<p>Identity Card Number</p>
<p>NRIC</p>
<p>IC</p>
<p>Foreign Identification Number</p>
<p>FIN</p>
<p>身份证</p>
<p>身份證</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 남아프리카 공화국 식별 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>공백을 포함할 수 있는 13자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>13자리 숫자:</p>
<ul>
<li><p>생년월일에 해당하는 YYMMDD 형식의 6자리 숫자</p></li>
<li><p>4자리 숫자</p></li>
<li><p>1자리 시민권 표시</p></li>
<li><p>숫자 "8" 또는 "9"</p></li>
<li><p>체크섬 숫자에 해당하는 1자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_south_africa_identification_number</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_south_africa_identification_number</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- South Africa Identification Number -->
<Entity id="e2adf7cb-8ea6-4048-a2ed-d89eb65f2780" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_south_africa_identification_number"/>
     <Match idRef="Keyword_south_africa_identification_number"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-122"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_south_africa_identification_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Identity card</p>
<p>ID</p>
<p>Identification</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 한국 주민 등록 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>하이픈을 포함하는 13자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>13자리 숫자:</p>
<ul>
<li><p>생년월일에 해당하는 YYMMDD 형식의 6자리 숫자</p></li>
<li><p>하이픈</p></li>
<li><p>세기 및 성별에 따라 결정되는 1자리 숫자</p></li>
<li><p>4자리 출생 지역 코드</p></li>
<li><p>앞 번호가 동일한 사람을 구분하기 위해 사용되는 1자리 숫자</p></li>
<li><p>검사 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_south_korea_resident_number</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_south_korea_resident_number</code> 에서 키워드를 발견 됩니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_south_korea_resident_number</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- South Korea Resident Registration Number -->
<Entity id="5b802e18-ba80-44c4-bc83-bf2ad36ae36a" recommendedConfidence="85" patternsProximity="300">
  <Pattern confidenceLevel="85">
     <IdMatch idRef="Func_south_korea_resident_number"/>
     <Match idRef="Keyword_south_korea_resident_number"/>
  </Pattern>
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Func_south_korea_resident_number"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-124"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_south_korea_resident_number</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>National ID card</p>
<p>Citizen's Registration Number</p>
<p>Jumin deungnok beonho</p>
<p>RRN</p>
<p>주민등록번호</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 스페인 SSN(사회 보장 번호)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>11-12자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>11-12자리 숫자:</p>
<ul>
<li><p>2자리 숫자</p></li>
<li><p>정방향 슬래시 1개(선택 사항)</p></li>
<li><p>7-8자리 숫자</p></li>
<li><p>정방향 슬래시 1개(선택 사항)</p></li>
<li><p>2자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_spanish_social_security_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Spain SSN -->
<Entity id="5df987c0-8eae-4bce-ace7-b316347f3070" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_spanish_social_security_number" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><p>없음</p></td>
</tr>
</tbody>
</table>


## 스웨덴 국가 ID


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>10 또는 12자리 숫자와 선택적 구분 기호</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10 또는 12자리 숫자와 선택적 구분 기호:</p>
<ul>
<li><p>2-4자리 숫자(선택 사항)</p></li>
<li><p>YYMMDD 날짜 형식의 6자리 숫자</p></li>
<li><p>구분 기호 "-" 또는 "+"(선택 사항) 및</p></li>
<li><p>4자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_swedish_national_identifier</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Sweden National ID -->
<Entity id="f69aaf40-79be-4fac-8f05-fd1910d272c8" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_swedish_national_identifier" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><p>없음</p></td>
</tr>
</tbody>
</table>


## 스웨덴 여권 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>8자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>8자리 연속 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_sweden_passport_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>다음 중 하나가 충족됩니다.</p>
<ul>
<li><p><code>Keyword_passport</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_sweden_passport</code>의 키워드가 발견되었습니다.</p></li>
</ul></li>
</ul>


```Command&nbsp;Line
<!-- Sweden Passport Number -->
<Entity id="ba4e7456-55a9-4d89-9140-c33673553526" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_sweden_passport_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_passport" />
          <Match idRef="Keyword_sweden_passport" />
        </Any>
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-128"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_sweden_passport</p></th>
<th> </th>
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>visa requirements</p>
<p>Alien Registration Card</p>
<p>Schengen visas</p>
<p>Schengen visa</p>
<p>Visa Processing</p>
<p>Visa Type</p>
<p>Single Entry</p>
<p>Multiple Entry</p>
<p>G3 Processing Fees</p></td>
<td> </td>
<td><p>Passport Number</p>
<p>Passport No</p>
<p>Passport #</p>
<p>Passport#</p>
<p>PassportID</p>
<p>Passportno</p>
<p>passportnumber</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n °</p>
<p>Passeport Non</p>
<p>Passeport #</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## SWIFT 코드


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>4개의 문자, 5-31개 문자 또는 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>4개의 문자, 5-31개 문자 또는 숫자:</p>
<ul>
<li><p>4문자 은행 코드(대/소문자 구분 안 함)</p></li>
<li><p>선택적 공백 1개</p></li>
<li><p>4-28개 문자 또는 숫자[BBAN(기본 은행 계좌 번호)]</p></li>
<li><p>선택적 공백 1개</p></li>
<li><p>1-3개 문자 또는 숫자(BBAN의 나머지)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_swift</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_swift</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<Entity id="cb2ab58c-9cb8-4c81-baf8-a4e106791df4" patternsProximity="300" recommendedConfidence="75">
<Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_swift" />
        <Match idRef="Keyword_swift" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-130"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_swift</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>international organization for standardization 9362</p>
<p>iso 9362</p>
<p>iso9362</p>
<p>swift#</p>
<p>swiftcode</p>
<p>swiftnumber</p>
<p>swiftroutingnumber</p>
<p>swift code</p>
<p>swift number #</p>
<p>swift routing number</p>
<p>bic number</p>
<p>bic code</p>
<p>bic #</p>
<p>bic#</p>
<p>bank identifier code</p>
<p>標準化9362</p>
<p>迅速＃</p>
<p>SWIFTコード</p>
<p>SWIFT番号</p>
<p>迅速なルーティング番号</p>
<p>BIC番号</p>
<p>BICコード</p>
<p>銀行識別コードのための国際組織</p>
<p>Organisation internationale de normalisation 9362</p>
<p>rapide #</p>
<p>code SWIFT</p>
<p>le numéro de swift</p>
<p>swift numéro d'acheminement</p>
<p>le numéro BIC</p>
<p># BIC</p>
<p>code identificateur de banque</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 대만 국가 ID


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>1개의 문자, 9자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>1개의 문자, 9자리 숫자:</p>
<ul>
<li><p>1개 문자(영문, 대/소문자 구분 안 함)</p></li>
<li><p>숫자 "1" 또는 "2"</p></li>
<li><p>8자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_taiwanese_national_id</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_taiwanese_national_id</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Taiwanese National ID -->
<Entity id="4C7BFC34-8DD1-421D-8FB7-6C6182C2AF03" patternsProximity="300" recommendedConfidence="85">
      <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_taiwanese_national_id" />
          <Match idRef="Keyword_taiwanese_national_id" />
      </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-132"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_taiwanese_national_id</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>身份證字號</p>
<p>身份證</p>
<p>身份證號碼</p>
<p>身份證號</p>
<p>身分證字號</p>
<p>身分證</p>
<p>身分證號碼</p>
<p>身份證號</p>
<p>身分證統一編號</p>
<p>國民身分證統一編號</p>
<p>簽名</p>
<p>蓋章</p>
<p>簽名或蓋章</p>
<p>簽章</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 대만 여권 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>생체 인식 여권 번호</p>
<dl>
<dd><p>9자리 숫자</p>
</dd>
</dl>
<p>비-생체 인식 여권 번호</p>
<dl>
<dd><p>9자리 숫자</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>생체 인식 여권 번호</p>
<ul>
<li><p>숫자 "3"</p></li>
<li><p>8자리 숫자</p></li>
</ul>
<p>비-생체 인식 여권 번호</p>
<ul>
<li><p>9자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_taiwan_passport</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_taiwan_passport</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Taiwan Passport Number -->
<Entity id="e7251cb4-4c2c-41df-963e-924eb3dae04a" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_taiwan_passport"/>
     <Match idRef="Keyword_taiwan_passport"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-134"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_taiwan_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ROC passport number</p>
<p>Passport number</p>
<p>Passport no</p>
<p>Passport Num</p>
<p>Passport #</p>
<p>护照</p>
<p>中華民國護照</p>
<p>Zhōnghuá Mínguó hùzhào</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 대만 거주 인증(ARC/TARC) 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>10개의 문자 및 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10개의 문자 및 숫자:</p>
<ul>
<li><p>2문자(대/소문자 구분 안 함)</p></li>
<li><p>8자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_taiwan_resident_certificate</code> 정규식 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_taiwan_resident_certificate</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- Taiwan Resident Certificate (ARC/TARC) -->
<Entity id="48269fec-05ea-46ea-b326-f5623a58c6e9" recommendedConfidence="75" patternsProximity="300">
  <Pattern confidenceLevel="75">
     <IdMatch idRef="Regex_taiwan_resident_certificate"/>
     <Match idRef="Keyword_taiwan_resident_certificate"/>
  </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-136"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_taiwan_resident_certificate</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Resident Certificate</p>
<p>Resident Cert</p>
<p>Resident Cert.</p>
<p>Identification card</p>
<p>Alien Resident Certificate</p>
<p>ARC</p>
<p>Taiwan Area Resident Certificate</p>
<p>TARC</p>
<p>居留證</p>
<p>外僑居留證</p>
<p>台灣地區居留證</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 영국 운전 면허 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>지정된 형식의 18개 문자 및 숫자 조합</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>18개의 문자 및 숫자:</p>
<ul>
<li><p>5개 문자(대/소문자 구분 안 함) 또는 문자 대신 숫자 "9" 사용</p></li>
<li><p>1자리 숫자</p></li>
<li><p>생년월일에 대한 DDMMY 날짜 형식의 5자리 숫자</p></li>
<li><p>2개 문자(대/소문자 구분 안 함) 또는 문자 대신 숫자 "9" 사용</p></li>
<li><p>5자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_uk_drivers_license</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_uk_drivers_license</code>의 키워드가 발견되었습니다.</p></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- U.K. Driver&#39;s License Number -->
<Entity id="f93de4be-d94c-40df-a8be-461738047551" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_uk_drivers_license" />
        <Match idRef="Keyword_uk_drivers_license" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-138"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_drivers_license</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DVLA</p>
<p>light vans</p>
<p>quadbikes</p>
<p>motor cars</p>
<p>125cc</p>
<p>sidecar</p>
<p>tricycles</p>
<p>motorcycles</p>
<p>photocard licence</p>
<p>learner drivers</p>
<p>licence holder</p>
<p>licence holders</p>
<p>driving licences</p>
<p>driving licence</p>
<p>dual control car</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 영국 선거 롤 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>2개의 문자, 1-4자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>2개의 문자(대/소문자 구분 안 함)와 1-4자리 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_uk_electoral</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_uk_electoral</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- U.K. Electoral Number -->
<Entity id="a3eea206-dc0c-4f06-9e22-aa1be3059963" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_uk_electoral" />
        <Any minMatches="1">
          <Match idRef="Keyword_uk_electoral" />
        </Any>
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-140"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_electoral</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>council nomination</p>
<p>nomination form</p>
<p>electoral register</p>
<p>electoral roll</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 영국 국립 보건 서비스 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>공백으로 구분된 10-17자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>10-17자리 숫자:</p>
<ul>
<li><p>3 또는 10자리 숫자</p></li>
<li><p>공백</p></li>
<li><p>3자리 숫자</p></li>
<li><p>공백</p></li>
<li><p>4자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_uk_nhs_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>다음 중 하나가 충족됩니다.</p>
<ul>
<li><p><code>Keyword_uk_nhs_number</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_uk_nhs_number1</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_uk_nhs_number_dob</code>의 키워드가 발견되었습니다.</p></li>
</ul></li>
<li><p>체크섬이 통과됩니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- U.K. NHS Number -->
<Entity id="3192014e-2a16-44e9-aa69-4b20375c9a78" patternsProximity="300" recommendedConfidence="85">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_uk_nhs_number" />
        <Any minMatches="1">
          <Match idRef="Keyword_uk_nhs_number" />
          <Match idRef="Keyword_uk_nhs_number1" />
          <Match idRef="Keyword_uk_nhs_number_dob" />
        </Any>
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-142"> </h3>
<div>
<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_nhs_number</p></th>
<th> </th>
<th><p>Keyword_uk_nhs_number1</p></th>
<th><p>Keyword_uk_nhs_number_dob</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>국립 보건 서비스</p>
<p>nhs</p>
<p>health services authority</p>
<p>health authority</p></td>
<td> </td>
<td><p>patient id</p>
<p>patient identification</p>
<p>patient no</p>
<p>patient number</p></td>
<td><p>GP</p>
<p>DOB</p>
<p>D.O.B</p>
<p>Date of Birth</p>
<p>Birth Date</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 영국 NINO(국민 보험 번호)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>7 문자나 공백이 나 파선으로 구분 하 여 9 문자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>두 가능한 패턴:</p>
<ul>
<li><p>처음 두 (유효한 NINOs이이 패턴의 유효성을 검사;는이 접두사에 특정 문자만 사용 하지 대/소문자 구분)</p></li>
<li><p>6자리 숫자</p></li>
<li><p>'A', 'B', 'C' 또는 명의 ' (예: 접두사를 특정 문자에에서는 사용할 수는 접미사; 하지 대/소문자 구분만)</p></li>
</ul>
<p>또는</p>
<ul>
<li><p>처음 두</p></li>
<li><p>공백 또는 대시</p></li>
<li><p>2자리 숫자</p></li>
<li><p>공백 또는 대시</p></li>
<li><p>2자리 숫자</p></li>
<li><p>공백 또는 대시</p></li>
<li><p>2자리 숫자</p></li>
<li><p>공백 또는 대시</p></li>
<li><p>두 'A', 'B', 'C' 또는 명의 '</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_uk_nino</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_uk_nino</code>의 키워드가 발견되었습니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_uk_nino</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_uk_nino</code>의 키워드가 발견되지 않았습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- U.K. NINO -->
<Entity id="16c07343-c26f-49d2-a987-3daf717e94cc" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_uk_nino" />
        <Any minMatches="1">
          <Match idRef="Keyword_uk_nino" />
        </Any>
    </Pattern>    
     <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_uk_nino" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_uk_nino" />
        </Any>
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-144"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_uk_nino</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>national insurance number</p>
<p>national insurance contributions</p>
<p>protection act</p>
<p>insurance</p>
<p>social security number</p>
<p>insurance application</p>
<p>medical application</p>
<p>social insurance</p>
<p>medical attention</p>
<p>social security</p>
<p>great britain</p>
<p>insurance</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 미국/영국 여권 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>9자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>9자리 연속 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_usa_uk_passport</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_passport</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<Entity id="178ec42a-18b4-47cc-85c7-d62c92fd67f8" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_usa_uk_passport" />
        <Match idRef="Keyword_passport" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-146"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_passport</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Passport Number</p>
<p>Passport No</p>
<p>Passport #</p>
<p>Passport#</p>
<p>PassportID</p>
<p>Passportno</p>
<p>passportnumber</p>
<p>パスポート</p>
<p>パスポート番号</p>
<p>パスポートのNum</p>
<p>パスポート＃</p>
<p>Numéro de passeport</p>
<p>Passeport n °</p>
<p>Passeport Non</p>
<p>Passeport #</p>
<p>Passeport#</p>
<p>PasseportNon</p>
<p>Passeportn °</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 미국 은행 계좌 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>8-17자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>8-17자리 연속 숫자</p></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Regex_usa_bank_account_number</code> 정규식이 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_usa_Bank_Account</code>의 키워드가 발견되었습니다.</p></li>
</ul>


```Command&nbsp;Line
<!-- U.S. Bank Account Number -->
<Entity id="a2ce32a8-f935-4bb6-8e96-2a5157672e2c" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Regex_usa_bank_account_number" />
        <Match idRef="Keyword_usa_Bank_Account" />
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-148"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_usa_Bank_Account</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Checking Account Number</p>
<p>Checking Account</p>
<p>Checking Account #</p>
<p>Checking Acct Number</p>
<p>Checking Acct #</p>
<p>Checking Acct No.</p>
<p>Checking Account No.</p>
<p>Bank Account Number</p>
<p>Bank Account #</p>
<p>Bank Acct Number</p>
<p>Bank Acct #</p>
<p>Bank Acct No.</p>
<p>Bank Account No.</p>
<p>Savings Account Number</p>
<p>Savings Account.</p>
<p>Savings Account #</p>
<p>Savings Acct Number</p>
<p>Savings Acct #</p>
<p>Savings Acct No.</p>
<p>Savings Account No.</p>
<p>Debit Account Number</p>
<p>Debit Account</p>
<p>Debit Account #</p>
<p>Debit Acct Number</p>
<p>Debit Acct #</p>
<p>Debit Acct No.</p>
<p>Debit Account No.</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 미국 운전 면허 번호


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>주마다 다릅니다.</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>주마다 다릅니다(예: 뉴욕).</p>
<ul>
<li><p>숫자 9 개 ddd ddd ddd 일치와 동일 하 게 서식이 지정 합니다.</p></li>
<li><p>Ddddddddd 같은 숫자 9 개 일치 하지 않습니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_new_york_drivers_license_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_[state_name]_drivers_license_name</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_us_drivers_license</code> 에서 키워드를 발견 됩니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 65% 신뢰합니다.</p>
<ul>
<li><p><code>Func_new_york_drivers_license_number</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_[state_name]_drivers_license_name</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_us_drivers_license_abbreviations</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Keyword_us_drivers_license</code>의 키워드가 발견되지 않았습니다.</p></li>
</ul>

```Command&nbsp;Line    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_new_york_drivers_license_number" />
        <Match idRef="Keyword_new_york_drivers_license_name" />
        <Match idRef="Keyword_us_drivers_license" />
    </Pattern>
    <Pattern confidenceLevel="65">
        <IdMatch idRef="Func_new_york_drivers_license_number" />
        <Match idRef="Keyword_new_york_drivers_license_name" />
        <Match idRef="Keyword_us_drivers_license_abbreviations" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Keyword_us_drivers_license" />
        </Any>
    </Pattern>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-150"> </h3>
<div>
<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_us_drivers_license_abbreviations</p></th>
<th> </th>
<th><p>Keyword_us_drivers_license</p></th>
<th><p>Keyword_[state_name]_drivers_license_name</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DL</p>
<p>DLS</p>
<p>CDL</p>
<p>CDLS</p>
<p>ID</p>
<p>IDs</p>
<p>DL#</p>
<p>DLS#</p>
<p>CDL#</p>
<p>CDLS#</p>
<p>ID#</p>
<p>IDs#</p>
<p>ID number</p>
<p>ID numbers</p>
<p>LIC</p>
<p>LIC#</p></td>
<td> </td>
<td><p>DriverLic</p>
<p>DriverLics</p>
<p>DriverLicense</p>
<p>DriverLicenses</p>
<p>Driver Lic</p>
<p>Driver Lics</p>
<p>Driver License</p>
<p>Driver Licenses</p>
<p>DriversLic</p>
<p>DriversLics</p>
<p>DriversLicense</p>
<p>DriversLicenses</p>
<p>Drivers Lic</p>
<p>Drivers Lics</p>
<p>Drivers License</p>
<p>Drivers Licenses</p>
<p>Driver'Lic</p>
<p>Driver'Lics</p>
<p>Driver'License</p>
<p>Driver'Licenses</p>
<p>Driver' Lic</p>
<p>Driver' Lics</p>
<p>Driver' License</p>
<p>Driver' Licenses</p>
<p>Driver'sLic</p>
<p>Driver'sLics</p>
<p>Driver'sLicense</p>
<p>Driver'sLicenses</p>
<p>Driver's Lic</p>
<p>Driver's Lics</p>
<p>Driver's License</p>
<p>Driver's Licenses</p>
<p>identification number</p>
<p>identification numbers</p>
<p>identification #</p>
<p>id card</p>
<p>id cards</p>
<p>identification card</p>
<p>identification cards</p>
<p>DriverLic#</p>
<p>DriverLics#</p>
<p>DriverLicense#</p>
<p>DriverLicenses#</p>
<p>Driver Lic#</p>
<p>Driver Lics#</p>
<p>Driver License#</p>
<p>Driver Licenses#</p>
<p>DriversLic#</p>
<p>DriversLics#</p>
<p>DriversLicense#</p>
<p>DriversLicenses#</p>
<p>Drivers Lic#</p>
<p>Drivers Lics#</p>
<p>Drivers License#</p>
<p>Drivers Licenses#</p>
<p>Driver'Lic#</p>
<p>Driver'Lics#</p>
<p>Driver'License#</p>
<p>Driver'Licenses#</p>
<p>Driver' Lic#</p>
<p>Driver' Lics#</p>
<p>Driver' License#</p>
<p>Driver' Licenses#</p>
<p>Driver'sLic#</p>
<p>Driver'sLics#</p>
<p>Driver'sLicense#</p>
<p>Driver'sLicenses#</p>
<p>Driver's Lic#</p>
<p>Driver's Lics#</p>
<p>Driver's License#</p>
<p>Driver's Licenses#</p>
<p>id card#</p>
<p>id cards#</p>
<p>identification card#</p>
<p>identification cards#</p></td>
<td><p>주 약어(예: "NY")</p>
<p>주 이름(예: "New York")</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 미국 ITIN(개인 납세자 번호)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>"9"로 시작되고, "7" 또는 "8"을 4번째 숫자로 포함하고, 경우에 따라 공백이나 대시로 서식이 지정된 9자리 숫자</p></td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>서식 있음:</p>
<ul>
<li><p>"9"자리 숫자</p></li>
<li><p>2자리 숫자</p></li>
<li><p>공백 또는 대시</p></li>
<li><p>"7" 또는 "8"</p></li>
<li><p>1자리 숫자</p></li>
<li><p>공백 또는 대시</p></li>
<li><p>4자리 숫자</p></li>
</ul>
<p>서식 없음:</p>
<ul>
<li><p>"9"자리 숫자</p></li>
<li><p>2자리 숫자</p></li>
<li><p>"7" 또는 "8"</p></li>
<li><p>5자리 숫자</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_formatted_itin</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>다음 중 하나 이상이 충족됩니다.</p>
<ul>
<li><p><code>Keyword_itin</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Func_us_address</code> 함수가 올바른 날짜 형식의 주소를 찾습니다.</p></li>
<li><p><code>Func_us_date</code> 함수가 올바른 날짜 형식의 날짜를 찾습니다.</p></li>
<li><p><code>Keyword_itin_collaborative</code>의 키워드가 발견되었습니다.</p></li>
</ul></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p><code>Func_unformatted_itin</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p>다음 중 하나 이상이 충족됩니다.</p>
<ul>
<li><p><code>Keyword_itin_collaborative</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Func_us_address</code> 함수가 올바른 날짜 형식의 주소를 찾습니다.</p></li>
<li><p><code>Func_us_date</code> 함수가 올바른 날짜 형식의 날짜를 찾습니다.</p></li>
</ul></li>
</ul>


```Command&nbsp;Line
<!-- U.S. Individual Taxpayer Identification Number (ITIN) -->
<Entity id="e55e2a32-f92d-4985-a35d-a0b269eb687b" patternsProximity="300" recommendedConfidence="75">
    <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_formatted_itin" />
        <Any minMatches="1">
          <Match idRef="Keyword_itin" />
          <Match idRef="Func_us_address" />
          <Match idRef="Func_us_date" />
          <Match idRef="Keyword_itin_collaborative" />
        </Any>
    </Pattern>
    <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_unformatted_itin" />
        <Match idRef="Keyword_itin" />
        <Any minMatches="1">
          <Match idRef="Keyword_itin_collaborative" />
          <Match idRef="Func_us_address" />
          <Match idRef="Func_us_date" />
        </Any>
    </Pattern>
</Entity>
```
</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-152"> </h3>
<div>
<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_itin</p></th>
<th> </th>
<th><p>Keyword_itin_collaborative</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>taxpayer</p>
<p>tax id</p>
<p>tax identification</p>
<p>itin</p>
<p>ssn</p>
<p>tin</p>
<p>social security</p>
<p>tax payer</p>
<p>itins</p>
<p>taxid</p>
<p>individual taxpayer</p></td>
<td> </td>
<td><p>License</p>
<p>DL</p>
<p>DOB</p>
<p>Birthdate</p>
<p>Birthday</p>
<p>Date of Birth</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>


## 미국 SSN(사회 보험 번호)


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>형식</p></td>
<td><p>서식 있는 패턴 또는 서식 없는 패턴으로 표시될 수 있는 9자리 숫자</p>

> [!NOTE]
> 2011 mid 하기 전에 발급 하는 경우는 SSN 강력한 위치 번호의 특정 부분 범위 내에 있어야 유효한 것으로 특정 범위 서식 지정 (다르지만 체크섬이 없는).


</td>
</tr>
<tr class="even">
<td><p>패턴</p></td>
<td><p>4 개의 함수 SSNs 4 개의 서로 다른 패턴에 나타나는지 확인합니다.</p>
<ul>
<li><p><code>Func_ssn</code> p r e 2011 강력한 서식이 적용 된 대시 또는 공백 (ddd-dd-dddd OR ddd dd dddd)으로 포맷 된 SSNs 발견</p></li>
<li><p><code>Func_unformatted_ssn</code> p r e 2011 강력한 서식이 지정 된 연속 되는 숫자 9 개 (ddddddddd)로 서식이 지정 된 되지 않은 SSNs 발견</p></li>
<li><p><code>Func_randomized_formatted_ssn</code> 대시 또는 공백 (ddd-dd-dddd OR ddd dd dddd)로 서식이 지정 된 게시물 2011 SSNs 발견</p></li>
<li><p><code>Func_randomized_unformatted_ssn</code> 연속 되는 숫자 9 개 (ddddddddd)로 서식이 지정 된 되지 않은 게시물 2011 SSNs 발견</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>체크섬</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>정의</p></td>
<td><p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 85% 신뢰합니다.</p>
<ul>
<li><p><code>Func_ssn</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_ssn</code>의 키워드가 발견되었습니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 75% 신뢰합니다.</p>
<ul>
<li><p>함수 <code>Func_unformatted_ssn</code> 패턴과 일치 하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_ssn</code>의 키워드가 발견되었습니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 65% 신뢰합니다.</p>
<ul>
<li><p><code>Func_randomized_formatted_ssn</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_ssn</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Func_ssn</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾지 않습니다.</p></li>
</ul>
<p>DLP 정책은 다음과 같은 경우 이러한 유형의 중요한 정보가 300자 이내의 접근성으로 검색되었음을 55% 신뢰합니다.</p>
<ul>
<li><p><code>Func_randomized_unformatted_ssn</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾습니다.</p></li>
<li><p><code>Keyword_ssn</code>의 키워드가 발견되었습니다.</p></li>
<li><p><code>Func_unformatted_ssn</code> 함수가 해당 패턴과 일치하는 콘텐츠를 찾지 않습니다.</p></li>
</ul>

```Command&nbsp;Line
<!-- U.S. Social Security Number (SSN) -->
    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77" patternsProximity="300" recommendedConfidence="75">
      <Pattern confidenceLevel="85">
        <IdMatch idRef="Func_ssn" />
        <Match idRef="Keyword_ssn" />
      </Pattern>
      <Pattern confidenceLevel="75">
        <IdMatch idRef="Func_unformatted_ssn" />
        <Match idRef="Keyword_ssn" />
      </Pattern>
      <Pattern confidenceLevel="65">
        <IdMatch idRef="Func_randomized_formatted_ssn" />
        <Match idRef="Keyword_ssn" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Func_ssn" />
        </Any>
      </Pattern>
      <Pattern confidenceLevel="55">
        <IdMatch idRef="Func_randomized_unformatted_ssn" />
        <Match idRef="Keyword_ssn" />
        <Any minMatches="0" maxMatches="0">
          <Match idRef="Func_unformatted_ssn" />
        </Any>
      </Pattern>
    </Entity>
```

</td>
</tr>
<tr class="odd">
<td><p>키워드</p></td>
<td><h3 id="section-154"> </h3>
<div>
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Keyword_ssn</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Social Security</p>
<p>Social Security#</p>
<p>Soc Sec</p>
<p>SSN</p>
<p>SSNS</p>
<p>SSN#</p>
<p>SS#</p>
<p>SSID</p></td>
</tr>
</tbody>
</table>

</div></td>
</tr>
</tbody>
</table>

