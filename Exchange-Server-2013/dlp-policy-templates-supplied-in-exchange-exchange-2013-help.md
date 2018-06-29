---
title: 'Exchange에서 제공 하는 DLP 정책 템플릿: Exchange 2013 Help'
TOCTitle: Exchange에서 제공 하는 DLP 정책 템플릿
ms:assetid: 7e1917ab-1920-4a52-97d1-7dfe2add6198
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150530(v=EXCHG.150)
ms:contentKeyID: 50482291
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange에서 제공 하는 DLP 정책 템플릿

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

Microsoft Exchange Server 2013과 Exchange Online에서는 DLP(데이터 손실 방지) 정책 템플릿을 시작점으로 사용하여 특정 규정 및 비즈니스 정책 요구 사항을 충족할 수 있게 해주는 DLP 정책을 만들 수 있습니다. 조직의 특정 요구 사항에 맞게 템플릿을 수정할 수 있습니다.


> [!WARNING]
> DLP 정책을 프로덕션 환경에서 실행하기 전에 테스트 모드에서 실행해야 합니다. 그러한 테스트 중에, 샘플 사용자 사서함을 구성한 다음 결과 확인을 위해 테스트 정책을 호출하는 테스트 메시지를 전송해보는 것이 좋습니다.<BR>이러한 정책을 사용하는 것만으로 반드시 모든 규정을 준수할 수 있는 것은 아닙니다. 테스트가 완료된 후에는 Exchange에서 구성을 필요한 대로 변경하여 정보 전송 시 조직의 정책을 준수하도록 하십시오. 예를 들어 알려진 비즈니스 파트너와의 TLS를 구성하거나, 특정 유형의 데이터가 포함된 메시지에 권한 보호 기능을 추가하는 등 보다 제한적인 전송 규칙 동작을 추가해야 할 수 있습니다.



## DLP에 사용할 수 있는 템플릿

