---
title: 'Exchange 2007 UM을 Exchange 2013 UM으로 업그레이드: Exchange 2013 Help'
TOCTitle: Exchange 2007 UM을 Exchange 2013 UM으로 업그레이드
ms:assetid: 642c922d-7e85-40f0-bb9b-0f20da692be3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn169227(v=EXCHG.150)
ms:contentKeyID: 54651817
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2007 UM을 Exchange 2013 UM으로 업그레이드

 

_<strong>적용 대상:</strong> Exchange Server 2013, Exchange Server 2016_

_<strong>마지막으로 수정된 항목:</strong> 2016-12-09_

UM(통합 메시징)을 사용하는 Microsoft Exchange 2007 조직이 Exchange 2013 통합 메시징을 사용하도록 업그레이드할 때는 몇 가지 필수 단계를 수행해야 합니다. 기타 단계는 Exchange 2007 UM 배포의 일부분으로 이미 완료되었습니다. Exchange 2007에서 통합 메시징을 지원하도록 만들고 구성한 UM 구성 요소 및 전화 통신 환경에 따라 VoIP(Voice over IP) 게이트웨이, IP PBX(Private Branch Exchange) 또는 일반/SIP 사용 가능 PBX를 비롯한 추가 전화 통신 장비를 배포한 다음 Exchange 2013 UM에 필요한 추가 UM 구성 요소를 만들고 구성해야 할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 45~90분

  - Exchange 2007 및 Exchange 2013 조직에서 모든 필요한 구성 요소를 만들고 구성하기 위한 적절한 권한이 있는지 확인합니다.

  - VoIP 게이트웨이 및 PBX, IP PBX 또는 SIP(Session Initiation Protocol) 사용 가능 PBX를 비롯한 전화 통신 구성 요소를 배포했으며 올바르게 구성했는지 확인합니다.

  - Microsoft Exchange UM(통합 메시징) 통화 라우터 서비스를 실행 중인 클라이언트 액세스 서버와 Microsoft Exchange UM(통합 메시징) 서비스를 실행 중인 사서함 서버를 올바르게 설치 및 구성했는지 확인합니다. UM 서비스에 대한 자세한 내용은 [UM 서비스](um-services-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 어떻게 해야 합니까?

## 1단계: 필요한 UM 언어 팩 다운로드 및 설치

UM 언어 팩을 사용하면 발신자와 Outlook Voice Access 사용자가 여러 언어로 음성 메일 시스템과 상호 작용할 수 있습니다. Exchange 2013 사서함 서버에 추가 언어를 설치한 후에는 발신자와 Outlook Voice Access 사용자가 해당 언어로 전자 메일 메시지를 듣고 음성 메일 시스템과 상호 작용할 수 있습니다. 그러나 모든 수신 전화에 대해 해당 언어를 사용할 수 있도록 하려면 모든 Exchange 2013 사서함 서버에 필요한 UM 언어 팩을 설치해야 합니다. 모든 Exchange 2013 사서함 서버가 통합 메시징의 수신 전화에 응답할 수 있기 때문입니다.

기본적으로 Exchange 2013 사서함 서버를 설치하면 미국 영어(en-US) 언어 팩이 설치됩니다. 다른 UM 언어 팩을 설치하지 않을 경우 다이얼 플랜에 이 언어 옵션만 사용할 수 있습니다. 미국 영어는 컴퓨터에서 사서함 서버를 제거하지 않는 한 제거할 수 없습니다. Exchange 2013 사서함 서버에 UM 언어 팩을 설치하고 나면 다이얼 플랜에 대한 기본 언어를 구성할 때 해당 언어 팩에 연결된 언어가 사용 가능한 옵션으로 나열됩니다. 기본적으로 UM 자동 전화 교환은 만들 때 UM 다이얼 플랜에 연결되므로 연결된 UM 다이얼 플랜의 기본 언어 설정을 사용합니다. 그러나 UM 자동 전화 교환을 만든 후에 이 설정을 변경할 수 있습니다.


> [!NOTE]
> 미국 영어만 다이얼 플랜에 제공하려는 경우 이 단계를 건너뛰고 2단계로 이동할 수 있습니다.



Setup.exe 명령을 사용 하 여 또는 [Exchange Server 2013 UM 언어팩](https://go.microsoft.com/fwlink/p/?linkid=266542)에서 UM 언어팩을 다운로드 한 후 *\<UMLanguagePack\>*.exe 설치 프로그램을 실행 하 여 UM 언어팩을 추가할 수 있습니다. 자세한 내용은 [UM 언어 팩 설치](install-a-um-language-pack-exchange-2013-help.md)을 참조 하십시오.

이 예에서는 setup.exe를 사용하여 일본어(ja-JP) UM 언어 팩을 설치합니다.

```powershell
setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms
```

## 2단계: Exchange 2013 시스템 사서함으로 Exchange 2007 사용자 지정 인사말, 알림, 메뉴, 음성 안내 이동

사용자 지정 인사말, 알림, 메뉴 및 음성 안내는 통합 메시징 다이얼 플랜 및 자동 전화 교환에서 사용됩니다. Exchange 2007 또는 Exchange 2013을 설치하면 시스템 사서함 {e0dc1c29-89c3-4034-b678-e6c29d823ed9}가 만들어지고 메시지 승인 및 여러 사서함 검색과 같은 기능을 지원하는 데 사용됩니다. 이 시스템 사서함은 다이얼 플랜 및 자동 전화 교환 사용자 지정 인사말, 알림, 메뉴 및 음성 안내를 저장하는 데에도 사용됩니다. 시스템 사서함이 없는 경우 <strong>Setup /PrepareAD</strong> 명령을 사용하여 시스템 사서함을 만들 수 있습니다.

시스템 사서함은 기본적으로 EAC(Exchange 관리 센터)에서 표시되지 않습니다. 다음 중 하나를 실행하여 시스템 사서함 목록을 확인할 수 있습니다.

이 명령은 모든 시스템 사서함 목록을 반환합니다.

```powershell
Get-Mailbox -Arbitration
```

이 명령은 시스템 사서함 및 시스템 사서함의 개별 속성이나 설정 목록을 반환합니다.

```powershell
Get-Mailbox -Arbitration |fl
```

Exchange 2007의 사용자 지정 인사말, 알림, 메뉴 및 음성 안내를 Exchange 2013으로 가지고 오는 경우 MigrateUMCustomPrompts.ps1 스크립트를 사용해야 합니다. EAC를 사용하여 사용자 지정 인사말, 알림, 메뉴 및 음성 안내를 가져올 수는 없습니다. MigrateUMCustomPrompts.ps1 스크립트는 모든 Exchange Server 2007 UM 사용자 지정 인사말, 알림, 메뉴 및 음성 안내의 복사본을 Exchange 2013 UM으로 마이그레이션합니다. 기본적으로 MigrateUMCustomPrompts.ps1 스크립트는 Exchange 2013 사서함 서버의 *\<Program Files\>*\\Microsoft\\Exchange Server\\V15\\Scripts 폴더에 있으며, Exchange 2013 사서함 서버에서 실행되어야 합니다. 스크립트를 실행하려면

1.  <strong>시작</strong> \> <strong>모든 프로그램</strong> \> <strong>Microsoft Exchange Server 2013</strong> \> <strong>Exchange 관리 셸</strong>을 클릭합니다.

2.  Exchange 관리 셸 프롬프트에 스크립트 경로를 입력합니다. 예를 들어, <strong>cd "D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"</strong>를 입력하고 Enter 키를 누릅니다.

3.  셸 프롬프트에 <strong>".\\MigrateUMCustomPrompts"</strong>를 입력한 다음 Enter 키를 누릅니다.


> [!NOTE]
> <STRONG>Import-UMPrompt</STRONG> cmdlet을 사용하여 사용자 지정 음성 안내를 개별적으로 가져올 수도 있습니다. 사용지 지정 음성 안내를 Exchange 2013 UM으로 복사할 때 Exchange 2007 UM <STRONG>Copy-UMCustomPrompt</STRONG> cmdlet은 사용할 수 없습니다.



Exchange 2013 서버에서 MigrateUMCustomPrompts.ps1 스크립트를 실행하면 스크립트에서 Active Directory의 자동 전화 교환이나 다이얼 플랜에 대해 GUID나 개체 식별자를 조회하고 이를 쿼리하여 사용자 지정 인사말, 알림, 메뉴 또는 음성 안내가 있는지 여부를 확인합니다. 사용자 지정 인사말, 알림, 메뉴 및 음성 안내가 있으면 이를 {e0dc1c29-89c3-4034-b678-e6c29d823ed9}라는 시스템 사서함으로 가져옵니다.

이 시스템 사서함을 사용하여 데이터베이스의 다른 사서함과 함께 사용자 지정 인사말, 알림, 메뉴 및 음성 안내를 백업하고 복원할 수 있습니다. 이렇게 하면 필요한 리소스의 양을 줄일 수 있습니다. 사용자 지정 인사말, 알림, 메뉴 및 음성 안내를 시스템 사서함에 저장하면 과거에 발생 가능했던 불일치 현상이 없어집니다. 사서함 이동에 대한 자세한 내용은 [Exchange 2013 사서함 이동](mailbox-moves-in-exchange-2013-exchange-2013-help.md)을 참조하십시오.

## 3단계: 인증서 내보내기 및 가져오기

Exchange 2007 조직에서 SIP 보안 또는 보안 다이얼 플랜을 사용하는 경우 사용된 인증서를 내보내 Exchange 2013 클라이언트 액세스 서버 및 사서함 서버로 가져와야 합니다. 상호 TLS(전송 계층 보안)를 사용하여 Exchange 2013 서버와 VoIP 게이트웨이, IP PBX 및 SIP 사용 가능 PBX 간에 전송되는 데이터를 암호화합니다. 인증서는 정보를 디지털 방식으로 암호화하고 서명하는 데 사용되는 전자 키(공개 및 개인) 쌍에 인증서 소유자의 ID를 바인딩합니다. UM 및 UM 통화 라우터 서비스에는 다음 인증서 중 하나를 사용할 수 있습니다.

  - 자체 서명된(Exchange) 인증서

  - 내부 PKI(공개 키 인프라) 인증서

  - 타사 상업용 인증서

기본적으로 Exchange 2013을 설치하면 자체 서명된 인증서 두 개, 즉, <strong>Microsoft Exchange Server 인증 인증서</strong> 및 <strong>Microsoft Exchange</strong>가 만들어집니다. <strong>Microsoft Exchange</strong> 자체 서명된 인증서를 UM에서 사용하여 데이터를 암호화할 수는 있지만, 이렇게 하려면 인증서를 UM 서비스 및 UM 통화 라우터 서비스에 할당해야 합니다. 이 자체 서명된 인증서를 복사한 다음 VoIP 게이트웨이, IP PBX 및 SIP 사용 가능 PBX로 가져올 수 있습니다. 그러나 UM을 Microsoft Lync Server와 통합할 때는 이 인증서를 사용할 수 없습니다.

UM에서 Exchange 2013 서버와 VoIP 게이트웨이, IP PBX 및 SIP 사용 가능 PBX 간에 전송되는 데이터를 암호화할 수 있도록 설정하려면 다음을 수행해야 합니다.

  - 기존 자체 서명된 UM 인증서를 사용하여 새 자체 서명된 Exchange 인증서를 만들거나, 내부 인증 기관에 PKI 인증서에 대한 인증서 요청을 제출하거나, Exchange 2013 사서함 서버 및 클라이언트 액세스 서버와 VoIP 게이트웨이, IP PBX 및 SIP 사용 가능 PBX 간에 상호 TLS용으로 사용할 수 있는 타사 상업용 인증서를 구입합니다.
    
    다음과 같이 EAC를 사용하여 Exchange 자체 서명된 인증서를 만듭니다.
    
    1.  EAC에서 <strong>서버</strong> \> <strong>인증서</strong>로 이동한 후 <strong>추가</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.
    
    2.  <strong>새 Exchange 인증서</strong> 페이지에서 <strong>자체 서명된 인증서 만들기</strong>를 선택한 후 <strong>다음</strong>을 선택합니다.
    
    3.  인증서의 이름을 입력하고 <strong>다음</strong>을 선택합니다.
    
    4.  <strong>추가</strong> ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 이 인증서를 적용할 Exchange 서버를 선택한 후 <strong>다음</strong>을 선택합니다.
    
    5.  인증서에 포함할 도메인을 지정하고 <strong>다음</strong>을 선택합니다. 서비스에 대해 도메인을 추가하려면 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.
    
    6.  포함한 도메인이 올바른지 확인한 후 <strong>마침</strong>을 선택합니다.
    

    > [!IMPORTANT]
    > EAC를 사용하여 인증서를 만들 때는 인증서에 대해 서비스를 사용하도록 설정하라는 메시지가 표시되지 않습니다. 인증서를 만든 후에 EAC를 통해 서비스를 사용하도록 설정할 수 있습니다. 서비스에서 인증서를 사용하도록 설정하는 방법에 대한 자세한 내용은 <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">UM 및 UM 통화 라우터 서비스에 인증서 할당</A>을 참조하십시오.

    
    셸에서 다음 명령을 실행하여 Exchange 자체 서명된 인증서를 만듭니다.
    
    ```powershell
    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
    ```

    > [!TIP]
    > <EM>Services</EM> 매개 변수를 통해 사용하도록 설정할 서비스를 지정하는 경우에는 만든 인증서에 대해 서비스를 사용하도록 설정하라는 메시지가 표시됩니다. 이 예에서는 통합 메시징 및 통합 메시징 통화 라우터 서비스에서 인증서를 사용하도록 설정하라는 메시지가 표시됩니다. 서비스에서 인증서를 사용하도록 설정하는 방법에 대한 자세한 내용은 <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">UM 및 UM 통화 라우터 서비스에 인증서 할당</A>을 참조하십시오.



  - 조직의 모든 Exchange 2013 클라이언트 액세스 서버 및 사서함 서버에서 사용할 인증서를 가져옵니다. Exchange 2013 자체 서명된 인증서를 사용하는 경우에는 해당 인증서를 복사한 다음 VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX로 가져와야 합니다. Exchange 2007의 자체 서명된 인증서를 사용하는 경우에는 SAN(주체 대체 이름)에 모든 Exchange 2013 서버의 컴퓨터 이름이 포함되어야 합니다. 조직에 Exchange 2007 통합 메시징 서버가 있으면 Exchange 2013 자체 서명된 인증서를 사용할 수 있지만, 이 경우 Exchange 2007 UM 서버의 컴퓨터 이름을 Exchange 2013 인증서의 SAN에 추가해야 합니다.

  - 조직의 클라이언트 액세스 서버와 사서함 서버의 UM 서비스 및 UM 통화 라우터 서비스에 사용할 인증서를 할당하거나 사용하도록 설정합니다.
    
    다음과 같이 EAC를 사용하여 모든 Exchange 2013 서버의 UM 서비스 및 UM 통화 라우터 서비스에서 Exchange 자체 서명된 인증서를 사용하도록 설정합니다.
    
    1.  EAC에서 <strong>서버</strong> \> <strong>인증서</strong>로 이동하여 서비스에서 사용하도록 설정할 인증서를 선택하고 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.
    
    2.  <strong>절차</strong> 페이지에서 <strong>서비스</strong>, <strong>통합 메시징</strong>, <strong>통합 메시징 통화 라우터</strong>를 차례로 선택합니다.
    
    셸에서 다음 명령을 실행하여 Exchange 자체 서명된 인증서를 사용하도록 설정합니다.
    
    ```powershell
    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'
    ```

  - 신규 또는 기존 UM 다이얼 플랜을 SIP 보안 또는 보안으로 구성합니다.

  - 조직의 클라이언트 액세스 서버 및 사서함 서버에서 UM 시작 모드를 TLS 또는 이중으로 구성합니다.

  - FQDN(정규화된 도메인 이름)을 사용하여 신규 또는 기존 UM IP 게이트웨이를 만들고 구성합니다.

  - TLS 포트 5061을 사용하도록 UM IP 게이트웨이의 수신 대기 포트를 구성합니다.

  - 모든 Exchange 2013 클라이언트 액세스 서버에서 UM 통화 라우터 서비스를 다시 시작하고 모든 Exchange 2013 사서함 서버에 대해 UM 서비스를 다시 시작합니다. UM 서비스에 대한 자세한 내용은 [UM 서비스](um-services-exchange-2013-help.md)를 참조하십시오.

## 4단계: 모든 Exchange 2013 클라이언트 액세스 서버에서 UM 시작 모드 구성

SIP 보안 또는 보안 다이얼 플랜을 사용하는 경우 Exchange 2013 클라이언트 액세스 서버에서 UM 시작 모드를 구성해야 합니다. EAC 또는 셸을 사용하여 Exchange 2013 클라이언트 액세스 서버에서 UM 통화 라우터 서비스에 대해 UM 시작 모드를 지정할 수 있습니다. 기본적으로 Exchange 2013 클라이언트 액세스 서버는 TCP 모드로 시작되지만 TLS(전송 계층 보안)를 사용하여 VoIP(Voice over IP) 트래픽을 암호화하는 경우에는 TLS 또는 이중 모드를 사용하도록 Exchange 2013 클라이언트 액세스 서버를 구성해야 합니다. 이중 모드를 UM 시작 모드로 사용하도록 모든 Exchange 2013 클라이언트 액세스 서버를 구성하는 것이 좋습니다. 모든 Exchange 2013 클라이언트 액세스 서버가 모든 UM 다이얼 플랜의 수신 전화에 응답할 수 있으며 이러한 다이얼 플랜의 보안 설정이 서로 다를 수 있기 때문입니다. UM 시작 모드를 변경하는 경우에는 UM 통화 라우터 서비스를 다시 시작해야 변경 내용이 적용됩니다. UM 서비스에 대한 자세한 내용은 [UM 서비스](um-services-exchange-2013-help.md)를 참조하십시오.

다음과 같이 EAC를 사용하여 Exchange 2013 클라이언트 액세스 서버에서 UM 시작 모드를 구성합니다.

1.  EAC에서 <strong>서버</strong> \> <strong>서버</strong>로 이동합니다.

2.  목록 보기에서 수정하려는 Exchange 서버를 선택하고 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  <strong>Exchange Server</strong> 페이지에서 <strong>통합 메시징</strong>을 클릭합니다.

4.  <strong>UM 통화 라우터 설정</strong> \> <strong>UM 시작 모드</strong>의 드롭다운 목록에서 다음 중 하나를 선택합니다.
    
      - <strong>TCP</strong>   mTLS를 사용하지 않으며 비보안 다이얼 플랜만 사용할 경우 이 옵션을 사용합니다.
    
      - <strong>TLS</strong>   mTLS를 사용하며 SIP 보안 또는 보안 다이얼 플랜만 사용할 경우 이 옵션을 사용합니다.
    
      - <strong>이중</strong>   mTLS를 사용하며 비보안, SIP 보안 또는 보안 다이얼 플랜을 사용할 경우 이 옵션을 사용합니다.

5.  UM 시작 모드를 선택한 후 <strong>저장</strong>을 클릭합니다.

셸에서 다음 명령을 실행하여 Exchange 2013 클라이언트 액세스 서버에서 UM 시작 모드를 구성합니다.

```powershell
Set-UMCallRouterSettings -Server MyUMCallRouter.northwindtraders.com -UMStartupMode Dual
```

## 5단계: 모든 Exchange 2013 사서함 서버에서 UM 시작 모드 구성

SIP 보안 또는 보안 다이얼 플랜을 사용하는 경우 Exchange 2013 사서함 서버에서 UM 시작 모드를 구성해야 합니다. EAC 또는 셸을 사용하여 Exchange 2013 사서함 서버에서 UM 서비스에 대해 UM 시작 모드를 지정할 수 있습니다. 기본적으로 Exchange 2013 사서함 서버는 TCP 모드로 시작되지만 TLS(전송 계층 보안)를 사용하여 VoIP(Voice over IP) 트래픽을 암호화하는 경우 TLS 또는 이중 모드를 사용하도록 Exchange 2013 사서함 서버를 구성해야 합니다. 이중 모드를 UM 시작 모드로 사용하도록 모든 Exchange 2013 사서함 서버를 구성하는 것이 좋습니다. 모든 Exchange 2013 사서함 서버가 모든 UM 다이얼 플랜의 수신 전화에 응답할 수 있으며 이러한 다이얼 플랜의 보안 설정이 서로 다를 수 있기 때문입니다. UM 시작 모드를 변경하는 경우에는 UM 서비스를 다시 시작해야 변경 내용이 적용됩니다. UM 서비스에 대한 자세한 내용은 [UM 서비스](um-services-exchange-2013-help.md)를 참조하십시오.

다음과 같이 EAC를 사용하여 Exchange 2013 사서함 서버에서 UM 시작 모드를 구성합니다.

1.  EAC에서 <strong>서버</strong> \> <strong>서버</strong>로 이동합니다.

2.  목록 보기에서 수정하려는 Exchange 서버를 선택하고 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  <strong>Exchange Server</strong> 페이지에서 <strong>통합 메시징</strong>을 클릭합니다.

4.  <strong>UM 서비스 설정</strong> \> <strong>UM 시작 모드</strong>의 드롭다운 목록에서 다음 중 하나를 선택합니다.
    
      - <strong>TCP</strong>   mTLS를 사용하지 않으며 비보안 다이얼 플랜만 사용할 경우 이 옵션을 사용합니다.
    
      - <strong>TLS</strong>   mTLS를 사용하며 SIP 보안 또는 보안 다이얼 플랜만 사용할 경우 이 옵션을 사용합니다.
    
      - <strong>이중</strong>   mTLS를 사용하며 비보안, SIP 보안 또는 보안 다이얼 플랜을 사용할 경우 이 옵션을 사용합니다.

5.  UM 시작 모드를 선택한 후 <strong>저장</strong>을 클릭합니다.

셸에서 다음 명령을 실행하여 Exchange 2013 사서함 서버에서 UM 시작 모드를 구성합니다.

   ```powershell
    Set-UMService -Identity MyUMServer -ExternalHostFqdn host.external.contoso.com -IPAddressFamily Any -UMStartupMode Dual
   ``` 

## 6단계: UM 다이얼 플랜 만들기 또는 기존 UM 다이얼 플랜 구성

기존 Exchange 2007 배포에 따라 새 UM 다이얼 플랜을 만들거나 기존 다이얼 플랜을 구성해야 할 수 있습니다. UM 다이얼 플랜은 공통 사용자 내선 번호를 공유하는 기존 또는 SIP 사용 가능 PBX(Private Branch eXchange), IP PBX 또는 SIP 사용 가능 PBX의 집합을 나타냅니다. 한 다이얼 플랜 내의 일반 또는 SIP 사용 가능 PBX나 IP PBX에서 호스트되는 모든 사용자의 내선 번호 자릿수는 동일합니다. 사용자는 내선 번호에 특별한 번호를 추가하거나 전체 전화 번호를 입력하지 않고도 서로의 내선 번호로 전화를 걸 수 있습니다.

UM 다이얼 플랜은 통합 메시징에서 사용자의 내선 번호를 고유하게 보장하는 데 사용됩니다. 일부 전화 통신 네트워크에서는 IP PBX, 기존 PBX 또는 SIP 사용 가능 PBX가 여러 대 있습니다. 이러한 전화 통신 네트워크에서는 동일한 전화 내선 번호를 갖는 두 명의 사용자가 존재할 수 있습니다. UM 다이얼 플랜은 이러한 경우의 문제를 해결해 줍니다. 두 명의 사용자를 두 UM 다이얼 플랜에 따로 추가하면 내선 번호가 고유하게 지정됩니다. 자세한 내용은 [UM 다이얼 플랜](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-dial-plans)을 참조하십시오.

필요한 경우 EAC를 사용하여 UM 다이얼 플랜을 만들 수 있습니다.

1.  EAC에서 <strong>통합 메시징</strong> \> <strong>UM 다이얼 플랜</strong>으로 이동한 다음 <strong>새로 만들기</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  <strong>새 UM 다이얼 플랜</strong> 페이지에서 다음 상자에 해당 정보를 입력합니다.
    
      - <strong>이름</strong>   다이얼 플랜의 이름을 입력합니다. UM 다이얼 플랜 이름은 필수이며 고유해야 합니다. 하지만 입력한 이름은 EAC와 셸에 표시되는 용도로만 사용됩니다. UM 다이얼 플랜 이름의 최대 길이는 64자이며 공백을 포함할 수 있습니다. 그러나 다음 문자는 사용할 수 없습니다. " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        다이얼 플랜의 이름 상자에는 64자까지 입력할 수 있지만 다이얼 플랜 이름은 49자보다 길 수 없습니다. 49자보다 많은 문자를 포함하는 다이얼 플랜 이름을 만들려고 하면 오류 메시지가 나타납니다. 메시지에는 UM 다이얼 플랜 이름이 너무 길어 UM 사서함 정책을 생성할 수 없다는 내용이 표시됩니다. 이 문제는 다이얼 플랜을 만들 때 이름이 *\<DialPlanName\>*<strong>기본 정책</strong>인 기본 UM 사서함 정책도 만들어지기 때문에 발생합니다. 기본 정책의 15자가 다이얼 플랜 이름에 추가되면 총 문자 수가 제한을 초과합니다. UM 다이얼 플랜과 UM 사서함 정책에 대한 *name* 매개 변수는 모두 64자일 수 있습니다. 하지만 다이얼 플랜의 이름이 49자보다 길면 기본 UM 사서함 정책의 이름이 64자보다 길어지므로 시스템에서 허용되지 않습니다.
    
      - <strong>내선 번호 길이(자릿수)</strong>   다이얼 플랜에서 내선 번호의 자릿수를 입력합니다. 내선 번호 자릿수는 PBX에 만들어진 전화 통신 다이얼 플랜을 기반으로 합니다. 예를 들어 전화 통신 다이얼 플랜과 연결된 사용자가 4자리 내선 번호를 돌려 동일한 전화 통신 다이얼 플랜의 다른 사용자에게 전화하는 경우 내선 번호 자릿수로 4를 선택합니다.
        
        이 항목은 필수 입력란이며 값의 범위는 1~20입니다. 일반적인 내선 번호 길이는 3~7자리입니다. 기존 전화 통신 환경에 내선 번호가 포함되어 있으면, 해당 내선 번호의 자릿수와 일치하는 자릿수를 지정해야 합니다.
        
        내선 번호 다이얼 플랜을 만들 때 사용자가 내선 번호 다이얼 플랜에 연결된 경우의 사용자 내선 번호를 입력해야 합니다. 내선 번호는 UM 사용 가능 사용자가 SIP URI 또는 E.164 다이얼 플랜에 연결된 경우 SIP(Session Initiation Protocol) 다이얼 플랜 또는 E.164 다이얼 플랜에도 필요합니다. 이 내선 번호는 Outlook Voice Access 사용자가 Exchange 사서함에 액세스할 때 사용됩니다.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_URI 형식)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_VoIP 보안)
    
      - <strong>국가/지역 코드</strong>   이 상자에 발신 전화에 사용될 국가/지역 번호를 입력합니다. 이 번호는 거는 전화 번호 앞에 자동으로 붙습니다. 이 상자에는 1~4자리 숫자를 입력할 수 있습니다. 예를 들어 미국 국가/지역 번호는 1이고, 영국 국가/지역 번호는 44입니다.

