---
title: 'Exchange 조직 외부에 사서함이 있는 사업부에 대 한 허용된 도메인 구성: Exchange 2013 Help'
TOCTitle: Exchange 조직 외부에 사서함이 있는 사업부에 대 한 허용된 도메인 구성
ms:assetid: ff46310b-5392-4eac-97bc-d39d397e1ce1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657737(v=EXCHG.150)
ms:contentKeyID: 50484613
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 조직 외부에 사서함이 있는 사업부에 대 한 허용된 도메인 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-08-06_

일부 경우에 도메인의 일부 또는 모든 받는 사람이 Exchange 조직에 사서함을 보유하고 있지 않은 사업부에 대한 허용 도메인을 구성하려고 할 수 있습니다. 예를 들어 조직이 둘 이상의 다른 전자 메일 시스템 사이에서 동일한 SMTP 주소 공간을 공유하는 경우에 이러한 상황이 발생할 수 있습니다. 이러한 경우 허용 도메인을 내부 릴레이 도메인으로 구성할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "허용 도메인" 항목

  - 경계 네트워크에 구독된 Edge 전송 서버가 있는 경우 Exchange 조직의 사서함 서버에 허용 도메인을 구성합니다. 허용 도메인 구성은 EdgeSync 동기화 중에 Edge 전송 서버로 복제됩니다. 자세한 내용은 [Edge 구독](edge-subscriptions-exchange-2013-help.md)을 참조하세요.

  - 허용 도메인을 구성하기 전에 SMTP 네임스페이스에 대한 공용 DNS(Domain Name System) MX 리소스 레코드가 있고 그 MX 리소스 레코드가 Exchange 조직에 연결된 서버 이름과 IP 주소를 참조하는지 확인해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 허용 도메인을 내부 릴레이 도메인으로 구성

1.  EAC에서 **메일 흐름** \> **허용 도메인**으로 이동한 후 구성하려는 도메인을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **이름** 필드에 허용 도메인의 표시 이름을 입력합니다. 조직에 대한 각 허용 도메인에는 고유한 표시 이름이 있어야 합니다. 이는 허용 도메인과 다를 수 있습니다. 예를 들어 Contoso.com 도메인에 Contoso Local Accepted Domain이라는 표시 이름이 있을 수 있습니다.

3.  **내부 릴레이 도메인**을 선택합니다.

4.  **저장**을 클릭합니다.

## 작동 여부는 어떻게 확인합니까?

허용 도메인을 내부 릴레이 도메인으로 성공적으로 구성했는지 확인하려면 내부 릴레이 도메인에서 Exchange 조직 내의 사서함으로 메시지를 전송한 다음 제대로 수신되는지 확인합니다.

