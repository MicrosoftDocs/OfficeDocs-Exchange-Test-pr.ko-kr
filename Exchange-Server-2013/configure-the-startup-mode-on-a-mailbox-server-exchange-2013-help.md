---
title: '사서함 서버에서 시작 모드를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 사서함 서버에서 시작 모드를 구성 합니다.
ms:assetid: 4457d6a0-52bd-4269-8cb5-d34d7fe9bfc3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423544(v=EXCHG.150)
ms:contentKeyID: 50555980
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 서버에서 시작 모드를 구성 합니다.

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-15_

사서함 서버의 Microsoft Exchange 통합 메시징 서비스에 대해 시작 모드를 지정할 수 있습니다. 기본적으로 사서함 서버는 TCP 모드로 시작되지만 TLS(전송 계층 보안)를 사용하여 VoIP(Voice over IP) 트래픽을 암호화하는 경우 TLS 또는 이중 모드를 사용하도록 사서함 서버를 구성해야 합니다. 시작 모드로 이중 모드를 사용하도록 사서함 서버를 구성하는 것이 좋습니다. 이는 모든 클라이언트 액세스 서버와 사서함 서버가 모든 UM 다이얼 플랜에 대한 수신 전화에 응답할 수 있고, 해당 다이얼 플랜은 서로 다른 보안 설정(보안되지 않음, SIP 보안 또는 보안)을 가질 수 있기 때문입니다. 시작 모드를 변경한 경우 Microsoft Exchange 통합 메시징 서비스를 다시 시작해야 변경 내용이 적용됩니다.


> [!IMPORTANT]
> 기본적으로 사서함 서버는 수신 전화에 응답하는 데 사용할 수 있습니다. UM과 Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server를 통합하는 경우가 아니면 UM 통화를 처리하기 위해 UM 다이얼 플랜에 사서함 서버를 추가할 필요가 없습니다.



통합 메시징 및 사서함 서버와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 항목의 "사서함 서버(UM 서비스)" 항목을 참조하십시오.

  - 클라이언트 액세스 서버와 동일한 컴퓨터나 별도의 컴퓨터에 사서함 서버가 설치되어 있는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 서버에서 시작 모드 구성

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  목록 보기에서 수정하려는 Exchange 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **Exchange Server** 페이지에서 **통합 메시징**을 클릭합니다.

4.  **UM 서비스 설정** \> **UM 시작 모드**의 드롭다운 목록에서 다음 중 하나를 선택합니다.
    
      - **TCP**   mTLS를 사용하지 않으며 비보안 다이얼 플랜만 사용할 경우 이 옵션을 사용합니다.
    
      - **TLS**   mTLS를 사용하고 SIP 보안 또는 보안 다이얼 플랜만 사용하려면 이 옵션을 사용합니다.
    
      - **이중**   mTLS를 사용하고 보안되지 않음, SIP 보안 및 보안 다이얼 플랜을 사용하려면 이 옵션을 사용합니다.

5.  UM 시작 모드를 선택한 후 **저장**을 클릭합니다.

## 셸을 사용하여 사서함 서버에서 시작 모드 구성

이 예에서는 `MyUMServer1`이라는 사서함 서버의 시작 모드를 이중 모드로 설정합니다.

```powershell
Set-UMService -Identity MyUMServer1 -UMStartUpMode Dual
```

이 예에서는 `MyUMServer1`이라는 사서함 서버의 시작 모드를 TLS 모드로 설정합니다.

```powershell
Set-UMService -Identity MyUMServer1 -UMStartUpMode TLS
```

