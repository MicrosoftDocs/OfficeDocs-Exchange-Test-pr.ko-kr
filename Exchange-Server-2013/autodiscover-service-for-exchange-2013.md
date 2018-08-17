---
title: 'Autodiscover 서비스: Exchange 2013 Help'
TOCTitle: Autodiscover 서비스
ms:assetid: b03c0f21-cbc2-4be8-ad03-73a7dac16ffc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124251(v=EXCHG.150)
ms:contentKeyID: 50556060
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autodiscover 서비스

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange 2013용 Exchange 자동 검색 서비스에 대해 알아봅니다. Exchange 자동 검색 서비스란 무엇이며 어떤 방식으로 작동하고 사용할 수 있는 배포 옵션은 무엇인지 알아봅니다.

MicrosoftExchange 2013에는 자동 검색 서비스라는 서비스가 포함되어 있습니다. 이 항목에서는 이 서비스에 대해 간략하게 설명하고, 이 서비스의 작동 방식 및 Outlook 클라이언트 구성 방식과, 메시징 환경에서 자동 검색 서비스를 배포하기 위한 옵션에 대해 설명합니다.

자동 검색 서비스는 다음 작업을 수행합니다.

  - MicrosoftOffice Outlook 2007, Outlook 2010 또는 Outlook 2013을 실행하는 클라이언트뿐만 아니라 지원되는 휴대폰에 대해서도 사용자 프로필 설정을 자동으로 구성합니다. Windows Mobile 6.1 이상 버전을 실행하는 전화가 지원됩니다. 전화가 Windows Mobile 전화가 아닌 경우 휴대폰 설명서에서 지원되는지 여부를 확인합니다.

  - Exchange 메시징 환경에 연결되어 있는 Outlook 2007, Outlook 2010 또는 Outlook 2013 클라이언트가 Exchange 기능에 액세스할 수 있도록 합니다.

  - Outlook 2007, Outlook 2010 또는 Outlook 2013 클라이언트와 지원되는 휴대폰에 프로필 설정을 제공할 때 사용자의 전자 메일 주소와 암호를 사용합니다. Outlook 클라이언트가 도메인에 가입되어 있을 경우 사용자의 도메인 계정이 사용됩니다.

**목차**

자동 검색 서비스 개요

자동 검색 서비스 작동 방식

자동 검색 서비스에 대한 배포 옵션

포리스트 간 이동을 위한 자동 검색 구성

## 자동 검색 서비스 개요

자동 검색 서비스를 사용하면 보다 쉽게 Outlook 2007, Outlook 2010 또는 Outlook 2013과 일부 휴대폰을 보다 쉽게 구성할 수 있습니다. Office Outlook 2007 이전 버전의 Outlook에는 자동 검색 서비스를 사용할 수 없습니다. 이전 버전의 Microsoft Exchange(Exchange 2003 SP2 이전) 및 Outlook(Outlook 2003 이전)에서는 Exchange에 액세스하기 위해 모든 사용자 프로필을 수동으로 구성해야 했습니다. 또한 메시징 환경이 변경되는 경우 이러한 프로필을 관리하려면 추가 작업을 수행해야 했습니다. 그렇지 않으면 Outlook 클라이언트가 제대로 작동하지 않게 됩니다.

Outlook은 자동 검색 서비스를 통해 사용자의 사서함 GUID + @ + 사용자의 기본 SMTP 주소 중 도메인 부분으로 구성된 새 연결 지점을 찾습니다. 자동 검색 서비스는 클라이언트에 다음 정보를 반환합니다.

  - 사용자의 표시 이름

  - 내외부 연결의 연결 설정 구분

  - 사용자 사서함 서버의 위치

  - 약속 있음/없음 정보, 통합 메시징 및 오프라인 주소록 같은 기능을 제어하는 여러 가지 Outlook 기능에 대한 URL입니다.

  - Outlook Anywhere 서버 설정

사용자의 Exchange 정보가 바뀌면 Outlook에서는 자동 검색 서비스를 사용하여 해당 사용자의 프로필을 자동으로 다시 구성합니다. 예를 들어 사용자의 사서함이 이동되거나 클라이언트가 이 사용자의 사서함이나 사용 가능한 Exchange 기능에 연결할 수 없을 경우 Outlook에서는 자동 검색 서비스에 연결해서 해당 사용자의 프로필을 자동으로 업데이트하여 사서함과 Exchange 기능에 연결하는 데 필요한 정보를 포함합니다.

맨 위로 이동

## 자동 검색 서비스 작동 방식

Exchange 2013에 클라이언트 액세스 서버를 설치하면 IIS(인터넷 정보 서비스)의 기본 웹 사이트에 Autodiscover라는 기본 가상 디렉터리가 만들어집니다. 이 가상 디렉터리는 다음과 같은 경우에 Outlook 2007, Outlook 2010 및 Outlook 2013 클라이언트와 지원되는 휴대폰의 자동 검색 서비스 요청을 처리합니다.

  - 사용자 계정이 구성 또는 업데이트되는 경우

  - Outlook 클라이언트가 정기적으로 Exchange 웹 서비스 URL 변경 내용을 확인하는 경우

  - Exchange 메시징 환경에서 기본 네트워크 연결이 변경되는 경우

또한 클라이언트 액세스 서버를 설치한 서버에 SCP(서비스 연결 지점)라는 새 Active Directory 개체가 만들어집니다.

