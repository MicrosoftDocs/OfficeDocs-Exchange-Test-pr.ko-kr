---
title: 'Active Directory: Exchange 2013 Help'
TOCTitle: Active Directory
ms:assetid: 8e8464df-2d1d-4d68-82de-b0c158c549c3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123715(v=EXCHG.150)
ms:contentKeyID: 50483634
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013Active Directory 를 사용 하 여 저장 하 고 Windows 와 디렉터리 정보를 공유 합니다. Exchange Server 2010Exchange 2013 에 대 한 Active Directory 포리스트 디자인 비슷합니다 아래에 설명 하는 몇가지 방법으로 제외 합니다.

## Active Directory 드라이버

Active Directory 드라이버 Exchange 서비스를 만들려면 다음을 허용 하는 핵심 Microsoft Exchange 구성 요소를 수정, 삭제 및 Active Directory 도메인 서비스 (AD DS) 데이터에 대 한 쿼리 됩니다. Exchange 2013Active Directory 에 대 한 모든 액세스 수행 자체 Active Directory 드라이버를 사용 합니다. 이전에 DSAccess Exchange 2010 SMTP, 메시지 전송 에이전트 (MTA) 및 Exchange 저장소 등의 구성 요소에 대 한 디렉터리 조회 서비스를 제공 합니다.

Active Directory 드라이버는 또한 Microsoft ExchangeActive Directory 디렉터리 서비스 액세스 (DSAccess) 토폴로지 데이터를 사용 하 여 Active Directory 드라이버를 허용 하는 토폴로지 (MSExchangeADTopology)를 사용 합니다. 이 데이터를 사용할 수 있는 도메인 컨트롤러 및 Exchange 요청을 처리 하는데 사용할 수 있는 글로벌 카탈로그 서버 목록을 포함 합니다. Active Directory 드라이버 대 한 자세한 내용은 [Active Directory 도메인 서비스](https://go.microsoft.com/fwlink/p/?linkid=110942)를 참조 하십시오.

## Active Directory 스키마 변경 사항

Exchange 2013 Active Directory 도메인 서비스 스키마에 새 특성을 추가 하 고도 같이 기존 클래스 및 특성을 다른 수정 합니다. Exchange 2013, 참조 [Exchange 2013 Active Directory 스키마 변경 사항](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)를 설치 하면 Active Directory 변경 하는 방법에 대 한 자세한 내용은 합니다.

## 자세한 내용

Exchange 2013 저장 하 고 그에 대 한 액세스를 계획할 수 있도록 Active Directory에 대 한 정보를 검색 하는 방법에 대 한 자세한 내용은, [Active Directory에 대 한 액세스](access-to-active-directory-exchange-2013-help.md)를 참조 하십시오.

Active Directory 포리스트 디자인 하는 방법에 대 한 자세한 내용은 [AD DS 디자인 가이드](https://go.microsoft.com/fwlink/p/?linkid=264957)을 참조 하십시오.

Active Directory 도메인의 Windows를 실행 하 고 Exchange 2013 연결 되지 않은 네임 스페이스가 있는 도메인에 배포 하는 컴퓨터에 대 한 자세한 내용은 [분리 된 네임 스페이스 시나리오](disjoint-namespace-scenarios-exchange-2013-help.md)를 참조 하십시오.

