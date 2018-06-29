---
title: 'Exchange ActiveSync 가상 디렉터리 관리 작업: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync 가상 디렉터리 관리 작업
ms:assetid: f0b339b7-e184-4392-a133-20523183459d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125170(v=EXCHG.150)
ms:contentKeyID: 50484499
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange ActiveSync 가상 디렉터리 관리 작업

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-05_

여러 Exchange ActiveSync 가상 디렉터리를 통해 Exchange Server 2013Exchange ActiveSync 응용 프로그램 설정을 관리할 수 있습니다. 가상 디렉터리를 Exchange ActiveSync 와 같은 웹 응용 프로그램에 대 한 액세스를 허용 하도록 인터넷 정보 서비스 (IIS)에서 사용 됩니다. Exchange ActiveSync 에 대 한 관리할 수 있는 가상 디렉터리 설정 중 일부를 인증, 보안 및 보고를 포함 합니다.

## Exchange ActiveSync 가상 디렉터리 설정

다음 속성 및 Exchange ActiveSync 가상 디렉터리에서 설정을 수정할 수 있습니다.

  - **InternalURL** InternalURL은 내부 클라이언트는 가상 디렉터리에 액세스 하는데 사용할 수 있는 URL입니다. 일반적으로 다음은 형식 https://servername/Microsoft-Server-ActiveSync 합니다. 예, 서버의 NetBIOS 이름이 Sequoia 인 경우는 InternalURL https://sequoia/Microsoft-Server-ActiveSync 것입니다.

  - **ExternalURL** ExternalURL은 외부 클라이언트는 가상 디렉터리에 액세스 하는데 사용할 수 있는 URL입니다. 이 URL은 내부 네트워크 외부에서 액세스할 수 있어야 합니다. 예, 프로그램 ExternalURL https://www.contoso.com/ 될 수 있습니다.

  - **인증 설정** Exchange ActiveSync 가상 디렉터리에 대 한 인증을 구성할 수 있습니다는 두가지 방법 기본 인증 및 클라이언트 인증서 인증 됩니다.

