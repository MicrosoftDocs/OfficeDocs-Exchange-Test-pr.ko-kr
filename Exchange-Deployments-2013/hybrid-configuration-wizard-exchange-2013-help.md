---
title: '하이브리드 구성 마법사: Exchange 2013 Help'
TOCTitle: 하이브리드 구성 마법사
ms:assetid: 2e6ed294-ee74-4038-8b71-b61786372ba4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh529921(v=EXCHG.150)
ms:contentKeyID: 50484627
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 하이브리드 구성 마법사

 

_<strong>적용 대상:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>마지막으로 수정된 항목:</strong>2016-12-09_

이 항목에서는 Exchange 하이브리드 배포 구성 프로세스의 개요, 사용 가능한 하이브리드 배포 기능과 옵션, 그리고 하이브리드 배포의 구성과 업데이트 모두에 필요한 핵심 작업을 실행하는 하이브리드 구성 엔진에 대해 살펴봅니다.

하이브리드 배포에 대한 자세한 내용은 [Exchange Server 하이브리드 배포](exchange-server-hybrid-deployments-exchange-2013-help.md)를 참조하십시오.

**목차**

하이브리드 구성 프로세스

하이브리드 구성 기능

하이브리드 구성 옵션

하이브리드 구성 엔진

## 하이브리드 구성 프로세스

하이브리드 구성 마법사 프로세스의 간략한 개요는 다음과 같습니다. 먼저, 마법사는 온-프레미스 Active Directory에 **HybridConfiguration** 개체를 만듭니다. 이 Active Directory 개체는 하이브리드 배포에 대한 하이브리드 구성 정보를 저장하고, 하이브리드 구성 마법사를 통해 업데이트됩니다. 그런 다음 마법사는 기존의 온-프레미스 Exchange 및 Active Directory 토폴로지 구성 데이터, Office 365 테넌트 및 Exchange Online 구성 데이터를 모으고, 여러 조직 매개 변수를 정의하고, 온-프레미스 및 Exchange Online 조직 모두에서 포괄적인 일련의 구성 작업을 실행합니다.


> [!IMPORTANT]
> 하이브리드 구성 마법사를 사용하기 전에 완료해야 할 몇 가지 중요한 고려 사항 및 선행 조건이 있습니다. <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">하이브리드 배포 필수 구성 요소</A>에 설명된 하이브리드 배포에 대한 요구 사항을 충족해야 합니다. 그러면 하이브리드 구성 마법사를 사용하여 하이브리드 배포를 위한 Exchange 조직을 구성할 준비가 됩니다.



하이브리드 배포 구성 프로세스의 일반 단계는 다음과 같습니다.

1.  **선행 조건 확인 및 토폴로지 확인 수행**   하이브리드 구성 마법사는 온-프레미스 및 Exchange Online 조직이 하이브리드 배포를 지원할 수 있는지 확인합니다. 온-프레미스 및 Exchange Online 조직에서 마법사가 확인하는 몇 가지 항목은 다음과 같습니다.
    
      - 온-프레미스 Exchange Server 버전
    
      - Exchange Online 버전
    
      - Active Directory 동기화 현재 상태 및 구성
    
      - 페더레이션 및 허용 도메인
    
      - 기존 페더레이션 트러스트 및 조직 관계
    
      - 웹 서비스 가상 디렉터리
    
      - Exchange 인증서

2.  **계정 자격 증명 테스트**   지정된 온-프레미스 및 Office 365 하이브리드 관리 계정은 온-프레미스 및 Exchange Online 조직에 액세스하여 선행 조건 확인 정보를 수집하고 하이브리드 배포 기능을 사용하도록 조직 매개 변수 구성을 변경합니다. 하이브리드 구성 마법사는 계정에 적합한 자격 증명이 있는지 그리고 온-프레미스 및 Exchange Online 조직에 연결할 수 있는지 확인합니다. 하이브리드 구성 마법사를 사용하여 이러한 작업을 완료하려면 온-프레미스 및 Office 365 조직 모두에 대한 하이브리드 배포 관리 계정이 조직 관리 역할 그룹의 구성원이어야 합니다.

3.  **하이브리드 배포 구성 변경**   하이브리드 구성 마법사는 하이브리드 관리 계정을 테스트하고, 확인 및 토폴로지 점검을 수행하고, 마법사 프로세스에서 정의한 구성 정보를 수집한 후에 하이브리드 배포를 만들고 사용하도록 구성을 변경합니다. 하이브리드 구성 변경 사항은 모두 하이브리드 구성 로그에 자동으로 기록됩니다. 기본적으로 하이브리드 구성 로그는 온-프레미스 사서함 서버(`%UserProfile%\AppData\Roaming\Microsoft\Exchange Hybrid Configuration`)에 있습니다.
    

    > [!IMPORTANT]
    > 인바운드 메일 흐름은 조직의 MX 레코드에 의해 제어됩니다. 하이브리드 배포에 대한 인바운드 인터넷 전자 메일은 하이브리드 구성 마법사로 구성되지 않습니다.



## 하이브리드 구성 기능

