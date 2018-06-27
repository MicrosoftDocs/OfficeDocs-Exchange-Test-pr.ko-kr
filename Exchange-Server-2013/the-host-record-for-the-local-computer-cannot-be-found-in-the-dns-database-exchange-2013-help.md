---
title: 'DNS 데이터베이스에서 로컬 컴퓨터의 호스트 레코드를 찾을 수 없습니다.: Exchange 2013 Help'
TOCTitle: DNS 데이터베이스에서 로컬 컴퓨터의 호스트 레코드를 찾을 수 없습니다.
ms:assetid: 2f18cb65-29fe-4b72-8d68-52fd503d5673
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.hostrecordmissing(v=EXCHG.150)
ms:contentKeyID: 50482755
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DNS 데이터베이스에서 로컬 컴퓨터의 호스트 레코드를 찾을 수 없습니다.

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2016-12-09_

DNS(Domain Name System) 데이터베이스에서 이 컴퓨터의 호스트(A) 레코드를 찾을 수 없기 때문에 Microsoft Exchange Server 2013 설치를 계속할 수 없습니다.

Exchange 2013을 설치하려면 도메인에 대해 신뢰할 수 있는 DNS 데이터베이스에 등록된 올바른 호스트(A) 레코드가 로컬 컴퓨터에 있어야 합니다.

Exchange는 DNS 호스트(A) 레코드를 통해 다음 내부 또는 외부 대상 서버의 IP 주소를 확인합니다.

이 문제를 해결하려면 다음을 수행하십시오.

  - 로컬 TCP/IP 구성 올바른 DNS 서버를 가리키는지 확인 합니다. 자세한 내용은 [TCP/IP 구성 설정](https://go.microsoft.com/fwlink/p/?linkid=108281)을 참조 하십시오.

  - Nslookup.exe를 사용 하 여 DNS 서버에 호스트 (A) 레코드가 있는지 확인 합니다. 자세한 내용은 [리소스를 확인 하려면 레코드가 DNS에 존재](https://go.microsoft.com/fwlink/?linkid=63001)을 참조 하십시오.

DNS 이름 확인, 문제 해결 및 호스트(A) 레코드에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [DNS 문제해결](https://go.microsoft.com/fwlink/p/?linkid=294828)

  - [리소스 레코드 관리](https://go.microsoft.com/fwlink/p/?linkid=294829)

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

