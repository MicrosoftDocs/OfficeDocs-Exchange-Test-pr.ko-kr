---
title: '하이브리드 배포 필수 구성 요소: Exchange 2013 Help'
TOCTitle: 하이브리드 배포 필수 구성 요소
ms:assetid: e7454db0-fed4-4662-8890-9501126b1ba2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh534377(v=EXCHG.150)
ms:contentKeyID: 50484642
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 하이브리드 배포 필수 구성 요소

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2017-07-25_

**요약:** 하이브리드 배포를 설정하기 전에 Exchange 환경에 필요한 항목에 대해 설명합니다.

하이브리드 구성 마법사를 사용하여 하이브리드 배포를 만들고 구성하기 전에 기존 온-프레미스 Exchange 조직이 특정 요구 사항을 충족해야 합니다. 이러한 요구 사항이 충족되지 않으면 하이브리드 구성 마법사 내의 각 단계를 완료할 수 없으며 온-프레미스 Exchange 조직과 Exchange Online 간에 하이브리드 배포를 구성할 수 없습니다.

## 하이브리드 배포의 필수 구성 요소

하이브리드 배포를 구성하려면 다음과 같은 필수 구성 요소가 필요합니다.

  - **온-프레미스 Exchange 조직**   하이브리드 배포는 온-프레미스 Exchange 2007 이상의 기반 조직에 대해 구성할 수 있습니다.
    
    온-프레미스 조직에 설치한 Exchange 버전이 설치할 수 있는 하이브리드 배포 버전을 결정합니다. 일반적으로 조직에서 지원되는 최신 하이브리드 배포 버전을 구성해야 합니다. 예를 들어, 온-프레미스 조직에서 Exchange 2007을 실행 중인 경우 Exchange 2013 기반 하이브리드 배포를 구성해야 합니다. 엔터프라이즈 하이브리드 배포 호환성에 대한 Exchange Server 및 Office 365의 완전한 목록은 다음 표를 참조하세요.
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>온-프레미스 환경</th>
    <th>Exchange 2016 기반 하이브리드 배포</th>
    <th>Exchange 2013 기반 하이브리드 배포</th>
    <th>Exchange 2010 기반 하이브리드 배포</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Exchange 2016</p></td>
    <td><p>지원됨</p></td>
    <td><p>지원되지 않음</p></td>
    <td><p>지원되지 않음</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2013</p></td>
    <td><p>지원됨</p></td>
    <td><p>지원됨</p></td>
    <td><p>지원되지 않음</p></td>
    </tr>
    <tr class="odd">
    <td><p>Exchange 2010</p></td>
    <td><p>지원됨</p></td>
    <td><p>지원</p></td>
    <td><p>지원됨</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2007</p></td>
    <td><p>지원되지 않음</p></td>
    <td><p>지원됨</p></td>
    <td><p>지원됨</p></td>
    </tr>
    </tbody>
    </table>


  - **온-프레미스 Exchange 릴리스** 하이브리드 배포를 사용하려면 온-프레미스 조직에 설치한 Exchange 버전에 사용할 수 있는 최신 누적 업데이트 또는 업데이트 롤업이 필요합니다. 최신 누적 업데이트 또는 업데이트 롤업을 설치할 수 없으면, 바로 이전 릴리스도 지원됩니다. 오래된 누적 업데이트 또는 업데이트 롤업은 지원되지 않습니다.
    
    예를 들어 온-프레미스 조직에 Exchange 2013 누적 업데이트 8을 설치했다고 가정하면, 사용할 수 있는 가장 최근 Exchange 2013 릴리스는 누적 업데이트 10입니다. 지원되는 하이브리드 구성에 남아 있으려면, Exchange 2013을 최신 누적 업데이트 9로 업그레이드해야 합니다. 하지만 누적 업데이트 10으로 업그레이드하는 것이 가장 좋습니다.
    
    누적 업데이트 및 업데이트 롤업은 분기별로 릴리스됩니다. 따라서 서버에 최신 누적 업데이트 또는 업데이트 롤업을 적용하면 업그레이드를 완료해야 할 추가 시간이 주기적으로 필요한 경우 유연성을 추가로 확보할 수 있습니다.

  - **온-프레미스 서버 역할** 온-프레미스 조직에 설치해야 하는 서버 역할은 설치한 Exchange 버전에 따라 다릅니다.
    
      - **Exchange 2010** 사서함, 허브 전송, 클라이언트 액세스 서버 역할이 설치된 서버 한 개 이상. 사서함, 허브 전송, 클라이언트 액세스 역할을 별도 서버에 설치할 수도 있지만, 이러한 모든 역할을 각 서버에 설치해 추가 유연성과 개선된 성능을 확보하는 것이 좋습니다.
    
      - **Exchange 2013** 사서함 및 클라이언트 액세스 서버 역할이 설치된 서버 한 개 이상. 사서함 및 클라이언트 액세스 역할을 별도 서버에 설치할 수도 있지만, 두 가지 역할을 각 서버에 모두 설치해 추가 유연성과 개선된 성능을 확보하는 것이 좋습니다.
    
      - **Exchange 2016 이상** 사서함 서버 역할이 설치된 서버 한 개 이상.
    
    하이브리드 배포는 Edge 전송 서버 역할을 실행하는 Exchange Server도 지원합니다. 또한 Edge 전송 서버는 설치한 Exchange 버전의 최신 누적 업데이트 또는 업데이트 롤업으로 업데이트해야 합니다. 경계 네트워크에 Edge 전송 서버를 배포하는 것이 좋습니다. 사서함 및 클라이언트 액세스 서버는 경계 네트워크에서 배포할 수 없습니다.

  - **Office 365**   하이브리드 배포는 Azure Active Directory 동기화를 지원하는 모든 Office 365 계획에서 지원됩니다. Office 365 Enterprise/Government/Academic/Midsize 계획은 모두 하이브리드 배포를 지원하지만, Office 365 Business/Home 계획은 하이브리드 배포를 지원하지 않습니다.
    
    자세한 내용은 [Office 365 등록](https://go.microsoft.com/fwlink/p/?linkid=203981)을 참조하세요.

  - **사용자 지정 도메인**   하이브리드 배포에서 사용할 모든 사용자 지정 도메인을 Office 365에 등록합니다. 이렇게 하려면 Office 365 관리 포털을 사용하거나, 경우에 따라 온-프레미스 조직에서 AD FS(Active Directory Federation Services)를 구성합니다.
    
    자세한 내용은 [Office 365에 도메인 추가](https://go.microsoft.com/fwlink/p/?linkid=229238)를 참조하세요.

  - **Active Directory 동기화**   온-프레미스 조직과의 Active Directory 동기화를 사용하도록 설정하기 위해 Azure Active Directory Connect 도구를 배포합니다.
    
    [Azure AD Connect 사용자 로그인 옵션](http://go.microsoft.com/fwlink/p/?linkid=723514)에서 자세히 알아보세요.

  - **자동 검색 DNS 레코드**   온-프레미스 Exchange 2013 클라이언트 액세스 서버를 가리키는 기존 SMTP 도메인에 대한 자동 검색 공용 DNS 레코드를 구성합니다.

  - **EAC(Exchange 관리 센터)의 Office 365 조직**   Office 365 조직 노드는 기본적으로 온-프레미스 EAC에 포함되어 있지만, 하이브리드 구성 마법사를 사용하려면 먼저 Office 365 관리자 자격 증명을 사용해 EAC를 Office 365 조직에 연결해야 합니다. 이렇게 하면 단일 관리 콘솔에서 온-프레미스 및 Exchange Online 조직을 모두 관리할 수 있습니다.
    
    자세한 내용은 [Exchange 하이브리드 배포에서 하이브리드 관리](hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md)를 참조하십시오.

  - 
    
    **인증서**   Exchange 서비스를 설치하고 신뢰할 수 있는 공용 CA(인증 기관)에서 구입한 유효한 디지털 인증서에 할당합니다. Microsoft 페더레이션 게이트웨이를 통해 온-프레미스 페더레이션 트러스트에 자체 서명된 인증서를 사용해야 하지만 하이브리드 배포의 Exchange 서비스에는 자체 서명된 인증서를 사용할 수 없습니다. 하이브리드 배포에 구성된 Exchange 서버의 IIS(인터넷 정보 서비스) 인스턴스에는 신뢰할 수 있는 CA에서 구입한 유효한 디지털 인증서가 있어야 합니다. 또한 EWS 외부 URL 및 공용 DNS에 지정된 자동 검색 끝점이 인증서의 SAN(주체 대체 이름)에 나열되어야 합니다. 하이브리드 배포에서 메일 전송에 사용하기 위해 Exchange 서버에 설치한 인증서는 모두 동일해야 합니다. 즉, 동일한 CA에서 발급한 것이어야 하며 동일한 주체를 가지고 있어야 합니다.
    
    자세한 내용은 [하이브리드 배포를 위한 인증서 요구 사항](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)를 참조하십시오.

  - **EdgeSync**   온-프레미스 조직에 Edge 전송 서버를 배포했으며 하이브리드 보안 메일 전송을 위해 Edge 전송 서버를 구성하려는 경우, 하이브리드 구성 마법사를 사용하기 전에 먼저 EdgeSync를 구성해야 합니다. 또한 Edge 전송 서버에 새 누적 업데이트 또는 업데이트 롤업을 적용할 때마다 EdgeSync도 실행해야 합니다.
    

    > [!IMPORTANT]
    > EdgeSync는 Edge 전송 서버를 사용한 배포에서 필수 요소지만, 하이브리드 보안 메일 전송을 위해 Edge 전송 서버를 구성할 경우 추가적인 수동 전송 구성 설정이 필요합니다.

    
    자세한 내용은 [하이브리드 배포의 Edge 전송 서버](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md)를 참조하십시오.

  - **UM(통합 메시징) 사용 가능 사서함** UM 사용 가능 사서함이 있고 이 사서함을 Office 365로 이동하려는 경우 Exchange 하이브리드 배포 외에 다음이 필요합니다. UM 사용 가능 사서함을 Office 365로 이동하기 **전에** 이러한 요구 사항을 충족해야 합니다.
    
      - 온-프레미스 전화 통신 시스템과 통합된 Lync Server 2010 Lync Server 2013 또는 비즈니스용 Skype 서버 2015 이상 **또는**
    
      - 온-프레미스 전화 통신 시스템과 통합된 비즈니스용 Skype Online **또는**
    
      - 기존의 온-프레미스 PBX 또는 IP-PBX 솔루션
    
      - Exchange Online에서 만들었으며 온-프레미스 조직에서 UM 사서함 정책의 이름을 반영하는 UM 사서함 정책
        

        > [!NOTE]
        > 여러 온-프레미스 UM 사서함 정책을 Exchange Online의 단일 UM 사서함 정책에 매핑할 수 있습니다. 이렇게 하려면 Exchange 관리 셸을 사용하여 각 온-프레미스 UM 사서함 정책을 Exchange Online 정책을 수동으로 매핑해야 합니다.

    
    자세한 내용은 [Um 전화 시스템 통합](https://technet.microsoft.com/ko-kr/library/jj673558\(v=exchg.150\)), [Exchange 2013에 대 한 전화 통신 관리자](https://technet.microsoft.com/ko-kr/library/ee364753\(v=exchg.150\)) 및 [클라우드 PBX 음성 메일 설정](https://go.microsoft.com/fwlink/p/?linkid=826207)을 참조하세요.

## 하이브리드 배포 프로토콜, 포트 및 끝점

하이브리드 배포 기능 및 구성 요소가 올바르게 작동하려면 특정 들어오는 프로토콜, 포트 및 연결 끝점에서 Office 365에 액세스할 수 있어야 합니다. 하이브리드 배포를 구성하기 전에 온-프레미스 네트워크 및 보안 구성에서 아래 표의 기능 및 구성 요소를 지원하는지 확인합니다. 특정 인바운드 프로토콜, 포트 및 끝점을 허용하는 것 외에, 네트워크에 있는 컴퓨터가 [Office 365 URL 및 IP 주소 범위](https://go.microsoft.com/fwlink/?linkid=823100)에 나열된 IP 주소, 포트 및 URL에 액세스할 수 있어야 합니다.


<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>전송 프로토콜</th>
<th>상위 수준 프로토콜</th>
<th>기능/구성 요소</th>
<th>온-프레미스 끝점</th>
<th>온-프레미스 경로</th>
<th>인증 공급자</th>
<th>권한 부여 방법</th>
<th>사전 인증 지원</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP 25(SMTP)</p></td>
<td><p>SMTP/TLS</p></td>
<td><p>Office 365와 온-프레미스 간의 메일 흐름</p></td>
<td><p>Exchange 2016 사서함/Edge</p>
<p>Exchange 2013 CAS/Edge</p>
<p>Exchange 2010 HUB/EDGE</p></td>
<td><p>해당 없음</p></td>
<td><p>해당 없음</p></td>
<td><p>인증서 기반</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>TCP 443(HTTPS)</p></td>
<td><p>자동 검색</p></td>
<td><p>자동 검색</p></td>
<td><p>Exchange 2016 사서함</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Azure AD 인증 시스템</p></td>
<td><p>WS-Security 인증</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443(HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>약속 있음/없음, 메일 설명, 메시지 추적</p></td>
<td><p>Exchange 2016 사서함</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p></td>
<td><p>Azure AD 인증 시스템</p></td>
<td><p>WS-Security 인증</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>TCP 443(HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>여러 사서함 검색</p></td>
<td><p>Exchange 2016 사서함</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>인증 서버</p></td>
<td><p>WS-Security 인증</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443(HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>사서함 마이그레이션</p></td>
<td><p>Exchange 2016 사서함</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/mrsproxy.svc</p></td>
<td><p>NTLM</p></td>
<td><p>기본</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>TCP 443(HTTPS)</p></td>
<td><p>자동 검색</p>
<p>EWS</p></td>
<td><p>OAuth</p></td>
<td><p>Exchange 2016 사서함</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>인증 서버</p></td>
<td><p>WS-Security 인증</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443(HTTPS)</p></td>
<td><p>해당 없음</p></td>
<td><p>AD FS(Windows에 포함)</p></td>
<td><p>Windows 2008/2012 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Azure AD 인증 시스템</p></td>
<td><p>구성에 따라 다름</p></td>
<td><p>2단계</p></td>
</tr>
<tr class="even">
<td><p>TCP 443(HTTPS)</p></td>
<td><p>해당 없음</p></td>
<td><p>AD FS를 사용하는 Azure Active Directory Connect</p></td>
<td><p>Windows 2012 R2 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Azure AD 인증 시스템</p></td>
<td><p>구성에 따라 다름</p></td>
<td><p>2단계</p></td>
</tr>
</tbody>
</table>


## 권장 도구 및 서비스

하이브리드 구성 마법사로 하이브리드 배포를 구성할 때 앞에서 설명한 필수 구성 요소 외에 다음과 같은 다른 도구 및 서비스를 사용하면 유용합니다.

  - **Exchange Server 배포 도우미**   Exchange Server 배포 도우미는 온-프레미스 조직에 Exchange을 배포하거나, 온-프레미스 조직과 Office 365 간에 하이브리드 배포를 구성하거나, Office 365로 완전히 마이그레이션하도록 도와주는 무료 웹 기반 도구입니다. 이 도구는 몇 가지 간단한 사항을 질문하고 사용자의 대답에 따라 Exchange Server를 배포하거나 구성하기 위한 지침이 포함된 사용자 지정 검사 목록을 만듭니다. 배포 도우미는 하이브리드 배포를 구성하는 데 필요한 올바른 정보를 정확히 제공합니다.
    
    자세한 내용은 [Exchange Server 배포 도우미](https://technet.microsoft.com/exdeploy2013)를 참조하세요.
    
     

  - **원격 연결 분석기 도구**   Microsoft 원격 연결 분석기 도구는 온-프레미스 Exchange 조직의 외부 연결을 확인하여 하이브리드 배포를 구성할 준비가 되었는지 확인합니다. 하이브리드 구성 마법사로 하이브리드 배포를 구성하기 전에 원격 연결 분석기 도구를 사용하여 온-프레미스 조직을 확인하는 것이 좋습니다.
    
    자세한 내용은 [Microsoft Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/)를 참조하십시오.
    
     

  - **Single Sign-On**   Single Sign-On을 사용하면 사용자가 단일 사용자 이름 및 암호로 온-프레미스 및 Exchange Online 조직 모두에 액세스할 수 있습니다. Single Sign-On은 사용자에게 익숙한 로그온 환경을 제공하고 이를 통해 관리자는 온-프레미스 Active Directory 관리 도구를 사용하여 Exchange Online 조직 사서함에 대한 계정 정책을 쉽게 제어할 수 있습니다.
    
    Single Sign-On을 배포할 때 암호 동기화 및 Active Directory Federation Services의 두 가지 옵션이 있습니다. 두 옵션은 Azure Active Directory Connect에서 제공됩니다. 암호 동기화는 규모에 관계 없이 거의 모든 조직에서 Single Sign-On을 쉽게 구현할 수 있도록 합니다. 그뿐 아니라 하이브리드 배포의 사용자 환경이 Single Sign-On을 설정하는 경우보다 훨씬 더 나으므로 이 방식을 구현할 것을 강력히 권장합니다. 하이브리드 배포에 참가해야 하는 여러 Active Directory 포리스트가 있는 대규모 조직에는 Active Directory Federation Services가 필요합니다.
    
    자세한 내용은 다음을 참조하세요. [하이브리드 배포 SSO(Single Sign-On)](single-sign-on-with-hybrid-deployments-exchange-2013-help.md)

