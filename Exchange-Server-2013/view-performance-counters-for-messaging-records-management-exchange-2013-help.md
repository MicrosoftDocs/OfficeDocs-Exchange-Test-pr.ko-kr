﻿---
title: '메시징 레코드 관리에 대 한 성능 카운터 보기: Exchange 2013 Help'
TOCTitle: 메시징 레코드 관리에 대 한 성능 카운터 보기
ms:assetid: ec374d31-2797-4f8b-8c96-3839d01a662c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb397227(v=EXCHG.150)
ms:contentKeyID: 51407764
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시징 레코드 관리에 대 한 성능 카운터 보기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2009-12-09_

선택 하 고 메시징 레코드 관리 (MRM)에 대 한 성능 카운터를 보려면 Windows 안정성 및 성능 모니터 (Perfmon.exe)를 사용할 수 있습니다. 성능 카운터를 사용 하 여 모니터링할 수 있습니다는 관리 되는 폴더 도우미가 리소스 사용량이 MRM 프로세스를 실행 하는 동안.

MRM에 대 한 성능 카운터의 목록, [메시징 레코드 관리에 대 한 성능 카운터](performance-counters-for-https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/messaging-records-management/messaging-records-management)을 참조 하십시오.

모니터링 MRM과 관련 된 다른 작업을 찾고 있습니까? [모니터링 메시징 레코드 관리](monitoring-https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/messaging-records-management/messaging-records-management)확인할 수 있습니다.

## Windows 안정성 및 성능 모니터를 사용 하 여 MRM에 대 한 성능 카운터를 보려면

이 절차를 수행 하려면 사용 하는 계정이 위임 된 로컬 Administrators 그룹 구성원 이어야 합니다.

1.  Windows 안정성 및 성능 모니터를 시작 하려면 **시작** 을 클릭, **실행** 을 차례로 클릭 하 고 **perfmon**을 입력 합니다.

2.  콘솔 트리에서 **모니터링** 도구 이동 \> **성능 모니터** 합니다.

3.  도구 모음에 있는 더하기 기호 (+) 단추를 클릭 합니다. **카운터 추가** 대화 상자가 나타납니다.

4.  **컴퓨터에서 카운터 선택** 목록에서 다음 옵션 중 하나를 선택 합니다.
    
      - 로컬 컴퓨터에서이 절차를 수행 하는 경우에 **\< 로컬 컴퓨터 \>** 를 선택 합니다. 이 옵션은 기본 선택 합니다.
    
      - 이 절차를 원격으로 수행 되는 경우를 모니터링 하려는 서버를 선택 합니다.

5.  성능 카운터 목록에서 **MSExchange 비서-당 데이터베이스** 또는은 **MSExchange 관리 되는 폴더 도우미** 를 확장 합니다.

6.  모니터링할 성능 카운터를 선택 합니다.

7.  **MSExchange 비서-당 데이터베이스** 성능 카운터에 대 한 모든 사서함 데이터베이스에 대 한 카운터에서 **선택한 개체의 인스턴스** 를 보려면 **모든 인스턴스** 를 클릭 합니다. 또는 하나 이상의 사서함 데이터베이스를 지정 하려면 목록에서 인스턴스를 선택 합니다.

8.  Windows 안정성 및 성능 모니터 카운터 표시 되도록 선택된 된 카운터를 추가 하 고 성능 데이터 수집을 시작 하려면 **추가** 클릭 합니다.

