---
title: '사서함 데이터베이스 복사본 활성화: Exchange 2013 Help'
TOCTitle: 사서함 데이터베이스 복사본 활성화
ms:assetid: d948269b-c902-4d8d-8c2b-269473359baa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee364750(v=EXCHG.150)
ms:contentKeyID: 50484264
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 데이터베이스 복사본 활성화

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-01_

사서함 데이터베이스의 새 활성 복사본으로 특정 수동 복사본을 지정 하는 과정은 사서함 데이터베이스 복사본을 활성화 합니다. 이 과정은 *데이터베이스 전환*을 이라고 합니다. 데이터베이스 전환을 현재 활성 데이터베이스를 분리 하는 새 활성 사서함 데이터베이스 복사본으로 지정된 된 서버에서 데이터베이스 복사본을 탑재 하는 작업이 포함 됩니다. 정상 상태이 고 현재 활성 사서함 데이터베이스를 만드는 하는 데이터베이스 복사본 이어야 합니다.

사서함 데이터베이스 복사본과 관련된 다른 관리 작업에 대한 자세한 내용은 [사서함 데이터베이스 복사본 관리](managing-mailbox-database-copies-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 활성 사서함 데이터베이스 이동

1.  EAC에서 **서버** \> **데이터베이스**로 이동합니다.

2.  데이터베이스 복사본을 활성화 하려면 선택 합니다.

3.  세부 정보 창에서 **데이터베이스 복사본** 활성화 하려면 데이터베이스 복사본에서 **활성화** 를 클릭 합니다.

4.  **예** 를 데이터베이스 복사본 활성화를 클릭 합니다.

## 셸을 사용 하 여 활성 사서함 데이터베이스를 이동 하려면

이 예제에서는 활성화 하 고 새 활성 사서함 데이터베이스 m b x 3에서 DB4 호스트 된 데이터베이스의 복사본을 탑재 합니다. 이 명령은 DB4 새 활성 사서함 데이터베이스를 만들고 m b x 3에서 데이터베이스 탑재 다이얼 설정이 무시 하지 않습니다.

    Move-ActiveMailboxDatabase DB4 -ActivateOnServer MBX3 -MountDialOverride:None

사서함 서버 m b x 1 DB2 데이터베이스의 전환을 수행 하는이 예제입니다. 명령이 완료 되 면 m b x 1 d b 2의 활성 복사본을 호스트 합니다. *MountDialOverride* 매개 변수는 `None`로설정하면 때문에 m b x 1에서 자체 정의 된 데이터베이스 자동 탑재 다이얼 설정을 사용 하 여 데이터베이스를 탑재 합니다.

    Move-ActiveMailboxDatabase DB2 -ActivateOnServer MBX1 -MountDialOverride:None

사서함 서버 m b x 3 데이터베이스 d b 1의 전환을 수행 하는이 예제입니다. 명령이 완료 되 면 m b x 3 d b 1의 활성 복사본을 호스트 합니다. M b x 3 자동 데이터베이스 탑재를 사용 하 여 데이터베이스를 탑재 *MountDialOverride* 매개 변수는 `Good Availability`의 값으로 지정 되어 있으므로 *GoodAvailability*의 설정을 전화 접속 합니다.

    Move-ActiveMailboxDatabase DB1 -ActivateOnServer MBX3 -MountDialOverride:GoodAvailability

이 예에서는 데이터베이스 DB3을 사서함 서버 MBX4로 전환합니다. 명령을 완료하면 MBX4가 DB3의 활성 복사본을 호스트합니다. *MountDialOverride* 매개 변수를 지정하지 않았으므로 MBX4는 *Lossless*의 데이터베이스 자동 탑재 다이얼 설정을 사용하여 데이터베이스를 탑재합니다.

    Move-ActiveMailboxDatabase DB3 -ActivateOnServer MBX4

이 예에서는 사서함 서버 MBX1에 대해 서버 전환을 수행합니다. MBX1의 모든 활성 사서함 데이터베이스 복사본이 MBX1의 양호한 활성 데이터베이스 복사본을 사용하여 하나 이상의 다른 사서함 서버에서 활성화됩니다.

    Move-ActiveMailboxDatabase -Server MBX1

사서함 서버 MBX5 DB4 데이터베이스의 전환을 수행 하는이 예제입니다. 이 예제에서는 MBX5에 데이터베이스 복사본에는 6 보다 큰 재생 큐 있습니다. 결과적으로, MBX5에 데이터베이스 복사본을 활성화 하려면 *SkipLagChecks* 매개 변수를 지정 합니다.

    Move-ActiveMailboxDatabase DB4 MBX5 -SkipLagChecks

사서함 서버 MBX6 DB5 데이터베이스의 전환을 수행 하는이 예제입니다. 이 예제에서는 MBX6에 데이터베이스 복사본에는 failed *ContentIndexState* 있습니다. 결과적으로, MBX6에 데이터베이스 복사본을 활성화 하려면 *SkipClientExperienceChecks* 매개 변수를 지정 합니다.

    Move-ActiveMailboxDatabase DB5 MBX6 -SkipClientExperienceChecks

## 작동 여부는 어떻게 확인합니까?

사서함 데이터베이스 복사본을 활성화 하 고 성공적으로 했을 때 있는지를 확인 하려면 다음 중 하나를 수행 합니다.

  - EAC에서 **서버** \> **데이터베이스**로 이동합니다. 적절한 데이터베이스를 선택하고 세부 정보 창에서 **세부 정보 보기**를 클릭하여 데이터베이스 복사 속성을 봅니다.

  - 셸에서 다음 명령을 실행하여 데이터베이스 복사본에 대한 상태 정보를 표시합니다.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## 자세한 내용

[사서함 데이터베이스 복사본](mailbox-database-copies-exchange-2013-help.md)

[사서함 데이터베이스 복사본 속성 구성](configure-mailbox-database-copy-properties-exchange-2013-help.md)

