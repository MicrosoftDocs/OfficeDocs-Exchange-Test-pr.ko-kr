---
title: 'Exchange 2013 클라이언트 액세스 서버 구성: Exchange 2013 Help'
TOCTitle: Exchange 2013 클라이언트 액세스 서버 구성
ms:assetid: 01432ae4-2a00-44a4-a4dd-4eb8d7e6cfae
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh529912(v=EXCHG.150)
ms:contentKeyID: 50482377
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 클라이언트 액세스 서버 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-07-25_

Exchange 2013 클라이언트 액세스 서버를 설치한 후에는 다양한 구성 작업을 수행할 수 있습니다. Exchange 2013의 클라이언트 액세스 서버는 클라이언트 프로토콜을 처리하지 않지만 가상 디렉터리 설정과 인증서 설정을 포함한 여러 설정을 클라이언트 액세스 서버에 적용해야 합니다.

## 서버 인증서 구성

Exchange 2013에서 인증서 마법사를 사용하여 인증 기관에서 발급한 디지털 인증서를 요청할 수 있습니다. 디지털 인증서를 요청한 후에는 해당 디지털 인증서를 클라이언트 액세스 서버에 설치해야 합니다.

조직의 사서함 서버에는 디지털 인증서를 설치할 필요가 없습니다. 자체 서명된 인증서가 사서함 서버에 기본적으로 설치되어 있으며 이 인증서는 바꿀 필요가 없습니다. 조직의 클라이언트 액세스 서버가 사서함 서버의 자체 서명된 인증서를 암시적으로 신뢰합니다. 자세한 내용은 [Exchange 2013 인증서 관리 UI](exchange-2013-certificate-management-ui-exchange-2013-help.md)를 참조하십시오.

## 가상 디렉터리 구성

가상 디렉터리에서 여러 OAB(오프라인 주소록), Exchange 웹 서비스, Exchange ActiveSync, Outlook Web App 및 Exchange 관리 센터 설정을 구성할 수 있습니다. 가상 디렉터리 관리에 대한 자세한 내용은 [가상 디렉터리 관리](virtual-directory-management-exchange-2013-help.md)를 참조하십시오. 다음 명령을 사용하여 가상 디렉터리를 구성할 수 있습니다.

  - Exchange 2013에서는 관리자가 내부 끝점과 외부 끝점을 모두 구성할 수 있도록 외부에서 Outlook 사용 구성에 대해 두 가지 HTTP 연결 설정 집합을 제공합니다.
    
    연결용 URL 하나를 사용하여 외부에서 Outlook 사용을 구성하려면 Exchange 관리 셸에서 다음 명령을 사용하여 호스트 이름, SSL 필요 여부 및 authpackage를 지정해야 합니다.
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    
    Exchange 관리 셸에서 다음 명령을 사용하여 외부에서 연결 가능한 끝점을 지정할 수도 있습니다.
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -ExternalHostname "externalServer.company.com" -ExternalClientAuthenticationMethod Basic -ExternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    

    > [!TIP]
    > Exchange 2013은 외부에서 Outlook 사용 HTTP 인증을 위한 협상을 지원하지만, 환경의 모든 서버가 Exchange 2013을 실행하는 경우에만 이 협상을 사용해야 합니다.



  - Exchange Activesync를 구성하려면 다음 명령을 실행합니다.
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2013>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl "https://mail.contoso.com/Microsoft-Server-ActiveSync"

  - Exchange 웹 서비스 가상 디렉터리를 구성하려면 다음 명령을 실행합니다.
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalUrl https://mail.contoso.com/EWS/Exchange.asmx

  - 오프라인 주소록을 구성하려면 다음 명령을 실행합니다.
    
        Set-OABVirtualDirectory -Identity "<CAS2013>\OAB (Default Web Site)" -ExternalUrl "https://mail.contoso.com/OAB"

  - 서비스 연결 지점을 구성하려면 다음 명령을 실행합니다.
    
        Set-ClientAccessServer -Identity <CAS2013> -AutoDiscoverServiceInternalURI https://autodiscover.contoso.com/AutoDiscover/AutoDiscover.xml

## Exchange 2007 및 2010 클라이언트 액세스에서 업그레이드

이 섹션의 내용을 참조하여 Exchange 2013 클라이언트 액세스 서버의 프로토콜에 대한 외부 액세스를 구성할 수 있습니다. 위의 가상 디렉터리 구성 섹션에 나와 있는 Exchange 관리 셸 명령과 아래 명령을 모두 실행하십시오.

Exchange 2013에 대해 가상 디렉터리를 구성하려면 다음 명령을 실행해야 합니다.

1.  Outlook Web App용 외부 URL을 구성하려면 Exchange 관리 셸에서 다음 명령을 실행합니다.
    
        Set-OwaVirtualDirectory "<CAS2013>\OWA (Default Web Site)" -ExternalUrl https://mail.contoso.com/OWA
    
    Outlook Web App 가상 디렉터리를 설정한 후 명령 프롬프트에서 다음 명령을 실행합니다.
    
        Net stop IISAdmin /y
    
        Net start W3SVC

2.  외부 EAC 액세스를 구성하려면 Exchange 관리 셸에서 다음 명령을 실행합니다.
    
        Set-EcpVirtualDirectory "<CAS2013>\ECP (Default Web Site)" -ExternalUrl https://mail.contoso.com/ECP -InternalURL https://mail.contoso.com/ECP 

3.  가용성 서비스를 구성하려면 Exchange 관리 셸에서 다음 명령을 실행합니다.
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalURL https://mail.contoso.com/EWS/Exchange.asmx

에 Exchange ActiveSync 또는 Outlook Web App 에 대 한 외부 URL이 올바르게 구성 되었는지 확인 하려면 원격 연결 분석기 Microsoft에서 제공 하는 무료 웹 기반 도구를 사용할 수 있습니다. 원격 연결 분석기 [여기](http://go.microsoft.com/fwlink/?linkid=154308)를 찾을 수 있습니다.

Exchange ActiveSync 또는 Outlook Web App에 대해 인증을 올바르게 구성했는지 확인할 때에도 ExRCA를 사용할 수 있습니다.

Outlook Web App에 대해 직접 파일 액세스를 올바르게 구성했는지 확인하려면 공용 컴퓨터 옵션을 사용하여 사용자로 Outlook Web App에 로그인한 후 전자 메일 메시지에 첨부된 파일에 액세스하고 파일을 저장해 봅니다.

## Exchange 2007 클라이언트 액세스 서버에서 프로토콜 구성

Exchange 2007에 대해 가상 디렉터리를 구성하려면 다음 명령을 실행해야 합니다.

  - Exchange ActiveSync 가상 디렉터리에서 외부 URL을 구성하려면 Exchange 관리 셸에서 다음 명령을 실행합니다.
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2007>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl https://mail.contoso.com/Microsoft-Server-ActiveSync

  - Outlook Web App 가상 디렉터리에서 외부 URL을 구성하려면 Exchange 관리 셸에서 다음 명령을 실행합니다.
    
        Set-OwaVirtualDirectory -Identity "<CAS2007>\owa (Default Web Site)" -ExternalUrl https://legacy.contoso.com/owa

