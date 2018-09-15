---
title: '정보 권한 관리: Exchange 2013 Help'
TOCTitle: 정보 권한 관리
ms:assetid: 6ea3a695-3ddd-4d53-b3c6-90041f44ef64
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638140(v=EXCHG.150)
ms:contentKeyID: 50483336
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 정보 권한 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

정보 근로자는 일상 업무에서 재무 보고서와 데이터, 법적 계약, 기밀 제품 정보, 매출 보고서 및 매출 예상, 경쟁 분석, 연구 및 특허 정보, 고객 및 직원 정보와 같은 중요한 정보를 전자 메일을 사용하여 교환합니다. 사람들은 이제 어디에서나 자신의 전자 메일에 액세스할 수 있기 때문에 사서함은 잠재적으로 중요한 정보를 대량 포함하는 리포지토리로 변모했고, 그에 따라 정보 유출은 조직에 심각한 위협이 될 수 있습니다. Microsoft Exchange Server 2013에는 정보 유출을 방지하기 위해 전자 메일 메시지와 첨부 파일을 온라인과 오프라인에서 지속적으로 보호하는 IRM(정보 권한 관리) 기능이 포함되어 있습니다.

**목차**

What is information leakage?

Traditional solutions to information leakage

IRM in Exchange 2010

Applying IRM protection to messages

Scenarios for IRM protection

Decrypting IRM-protected messages to enforce messaging policies

Prelicensing

IRM agents

IRM requirements

Configuring and testing IRM

Extend Rights Management with the Rights Management connector

## 정보 유출이란?

잠재적으로 중요한 정보가 유출되면 조직에서 큰 대가를 치르게 되고 조직과 조직의 비즈니스, 직원, 고객 및 파트너에게 광범위하게 영향을 줄 수 있습니다. 국내 및 산업 규정은 점점 더 특정 유형의 정보를 저장하고, 전송하고, 보안하는 방법을 통제하고 있습니다. 해당 규정을 위반하지 않기 위해 조직은 고의, 부주의 또는 사고로 인한 정보 유출에 대비하여 스스로 보호해야 합니다.

다음은 정보 유출로 인한 부정적인 결과의 예입니다.

  - **금전적 손실** 규모, 산업, 국내 규정에 따라, 정보 유출은 사업 손실 또는 사법 기관이나 규제 당국이 부과하는 벌금 및 처벌로 인해 금전적으로 타격을 줄 수 있습니다. 또한 공개 기업의 경우 부정적인 언론 보도로 인해 시가총액이 낮아지는 위험을 각오해야 할 수도 있습니다.

  - **기업 이미지 및 신뢰도 하락** 정보 유출은 조직의 이미지, 고객과의 신뢰에 영향을 줄 수 있습니다. 더욱이 통신의 특성상, 유출된 전자 메일 메시지는 보낸 사람 및 조직을 잠재적으로 곤란한 상황에 빠지게 할 수 있습니다.

  - **경쟁 우위 상실** 정보 유출로 인한 가장 심각한 위협 중 하나는 비즈니스에서 경쟁 우위를 상실하는 것입니다. 전략적 계획 또는 인수 합병 정보가 유출되면 잠재적으로 매출 손실이나 시가총액 감소로 이어질 수 있습니다. 다른 위협으로는 연구 정보, 분석 데이터 및 그 밖의 지적 재산 손실을 들 수 있습니다.

맨 위로 이동

## 정보 유출에 대한 기존 솔루션

정보 유출에 대해 기존 솔루션은 초기 데이터 액세스를 보호하기는 하지만 지속적인 보호를 제공하지는 않는 경우가 많습니다. 다음 표에는 일부 기존 솔루션과 그 한계가 나와 있습니다.

