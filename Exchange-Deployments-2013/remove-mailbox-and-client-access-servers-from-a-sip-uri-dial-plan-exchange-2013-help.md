---
title: 'SIP URI 다이얼 플랜에서 사서함 및 클라이언트 액세스 서버를 제거 합니다.: Exchange 2013 Help'
TOCTitle: SIP URI 다이얼 플랜에서 사서함 및 클라이언트 액세스 서버를 제거 합니다.
ms:assetid: 367441e1-1a0f-42c8-9fa8-8abe80b3d015
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997238(v=EXCHG.150)
ms:contentKeyID: 54651812
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# SIP URI 다이얼 플랜에서 사서함 및 클라이언트 액세스 서버를 제거 합니다.

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-04-16_

클라이언트 액세스 서버와 사서함 서버를 SIP URI 다이얼 플랜에서 제거할 수 있습니다. Microsoft Lync Server를 배포하는 경우 아웃바운드 통화가 정상적으로 작동하도록 설정하려면 Lync Server용으로 만든 SIP URI 다이얼 플랜에 모든 클라이언트 액세스 서버와 사서함 서버를 수동으로 추가해야 합니다. 그러나 유지 관리를 수행하거나 서버를 오프라인으로 전환하는 등의 경우에는 Lync 배포에서 클라이언트 액세스 서버 또는 사서함 서버를 제거해야 할 수 있습니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 SIP URI 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 서버를 SIP URI 다이얼 플랜에서 제거

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  목록 보기에서 수정하려는 사서함 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **Exchange Server** 페이지에서 **통합 메시징**을 클릭합니다.

4.  **UM 서비스 설정** \> **연결된 다이얼 플랜**에서 제거할 SIP URI 다이얼 플랜을 찾은 다음 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거"), **저장**을 차례로 클릭합니다. 둘 이상의 SIP URI 다이얼 플랜을 제거하려면 Ctrl 키를 누른 상태로 제거할 다이얼 플랜을 선택하고 **저장**을 클릭합니다.

## 셸을 사용하여 사서함 서버를 SIP URI 다이얼 플랜에서 제거

이 예에서는 `MyMailboxServer`라는 사서함 서버를 `MySIPDialPlan`이라는 SIP URI 다이얼 플랜에서 제거합니다.

```powershell
$dp= Get-UMDialPlan "MySIPDialPlan"
$s=Get-UMService MyMailboxServer
$s.dialplans-=$dp.identity
Set-UMService -id MyMailboxServer -dialplans:$s.dialplans
```

이 예에는 SipDP1, SipDP2, SipDP3의 3개 SIP URI 다이얼 플랜이 있습니다. 이 예에서는 `MyMailboxServer`라는 사서함 서버를 SipDP3 다이얼 플랜에서 제거합니다.

```powershell
Set-UMService -id MyMailboxServer -DialPlans SipDP1,SipDP2
```

이 예에는 SipDP1 및 SipDP2의 2개 SIP URI 다이얼 플랜이 있습니다. 이 예에서는 `MyMailboxServer`라는 사서함 서버를 SipDP2 다이얼 플랜에서 제거합니다.

```powershell
Set-UMService -id MyMailboxServer -DialPlans SipDP1
```

이 예에서는 `MyMailboxServer`라는 사서함 서버를 모든 SIP 다이얼 플랜에서 제거합니다.

```powershell
Set-UMService -id MyUMServer -DialPlans $null
```

## EAC를 사용하여 클라이언트 액세스 서버를 SIP URI 다이얼 플랜에서 제거

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  목록 보기에서 수정하려는 클라이언트 액세스 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **Exchange Server** 페이지에서 **통합 메시징**을 클릭합니다.

4.  **UM 통화 라우터 설정** \> **연결된 다이얼 플랜**에서 제거할 SIP URI 다이얼 플랜을 찾은 다음 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거"), **저장**을 차례로 클릭합니다. 둘 이상의 SIP URI 다이얼 플랜을 제거하려면 Ctrl 키를 누른 상태로 제거할 다이얼 플랜을 선택하고 **저장**을 클릭합니다.

## 셸을 사용하여 클라이언트 액세스 서버를 SIP URI 다이얼 플랜에서 제거

이 예에서는 `MyClientAccessServer`라는 클라이언트 액세스 서버를 `MySIPDialPlan`이라는 SIP URI 다이얼 플랜에서 제거합니다.

```powershell
$dp= Get-UMDialPlan "MySIPDialPlan"
$s=Get-UMCallRouterSettings MyClientAccessServer
$s.dialplans-=$dp.identity
Set-UMCallRouterSettings -id MyClientAccessServer -dialplans:$s.dialplans
```

이 예에는 SipDP1, SipDP2, SipDP3의 3개 SIP URI 다이얼 플랜이 있습니다. 이 예에서는 `MyClientAccessServer`라는 클라이언트 액세스 서버를 SipDP3 다이얼 플랜에서 제거합니다.

```powershell
Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1,SipDP2
```

이 예에는 SipDP1 및 SipDP2의 2개 SIP URI 다이얼 플랜이 있습니다. 이 예에서는 `MyClientAccessServer`라는 클라이언트 액세스 서버를 SipDP2 다이얼 플랜에서 제거합니다.

```powershell
Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1
```

이 예에서는 `MyClientAccessServer`라는 클라이언트 액세스 서버를 모든 SIP 다이얼 플랜에서 제거합니다.

```powershell
Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans $null
```

