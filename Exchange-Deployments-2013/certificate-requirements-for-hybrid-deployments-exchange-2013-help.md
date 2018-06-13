---
title: '하이브리드 배포를 위한 인증서 요구 사항: Exchange 2013 Help'
TOCTitle: 하이브리드 배포를 위한 인증서 요구 사항
ms:assetid: 48d532cc-29f9-4009-9d2d-f19a9c13c320
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh563848(v=EXCHG.150)
ms:contentKeyID: 50484629
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 하이브리드 배포를 위한 인증서 요구 사항

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

하이브리드 배포에서 디지털 인증서는 온-프레미스 Exchange 조직과 Office 365 간 통신의 보안을 유지하기 위한 중요한 부분입니다. 인증서를 사용하면 각 Exchange 조직은 상대방을 신뢰할 수 있습니다. 인증서는 또한 각 Exchange 조직이 올바른 소스와 통신하도록 보장합니다.

하이브리드 배포에서는 많은 서비스가 인증서를 사용합니다.

  - **AD FS(Active Directory Federation Services)를 사용하는 Azure AD Connect(Azure Active Directory Connect)**   AD FS를 사용하는 Azure AD Connect를 하이브리드 배포의 일부로서 배포하는 경우, 웹 클라이언트와 페더레이션 서버 프록시 사이의 트러스트를 설정하고, 보안 토큰에 서명하고, 보안 토큰을 해독하는 데에는 신뢰할 수 있는 타사 CA(인증 기관)에서 발급한 인증서가 사용됩니다.
    
    자세한 내용은 [인증서](http://go.microsoft.com/fwlink/p/?linkid=205993)를 참조하십시오.

  - **Exchange 페더레이션**   온-프레미스 Exchange 서버와 Azure Active Directory 인증 시스템 간 보안 연결을 만드는 데에는 자체 서명된 인증서가 사용됩니다.
    
    자세한 내용은 [공유](https://technet.microsoft.com/ko-kr/library/dd638083\(v=exchg.150\))를 참조하십시오.

  - **Exchange 서비스**Exchange 서버와 클라이언트 사이의 보안 SSL(Secure Sockets Layer) 통신을 지원하는 데에는 신뢰할 수 있는 타사 CA에서 발급된 인증서가 사용됩니다. 인증서를 사용하는 서비스에는 웹에서 Outlook, Exchange ActiveSync, 외부에서 Outlook 사용 및 보안 메시지 전송이 포함됩니다.

  - **기존 Exchange 서버**   기존 Exchange 서버에서는 인증서를 사용하여 보안 웹에서 Outlook 통신, 메시지 전송 등을 지원할 수 있습니다. Exchange 서버에서 인증서를 사용하는 방법에 따라 자체 서명된 인증서를 사용할 수도 있고 신뢰할 수 있는 타사 CA에서 발급된 인증서를 사용할 수도 있습니다.

## 하이브리드 배포를 위한 인증서 요구 사항

하이브리드 배포를 구성할 때에는 신뢰할 수 있는 타사 CA에서 구매한 인증서를 사용하고 구성해야 합니다. 하이브리드 보안 메일 전송에 사용되는 인증서를 모든 온-프레미스 사서함(Exchange 2016 이상), 사서함 및 클라이언트 액세스(Exchange 2013 및 이전) 서버에 설치해야 합니다.


> [!IMPORTANT]
> 여러 Active Directory 포리스트에 Exchange 서버가 배포된 조직에 하이브리드 배포를 구성하려면 Active Directory 포리스트<EM>마다</EM> 별도의 타사 CA 인증서를 사용해야 합니다.




> [!NOTE]
> Exchange Edge 전송 서버를 온-프레미스 조직에 배포하는 경우 이 인증서를 모든 Edge 전송 서버에도 설치해야 합니다. 하이브리드 보안 메일이 올바르게 작동하도록 하려면 각 전송 서버에서 동일한 발급 CA 및 동일한 주체를 공유하는 인증서를 사용해야 합니다.



ADFS, Exchange 페더레이션, 서비스 및 Exchange 등의 여러 서비스에 각각 인증서가 필요합니다. 조직에 따라 다음 중 하나를 선택할 수 있습니다.

  - 여러 서버의 모든 서비스에 타사 인증서 사용

  - 서비스를 제공하는 각 서버에 대해 타사 인증서 사용

모든 서비스에 대해 동일한 인증서를 사용할지 또는 각 서비스에 대해 전용 인증서를 사용할지는 조직 및 구현하는 서비스에 따라 결정됩니다. 각 옵션에 대해 고려해야 할 몇 가지 사항은 다음과 같습니다.

  - **여러 서버에서 단일 타사 인증서 사용**   여러 서버의 모든 서비스에 대해 단일 타사 인증서를 사용하는 경우 비용은 다소 저렴할지라도 갱신과 교체가 복잡할 수 있습니다. 복잡한 이유는 교체가 필요할 때마다 인증서가 설치된 모든 서버에서 인증서를 교체해야 하기 때문입니다.

  - **각 서버에 대해 단일 타사 인증서 사용**   서비스를 호스트하는 각 서버에 대해 전용 인증서를 사용하면 해당 서버의 서비스에 대해서만 특별히 인증서를 구성할 수 있습니다. 인증서를 교체하거나 갱신해야 하는 경우 서비스가 설치된 서버에서만 교체하면 됩니다. 다른 서버에는 영향을 주지 않습니다.

선택적인 ADFS 서버에는 전용 타사 인증서를 사용하고, 하이브리드 배포용 Exchange 서비스에는 또 다른 인증서를 사용하고, 필요한 경우 기타 필요한 서비스나 기능용 Exchange 서버에도 별도의 인증서를 사용하는 것이 좋습니다. 하이브리드 배포에서 페더레이션된 공유의 일부로 구성된 온-프레미스 페더레이션 트러스트는 기본적으로 자체 서명된 인증서를 사용합니다. 특정 요구 사항이 없는 경우 하이브리드 배포의 일부로 구성된 페더레이션 트러스트에 타사 인증서를 사용할 필요가 없습니다.

단일 서버에 서비스가 설치된 경우 해당 서버에 대해 여러 개의 FQDN(정규화된 도메인 이름)을 구성해야 할 수도 있습니다. 필요한 최대 수의 FQDN을 사용할 수 있는 인증서를 구매해야 합니다. 인증서는 주체(또는 사용자 이름으로도 불림) 및 하나 이상의 SAN(주체 대체 이름)으로 구성됩니다. 주체 이름은 인증서가 발급된 FQDN이며, 온-프레미스 조직과 Exchange Online 조직 간에 공유하는 기본 SMTP 도메인을 사용해야 합니다. SAN은 주체 이름 외에 인증서에 추가할 수 있는 추가 FQDN입니다. 5개의 FQDN을 지원하는 인증서가 필요한 경우 5개의 도메인을 추가할 수 있는 인증서를 구입해야 합니다. 이 경우 하나는 주체 이름이고 4개는 SAN입니다.

다음 표에는 하이브리드 배포에 사용하도록 구성된 인증서에 포함해야 할 최소한의 제안 FQDN이 요약되어 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>서비스</th>
<th>FQDN 제안</th>
<th>필드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 공유 SMTP 도메인</p></td>
<td><p>contoso.com</p></td>
<td><p>주체 이름</p></td>
</tr>
<tr class="even">
<td><p>자동 검색</p></td>
<td><p>Exchange 2013 클라이언트 액세스 서버의 외부 자동 검색 FQDN과 일치하는 레이블(예: autodiscover.contoso.com)</p></td>
<td><p>주체 대체 이름</p></td>
</tr>
<tr class="odd">
<td><p>전송</p></td>
<td><p>Edge 전송 서버의 외부 FQDN과 일치하는 레이블(예: edge.contoso.com)</p></td>
<td><p>주체 대체 이름</p></td>
</tr>
</tbody>
</table>