### 기존 솔루션

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>솔루션</th>
<th>설명</th>
<th>제한</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TLS(전송 계층 보안)</p></td>
<td><p>TLS는 암호화로 네트워크를 통한 통신을 보안하는 데 사용하는 인터넷 표준 프로토콜입니다. 메시징 환경에서 TLS는 서버/서버 및 클라이언트/서버의 통신을 보안하는 데 사용됩니다.</p>
<p>기본적으로 Exchange 2010 TLS를 사용 하 여 모든 내부 메시지 전송에 합니다. 편의적 TLS 외부 호스트를 사용 하 여 세션에 대 한도 기본적으로 설정 됩니다. Exchange 은 먼저는 세션에 대 한 TLS 암호화를 사용 하려고 하지만 Exchange SMTP를 사용 하 여 대상 서버와 TLS 연결을 설정할 수 없으면, 합니다. 외부 조직과 mutual TLS를 적용 하려면 도메인 보안을 구성할 수도 있습니다.</p></td>
<td><p>TLS는 두 SMTP 호스트 간의 SMTP 세션만 보호합니다. 즉, TLS는 동작 중인 정보를 보호하지만, 메시지 수준 또는 정지되어 있는 정보를 보호하지 않습니다. 다른 방법을 사용하여 메시지를 암호화하지 않은 경우, 보낸 사람 및 받는 사람의 사서함에 있는 정보는 보호되지 않은 상태로 있습니다. 조직 외부로 보내는 전자 메일의 경우 첫 번째 홉에 대해서만 TLS가 필요합니다. 조직 외부의 원격 SMTP 호스트가 메시지를 받으면 암호화되지 않은 세션을 통해 다른 SMTP 호스트로 메시지를 릴레이할 수 있습니다. TLS는 전송 계층 기술이므로 메시지를 받는 사람이 해당 메시지로 수행하는 작업에 대해서는 제어할 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>전자 메일 암호화</p></td>
<td><p>사용자가 S/MIME 같은 기술을 사용하여 메시지를 암호화할 수 있습니다.</p></td>
<td><p>사용자가 메시지를 암호화할 것인지 결정합니다. 암호화에는 사용자에 대한 인증서 관리 오버헤드 및 개인 키 보호가 수반되므로 PKI(공개 키 인프라) 배포 비용이 추가로 소요됩니다. 메시지 암호가 해독된 후에는 메시지를 받은 사람이 해당 정보로 수행할 수 있는 작업에 대해서는 제어하지 않습니다. 즉 암호를 해독한 정보를 복사하거나 인쇄하거나 전달할 수 있습니다. 기본적으로 저장된 첨부 파일은 보호되지 않습니다.</p>
<p>S/MIME 같은 기술을 사용하여 암호화된 메시지는 조직에서 액세스할 수 없습니다. 조직은 메시지 콘텐츠를 검사할 수 없으므로 메시징 정책을 적용하거나 바이러스 또는 악의적 콘텐츠를 검색할 수 없고, 해당 콘텐츠에 액세스해야 하는 작업도 수행할 수 없습니다.</p></td>
</tr>
</tbody>
</table>


결국 기존 솔루션에는 정보 유출을 막기 위해 일관된 메시징 정책을 적용하는 시행 도구가 부족한 편입니다. 예를 들어, 한 사용자가 중요한 정보가 담긴 메시지를 **회사 기밀** 및 **전달하지 않음**으로 표시하여 보냅니다. 메시지가 받는 사람에게 배달된 후에는 보낸 사람이나 조직이 더 이상 이 정보를 제어할 수 없습니다. 받는 사람은 자동 전달 규칙과 같은 기능을 사용하여 의도적이든 비의도적이든 외부 전자 메일 계정에 메시지를 전달할 수 있으므로 조직은 상당한 정보 유출 위험에 직면해 있습니다.

맨 위로 이동

## Exchange 2013의 IRM

Exchange 2013에서는 IRM 기능을 사용하여 메시지와 첨부 파일을 영구적으로 보호할 수 있습니다. IRM은 Windows Server 2008 이상의 정보 보호 기술인 AD RMS(Active Directory Rights Management Services)를 사용합니다. Exchange 2013의 IRM 기능을 사용하여 조직과 사용자는 전자 메일을 받는 사람이 갖는 권한을 제어할 수 있습니다. 또한 IRM을 사용하면 받는 사람이 다른 받는 사람에게 메시지를 전달하거나, 메시지 또는 첨부 파일을 인쇄하거나, 복사하여 붙여넣기로 메시지 또는 첨부 파일 콘텐츠를 추출하는 등의 작업을 허용하거나 제한할 수도 있습니다. IRM 보호는 Microsoft Outlook이나 Microsoft Office Outlook Web App의 사용자가 적용하거나, 조직의 메시징 정책을 기반으로 전송 보호 규칙 또는 Outlook 보호 규칙을 사용하여 적용할 수 있습니다. 다른 전자 메일 암호화 솔루션과 달리, IRM은 조직에서 정책 준수를 위해 보호된 콘텐츠의 암호를 해독하는 것을 허용합니다.

