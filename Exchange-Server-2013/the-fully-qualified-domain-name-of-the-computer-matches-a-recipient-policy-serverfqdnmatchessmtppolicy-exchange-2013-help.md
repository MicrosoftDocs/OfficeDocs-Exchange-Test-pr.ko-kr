---
title: '받는 사람 policy_ServerFQDNMatchesSMTPPolicy 일치 하는 컴퓨터의 정규화 된 도메인 이름: Exchange 2013 Help'
TOCTitle: 받는 사람 policy_ServerFQDNMatchesSMTPPolicy 일치 하는 컴퓨터의 정규화 된 도메인 이름
ms:assetid: f3ea61f8-1788-4cbf-814e-f7c088c1ac47
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.serverfqdnmatchessmtppolicy(v=EXCHG.150)
ms:contentKeyID: 50484496
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 받는 사람 policy\_ServerFQDNMatchesSMTPPolicy 일치 하는 컴퓨터의 정규화 된 도메인 이름

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft® Exchange Server 2007 설치 프로그램의 정규화 된 도메인 이름 (FQDN)는 로컬 컴퓨터의 받는 사람 정책의 SMTP Simple Mail Transfer Protocol () 주소와 일치 하기 때문에 계속할 수 없습니다.

Microsoft Exchange 설치 Exchange 조직에 있는 서버의 FQDN 같은 Exchange 조직에서 받는 사람 정책의 모든 SMTP 주소가 일치 하지 필요 합니다.

받는 사람 정책의 SMTP 주소와 일치 하는 컴퓨터의 FQDN이이 일치 하는 메일 장애 조치 SMTP 및 MTA 큐에 대 한 칸을 하면 발생할 수 있습니다.

이 문제를 해결 하려면 로컬 컴퓨터의 이름을 바꿀 또는 제거 또는 받는 사람 정책의 이름을 변경 하 고 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

로컬 컴퓨터의 이름을 바꾸려면

1.  **제어판** 에서 **시스템** 을 엽니다.

2.  **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.

3.  **컴퓨터 이름** 아래에서 컴퓨터에 대 한 새 이름을 입력 한 다음 **확인** 을 클릭 합니다. 사용자 이름 및 도메인의 컴퓨터의 이름을 바꾸려면 사용자 암호를 제공 하 라는 메시지가 표시 됩니다.

4.  **시스템 속성** 대화 상자를 닫으려면 **확인** 클릭 합니다. 변경 내용을 적용 하려면 컴퓨터를 다시 시작 하 라는 메시지가 표시 됩니다.


> [!IMPORTANT]
> 이름을 바꿀 하는 컴퓨터에서 도메인 컨트롤러를 있으면 "도메인 컨트롤러의 이름을 바꿀"를 참조 (<A href="https://go.microsoft.com/fwlink/?linkid=66828">https://go.microsoft.com/fwlink/?LinkId=66828</A>).



받는 사람 정책 SMTP 주소를 수정 하려면

1.  Exchange System Manager를 시작 합니다.

2.  **조직** 을 클릭, **받는 사람** 클릭 하 고 **받는 사람 정책** 을 차례로 클릭 합니다.

3.  변경 하려는 정책을 두번클릭 합니다.

4.  **전자 메일 주소** 탭을 클릭 한 다음 적절 한 SMTP 주소를 변경

받는 사람 정책 명명 문제에 대 한 자세한 내용은 Microsoft 기술 자료 문서 288175을 참조 하십시오. "XCON: 받는 사람 정책 5.4.8 조직에서 모든 서버의 FQDN과 일치할 수 없도록 하는 Ndr" ([http://go.microsoft.com/fwlink/?linkid=3052\&kbid=288175](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=288175)).