3.  <strong>저장</strong>을 클릭합니다.

필요한 경우 셸에서 다음 명령을 실행하여 UM 다이얼 플랜을 만들 수 있습니다.

```powershell
New-UMDialplan -Name MyUMDialPlan -URIType E164 -NumberOfDigitsInExtension 5 -VoIPSecurity Secured
```

필요한 경우 EAC를 사용하여 기존 UM 다이얼 플랜을 구성할 수 있습니다.

1.  EAC에서 <strong>통합 메시징</strong> \> <strong>UM 다이얼 플랜</strong>으로 이동합니다.

2.  목록 보기에서 보거나 수정하려는 UM 다이얼 플랜을 선택하고 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  <strong>UM 다이얼 플랜</strong> 페이지에서 <strong>구성</strong>을 클릭합니다. 구성 옵션을 사용하여 특정 다이얼 플랜 설정을 보고, 기능을 사용하거나 사용하지 않도록 설정합니다.

필요한 경우 셸에서 다음 명령을 실행하여 기존 UM 다이얼 플랜을 구성할 수 있습니다.

```powershell
Set-UMDialplan -Identity MyDialPlan -AccessTelephoneNumbers 4255551234 -AudioCodec Wma -CallAnsweringRulesEnabled $false -OutsideLineAccessCode 9 -VoIPSecurity SIPSecured
```