SCP 개체에는 해당 포리스트의 자동 검색 서비스 URL에 대해 신뢰할 수 있는 목록이 포함되어 있습니다. SCP 개체는 **Set-ClientAccessServer** cmdlet을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Set-ClientAccessServer](https://technet.microsoft.com/ko-kr/library/bb125157\(v=exchg.150\))를 참조하십시오.


> [!IMPORTANT]
> <STRONG>Set-ClientAccessServer</STRONG> cmdlet을 실행하기 전에 클라이언트 액세스 서버의 인증된 사용자 계정에 해당 SCP 개체에 대한 읽기 권한이 있는지 확인합니다. 사용자에게 올바른 권한이 없으면 항목을 검색하고 읽을 수 없습니다.



SCP 개체에 대한 자세한 내용은 [서비스 연결 지점을 사용한 게시](https://go.microsoft.com/fwlink/p/?linkid=72744)를 참조하세요.

외부 액세스의 경우나 DNS를 사용하는 경우 클라이언트는 사용자의 전자 메일 주소 중 기본 SMTP 도메인 주소를 사용하여 인터넷에서 자동 검색 서비스를 찾습니다.


> [!NOTE]
> Outlook 클라이언트가 DNS를 사용하여 자동 검색 서비스를 검색할 수 있도록 하려면 DNS에서 호스트 서비스(SRV) 리소스 레코드를 제공해야 합니다. 자세한 내용은 DNS 구성에 대한 Windows 설명서와 <A href="https://go.microsoft.com/fwlink/p/?linkid=85214">백서: Exchange 2007 자동 검색 서비스</A>를 참조하세요.



자동 검색 서비스를 별도의 사이트에 구성했는지 여부에 따라 자동 검색 서비스 URL은 https://\<*smtp-address-domain*\>/autodiscover/autodiscover.xml 또는 https://autodiscover.\<*smtp-address-domain*\>/autodiscover/autodiscover.xml일 수 있습니다. 여기서 ://\<*smtp-address-domain*\>은 기본 SMTP 도메인 주소입니다. 예를 들어 사용자의 전자 메일 주소가 tony@contoso.com인 경우 기본 SMTP 도메인 주소는 contoso.com입니다. 클라이언트는 Active Directory에 연결할 때 설치 중 만들어진 SCP 개체를 찾습니다. 클라이언트 액세스 서버가 여러 대 있는 배포에서는 클라이언트 액세스 서버마다 Autodiscover SCP 개체가 하나씩 만들어집니다. 이러한 SCP 개체에는 https://CAS01/autodiscover/autodiscover.xml 형식으로 된 클라이언트 액세스 서버의 FQDN(정규화된 도메인 이름)을 포함하는 *ServiceBindingInfo* 특성이 포함되어 있습니다. 여기서 CAS01은 클라이언트 액세스 서버의 FQDN입니다. Outlook 2007, Outlook 2010 또는 Outlook 2013 클라이언트는 사용자 자격 증명을 사용하여 Active Directory에 인증한 후 자동 검색 SCP 개체를 검색합니다. 클라이언트는 자동 검색 서비스 인스턴스를 얻고 열거한 후에는 열거한 목록의 첫째 클라이언트 액세스 서버에 연결해서 사용자의 사서함과 사용 가능한 Exchange 기능에 연결하는 데 필요한 프로필 정보(XML 데이터 형식으로 되어 있음)를 얻습니다.

맨 위로 이동

## 자동 검색 서비스에 대한 배포 옵션

Outlook 2007, Outlook 2010 및 Outlook 2013 클라이언트가 오프라인 주소록, 가용성 서비스 및 UM(통합 메시징) 같은 Exchange 기능에 자동으로 연결되도록 하려면 자동 검색 서비스를 올바르게 배포 및 구성해야 합니다. 자동 검색 서비스 배포는 Outlook 2007, Outlook 2010 또는 Outlook 2013 클라이언트에서 가용성 서비스 같은 Exchange 서비스에 액세스할 수 있도록 하는 데 필요한 한 단계일 뿐입니다.

## 포리스트 간 이동을 위한 자동 검색 구성

자동 검색 서비스는 한 Outlook 포리스트에서 다른 포리스트로 이동된 사서함에 대한 Exchange 클라이언트를 연결하기 위해 사용자 프로필 정보를 제공할 수 있습니다. 이를 위해서는 **New-MailUser** cmdlet을 사용하여 사용자 사서함이 있는 원래 포리스트와 대상 포리스트 모두에 메일 사용 가능 사용자를 구성해야 합니다. 원본 포리스트의 경우 cmdlet에서 *ExternalEmailAddress* 매개 변수를 사용하여 대상 포리스트의 사서함에 대한 새 전자 메일 주소를 지정합니다. 자세한 내용은 [New-MailUser](https://technet.microsoft.com/ko-kr/library/aa996335\(v=exchg.150\)) 항목을 참조하십시오.

메일 사용 가능 사용자를 구성할 경우 원래 포리스트의 자동 검색 서비스는 인증하는 사용자를 대상 포리스트의 새 전자 메일 주소로 리디렉션합니다. 그런 다음 연결하는 Outlook 클라이언트는 사서함이 제거된 대상 포리스트의 클라이언트 액세스 서버로 리디렉션됩니다.

맨 위로 이동

