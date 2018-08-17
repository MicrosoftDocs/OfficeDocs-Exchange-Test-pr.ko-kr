---
title: 'Exchange 작업 관리: Exchange 2013 Help'
TOCTitle: Exchange 작업 관리
ms:assetid: 276740c4-bdb7-49f1-9470-ae6f2bfd65aa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150503(v=EXCHG.150)
ms:contentKeyID: 50482746
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 작업 관리

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-11-16_

Exchange 작업은 Exchange 시스템 리소스 관리를 위해 명시적으로 정의된 Exchange Server 기능, 프로토콜 또는 서비스입니다. 각 Exchange 작업은 사용자 요청이나 백그라운드 작업을 실행하기 위해 CPU, 사서함 데이터베이스 작업 또는 Active Directory 요청 등과 같은 시스템 리소스를 사용합니다. Exchange 작업의 예로는 Outlook Web App, Exchange ActiveSync, 사서함 마이그레이션 및 사서함 도우미가 있습니다.

(Exchange 2010에서 제한 되는 사용자가 라고도 함)는 개별 사용자가 리소스를 사용 하는 방식을 제어 하 여 Exchange 작업을 관리 합니다. 개별 사용자가 Exchange 시스템 리소스를 사용 하는 방법을 제어 Exchange Server 2010 가능한 되었으며 Exchange Server 2013 에 대 한이 기능이 확장 되었습니다.


> [!NOTE]
> Microsoft 고객 서비스 및 지원의 지시에 따라 조직에서 Exchange 서버에서 시스템 리소스 상태를 모니터링 하 여 작업 관리만 수행 해야 합니다.



## 개별 사용자가 리소스를 사용하는 방식을 제어하여 작업 관리

Exchange 2013에서는 제한 기능이 향상되었습니다. 즉, 개별 사용자가 리소스를 과다하게 사용하더라도 서버 성능이나 사용자 환경에 미치는 부정적 영향이 최소화되도록 기능이 향상되었습니다.

기본적으로 제한 Exchange 2013 에 사용자를 사용 하면 대역폭을 줄이고 발생 하지 않고 짧은 기간에 대 한 리소스 사용을 높일 수 있습니다. 또한 매우 많은 양의 리소스를 사용 하는 사용자의 전체 잠금 자주, 취소가 것인지 또는 발생 하지 않습니다. 사용자 작업 수행이 완전히 차단, 되지 않고 제한 발생 하 고 프로세스 ("microdelays"으로 쿼리하고 인지,) 시간의 짧은 기간에 대 한 지연 되는 서버에 상당한 영향을 발생 하기 전에 발생 합니다.

**주요 기능**

Exchange가 Exchange 2013의 개별 사용자가 리소스를 사용하는 방식을 제어하는 주요 방법 몇 가지는 다음과 같습니다.

  - **급증 허용**   사용자는 제한을 경험하지 않고 짧은 시간 동안 리소스 사용량을 늘릴 수 있습니다.

  - **재충전 비율**   리소스 예산 시스템을 사용하여 사용자의 리소스 사용을 관리합니다. 사용자의 리소스 예산이 재충전되는 비율을 설정할 수 있습니다. 예를 들어 값이 600,000(밀리초)이면 사용자의 예산은 시간당 10분 사용의 비율로 재충전됩니다.

  - **트래픽 셰이핑**   사용자의 리소스 사용이 특정 기간 동안 구성된 제한에 도달하면 서버에 큰 영향을 미치기 전에 매우 짧은 시간 동안 해당 사용자가 지연됩니다. 사용자는 일반적으로 이러한 "마이크로 지연"을 인지하지 못합니다. 이러한 프로세스를 통해 Exchange 2013은 사용자의 생산성을 저하시키지 않고 트래픽을 효율적으로 관리할 수 있습니다. 트래픽 셰이핑은 조기 잠금에 비해 사용자에게 미치는 영향이 적고 잠금이 발생할 확률을 크게 감소시킵니다.

  - **최대 사용량**   드문 경우지만 사용자 한 명이 짧은 시간 동안 매우 많은 양의 리소스를 사용할 수 있습니다. 사전 예방 차원에서 최대 사용량 임계값에 도달한 사용자의 리소스 사용을 일시적으로 차단할 수 있습니다. 리소스 사용이 일시적으로 차단된 사용자는 사용 예산이 재충전되면 곧바로 차단이 해제됩니다.

개별 사용자가 리소스를 사용 하는 방법을 제어 하는데 사용할 수는 cmdlet의 목록에 대 한이 항목 뒷부분의 "개별 사용자가 리소스를 사용 하는 방법을 제어 하기 위한 Cmdlet"를 참조 하십시오.

**Exchange 2013 제한 기능 및 배포 고려 사항**