Exchange 2007 통합 메시징을 배포할 때는 UM이 수신 전화 응답하도록 하기 위해 통합 메시징 서버를 UM 다이얼 플랜에 추가해야 했습니다. 이제 이 작업은 필요하지 않습니다. Exchange 2013에서는 클라이언트 액세스 서버 및 사서함 서버를 내선 번호 또는 E.164 다이얼 플랜에 연결할 수 없는 대신 SIP URI 다이얼 플랜에 연결해야 합니다. 클라이언트 액세스 서버 및 사서함 서버는 모든 유형의 다이얼 플랜에 대한 모든 수신 전화에 응답합니다.

## 7단계: UM IP 게이트웨이 만들기 또는 기존 UM IP 게이트웨이 구성

기존 Exchange 2007 배포에 따라 새 UM IP 게이트웨이를 만들거나 기존 UM IP 게이트웨이를 구성해야 할 수 있습니다. SIP 보안 또는 보안 다이얼 플랜을 사용하는 경우 FQDN을 사용해 UM IP 게이트웨이를 만든 다음 셸을 사용해 포트 5061에서 수신 대기하도록 게이트웨이를 구성해야 합니다. 기존 UM IP 게이트웨이의 경우 FQDN을 사용하여 구성되었으며 포트 5061에서 수신 대기하는지 확인합니다. UM IP 게이트웨이가 FQDN을 사용하지 않는 경우 EAC 또는 셸을 사용하여 주소를 변경합니다. UM IP 게이트웨이가 포트 5061을 사용하지 않으면 셸을 사용하여 포트를 변경합니다. <strong>Get-UMIPGateway</strong> cmdlet을 사용하여 UM IP 게이트웨이의 설정을 확인할 수 있습니다.

