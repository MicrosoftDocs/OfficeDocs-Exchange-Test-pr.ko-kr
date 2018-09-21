---
title: 'Exchange 2010 시스템 사서함을 Exchange 2013으로 이동: Exchange 2013 Help'
TOCTitle: Exchange 2010 시스템 사서함을 Exchange 2013으로 이동
ms:assetid: a3b03c4e-0bc7-41a2-885c-e9cac37566c8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn249849(v=EXCHG.150)
ms:contentKeyID: 54915200
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2010 시스템 사서함을 Exchange 2013으로 이동

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2015-04-07_

Exchange 2010, 시스템 사서함 관리자 감사 로그를 eDiscovery 검색 하 고 메뉴, 예: 통합 메시징 데이터에 대 한 메타 데이터와 같은 조직 전체의 데이터를 저장 하는데 사용 되는 중재 사서함이 Microsoft Exchange에서에서 다이얼 플랜 및 사용자 지정 인사말 합니다. Microsoft Exchange 시스템 사서함 <strong>SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}</strong>; 라고 합니다. 표시 이름은 <strong>Microsoft Exchange</strong> 입니다.

기존 Exchange 2010 조직 Exchange 2013 를 업그레이드 하면 Exchange 2013 사서함 서버에서 사서함 데이터베이스에 Microsoft Exchange 시스템 사서함을 이동 해야 합니다. 설치 하 고 Exchange 2013 확인 한 후에이 사서함을 이동 해야 합니다. 시스템 사서함이 Exchange 2013 으로 이동 하지 Exchange 2010 및 Exchange 2013 동시에 Exchange 조직에서 사용 되는 경우 다음과 같은 문제가 발생 합니다.

  - Exchange 2013 작업이 관리자 감사 로그에 저장되지 않습니다. <strong>Search-AdminAuditLog</strong> cmdlet을 실행하거나 EAC에 있는 관리자 감사 로그를 내보내려고 할 때 Exchange 2013을 실행하지 않는 서버에 있는 시스템 사서함 SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9} 때문에 관리자 감사 로그 검색을 만들 수 없다는 오류가 발생합니다. 이벤트 ID가 5000인 Microsoft Exchange 오류는 명령이 실행될 때마다 Windows 응용 프로그램 로그에도 기록됩니다.

  - Exchange 2013 에서 EAC 또는 셸을 사용 하 여 eDiscovery 검색을 실행할 수 없습니다. 사서함 검색을 만든 큐에 대기 하 고 있지만 시작할 수 없습니다. 이벤트 ID가 6 인 오류가 <strong>Start-MailboxSearch</strong> cmdlet은 하지 못했음을 알리는 MsExchange 관리 로그에 기록 됩니다. 그러나 Exchange 2010 에서 셸 및 컨트롤 패널 ECP (Exchange)를 사용 하 여 사서함을 검색할 수 있습니다.

Exchange 2013 Exchange 2010 업그레이드의 일환으로 Microsoft Exchange 시스템 사서함 이동 해야하는 Exchange 2013 에 메시징 통합 합니다.

Exchange 2013으로 업그레이드하는 작업에 대한 자세한 내용은 다음 항목을 참조하세요.

  - [Exchange 2010에서 Exchange 2013으로 업그레이드](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)

  - [Exchange 2010 UM을 Exchange 2013 UM으로 업그레이드](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 20분. 실제 시간은 시스템 사서함의 크기에 따라 달라질 수 있습니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 이동 및 마이그레이션 권한" 항목

  - Exchange 2013에서 다음 명령을 실행하여 조직의 시스템 사서함이 포함된 Exchange Server 및 사서함 데이터베이스의 ID와 버전을 가져옵니다.
    
    ```powershell
Get-Mailbox -Arbitration | FL Name,DisplayName,ServerName,Database,AdminDisplayVersion
```
    
    <strong>AdminDisplayVersion</strong> 속성은 서버가 실행되는 Exchange의 버전을 나타냅니다. `Version 14.x` 값은 Exchange 2010을, `Version 15.x` 값은 Exchange 2013을 나타냅니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 수행하려는 작업

## EAC를 사용하여 시스템 사서함 이동

1.  EAC에서 <strong>받는 사람</strong> \> <strong>마이그레이션</strong>으로 이동합니다.

2.  <strong>새로 만들기</strong>(![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가"))를 클릭한 다음 <strong>다른 데이터베이스로 이동</strong>을 클릭합니다.

3.  <strong>새 로컬 사서함 이동</strong> 페이지에서 <strong>이동할 사용자 선택</strong>를 클릭한 다음 <strong>추가</strong>(![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가"))를 클릭합니다.

4.  <strong>사서함 선택</strong> 페이지에서 속성이 다음과 같은 사서함을 추가합니다.
    
      - 표시 이름이 <strong>Microsoft Exchange</strong>입니다.
    
      - 사서함 전자 메일 주소의 별칭이 <strong>SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}</strong>입니다.

5.  <strong>확인</strong>, <strong>다음</strong>을 차례로 클릭합니다.

6.  <strong>구성 이동</strong> 페이지에서 마이그레이션 일괄 처리 이름을 입력한 다음 <strong>대상 데이터베이스</strong> 상자 옆에 있는 <strong>찾아보기</strong>를 클릭합니다.

7.  <strong>사서함 데이터베이스 선택</strong> 페이지에서 시스템 사서함을 이동할 사서함 데이터베이스를 추가합니다. 선택한 사서함 데이터베이스가 버전 15.x인지 확인합니다. 이 버전은 데이터베이스가 Exchange 2013 서버에 있음을 나타냅니다.

8.  <strong>확인</strong>, <strong>다음</strong>을 차례로 클릭합니다.

9.  <strong>일괄 처리 시작</strong> 페이지에서 자동으로 시작할 옵션을 선택하고 마이그레이션 요청을 완료한 다음 <strong>새로 만들기</strong>를 클릭합니다.

## 셸을 사용하여 시스템 사서함 이동

먼저 Exchange 2013에서 다음 명령을 실행하여 조직에 있는 모든 사서함 데이터베이스의 이름과 버전을 가져옵니다.

```powershell
Get-MailboxDatabase -IncludePreExchange2013 | FL Name,Server,AdminDisplayVersion
```

조직에 있는 사서함 데이터베이스의 이름을 확인한 후에 Exchange 2013에서 다음 명령을 실행하여 Microsoft Exchange 시스템 사서함을 Exchange 2013 서버에 있는 사서함 데이터베이스로 이동합니다.

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | New-MoveRequest -TargetDatabase <name of Exchange 2013 database>

## 작동 여부를 확인하는 방법

Microsoft Exchange 시스템 사서함이 Exchange 2013 서버에 있는 사서함 데이터베이스로 이동되었는지 확인하려면 셸에 다음 명령을 실행합니다.

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | FL Database,ServerName,AdminDisplayVersion

<strong>AdminDisplayVersion</strong> 속성 값이 <strong>버전 15.x(빌드 xxx.x)</strong>이면 시스템 사서함이 Exchange 2013 서버에 있는 사서함 데이터베이스에 있음이 확인된 것입니다.

Microsoft Exchange 시스템 사서함을 Exchange 2013으로 이동한 후에는 다음의 관리 작업도 수행할 수 있습니다.

  - <strong>Search-AdminAuditLog</strong> cmdlet을 실행합니다.

  - EAC에서 관리자 감사 로그를 내보냅니다.

  - Exchange 2013에서 EAC 또는 셸을 사용하여 eDiscovery 검색을 만들고 시작합니다.

