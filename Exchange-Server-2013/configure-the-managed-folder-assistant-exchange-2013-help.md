---
title: '관리 되는 폴더 도우미를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 관리 되는 폴더 도우미를 구성 합니다.
ms:assetid: 9fcfb9b6-bd24-4218-a163-bc599cd5476a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123958(v=EXCHG.150)
ms:contentKeyID: 50483801
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리 되는 폴더 도우미를 구성 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-10-01_

다음은 *관리 되는 폴더 도우미가* 사서함 도우미 보존 정책에 구성 된 메시지 보존 설정을 적용 하는 MicrosoftExchange 입니다.

MRM(메시징 레코드 관리)과 관련된 추가 관리 작업에 대한 자세한 내용은 [메시징 레코드 관리 절차](messaging-records-management-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 완료 시간: 1 분입니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "메시징 레코드 관리" 항목

  - 관리 되는 폴더 도우미를 구성 하려면 Exchange 관리 센터 (EAC)를 사용할 수 없습니다. 셸을 사용 해야 합니다.

  - Exchange 2013 관리 되는 폴더 도우미는 스로틀 기반 도우미입니다. 비서 스로틀 기반 항상를 실행 하는 하 고 예약할 수 필요가 없습니다. 사용할 수 있는 시스템 리소스 제한 됩니다. 관리 되는 폴더 도우미가 특정 기간 동안 내에서 사서함 서버의 모든 사서함을 처리를 위해 구성할 수 있습니다 (라고 한 *주기 작동)*합니다. 작업 주기는 기본적으로 1 일에 설정 됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용 하 여 구성 관리 되는 폴더 도우미

이 예에서는 구성의 관리 되는 폴더 도우미가 1 일 내에서 모든 사서함을 처리 합니다.

    Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1

구문과 매개 변수에 대한 자세한 내용은 [Set-MailboxServer](https://technet.microsoft.com/ko-kr/library/aa998651\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

성공적으로 구성 했는지 관리 되는 폴더 도우미를 확인 하려면 *ManagedFolderWorkCycle* 매개 변수를 확인 하려면 [Get-MailboxServer](https://technet.microsoft.com/ko-kr/library/bb123539\(v=exchg.150\)) cmdlet을 사용 합니다.

이 명령은 조직에서 모든 사서함 서버를 검색 하 고 표 형식에서 각 서버에서의 관리 되는 폴더 도우미의 작업 사이클을 새로 속성을 출력 합니다. *Auto* 스위치는 열 너비에 맞게 자동으로 사용 됩니다.

    Get-MailboxServer | Format-Table Name,ManagedFolderWorkCycle* -Auto

## 셸을 사용 하 여 관리 되는 폴더 도우미를 시작 하려면

이 트리거하는이 예제는 관리 되는 폴더 도우미가 즉시 Morris Cornejo 사서함을 처리 합니다.

    Start-ManagedFolderAssistant -Identity morris.cornejo@contoso.com

자세한 구문 및 매개 변수 정보에 대 한 [Start-ManagedFolderAssistant](https://technet.microsoft.com/ko-kr/library/aa998864\(v=exchg.150\))를 참조 하십시오.

