---
title: 'IIS 로그 및 로그 파서 Studio 보고서: Exchange 2013 Help'
TOCTitle: IIS 로그 및 로그 파서 Studio 보고서
ms:assetid: 01fa67d4-dc02-4c5f-93af-6da7b97d282f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn904092(v=EXCHG.150)
ms:contentKeyID: 63910909
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 로그 및 로그 파서 Studio 보고서

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2016-12-09_

## 로그 파서 Studio 보고서 분석

Log Parser Studio는을 통해 검색 하 고 여러 종류의 로그 파일을 포함 하 여 인터넷 정보 서비스 (IIS)에 대 한 보고서를 만들 수 있도록 하는 유틸리티입니다. Log Parser 2.2을 기반으로 구축 하 고은 쉽게 만들기 및 관리 관련된 SQL 쿼리를 실행 하는 것에 대 한 전체 사용자 인터페이스를 제공 합니다.

[Log Parser Studio 다운로드](https://go.microsoft.com/fwlink/p/?linkid=524244) 및 다음 [Log Parser Studio 시작](https://go.microsoft.com/fwlink/p/?linkid=524243)블로그 게시물을 검토 합니다.

기억 하는 Exchange 2013, IIS를 통해 이동에 대 한 모든 트래픽을 합니다. 즉, IIS 로그 분석 한 전체적인 그림을 방문 하는 서버를 대부분에 있는 사용자와의 연결에 대 한 프로토콜 관련 정보의 성능에 영향을 주지는 연결의 수를 얻을 수 있는 가장 좋은 방법입니다. Exchange 2013 성능 문제를 해결 하기 위해 20 개가 넘는 새로운 보고서 Log Parser Studio에 대 한 개발 되었습니다.

## Log Parser Studio 2013 성능 문제를 Exchange에 대 한 보고

Exchange 2013 환경에서 전체 부하에 대 한 포괄적인 이해를 활용 하려면 다음 보고 기능을 사용 하 고 각 서버에 대해 번호를 비교 합니다.

여기에 나열 된 Log Parser Studio 보고서 및 추가 문제해결 관련 보고서를 포함 하는.zip 파일에는 [여기에서 다운로드 한](https://go.microsoft.com/fwlink/p/?linkid=524245)될 수 있습니다.

  - <strong>IIS: 요청을 시간당</strong>합니다. 한번에 하나만 하지만 기본 웹사이트 (W3SVC1 디렉터리) 또는 백엔드 웹사이트 (W3SVC2 디렉터리)에서 IIS 로그에 공급 합니다.

  - <strong>ACTIVESYNC\_WP: %는 클라이언트가</strong>합니다. 모든 ActiveSync 요청 구분 하 여 사용자 에이전트 및 각 클라이언트의 백분율 요청의 총 수를 계산 합니다.

  - <strong>ACTIVESYNC\_WP: 요청을 시간당 (CSV)</strong>합니다. 시간당 ActiveSync 요청을 나열 하 고 결과 CSV 파일로 보냅니다.

  - <strong>ACTIVESYNC\_WP: 사용자 (CSV) 당 요청</strong>합니다. 사용자 당 ActiveSync 요청을 나열 하 고 결과 CSV 파일로 보냅니다.

  - <strong>ACTIVESYNC\_WP: 사용자 (위 10k) 당 요청</strong>합니다. 상위 10, 000 사용자에 대 한 사용자 당 ActiveSync 요청을 나열합니다.

  - <strong>ACTIVESYNC\_WP: 시작 (CSV) 가지 주요</strong>합니다. 가장 낮은 요청 수를 가장 높은에서 위쪽 ActiveSync 클라이언트를 나열 하 고 결과 CSV 파일로 보냅니다.

  - <strong>EWS\_WP: 클라이언트 %</strong>합니다. 모든 EWS 요청 구분 하 여 사용자 에이전트 및 각 클라이언트의 백분율 요청의 총 수를 계산 합니다.

  - <strong>EWS\_WP: 요청을 시간당 (CSV)</strong>합니다. 시간당 EWS 요청의 총 수를 나열합니다.

  - <strong>EWS\_WP: 사용자 (CSV) 당 요청</strong>합니다. 사용자 당 EWS 요청을 나열 하 고 결과 CSV 파일로 보냅니다.

  - <strong>EWS\_WP: 사용자 (위 10k) 당 요청</strong>합니다. 상위 10, 000 사용자에 대 한 사용자 당 EWS 요청을 나열합니다.

  - <strong>EWS\_WP: 시작 (CSV) 가지 주요</strong>합니다. 가장 낮은 요청 수를 가장 높은에서 위쪽 EWS 클라이언트를 나열합니다.

  - <strong>OLA\_WP: 하루 시간당 사용자 당 오류</strong>합니다. 외부에서 outlook 사용자의 요청 수입니다.

  - <strong>OLA\_WP: 요청을 시간당</strong>합니다. 시간당 외부에서 Outlook 사용 요청을 나열합니다.

  - <strong>OLA\_WP: 요청을 시간당 사용자 당</strong>합니다. 사용자별 시간당 외부에서 Outlook 사용 요청을 나열합니다.

  - <strong>OLA\_WP: 사용자 (CSV) 당 요청</strong>합니다. 사용자 당 요청 외부에서 Outlook 사용을 나열합니다.

  - <strong>OLA\_WP: (위 10k) 사용자 당 요청</strong>합니다. 상위 10, 000 개 사용자에 대 한 사용자 당 요청 외부에서 Outlook 사용을 나열합니다.

  - <strong>OLA\_WP: 시작 가지 주요</strong>합니다. 위쪽 외부에서 Outlook 클라이언트에서 가장 높은 가장 낮은 요청 수를 나열합니다.

  - <strong>OWA\_WP: %는 클라이언트가</strong>합니다. 모든 OWA 요청 구분 하 여 사용자 에이전트 및 각 클라이언트의 백분율 요청의 총 수를 계산 합니다.

  - <strong>OWA\_WP: 요청을 시간당 (CSV)</strong>합니다. 시간당 OWA 요청을 나열 하 고 결과 CSV 파일로 보냅니다.

  - <strong>OWA\_WP: 사용자 (CSV) 당 요청</strong>합니다. 사용자 당 OWA 요청을 나열 하 고 결과 CSV 파일로 보냅니다.

  - <strong>OWA\_WP: 사용자 (위 10k) 당 요청</strong>합니다. 상위 10, 000 사용자에 대 한 사용자 당 OWA 요청을 나열합니다.

  - <strong>OWA\_WP: 시작 (CSV) 가지 주요</strong>합니다. 가장 낮은 요청 수를 가장 높은에서 위쪽 OWA 클라이언트를 나열 하 고 결과 CSV 파일로 보냅니다.

