---
title: 'Exchange 검색: Exchange 2013 Help'
TOCTitle: Exchange 검색
ms:assetid: 967e2a13-4e54-486a-ac22-08768674abbb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232132(v=EXCHG.150)
ms:contentKeyID: 52058102
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 검색

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-09-17_

사서함 크기의 증가 및 메시지와 첨부 파일 형태로 사서함에 저장되는 데이터 양의 증가로 인해, 원하는 메시지를 빠르게 검색하고 찾을 수 있는 것이 사용자에게는 중요합니다. [전체에서 Exchange 2013의 보관](in-place-archiving-in-exchange-2013-exchange-2013-help.md)은 오래된 항목이나 가끔 액세스하는 항목을 보관함으로 이동시켜 .pst 파일의 사용을 줄이거나 아예 사용하지 않도록 도와줍니다. 이로 인해 사용자가 저장하는 사서함 데이터가 증가할 수 있고, 따라서 사용자의 기본 사서함과 보관 사서함 전반에서의 검색이 중요한 생산성 도구가 됩니다. [원본 위치 eDiscovery](in-place-ediscovery-exchange-2013-help.md)를 통해 인증된 사용자는 전자 검색(eDiscovery) 요청, 규정 감사 또는 내부 조사에 응하기 위해 온-프레미스 및 클라우드 기반 Exchange 조직에서 사서함의 콘텐츠를 검색할 수 있습니다. 원본 위치 eDiscovery는 Exchange 검색에서 만든 콘텐츠 인덱스를 사용합니다.

Exchange Search는 Exchange Server 2003의 전체 텍스트 인덱싱과 다르며, 성능, 콘텐츠 인덱싱 및 검색 면에서 향상되었습니다. 새 항목이 만들어지거나 사서함에 배달되면 전송 파이프라인에서 새 항목이 거의 즉시 인덱싱되므로 사용자는 빠르고 안정적이며 보다 신뢰할 수 있는 방식으로 사서함 데이터를 검색할 수 있습니다. 콘텐츠 인덱싱은 기본적으로 사용하도록 설정되며 초기 설정이나 구성이 필요하지 않습니다.

Exchange 검색에 대 한 자세한 내용은 다음을 참조 합니다.

  - [Exchange 검색에서 인덱싱하는 파일 형식](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Exchange 검색에서 인덱싱하는 메시지 속성](message-properties-indexed-by-exchange-search-exchange-2013-help.md)

Exchange 검색과 관련된 관리 작업에 대한 자세한 내용은 [Exchange 검색 절차](exchange-search-procedures-exchange-2013-help.md)를 참조하십시오.

## 새로운 기능

Exchange 2013에서는 Exchange 검색이 다음과 같이 변경됩니다.

  - 기본 콘텐츠 인덱싱 엔진이 Microsoft Search Foundation으로 대체되었습니다. Microsoft Search Foundation은 향상된 성능 및 기능을 제공하며, Exchange 및 SharePoint에서 공통 기본 콘텐츠 인덱싱 엔진으로 사용됩니다. 단, 관리 인터페이스는 기본 콘텐츠 인덱싱 엔진과 동일합니다.

  - 기본적으로 Search Foundation은 전자 메일 첨부 파일에서 가장 일반적인 파일 형식을 처리합니다. 더 이상 Exchange Search용 Microsoft Office Filter Pack을 설치하지 않아도 됩니다. Exchange Search에서 처리하는 파일 형식 목록은 [Exchange 검색에서 인덱싱하는 파일 형식](file-formats-indexed-by-exchange-search-exchange-2013-help.md)을 참조하십시오.
    
    이전 버전의 Exchange 에서처럼 Ifilter 설치 하 여 추가 파일 형식에 대 한 지원을 추가할 수 있습니다.

  - 이제 전송 파이프라인에서 메시지가 처리되므로 콘텐츠 인덱싱이 보다 효율적으로 수행됩니다. 따라서 여러 받는 사람이나 메일 그룹에 보내는 메시지가 한 번만 처리됩니다. 주석 스트림이 메시지에 첨부되어 더 적은 리소스를 사용하면서도 콘텐츠 인덱싱 속도가 대폭 향상됩니다.

