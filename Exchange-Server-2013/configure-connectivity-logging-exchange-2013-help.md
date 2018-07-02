---
title: '연결 로깅 구성: Exchange 2013 Help'
TOCTitle: 연결 로깅 구성
ms:assetid: 24e46a79-33ea-44e9-b03c-549db1c86a6f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996827(v=EXCHG.150)
ms:contentKeyID: 50482665
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 연결 로깅 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-18_

연결 로깅은 Exchange 서버의 전송 서비스에서 메시지를 전송하는 데 사용되는 아웃바운드 연결 활동을 기록합니다. 연결 로깅은 연결 소스, 대상, 전송된 바이트 수 및 메시지 수, 연결 실패 정보를 기록합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 서비스", "프런트 엔드 전송 서비스" 및 "사서함 전송 서비스" 항목

  - EAC(Exchange 관리 센터)에서는 연결 로깅을 사용하거나 사용하지 않도록 설정하거나 전송 서비스의 연결 로그 경로를 설정하는 작업만 할 수 있습니다. 다른 전송 서비스의 기타 모든 연결 로깅 옵션에 대해서는 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 전송 서비스에서 연결 로깅 구성

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  구성하려는 사서함 서버를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **전송 로그**를 클릭합니다.

4.  **연결 로그** 섹션에서 다음을 변경합니다.
    
      - **연결 로그 사용**   서버에서 연결 로깅을 사용하지 않도록 설정하려면 확인란을 선택 취소합니다. 서버에서 연결 로깅을 사용하도록 설정하려면 확인란을 선택합니다.
    
      - **연결 로그 경로**   지정하는 값은 로컬 Exchange 서버에 있어야 합니다. 해당 폴더가 없는 경우 **저장**을 클릭하면 만들어집니다.
    
    작업을 마치면 **저장**을 클릭합니다.

## 셸을 사용하여 연결 로깅 구성

연결 로깅을 구성하려면 다음 명령을 실행합니다.

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ConnectivityLogEnabled <$true | $false> -ConnectivityLogMaxAge <dd.hh:mm:ss> -ConnectivityLogMaxDirectorySize <Size> -ConnectivityLogMaxFileSize <Size> -ConnectivityLogPath <LocalFilePath>

이 예에서는 Mailbox01이라는 사서함 서버의 전송 서비스에서 다음과 같은 연결 로그 설정을 지정합니다.

  -  
    연결 로그 파일의 위치를 D:\\Hub Connectivity Log로 설정합니다. 해당 폴더가 없는 경우 새로 만들어집니다.

  -  
    연결 로그 파일의 최대 크기를 20MB로 설정합니다.

  -  
    연결 로그 디렉터리의 최대 크기를 1.5GB로 설정합니다.

  -  
    연결 로그 파일의 최대 보존 기간을 45일로 설정합니다.

<!-- end list -->

    Set-TransportService Mailbox01 -ConnectivityLogPath "D:\Hub Connectivity Log" -ConnectivityLogMaxFileSize 20MB -ConnectivityLogMaxDirectorySize 1.5GB -ConnectivityLogMaxAge 45.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>사서함 서버의 사서함 전송 서비스에서 연결 로그 설정을 구성하려면 <STRONG>Set-MailboxTransportService</STRONG> cmdlet을 사용합니다. 클라이언트 액세스 서버의 프런트 엔드 전송 서비스에서 연결 로그 설정을 구성하려면 <STRONG>Set-FrontEndTransportService</STRONG> cmdlet을 사용합니다.</P>
> <LI>
> <P><EM>ConnectivityLogPath</EM> 매개 변수를 <CODE>$null</CODE> 값으로 설정하면 연결 로깅을 사용할 수 없습니다. 하지만 <EM>ConnectivityLogEnabled</EM> 매개 변수의 값이 <CODE>$true</CODE>이면 이벤트 로그 오류가 생성됩니다.</P>
> <LI>
> <P><EM>ConnectivityLogMaxAge</EM> 매개 변수를 <CODE>00:00:00</CODE>으로 설정하면 기간 만료로 인해 연결 로그 파일이 자동으로 제거되는 것이 방지됩니다.</P></LI></UL>



## 작동 여부는 어떻게 확인합니까?

연결 로깅이 구성되었는지 확인하려면 다음을 수행합니다.

1.  셸에서 다음 명령을 실행합니다.
    
        <Get-TransportService | Get-FrontEndTransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List ConnectivityLog*

2.  표시된 값이 구성한 값인지 확인합니다.

