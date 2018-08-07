---
title: '스키마 마스터가 Windows Server 2003 서비스 팩 1 이상을 실행하지 않음'
TOCTitle: 스키마 마스터에는 Windows Server 2003 서비스 팩 1 또는 later_SchemaFSMONotWin2003SPn 실행 되지 않음
ms:assetid: 644a85ca-7b36-4ed0-bd21-c64f2742df70
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.schemafsmonotwin2003spn(v=EXCHG.150)
ms:contentKeyID: 50483278
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 스키마 마스터에는 Windows Server 2003 서비스 팩 1 또는 later\_SchemaFSMONotWin2003SPn 실행 되지 않음

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft Exchange Server 2007를 계속할 수 없습니다는 도메인 컨트롤러에 할당 된 Microsoft Windows Server 2003 서비스 팩 1 (SP1) 또는 이후 버전의 Active Directory 디렉터리 서비스 스키마 마스터 역할을로 알려져 유연한 단일 마스터 작업 (FSMO)가 실행 되지 않음.

Exchange 2007 설치 프로그램 역할 스키마 FSMO 하는 도메인 컨트롤러는 Windows Server 2003 SP1 또는 이후 버전을 실행 하는 필요 합니다.

FSMO 모든 업데이트 및 Active Directory 스키마를 수정한 경우를 제어합니다.

이 문제를 해결 하려면 다음 중 하나 이상을 수행 합니다.

  - Windows Server 2003 SP1 또는 이후 버전으로 FSMO 도메인 컨트롤러를 업그레이드 하 고 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

  - Exchange 조직에서 Microsoft Windows Server 2003 서비스 팩 1 (SP1) 또는 이후 버전을 실행 하는 FSMO 도메인 컨트롤러 없으면 Exchange 2007 설치 프로그램을 실행 하 여 해당 FSMO 도메인 컨트롤러를 가리키는 /domaincontroller 매개 변수를 사용 합니다.
    
    \[*/DomainController*또는 */dc\<FQDN of domain controller\>*\]
    
    */DomainController* 매개 변수를 사용 하 여 속성 읽기 및 설치 하는 동안 Active Directory 에 쓰기를 사용 하 여 도메인 컨트롤러를 지정할 수 있습니다. NetBIOS 또는 정규화 된 도메인 이름 (FQDN) 형식을 사용할 수 있습니다.

Windows Server 2003 용 최신 서비스 팩을 얻으려면 "Windows Server TechCenter" ([https://go.microsoft.com/fwlink/?LinkId=45315](https://go.microsoft.com/fwlink/?linkid=45315))를 참조 합니다.

Exchange Server 2007 설치 매개 변수에 대 한 자세한 내용은 Exchange Server 2007 제품 설명서에 어떻게를 설치 Exchange 2007에서 무인 모드 "" ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476))를 참조 하십시오.