UM IP 게이트웨이는 실제 VoIP(Voice over IP) 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX를 나타냅니다. 음성 사서함 사용자가 수신 전화에 응답하고 발신 전화를 보내는 데 VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX를 사용하려면 디렉터리 서비스에서 UM IP 게이트웨이를 만들어야 합니다.

UM IP 게이트웨이와 UM 헌트 그룹의 조합으로 VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX와 UM 다이얼 플랜 간의 연결이 설정됩니다. 여러 UM 헌트 그룹을 만들면 단일 UM IP 게이트웨이를 여러 UM 다이얼 플랜과 연결할 수 있습니다. 자세한 내용은 [UM IP 게이트웨이](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-ip-gateways)를 참조하십시오.

필요한 경우 다음과 같이 EAC를 사용하여 UM IP 게이트웨이를 만들 수 있습니다.

1.  EAC에서 <strong>통합 메시징</strong> \> <strong>UM IP 게이트웨이</strong>로 이동한 다음 <strong>추가</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  <strong>새 UM IP 게이트웨이</strong> 페이지에서 다음 정보를 입력합니다.
    
      - <strong>이름</strong>   이 상자에 UM IP 게이트웨이의 고유 이름을 지정합니다. 이 이름은 EAC에 나타나는 표시 이름입니다. UM IP 게이트웨이를 만든 후 표시 이름을 변경해야 하는 경우 먼저 기존 UM IP 게이트웨이를 삭제한 다음 적합한 이름으로 다른 UM IP 게이트웨이를 만들어야 합니다. UM IP 게이트웨이 이름은 필수 항목이지만 표시 목적으로만 사용됩니다. 조직에서 여러 UM IP 게이트웨이를 사용할 수 있기 때문에 UM IP 게이트웨이에 의미 있는 이름을 사용하는 것이 좋습니다. UM IP 게이트웨이 이름의 최대 길이는 64자이며 공백을 포함할 수 있습니다. 그러나 다음 문자는 사용할 수 없습니다. " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - <strong>주소</strong>   IPv4 또는 IPv6 주소나 FQDN으로 UM IP 게이트웨이를 구성할 수 있습니다. 이 상자에 VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX에 구성된 IP 주소나 FQDN을 지정합니다. 이 상자에는 올바른 형식의 유효한 FQDN만 입력할 수 있습니다.
        
        알파벳과 숫자를 입력할 수 있습니다. IPv4 주소, IPv6 주소 및 FQDN을 사용할 수 있습니다. SIP 보안이나 보안 모드에서 작동하는 다이얼 플랜과 UM IP 게이트웨이 간에 상호 TLS를 사용하려는 경우 FQDN으로 UM IP 게이트웨이를 구성해야 합니다. 또한 포트 5061에서 수신 대기하도록 UM IP 게이트웨이를 구성하고, VoIP 게이트웨이 또는 IP PBX도 포트 5061에서 상호 TLS 요청을 수신 대기하도록 구성되었는지 확인해야 합니다. UM IP 게이트웨이를 구성하려면 셸에서 다음 명령을 실행합니다. `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`
        
        FQDN을 사용하는 경우 호스트 이름이 올바른 IP 주소로 확인되도록 VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX의 DNS 호스트 레코드가 올바르게 구성되었는지도 확인해야 합니다. 또한 IP 주소 대신 FQDN을 사용하고 UM IP 게이트웨이에 대한 DNS 구성이 변경된 경우 UM IP 게이트웨이의 구성 정보가 올바르게 업데이트되려면 UM IP 게이트웨이를 사용하지 않도록 설정한 후 사용하도록 다시 설정해야 합니다.
    
      - <strong>UM 다이얼 플랜</strong>   <strong>찾아보기</strong>를 클릭하여 UM IP 게이트웨이와 연결할 UM 다이얼 플랜을 선택합니다. UM IP 게이트웨이와 연결할 UM 다이얼 플랜을 선택하면 기본 UM 헌트 그룹도 만들어져 선택한 UM 다이얼 플랜과 연결됩니다. UM 다이얼 플랜을 선택하지 않는 경우 UM 헌트 그룹을 수동으로 만든 다음 해당 UM 헌트 그룹을 만든 UM IP 게이트웨이와 연결해야 합니다.

3.  <strong>저장</strong>을 클릭합니다.

필요한 경우 셸에서 다음 명령을 실행하여 UM IP 게이트웨이를 만들 수 있습니다.

```powershell
New-UMIPGateway -Identity MyUMIPGateway -Address "MyUMIPGateway.contoso.com"
```

필요한 경우 EAC를 사용하여 기존 UM IP 게이트웨이를 구성할 수 있습니다.

1.  EAC에서 <strong>통합 메시징</strong> \> <strong>UM IP 게이트웨이</strong>로 이동한 다음 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  <strong>UM IP 게이트웨이</strong> 페이지에서 <strong>구성</strong>을 클릭합니다. 구성 옵션을 사용하여 특정 UM IP 게이트웨이 설정을 보고, 기능을 사용하거나 사용하지 않도록 설정합니다.

