---
title: '도메인 컨트롤러를 재정의 Registry_ConfigDCHostNameMismatch에서 설정: Exchange 2013 Help'
TOCTitle: 도메인 컨트롤러를 재정의 Registry_ConfigDCHostNameMismatch에서 설정
ms:assetid: 3aef5470-d510-4b59-a4b6-36d274a984ae
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.configdchostnamemismatch(v=EXCHG.150)
ms:contentKeyID: 50482905
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 도메인 컨트롤러를 재정의 Registry\_ConfigDCHostNameMismatch에서 설정

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2016-12-15_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

지정 된 도메인 컨트롤러를 사용 하 여 해당 시도가 실패 했기 때문에 Microsoft Exchange Server 2007 설치를 계속할 수 없습니다. 도메인 컨트롤러의 레지스트리에 정적으로 매핑 되었습니다.

Exchange 2007 설치 프로그램 설치 명령에 지정 된 도메인 컨트롤러는 정적으로 매핑된 레지스트리 재정의 사용 하는 도메인 컨트롤러 일치 해야 합니다.

이 문제, 설치 프로그램을 실행된을 다시 해결 하려면 정적으로 매핑된 도메인 컨트롤러에 대 한을 지정 하는 **/DomainController: \<***FQDN of thestatically mapped domain controller***\>** 매개 변수입니다.

자세한 내용은 대 한 DSAccess 및 디렉터리 서비스 감지 Microsoft 기술 자료 문서 250570, "디렉터리 서비스 서버 감지 및 DSAccess 사용" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=250570](https://go.microsoft.com/fwlink/?linkid=3052&kbid=250570))를 참조 합니다.

