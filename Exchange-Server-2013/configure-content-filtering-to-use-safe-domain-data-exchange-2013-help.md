---
title: '콘텐츠 안전한 도메인 데이터를 사용 하 여 필터링 구성: Exchange 2013 Help'
TOCTitle: 콘텐츠 안전한 도메인 데이터를 사용 하 여 필터링 구성
ms:assetid: 1ee2b663-b4f3-4fef-8954-986f2d820924
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn467930(v=EXCHG.150)
ms:contentKeyID: 59635523
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 콘텐츠 안전한 도메인 데이터를 사용 하 여 필터링 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-12-16_

안전한 도메인 데이터를 다른 사용자의 수신 허용-보낸사람 목록에 저장 된 전체 도메인 (예, @contoso.com 같은). 기본적으로 콘텐츠 필터 에이전트를 콘텐츠 필터링을 무시 하도록 허용 되는 보낸사람을 식별 안전한 도메인 데이터를 사용 하지 않습니다.

이 기본 설정은 조직에 게 전달 되는 스팸의 양을 줄일 수 있습니다. 등 사용자가 수신 허용-보낸사람 목록에 큰 전자 메일 공급자의 도메인을 추가할 수 있습니다. 이 도메인은 자주 사용 되는 또는 스팸, 스푸핑 하는 경우 및 안전 하 게 메시지를 표시 하려면 안전한 도메인 데이터를 사용 하도록 구성 된 콘텐츠 필터링 하는 경우 조직에서 받는 사람에 게 해당 도메인의 모든 보낸에서 사람의 메시지를 배달 것입니다.

대부분의 경우에서 기본 설정은 수정 하지 하는 것이 좋습니다. 그러나 Active Directory 에 저장 하 고 콘텐츠를 안전한 것으로 메시지를 표시 하려면 필터링 하 여 사용 하려면 사용자의 수신 허용-도메인 데이터를 구성할 수 있습니다. 이 작업을 수행 하려면이 항목의 뒷부분에 나오는 설명으로 Microsoft Exchange 사서함 도우미 서비스와 관련 된 MSExchangeMailboxAssistants.exe.config XML 응용 프로그램 구성 파일을 수정 하려면 해야 합니다. 이 구성을 변경 해도 안전한 도메인 데이터 해시를 업데이트 하 고 수신 허용 목록 집계의 일부로 Active Directory 의 각 사용자의 **msExchSafeSenderHash** 사용자 개체 특성에 저장 됩니다. 콘텐츠 필터 에이전트에서 사용 하 여 수 안전한 도메인 데이터 안전한 것으로 해당 도메인에 있는 사람이 보낸 메시지를 표시 합니다. 수신 허용 목록 집계 하는 방법에 대 한 자세한 내용은 [수신 허용 목록 집계](safelist-aggregation-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분

  - 이 항목의 절차에는 Exchange 권한이 적용되지 않습니다. 이 절차는 Exchange Server의 운영 체제에서 수행됩니다.

  - Microsoft Exchange 사서함 도우미 서비스를 다시 시작 하면 MSExchangeMailboxAssistants.exe.config 파일에 저장 하면 변경 내용이 적용 됩니다.

  - Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 파일 또는 사서함 서버의 EdgeTransport.exe.config 파일)에 설정하는 사용자 지정된 모든 서버 단위 설정은 Exchange CU(누적 업데이트)를 설치하면 덮어쓰게 됩니다. 설치 후 서버를 쉽게 다시 구성할 수 있도록 이 정보를 저장했는지 확인하세요. 이러한 설정은 Exchange CU를 설치한 후에 다시 구성해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 명령 프롬프트를 사용 하 여 안전한 도메인 데이터를 사용 하 여 콘텐츠 필터링을 구성 하려면

1.  명령 프롬프트 창에서 다음 명령을 실행 하 여 MSExchangeMailboxAssistants.exe.config 파일을 메모장에서에서 엽니다.
    
        Notepad %ExchangeInstallPath%Bin\MSExchangeMailboxAssistants.exe.config

2.  파일의 끝에 *\</appsettings\>* 키를 찾아 *\</appsettings\>* 키 하기 전에 다음 키를 붙여넣습니다.
    
        <add key="IncludeSafeDomains" value="true" />

3.  작업이 끝나면 저장 하 고 MSExchangeMailboxAssistants.exe.config 파일을 닫습니다.

4.  다음 명령을 실행 하 여 Microsoft Exchange 사서함 도우미 서비스를 다시 시작 합니다.
    
        net stop MSExchangeMailboxAssistants && net start MSExchangeMailboxAssistants

## 작동 여부는 어떻게 확인합니까?

성공적으로 구성한 안전한 도메인 데이터를 사용 하 여 콘텐츠 필터링을 확인 하려면 다음을 수행 합니다.

1.  Outlook에서 사용자의 수신 허용-보낸사람 목록에 도메인 추가 (영문) Active Directory 에서 사용자의 **msExchSafeSenderHash** 특성을 업데이트를 확인 합니다. 이 작업을 수행 ADSIEdit.exe 또는 LDP.exe에서이 특성을 볼, Outlook에서 사용자의 사서함을 열, 수신 허용-보낸사람 목록에 도메인을 추가, 명령 `Update-Safelist <username>`를 실행 하 고 **msExchSafeSenderHash** 의 원래 및 현재 값의 다른 지 확인 합니다.

2.  안전한 도메인 데이터 Active Directory 에 저장 된을 확인 한 후는 조직에서 사용자에 게 해당 도메인에 외부의 보낸 사람에서 테스트 메시지를 보냅니다. 확인 메시지는 메시지 헤더의 스팸 방지 헤더 필드를 검사 하 여 안전한 것으로 표시 됩니다.

