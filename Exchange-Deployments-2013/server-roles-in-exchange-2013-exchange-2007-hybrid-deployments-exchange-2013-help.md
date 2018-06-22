---
title: 'Exchange 2013/Exchange 2007 하이브리드 배포에서의 서버 역할: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2007 하이브리드 배포에서의 서버 역할
ms:assetid: d7104efe-6d2a-4260-bc4e-f05da477e30b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn151302(v=EXCHG.150)
ms:contentKeyID: 54651855
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2007 하이브리드 배포에서의 서버 역할

이 항목은 진행 중입니다.  

_<strong>적용 대상:</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong>2016-12-09_

Exchange 2007 조직에서 하이브리드 배포를 구성할 때는 기존 Exchange 2007 조직에서 클라이언트 액세스 서버 역할 및 사서함 서버 역할과 함께 Exchange 2013 서버를 하나 이상 설치해야 합니다. Exchange 2013 클라이언트 액세스 서버 및 사서함 서버는 기존 Exchange 2007 온-프레미스 조직과 Exchange Online 조직 간의 통신을 조정합니다. 이 통신에는 온-프레미스 조직과 Exchange Online 조직 사이의 메시지 전송 및 메시징 기능이 포함됩니다.

온-프레미스 조직에 Exchange 2013 서버를 둘 이상 설치하여 하이브리드 배포 기능의 안정성과 가용성을 높이는 것이 좋습니다.

## 하이브리드 배포에서 서버 역할