필요한 경우 셸에서 다음 명령을 실행하여 기존 UM IP 게이트웨이를 구성할 수 있습니다.

```powershell
Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false
```

## 8단계: UM 헌트 그룹 만들기

기존 Exchange 2007 배포에 따라 새 UM 헌트 그룹을 만들어야 할 수 있습니다. 전화 통신 헌트 그룹을 사용하면 단일 번호로 걸려 온 전화 통화를 여러 내선 번호 또는 전화 번호로 분배할 수 있습니다. 통합 메시징에서 UM 헌트 그룹이란 전화 통신 헌트 그룹을 논리적으로 나타낸 것으로, UM IP 게이트웨이를 UM 다이얼 플랜에 연결합니다.

각 IP PBX 또는 PBX 헌트 그룹에 대해 UM 헌트 그룹이 하나 이상 있어야 합니다. 다음 절차를 완료하면 기본적으로 UM 헌트 그룹 한 개가 만들어집니다. IP PBX 또는 PBX 헌트 그룹이 둘 이상 있는 경우 추가 UM 헌트 그룹을 만들어야 합니다. UM 헌트 그룹에 대한 자세한 내용은 [UM 헌트 그룹](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups)을 참조하십시오.

필요한 경우 EAC를 사용하여 UM 헌트 그룹을 만들 수 있습니다.

1.  EAC에서 <strong>통합 메시징</strong> \> <strong>UM 다이얼 플랜</strong>으로 이동합니다. 목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  <strong>UM 다이얼 플랜</strong> 페이지의 <strong>UM 헌트 그룹</strong>에서 <strong>새로 만들기</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

3.  <strong>새 UM 헌트 그룹</strong> 페이지에서 다음 정보를 입력합니다.
    
      - <strong>이름</strong>   이 상자에 UM 헌트 그룹의 표시 이름을 입력합니다. UM 헌트 그룹 이름은 필수 항목이며 고유해야 하지만, EAC와 셸에 표시되는 용도로만 사용됩니다. 헌트 그룹을 만든 후 표시 이름을 변경해야 하는 경우에는 기존 헌트 그룹을 먼저 삭제한 다음 적합한 이름으로 다른 헌트 그룹을 만들어야 합니다. 조직에서 여러 개의 헌트 그룹을 사용하고 있는 경우 헌트 그룹에 대해 의미 있는 이름을 사용하는 것이 좋습니다. UM 헌트 그룹 이름의 최대 길이는 64자이며 공백을 포함할 수 있습니다. 그러나 다음 문자는 사용할 수 없습니다. " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - <strong>UM IP 게이트웨이</strong>   이 상자에서 UM IP 게이트웨이를 선택합니다. 이 상자에는 UM 헌트 그룹과 연결될 UM IP 게이트웨이의 이름이 표시됩니다. UM IP 게이트웨이를 UM 헌트 그룹에 연결하려면 <strong>찾아보기</strong>를 클릭합니다.
    
      - <strong>파일럿 식별자</strong>   이 상자에 PBX 또는 IP PBX에 구성된 파일럿 식별자를 고유하게 식별하는 문자열을 지정합니다. 이 상자에는 내선 번호나 SIP URI(Uniform Resource Identifier)를 사용할 수 있고, 영숫자 문자를 입력할 수 있습니다. 레거시 PBX의 경우 숫자 값이 파일럿 식별자로 사용됩니다. 그러나 일부 IP PBX 및 SIP 사용 가능 PBX는 SIP URI를 사용할 수 있습니다.

4.  <strong>저장</strong>을 클릭합니다.

필요한 경우 셸에서 다음 명령을 실행하여 UM 헌트 그룹을 만들 수 있습니다.

```powershell
New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialPlan MyUMDialPlan -UMIPGateway MyUMIPGateway
```

> [!TIP]
> UM 헌트 그룹의 설정은 구성하거나 변경할 수 없습니다. UM 헌트 그룹의 구성 설정을 변경하려면 해당 그룹을 삭제한 후 올바른 설정으로 새 UM 헌트 그룹을 추가해야 합니다.



## 9단계: UM 자동 전화 교환 만들기 또는 구성

기존 Exchange 2007 배포에 따라 새 UM 자동 전화 교환을 만들어야 할 수 있습니다. UM 자동 전화 교환을 사용하여 음성 메뉴 시스템을 만들 수 있으며, 이 시스템을 통해 외부 발신자 및 내부 발신자가 UM 자동 전화 교환 메뉴 시스템을 사용하여 원하는 사람을 찾고 조직 내의 회사 사용자나 부서로 전화를 걸거나 연결할 수 있습니다. 자세한 내용은 [자동으로 응답 한 들어오는 호출을 라우팅](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/automatically-answer-and-route-calls)을 참조하십시오.

소규모 배포에서는 발신자가 사용자에게 음성 메일만 남길 수 있도록 UM을 배포할 수도 있습니다. 이러한 배포에서는 자동 전화 교환을 만들 필요가 없습니다. 그러나 대부분의 경우 자동 전화 교환을 사용하면 외부 발신자가 조직에 전화를 걸 때 유용합니다.

필요한 경우 다음과 같이 EAC를 사용하여 UM 자동 전화 교환을 만들 수 있습니다.

1.  EAC에서 <strong>통합 메시징</strong> \> <strong>UM 다이얼 플랜</strong>으로 이동합니다. 자동 전화 교환을 추가할 UM 다이얼 플랜을 선택한 다음 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  <strong>UM 다이얼 플랜</strong> 페이지의 <strong>UM 자동 전화 교환</strong>에서 <strong>추가</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

3.  <strong>새 UM 자동 전화 교환</strong> 페이지에서 다음 상자에 해당 정보를 입력합니다.
    
      - <strong>이름</strong>   이 상자에 UM 자동 전화 교환의 표시 이름을 입력합니다. UM 자동 전화 교환 이름은 필수이며 고유해야 합니다. 하지만 이 이름은 EAC와 셸에 표시되는 용도로만 사용됩니다. 자동 전화 교환을 만든 후 표시 이름을 변경해야 하는 경우 먼저 기존 UM 자동 전화 교환을 삭제한 다음 적합한 이름으로 다른 자동 전화 교환을 만들어야 합니다. 조직에서 여러 개의 UM 자동 전화 교환을 사용하고 있는 경우 UM 자동 전화 교환에 대해 의미 있는 이름을 사용하는 것이 좋습니다. UM 자동 전화 교환 이름의 최대 길이는 64자이며 공백을 포함할 수 있습니다.
        
        새 UM 자동 전화 교환에 대해 공백이 포함된 이름을 지정할 수는 있지만, 통합 메시징과 Lync Server를 통합하는 경우 자동 전화 교환의 이름에 공백을 포함할 수 없습니다. 따라서 표시 이름에 공백이 포함된 자동 전화 교환을 만들고 Lync Server와 통합하는 경우 먼저 자동 전화 교환을 삭제한 다음 표시 이름에 공백이 포함되지 않은 다른 자동 전화 교환을 만들어야 합니다.
    
      - <strong>이 자동 전화 교환을 사용 가능하도록 만들기</strong>   UM 자동 전화 교환 만들기를 완료할 때 자동 전화 교환이 수신 전화에 응답할 수 있도록 하려면 이 확인란을 선택합니다. 새 자동 전화 교환을 만들면 기본적으로 사용할 수 없습니다. 사용하지 않도록 설정된 상태로 UM 자동 전화 교환을 만드는 경우 자동 전화 교환을 만드는 작업을 완료한 후 EAC나 셸을 사용하여 자동 전화 교환을 사용하도록 설정할 수 있습니다.
    
      - <strong>음성 명령에 응답하도록 자동 전화 교환 설정</strong>   UM 자동 전화 교환에 음성을 사용하도록 설정하려면 이 확인란을 선택합니다. 자동 전화 교환에서 음성을 사용하도록 설정하면 발신자가 터치톤이나 음성 입력을 사용하여 UM 자동 전화 교환에서 사용하는 시스템 또는 사용자 지정 음성 안내에 응답할 수 있습니다. 기본적으로 자동 전화 교환이 만들어질 때는 음성을 사용할 수 없습니다. 미국 영어(en-US) 이외의 언어로 음성 사용이 가능한 자동 전화 교환을 사용할 발신자의 경우 적절한 UM 언어 팩을 설치하고 이 언어를 사용하도록 자동 전화 교환의 속성을 구성해야 합니다. en-US UM 언어 팩은 Exchange 2013 사서함 서버를 설치할 때 기본적으로 설치됩니다.
    
      - <strong>액세스 번호</strong>   자동 전화 교환에 연결하기 위해 발신자가 사용할 내선 번호나 전화 번호를 입력합니다. 상자에 내선 번호나 전화 번호를 입력한 다음 <strong>추가</strong>를 클릭하여 목록에 번호를 추가합니다. 제공하는 내선 번호나 전화 번호의 자릿수가 연결된 UM 다이얼 플랜에서 구성된 내선 번호의 자릿수와 일치할 필요는 없습니다. 이것은 UM 자동 전화 교환에 대해 직접 통화가 허용되기 때문입니다.
        
        입력할 수 있는 내선 번호 또는 액세스 번호의 수에는 제한이 없습니다. 그러나 내선 번호 또는 전화 번호를 나열하지 않고 새 자동 전화 교환을 만들 수 있습니다. 내선 번호 또는 전화 번호는 필수 항목이 아닙니다. 기존 내선 번호 또는 파일럿 식별자를 편집하거나 제거할 수 있습니다. 기존 내선 번호 또는 전화 번호를 편집하려면 <strong>편집</strong>을 클릭합니다. 목록에서 기존 내선 번호 또는 전화 번호를 제거하려면 <strong>제거</strong>를 클릭합니다.

