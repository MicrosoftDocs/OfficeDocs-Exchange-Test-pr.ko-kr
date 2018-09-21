---
title: '사서함 서버에서 들어오는 호출의 수를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 사서함 서버에서 들어오는 호출의 수를 구성 합니다.
ms:assetid: 419e1de9-2bf8-48a8-824d-2a536b0a6d90
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997637(v=EXCHG.150)
ms:contentKeyID: 50555974
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 서버에서 들어오는 호출의 수를 구성 합니다.

 

_**적용 대상:** Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-23_

Microsoft Exchange 통합 메시징 서비스를 실행 중인 사서함 서버에서 허용할 들어오는 동시 연결 수를 구성할 수 있습니다. 여기에는 Outlook Voice Access, 전화 응답, 자동 전화 교환 및 팩스 호출 등을 비롯한 모든 수신 전화가 포함됩니다. 사서함 서버의 동시 연결 수를 늘리는 데는 동시 전화 수를 줄일 때보다 시스템 리소스가 더 많이 필요합니다. 통합 메시징 서비스가 설치되어 있는 저속 컴퓨터에서는 동시 전화 수를 줄이는 것이 특히 중요합니다. 동시 음성 전화 수의 범위는 0~200입니다. 기본 설정은 100입니다.

통합 메시징 및 사서함 서버와 관련된 추가 작업에 대한 자세한 내용은 [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 항목의 "사서함 서버(UM 서비스)" 항목을 참조하십시오.

  - 클라이언트 액세스 및 사서함 서버를 올바르게 설치했는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 서버에 대해 들어오는 전화 수 구성

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  목록 보기에서 수정하려는 Exchange 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **Exchange Server** 페이지에서 **통합 메시징**을 클릭합니다.

4.  **UM 서비스 설정**의 **허용된 최대 전화 수**에 0~200 범위에 포함되는 숫자를 입력하고 **저장**을 클릭합니다.

## 셸을 사용하여 사서함 서버에 대해 들어오는 전화 수 구성

이 예에서는 `MyMailboxServer1`이라는 사서함 서버에서 허용할 수 있는 수신 음성 통화, Outlook Voice Access 및 팩스 호출 수를 50으로 설정합니다.

```powershell
Set-UMService -Identity MyMailboxServer1 -MaxCallsAllowed 50
```