다음은 하이브리드 배포에서 Exchange 2013 서버 역할에 대한 간단한 개요입니다.

  - **클라이언트 액세스 서버 역할**   Exchange 2013 클라이언트 액세스 서버 역할은 일반적으로 조직의 Exchange 2007 클라이언트 액세스 서버를 통해 제공되는 것과 같은 대부분의 기능과, 하이브리드 배포 및 Exchange 2007과의 동시 사용을 지원하는 데 필요한 몇 가지 추가 기능을 제공합니다. 또한 클라이언트 액세스 서버는 Exchange Online 조직에서 온-프레미스 조직으로 보내는 보안 메일 메시지를 처리하며, 하이브리드 배포의 전송 규칙, 저널링 정책 및 사서함 서버로의 메시지 배달도 처리합니다. 보안 하이브리드 메일 전송을 지원하기 위해 클라이언트 액세스 서버에 전용 수신 커넥터가 기본적으로 구성됩니다. Outlook 클라이언트 액세스, Outlook Web App 및 외부에서 Outlook 사용을 비롯한 모든 클라이언트 연결은 클라이언트 액세스 서버 역할을 통과합니다. 약속 있음/없음 공유와 같은 온-프레미스 조직과 Exchange Online 조직 간의 조직 관계 기능도 클라이언트 액세스 서버 역할에 의해 처리됩니다.
    
    자세한 내용은 [클라이언트 액세스 서버](https://technet.microsoft.com/ko-kr/library/dd298114\(v=exchg.150\))를 참조하십시오.

  - **사서함 서버 역할**   Exchange 2013 사서함 서버 역할은 온-프레미스 조직에서 Exchange Online 조직으로 보내는 보안 메일 메시지를 처리합니다. 또한 일반적인 경우는 아니지만 온-프레미스 받는 사람 사서함도 호스트할 수 있으며, 온-프레미스 클라이언트 액세스 서버를 통해 프록시로 Exchange Online 조직과 통신할 수 있습니다. 기본적으로 보안 하이브리드 메일 전송을 지원하기 위해 사서함 서버 역할에 전용 송신 커넥터가 구성됩니다.
    
    자세한 내용은 [사서함 서버](https://technet.microsoft.com/ko-kr/library/jj150491\(v=exchg.150\))를 참조하십시오.

원하는 하이브리드 배포 구성에 따라 Exchange 2013 서버에 서버 역할 하나 또는 둘 모두를 설치해야 합니다.

  - **단일 Exchange 서버**   온-프레미스 조직에 단일 Exchange 서버를 설치하도록 선택하는 경우 단일 서버에 클라이언트 액세스 서버 및 사서함 서버 역할을 모두 설치해야 합니다.

  - **둘 이상의 Exchange 서버**   온-프레미스 조직에 Exchange 서버를 둘 이상 설치하도록 선택하는 경우에는 온-프레미스 조직의 개별 서버마다 서버 역할을 설치할 수 있습니다. 예를 들어 사서함 및 클라이언트 액세스 역할이 설치되어 있는 Exchange 2013 서버 하나를 설치하고, 클라이언트 액세스 서버 역할만 설치되어 있는 또 다른 Exchange 서버를 설치할 수도 있습니다. 그러나 모범 사례 및 권장되는 서버 구성은 온-프레미스 조직에 배포된 Exchange 2013 서버 *각각*에 클라이언트 액세스 서버 및 사서함 서버 역할을 둘 다 설치하는 것입니다.

[용량 계획에서의 다중 서버 역할 구성 이해](http://go.microsoft.com/fwlink/?linkid=266576)에서 Exchange 용량 계획에 대한 자세한 내용을 참조하십시오.

## 하이브리드 배포에서 Exchange 서버의 기능

Exchange 서버는 하이브리드 배포에서 온-프레미스 조직에 몇 가지 중요한 기능을 제공합니다.

  - **페더레이션**   Exchange 2013 서버를 사용하면 Microsoft Federation Gateway를 통해 온-프레미스 조직용 페더레이션 트러스트를 만들 수 있습니다. Microsoft Federation Gateway는 Microsoft에서 제공하는 무료, 클라우드 기반 서비스로서 온-프레미스 조직과 Office 365 테넌트 조직 사이에서 트러스트 브로커 역할을 합니다. 페더레이션은 온-프레미스 조직과 Exchange Online 조직 간 조직 관계를 만들기 위해 필요합니다.
    
    자세한 내용은 [페더레이션](https://technet.microsoft.com/ko-kr/library/dd335047\(v=exchg.150\))를 참조하십시오.

  - **조직 관계**   클라이언트 액세스 서버 역할이 설치되어 있는 Exchange 2013 서버를 사용하면 온-프레미스 조직과 Exchange Online 조직 간에 조직 관계를 만들 수 있습니다. 약속 있음/없음 일정 정보 공유, 메시지 추적, 온-프레미스 조직과 Exchange Online 조직 간의 사서함 이동 등 하이브리드 배포의 여러 다른 서비스를 사용하려면 조직 관계가 필요합니다.
    
    자세한 내용은 [공유](https://technet.microsoft.com/ko-kr/library/dd638083\(v=exchg.150\))를 참조하십시오.

  - **메시지 전송**   클라이언트 액세스 서버 및 사서함 서버 역할이 설치되어 있는 Exchange 2013 서버는 하이브리드 배포에서 메시지 전송을 담당합니다. 이러한 서버는 송신 및 수신 커넥터를 사용하여, 들어오는 외부 메시지의 연결 끝점 역할을 하면서 아웃바운드 메시지를 인터넷과 Exchange Online 조직으로 배달하는 기능도 제공합니다.
    
    자세한 내용은 [Exchange 2013/Exchange 2007 하이브리드 배포에서의 전송 옵션](transport-options-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md)을 참조하십시오.

  - **메시지 전송 보안**   클라이언트 액세스 서버 및 사서함 서버 역할이 설치되어 있는 Exchange 2013 서버는 Exchange 2013의 도메인 보안 기능을 사용하여 온-프레미스 조직과 Exchange Online 조직 간의 메시지 통신을 보호할 수 있도록 지원합니다. 메시지 통신에 상호 전송 계층 보안 인증 및 암호화를 사용하여 보안을 강화할 수 있습니다.
    
    자세한 내용은 [도메인 보안 이해](http://go.microsoft.com/fwlink/p/?linkid=266581)를 참조하십시오.

  - **Outlook Web App**   클라이언트 액세스 서버 역할이 설치되어 있는 Exchange 2013 서버는 온-프레미스 사서함과 Exchange Online 사서함에 대한 외부 연결용으로 단일 URL 끝점을 구성할 수 있도록 지원합니다. 온-프레미스 사서함의 경우 클라이언트 액세스 서버는 Outlook Web App 요청을 처리하도록 구성됩니다. Exchange Online 조직 사서함의 경우 클라이언트 액세스 서버는 Exchange Online 조직의 Outlook Web App 끝점으로 연결되는 링크를 자동으로 표시하도록 구성됩니다.
    
    자세한 내용은 [Outlook Web App](https://technet.microsoft.com/ko-kr/library/jj657718\(v=exchg.150\))을 참조하십시오.

## Exchange 서버 토폴로지

하이브리드 배포를 지원하기 위해 Exchange 2013 서버를 더 추가하려는 경우 Exchange 서버는 기존 Exchange 2007 조직에 배포되는 다른 Exchange 서버와 유사한 방식으로 배포됩니다. 기존 온-프레미스 Exchange 2007 조직을 하이브리드 배포용으로 구성하는 데는 특수한 Exchange 서버 토폴로지가 필요 없습니다. 그러나 Office 365와의 호환성을 유지하고 완전한 하이브리드 기능을 사용하려면 Exchange 2007 서버에 Exchange 2007 SP3(서비스 팩 3) 업데이트 롤업 10을 설치해야 하며 Exchange 2013 CU1(누적 업데이트 1) 이상도 설치해야 합니다.

다음 표에서는 하이브리드 배포를 구성한 후의 서비스 변경 내용에 대해 간략하게 설명합니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>서비스</th>
<th>하이브리드 배포 전</th>
<th>하이브리드 배포 후</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>메시지 전송(인바운드 및 아웃바운드)</p></td>
<td><p>Exchange 2007 클라이언트 액세스 서버</p></td>
<td><p>Office 365에 포함된 Exchange 2013 클라이언트 액세스 서버 또는 EOP(Exchange Online Protection)</p></td>
<td><p>도메인에 대한 MX(메일 교환기) 레코드는 변경되지 않거나 EOP를 가리키도록 업데이트될 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App 공용 URL</p></td>
<td><p>Exchange 2007 클라이언트 액세스 서버</p></td>
<td><p>Exchange 2013 클라이언트 액세스 서버</p></td>
<td><p>Exchange 2013 클라이언트 액세스 서버는 온-프레미스 사서함에 대한 Outlook Web App 요청을 Exchange 2007 클라이언트 액세스 서버로 프록시합니다. Exchange Online에서 호스트되는 사서함에 대한 Outlook Web App 요청은 Exchange Online Outlook Web App URL 링크와 함께 제공됩니다.</p></td>
</tr>
</tbody>
</table>


## Exchange 서버 소프트웨어

Exchange 2013 CU1 이상을 설치하면 하이브리드 구성 마법사를 통해 하이브리드 배포 기능을 사용하도록 설정할 수 있습니다. Exchange 2013 서버를 추가로 설치할 때는 모든 Exchange 2013 CU1 이상 미디어를 사용할 수 있습니다.

Exchange 2013 최신 버전을 다운로드하는 방법에 대한 자세한 내용은 [Exchange 2013용 업데이트](http://technet.microsoft.com/library/jj907309)를 참조하세요.


> [!IMPORTANT]
> Exchange 2013 또는 2010, Office 365를 사용하여 하이브리드 배포를 구성할 때 하이브리드 서버 라이선스를 획득해야 합니다. 하이브리드 배포를 구성할 때 사용할 Exchange Server 제품 키를 무료로 받으려면 <A href="https://aka.ms/hybridkey">Hybrid Edition 제품 키 도구</A>를 사용하세요.