4.  <strong>저장</strong>을 클릭합니다.

필요한 경우 셸에서 다음 명령을 실행하여 UM 자동 전화 교환을 만들 수 있습니다.

```powershell
New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true -Status Enabled
```

필요한 경우 EAC를 사용하여 기존 자동 전화 교환을 구성할 수 있습니다.

1.  EAC에서 <strong>통합 메시징</strong> \> <strong>UM 다이얼 플랜</strong>으로 이동한 다음 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  <strong>UM 다이얼 플랜</strong> 페이지의 <strong>UM 자동 전화 교환</strong>에서 보거나 구성할 UM 자동 전화 교환을 선택한 다음 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다. 구성 옵션을 사용하여 특정 자동 전화 교환 설정을 보고, 기능을 사용하거나 사용하지 않도록 설정합니다.

필요한 경우 셸에서 다음 명령을 실행하여 기존 자동 전화 교환을 구성할 수 있습니다.

```powershell
Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true -StaroutToDialPlanEnabled $true
```

## 10단계: UM 사서함 정책 만들기 또는 구성

기존 Exchange 2007 배포에 따라 새 UM 사서함 정책을 만들거나 기존 UM 사서함 정책을 구성해야 할 수 있습니다. UM 사서함 정책은 통합 메시징을 사용자가 사용할 수 있도록 설정하는 데 필요합니다. 각 UM 사용 가능 사용자의 사서함은 단일 UM 사서함 정책에 연결되어야 합니다. 하나의 UM 사서함 정책을 만든 후에 하나 이상의 UM 사용 가능 사서함을 해당 UM 사서함 정책에 연결합니다. 이렇게 하면 해당 UM 사서함 정책에 연결된 UM 사용 가능 사용자에 대해 PIN의 최소 자릿수 또는 최대 로그온 시도 횟수와 같은 PIN 보안 설정을 제어할 수 있습니다. 자세한 내용은 [UM 사서함 정책](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policies)을 참조하십시오.

필요한 경우 EAC를 사용하여 UM 사서함 정책을 만들 수 있습니다.

