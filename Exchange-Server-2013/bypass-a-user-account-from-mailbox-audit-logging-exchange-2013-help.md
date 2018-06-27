---
title: '프로그램에서 사용자 계정을 사서함 감사 로깅 바이패스: Exchange 2013 Help'
TOCTitle: 프로그램에서 사용자 계정을 사서함 감사 로깅 바이패스
ms:assetid: 98a87071-fe31-4b67-beb8-a73799e54df2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff461934(v=EXCHG.150)
ms:contentKeyID: 50483728
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 프로그램에서 사용자 계정을 사서함 감사 로깅 바이패스

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2013-05-21_

사서함에 대해 사서함 감사 로깅을 사용하도록 설정하면 지정한 사서함 액세스 이벤트(예: 폴더나 메시지에 액세스 또는 메시지 영구 삭제)가 기록됩니다. 하지만 타사 도구에 사용되는 계정이나 합법적인 모니터링에 사용되는 계정 등의 일부 인증된 계정으로 액세스한 결과 사서함 감사 로그 항목이 너무 많이 생성되어 조직에 좋지 않은 영향을 줄 수 있습니다.

사서함 감사 로깅을 바이패스하도록 사용자 또는 컴퓨터 계정을 구성하면 해당 사용자 또는 계정이 사서함에 대해 수행한 작업이 전혀 기록되지 않습니다. 사서함에 자주 액세스해야 하는 신뢰할 수 있는 사용자 또는 컴퓨터 계정을 바이패스하도록 하면 사서함 감사 로그를 깔끔하게 정리할 수 있습니다.


> [!WARNING]
> 사서함 감사 로깅을 사용하여 사서함 액세스 및 작업을 감사하는 경우 주기적으로 사서함 감사 바이패스 연결을 모니터링해야 합니다. 사서함 감사 바이패스 연결이 계정에 추가될 경우 해당 계정은 액세스나 메시지 삭제 등의 수행 작업에 대해 사서함 감사 로깅 항목을 전혀 생성하지 않고 조직에서 사용 권한이 할당된 모든 사서함에 액세스할 수 있습니다.



사서함 감사 로깅과 관련된 추가 관리 작업에 대한 자세한 내용은 [사서함 감사 로깅 절차](mailbox-audit-logging-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "사서함 감사 로깅" 항목

  - 사서함 감사 로깅을 바이패스하도록 계정을 구성하면 해당 계정의 사서함 액세스는 전혀 기록되지 않습니다. 특정 사서함에 대한 액세스 로깅을 바이패스하도록 계정을 구성할 수는 없습니다.

  - EAC를 사용하여 계정에 대해 사서함 감사 로깅 우회를 사용하거나 사용하지 않도록 설정할 수는 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 계정에 대해 사서함 감사 로깅 우회를 사용 또는 사용하지 않도록 설정

계정에 대해 사서함 감사 로깅 우회를 사용하도록 설정하는 방법에 대한 예는 [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/ko-kr/library/ff696758\(v=exchg.150\))에서 [Examples](https://technet.microsoft.com/ko-kr/ff696758\(exchg.150\)#examples) 항목을 참조하십시오.

계정에 대해 사서함 감사 로깅 우회를 사용하지 않도록 설정하는 방법에 대한 예는 [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/ko-kr/library/ff696758\(v=exchg.150\))에서 [Examples](https://technet.microsoft.com/ko-kr/ff696758\(exchg.150\)#examples)를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사서함 감사 로깅에서 사용자 계정을 우회한 후 [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/ko-kr/library/ff696741\(v=exchg.150\)) cmdlet을 실행하여 우회 설정을 확인할 수 있습니다.

사서함 감사 우회 연결을 확인하는 방법에 대한 예는 [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/ko-kr/library/ff696741\(v=exchg.150\))에서 [Examples](https://technet.microsoft.com/ko-kr/ff696741\(exchg.150\)#examples)를 참조하십시오.

