---
title: '신뢰할 수 있는 페이지로 Exchange 조직 내에서 허용된 도메인 구성: Exchange 2013 Help'
TOCTitle: 신뢰할 수 있는 페이지로 Exchange 조직 내에서 허용된 도메인 구성
ms:assetid: e182d54f-e58a-47ba-a5c1-28c0dfa86eed
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657734(v=EXCHG.150)
ms:contentKeyID: 50484332
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 신뢰할 수 있는 페이지로 Exchange 조직 내에서 허용된 도메인 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-02-17_

조직에 속하는 도메인이 SMTP 네임스페이스에 있는 모든 받는 사람의 사서함을 호스트하는 경우 해당 도메인은 신뢰할 수 있는 도메인으로 간주됩니다. 기본적으로 Exchange 조직에 대해 하나의 허용 도메인만 신뢰할 수 있는 도메인으로 구성됩니다. 조직에 둘 이상의 SMTP 네임스페이스가 있는 경우 둘 이상의 허용 도메인을 신뢰할 수 있는 도메인으로 구성할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "허용 도메인" 항목

  - 경계 네트워크에 구독된 Edge 전송 서버가 있는 경우 Exchange 조직의 사서함 서버에 허용 도메인을 구성합니다. 허용 도메인 구성은 EdgeSync 동기화 중에 Edge 전송 서버로 복제됩니다. 자세한 내용은 [Edge 구독](edge-subscriptions-exchange-2013-help.md)을 참조하세요.

  - 이미 구성된 원격 도메인과 이름이 동일한 허용 도메인은 만들 수 없습니다. 예를 들어 원격 도메인으로 구성된 fabrikam.com이 있는 경우 fabrikam.com에 대한 허용 도메인을 만들 수 없습니다.

  - 허용 도메인을 구성하기 전에 SMTP 네임스페이스에 대한 공용 DNS(Domain Name System) MX 리소스 레코드가 있고 그 MX 리소스 레코드가 Exchange 조직에 연결된 서버 이름과 IP 주소를 참조하는지 확인해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 허용 도메인을 신뢰할 수 있는 도메인으로 구성

Exchange 조직의 허용 도메인이 해당 도메인의 SMTP 네임스페이스에 있는 받는 사람의 모든 사서함을 호스트하는 경우 신뢰할 수 있는 도메인으로 구성하려고 할 수 있습니다.

1.  EAC에서 **메일 흐름** \> **허용 도메인**으로 이동한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **이름** 필드에 허용 도메인의 표시 이름을 입력합니다. 조직의 각 허용 도메인은 고유한 표시 이름이 있어야 합니다. 이 이름은 허용 도메인과는 다를 수 있습니다. 예를 들어 contoso.com 도메인의 표시 이름은 Contoso Local Accepted Domain일 수 있습니다.

3.  **허용 도메인** 필드에 허용된 도메인을 입력합니다. 조직이 전자 메일 메시지를 수락하는 SMTP 네임스페이스를 지정합니다. (예: Contoso.com).

4.  **신뢰할 수 있는 도메인**을 선택합니다. 이 옵션은 SMTP 네임스페이스에 있는 모든 받는 사람의 사서함을 호스트하는 허용 도메인에 대해 Exchange 조직 내의 서버로 전달되는 전자 메일과 관련된 것입니다.

5.  **저장**을 클릭합니다.


> [!TIP]
> 미리 만든 허용 도메인을 구성하려면 허용 도메인 목록에서 도메인을 선택하고 <STRONG>편집</STRONG><IMG title="편집 아이콘" alt="편집 아이콘" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">을 클릭합니다. 둘 이상의 도메인을 신뢰할 수 있는 도메인으로 구성할 수 있습니다.



## 작동 여부는 어떻게 확인합니까?

새 허용 도메인은 EAC의 허용 도메인 목록에 표시됩니다. 허용 도메인을 신뢰할 수 있는 도메인으로 성공적으로 구성했는지 확인하려면 해당 도메인으로 메일을 보낸 후 수신되었는지 확인하십시오.

