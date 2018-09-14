---
title: 'Lync Server와 함께 작동 하는 UM 구성: Exchange 2013 Help'
TOCTitle: Lync Server와 함께 작동 하는 UM 구성
ms:assetid: 29bdddbf-75d5-4c92-988e-c8506ecc7a1c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ966276(v=EXCHG.150)
ms:contentKeyID: 52058063
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lync Server와 함께 작동 하는 UM 구성

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-06-11_

Microsoft Lync Server와 Exchange UM(통합 메시징)을 통합하는 경우 셸에서 ExchUcUtil.ps1 스크립트를 실행해야 합니다. ExchUcUtil.ps1 스크립트는 다음을 수행합니다.

  - 각 Lync Server 풀에 대해 UM IP 게이트웨이를 만듭니다.
    

    > [!IMPORTANT]
    > ExchUcUtil.ps1 스크립트는 UM IP 게이트웨이를 하나 이상 만듭니다. 스크립트가 만들어진 한 게이트웨이를 제외한 모든 UM IP 게이트웨이에서 발신 전화를 사용하지 않도록 설정해야 합니다. 또한 스크립트를 실행하기 전에 만들어진 UM IP 게이트웨이에서도 발신 전화를 사용하지 않도록 설정합니다. UM IP 게이트웨이에서 발신 전화를 사용하지 않도록 설정하려면 <A href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/disable-outgoing-calls-on-um-ip-gateways">UM IP 게이트웨이에서 거는 전화를 사용 하지 않도록 설정</A>을 참조하세요.



  - 각 UM IP 게이트웨이에 대해 UM 헌트 그룹을 만듭니다. 각 헌트 그룹의 파일럿 식별자는 Lync Server 프런트 엔드 풀 또는 UM IP 게이트웨이와 연결된 Standard Edition 서버에서 사용되는 UM SIP URI 다이얼 플랜을 지정합니다.

  - UM 다이얼 플랜, 자동 전화 교환, UM IP 게이트웨이, UM 헌트 그룹 등의 Active Directory UM 컨테이너 개체를 읽을 수 있도록 Lync Server에 사용 권한을 부여합니다.


> [!IMPORTANT]
> 각 UM 포리스트는 Lync Server 2013이 배포된 포리스트를 신뢰할 수 있도록 구성해야 하고, Lync Server 2013이 배포된 포리스트는 각 UM 포리스트를 신뢰할 수 있도록 구성해야 합니다. Exchange UM이 여러 포리스트에 설치된 경우 각 UM 포리스트에서 Exchange Server 통합 단계를 수행해야 하며, 그렇지 않을 경우 Lync Server 도메인을 지정해야 합니다. 예를 들면 <EM>ExchUcUtil.ps1 –Forest:&lt;lync-domain-controller-fqdn&gt;</EM> 등이 있습니다.



Lync Server와 통합 메시징를 통합하는 일과 관련된 추가 관리 작업은 [Exchange 2013 UM 및 Lync Server 배포 개요](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)을 참조하세요.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\)) 항목의 "권한 Cmdlet\&quot; 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 ExchUcUtil.ps1 스크립트 실행

Microsoft Lync Server와 같은 토폴로지에 있는 조직의 Exchange Server에서 ExchUcUtil.ps1 스크립트를 실행합니다. 셸을 사용하여 사서함 서버에서 스크립트를 실행하거나, 클라이언트 액세스 서버에서 원격 Windows PowerShell을 사용하여 스크립트를 실행할 수 있습니다. 조직의 클라이언트 액세스 서버에서 스크립트를 실행하면 클라이언트 액세스 서버가 원격 Windows PowerShell 세션을 조직에 있는 사서함 서버로 프록시합니다.


> [!IMPORTANT]
> ExchUcUtil.ps1 스크립트는 UM IP 게이트웨이를 하나 이상 만듭니다. 스크립트가 만들어진 한 게이트웨이를 제외한 모든 UM IP 게이트웨이에서 발신 전화를 사용하지 않도록 설정해야 합니다. 또한 스크립트를 실행하기 전에 만들어진 UM IP 게이트웨이에서도 발신 전화를 사용하지 않도록 설정합니다. UM IP 게이트웨이에서 발신 전화를 사용하지 않도록 설정하려면 <A href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/disable-outgoing-calls-on-um-ip-gateways">UM IP 게이트웨이에서 거는 전화를 사용 하지 않도록 설정</A>을 참조하세요.




> [!IMPORTANT]
> 사용자는 Exchange 조직 관리 역할의 사용 권한이 있거나, 스크립트를 실행할 수 있는 Exchange 조직 관리 보안 그룹의 구성원이어야 합니다.



1.  Exchange 관리 셸을 엽니다.

2.  `C:\Windows\System32` 프롬프트에서 <strong>cd \&quot;\<드라이브 문자\>\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts\>.ExchUcUtil.ps1\&quot;</strong>을 입력한 다음 Enter 키를 누릅니다.

## 작동 여부를 확인하는 방법

ExchUcUtul.ps1 스크립트가 완료되었는지 확인하려면 다음을 수행합니다.

  - **Get-UMIPGateway** cmdlet 또는 EAC를 사용하여 새로운 UM IP 게이트웨이 또는 만들어진 게이트웨이를 확인합니다.

  - **Get-UMHuntGroup** cmdlet 또는 EAC를 사용하여 새로운 UM 헌트 그룹 또는 만들어진 그룹을 확인합니다.