AD RMS는 XrML(eXtensible Rights Markup Language) 기반 인증서와 라이선스를 사용하여 컴퓨터와 사용자를 인증하고 콘텐츠를 보호합니다. AD RMS를 사용하여 문서나 메시지 등의 콘텐츠를 보호하는 경우 권한 있는 사용자가 해당 콘텐츠에 대해 가지는 권한을 포함하는 XrML 라이선스가 첨부됩니다. IRM으로 보호된 콘텐츠에 액세스하려면 AD RMS 사용이 가능한 응용 프로그램이 AD RMS 클러스터에서 권한 있는 사용자에 대한 사용권을 가져와야 합니다.


> [!NOTE]
> Exchange 2013에서는 이전 라이선스 에이전트가 조직의 AD RMS 클러스터를 사용하여 보호된 메시지에 사용권을 첨부합니다. 자세한 내용은 이 항목 뒷부분에 있는 Prelicensing를 참조하십시오.



콘텐츠를 만드는 데 사용되는 응용 프로그램은 AD RMS를 사용하여 지속적인 콘텐츠 보호를 적용할 수 있도록 RMS 사용이 가능해야 합니다. Microsoft Office 응용 프로그램(예: Word, Excel, PowerPoint 및 Outlook)은 RMS 사용이 가능하여 이를 통해 보호되는 콘텐츠를 만들고 사용할 수 있습니다.

IRM을 사용하면 다음 작업을 수행할 수 있습니다.

  - 권한 있는 받는 사람이 IRM으로 보호된 콘텐츠를 전달, 수정, 인쇄, 팩스, 저장 또는 잘라내기/붙여넣기할 수 없도록 합니다.

  - 지원되는 첨부 파일 형식을 메시지와 동일한 수준으로 보호합니다.

  - IRM으로 보호된 메시지의 만료를 지원하여 지정된 기간 이후에는 이 메시지를 볼 수 없도록 합니다.

  - Microsoft Windows의 캡처 도구를 사용하여 IRM으로 보호된 콘텐츠를 복사할 수 없도록 합니다.

그러나 IRM은 다음 방법을 사용한 정보 복사는 막을 수 없습니다.

  - 타사 화면 캡처 프로그램

  - 화면에 표시된 IRM으로 보호된 콘텐츠를 촬영하는 이미징 장치(예: 카메라)

  - 사용자의 기억 또는 수동으로 정보 기록

AD RMS에 대 한 자세한 내용은, [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823)를 참조 하십시오.

## AD RMS 권한 정책 템플릿

AD RMS는 XrML 기반 권한 정책 템플릿을 사용하여 호환되는 IRM 사용이 가능한 응용 프로그램에서 일관된 보호 정책을 적용할 수 있게 합니다. Windows Server 2008 버전 이상에서는 템플릿을 열거하고 가져오기 위해 사용할 수 있는 웹 서비스가 AD RMS 서버에 표시됩니다. Exchange 2013은 전달하지 않음 템플릿을 제공합니다. 전달하지 않음 템플릿이 메시지에 적용되면 메시지에 지정되어 있는 받는 사람만 메시지의 암호를 해독할 수 있습니다. 받는 사람은 메시지를 전달하거나 메시지의 콘텐츠를 복사하거나 메시지를 인쇄할 수 없습니다. 조직의 AD RMS 서버에 RMS 템플릿을 추가로 만들어 IRM 보호 요구 사항을 충족할 수 있습니다.

IRM 보호는 AD RMS 권한 정책 템플릿을 사용하여 적용됩니다. 정책 템플릿을 사용하면 받는 사람이 메시지에 대해 가지는 사용 권한을 제어할 수 있습니다. 즉, 메시지에 적절한 권한 정책 템플릿을 적용하여 회신, 전체 회신, 전달, 메시지에서 정보 추출, 메시지 저장, 또는 메시지 인쇄 등의 작업을 제어할 수 있습니다.

