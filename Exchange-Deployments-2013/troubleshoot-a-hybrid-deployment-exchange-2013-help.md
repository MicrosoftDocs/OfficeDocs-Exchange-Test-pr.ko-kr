---
title: '하이브리드 배포 문제 해결: Exchange 2013 Help'
TOCTitle: 하이브리드 배포 문제 해결
ms:assetid: bbae72f3-6a1e-4cbf-80da-d8f73d969c6b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ659053(v=EXCHG.150)
ms:contentKeyID: 50484638
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 하이브리드 배포 문제 해결

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-04-29_

하이브리드 구성 마법사를 사용하여 Exchange에서 하이브리드 배포를 구성하면 하이브리드 배포에서 문제가 발생할 가능성이 최소화됩니다. 그러나 하이브리드 구성 마법사의 범위를 벗어나는 몇 가지 일반적인 영역에서 잘못 구성된 경우 하이브리드 배포에서 문제가 발생할 수 있습니다. 이 항목에서는 문제가 발생할 수 있는 다음과 같은 일반적인 영역을 알아보고 문제를 확인하거나 해결하기 위한 기본 단계를 간략하게 설명합니다.

  - 온-프레미스 Exchange 서버

  - 인증서

  - 하이브리드 구성 마법사의 특정 오류


> [!NOTE]
> 이 항목에서 "Exchange 서버"는 다음을 나타냅니다. 
> <UL>
> <LI>
> <P><STRONG>클라이언트 액세스 서버</STRONG> Exchange 2013 및 이전 버전</P>
> <LI>
> <P><STRONG>사서함 서버</STRONG> Exchange 2016 이상 버전</P></LI></UL>



자세한 내용은 [Exchange Server 하이브리드 배포](exchange-server-hybrid-deployments-exchange-2013-help.md)를 참조하세요.

