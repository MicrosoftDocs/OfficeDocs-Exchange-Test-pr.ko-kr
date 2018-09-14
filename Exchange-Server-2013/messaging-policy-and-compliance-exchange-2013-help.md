---
title: '메시징 정책 및 규정 준수: Exchange 2013 Help'
TOCTitle: 메시징 정책 및 규정 준수
ms:assetid: 65f20a20-27a4-4f6e-9b27-f8705d65b8d9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998599(v=EXCHG.150)
ms:contentKeyID: 50483285
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시징 정책 및 규정 준수

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

전자 메일은 모든 규모의 조직에서 정보 근로자를 위한 안정적이고 보편적인 통신 수단으로 자리잡았습니다. 메시징 저장소 및 사서함은 중요한 데이터를 보관하는 리포지토리가 되었습니다. 조직은 메시징 시스템이 적법하게 사용되도록 메시지 정책을 마련하고, 사용자에게 정책 준수 방법을 안내하는 사용자 지침을 제공하고, 필요한 경우 허용되지 않는 통신 유형에 대한 자세한 정보를 제공해야 합니다.

또한 전자 메일 수명 주기를 관리하고 비즈니스, 법 및 규정 요구 사항에 따라 특정 기간 동안 메시지를 보존하고 소송 및 조사를 위해 전자 메일 레코드를 보존하기 위한 정책도 마련해야 합니다. 또한 eDiscovery 요청을 충족하는 데 필요한 전자 메일 레코드를 검색하고 제공할 준비가 되어 있어야 합니다.

지적 재산권, 영업 비밀, 사업 계획, 조직에서 수집하거나 처리하는 PII(개인 식별 정보)도 유출되지 않도록 보호해야 합니다.

## Exchange 2013의 메시징 정책 및 규정 준수