다음 표에는 Exchange의 DLP 정책 템플릿이 나와 있습니다. 이러한 템플릿을 사용자 지정하여 DLP 템플릿을 만드는 방법에 대한 자세한 내용은 [DLP 정책 관리](manage-dlp-policies-exchange-2013-help.md)를 참조하십시오.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>템플릿</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>호주 재무 데이터</p></td>
<td><p>일반적으로 호주에서 재무 데이터로 간주되는 정보(예: 신용 카드 및 SWIFT 코드)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>호주 HRIP Act(Health Records Act)</p></td>
<td><p>일반적으로 호주에서 HRIP(Health Records and Information Privacy - 보건 기록 및 정보 보호) 법의 구속을 받는 것으로 간주되는 정보(예: 의료 계정 번호 및 세금 파일 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>호주 PII(개인 식별 정보) 데이터</p></td>
<td><p>일반적으로 호주에서 PII(개인 식별 정보)로 간주되는 정보(예: 세금 파일 번호 및 운전 면허 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>호주 개인 정보 보호법</p></td>
<td><p>일반적으로 호주에서 개인 정보 보호법의 구속을 받는 것으로 간주되는 정보(예: 운전 면허 번호 및 여권 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>캐나다 재무 데이터</p></td>
<td><p>일반적으로 캐나다에서 재무 데이터로 간주되는 정보(예: 은행 계좌 번호 및 신용 카드)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>캐나다 HIA(Health Information Act)</p></td>
<td><p>캐나다 앨버타주에서 HIA(Health Information Act - 보건 정보법)의 구속을 받는 정보(예: 여권 번호 및 보건 정보)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>캐나다 PHIPA(Personal Health Act) - 온타리오</p></td>
<td><p>캐나다 온타리오주에서 PHIPA(Personal Health Information Protection Act - 개인 보건 정보 보호법)의 구속을 받는 정보(예: 여권 번호 및 보건 정보)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>캐나다 PHIA(Personal Health Information Act) - 매니토바</p></td>
<td><p>캐나다 매니토바주에서 PHIA(Personal Health Information Act - 개인 보건 정보법)의 구속을 받는 정보(예: 보건 정보)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>캐나다 PIPA(Personal Information Protection Act)</p></td>
<td><p>캐나다 브리티시 컬럼비아주에서 PIPA(Personal Information Protection Act - 개인 정보 보호법)의 구속을 받는 정보(예: 여권 번호 및 보건 정보)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>캐나다 PIPEDA(Personal Information Protection Act)</p></td>
<td><p>캐나다 브리티시 컬럼비아주에서 PIPEDA(Personal Information Protection and Electronic Documents Act - 개인 정보 보호 및 전자 문서법)의 구속을 받는 정보(예: 여권 번호 및 보건 정보)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>캐나다 PII(개인 식별 정보) 데이터</p></td>
<td><p>일반적으로 캐나다에서 PII(개인 식별 정보)로 간주되는 정보(예: 보건 등록 번호 및 사회 보장 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>프랑스 데이터 보호법</p></td>
<td><p>일반적으로 프랑스에서 데이터 보호법의 구속을 받는 것으로 간주되는 정보(예: 의료 보장 카드 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>프랑스 재무 데이터</p></td>
<td><p>일반적으로 프랑스에서 재무 정보로 간주되는 정보(예: 신용 카드, 계좌 정보 및 직불 카드 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>프랑스 PII(개인 식별 정보) 데이터</p></td>
<td><p>일반적으로 프랑스에서 PII(개인 식별 정보)로 간주되는 정보(예: 여권 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>독일 재무 데이터</p></td>
<td><p>일반적으로 독일에서 재무 데이터로 간주되는 정보(예: EU 직불 카드 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>독일 PII(개인 식별 정보) 데이터</p></td>
<td><p>일반적으로 독일에서 PII(개인 식별 정보)로 간주되는 정보(예: 운전 면허 번호 및 여권 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>이스라엘 재무 데이터</p></td>
<td><p>일반적으로 이스라엘에서 재무 데이터로 간주되는 정보(예: 은행 계좌 번호 및 SWIFT 코드)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>이스라엘 PII(개인 식별 정보) 데이터</p></td>
<td><p>일반적으로 이스라엘에서 PII(개인 식별 정보)로 간주되는 정보(예: 신분증 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>이스라엘 개인 정보 보호</p></td>
<td><p>일반적으로 이스라엘에서 개인 정보 보호법의 구속을 받는 것으로 간주되는 정보(예: 은행 계좌 번호 또는 신분증 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>일본 재무 데이터</p></td>
<td><p>일반적으로 일본에서 재무 정보로 간주되는 정보(예: 신용 카드, 계좌 정보 및 직불 카드 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>일본 PII(개인 식별 정보) 데이터</p></td>
<td><p>일반적으로 일본에서 PII(개인 식별 정보)로 간주되는 정보(예: 운전 면허 번호 및 여권 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>일본 개인 정보 보호</p></td>
<td><p>일본 개인 정보 보호법의 구속을 받는 정보(예: 주민 등록 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>PCI DSS(PCI Data Security Standard)</p></td>
<td><p>PCI DSS(PCI Data Security Standard - PCI 데이터 보안 표준)의 구속을 받는 정보(예: 신용 카드 또는 직불 카드 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>사우디 아라비아 - 사이버 범죄 방지법</p></td>
<td><p>일반적으로 사우디 아라비아에서 사이버 범죄 방지법의 구속을 받는 것으로 간주되는 정보(예: 국제 은행 계좌 번호 및 SWIFT 코드)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>사우디 아라비아 재무 데이터</p></td>
<td><p>일반적으로 사우디 아라비아에서 재무 데이터로 간주되는 정보(예: 국제 은행 계좌 번호 및 SWIFT 코드)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>사우디 아라비아 PII(개인 식별 정보) 데이터</p></td>
<td><p>일반적으로 사우디 아라비아에서 PII(개인 식별 정보)로 간주되는 정보(예: 신분증 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>영국 의료 보고 접근 규제법</p></td>
<td><p>영국 의료 보고 접근 규제법의 구속을 받는 정보(예: 국가 의료 서비스 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>영국 데이터 보호법</p></td>
<td><p>영국 데이터 보호법의 구속을 받는 정보(예: 국가 보장 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>영국 재무 데이터</p></td>
<td><p>일반적으로 영국에서 재무 정보로 간주되는 정보(예: 신용 카드, 계좌 정보 및 직불 카드 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>영국 PIOCP(Personal Information Online Code of Practice)</p></td>
<td><p>영국 PIOCP(Personal Information Online Code of Practice - 온라인 개인 정보 보호 정책)의 구속을 받는 정보(예: 보건 정보)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>영국 PII(개인 식별 정보) 데이터</p></td>
<td><p>일반적으로 영국에서 PII(개인 식별 정보)로 간주되는 정보(예: 운전 면허 번호 및 여권 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>영국 개인 정보 보호 및 전자 통신 규정</p></td>
<td><p>영국 개인 정보 보호 및 전자 통신 규정의 구속을 받는 정보(예: 재무 정보)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>미국 FTC(Federal Trade Commission) 소비자 규약</p></td>
<td><p>미국 FTC(Federal Trade Commission - 연방 통상 위원회) 소비자 규약의 구속을 받는 정보(예: 신용 카드 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>미국 재무 데이터</p></td>
<td><p>일반적으로 미국에서 재무 정보로 간주되는 정보(예: 신용 카드, 계좌 정보 및 직불 카드 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>미국 GLBA(Gramm-Leach-Bliley Act)</p></td>
<td><p>GLBA(Gramm-Leach-Bliley Act)의 구속을 받는 정보(예: 사회 보장 번호 또는 신용 카드 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>미국 HIPAA(Health Insurance Act)</p></td>
<td><p>미국 HIPAA(Health Insurance Portability and Accountability Act - 건강보험 이전 가능성 및 책임에 관한 법률)의 구속을 받는 정보(예: 사회 보장 번호 및 보건 정보)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>미국 애국법</p></td>
<td><p>일반적으로 미국 애국법의 구속을 받는 정보(예: 신용 카드 번호 또는 세금 식별 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>미국 PII(개인 식별 정보) 데이터</p></td>
<td><p>일반적으로 미국에서 PII(개인 식별 정보)로 간주되는 정보(예: 사회 보장 번호 및 운전 면허 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>미국 개인 정보 침해 고지법</p></td>
<td><p>미국 개인 정보 침해 고지법의 구속을 받는 정보(예: 사회 보장 번호 및 신용 카드 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>미국 사회 보장 번호 기밀 유지법</p></td>
<td><p>미국 사회 보장 번호 기밀 유지법의 구속을 받는 정보(예: 사회 보장 번호)가 있는지 여부를 검색할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


## 자세한 내용

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[템플릿에서 DLP 정책 만들기](how-to-new-dlp-data-loss-prevention-policy-template.md)

[Exchange의 중요 한 정보 유형 찾아보십시오](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

