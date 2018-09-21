---
title: '서버 전환 수행: Exchange 2013 Help'
TOCTitle: 서버 전환 수행
ms:assetid: ffcefd56-b0a0-4229-9011-fff4197b7c74
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298187(v=EXCHG.150)
ms:contentKeyID: 62523793
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 서버 전환 수행

 

_<strong>적용 대상:</strong> Exchange Server 2013 SP1_

_<strong>마지막으로 수정된 항목:</strong> 2014-06-23_

서버 전환은 현재 사서함 서버의 활성 사서함 데이터베이스 복사본을 DAG(데이터베이스 가용성 그룹)에 있는 하나 이상의 다른 사서함 서버로 모두 이동하는 작업입니다. 이 작업은 현재 사서함 서버에 대한 예약된 중단을 준비하는 작업의 일부로 수행됩니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 데이터베이스당 30초

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "데이터베이스 사용 가능 그룹" 항목


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## EAC를 사용하여 서버 전환 수행

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

1.  EAC에서 <strong>서버</strong> \> <strong>서버</strong>로 이동합니다.

2.  전환할 사서함 서버를 선택합니다.

3.  세부 정보 창에서 <strong>서버 전환</strong>을 선택합니다.

4.  <strong>서버 전환</strong> 페이지에서 다음 중 하나를 수행합니다.
    
    1.  <strong>대상 서버를 자동으로 선택합니다.</strong>(전환할 각 데이터베이스에 대해 가장 적합한 사서함 서버를 시스템이 자동으로 선택함)의 기본 설정을 그대로 적용한 다음 <strong>저장</strong>을 클릭합니다.
    
    2.  <strong>지정한 대상 서버를 사용합니다.</strong>를 클릭하고 <strong>찾아보기</strong>를 클릭하여 사서함 서버를 선택한 다음 <strong>저장</strong>을 클릭합니다.

5.  전환이 완료되면 <strong>닫기</strong>를 클릭하여 <strong>서버 전환</strong> 페이지를 끝냅니다.

## 셸을 사용하여 서버 전환 수행

이 예에서는 서버 MBX1에 대해 서버 전환을 수행합니다. 시스템은 MBX1의 각 활성 데이터베이스에 가장 적합한 사서함 서버를 자동으로 선택합니다.

```powershell
Move-ActiveMailboxDatabase -Server MBX1
```

이 예에서는 사서함 서버 MBX4에 대해 서버 전환을 수행합니다. 명령이 완료되면 MBX5는 이전에 MBX4에서 활성화된 데이터베이스의 활성 복사본을 호스트합니다.

```powershell
Move-ActiveMailboxDatabase -Server MBX4 -ActivateOnServer MBX5
```

구문과 매개 변수에 대한 자세한 내용은 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/ko-kr/library/dd298068\(v=exchg.150\))를 참조하십시오.

