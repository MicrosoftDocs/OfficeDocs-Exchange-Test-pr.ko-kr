---
title: 'Exchange 2013/Exchange 2007 하이브리드 배포에서의 전송 옵션: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2007 하이브리드 배포에서의 전송 옵션
ms:assetid: 92d9e3ca-8d79-4872-9ff7-0067fcdbd434
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn151301(v=EXCHG.150)
ms:contentKeyID: 54651853
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2007 하이브리드 배포에서의 전송 옵션

이 항목은 진행 중입니다.  

_**적용 대상:**Exchange Online, Exchange Server, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

하이브리드 배포에서는 사서함이 온-프레미스 Exchange 조직에 있을 수도 있고 Exchange Online 조직에 있을 수도 있습니다. 이러한 두 개의 별도 조직을 사용자 및 두 조직 간에 교환되는 메시지에 하나의 결합된 조직으로 나타나게 하는 중요 구성 요소는 하이브리드 전송입니다. 하이브리드 전송을 사용하면 한 조직에서 받는 사람 간에 전송된 메시지가 TLS(전송 계층 보안)를 사용하여 인증, 암호화 및 전송되며 전송 규칙, 저널링 및 스팸 방지 정책과 같은 Exchange 구성 요소에 "내부"로 표시됩니다. Exchange 2013의 하이브리드 구성 마법사가 하이브리드 전송을 자동으로 구성합니다.

하이브리드 구성 마법사에서 하이브리드 전송을 구성하려면 Exchange Online 조직의 전송을 처리하는 Microsoft EOP(Exchange Online Protection)에서의 연결을 허용하는 온-프레미스 SMTP 끝점이 Exchange 2013 클라이언트 액세스 서버, Exchange 2013 Edge 전송 서버 또는 Exchange Server 2010 SP3(서비스 팩 3) Edge 전송 서버여야 합니다.


> [!IMPORTANT]
> 온-프레미스 Exchange 2013 클라이언트 액세스 서버 또는 Exchange 2013/Exchange 2010 SP3 Edge 전송 서버와 EOP 간에 다른 SMTP 호스트 또는 서비스가 있어서는 안 됩니다. 하이브리드 전송 기능을 사용하는 메시지에 추가된 정보는 Exchange 2013 이외의 서버, Exchange 2010 SP3 이전 서버 또는 SMTP 호스트를 통과할 때 제거됩니다. 조직에 배포된 Exchange 2010 SP2 Edge 전송 서버를 하이브리드 전송에 사용하려면 Exchange 2010 SP3으로 업그레이드해야 합니다.



외부 인터넷 보낸 사람이 두 조직의 받는 사람에게 보낸 인바운드 메시지는 일반적인 인바운드 라우팅을 따릅니다. 조직에서 외부 인터넷 받는 사람에게 보낸 아웃바운드 메시지는 일반적인 아웃바운드 경로를 따르거나 독립적인 라우팅을 통해 보낼 수 있습니다.

하이브리드 배포를 계획하고 구성할 때에는 인바운드 및 아웃바운드 메일의 라우팅 방법을 선택해야 합니다. 온-프레미스 조직 및 Exchange Online 조직의 받는 사람이 보내고 받는 인바운드 및 아웃바운드 메시지에 사용되는 경로는 다음에 따라 달라집니다.

  - 온-프레미스 사서함과 Exchange Online 사서함 모두의 인바운드 인터넷 메일이 Microsoft Office 365와 EOP 또는 온-프레미스 조직을 통과하도록 라우팅하시겠습니까?
    
    온-프레미스 조직 또는 EOP와 Exchange Online 조직을 통해 두 조직에 대한 인바운드 인터넷 메일을 라우팅하도록 선택할 수 있습니다. 두 조직에 대해 인바운드 메시지를 라우팅하는 것은 하이브리드 배포에서 중앙 집중식 메일 전송을 사용하는지 여부에 따라 달라집니다.

  - Exchange Online 조직에서 외부 받는 사람에게 보내는 아웃바운드 메일을 온-프레미스 조직을 통해 라우팅하시겠습니까(중앙 집중식 메일 전송), 아니면 인터넷으로 직접 라우팅하시겠습니까?
    
    중앙 집중식 메일 전송에 의하면 Exchange Online 조직의 사서함에 있는 모든 메일을 인터넷으로 배달하기 전에 온-프레미스 조직을 통해 라우팅할 수 있습니다. 이 방법은 인터넷에서 주고받는 모든 메일을 온-프레미스 서버에서 처리해야 하는 규정 준수 시나리오에서 유용합니다. 또는 외부 받는 사람에 대한 메시지를 인터넷에 배달하도록 Exchange Online을 구성할 수 있습니다.
    

    > [!NOTE]
    > 중앙 집중식 메일 전송은 특정 준수 관련 전송 요구가 있는 조직에만 권장됩니다. 일반적인 Exchange 조직은 중앙 집중식 메일 전송을 사용하지 않는 것이 좋습니다.



  - 온-프레미스 조직에 Edge 전송 서버를 배포하시겠습니까?
    
    도메인에 구독된 내부 Exchange 2013 서버가 인터넷에 직접 노출되지 않도록 하려는 경우 경계 네트워크에 Exchange 2013 Edge 전송 서버 또는 Exchange 2010 SP3 Edge 전송 서버를 배포할 수 있습니다. Edge 전송 서버를 하이브리드 배포에 추가하는 방법에 대한 자세한 내용은 [Exchange 2013/Exchange 2007 하이브리드 배포의 Edge 전송 서버](edge-transport-servers-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md)를 참조하십시오.

