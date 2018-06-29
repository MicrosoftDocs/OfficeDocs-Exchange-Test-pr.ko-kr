---
title: 'Exchange Server 2013의 Exchange Online Protection에서 제공되는 스팸 방지 기능의 이점: Exchange 2013 Help'
TOCTitle: Exchange Server 2013의 Exchange Online Protection에서 제공되는 스팸 방지 기능의 이점
ms:assetid: 00e37a3c-3fbc-488f-bdad-d52a3c80fd72
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673032(v=EXCHG.150)
ms:contentKeyID: 50482372
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange Server 2013의 Exchange Online Protection에서 제공되는 스팸 방지 기능의 이점

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-05-26_

다음은 Microsoft Exchange Server 2013, 대부분의 Microsoft Exchange Server 2010 는 동일한 기본 제공 스팸 방지 기능을 사용 하는 것과 반대로 클라우드 (Microsoft Exchange Online 또는 Microsoft Exchange Online Protection )에서 Exchange 스팸 방지 보호 기능을 사용할 때의 이점:

  - **더 많은 제어 및 쉽게 구성**   관리자는 스팸 필터링 하 여 조직의 요구를 충족 하는 최상의 자신이 되도록 설정 사용자 지정 하기 위해 Exchange 관리 센터 (EAC) 웹 기반 관리 콘솔을 사용할 수 있습니다. Exchange Server 2013 스팸 방지 사용자 인터페이스가 없습니다. EOP 스팸 방지 보호 기능 Exchange Online 에 포함 된

  - **더욱 강력한 콘텐츠 필터링**   Exchange 2013 연결 필터링 IP 허용 목록 및 IP 차단 목록은 경계 네트워크의 Edge 전송 서버를 설치 하는 경우에 사용할 수 있습니다. 자세한 내용은 [Edge 전송 서버](edge-transport-servers-exchange-2013-help.md)를 참조 하십시오. 클라우드, 신뢰할 수 있는 보낸사람 (다양 한 타사 소스에서 수집 된), 이러한 메시지는 표시 되지 않도록 실수로 스팸으로 확인에서 보낸 전자 메일 메시지에 대 한 필터링 스팸 건너뛸를 선택할 수 있습니다. 또한 호스팅되는 필터링 서비스를 사용 하 여 Microsoft의 차단 목록 및 목록 공급 업체 로부터 집계 된 큰 IP 수준 필터링을 제공 합니다.

  - **더욱 강력한 콘텐츠 필터링**   다음과 같이 콘텐츠 필터 정책을 손쉽게 구성할 수 있습니다.
    
      - 특정 언어로 작성된 메시지를 필터링합니다.
    
      - 특정 국가 또는 지역에서 보낸 메시지를 필터링합니다.
    
      - 대량 전자 메일 메시지(예: 광고 및 마케팅 전자 메일)를 스팸으로 표시합니다.
    
      - 메시지에서 특성을 검색하고 특정 고급 스팸 옵션 특성과 일치하는 경우 해당 메시지에 대한 작업을 수행합니다. 피싱이 염려되는 경우 이러한 옵션 중 일부는 보낸 사람 ID 및 SPF 기술의 조합을 제공하여 메시지를 인증하고 메시지가 스푸핑되지 않았는지 확인합니다.
    
    EAC에서 구성할 수 있는 위의 콘텐츠 필터 옵션 외에도 호스트된 필터링 서비스는 추가 URL 목록을 사용하여 메시지 본문에 특정 URL이 포함된 의심스러운 메시지를 차단합니다.

  - **더 신속한 업데이트**   스팸 업데이트가 보다 신속하게 네트워크를 통해 전파됩니다. Exchange Server 2013에서 업데이트는 매달 두 번 발생하지만 서비스는 매시간 여러 번 업데이트됩니다.

  - **아웃바운드 필터링**   아웃바운드 전자 메일 보내기를 위해 호스티드 서비스를 사용하는 경우 아웃바운드 스팸 필터링이 항상 사용하도록 설정되므로 이 서비스를 사용하는 조직 및 해당 받는 사람이 보호됩니다.

