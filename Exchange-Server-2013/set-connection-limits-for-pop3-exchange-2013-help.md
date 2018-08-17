﻿---
title: 'P o p 3에 대 한 연결 제한 설정: Exchange 2013 Help'
TOCTitle: P o p 3에 대 한 연결 제한 설정
ms:assetid: 512d61c2-2a34-4813-92a9-875339d3388b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997988(v=EXCHG.150)
ms:contentKeyID: 50555992
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# P o p 3에 대 한 연결 제한 설정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-28_

조직에 대 한 POP3 연결 제한을 관리 하는 EAC 또는 셸을 사용할 수 있습니다.

P o p 3에 대 한 연결 제한을 지정 하는 경우에 서버, IP 주소, 또는 특정 사용자에 대 한 연결 제한을 선택할 수 있습니다.

POP3에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "POP3 설정" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EMC를 사용 하 여 서버, IP 주소 또는 사용자에 대 한 POP3 연결 제한 설정

1.  EAC에서 **서버\>서버**로 이동합니다.

2.  서버 목록에서 클라이언트 액세스 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **POP3**를 클릭합니다.

4.  아래로 스크롤한 후 **기타 옵션**을 클릭합니다.

5.  **연결 제한**에서 다음 설정을 사용합니다.
    
      - **최대 연결 수**   지정한 서버에서 허용할 총 연결 수를 지정합니다. 여기에는 인증된 연결과 인증되지 않은 연결이 모두 포함됩니다. 기본값은 2,147,483,647이고, 1에서 2,147,483,647까지의 값을 사용할 수 있습니다.
    
      - **단일 IP 주소의 최대 연결 수**   서버가 단일 IP 주소에서 허용할 연결 수를 지정합니다. 기본값은 2,147,483,647이고, 1에서 2,147,483,647까지의 값을 사용할 수 있습니다.
    
      - **단일 사용자의 최대 연결 수**   서버가 특정 사용자에 대해 허용할 최대 연결 수를 지정합니다. 기본값은 16이고, 1에서 2,147,483,647까지의 값을 사용할 수 있습니다.
    
      - 단일 명령의 최대 크기를 지정 하는 **최대 명령 크기 (바이트)**. 다음은 기본 크기는 512 합니다. 1, 024 통해 40에서 사용 가능한 값은 합니다.

6.  **적용**을 클릭한 다음 **확인**을 클릭하여 변경 내용을 저장합니다.

연결 제한을 설정한 후에 POP3 서비스를 다시 시작 해야 합니다. POP3 서비스를 다시 시작 하는 방법에 대 한 정보를 [시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md)을 참조 하십시오.

## 셸을 사용 하 여 서버, IP 주소 또는 사용자에 대 한 POP3 연결 제한 설정

이 예에서는 서버에 대한 연결 제한을 설정합니다.

    Set-PopSettings -Identity CAS01 -MaxConnections Value

이 예에서는 IP 주소에 대한 연결 제한을 설정합니다.

    Set-PopSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value

이 예에서는 사용자에 대한 연결 제한을 설정합니다.

    Set-PopSettings -MaxConnectionsPerUser Value 

이 예에서는 최대 명령 크기를 설정합니다.

    Set-PopSettings -MaxCommandSize Value

연결 제한을 설정한 후에 POP3 서비스를 다시 시작 해야 합니다. POP3 서비스를 다시 시작 하는 방법에 대 한 정보를 [시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md)을 참조 하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-PopSettings](https://technet.microsoft.com/ko-kr/library/aa997154\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

연결 제한이 설정되었는지 확인하려면 다음 중 하나를 수행합니다.

1.  EAC에서 **서버\>서버**로 이동합니다.

2.  서버 목록에서 클라이언트 액세스 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **POP3**를 클릭합니다.

4.  아래로 스크롤한 후 **기타 옵션**을 클릭합니다.

5.  **연결 제한**에서 연결 설정이 올바른지 확인합니다.

또는

1.  셸에서 다음 명령을 실행합니다.
    
        Get-PopSettings | format-list

2.  연결 설정이 올바른지 확인합니다.

## 자세한 내용

서버, IP 주소 또는 사용자에 대 한 POP3 연결 제한을 설정 하 고 나면을 할 수 있습니다.

[Exchange 2013에서 POP3 사용](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[P o p 3에 대 한 연결 시간 제한 설정](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

