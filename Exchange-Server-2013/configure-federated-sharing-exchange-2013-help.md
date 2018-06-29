---
title: '페더레이션 공유 구성: Exchange 2013 Help'
TOCTitle: 페더레이션 공유 구성
ms:assetid: b25ae450-def3-4797-a5fc-6e9bcee71a5d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657483(v=EXCHG.150)
ms:contentKeyID: 50483945
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 페더레이션 공유 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-07_

Exchange Server 2013에서 페더레이션 공유를 사용하면 사용자는 외부 페더레이션 조직의 받는 사람과 정보를 공유할 수 있습니다. 여기에는 일정 예약을 목적으로 하는 약속 있음/약속 없음(일정 가용성이라고도 함) 정보의 공유, 또는 비즈니스 관계의 특성에 따라 보다 자세한 일정 정보의 공유가 포함됩니다. 페더레이션 공유에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> Exchange Server 2013의 이 기능은 현재 중국에서 21Vianet에 의해 운영되는 Office 365와는 완전히 호환되지는 않으며 일부 기능 제한이 적용될 수 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet에 의해 운영되는 Office 365 정보</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 1시간입니다.

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 페더레이션 트러스트 만들기 및 구성

페더레이션 트러스트는 Exchange 2013 조직과 Azure Active Directory 인증 시스템 간에 트러스트 관계를 설정 하 고 페더레이션 공유에 대 한 요구 사항입니다.

자세한 내용은 [페더레이션 트러스트를 구성 합니다.](configure-a-federation-trust-exchange-2013-help.md)를 참조하십시오.

## 2단계: 조직 관계 만들기

조직 관계에는 Exchange 조직의 사용자가 다른 페더레이션 Exchange 조직과 페더레이션 공유의 일부로 일정 약속 있음/없음 정보를 공유할 수 있습니다. 두 페더레이션된 Exchange 2013 조직 간에 또는 페더레이션된 Exchange 2013 조직 및 페더레이션된 Exchange 2010 조직 간의 페더레이션 공유를 구성할 수 있습니다.

자세한 내용은 [조직 관계 만들기](create-an-organization-relationship-exchange-2013-help.md)를 참조하십시오.

## 3단계: 공유 정책 만들기

공유 정책을 사용하면 일정 정보를 여러 유형의 외부 사용자와 함께 사용자가 설정한 대로 사용자 간에 공유할 수 있습니다. 공유 정책은 외부 페더레이션 조직, 외부 비페더레이션 조직 및 인터넷 액세스 권한이 있는 개인과의 일정 및 연락처 정보 공유를 지원합니다. 사용자 간 공유 또는 연락처 공유(조직 수준의 공유에만 해당)를 구성하지 않아도 되면 공유 정책을 구성할 필요가 없습니다.

자세한 내용은 [공유 정책 만들기](create-a-sharing-policy-exchange-2013-help.md)를 참조하십시오.

## 4단계: 자동 검색 공용 DNS 레코드 구성

공용 DNS에 별칭 정식 이름(CNAME) 리소스 레코드를 추가해야 합니다. 새 CNAME 레코드는 자동 검색 서비스를 실행 중인 인터넷 연결 Exchange 2013 클라이언트 액세스 서버를 가리켜야 합니다.

CNAME 레코드 추가 방법에 대한 자세한 내용은 공용 DNS 레코드의 호스트 서비스를 참조하십시오. 일반적으로 이 서비스는 도메인 웹 사이트도 호스트하는 인터넷 기반 서비스입니다.

