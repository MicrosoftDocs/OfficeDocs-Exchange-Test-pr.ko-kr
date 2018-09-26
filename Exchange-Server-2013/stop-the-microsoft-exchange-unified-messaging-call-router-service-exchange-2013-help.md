---
title: 'Microsoft Exchange 통합 메시징 호출 라우터 서비스를 중지 합니다.: Exchange 2013 Help'
TOCTitle: Microsoft Exchange 통합 메시징 호출 라우터 서비스를 중지 합니다.
ms:assetid: 79935528-1a8c-4f22-826c-8f9a60f4f6f4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673535(v=EXCHG.150)
ms:contentKeyID: 50556015
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Microsoft Exchange 통합 메시징 호출 라우터 서비스를 중지 합니다.

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-16_

Microsoft MMC(Microsoft Management Console)에서 서비스 스냅인을 사용하거나 명령 프롬프트에서 cmd.exe를 사용하여 클라이언트 액세스 서버의 MicrosoftExchange 통합 메시징 통화 라우터 서비스를 중지할 수 있습니다. 예를 들어 클라이언트 액세스 서버를 오프라인으로 만들어야 하는 경우와 같이 이 서비스를 중지해야 할 때가 있을 수 있습니다. MicrosoftExchange 통합 메시징 통화 라우터 서비스를 중지하면 클라이언트 액세스 서버에서 수신 전화를 수락하거나 처리할 수 없습니다.

클라이언트 액세스 서버와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 다음 절차를 수행하려면 로컬 관리자 그룹의 구성원인 계정을 사용하여 클라이언트 액세스 서버에 로그온해야 합니다.

  - 사서함 서버와 동일한 컴퓨터나 별도의 컴퓨터에 클라이언트 액세스 서버가 설치되어 있는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## MMC 서비스 스냅인을 사용하여 Microsoft Exchange 통합 메시징 통화 라우터 서비스 중지

1.  **시작**, **제어판**을 차례로 클릭합니다.

2.  제어판에서 **관리 도구**를 두 번 클릭합니다.

3.  **관리 도구**에서 **서비스**를 두 번 클릭합니다.

4.  **서비스** 세부 정보 창에서 **Microsoft Exchange 통합 메시징 통화 라우터**를 마우스 오른쪽 단추로 클릭하고 **중지**를 클릭합니다.

## 명령 프롬프트를 사용하여 Microsoft Exchange 통합 메시징 통화 라우터 서비스 중지

1.  **시작**, **실행**을 차례로 클릭합니다.

2.  **열기** 상자에 다음 명령을 입력하고 Enter 키를 누릅니다.
    
    ```powershell
    net stop MSExchangeUMCR
    ```

