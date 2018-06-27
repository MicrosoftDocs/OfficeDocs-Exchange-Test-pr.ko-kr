---
title: '주 DNS 서버 contacted_PrimaryDNSTestFailed 아니어야 합니다.: Exchange 2013 Help'
TOCTitle: 주 DNS 서버 contacted_PrimaryDNSTestFailed 아니어야 합니다.
ms:assetid: 5b39cb64-c8f1-4fd3-843b-ecd23f99fe3a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.primarydnstestfailed(v=EXCHG.150)
ms:contentKeyID: 50483200
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주 DNS 서버 contacted\_PrimaryDNSTestFailed 아니어야 합니다.

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

기본 시스템 DNS (Domain Name) 서버와의 통신을 설정할 수 없는 Microsoft® Exchange Server 2007 설치를 계속할 수 없습니다.

Exchange 2007 설치는 로컬 컴퓨터의 도메인에 대 한 신뢰할 수 있는 DNS 데이터베이스 통신 필요 합니다.

Microsoft Exchange를 통해 다음 내부 또는 외부 대상 서버의의 IP 주소를 해결 하는 DNS에 따라 달라 집니다.

주 DNS 서버와의 통신은 다음과 같은 이유로 실패할 수 있습니다.

  - 로컬 TCP/IP 구성 올바른 DNS 서버를 가리키지 않습니다.

  - 네트워크 오류 또는 기타 이유로 인해 DNS 서버가 다운 되었거나 연결할 수 없는 되었습니다.

이 문제를 해결하려면 다음을 수행하십시오.

  - 로컬 TCP/IP 구성 올바른 DNS 서버를 가리키는지 확인 합니다.

로컬 TCP/IP 구성 되었는지 확인 하려면

1.  로컬 TCP/IP 구성을 검토 합니다.
    
    자세한 내용은 "DNS를 사용 하 여 TCP/IP 구성"을 참조 하십시오. ([https://go.microsoft.com/fwlink/?LinkId=68094](https://go.microsoft.com/fwlink/?linkid=68094)).

<!-- end list -->

  - DNS 서버가 실행 되 고 연결할 수 있음을 확인 합니다.

DNS 서버가 실행 되 고에 연결할 수 있는지 확인 하려면

1.  다음 확인 작업 중 하나를 수행하여 DNS 서버가 실행되고 있는지 확인합니다.
    
      - DNS 서버의 DNS 관리 프로그램에서 DNS 서버 상태를 확인합니다.
    
      - DNS 서버를 다시 시작 합니다.
        
        자세한 내용은 "시작, 중지, 일시 중지, 또는 DNS 서버를 다시 시작"를 참조 하십시오. ([https://go.microsoft.com/fwlink/?LinkId=62999](https://go.microsoft.com/fwlink/?linkid=62999)).
    
      - **Nslookup** 명령을 사용 하 여 DNS 서버 응답을 확인 합니다.
        
        자세한 내용은의 지침을 참조 하십시오. "nslookup 명령을 사용 하 여 DNS 서버 응답을 확인 합니다." ([https://go.microsoft.com/fwlink/?LinkId=63000](https://go.microsoft.com/fwlink/?linkid=63000)).