Exchange 2013을 새로 설치하거나 Exchange 2013을 Exchange 2010 컴퓨터가 포함된 동시 사용 환경에 설치하는 경우 Exchange 2013을 실행하는 컴퓨터에 사서함이 있는 모든 사용자는 새로운 Exchange 2013 제한 기능을 사용하여 제한됩니다. 하지만 Exchange 2010 클라이언트 액세스 서버를 통해 사서함에 액세스할 경우 Exchange 2010 사서함은 Exchange 2010 제한 기능을 통해 제한됩니다.

Exchange 2013을 동시 사용 환경에 설치한 경우 Exchange 2013 설치 프로세스는 사용자가 Exchange 2010 구성에서 설정한 제한 설정 중 일부를 가져오려고 시도할 수 있습니다. 하지만 Exchange 2013 제한 기능은 매우 다르기 때문에 레거시 제한 설정의 영향은 일반적으로 Exchange 2013에서 제한이 작동하는 방식에 영향을 미치지 않습니다.

**범위를 사용하여 제한 정책 관리**

Exchange 2010과 마찬가지로 Exchange 2013에는 하나의 기본 제한 정책이 있습니다. Exchange 2013에서 기본 제한 정책의 이름은 **GlobalThrottlingPolicy**입니다. 이 정책에는 **Global** 범위가 있습니다. 이외에 사용할 수 있는 사용자 제한 범위는 **Organization** 및 **Regular**입니다. Exchange 2013 사용자 제한 정책에 대해 범위 할당이 도입되어, 이제는 Exchange 2010에서와 다른 방법으로 제한 정책을 관리합니다. **GlobalThrottlingPolicy**는 조직에 대해 사용자 지정된 제한 정책이 있는 경우 외에는 조직의 모든 새 사용자 및 기존 사용자에 대한 기준 기본 제한 설정을 정의합니다. **GlobalThrottlingPolicy**는 대다수의 일반적인 Exchange 배포 시나리오에서의 사용자 관리에 적합합니다.

**GlobalThrottlingPolicy**를 수정하여 제한 설정을 사용자 지정하지 않는 것이 좋습니다. 대신 추가 제한 정책을 만들어야 합니다. 추가 제한 정책을 만들면 작업을 더 효율적으로 관리할 수 있습니다. 또한 제한 정책 설정의 수정 내용을 향후의 Exchange 2013 업데이트가 덮어쓰는 것도 방지할 수 있습니다.

조직의 모든 사용자에게 적용되는 제한 설정을 사용자 지정하려면 범위 할당이 **Organization**인 새 제한 정책을 만듭니다. 새 Organization 범위 정책에서는 **GlobalThrottlingPolicy**와 다른 제한 설정만 설정해야 합니다. 조직의 특정 사용자에게 적용되는 제한 설정을 사용자 지정하려면 범위 할당이 **Regular**인 새 제한 정책을 만듭니다. 새 Regular 범위 정책에서는 **GlobalThrottlingPolicy**와 다른 조직 정책과 다른 제한 설정만 설정해야 합니다. 이렇게 하면 정책 설정의 나머지를 **GlobalThrottlingPolicy**에서 상속하고 향후의 Exchange 업데이트에 추가되는 제한 정책의 모든 업데이트의 이점을 활용할 수 있습니다.

## 작업 제한 설정 관리

Exchange 관리 셸을 사용하여 Exchange 작업 제한 설정을 관리할 수 있습니다.

**개별 사용자가 리소스를 사용하는 방식을 제어하기 위한 cmdlet**

Exchange 2010에서 추가된 다음의 cmdlet을 사용하여 제한 설정을 관리할 수 있습니다.

제한 정책 관리

  - [Get-ThrottlingPolicy](https://technet.microsoft.com/ko-kr/library/dd351264\(v=exchg.150\))

  - [New-ThrottlingPolicy](https://technet.microsoft.com/ko-kr/library/dd351045\(v=exchg.150\))

  - [Remove-ThrottlingPolicy](https://technet.microsoft.com/ko-kr/library/dd351178\(v=exchg.150\))

  - [Set-ThrottlingPolicy](https://technet.microsoft.com/ko-kr/library/dd298094\(v=exchg.150\))

제한 정책 할당

  - [Get-ThrottlingPolicyAssociation](https://technet.microsoft.com/ko-kr/library/ff459241\(v=exchg.150\))

  - [Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/ko-kr/library/ff459231\(v=exchg.150\))


> [!NOTE]
> <STRONG>*-ResourcePolicy</STRONG>, <STRONG>*-WorkloadManagementPolicy</STRONG> 및 <STRONG>*-WorkloadPolicy</STRONG> 시스템 작업 관리 cmdlet가 사용 되지 않습니다. Microsoft 고객 서비스 및 지원의 지시에 따라만 시스템 작업 관리 설정은 사용자 지정 해야 합니다.


