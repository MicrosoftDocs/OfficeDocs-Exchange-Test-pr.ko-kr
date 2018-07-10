---
title: '오프 라인 주소록 가상 디렉터리 만들기: Exchange 2013 Help'
TOCTitle: 오프 라인 주소록 가상 디렉터리 만들기
ms:assetid: 2c70e21f-2b12-414a-9e8c-65634a767c72
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996917(v=EXCHG.150)
ms:contentKeyID: 50482718
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 오프 라인 주소록 가상 디렉터리 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-16_

OAB 가상 디렉터리는 OAB의 배포입니다. Microsoft Exchange Server 2013을 설치하면 기본적으로 IIS(인터넷 정보 서비스)의 기본 내부 웹 사이트에 OAB라는 새 가상 디렉터리가 만들어집니다. 조직의 방화벽 외부에서 MicrosoftOutlook에 연결하는 클라이언트 쪽 사용자인 경우 외부 웹 사이트를 추가할 수 있습니다. 또는 셸에서 **New-OABVirtualDirectory** cmdlet을 실행하는 경우 로컬 Exchange 서버의 기본 IIS 웹 사이트에 새 가상 디렉터리 OAB가 만들어집니다.

OAB 가상 디렉터리를 만드는 것은 일반적인 작업이 아닙니다. Exchange에서는 이름이 OAB인 OAB 가상 디렉터리를 하나만 허용하므로 기존 OAB 가상 디렉터리에 문제가 있고 이전 OAB 가상 디렉터리가 제거된 경우에만 OAB 가상 디렉터리를 만들어야 합니다.

OAB와 관련된 추가 관리 작업에 대한 자세한 내용은 [오프 라인 주소록 절차](offline-address-book-procedures-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> OAB 가상 디렉터리를 만들기 전에 사용자가 변경 작업에 대해 알고 있어야 합니다. 이 프로세스로 인해 사용자의 OAB 다운로드 프로세스가 중단될 수 있기 때문입니다.



## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "오프라인 주소록" 항목

  - 로컬 Exchange 서버에 클라이언트 액세스 서버 역할이 설치되어 있어야 합니다.

  - 기본 IIS 웹 사이트(예: /w3svc/1/root)가 있어야 합니다.

  - 가상 디렉터리 OAB가 아직 없습니다.

  - 기본적으로는 웹 기반 배포가 사용되며 추가로 구성 작업을 수행할 필요가 없지만, OAB 배포 지점에 대해 SSL(Secure Sockets Layer)을 사용하도록 설정하는 것이 좋습니다.

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 OAB 가상 디렉터리 만들기

모든 기본 설정을 지정하여 OAB 가상 디렉터리를 만들려면 매개 변수 없이 **New-OABVirtualDirectory** cmdlet을 실행합니다. 사용자 지정 설정으로 OAB 가상 디렉터리를 만들려면 다음 절차를 사용하십시오.


> [!NOTE]
> OAB 가상 디렉터리를 만들 때는 SSL을 사용할 수 있도록 설정하는 것이 좋습니다.



이 예에서는 SSL을 사용하도록 설정되어 있고 외부 URL이 있는 CASServer01이라는 클라이언트 액세스 서버에 OAB 가상 디렉터리를 만듭니다.

    New-OABVirtualDirectory -Server CASServer01 -RequireSSL $true -ExternalURL "https://www.contoso.com/OAB"

새 OAB 가상 디렉터리를 만든 후에 웹 기반 배포를 사용하여 OAB 가상 디렉터리에 다시 연결하는 각 OAB의 설정을 편집해야 합니다. 자세한 내용은 [오프 라인 주소록 생성 일정이 변경](change-the-offline-address-book-generation-schedule-exchange-2013-help.md)을 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [New-OabVirtualDirectory](https://technet.microsoft.com/ko-kr/library/bb123735\(v=exchg.150\))를 참조하십시오.

