---
title: '단순 메일 전송 프로토콜 installed_SMTPSvcInstalled 현재입니다.: Exchange 2013 Help'
TOCTitle: 단순 메일 전송 프로토콜 installed_SMTPSvcInstalled 현재입니다.
ms:assetid: f786a93c-876d-4f4e-adb6-4dfea3d820d1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.smtpsvcinstalled(v=EXCHG.150)
ms:contentKeyID: 50484529
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 단순 메일 전송 프로토콜 installed\_SMTPSvcInstalled 현재입니다.

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft Windows Server™ 2003의 SMTP Simple Mail Transfer Protocol () 서비스가이 컴퓨터에 설치 된 Microsoft® Exchange Server 2007 설치를 계속할 수 없습니다.

Microsoft Exchange 설치 Exchange 2007에 사용 되는 서버에 SMTP 서비스를 설치 하지는 필요 합니다.

이 문제를 해결 하려면 SMTP 서비스를 제거 하 고 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

제어판에서 Windows 구성 요소를 제거 또는 추가 사용 하 여 SMTP 서비스를 제거 합니다.

1.  **시작** 메뉴에서 **제어판**을 클릭합니다.

2.  **프로그램 추가/제거**를 두 번 클릭합니다.

3.  **Windows 구성 요소 추가/제거** 를 클릭 합니다.

4.  **구성 요소** 목록에서 **응용 프로그램 서버** 확인란을 선택 하 고 **자세히** 를 클릭 합니다.

5.  **인터넷 정보 서비스 관리자** 를 선택한 다음 **자세히** 를 클릭 합니다.

6.  **SMTP 서비스** 를 선택 하 고 확인란의 선택을 취소를 클릭 합니다.

7.  **구성 요소** 목록에 반환 하 고 **다음** 을 클릭 한 다음에 두 번 **확인** 을 클릭 합니다.

8.  SMTP 서비스를 제거 하는 경우 **완료** 를 클릭 합니다.

