---
title: '스팸 방지 에이전트 로깅 구성: Exchange 2013 Help'
TOCTitle: 스팸 방지 에이전트 로깅 구성
ms:assetid: df157ca3-ad8e-4302-acbc-5fbb8570c21d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb691337(v=EXCHG.150)
ms:contentKeyID: 50484319
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 스팸 방지 에이전트 로깅 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-08_

로깅 에이전트는 특정 Exchange 스팸 방지 에이전트에 의해 수행 되는 작업을 기록 합니다. 에이전트 로그에 기록 하는 정보는 에이전트, SMTP 이벤트 및 메시지에서 수행 되는 작업에 따라 다릅니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "전송 서비스" 및 [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "Edge 전송 서버" 항목.

  - 기본적으로 스팸 방지 기능은 사서함 서버의 전송 서비스에서 사용되지 않도록 설정되어 있습니다. 일반적으로 Exchange 조직에서 들어오는 메시지를 수락하기 전에 스팸 방지 필터링을 미리 수행하지 않은 경우에만 사서함 서버에서 스팸 방지 기능을 사용하도록 설정할 수 있습니다. 자세한 내용은 [사서함 서버에서 스팸 방지 기능을 사용 하도록 설정](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)을 참조하세요.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용 하 여 스팸 방지 에이전트 로깅 구성

다음 명령을 실행합니다.

    Set-TransportService <ServerIdentity> -AgentLogEnabled <$true | $false> -AgentLogMaxAge <dd.hh:mm:ss> -AgentLogMaxDirectorySize <Size> -AgentLogMaxFileSize <Size> -AgentLogPath <LocalFilePath>

이 예에서는 mailbox01 사서함 서버의 다음 에이전트 로그 설정 설정:

  -  
    D:\\Anti-Spam 에이전트 로그에는 에이전트의 위치 로그 파일을 설정합니다. 메모는 폴더가 존재 하지 않는 경우 만들어집니다 있습니다.

  -  
    20MB로 에이전트의 최대 크기를 로그 파일을 설정합니다.

  -  
    최대 크기를 설정 하는 에이전트의 로그 디렉터리 400 MB입니다.

  -  
    14 일에는 에이전트의 최대 사용 기간 로그 파일을 설정합니다.

<!-- end list -->

    Set-TransportService Mailbox01 -AgentLogPath "D:\Anti-Spam Agent Log" -AgentLogMaxFileSize 20MB -AgentLogMaxDirectorySize 400MB -AgentLogMaxAge 14.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>값 <CODE>$null</CODE>를 <EM>AgentLogPath</EM> 매개 변수를 설정 하는 경우 효과적으로 로깅 에이전트를 비활성화 합니다. 그러나 <EM>AgentLogPath</EM><CODE>$null</CODE> 를 설정 하면 <EM>AgentLogEnabled</EM> 매개 변수 값은 <CODE>$true</CODE>때 이벤트 로그 오류 생성 됩니다. 로깅 에이전트를 사용 하지 않도록 설정 하는 기본 방법 <CODE>$false</CODE>에 <EM>AgentLogEnabled</EM> 를 설정 하는 것입니다.</P>
> <LI>
> <P>값 <CODE>00:00:00</CODE> 를 <EM>AgentLogMaxAge</EM> 매개 변수를 설정로 인해 에이전트 로그 파일이 자동으로 제거가 되지 않습니다.</P></LI></UL>



자세한 구문 및 매개 변수 정보에 대 한 [Set-TransportService](https://technet.microsoft.com/ko-kr/library/jj215682\(v=exchg.150\))의 *AgentLog* 매개 변수를 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

스팸 방지 에이전트 로깅 성공적으로 구성 했는지를 확인 하려면 다음을 수행 합니다.

1.  셸에서 다음 명령을 실행합니다.
    
        Get-TransportService <ServerIdentity> | Format-List AgentLog*

2.  표시된 값이 구성한 값인지 확인합니다.

