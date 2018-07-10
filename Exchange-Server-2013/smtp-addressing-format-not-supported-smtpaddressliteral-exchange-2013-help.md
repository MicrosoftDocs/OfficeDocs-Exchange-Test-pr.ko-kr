---
title: '서식을 지정합니다 하지 Supported_SMTPAddressLiteral SMTP 주소 지정: Exchange 2013 Help'
TOCTitle: 서식을 지정합니다 하지 Supported_SMTPAddressLiteral SMTP 주소 지정
ms:assetid: b8b55917-d81f-4c0a-ad65-7bb10ac58df8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.smtpaddressliteral(v=EXCHG.150)
ms:contentKeyID: 50483991
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 서식을 지정합니다 하지 Supported\_SMTPAddressLiteral SMTP 주소 지정

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

지정 된 받는 사람 정책을 지원 하지 않는 SMTP Simple Mail Transfer Protocol () 주소 형식을 사용 하 여 Microsoft Exchange Server 2007 및 Exchange Server 2010 설치를 계속할 수 없습니다.

Exchange 2007 및 Exchange 2010 설치 필요는 전자 메일 주소 정책에 사용 되는 모든 SMTP 주소가 들어있지 IP 주소 리터럴을 예: *user@\[10.10.1.1\]*합니다.

이 문제를 해결 하려면 리터럴 IP 주소를 포함 하지 않는 있도록 받는 사람 정책에서 SMTP 주소 값을 변경 합니다. 대괄호 ()과 바꿉니다 리터럴 IP 주소 (10.10.1.1) 수가 시스템 DNS (Domain Name) 이름 형식, 예: *user@contoso.com*다음 Exchange 설치를 다시 실행 합니다.

Exchange Server 2007의 받는 사람 정책을 관리 하는 방법에 대 한 자세한 내용은 "관리 전자 메일 주소 정책" ([https://go.microsoft.com/fwlink/?LinkId=86653](https://go.microsoft.com/fwlink/?linkid=86653))을 참조 하십시오.

Exchange Server 2010에서의 받는 사람 정책을 관리 하는 방법에 대 한 자세한 내용은 "관리 전자 메일 주소 정책" ([https://go.microsoft.com/fwlink/?LinkId=179519](https://go.microsoft.com/fwlink/?linkid=179519))을 참조 하십시오.

