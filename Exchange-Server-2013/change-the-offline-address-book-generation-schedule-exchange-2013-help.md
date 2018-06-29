---
title: '오프 라인 주소록 생성 일정이 변경: Exchange 2013 Help'
TOCTitle: 오프 라인 주소록 생성 일정이 변경
ms:assetid: d2b4d527-311e-442d-9f1f-54fac8371b80
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124719(v=EXCHG.150)
ms:contentKeyID: 50484219
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.OfflineAddressBookGeneralPage
ms.translationtype: MT
---

# 오프 라인 주소록 생성 일정이 변경

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-12-05_

OAB(오프라인 주소록)는 다운로드된 주소록의 복사본이므로 Outlook 사용자는 서버와의 연결이 끊긴 동안 OAB에 포함된 정보에 액세스할 수 있습니다. Set-MailboxServer cmdlet에서 *OABGeneratorWorkCycle* 및 *OABGeneratorWorkCycleCheckpoint* 매개 변수를 사용하면 OAB 생성 빈도를 구성할 수 있습니다.

OAB와 관련된 추가 관리 작업에 대한 자세한 내용은 [오프 라인 주소록 절차](offline-address-book-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "오프라인 주소록" 항목

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 OAB 속성 구성

이 예에서는 매일 6시간마다 사서함 서버 MBXServer01에서 오프라인 주소록이 생성됩니다.

    Set-MailboxServer -Identity MBXServer01 -OABGeneratorWorkCycle 01.00:00:00 -OABGeneratorWorkCycleCheckpoint 06:00:00 

구문과 매개 변수에 대한 자세한 내용은 [Set-OfflineAddressBook](https://technet.microsoft.com/ko-kr/library/aa996330\(v=exchg.150\))를 참조하십시오.