다음 표에서는 Microsoft Exchange Server 2013의 메시징 정책 및 규정 준수 기능을 간략히 살펴보고, 기능 관리 방법을 비롯한 한 자세한 정보를 제공하는 항목에 대한 링크를 제공합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명</th>
<th>Resources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MRM(메시징 레코드 관리)</p></td>
<td><p>조직은 적용 가능한 규정을 준수하거나 법 또는 비즈니스 요구 사항을 충족하기 위해 메시징 정책에 전자 메일 수명 주기 정책을 포함합니다. 이러한 정책에서 다루어야 하는 일반적인 질문은 다음과 같습니다.</p>
<ul>
<li><p>메시지를 얼마 동안이나 보존해야 하는가?</p></li>
<li><p>메시지를 어디에 보존해야 하는가?</p></li>
<li><p>모든 메시지를 같은 기간 동안 보존해야 하는가?</p></li>
</ul>
<p>Exchange 2013에는 조직의 전자 메일 수명 주기 정책을 구현할 수 있게 해 주는 MRM 기능이 포함되어 있습니다. MRM을 사용하면 모든 메시지에 일관된 보존 설정을 적용하고, 사용자 지정 보존 정책을 사용하여 사서함에 대한 기준 보존 설정을 적용하고, 필요한 경우 사용자가 직접 메시지를 분류하여 지정한 기간 동안 보존하도록 허용할 수 있습니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/messaging-records-management/messaging-records-management">메시징 레코드 관리</a></p></td>
</tr>
<tr class="even">
<td><p>원본 보관</p></td>
<td><p><em>원본 위치 보관</em> 기능을 사용하면 개인 저장소 파일(.pst)을 사용하지 않아도 사용자가 Outlook 2010 이상 및 Outlook Web App에서 액세스할 수 있는 <em>보관 사서함</em>에 메시지를 저장할 수 있으므로 조직의 메시징 데이터를 다시 제어할 수 있습니다.</p></td>
<td><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">전체에서 Exchange 2013의 보관</a></p></td>
</tr>
<tr class="odd">
<td><p>원본 유지</p></td>
<td><p>소송 가능성이 존재하는 경우 조직은 해당 사례와 관련된 전자 메일을 비롯한 ESI(전자적으로 저장된 정보)를 보존해야 합니다. 원본 위치 유지 기능을 사용하면 쿼리 매개 변수와 일치하는 메시지를 검색하여 보존할 수 있습니다. 이렇게 하면 메시지가 삭제, 수정, 위조되지 않으며 무기한으로 또는 지정한 기간 동안 메시지를 보존할 수 있습니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-and-litigation-holds">원본 위치 유지 및 소송 보존</a></p></td>
</tr>
<tr class="even">
<td><p>원본 eDiscovery</p></td>
<td><p>원본 위치 eDiscovery를 사용하면 Exchange 조직 간에 사서함 데이터를 검색할 수 있으며 검색 결과를 미리 보고 검색 사서함에 복사할 수 있습니다.</p></td>
<td><p><a href="in-place-ediscovery-exchange-2013-help.md">원본 위치 eDiscovery</a></p></td>
</tr>
<tr class="odd">
<td><p>저널링</p></td>
<td><p>저널링은 조직이 인바운드 및 아웃바운드 전자 메일 통신을 기록하여 법적, 규정 및 조직의 준수 요구 사항에 대응하는 데 도움이 됩니다. 메시징 보존 및 준수에 대한 계획을 세울 때는 저널링을 이해하고, 저널링이 조직의 준수 정책과 잘 맞는지 및 Exchange 2013이 저널링된 메시지의 보안을 유지하는 데 어떤 식으로 도움이 되는지 이해하는 것이 중요합니다.</p></td>
<td><p><a href="journaling-exchange-2013-help.md">저널링</a></p></td>
</tr>
<tr class="even">
<td><p>전송 규칙</p></td>
<td><p>전송 규칙을 사용하면 조직을 경유한 메시지에서 특정 조건을 조회한 후 메시지에 대해 작업을 수행할 수 있습니다. 전송 규칙을 사용하여 전자 메일 메시지에 메시징 정책을 적용하고, 메시지를 보호하고, 메시징 시스템을 보호하고, 정보 유출을 방지할 수 있습니다.</p></td>
<td><p><a href="mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md">메일 흐름 또는 전송 규칙</a></p></td>
</tr>
<tr class="odd">
<td><p>DLP(데이터 손실 방지)</p></td>
<td><p>DLP 기능을 사용하면 중요한 데이터를 보호하고 사용자에게 정책 및 규정에 대해 알려 줄 수 있습니다. 사용자가 실수로 중요한 정보를 권한이 없는 사용자에게 보내지 못하도록 방지할 수도 있습니다. DLP 정책을 구성할 때 수많은 관련 파일 형식이 포함된 메시징 시스템의 콘텐츠를 분석하여 중요한 데이터를 식별하고 보호할 수 있습니다. Exchange 2013에 제공된 DLP 정책 템플릿은 PII 및 PCI-DSS(Payment Card Industry Data Security Standard)와 같은 규정 표준에 기반을 두고 있습니다. DLP는 확장 가능하므로 조직에 중요한 다른 정책을 포함할 수 있습니다. 또한 새 정책 팁 기능을 사용하면 중요한 데이터가 전송되기 전에 사용자에게 정책 위반에 대해 알려 줄 수 있습니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention">데이터 손실 방지</a></p></td>
</tr>
<tr class="even">
<td><p>IRM(정보 권한 관리)</p></td>
<td><p>IRM(정보 권한 관리)은 AD RMS(Active Directory Rights Management Services)를 사용하여 전자 메일 메시지 및 첨부 파일에 대해 일관된 온라인 및 오프라인 보호를 제공합니다.</p></td>
<td><p><a href="information-rights-management-exchange-2013-help.md">정보 권한 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>S/MIME</p></td>
<td><p>S/MIME(Secure/Multipurpose Internet Mail Extensions)을 사용하면 Office 365 사서함 및 Exchange 2013/Exchange Online 사용자가 조직 내에서 서명/암호화된 전자 메일을 보내 중요한 정보를 보호할 수 있습니다. 관리자는 Office 365와 온-프레미스 서버 간에 사용자 인증서를 동기화하고 S/MIME을 지원하도록 Outlook Online을 구성하여 Office 365 사서함에 대해 S/MIME을 사용하도록 설정할 수 있습니다.</p></td>
<td><p><a href="s-mime-for-message-signing-and-encryption-exchange-2013-help.md">메시지 서명 및 암호화를 위한 S/MIME</a></p></td>
</tr>
<tr class="even">
<td><p>사서함 감사 로깅</p></td>
<td><p>사서함에 HBI(높은 업무상의 영향) 정보 및 PII가 포함될 수 있으므로 조직의 사서함에 로그온하는 사람과 수행되는 작업을 추적하는 것이 중요합니다. 사서함 소유자(위임 사용자라고 함)가 아닌 사용자의 사서함 액세스를 추적하는 것이 특히 중요합니다. 사서함 감사 로깅을 사용하면 사서함 소유자, 대리인(전체 사서함 액세스 권한이 있는 관리자 포함) 및 관리자의 사서함 액세스를 로깅할 수 있습니다.</p></td>
<td><p><a href="mailbox-audit-logging-exchange-2013-help.md">사서함 감사 로깅</a></p>
<p><a href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/exchange-auditing-reports/exchange-auditing-reports">감사 보고서를 교환 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>관리자 감사 로깅</p></td>
<td><p>관리자 감사 로그를 사용하면 관리자가 Exchange 서버와 조직 구성, Exchange 받는 사람에 대해 변경한 사항의 로그를 보관할 수 있습니다. 관리자 감사 로깅을 변경 제어 프로세스의 일부로 사용하여 준수 목적으로 구성 및 받는 사람에 대한 액세스 변경 사항과 액세스를 추적할 수 있습니다.</p></td>
<td><p><a href="administrator-audit-logging-exchange-2013-help.md">관리자 감사 로깅</a></p></td>
</tr>
</tbody>
</table>

