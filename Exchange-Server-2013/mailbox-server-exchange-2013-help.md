---
title: '사서함 서버: Exchange 2013 Help'
TOCTitle: 사서함 서버
ms:assetid: 1aacc1c9-c81b-47d4-b222-ee73956cf968
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150491(v=EXCHG.150)
ms:contentKeyID: 50482591
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 사서함 서버

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2013-02-19_

Microsoft Exchange Server 2010에서 사서함 서버 역할은 사서함 및 공용 폴더 데이터베이스를 모두 호스트하고 전자 메일 메시지 저장소도 제공했습니다. 이제 Exchange Server 2013에서 사서함 서버 역할에는 클라이언트 액세스 프로토콜, 전송 서비스 사서함 데이터베이스 및 통합 메시징 구성 요소도 포함됩니다.

Exchange 2013에서는 사서함 서버 역할이 다음과 같은 프로세스에서 Active Directory, 클라이언트 액세스 서버 및 Microsoft Outlook 클라이언트와 직접 상호 작용합니다.

  - 사서함 서버는 Active Directory의 받는 사람, 서버 및 조직 구성 정보에 액세스하기 위해 LDAP를 사용합니다.

  - 클라이언트 액세스 서버는 클라이언트의 요청을 사서함 서버에 보내고 사서함 서버의 데이터를 클라이언트에 반환합니다. 또한 클라이언트 액세스 서버는 NetBIOS 파일 공유를 통해 사서함 서버의 OAB(온라인 주소록) 파일에 액세스합니다. 클라이언트 액세스 서버는 클라이언트와 사서함 간에 메시지, 약속 있음/없음 데이터, 클라이언트 프로필 설정 및 OAB 데이터를 전송합니다.

  - 방화벽 내부에 있는 Outlook 클라이언트는 클라이언트 액세스 서버에 액세스하여 메시지를 보내고 검색합니다. 방화벽 외부에 있는 Outlook 클라이언트는 HTTP 프록시 구성 요소를 통해 RPC를 사용하는 외부에서 Outlook 사용을 통해 클라이언트 액세스 서버에 액세스할 수 있습니다.

  - 공용 폴더 사서함에는 클라이언트가 방화벽 안쪽에 있거나 바깥쪽에 있거나 관계없이 RPC over HTTP를 통해 액세스할 수 있습니다.

  - 관리자 전용 컴퓨터는 Microsoft Exchange Active Directory 토폴로지 서비스에서 Active Directory 토폴로지 정보를 검색합니다. 또한 이 컴퓨터는 전자 메일 주소 정책 정보와 주소 목록 정보를 검색합니다.

  - 클라이언트 액세스 서버는 LDAP 또는 NSPI(Name Service Provider Interface)를 사용하여 Active Directory 서버에 연결하고 사용자의 Active Directory 정보를 검색합니다.

**사서함 및 클라이언트 액세스 서버 상호 작용 및 아키텍처**

![클라이언트 액세스 및 사서함 서버 상호 작용](images/JJ150491.d14577bf-14f9-40fa-bd49-a92932eb003a(EXCHG.150).gif "클라이언트 액세스 및 사서함 서버 상호 작용")

자세한 내용은 [Exchange 2013의 새로운 기능](what-s-new-in-exchange-2013-exchange-2013-help.md)의 "Exchange 2013 아키텍처" 섹션을 참조하십시오.

## 새 사서함 기능

다음 목록에서는 Exchange 2013 사서함 역할의 몇 가지 향상된 기능 및 새로운 기능에 대해 설명합니다.

  - Exchange 2010 DAG(데이터베이스 사용 가능 그룹)의 진화:
    
      - 수동 데이터베이스 복사본에서 깊은 검사점을 사용한 빠른 장애 조치(failover)를 위해 트랜잭션 로그 코드가 재조정되었습니다.
    
      - 향상된 사이트 복구를 지원하기 위해 서버는 서로 다른 위치에 있을 수 있습니다.

  - Exchange 2013에서는 이제 몇 가지 클라이언트 액세스 구성 요소, 전송 구성 요소 및 통합 메시징 구성 요소를 호스트합니다.

  - Exchange 저장소는 추가적인 I/O 감소 및 안정성의 성능을 향상시키기 위해 관리되는 코드로 재작성되었습니다.

  - 이제 각 Exchange 2013 데이터베이스가 자체 프로세스에서 실행됩니다.

  - Exchange 2010의 여러 사서함 검색 인프라는 스마트 검색으로 대체되었습니다.

## 사서함 서버 보안

기본적으로 사서함 서버와 기타 Exchange 서버 역할/도메인 컨트롤러/글로벌 카탈로그 서버 간의 HTTP, Microsoft Exchange ActiveSync, POP3 및 IMAP4 통신은 암호화됩니다. 또한 인터넷에서 사서함 서버에 액세스할 수 없는지 확인하십시오.

## 자세한 내용

[통합 메시징](unified-messaging-exchange-2013-help.md)

[메일 흐름](mail-flow-exchange-2013-help.md)

[고가용성 및 사이트 복구](high-availability-and-site-resilience-exchange-2013-help.md)

[메시징 정책 및 규정 준수](messaging-policy-and-compliance-exchange-2013-help.md)

[Exchange 2013 사서함 이동](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

[Exchange 2013의 사서함 데이터베이스를 관리 합니다.](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)

[메시징 정책 및 규정 준수](messaging-policy-and-compliance-exchange-2013-help.md)

[받는 사람](recipients-exchange-2013-help.md)

[공동 작업](collaboration-exchange-2013-help.md)

