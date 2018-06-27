---
title: '큐에서 메시지 내보내기: Exchange 2013 Help'
TOCTitle: 큐에서 메시지 내보내기
ms:assetid: 688b342c-f380-4fe0-afce-7e38cf490627
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998625(v=EXCHG.150)
ms:contentKeyID: 51407709
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 큐에서 메시지 내보내기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-05-05_

메시지를 큐에서 파일로 내보내도 메시지는 큐에서 제거되지 않습니다. 메시지는 지정된 위치에서 일반 텍스트 파일로 복사됩니다. 결과 파일은 텍스트 편집기 또는 전자 메일 클라이언트 응용 프로그램 등과 같은 응용 프로그램에서 표시할 수 있으며 또는 Exchange 조직 내부 또는 외부에 있는 다른 모든 사서함 서버나 Edge 전송 서버의 Replay 디렉터리를 사용하여 메시지 파일을 다시 전송할 수도 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "큐" 항목

  - 내보내기를 완료하려면 메시지가 Suspended 상태여야 합니다. 배달 큐, 연결할 수 없는 큐 또는 유해한 메시지 큐에서 메시지를 내보낼 수 있습니다. 포이즌 메시지 큐의 메시지는 이미 Suspended 상태에 있습니다. 전송 큐에 있는 메시지는 일시 중단하거나 내보낼 수 없습니다.

  - Exchange 도구 상자의 큐 뷰어를 사용하여 메시지를 내보낼 수는 없습니다. 그러나 셸을 사용하여 메시지를 내보내기 전에 큐 뷰어를 사용하여 메시지를 찾고 식별하고 일시 중단할 수는 있습니다.

  - 메시지 파일의 대상 디렉터리 위치에 대한 다음 정보를 확인합니다.
    
      - 메시지를 내보내려면 대상 디렉터리가 있어야 합니다. 디렉터리는 자동으로 만들어지지 않습니다. 절대 경로를 지정하지 않으면 현재 Exchange 관리 셸 작업 디렉터리가 사용됩니다.
    
      - 경로는 Exchange 서버의 로컬 경로 또는 원격 서버에서 공유할 수 있는 UNC(범용 명명 규칙) 경로일 수 있습니다.
    
      - 사용하는 계정에 대상 디렉터리에 대한 **쓰기** 권한이 있어야 합니다.
    
      - 내보낸 메시지의 파일 이름을 지정할 때는 파일이 전자 메일 클라이언트 응용 프로그램에 의해 쉽게 열리고 Replay 디렉터리에 의해 제대로 처리되도록 파일 이름에 확장명 .eml이 포함되도록 해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 특정 큐에서 특정 메시지 내보내기

특정 큐에서 특정 메시지를 내보내려면 다음 명령을 실행합니다.

    Export-Message -Identity <MessageIdentity> | AssembleMessage -Path <FilePath>\<FileName>.eml

이 예에서는 서버 Mailbox01의 도메인 contoso.com 배달 큐에 있는 1234라는 **InternalMessageID**를 갖고 있는 메시지의 복사본을 D:\\Contoso Export 경로의 export.eml 파일로 내보냅니다.

    Export-Message -Identity Exchange01\Contoso.com\1234 | AssembleMessage -Path "D:\Contoso Export\export.eml"

## 셸을 사용하여 특정 큐에서 모든 메시지 내보내기

특정 큐에서 모든 메시지를 내보내고 각 메시지의 **InternetMessageID** 값을 파일 이름으로 사용하려면 다음 구문을 사용합니다.

    Get-Message -Queue <QueueIdentity> | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

**InternetMessageID** 값에는 꺾쇠 괄호(\> 및 \<)가 포함되어 있으며 꺾쇠 괄호는 파일 이름에서 허용되지 않으므로 제거해야 합니다.

이 예에서는 Mailbox01 서버의 contoso.com 배달 큐에 있는 모든 메시지의 복사본을 D:\\Contoso Export라는 로컬 디렉터리로 내보냅니다.

    Get-Message -Queue Mailbox01\Contoso.com | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

## 셸을 사용하여 서버의 모든 큐에서 특정 메시지 내보내기

서버의 모든 큐에서 특정 메시지를 내보내고 각 메시지의 **InternetMessageID** 값을 파일 이름으로 사용하려면 다음 구문을 사용합니다.

    Get-Message -Filter {<MessageFilter>} [-Server <ServerIdentity>] | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

**InternetMessageID** 값에는 꺾쇠 괄호(\> 및 \<)가 포함되어 있으며 꺾쇠 괄호는 파일 이름에서 허용되지 않으므로 제거해야 합니다.

이 예에서는 Mailbox01 서버의 모든 큐에서 contoso.com 도메인의 보낸 사람이 보낸 모든 메시지 복사본을 D:\\Contoso Export라는 로컬 디렉터리로 내보냅니다.

    Get-Message -Filter {FromAddress -like "*@contoso.com"} -Server Mailbox01 | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}


> [!NOTE]
> <EM>Server</EM> 매개 변수를 생략할 경우 이 명령은 로컬 서버에서 작동합니다.


