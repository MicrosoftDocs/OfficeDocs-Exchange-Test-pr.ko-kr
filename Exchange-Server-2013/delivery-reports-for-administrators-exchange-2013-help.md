---
title: '관리자에 대 한 배달 보고서: Exchange 2013 Help'
TOCTitle: 관리자에 대 한 배달 보고서
ms:assetid: d98623d3-e0b7-4cb9-93fb-6351b4a06137
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ919241(v=EXCHG.150)
ms:contentKeyID: 51407751
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리자에 대 한 배달 보고서

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

관리자에 대 한 배달 보고서를 사용 하 여 전송 또는 조직에서 특정 사서함에서 받은 메시지에 대 한 배달 정보를 추적할 수 있습니다. 특히, 배달 보고서 관리자를 위한 Exchange 관리 센터 (EAC)를 사용 하 여 메시지 추적 로그의 대상으로 지정 된 검색을 수행 합니다. 검색은 항상 특정 사서함에 범위가 지정 됩니다. 를 사용 하는 사서함에서 보내거나 사서함에 보낸 메시지를 검색할 수 및 메시지 제목으로 검색 결과 필터링 할 수 있습니다.

배달 보고서에 메시지 본문의 콘텐츠가 반환 되지 않습니다 있지만 제목줄 결과에 표시 됩니다. 메시지 내용에 따라 특정 전자 메일 메시지에 대 한 조직에서 사서함을 검색 하려면 [원본 위치 eDiscovery](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)를 참조 하십시오.

다음과 같은 경우에 유용 배달 보고서 검색을 찾을 수 있습니다.

  - 관리자는 학습자 시간에 대 한 할당으로 설정 하지 않았으므로 때문에 학습자에 대 한 불량 검토를 제공 합니다. 학습자 첨부 된 배정 된 메시지를 보낼 것을 원치 합니다. 관리자를 묻는 메시지의 상태를 확인할 수 있습니다.

  - 보안 공지를 즉시 회신할 수 있지만 아무도 회신에 요청 하는 사용자에 게 전송 되었습니다. 메시지 무시는 또는 자신이 방금 수신 하지 않은?

  - 사용자가 메시지를 받고 아무도 있다는 불만 제기 합니다. 이들은 자신의 메일에 대 한 배달 상태를 확인 하지만 상황을 알 수 없습니다. 조직 수준에서 메시지에 적용 되는 규칙 때문일 수 있습니다.

결과 배달 보고서는 다음과 같은 정보를 표시 한 배달 보고서 검색을 만든 후: from 및 to, 제목줄, 메시지를 보낸 사람과 때 메시지를 보냈습니다. 배달 보고서는 또한 메시지 배달 상태 및 배달 수 해당 작업을 지연 또는 실패 이유는 이유를 표시 합니다.

## 배달 보고서에 대 한 자세한

  - 다음은 새 배달 보고서를 만드는 방법: [배달 보고서로 메시지 추적](track-messages-with-delivery-reports-exchange-2013-help.md)합니다.

  - 온-프레미스 Exchange 조직이 모두 Exchange 관리 셸을 사용 하 여 메시지 추적 로그를 직접 쿼리 하 수 있습니다. 자세한 내용은 [메시지 추적 로그 검색](search-message-tracking-logs-exchange-2013-help.md)을 참조 하십시오.

  - 사용자가 자신의 메시지를 추적할 수 있습니다. 자세한 내용은 [사용자에 대 한 배달 보고서](https://go.microsoft.com/fwlink/?linkid=279920)를 참조 하십시오.

  - 조직에 이전 버전의 Exchange 있으면 배달 Exchange 버전 간에 Exchange 2013 works의 기능을 보고 하는 방법을 고려해 야 합니다.
    
      - Exchange 2013 배달 보고서는 동일한 Active Directory 사이트의 Exchange 2010 서버 간에 메시지를 추적할 수 있습니다.
    
      - Exchange 2013 배달 보고서는 동일한 Active Directory 사이트의 Exchange 2007 서버 간에 메시지를 추적할 수 없습니다. 배달 보고서 기능에는 원격 프로시저 호출 Exchange 2007 에 존재 하지 않는 웹 서비스 인터페이스를 사용 합니다.

