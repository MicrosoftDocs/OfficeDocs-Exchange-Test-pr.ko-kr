---
title: '상태 집합 및 서버 상태 관리: Exchange 2013 Help'
TOCTitle: 상태 집합 및 서버 상태 관리
ms:assetid: a4f84312-6cfa-4f17-9707-676aadab1143
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn482054(v=EXCHG.150)
ms:contentKeyID: 59890395
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 상태 집합 및 서버 상태 관리

 

_**적용 대상:** Exchange Online, Exchange Server 2013 SP1_

_**마지막으로 수정된 항목:** 2013-12-02_

기본 제공 상태 보고 cmdlet을 사용하여 관리되는 가용성과 관련한 다음과 같은 여러 작업을 수행할 수 있습니다.

  - 서버 또는 서버 그룹의 상태 보기

  - 상태 집합 목록 보기

  - 특정 상태 집합과 관련된 프로브, 모니터 및 응답자 목록 보기

  - 모니터 및 모니터의 현재 상태 목록 보기

## 시작하기 전에 알아야 할 사항은 무엇입니까?

  - 각 절차의 예상 완료 시간: 2분

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 서버 상태 보기

셸을 사용하여 Exchange 2013을 실행 중인 서버의 상태 요약을 가져올 수 있습니다.

## 셸을 사용하여 서버 상태 보기

Exchange 2013을 실행 중인 서버에서 상태 집합 및 상태 정보를 보려면 다음 명령 중 하나를 실행합니다.

```powershell
Get-HealthReport -Identity <ServerName>
```

```powershell
Get-ServerHealth -Identity <ServerName> | Format-Table Server,CurrentHealthSetState,Name,HealthSetName,AlertValue,HealthGroupName -Auto
```

Exchange 2013을 실행 중인 서버 또는 데이터베이스 가용성 그룹의 상태 집합을 보려면 다음 명령 중 하나를 실행합니다.

```powershell
Get-ExchangeServer | Get-HealthReport -RollupGroup
```

```powershell
Get-ExchangeServer | Get-HealthReport -RollupGroup -HealthSetName <HealthSet>
```

```powershell
(Get-DatabaseAvailabiltyGroup <DAGName>).Servers | Get-HealthReport -RollupGroup
```

## 상태 집합 목록 보기

상태 집합은 구성 요소의 상태(정상 또는 비정상)를 확인하는 구성 요소의 모니터/프로브/응답자 그룹입니다. 셸을 사용하여 Exchange 2013을 실행 중인 서버의 상태 집합 목록을 확인할 수 있습니다.

## 셸을 사용하여 상태 집합 목록 보기

Exchange 2013을 실행 중인 서버의 상태 집합을 보려면 다음 명령을 실행합니다.

```powershell
Get-HealthReport -Server <ServerName>
```

## 상태 집합에 대한 프로브, 모니터 및 응답자 보기

상태 집합은 구성 요소의 상태(정상 또는 비정상)를 확인하는 구성 요소의 모니터/프로브/응답자 그룹입니다. 셸을 사용하여 Exchange 2013을 실행 중인 서버의 상태 집합과 관련된 프로브, 모니터 및 응답자 목록을 확인할 수 있습니다.

## 셸을 사용하여 상태 집합에 대한 프로브, 모니터링 및 응답자 보기

Exchange 2013을 실행 중인 서버의 상태 집합과 관련된 프로브, 모니터 및 응답자를 확인하려면 다음 명령을 실행합니다.

```powershell
Get-MonitoringItemIdentity -Server <ServerName> -Identity <HealthSetName> | Format-Table Identity,ItemType,Name -Auto
```

## 모니터 및 모니터의 현재 상태 목록 보기

모니터의 현재 상태는 상태 집합에서 "최악의 상태"인 모니터를 사용하여 보고됩니다. 상태 집합 세부 정보를 확인하면 정상 및 비정상 상태인 모니터를 파악할 수 있습니다.

## 셸을 사용하여 모니터 및 해당 현재 상태 목록 보기

Exchange 2013을 실행 중인 서버의 모니터 및 모니터의 현재 상태 목록을 보려면 다음 명령을 실행합니다.

```powershell
Get-ServerHealth -HealthSet <HealthSetName> -Server <ServerName> | Format-Table Name, AlertValue -Auto
```

