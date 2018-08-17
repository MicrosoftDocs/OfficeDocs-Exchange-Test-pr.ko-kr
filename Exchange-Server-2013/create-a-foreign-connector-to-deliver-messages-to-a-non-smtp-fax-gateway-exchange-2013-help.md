---
title: '비 SMTP 팩스 게이트웨이에 메시지 배달에 대 한 외부 커넥터 만들기: Exchange 2013 Help'
TOCTitle: 비 SMTP 팩스 게이트웨이에 메시지 배달에 대 한 외부 커넥터 만들기
ms:assetid: 589db487-3c4c-409a-92e3-c78dd8f639b6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ710163(v=EXCHG.150)
ms:contentKeyID: 50483168
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 비 SMTP 팩스 게이트웨이에 메시지 배달에 대 한 외부 커넥터 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-17_

SMTP를 기본 전송 메커니즘으로 사용하지 않는 팩스 게이트웨이 서버로 메시지를 보내거나 해당 서버에서 메시지를 받으려는 경우가 있습니다. 이 절차의 단계를 따르면 외부 시스템으로 메시지를 배달하고 해당 외부 시스템에서 메시지를 받는 외부 커넥터를 만들 수 있습니다.


> [!TIP]
> SMTP 이외 시스템으로 아웃바운드 메시지를 전달해야 하는 대부분의 경우에는 메시지의 큐 관리에 허용되고, 메시지를 파일 시스템에 쓸 필요가 없는 등, 여러 이점이 있으므로 배달 에이전트 커넥터가 권장됩니다. <A href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">배달 에이전트 및 배달 에이전트 커넥터</A> 항목에서 보다 자세한 내용을 제공합니다.



이 절차가 사용된 시나리오에 관심이 있으면 다음 항목을 참조하십시오.

  - [계획 및 배포](planning-and-deployment-for-exchange-2013-installation-instructions.md)

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 30분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "외부 커넥터" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 셸을 사용하여 비 SMTP 게이트웨이 서버로 메시지를 보내는 외부 커넥터 만들기

1.  다음 명령을 실행하여 외부 커넥터를 만듭니다.
    
        New-ForeignConnector -Name "Contoso Foreign Connector" -AddressSpaces "X400:c=US;a=Fabrikam;P=Contoso;5" -SourceTransportServers Hub01,Hub02
    
    이 예에서 Hub01과 Hub02는 외부 시스템으로 메시지를 배달하도록 지정된 조직의 원본 서버입니다. 원본 서버를 둘 이상 사용하면 내결함성이 제공됩니다.

외부 커넥터를 만든 후 조직의 요구 사항에 따라 Drop, Pickup 및 Replay 디렉터리를 구성할 수 있습니다.

## 이 단계의 작동 여부는 어떻게 확인합니까?

외부 커넥터가 만들어졌는지 확인하려면 다음 명령을 실행합니다.

    Get-ForeignConnector | Format-List Name

만든 외부 커넥터의 이름이 나타나는지 확인합니다.

## 2단계: 셸을 사용하여 전송 서비스를 실행하는 사서함 서버의 Drop 디렉터리 구성

전송 서비스를 실행하는 사서함 서버의 Drop 디렉터리는 외부 커넥터에서 보낸 아웃바운드 메시지를 배달하는 데 사용됩니다.

Drop 디렉터리로 사용할 디렉터리를 로컬 파일 시스템에 만듭니다. 네트워크 파일 공유의 디렉터리를 사용할 수도 있습니다.

1.  다음 스크립트를 실행하여 외부 커넥터의 Drop 디렉터리를 지정합니다(*DropDirectory* 매개 변수 값을 환경에서 사용하는 해당 경로로 변경).
    
        Set-ForeignConnector "Contoso Foreign Connector" -DropDirectory "C:\Drop Directory"

## 이 단계의 작동 여부는 어떻게 확인합니까?

Drop 디렉터리가 설정되었는지 확인하려면 다음 cmdlet 스크립트를 실행하여 *DropDirectory* 매개 변수의 값을 확인합니다.

    Get-ForeignConnector "Contoso Foreign Connector" | Format-List

외부 커넥터를 만들고 Drop 디렉터리를 지정했으면 만든 외부 커넥터가 있는 사서함 서버에서 메시지를 보내 파일이 Drop 디렉터리로 배달되는지 확인할 수 있습니다.

## 3단계: 셸을 사용하여 사서함 서버에 있는 전송 서비스의 Pickup 디렉터리 구성

사서함 서버에 있는 전송 서비스의 Pickup 디렉터리는 비 SMTP 시스템에서 생성한 메시지를 수집하는 데 사용됩니다. 팩스 게이트웨이 서버와 같은 비 SMTP 시스템에서 생성한 새 메시지를 파일 전송을 통해 수집하려는 경우 이 절차를 따르십시오.

Pickup 디렉터리를 구성하기 위한 자세한 지침은 [Pickup 디렉터리 및 Replay 디렉터리 구성](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md) 항목을 참조하십시오.

## 이 단계의 작동 여부는 어떻게 확인합니까?

Pickup 디렉터리가 설정되었는지 확인하려면 다음 명령을 실행하여 *PickupDirectoryPath* 매개 변수의 값을 확인합니다.

    Get-TransportService | Format-List PickupDirectoryPath

## 4단계: 셸을 사용하여 사서함 서버에 있는 전송 서비스의 Replay 디렉터리 구성

사서함 서버에 있는 전송 서비스의 Replay 디렉터리는 비 SMTP 시스템에서 생성한 메시지를 수집하는 데 사용됩니다. Exchange 환경에서 생성되고 Exchange 전송에서 내보낸 전자 메일 메시지를 비 SMTP 외부 게이트웨이 서버에서 다시 전송하려는 경우 이 절차에 따라 Replay 디렉터리를 구성하십시오.

Pickup 디렉터리를 구성하기 위한 자세한 지침은 [Pickup 디렉터리 및 Replay 디렉터리 구성](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md) 항목을 참조하십시오.

## 이 단계의 작동 여부는 어떻게 확인합니까?

Replay 디렉터리가 설정되었는지 확인하려면 다음 명령을 실행하여 *ReplayDirectoryPath* 매개 변수의 값을 확인합니다.

    Get-TransportService | Format-List ReplayDirectoryPath

## 자세한 내용

[외부 커넥터](foreign-connectors-exchange-2013-help.md)

[배달 에이전트 및 배달 에이전트 커넥터](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

