---
title: '라우팅 테이블 로깅 구성: Exchange 2013 Help'
TOCTitle: 라우팅 테이블 로깅 구성
ms:assetid: 7184f8f7-4eb8-468a-aafe-b2d72868f820
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201696(v=EXCHG.150)
ms:contentKeyID: 50483414
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 라우팅 테이블 로깅 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

라우팅 테이블 기록은 Microsoft Exchange Server 2013에서 메시지를 해당 대상으로 라우팅하는 데 사용하는 라우팅 테이블의 스냅숏을 정기적으로 기록합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 서비스" 및 "Edge 전송 서버" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 라우팅 테이블의 자동 새로 고치기 시간 간격을 구성하려면 EdgeTransport.exe.config XML 응용 프로그램 구성 파일을 수정합니다. 이 파일에 저장하는 변경 내용은 Microsoft Exchange Transport Service를 다시 시작하고 나면 적용됩니다. 이 서비스를 다시 시작하면 서버의 메일 흐름이 일시적으로 중지됩니다.

  - Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 파일 또는 사서함 서버의 EdgeTransport.exe.config 파일)에 설정하는 사용자 지정된 모든 서버 단위 설정은 Exchange CU(누적 업데이트)를 설치하면 덮어쓰게 됩니다. 설치 후 서버를 쉽게 다시 구성할 수 있도록 이 정보를 저장했는지 확인하세요. 이러한 설정은 Exchange CU를 설치한 후에 다시 구성해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 라우팅 테이블 기록 구성

다음 명령을 실행합니다.

    Set-TransportService <ServerIdentity> -RoutingTableLogMaxAge <dd.hh:mm:ss> -RoutingTableLogMaxDirectorySize <Size>  -RoutingTableLogPath <LocalFilePath>

이 예에서는 Mailbox01이라는 사서함 서버의 다음과 같은 라우팅 테이블 로그 설정을 지정합니다.

  - 라우팅 테이블 로그 파일의 위치를 D:\\Routing Table Log로 설정합니다. 해당 폴더가 없는 경우 새로 만들어집니다.

  - 라우팅 테이블 로그 폴더의 최대 크기를 70MB로 설정합니다.

  - 라우팅 테이블 로그 파일의 최대 보존 기간을 45일로 설정합니다.

<!-- end list -->

    Set-TransportService Mailbox01 -RoutingTableLogPath "D:\Routing Table Log" -RoutingTableLogMaxDirectorySize 70MB -RoutingTableLogMaxAge 45.00:00:00


> [!NOTE]
> <EM>RoutingTableLogMaxAge</EM> 매개 변수를 <CODE>00:00:00</CODE> 값으로 설정하면 기간 만료로 인해 라우팅 테이블 로그 파일이 자동으로 제거되는 것을 방지할 수 있습니다.



## 작동 여부는 어떻게 확인합니까?

라우팅 테이블 기록이 구성되었는지 확인하려면 다음을 수행합니다.

1.  셸에서 다음 명령을 실행합니다.
    
        Get-TransportService <ServerIdentity> | Format-List RoutingTableLog*

2.  표시된 값이 구성한 값인지 확인합니다.

## 명령 프롬프트를 사용하여 EdgeTransport.exe.config 파일에서 라우팅 테이블의 자동 새로 고치기 간격 구성

1.  명령 프롬프트 창에서 다음 명령을 실행하여 EdgeTransport.exe.config 응용 프로그램 구성 파일을 메모장에서 엽니다.
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  `<appSettings>` 섹션의 다음 키를 수정합니다.
    
        <add key="RoutingConfigReloadInterval" value="<hh:mm:ss>" />
    
    예를 들어 라우팅 테이블의 자동 새로 고치기 간격을 10시간으로 변경하려면 다음 값을 사용합니다.
    
        <add key="RoutingConfigReloadInterval" value="10:00:00" />

3.  작업을 마친 후 저장하고 EdgeTransport.exe.config 파일을 닫습니다.

4.  다음 명령을 실행하여 Microsoft Exchange Transport Service를 다시 시작합니다.
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 작동 여부는 어떻게 확인합니까?

라우팅 테이블의 자동 새로 고치기 간격이 구성되었는지 확인하려면 지정한 시간 간격 동안 라우팅 테이블 로그가 업데이트되었는지 확인합니다.

다음과 같은 상황이 발생하면 *RoutingConfigReloadInterval* 키로 지정한 값보다 이전에 라우팅 테이블의 새로 고치기와 기록이 수행됩니다.

  - 라우팅 구성 변경이 검색되는 경우. 예를 들어 송신 커넥터 또는 수신 커넥터가 추가, 제거 또는 수정되거나 6시간 간격으로 Kerberos 토큰 갱신이 발생하는 경우

  - Microsoft Exchange Transport Service가 시작되는 경우