인터넷으로 메시지를 라우팅하는지 여부와 상관없이 온-프레미스 조직과 Exchange Online 조직 간에 전송된 모든 메시지는 보안 전송을 사용하여 전송됩니다. 자세한 내용은 이 항목 뒷부분의 [Trusted communication](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md)을 참조하십시오.

이러한 옵션이 조직의 메시지 라우팅에 미치는 영향에 대한 자세한 내용은 [Exchange 2013/Exchange 2007 하이브리드 배포의 전송 라우팅](transport-routing-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md)을 참조하십시오.

## 하이브리드 배포에서 Exchange Online Protection

EOP는 Microsoft에서 제공하는 온라인 서비스이며 바이러스, 스팸, 피싱 메일 및 정책 위반으로부터 많은 회사의 온-프레미스 조직을 보호하는 데 사용됩니다. Office 365에서 EOP는 Exchange Online 조직을 같은 위협으로부터 보호하는 데 사용됩니다. Office 365에 등록하면 Exchange Online 조직에 연결된 EOP 회사가 자동으로 만들어집니다.

EOP 회사에는 Exchange Online 조직에 대해 구성할 수 있는 메일 전송 설정이 여러 개 있습니다. 특정 IP 주소에서 받아야 하는 SMTP 도메인, TLS 및 SSL(Secure Sockets Layer) 인증서가 필요한 SMTP 도메인 또는 준수 정책 등을 무시할 수 있는 SMTP 도메인을 지정할 수 있습니다. EOP는 Exchange Online 조직의 정문과도 같습니다. 모든 메시지는 출처에 관계없이 Exchange Online 조직의 사서함에 도달하기 전에 EOP를 통과해야 합니다. 또한 Exchange Online 조직에서 보낸 모든 메시지는 인터넷에 도달하기 전에 EOP를 거쳐야 합니다.

하이브리드 구성 마법사로 하이브리드 배포를 구성하면, 모든 전송 설정이 Exchange Online 조직에 포함된 EOP 회사와 온-프레미스 조직에서 자동으로 구성됩니다. 하이브리드 구성 마법사는 온-프레미스와 Exchange Online 조직 간에 전송된 메시지를 보호하고 올바른 대상으로 메시지를 라우팅하도록 이 EOP 회사에 모든 인바운드 및 아웃바운드 연결과 기타 설정을 구성합니다. Exchange Online 조직에 대해 사용자 지정 전송 설정을 구성하려면 이 EOP 회사에서도 이러한 설정을 구성해야 합니다.

## 신뢰할 수 있는 통신

온-프레미스 조직과 Exchange Online 조직의 받는 사람을 보호하고 두 조직 간에 보낸 메시지를 가로채거나 읽지 못하게 하기 위해, 온-프레미스 조직과 EOP 간 전송에 강제 적용된 TLS를 사용하도록 구성됩니다. TLS 전송은 타사 CA(인증 기관)에서 제공한 SSL(Secure Sockets Layer) 인증서를 사용합니다. EOP와 Exchange Online 조직 간 메시지에도 TLS를 사용합니다.

강제 TLS 전송을 사용하는 경우 보내는 서버와 받는 서버는 다른 서버에 구성된 인증서를 검사합니다. 인증서에서 구성된 주체 이름 또는 SAN(주체 대체 이름) 중 하나는 관리자가 다른 서버에서 명시적으로 지정한 FQDN과 일치해야 합니다. 예를 들어 EOP가 mail.contoso.com FQDN에서 전송된 메시지를 수락 및 보호하도록 구성된 경우 보내는 온-프레미스 클라이언트 액세스 또는 Edge 전송 서버는 주체 이름이나 SAN에서 mail.contoso.com이 포함된 SSL 인증서를 가져야 합니다. 이 요구 사항이 충족되지 않으면 EOP에서 연결이 거부됩니다.


> [!NOTE]
> 사용되는 FQDN이 받는 사람의 전자 메일 도메인 이름과 일치할 필요는 없습니다. 유일한 요구 사항은 인증서 주체 이름 또는 SAN의 FQDN이 받거나 보내는 서버에서 수락하도록 구성된 FQDN과 일치해야 한다는 것입니다.



TLS를 사용하는 것 외에도 조직 간의 메시지가 "내부" 메시지로 취급됩니다. 이러한 방법 덕분에 메시지는 스팸 방지 설정 및 다른 서비스를 무시할 수 있습니다.

SSL 인증서 및 도메인 보안에 대한 자세한 내용은 [하이브리드 배포를 위한 인증서 요구 사항](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md) 및 [TLS 인증서 이해](http://go.microsoft.com/fwlink/p/?linkid=187237)를 참조하십시오.