하이브리드 배포와 관련된 추가 관리 작업에 대한 자세한 내용은 [하이브리드 배포 절차](hybrid-deployment-procedures-exchange-2013-help.md) 항목을 참조하세요.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 하이브리드 배포 문제의 유형에 따라 다름

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요.[Exchange 및 셸 인프라 권한](https://technet.microsoft.com/ko-kr/library/dd638114\(v=exchg.150\)) 항목의 "하이브리드 배포" 항목을 참조하십시오.

  - 이 항목의 지침은 하이브리드 구성 마법사를 사용하여 구성된 하이브리드 배포에 적용됩니다. 수동으로 구성된 하이브리드 배포는 지원되지 않습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](https://technet.microsoft.com/ko-kr/library/jj150484\(v=exchg.150\))을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 온-프레미스 Exchange 서버 문제 해결

온-프레미스 Exchange 서버의 구성은 일반적으로 대부분의 문제가 하이브리드 배포에서 발생할 수 있는 영역입니다. 일반적으로 조사해야 하는 영역은 다음과 같습니다.

  - **사용 가능성**   하이브리드 배포에서 기능이 올바르게 작동하려면 온-프레미스 Exchange 서버를 인터넷에 올바르게 게시해야 합니다. 하이브리드 기능이 제대로 작동하려면 인터넷에서 Exchange 서버의 자동 검색 및 EWS(Exchange 웹 서비스) 끝점으로의 인바운드 액세스를 허용하도록 온-프레미스 방화벽 또는 다른 보안 어플라이언스를 구성해야 합니다. 또한 인바운드 SMTP 메일을 허용하도록 Exchange 서버를 구성해야 합니다. Office 365 조직에 포함된 Microsoft EOP(Exchange Online Protection) 서비스에서 온-프레미스 Exchange 서버에 연결할 수 없는 경우에는 Exchange Online 조직에서 온-프레미스 조직으로의 보안 메일 전송이 올바르게 작동하지 않습니다.

  - **인증서**   온-프레미스 조직과 Exchange Online 조직 간의 보안 메일 전송에 사용되는 디지털 인증서는 Exchange Online과 통신할 모든 온-프레미스 인터넷 연결 Exchange 서버에 설치되고, 타사 CA(인증 기관)에서 발급되어야 하며, 만료되지 않아야 하고 IIS 및 SMTP 서비스가 할당되어야 합니다. 이러한 인증서 요구 사항을 충족하지 않으면 Exchange Online 조직에서 온-프레미스 조직으로의 보안 메일 전송이 올바르게 작동하지 않습니다. 인증서 요구 사항에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "인증서 문제 해결"에서 제공됩니다.

## Exchange 서버가 올바르게 구성되어 있는지 확인하는 방법

온-프레미스 Exchange 서버를 성공적으로 게시했는지 확인하려면 Microsoft 원격 연결 분석기를 사용하여 온-프레미스 Exchange 서버에 대한 인바운드 인터넷 연결을 확인합니다. 다음을 수행합니다.

1.  [원격 연결 분석기](https://www.testexchangeconnectivity.com/) 도구로 이동합니다.

2.  이 단계는 EWS 작업이 작동하고 EWS 끝점이 구성되어 있는지 확인하기 위한 일반적인 테스트 단계입니다.
    
    **Microsoft Exchange 웹 서비스 연결 테스트** 섹션에서 **동기화, 알림, 가용성 및 자동 회신(OOF)** 테스트를 실행하여 오류가 없는지 확인합니다. 오류가 발생한 경우 테스트에서 식별한 항목을 수정합니다.

3.  이 단계는 자동 검색 서비스가 작동하고 자동 검색 끝점이 구성되어 있는지 확인하기 위한 일반적인 테스트 단계입니다.
    
    **Microsoft Office Outlook 연결 테스트** 섹션에서 **Outlook 자동 검색**을 실행하여 오류가 없는지 확인합니다. 오류가 발생한 경우 테스트에서 식별한 항목을 수정합니다.

4.  이 단계는 SMTP 연결이 작동하고 Exchange 서버에서 인바운드 인터넷 메일을 받을 수 있는지 확인하기 위한 일반적인 테스트 단계입니다.
    
    **인터넷 전자 메일 테스트** 섹션에서 **인바운드 SMTP 전자 메일** 테스트를 실행하여 오류가 없는지 확인합니다. 오류가 발생한 경우 테스트에서 식별한 항목을 수정합니다.

## 인증서 문제 해결

온-프레미스 Exchange 서버에 설치된 인증서의 구성은 하이브리드 배포에서 발생하는 문제의 원인일 수 있습니다. 대부분의 경우 다음 인증서 관련 문제는 하이브리드 기능에 영향을 줍니다.

  - **인증서 형식**   보안 하이브리드 전송에 사용되고 하이브리드 구성 마법사에서 정의된 디지털 인증서는 타사 CA에서 발급되어야 합니다. 자체 서명된 인증서는 하이브리드 전송 인증에 사용할 수 없습니다. 자체 서명된 인증서를 잘못 선택하거나 할당한 경우 Exchange Online과 온-프레미스 조직 간의 보안 메일 전송이 올바르게 작동하지 않습니다.

  - **할당된 서비스**   하이브리드 전송에 사용되는 디지털 인증서에 IIS(인터넷 정보 서비스) 및 SMTP(Simple Mail Transport Protocol) 서비스를 할당해야 합니다. 이러한 서비스를 할당하지 않으면 Exchange Online과 온-프레미스 조직 간의 보안 메일 전송이 올바르게 작동하지 않습니다.

  - **설치**   온-프레미스 조직과 Exchange Online 조직 간의 보안 메일 전송에 사용되는 디지털 인증서를 모든 온-프레미스 Exchange 서버에 설치해야 합니다. 온-프레미스 Edge 전송 서버와 함께 하이브리드를 배포한 경우 Edge 전송 서버에도 디지털 인증서를 설치해야 합니다. 온-프레미스 서버에 인증서를 설치하지 않으면 Exchange Online과 온-프레미스 조직 간의 보안 메일 전송이 올바르게 작동하지 않습니다.

  - **만료**   온-프레미스 조직과 Exchange Online 조직 간의 보안 메일 전송에 사용되는 디지털 인증서는 만료되어서는 안 됩니다. 인증서가 만료되면 Exchange Online과 온-프레미스 조직 간의 보안 메일 전송이 올바르게 작동하지 않습니다.

## 인증서가 올바르게 구성되어 있는지 확인하는 방법

온-프레미스 Exchange 서버에서 하이브리드 메일 전송용 인증서가 올바르게 구성되었는지 확인하려면 다음을 수행합니다.

1.  온-프레미스 Exchangex 서버에서 Exchange 관리 셸을 엽니다.

2.  Exchange 관리 셸에서 다음 명령을 실행합니다.
    
        Get-ExchangeCertificate| format-list

3.  하이브리드 구성 마법사에서 정의한 보안 메일 전송에 사용할 인증서에 대한 정보를 찾습니다.

4.  다음 매개 변수가 인증서에 할당되어 있는지 확인합니다.
    
      - **IsSelfSigned 매개 변수**   이 매개 변수 값은 *False*여야 합니다.
    
      - **RootCAType 매개 변수**   이 매개 변수 값은 *Third Party*여야 합니다.
    
      - **Services 매개 변수**   이 매개 변수 값은 *IIS, SMTP*여야 합니다.
    
      - **NotAfter 매개 변수**   이 매개 변수 값은 인증서 만료 날짜여야 합니다. 여기에 나열된 날짜는 만료되어서는 안 됩니다.

## 하이브리드 구성 마법사의 특정 오류 문제 해결

하이브리드 구성 마법사를 실행하는 동안 오류가 발생하는 경우 대부분 몇 가지 간단한 검사 또는 작업을 수행하여 문제를 해결할 수 있습니다. 하이브리드 구성 마법사를 실행하는 동안 발생할 수 있는 특정 메시지 또는 문제를 해결하기 위한 다음 제안 사항을 참조하세요.

  - **메시지:“\<서버 이름\> 서버에서 기본 수신 커넥터를 찾을 수 없습니다.”** `(Get-HybridConfiguration).ReceivingTransportServers.` 특성에 나열된 Exchange 서버의 수신 커넥터가 IPv4 및 IPv6 프로토콜 둘 다에 대해 TCP 포트 25를 수신 대기하지 않는 경우 이 메시지가 나타납니다.
    
      -  
        `(Get-HybridConfiguration).ReceivingTransportServers.`를 실행할 때 나열된 Exchange 서버의 수신 커넥터가 올바르게 바인딩되어 있는지 확인하려면 Exchange 관리 셸에서 다음 명령을 실행합니다.
        
            Get-ReceiveConnector -Server <Server Name> | FT Identity, Bindings
        
        Exchange 서버에 대해 나열된 `{[::]:25, 0.0.0.0:25}` 항목을 확인해야 합니다.
        
        이 바인딩이 나열되지 않으면 **Set-ReceiveConnector** cmdlet의 *Bindings* 매개 변수를 사용하여 수신 커넥터에 추가해야 합니다. 자세한 내용은 [Set-ReceiveConnector](https://technet.microsoft.com/ko-kr/library/bb125140\(v=exchg.150\))를 참조하세요.