권한 정책 서식 파일에 대 한 자세한 내용은 [AD RMS 정책 템플릿 고려 사항](https://go.microsoft.com/fwlink/p/?linkid=179455)을 참조 하십시오.

AD RMS 권한 정책 템플릿 만들기에 대 한 자세한 내용은 [AD RMS 권한 정책 템플릿 배포 단계별 가이드](https://go.microsoft.com/fwlink/p/?linkid=136593)를 참조 하십시오.

맨 위로 이동

## 메시지에 IRM 보호 적용

Exchange 2010 다음과 같은 방법을 사용 하 여 메시지에 IRM 보호를 적용할 수 있습니다.

  - **Outlook 사용자가 수동으로 시작**   Outlook 사용자가 자신에 게 사용할 수 있는 AD RMS 권한 정책 템플릿 사용 하 여 IRM 보호 메시지 수입니다. 이 프로세스는 Outlook 및 Exchange 하지는 IRM 기능을 사용합니다. 그러나 Exchange 액세스 메시지에 사용할 수 있으며 (예: 전송 규칙을 적용 하면) 작업을 수행할 수 있습니다의 조직에 적용할 정책 메시징 합니다. Outlook 에서 IRM을 사용 하는 방법에 대 한 자세한 내용은 [전자 메일 메시지에 대 한 IRM 사용 소개](https://go.microsoft.com/fwlink/p/?linkid=166897)를 참조 하십시오.

  - **Outlook Web App 사용자가 수동으로**  Outlook Web App에서 IRM을 사용하면 사용자는 보내는 메시지를 IRM으로 보호할 수 있고, IRM으로 보호된 받은 메시지를 볼 수 있습니다. Exchange 2013 CU1(누적 업데이트 1)에서 Outlook Web App 사용자는 Web-Ready 문서 보기를 사용하여 IRM으로 보호된 첨부 파일도 볼 수 있습니다. Outlook Web App의 IRM에 대한 자세한 내용은 [Outlook Web App에서 정보 권한 관리](information-rights-management-in-outlook-web-app-exchange-2013-help.md)를 참조하십시오.

  - **Windows Mobile와 Exchange ActiveSync 장치 사용자가 수동으로**   Exchange 2010 의 버전 (RTM) manufacturing 릴리스에서 Windows 모바일 장치의 사용자가 볼 수 있고 IRM으로 보호 된 메시지를 만듭니다. 이 사용자의 컴퓨터에 지원 되는 Windows 모바일 장치를 연결 및 IRM에 대 한이 활성화 해야 합니다. Exchange 2010 s p 1에서에서 Exchange ActiveSync 장치 ( Windows 모바일 장치 포함)의 사용자를 볼 수 있도록 Microsoft Exchange ActiveSync 에서 IRM을 사용 하도록 설정, 회신, 전달, 및 IRM으로 보호 된 메시지를 만들 수 있습니다. Exchange ActiveSync 에서 IRM에 대 한 자세한 내용은 [Exchange ActiveSync의 정보 권한 관리](information-rights-management-in-exchange-activesync-exchange-2013-help.md)을 참조 하십시오.

  - **Outlook 2010 이상에서 자동으로**   Outlook 2010 이상에서 메시지를 자동으로 IRM으로 보호하는 Outlook 보호 규칙을 만들 수 있습니다. Outlook 보호 규칙은 Outlook 2010 클라이언트에 자동으로 배포되며 IRM 보호는 사용자가 메시지를 작성할 때 Outlook 2010에 의해 적용됩니다. Outlook 보호 규칙에 대한 자세한 내용은 [Outlook 보호 규칙](outlook-protection-rules-exchange-2013-help.md)를 참조하십시오.

  - **사서함 서버에서 자동으로**   Exchange 2013 사서함 서버에서 메시지를 자동으로 IRM으로 보호하는 전송 보호 규칙을 만들 수 있습니다. 전송 보호 규칙에 대한 자세한 내용은 [전송 보호 규칙](transport-protection-rules-exchange-2013-help.md)를 참조하십시오.
    

    > [!NOTE]
    > 이미 IRM으로 보호된 메시지에는 IRM 보호가 다시 적용되지 않습니다. 예를 들어, 사용자가 Outlook 또는 Outlook Web App에서 메시지를 IRM으로 보호하는 경우 IRM 보호는 전송 보호 규칙을 사용하는 메시지에 적용되지 않습니다.



맨 위로 이동

## IRM 보호를 지원하는 시나리오

IRM 보호를 지원하는 시나리오는 다음 표에 설명되어 있습니다.

### IRM 보호를 지원하는 시나리오

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>IRM으로 보호된 메시지 보내기</th>
<th>지원됨</th>
<th>요구 사항</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>동일한 온-프레미스 Exchange 2013 배포 내에서</p></td>
<td><p>예</p></td>
<td><p>요구 사항에 대한 자세한 내용은 이 항목 뒷부분에 나오는 IRM Requirements을 참조하십시오 .</p></td>
</tr>
<tr class="even">
<td><p>온-프레미스 배포에서 다른 포리스트 사이</p></td>
<td><p>예</p></td>
<td><p>요구 사항에 대 한 <a href="https://go.microsoft.com/fwlink/p/?linkid=199009">포리스트를 사용한 Exchange Server 2010에서 여러 통합 되도록 AD RMS 구성</a>를 참조 하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>온-프레미스 Exchange 2013 배포와 클라우드 기반 Exchange 조직 사이</p></td>
<td><p>예</p></td>
<td><ul>
<li><p>온-프레미스 AD RMS 서버를 사용합니다.</p></li>
<li><p>트러스트된 게시 도메인을 온-프레미스 AD RMS 서버에서 내보냅니다.</p></li>
<li><p>트러스트된 게시 도메인을 클라우드 기반 조직으로 가져옵니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>외부 받는 사람에게</p></td>
<td><p>아니요</p></td>
<td><p>Exchange 2010 비 페더레이션 조직에서 외부 받는 사람에 게 IRM으로 보호 된 메시지를 보내기 위한 솔루션에 포함 되지 않습니다. AD RMS 트러스트 정책을 사용 하 여 솔루션을 제공 합니다. AD RMS 클러스터 및 Microsoft 계정 (이전의 Windows Live ID) 간의 트러스트 정책을 구성할 수 있습니다. 두 조직 간에 보낸 메시지에 대 한 Active Directory Federation Services (AD FS)를 사용 하 여 두 Active Directory 포리스트 간에 페더레이션된 트러스트를 만들 수 있습니다. 자세한 내용은, <a href="https://go.microsoft.com/fwlink/p/?linkid=182909">이해 AD RMS 트러스트 정책</a>를 참조 합니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 메시징 정책 준수를 위해 IRM으로 보호된 메시지의 암호 해독

메시징 정책 및 규정 준수를 위해서는 암호화된 메시지 콘텐츠에 액세스할 수 있어야 합니다. 소송, 규제 감사, 내부 조사에 따른 eDiscovery 요구 사항을 충족하려면 암호화된 메시지를 검색할 수 있어야 합니다. 이러한 작업을 돕기 위해 Exchange 2013에는 다음 IRM 기능이 포함되어 있습니다.

  - **전송 암호 해독**   메시징 정책을 적용하기 위해서는 전송 에이전트(예: 전송 규칙 에이전트)가 메시지 콘텐츠에 액세스할 수 있어야 합니다. 전송 암호 해독은 Exchange 2013 서버에 설치된 전송 에이전트가 메시지 콘텐츠에 액세스하는 것을 허용합니다. 자세한 내용은 [전송 암호 해독](transport-decryption-exchange-2013-help.md)를 참조하십시오.

  - **저널 보고서 암호 해독**   규정 또는 비즈니스 요구 사항을 충족하기 위해 조직에서는 저널링을 사용하여 메시징 콘텐츠를 유지할 수 있습니다. 저널링 에이전트는 저널링 대상인 메시지에 대한 저널 보고서를 만들고 메시지에 대한 메타데이터를 보고서에 포함합니다. 원본 메시지는 저널 보고서에 첨부됩니다. 저널 보고서의 메시지가 IRM으로 보호되지 않은 경우 저널 보고서 암호 해독은 메시지의 일반 텍스트 사본을 저널 보고서에 첨부합니다. 자세한 내용은 [저널 보고서 암호 해독](journal-report-decryption-exchange-2013-help.md)를 참조하십시오.

  - **Exchange Search를 위한 IRM 암호 해독**   Exchange Search를 위한 IRM 암호 해독을 사용하면 Exchange Search는 IRM으로 보호된 메시지의 콘텐츠를 인덱싱할 수 있습니다. 검색 관리자가 원본 위치 eDiscovery 검색을 수행하는 경우 IRM으로 보호되는 인덱싱된 메시지가 검색 결과에 반환됩니다. 자세한 내용은 [원본 위치 eDiscovery](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery) 항목을 참조하십시오.
    

    > [!NOTE]
    > Exchange 2010 s p 1에서에서 그리고 나중에 검색 관리 역할 그룹의 구성원 검색에서 반환 하 고 검색 사서함에 있는 IRM으로 보호 된 메시지에 액세스할 수 있습니다. 이 기능을 활성화 하려면 <A href="https://technet.microsoft.com/ko-kr/library/dd979792(v=exchg.150)">Set-IRMConfiguration</A> cmdlet과 함께 <EM>EDiscoverySuperUserEnabled</EM> 매개 변수를 사용 합니다. 자세한 내용은 <A href="configure-irm-for-exchange-search-and-https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery">Exchange 검색 및 원본 위치 eDiscovery에 대 한 IRM 구성</A>을 참조 하십시오.



이러한 암호 해독 기능을 사용하려면 Exchange 서버가 메시지에 액세스할 수 있어야 합니다. 이는 Exchange 설치 프로그램에 의해 만들어진 시스템 사서함인 페더레이션 사서함을 AD RMS 서버의 Super Users 그룹에 추가하면 가능합니다. 자세한 내용은 [AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 이전 라이선스

IRM으로 보호된 메시지와 첨부 파일을 보기 위해 Exchange 2013 2010은 보호된 메시지에 이전 라이선스를 자동으로 첨부합니다. 이렇게 하면 클라이언트가 사용권을 검색하기 위해 AD RMS 서버에 대해 반복적인 트립을 만들지 않아도 되고 IRM으로 보호된 메시지와 첨부 파일을 오프라인으로도 볼 수 있습니다. 이전 라이선스를 통해서도 IRM으로 보호되는 메시지를 Outlook Web App에서 볼 수 있습니다. IRM 기능을 사용하는 경우 이전 라이선스는 기본적으로 사용됩니다.

맨 위로 이동

## IRM 에이전트

Exchange 2013에서 IRM 기능은 전송 에이전트를 사용하여 사서함 서버의 전송 서비스에서 사용하도록 설정됩니다. IRM 에이전트는 Exchange 설치 프로그램에 의해 사서함 서버에 설치됩니다. 사용자는 IRM 에이전트에 대한 관리 작업을 사용하여 IRM 에이전트를 제어할 수 없습니다.


> [!NOTE]
> Exchange 2013에서 IRM 에이전트는 기본 제공 에이전트입니다. 기본 제공 에이전트는 <STRONG>Get-TransportAgent</STRONG> cmdlet이 반환하는 에이전트 목록에 포함되지 않습니다. 자세한 내용은 <A href="transport-agents-exchange-2013-help.md">전송 에이전트</A>를 참조하십시오.



다음 표에서는 사서함 서버의 전송 서비스에서 구현되는 IRM 에이전트를 보여 줍니다.

### 사서함 서버의 전송 서비스에 있는 IRM 에이전트

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>에이전트</th>
<th>이벤트</th>
<th>기능</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RMS 암호 해독 에이전트</p></td>
<td><p>OnEndOfData(SMTP) 및 OnSubmittedMessage</p></td>
<td><p>전송 에이전트가 액세스할 수 있도록 메시지를 암호 해독합니다.</p></td>
</tr>
<tr class="even">
<td><p>전송 규칙 에이전트</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>RMS 암호화 에이전트에 의해 IRM으로 보호되기 위한 전송 보호 규칙의 규칙 조건에 일치하는 메시지에 플래그를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>RMS 암호화 에이전트</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>전송 규칙 에이전트에 의해 플래그가 지정된 메시지에 IRM 보호를 적용하고 전송 암호가 해독된 메시지를 다시 암호화합니다.</p></td>
</tr>
<tr class="even">
<td><p>사전 라이선스 에이전트</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>이전 라이선스를 IRM으로 보호된 메시지에 첨부합니다.</p></td>
</tr>
<tr class="odd">
<td><p>저널 보고서 암호 해독 에이전트</p></td>
<td><p>OnCategorizedMessage</p></td>
<td><p>저널 보고서에 첨부된 IRM으로 보호된 메시지의 암호를 해독하고, 암호화된 원본 메시지와 함께 일반 텍스트 버전을 포함합니다.</p></td>
</tr>
</tbody>
</table>


전송 에이전트에 대한 자세한 내용은 [전송 에이전트](transport-agents-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## IRM 요구 사항

Exchange 2013 조직 내에 IRM을 구현하려면 배포는 다음 표에 설명된 요구 사항을 충족해야 합니다.

### IRM 요구 사항

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>서버</th>
<th>요구 사항</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AD RMS 클러스터</p></td>
<td><ul>
<li><p><strong>운영 체제</strong>   Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 SP2와 핫픽스 <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=973247">Windows Server 2008의 Active Directory Rights Management Services 역할</a> 항목이 필요합니다.</p></li>
<li><p><strong>서비스 연결 지점</strong> Exchange 2010 및 AD RMS 인식 응용 프로그램 Active Directory 에 등록 된 서비스 연결 지점을 사용 하 여 AD RMS 클러스터 및 Url을 검색 하도록 합니다. AD RMS를 사용 하면 AD RMS 설치 프로그램 내에서 서비스 연결 지점을 등록할 수 있습니다. AD RMS를 설정 하려면 사용 하는 계정은 Enterprise Admins 보안 그룹의 구성원이 아니면 설치가 완료 된 후 서비스 연결 지점 등록을 수행할 수 있습니다. 하나의 서비스 연결 지점을 Active Directory 포리스트의 AD RMS에 대 한 방법이 있습니다.   </p></li>
<li><p><strong>권한</strong>   AD RMS 서버 인증 파이프 라인에 대한 읽기 및 실행 권한(AD RMS 서버의 <code>ServerCertification.asmx</code> 파일)은 다음과 같이 지정해야 합니다.</p>
<ul>
<li><p>Exchange 서버 그룹 또는 개인 Exchange 서버</p></li>
<li><p>AD RMS 서버의 AD RMS 서비스 그룹</p></li>
</ul>
<p>기본적으로 ServerCertification.asmx 파일은 AD RMS 서버에서 <code>\inetpub\wwwroot\_wmcs\certification\</code> 폴더에 있는 됩니다. 자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=186951">AD RMS 서버 인증 파이프라인에 대 한 설정 권한</a>를 참조 합니다.</p></li>
<li><p><strong>AD RMS Super Users</strong>   전송 암호 해독, 저널 보고서 암호 해독, Outlook Web App의 IRM, Exchange Search를 위한 IRM을 사용하도록 설정하려면 페더레이션 사서함, Exchange 2013 설치 프로그램에 의해 만들어진 시스템 사서함을 AD RMS 클러스터의 Super Users 그룹에 추가해야 합니다. 자세한 내용은 <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.</a>를 참조하십시오.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange</p></td>
<td><ul>
<li><p>Exchange 2010 이후 버전이 필요 합니다.</p></li>
<li><p>핫픽스 <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=973136">FIX: .NET Framework 2.0 SP2 기반 응용 프로그램이 ASP.NET 웹 서비스 요청을 비동기화하기 위해 길이가 0인 콘텐츠로 응답을 처리하려고 시도할 경우의 ArgumentNullException 예외 오류 메시지: &quot;값이 Null일 수 없음&quot;</a> 항목을 Microsoft .NET Framework 2.0 SP2의 경우에 참조하십시오.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>사용자가 Outlook의 메시지를 IRM으로 보호할 수 있습니다. Outlook 2003으로 시작하여 IRM으로 보호하는 메시지를 위한 AD RMS 템플릿을 지원합니다.</p></li>
<li><p>Outlook 보호 규칙은는 Exchange 2010 및 Outlook 2010 기능입니다. 이전 버전의 Outlook 이 기능을 지원 하지 않습니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>Exchange ActiveSync 프로토콜 버전 14.1을 지원하는 장치(Windows Mobile 장치 포함)는 Exchange ActiveSync의 IRM을 지원할 수 있습니다. 장치에 있는 모바일 전자 메일 응용 프로그램은 Exchange ActiveSync 프로토콜 버전 14.1에서 정의한 <strong>RightsManagementInformation</strong> 태그를 지원해야 합니다. Exchange 2013에서는 지원되는 장치를 가진 사용자가 해당 장치를 컴퓨터에 연결하여 활성화하지 않고도 Exchange ActiveSync의 IRM을 통해서 IRM으로 보호된 메시지를 보고, 회신하고, 전달하고, 만들 수 있습니다. 자세한 내용은 <a href="information-rights-management-in-exchange-activesync-exchange-2013-help.md">Exchange ActiveSync의 정보 권한 관리</a>를 참조하십시오.</p></li>
</ul></td>
</tr>
</tbody>
</table>



> [!NOTE]
> <EM>AD RMS클러스터</EM>는 단일 서버 배포를 포함하여 조직에서의 AD RMS 배포에 사용되는 용어입니다. AD RMS는 웹 서비스이며, 사용자가 Windows Server 장애 조치(failover) 클러스터를 설정할 필요가 없습니다. 고가용성 및 부하 분산을 위해 여러 AD RMS 서버를 클러스터에 배포하고 네트워크 부하 분산을 사용할 수 있습니다.




> [!IMPORTANT]
> 프로덕션 환경에서 동일한 서버에 AD RMS와 Exchange를 설치하는 것은 지원되지 않습니다.



Exchange 2013 IRM 기능에는 Microsoft Office 파일 형식을 지원 합니다. 사용자 지정 보호 기능을 배포 하 여 다른 파일 형식으로 제공 하는 IRM 보호 기능을 확장할 수 있습니다. 사용자 지정 보호 기능에 대 한 자세한 내용은 정보 보호 및 제어 파트너 [독립 소프트웨어 공급 업체](https://go.microsoft.com/fwlink/p/?linkid=210336)에서 참조 하십시오.

맨 위로 이동

## IRM 구성 및 테스트

Exchange 2013에서 IRM 기능을 구성하려면 Exchange 관리 셸을 사용해야 합니다. 개별 IRM 기능을 구성하려면 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\)) cmdlet을 사용합니다. 내부 메시지, 전송 암호 해독, 저널 보고서 암호 해독, Exchange Search 및 Outlook Web App에 대해 IRM을 사용하도록 설정하거나 사용하지 않도록 설정할 수 있습니다. IRM 기능 구성에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md)를 참조하십시오.

Exchange 2013 서버를 설치한 후 [Test-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979798\(v=exchg.150\)) cmdlet을 사용하여 IRM 배포에 대한 종단 간 테스트를 수행할 수 있습니다. 이 테스트는 초기 IRM 구성 직후 및 지속적으로 IRM 기능을 확인하는 데 유용합니다. cmdlet은 다음 테스트를 수행합니다.

  - Exchange 2013 조직의 IRM 구성을 검사합니다.

  - AD RMS 서버의 버전 및 핫픽스 정보를 확인합니다.

  - RAC(권한 계정 인증서) 및 CLC(클라이언트 사용 허가자 인증서)를 검색하여 Exchange 서버가 RMS에 대해 활성화될 수 있는지를 확인합니다.

  - AD RMS 서버에서 AD RMS 권한 정책 템플릿을 가져옵니다.

  - 지정된 보낸 사람이 IRM으로 보호된 메시지를 보낼 수 있는지 확인합니다.

  - 지정된 받는 사람에 대한 슈퍼 사용자 사용권을 검색합니다.

  - 지정된 보낸 사람에 대해 이전 라이선스를 가져옵니다.

맨 위로 이동

## RMS(Rights Management) 커넥터를 사용하여 RMS 확장

Microsoft RMS(Rights Management) 커넥터는 클라우드 기반 Microsoft RMS 서비스를 사용하여 Exchange 2013 서버의 데이터 보호 기능을 향상시키는 응용 프로그램(선택 사항)입니다. RMS 커넥터를 설치하면 정보가 효력을 발휘하는 동안 계속해서 데이터를 보호합니다. 이러한 서비스는 사용자가 지정할 수 있기 때문에 각자에게 필요한 보호 수준을 정의할 수 있습니다. 예를 들어 특정 사용자에게 전자 메일 메시지에 대한 액세스를 제한하거나 특정 메시지에 보기 전용 권한을 설정할 수 있습니다.

RMS 커넥터 및 설치 하는 방법에 대 한 자세한 내용은, [권한 관리 커넥터](https://technet.microsoft.com/en-us/library/dn375964.aspx)를 참조 하십시오.

