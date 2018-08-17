---
title: 'UM에 대 한 인증서를 만듭니다.: Exchange 2013 Help'
TOCTitle: UM에 대 한 인증서를 만듭니다.
ms:assetid: 66807ee7-3d3f-482d-a3ac-d4e9baca3271
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn205141(v=EXCHG.150)
ms:contentKeyID: 54651823
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM에 대 한 인증서를 만듭니다.

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-04-29_

셸이나 EAC에서 새 Exchange 인증서 마법사를 사용하여 내부 PKI(공개 키 인프라) 인증서에 대한 인증서 요청이나 자체 서명된 인증서를 만들 수 있습니다. UM(통합 메시징)의 경우 Microsoft Exchange 통합 메시징 서비스 및 Microsoft Exchange 통합 메시징 통화 라우터 서비스 둘 다에 대해 이러한 인증서 중 하나를 사용할 수 있습니다. 두 서비스에 대해 같은 인증서를 사용해도 되고 서비스마다 다른 인증서를 사용해도 됩니다. UM 서비스에 대해 타사 상업용 인증서를 구입한 후 가져올 수도 있습니다. UM에 대해 자체 서명된 인증서를 사용하는 경우 SAN(주체 대체 이름)에 클라이언트 액세스 서버 및 사서함 서버의 이름을 포함해야 할 수 있습니다.

기본적으로 Exchange Server 2013 설치 시 두 개의 자체 서명된 인증서 즉, **Microsoft Exchange Server 인증 인증서** 및 **Microsoft Exchange**가 만들어집니다. **Microsoft Exchange** 자체 서명된 인증서를 UM에서 사용하여 데이터를 암호화할 수는 있지만, 이렇게 하려면 인증서를 UM 서비스 및 UM 통화 라우터 서비스에 할당해야 합니다. 인증서를 통합 메시징 서비스에 할당하고 나면 VoIP 게이트웨이, IP PBX 및 SIP 사용 가능 PBX로 복사하고 가져올 수 있습니다. 단, 기본 자체 서명된 인증서를 사용하는 대신 통합 메시징에 대해 구체적으로 다른 인증서를 만들어야 할 수 있습니다.


> [!WARNING]
> UM을 Microsoft Lync Server에 통합한 경우에는 자체 서명된 인증서를 사용할 수 없습니다.



통합 메시징용 인증서 관리와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 절차에 대 한 인증서를 배포합니다.](deploying-certificates-for-um-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "인증서 관리" 항목 및 [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 서비스" 항목 역시 해당 컴퓨터의 로컬 관리자 그룹 구성원인 계정을 사용하여 로그온해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM에 대한 인증서 요청 만들기

1.  EAC에서 **서버** \> **인증서**로 이동한 후 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 Exchange 인증서** 페이지에서 **인증 기관의 인증서에 대한 요청 만들기**를 선택하고 **다음**을 클릭합니다.

3.  인증서의 이름을 입력하고 **다음**을 클릭합니다.

4.  와일드카드 인증서가 필요하지 않으면 **다음**을 클릭합니다. 와일드카드 인증서가 필요하면 <strong>와일드카드 인증서를 요청합니다. 와일드카드 인증서를 사용하면 단일 인증서로 루트 도메인 아래의 모든 하위 도메인을 보호할 수 있습니다.</strong>를 선택하고 루트 도메인 이름을 입력한 후 **다음**을 클릭합니다.

5.  **이 서버에 인증서 요청 저장**에서 **찾아보기**를 클릭하여 파일을 저장할 위치로 이동합니다. Exchange 조직의 아무 클라이언트 액세스 서버 또는 사서함 서버에 인증서 요청을 저장할 수 있습니다. 위치를 선택하고 **확인**을 클릭한 후 **다음**을 클릭합니다.

6.  와일드카드 인증서를 요청한 경우 9단계로 건너뜁니다.

7.  와일드카드 인증서를 요청하지 않은 경우에는 인증서에 포함할 도메인을 지정해야 합니다. 도메인을 편집하려면 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하고 **다음**을 클릭합니다.

8.  <strong>선택 항목을 바탕으로 다음 도메인이 인증서에 포함됩니다. 여기에서 도메인을 더 추가하거나 원하는 항목을 변경할 수 있습니다.</strong>에서 **도메인** 아래에 나열된 도메인 이름을 추가, 편집, 제거 또는 확인할 수 있습니다. **다음**을 클릭합니다.

9.  <strong>조직에 대한 정보를 지정합니다. 이 정보는 인증 기관에서 필요로 합니다.</strong>에서 다음 정보를 입력합니다.
    
      - **조직 이름**
    
      - **부서 이름**
    
      - **구/군/시**
    
      - **시/도**
    
      - **국가/지역 이름**   이 옵션에서는 드롭다운 목록을 사용하여 국가나 지역을 선택합니다.

10. **다음 파일에 인증서 요청 저장**에서 인증서 파일 이름을 입력한 후 **마침**을 클릭합니다.

## 셸을 사용하여 UM에 대한 인증서 요청 만들기

이 예에서는 `MyMailboxServer`라는 사서함 서버에 대해 이름이 `CertUM`인 새 Exchange 인증서 요청을 만듭니다.

    New-ExchangeCertificate -FriendlyName 'CertUM' -GenerateRequest -PrivateKeyExportable $true -KeySize '2048' -DomainName '*.northwindtraders.com' -SubjectName 'C=US,S=wa,L=redmond,O=northwindtraders,OU=servers,CN= northwindtraders.com' -Server 'MyMailboxServer'

## EAC를 사용하여 UM에 대한 자체 서명된 인증서 만들기

1.  EAC에서 **서버** \> **인증서**로 이동한 후 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 Exchange 인증서** 페이지에서 **자체 서명된 인증서 만들기**를 선택한 후 **다음**을 선택합니다.

3.  인증서의 이름을 입력하고 **다음**을 선택합니다.

4.  **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 이 인증서를 적용할 Exchange 서버를 선택한 후 **다음**을 선택합니다.

5.  인증서에 포함할 도메인을 지정하고 **다음**을 선택합니다. 서비스에 대해 도메인을 추가하려면 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

6.  포함한 도메인이 올바른지 확인한 후 **마침**을 선택합니다.


> [!IMPORTANT]
> EAC를 사용하여 자체 서명된 인증서를 만들 경우 인증서에 대해 서비스를 사용하도록 설정하라는 메시지가 표시되지 않습니다. 인증서를 만들고 난 후 EAC를 사용하거나 셸에서 <STRONG>Enable-ExchangeCertificate</STRONG> cmdlet을 사용하여 Exchange 서비스를 사용하도록 설정할 수 있습니다. 인증서를 UM 서비스에 할당하는 방법에 대한 자세한 내용은 <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">UM 및 UM 통화 라우터 서비스에 인증서 할당</A>을 참조하십시오.



## 셸을 사용하여 UM에 대한 자체 서명된 인증서 만들기

이 예에서는 `MyMailboxServer`라는 사서함 서버에 대해 이름이 `UMCert`인 새 Exchange 자체 서명된 인증서를 만듭니다.

    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true


> [!TIP]
> <EM>Services</EM> 매개 변수를 사용하여 사용하도록 설정할 서비스를 지정할 경우 해당 서비스를 할당하라는 메시지가 표시됩니다. 이 예에서는 UM 및 UM 통화 라우터 서비스에서 인증서를 사용하도록 설정하라는 메시지가 표시됩니다. 서비스에서 인증서를 사용하도록 설정하는 방법에 대한 자세한 내용은 <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">UM 및 UM 통화 라우터 서비스에 인증서 할당</A>을 참조하십시오.