1.  EAC에서 <strong>통합 메시징</strong> \> <strong>UM 다이얼 플랜</strong>으로 이동합니다. 목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  <strong>UM 다이얼 플랜</strong> 페이지의 <strong>UM 사서함 정책</strong>에서 <strong>추가</strong> ![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭합니다.

3.  <strong>새 UM 사서함 정책</strong> 페이지의 <strong>이름</strong> 상자에 새 UM 사서함 정책의 이름을 입력합니다.
    

    > [!NOTE]
    > 이 상자에 UM 사서함 정책의 고유 이름을 지정합니다. 이 이름은 EAC에 나타나는 표시 이름입니다. UM 사서함 정책을 만든 후 표시 이름을 변경해야 하는 경우 기존 UM 사서함 정책을 먼저 삭제한 다음 적합한 이름으로다른 UM 사서함 정책을 만들어야 합니다. UM 사용 가능 사용자가 연결되어 있는 UM 사서함 정책은 삭제할 수 없습니다. UM 사서함 정책 이름은 필수 항목이지만 표시 목적으로만 사용됩니다. 조직에서 여러 개의 UM 사서함 정책을 사용할 수 있기 때문에 UM 사서함 정책에 대해 의미 있는 이름을 사용하는 것이 좋습니다. UM 사서함 정책 이름의 최대 길이는 64자이며 공백을 포함할 수 있습니다. 그러나 다음 문자는 사용할 수 없습니다. " / \ [ ] : ; | = , + * ? &lt; &gt;.



4.  <strong>저장</strong>을 클릭합니다.
    

    > [!NOTE]
    > UM 사서함 정책을 저장할 때 PIN 정책, 음성 메일 기능 및 보호된 음성 메일 설정을 비롯한 모든 기본 설정이 사용되도록 설정됩니다. 방금 만든 UM 사서함 정책의 기본 설정을 사용자 지정하거나 변경하려면 <STRONG>Set-UMMailbox</STRONG> cmdlet 또는 EAC를 사용합니다.



필요한 경우 셸에서 다음 명령을 실행하여 UM 사서함 정책을 만들 수 있습니다.

```powershell
New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan
```

필요한 경우 EAC를 사용하여 기존 UM 사서함 정책을 구성할 수 있습니다.

1.  EAC에서 <strong>통합 메시징</strong> \> <strong>UM 다이얼 플랜</strong>으로 이동한 다음 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  <strong>UM 다이얼 플랜</strong> 페이지의 <strong>UM 사서함 정책</strong>에서 보거나 구성하려는 UM 사서함 정책을 선택하고 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다. 구성 옵션을 사용하여 특정 UM 사서함 정책 설정을 보고, 기능을 사용하거나 사용하지 않도록 설정합니다.

필요한 경우 셸에서 다음 명령을 실행하여 기존 UM 사서함 정책을 구성할 수 있습니다.

```powershell
Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."
```

## 11단계: 기존 UM 사용 가능 사서함을 Exchange 2013으로 이동

Exchange 2007 통합 메시징에서 조직의 사용자가 음성 메일을 사용하도록 설정하고 나면 사용자가 UM 기능을 사용할 수 있도록 UM 속성의 기본 집합이 사용자에게 적용됩니다. 자세한 내용은 [사용자에 대 한 음성 메일](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-for-users)을 참조하십시오.

업그레이드 프로세스 동안 Exchange 2007 사서함 서버 및 Exchange 2013 사서함 서버 둘 다에서 일정 기간 동안 UM 사용 가능 사서함이 포함됩니다. 그러나 모든 UM 사용 가능 사용자를 Exchange 2013 사서함 서버로 이동하려면 Exchange 2013 서버의 셸에서 <strong>New-MoveRequest</strong> cmdlet을 사용하거나 EAC를 사용하여 모든 속성과 설정(사용자의 PIN 포함)을 보존해야 합니다.

이동 요청은 한 사서함 데이터베이스에서 다른 사서함 데이터베이스로 사서함을 이동하는 프로세스입니다. 로컬 이동 요청은 단일 포리스트 내에서 발생하는 사서함 이동입니다. 사서함 이동에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Exchange 2013 사서함 이동](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

  - [New-MoveRequest](https://technet.microsoft.com/ko-kr/library/dd351123\(v=exchg.150\))

  - [New-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219166\(v=exchg.150\))

  - [사서함 이동](https://go.microsoft.com/fwlink/p/?linkid=296351)

EAC를 사용하여 Exchange 2007 사서함을 Exchange 2013 사서함 서버로 이동하려면

1.  EAC에서 <strong>받는 사람</strong> \> <strong>마이그레이션</strong>을 클릭한 후 <strong>추가</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭합니다.

2.  <strong>새 로컬 사서함 이동</strong> 마법사에서 이동할 사용자를 선택하고 <strong>확인</strong>을 클릭한 후 <strong>다음</strong>을 클릭합니다.

3.  <strong>이동 구성</strong> 페이지에서 새 일괄 처리의 이름을 지정합니다. 보관 사서함에 대해 원하는 옵션과 사서함 데이터베이스 위치를 선택하고 <strong>새로 만들기</strong>를 클릭합니다.

셸을 사용하여 Exchange 2007사서함을 Exchange 2013 사서함 서버로 이동하려면 다음 명령을 실행합니다.

```powershell
New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase "DB01"
```

## 12단계: 새 사용자가 UM을 사용하도록 설정하거나 기존 UM 사용 가능 사용자의 설정 구성

사용자가 통합 메시징을 사용할 수 있으려면 사서함이 있어야 합니다. 그러나 사서함이 있는 사용자는 기본적으로 UM을 사용하도록 설정되지 않습니다. 사용자가 UM을 사용할 수 있으면 해당 사용자에 대한 UM 속성과 음성 메일 기능을 관리, 수정 및 구성할 수 있습니다. EAC 또는 셸을 사용하여 사용자가 UM을 사용하도록 설정할 수 있습니다. 자세한 내용은 [사용자에 대 한 음성 메일](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-for-users)을 참조하십시오.

사용자가 UM을 사용하도록 설정할 때는 음성 메일이 사용자의 사서함에 전송될 때 UM에서 사용할 내선 번호를 최소 하나 이상 정의해야 합니다. 그래야 사용자가 Outlook Voice Access를 사용할 수 있습니다. 사용자가 UM을 사용하도록 설정한 후에는 EAC에서 보조 내선 번호를 사용자 사서함에 추가하거나, 사용자 사서함에 EUM(Exchange 통합 메시징) 프록시 주소를 구성하여 내선 번호를 수정 또는 제거하거나, 사용자에 대한 추가/보조 내선 번호를 추가 또는 제거할 수 있습니다. 내선 번호, E.164 번호 또는 SIP 주소를 추가, 수정 또는 제거하려면 [음성 메일 사용이 가능한 사용자 절차](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-enabled-user-procedures)를 참조하십시오.

EAC를 통해 사용자가 통합 메시징을 사용하도록 설정하려면 다음을 수행합니다.

1.  EAC에서 <strong>받는 사람</strong>을 클릭합니다.

2.  목록 보기에서 통합 메시징을 사용하도록 설정할 사서함의 사용자를 선택합니다.

3.  세부 정보 창의 <strong>전화 및 음성 기능</strong>에서 <strong>사용</strong>을 클릭합니다.

4.  <strong>UM 사서함 사용</strong> 페이지에서 <strong>UM 사서함 정책</strong> 옆에 있는 <strong>찾아보기</strong> 단추를 클릭하고 목록에서 사용자를 할당할 UM 사서함 정책을 찾은 다음 <strong>확인</strong>을 클릭합니다.

5.  <strong>UM 사서함 사용</strong> 페이지에서 다음 상자에 해당 정보를 입력합니다.
    
      - <strong>SIP 주소 또는 E.164 번호</strong>   사용자의 SIP 주소나 E.164 번호를 입력합니다. 통합 메시징을 사용할 수 있도록 설정한 사용자가 SIP URI 또는 E.164 다이얼 플랜에 연결된 UM 사서함 정책에 할당된 경우 이 옵션을 사용할 수 있습니다. 사용자가 내선 번호 다이얼 플랜에 연결되어 있으면 사용자의 SIP 주소 또는 E.164 번호를 추가할 수 없습니다. SIP URI 또는 E.164 다이얼 플랜에 연결된 UM 사서함 정책에 사용자를 할당할 경우에도 사용자의 내선 번호는 입력해야 합니다. 이 내선 번호는 사용자가 Outlook Voice Access를 사용하여 사서함에 액세스할 때 사용됩니다. 이 상자에서 구성하는 자릿수는 SIP URI 또는 E.164 다이얼 플랜에 구성된 자릿수와 일치해야 합니다.
    
      - <strong>내선 번호</strong>   UM을 사용할 수 있도록 설정할 사용자의 내선 번호를 입력합니다.
        
        사용자의 올바른 내선 번호를 입력해야 하며, 번호가 다이얼 플랜에 지정된 자릿수와 일치해야 합니다. 1에서 20까지의 숫자만 입력할 수 있습니다. 일반적인 내선 번호의 길이는 3~7자리입니다. 내선 번호의 자릿수는 사용자에게 할당된 UM 사서함 정책에 연결된 다이얼 플랜에서 설정됩니다.
    
      - <strong>PIN 설정</strong>에서 다음 상자에 해당 정보를 입력합니다.
        
          - <strong>PIN 자동 생성</strong>   UM 사용 가능 사용자가 Outlook Voice Access를 통한 음성 메일 액세스에 사용할 PIN을 자동으로 생성하려면 이 단추를 클릭합니다. 기본 설정입니다. 이 단추를 클릭하면 사용자에게 할당된 UM 사서함 정책에 구성된 PIN 정책을 기반으로 PIN이 자동으로 생성됩니다. 이 설정을 사용하여 사용자 PIN을 보호하는 것이 좋습니다. PIN은 사용자가 UM을 사용하도록 설정된 이후에 받는 환영 메시지를 통해 전송됩니다. 기본적으로는 음성 메일을 받기 위해 사서함에 처음 로그인할 때 이 PIN을 변경해야 합니다.
        
          - <strong>PIN 입력</strong>   사용자가 음성 메일 시스템에 액세스할 때 사용할 PIN을 직접 지정하려면 이 단추를 클릭합니다. PIN은 이 UM 사용 가능 사용자와 연결된 UM 사서함 정책에 구성된 PIN 정책 설정을 따라야 합니다. 예를 들어, 7자리 이상의 PIN만 받도록 UM 사서함 정책을 구성한 경우에는 이 상자에 입력하는 PIN의 길이가 7자리 이상이어야 합니다.
        
          - <strong>사용자에게 처음 로그인할 때 PIN 다시 설정 요구</strong>   사용자가 Outlook Voice Access를 사용하여 전화로 음성 메일 시스템에 처음으로 액세스할 때 음성 메일 PIN을 강제로 다시 설정하게 하려면 이 확인란을 선택합니다. 기억하기 좋은 PIN을 입력하라는 메시지가 표시됩니다. 이 옵션은 UM 사용 가능 사용자가 처음 로그인할 때 강제로 PIN을 변경하도록 하여 데이터 및 받은 편지함에 대한 무단 액세스로부터 보호하는 가장 좋은 보안 방법입니다. 이 확인란은 기본적으로 선택되어 있습니다.

6.  <strong>UM 사서함 사용</strong> 페이지에서 설정을 검토합니다. 사용자가 통합 메시징을 사용하도록 설정하려면 <strong>마침</strong>을 클릭합니다. 구성을 변경하려면 <strong>뒤로</strong>를 클릭합니다.

셸에서 사용자가 통합 메시징을 사용하도록 설정하려면 다음 명령을 실행합니다.

```powershell
Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -NotifyEmail administrator@contoso.com -PINExpired $true
```

필요한 경우 EAC를 사용하여 UM을 사용하도록 설정된 사용자를 구성할 수 있습니다.

1.  EAC에서 <strong>받는 사람</strong> \> <strong>사서함</strong>으로 이동합니다.

2.  목록 보기에서 UM 사서함 정책을 변경할 사서함을 선택합니다.

3.  세부 정보 창의 <strong>전화 및 음성 기능</strong> \> <strong>통합 메시징</strong>에서 <strong>자세히 보기</strong>를 클릭합니다.

4.  <strong>UM 사서함</strong> 페이지에서 <strong>UM 사서함 설정</strong>을 클릭하여 기존 UM 사용 가능 사용자의 다음 UM 속성을 보거나 변경합니다.
    
      - <strong>PIN 상태</strong>   이 표시 전용 상자에는 사용자 사서함의 상태가 표시됩니다. 기본적으로 사용자가 UM을 사용하면 PIN 상태가 <strong>잠겨 있지 않음</strong>으로 표시됩니다. 그러나 사용자가 잘못된 Outlook Voice Access PIN을 여러 번 입력하면 상태가 <strong>잠겨 있음</strong>으로 표시됩니다.
    
      - <strong>UM 사서함 정책</strong>   이 상자에는 UM 사용 가능 사용자와 연결되는 UM 사서함 정책의 이름이 표시됩니다. <strong>찾아보기</strong>를 클릭하여 이 UM 사서함과 연결되는 UM 사서함 정책을 찾아서 지정할 수 있습니다.
    
      - <strong>개인 교환원 내선 번호</strong>   사용자의 교환원 내선 번호를 지정하려면 이 상자를 사용합니다. 기본적으로 내선 번호는 구성되지 않습니다. 내선 번호는 1~20자까지 사용할 수 있습니다. UM 사용 가능 사용자에 대한 수신 전화를 이 상자에 지정하는 내선 번호로 전달할 수 있습니다.
        
        다이얼 플랜과 자동 전화 교환에서 다른 유형의 교환원 내선 번호를 구성할 수 있습니다. 그러나 해당 내선 번호는 일반적으로 회사 전체의 접수원이나 교환원에게 의미가 있습니다. 개인 교환원 내선 번호 설정은 관리자의 비서나 개인 비서가 특정 사용자에 대한 수신 전화에 응답할 때 사용될 수 있습니다.

5.  <strong>UM 사서함</strong> 페이지의 <strong>다른 내선 번호</strong>에서 사용자의 내선 번호를 추가, 변경 및 확인할 수 있습니다.
    
      - 내선 번호를 추가하려면 <strong>추가</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다. <strong>다른 내선 번호 추가</strong> 페이지에서 <strong>찾아보기</strong>를 통해 UM 다이얼 플랜을 선택하고 <strong>내선 번호</strong> 상자에 내선 번호를 입력합니다.
    
      - 내선 번호를 제거하려면 제거할 내선 번호를 선택하고 <strong>제거</strong>![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭합니다.

6.  변경한 내용이 있으면 <strong>저장</strong>을 클릭합니다.

필요한 경우 셸에서 다음 명령을 실행하여 사용자가 UM을 사용하도록 구성할 수 있습니다.

```powershell
Set-UMMailbox -Identity tony@contoso.com -CallAnsweringAudioCodec Wma -CallAnsweringRulesEnabled $false -FaxEnabled $false -UMSMSNotificationOption VoiceMail
```

## 13단계: Exchange 2013 클라이언트 액세스 서버로 들어오는 모든 수신 전화를 전송하도록 VoIP 게이트웨이, IP PBX 및 SIP 사용 가능 PBX 구성

Exchange 2013 클라이언트 액세스 서버 및 사서함 서버는 설치할 때 자동으로 사용하도록 설정되므로 수신 및 발신 음성 통화에 응답하고 음성 메일 메시지를 지정된 받는 사람에게 라우팅할 수 있습니다. Exchange 2013 클라이언트 액세스 서버 및 사서함 서버를 설치하고 통합 메시징을 배포할 때는 Exchange 2013 클라이언트 액세스 서버 또는 사서함 서버를 UM 다이얼 플랜에 연결하거나 추가할 필요가 없습니다. Exchange 2013 클라이언트 액세스 서버 및 사서함 서버는 모든 수신 전화에 응답한 후 UM 다이얼 플랜을 사용하여 사용자의 위치를 찾아냅니다.

Exchange 2013 클라이언트 액세스 서버는 통합 메시징의 인바운드 통화나 SIP(Session Initiation Protocol) 요청에 대한 진입점 역할을 합니다. Exchange 2013 클라이언트 액세스 서버에서 SIP 요청을 처리하는 서비스인 UM 통화 라우터 서비스는 조직의 각 Exchange 2013 클라이언트 액세스 서버에서 실행됩니다.

Exchange 2013 UM으로 업그레이드할 때는 전화 통신 네트워크의 PBX에 연결하기 위한 VoIP 게이트웨이 하나 또는 여러 개를 이미 설치 및 구성했거나, SIP(Session Initiation Protocol) 사용 가능 PBX 또는 IP PBX를 설치 및 구성한 상태여야 합니다.

Exchange 2013 UM으로 업그레이드하는 과정의 마지막 단계는 VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX가 수신 전화(사용자에게 음성 메일을 남기려는 발신자, Outlook Voice Access로 전화를 거는 UM 사용 가능 사용자의 전화 및 UM 자동 전화 교환으로 전화를 거는 발신자의 전화 포함)를 Exchange 2013 클라이언트 액세스 서버로 보내도록 구성하는 것입니다. 이러한 모든 통화는 먼저 VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX에서 수신된 다음 Exchange 2013 조직의 Exchange 2013 클라이언트 액세스 서버로 전달됩니다. 자세한 내용은 다음 리소스를 참조하십시오.

  -  [UM 서비스](um-services-exchange-2013-help.md)

  -  [지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)

  -  [Exchange 2013에 대 한 전화 통신 관리자](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013)

## 14단계: Exchange 2007 통합 메시징 서버에서 전화 응답을 사용하지 않도록 설정

Exchange 2007 통합 메시징 서버에서 UM을 사용하지 않도록 설정하거나 다이얼 플랜에서 UM 서버를 제거하여 전화 응답을 사용하지 않도록 설정할 수 있습니다. UM을 사용하지 않도록 설정하면 통합 메시징 서버에서 수신 전화에 응답하지 못합니다. 모든 통화의 연결을 즉시 끊거나 기존 통화가 처리될 때까지 기다린 후 통합 메시징 서버를 사용하지 않도록 설정할 수 있습니다. 서버가 수신 전화 처리를 완료하도록 하려면 다이얼 플랜에서 서버를 제거하기 전에 전화 응답을 사용하지 않도록 설정해야 합니다.

Exchange 관리 콘솔을 사용하여 Exchange 2007 UM 서버에서 통합 메시징을 사용하지 않도록 설정하려면 다음을 수행합니다.

1.  EMC의 콘솔 트리에서 <strong>서버 구성</strong> \> <strong>통합 메시징</strong>으로 이동합니다.

2.  결과 창에서 사용하지 않도록 설정할 통합 메시징 서버를 선택합니다.

3.  작업 창에서 다음 중 하나를 클릭합니다.
    
    1.  <strong>즉시 사용 안 함</strong> 옵션을 선택하면 통합 메시징 서버에 연결되어 있는 모든 통화의 연결이 끊어집니다.
    
    2.  <strong>통화 완료 후 사용 안 함</strong> 옵션을 선택하면 통합 메시징 서버가 새로운 통화를 받아들이지 않고 모든 통화가 처리된 후에야 사용할 수 없도록 설정됩니다.

4.  확인 대화 상자에서 <strong>예</strong>를 클릭하여 계속합니다.

셸을 사용하여 Exchange 2007 UM 서버에서 통합 메시징을 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

```powershell
Disable-UMServer -Identity MyUMServer -Immediate $true
```


> [!TIP]
> Exchange 2007 UM 서버에서 <STRONG>Disable-UMServer</STRONG> cmdlet을 사용하거나 Exchange 2013 사서함 서버에서 <STRONG>Disable-UMService</STRONG> cmdlet을 사용하여 전화 응답을 사용하지 않도록 설정할 수 있습니다.



## 15단계: 다이얼 플랜에서 Exchange 2007 통합 메시징 서버 제거

통화를 처리하려면 Exchange 2007 UM 서버를 하나 이상의 UM 다이얼 플랜에 추가해야 합니다. UM 서버 하나를 여러 UM 다이얼 플랜에 추가할 수 있습니다. UM 다이얼 플랜에서 Exchange 2007 UM 서버를 제거할 수 있습니다. 다이얼 플랜에서 제거한 UM 서버는 더 이상 전화에 응답하거나 UM 사용 가능 사용자에 대한 UM 통화를 처리하지 않습니다.

Exchange 관리 콘솔을 사용하여 다이얼 플랜에서 Exchange 2007 UM 서버를 제거하려면 다음을 수행합니다.

1.  EMC의 콘솔 트리에서 <strong>서버 구성</strong> \> <strong>통합 메시징</strong>으로 이동합니다.

2.  결과 창에서 통합 메시징 서버를 선택합니다.

3.  작업 창에서 <strong>속성</strong>을 클릭합니다.

4.  <strong>UM 설정</strong> 탭의 <strong>연결된 다이얼 플랜</strong> 섹션에서 <strong>제거</strong>를 클릭합니다.

5.  확인 대화 상자에서 <strong>예</strong>를 클릭하여 UM 다이얼 플랜에서 Exchange 2007 통합 메시징 서버 삭제를 확인합니다.

6.  <strong>확인</strong>을 클릭하여 속성 창을 닫습니다.

셸을 사용하여 다이얼 플랜에서 Exchange 2007 UM 서버를 제거하려면 다음 명령을 실행합니다.

```powershell
$dp= Get-UMDialPlan "MySIPDialPlan"
$s=Get-UMServer -id MyUMServer
$s.dialplans-=$dp.identity
Set-UMServer -id MyUMServer -dialplans:$s.dialplans
```

이 예에는 SipDP1, SipDP2, SipDP3의 3개 SIP URI 다이얼 플랜이 있습니다. 이 예에서는 `MyUMServer`라는 UM 서버를 SipDP3 다이얼 플랜에서 제거합니다.

```powershell
Set-UMServer -id MyUMServer -DialPlans SipDP1,SipDP2
```

이 예에는 SipDP1 및 SipDP2의 2개 SIP URI 다이얼 플랜이 있습니다. 이 예에서는 `MyUMServer`라는 UM 서버를 SipDP2 다이얼 플랜에서 제거합니다.

```powershell
Set-UMServer -id MyUMServer -DialPlans SipDP1
```


> [!TIP]
> Exchange 2007 통합 메시징 서버의 셸에서 <STRONG>Set-UMServer</STRONG> cmdlet을 사용하거나 Exchange 2013 사서함 서버에서 <STRONG>Set-UMService</STRONG> cmdlet을 사용하여 다이얼 플랜 하나 또는 여러 개에서 Exchange 2007 UM 서버를 제거할 수 있습니다. 예를 들어 모든 다이얼 플랜에서 UM 서버를 제거하려면 다음 명령을 실행합니다. <CODE>Set-UMServer -identity MyUMServer -DialPlan $null</CODE>



## 작동 여부는 어떻게 확인합니까?

통합 메시징을 설정한 후 다음 사항을 통해 통합 메시징이 제대로 작동하는지 확인할 수 있습니다.

  - 음성 메일을 사용하도록 설정한 사용자가 Outlook Web App 또는 Outlook에 로그인하고 통합 메시징 환영 메시지를 볼 수 있는지 여부.

  - UM 사용자가 음성 메시지를 받을 수 있는지 여부.

  - UM 사용자가 Outlook Voice Access 번호로 전화를 걸어 전자 메일, 일정 항목 및 음성 메일을 들을 수 있는지 여부.

  - UM에서 조직 외부 전화를 라우팅하며 사용자가 전화를 걸 수 있는지 여부.