하이브리드 구성 마법사를 실행할 때마다 기본적으로 모든 하이브리드 배포 기능을 사용하도록 자동으로 설정됩니다. 특정 하이브리드 기능을 사용하지 않도록 설정하려면 Exchange 관리 셸 및 **Set-HybridConfiguration** cmdlet을 사용해야 합니다. 다음 하이브리드 배포 기능은 마법사에서 기본적으로 사용할 수 있습니다.

  - **약속 있음/없음 공유**   이 기능을 사용하면 온-프레미스 조직 사용자와 Exchange Online 조직 사용자 간에 공유할 일정 정보를 사용할 수 있습니다. 약속 있음/없음 공유는 온-프레미스 조직과 Exchange Online 조직에 대한 페더레이션 공유 및 조직 관계 구성의 일부로 사용할 수 있습니다. 자세한 내용은 [공유](https://technet.microsoft.com/ko-kr/library/dd638083\(v=exchg.150\))를 참조하십시오.

  - **메일 설명**   사용자가 메시지를 작성할 때 표시되는 정보 메시지입니다. 하이브리드 배포에서 메일 설명을 사용하도록 설정하면, 온-프레미스 및 Exchange Online 보낸 사람은 작성 중인 메시지를 조정하여 조직 간에 원치 않는 상황이나 NDR(배달 못 함 보고서)을 방지할 수 있습니다. 자세한 내용은 [MailTips](https://technet.microsoft.com/ko-kr/library/jj649091\(v=exchg.150\))을 참조하십시오.

  - **온라인 보관**   Exchange Online 조직은 이 기능을 사용하여 온-프레미스 및 Exchange Online 사용자에 대한 사용자 전자 메일 보관함을 호스트할 수 있습니다. 자세한 내용은 [Exchange Online Archiving 구성](http://go.microsoft.com/fwlink/p/?linkid=266565)을 참조하십시오.

  - **웹에서 Outlook 리디렉션**웹에서 Outlook 리디렉션은 온-프레미스 및 Exchange Online 사서함에 액세스할 수 있는 공통된 단일 URL을 제공합니다. 클라이언트 액세스 서버는 웹에서 Outlook 요청을 자동으로 온-프레미스 사서함 서버로 리디렉션하거나 Exchange Online 조직의 사서함에 대한 링크를 사용자에게 제공합니다.

  - **Exchange ActiveSync 리디렉션**  온-프레미스 Exchange 조직에서 Exchange Online으로 사서함을 이동하는 경우 해당 사서함에 액세스하는 모든 클라이언트를 Exchange Online을 사용하도록 업데이트해야 합니다. 여기에는 Exchange ActiveSync 장치가 포함됩니다. 이제 Exchange Online으로 사서함을 이동할 때 대부분의 Exchange ActiveSync 클라이언트가 자동으로 다시 구성됩니다. 자세한 내용은 [Exchange 하이브리드 배포를 사용한 Exchange ActiveSync 장치 설정](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md)을 참조하세요.

  - **보안 메일**    TLS(전송 계층 보안) 프로토콜을 통해 온-프레미스 조직과 Exchange Online 조직 간에 안전한 메시지 배달을 보장합니다. 온-프레미스 및 Exchange Online 조직은 디지털 인증서 주체를 통해 상호 인증되며 전자 메일 헤더와 서식 있는 텍스트 메시지 서식이 조직 전체에서 유지됩니다.

## 하이브리드 구성 옵션

하이브리드 구성 마법사를 사용하면 몇몇 영역에서 하이브리드 배포를 위한 특정 옵션을 선택할 수 있습니다. 하이브리드 배포를 처음 구성한 후 특정 하이브리드 구성 옵션을 업데이트하려면, 하이브리드 구성 마법사 또는 Exchange 관리 셸을 사용하여 다른 구성 옵션을 선택할 수 있습니다.

아래 표에는 하이브리드 구성 마법사가 수정하고 구성하는 주요 옵션이 요약되어 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>구성 영역</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>도메인</p></td>
<td><p>마법사가 클라우드 조직에 대한 자동 검색 요청 및 하이브리드 메일 흐름을 위한 온-프레미스 조직에 허용 도메인을 추가합니다. <em>동시 사용 도메인</em>이라고 하는 이 도메인은, 하이브리드 구성 마법사에서 선택한 도메인용 <em>PrimarySmtpAddress</em> 템플릿이 있는 모든 전자 메일 주소 정책에 보조 프록시 도메인으로 추가됩니다. 기본적으로 이 도메인은 &lt;도메인&gt;.mail.onmicrosoft.com입니다.</p>
<p>Exchange Online의 Exchange 관리 셸에서 다음 명령을 실행하여 허용 도메인을 볼 수 있습니다.</p>
<pre><code>Get-AcceptedDomain | FL DomainName, IsCoexistenceDomain</code></pre></td>
</tr>
<tr class="even">
<td><p>보안 메일 인증서</p></td>
<td><p>이 마법사에서는 온-프레미스 조직과 Exchange Online 조직 간에 전송되는 보안 전자 메일 메시지의 인증에 사용되는, 타사 CA(인증 기관)에서 발급한 특정 인증서를 선택해야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 페더레이션 공유</p></td>
<td><p>마법사는 온-프레미스 조직에 대해 Azure Active Directory 인증 시스템과의 기존 OAuth 인증 관계 또는 페더레이션 트러스트가 있는지 확인합니다. 이러한 관계가 있는 경우 하이브리드 배포를 지원하는 데 기존 OAuth 인증 또는 페더레이션 트러스트가 사용됩니다. 이러한 관계가 없으면 마법사는 온-프레미스 Exchange 구성 유형에 따라 온-프레미스 조직에 대해 Azure AD 인증 시스템과의 OAuth 인증을 구성하거나 페더레이션 트러스트를 만듭니다. 또한 필요한 경우 하이브리드 구성 마법사 내에서 선택된 도메인이 페더레이션 트러스트에 추가됩니다.</p>
<p>OAuth 인증 또는 페더레이션 트러스트 구성 외에도 온-프레미스 및 Exchange Online 조직에 대한 조직 관계가 만들어지고 구성됩니다. 이러한 조직 관계를 사용하여 약속 있음/없음 공유, 웹에서 Outlook 리디렉션 및 메일 설명을 포함한 여러 하이브리드 배포 기능을 사용하도록 설정할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>메일 흐름</p></td>
<td><p>이 마법사를 사용하면 온-프레미스 조직과 Exchange Online 조직 간의 보안 메일 전송을 처리할 Exchange Server를 선택하고 구성할 수 있습니다. Exchange 2010 버전에서는 허브 전송 서버입니다. Exchange 2013 버전에서는 클라이언트 액세스 서버입니다. Exchange 2016 이후 버전에서는 사서함 서버입니다.</p>
<p>이 마법사는 하이브리드 메일 라우팅을 위한 온-프레미스 Exchange 및 Exchange Online 조직을 구성합니다. 이 마법사는 온-프레미스 조직에서 새 송신 및 수신 커넥터와 기존 송신 및 수신 커넥터를 구성하고 Exchange Online에서 인바운드 및 아웃바운드 커넥터를 구성하므로 사용자가 Exchange Online 조직에서 인터넷으로 배달된 아웃바운드 메시지를 외부 메일 받는 사람에게 직접 보낼 것인지 아니면 하이브리드 배포에 포함된 온-프레미스 Exchange 서버를 통해 라우팅할 것인지 선택할 수 있습니다.</p>

> [!IMPORTANT]
> 인바운드 메일 흐름은 조직의 MX 레코드에 의해 제어됩니다. 하이브리드 배포에 대한 인바운드 인터넷 전자 메일은 하이브리드 구성 마법사로 구성되지 않습니다.


</td>
</tr>
</tbody>
</table>


## 하이브리드 구성 엔진

하이브리드 구성 엔진은 하이브리드 배포 구성 및 업데이트에 필요한 주요 작업을 실행합니다. `Update-HybridConfiguration` cmdlet 작업을 처리하는 하이브리드 구성 엔진은 *HybridConfiguration*Active Directory 개체의 상태와 현재 온-프레미스 Exchange 및 Exchange Online 구성 설정을 비교한 다음 배포 구성 설정을 *HybridConfiguration*Active Directory 개체에 정의된 매개 변수에 일치시키는 작업을 실행합니다. 현재 온-프레미스 Exchange 및 Exchange Online 배포 구성 상태가 *HybridConfiguration*Active Directory 개체에 정의된 설정과 일치하는 경우 하이브리드 구성 엔진이 온-프레미스 또는 Exchange Online 조직을 변경하지 않습니다.

기존 하이브리드 배포를 업데이트할 때 하이브리드 구성 엔진이 다음 단계를 수행합니다.

1.  *Update-HybridConfiguration* cmdlet이 하이브리드 구성 엔진이 시작되도록 트리거합니다.

2.  하이브리드 구성 엔진이 `HybridConfiguration`Active Directory 개체에 저장된 "필요한 상태"를 읽습니다.

3.  하이브리드 구성 엔진이 온-프레미스 Exchange 조직에서 토폴로지 데이터와 현재 구성을 찾습니다.

4.  하이브리드 구성 엔진이 Exchange Online 조직에서 토폴로지 데이터와 현재 구성을 찾습니다.

5.  하이브리드 구성 엔진이 필요한 상태, 토폴로지 데이터 및 현재 구성을 기반으로 온-프레미스 Exchange 조직과 Exchange Online 조직 간의 "차이"를 설정한 다음, 구성 작업을 실행하여 필요한 상태를 설정합니다.

다음 그림은 하이브리드 구성 엔진이 하이브리드 배포 프로세스 중에 온-프레미스 Exchange 서버와 Exchange Online 구성 설정을 검색하고 수정하는 방법을 요약해서 보여줍니다.

![하이브리드 구성 엔진 흐름](images/Hh529921.7e01b239-b978-4377-9eac-aa5bc4561866(EXCHG.150).gif "하이브리드 구성 엔진 흐름")

