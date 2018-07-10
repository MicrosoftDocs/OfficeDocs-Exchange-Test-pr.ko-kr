---
title: '관리 되는 가용성 재정의 구성: Exchange 2013 Help'
TOCTitle: 관리 되는 가용성 재정의 구성
ms:assetid: c8f315b3-1d5e-4ad9-8bea-9c3a4a13ebfc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn482055(v=EXCHG.150)
ms:contentKeyID: 59890397
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리 되는 가용성 재정의 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2013 SP1_

_**마지막으로 수정된 항목:** 2015-11-30_

관리되는 가용성은 연속 검색을 수행하여 Exchange 구성 요소 또는 해당 종속성과 관련하여 발생할 수 있는 문제를 검색하며, 복구 작업을 수행하여 이러한 구성 요소의 문제로 인해 최종 사용자 환경이 영향을 받지 않도록 합니다. 그러나 기본 설정이 환경에 적합하지 않은 경우도 있습니다. 재정의를 작성하면 관리되는 가용성 프로브, 모니터 및 응답자를 사용자 정의할 수 있습니다.

재정의는 두가지 유형이: 로컬 및 전역 합니다. 이름에서 알 수 있듯이 로컬 재정의 기반이 만든 및 전역 재정의 재정의 여러 서버에 적용 되는 서버 에서만 사용할 수 있습니다. Exchange 있지만 동시에 하나만의 특정 버전 또는 특정 기간에 대 한 두 유형의 재정의 만들 수 있습니다.


> [!NOTE]
> 재정의 만들 때는 해당 하지 즉시 적용 됩니다. Microsoft Exchange 상태 관리 서비스 10 분 마다 구성 변경 내용을 확인 하 고 검색 된 구성 변경 내용을 로드 합니다. 대기 하지 않으려면 서비스를 다시 시작할 수 있습니다.



관리되는 가용성과 관련된 추가 관리 작업은 [상태 집합 및 서버 상태 관리](manage-health-sets-and-server-health-exchange-2013-help.md)를 참조하세요.

## 시작하기 전에 알아야 할 사항은 무엇입니까?

  - 각 절차의 예상 완료 시간: 5분

  - 이 절차는 셸을 사용해야 수행할 수 있습니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 사용 하 여 로컬 만들려는 Exchange 관리 셸 재정의

특정 기간에 대 한 로컬 재정의 만들려면 다음 구문을 사용 합니다.

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Duration <dd.hh:mm:ss>

Exchange 의 특정 버전에 대 한 로컬 재정의 만들려면 다음 구문을 사용 합니다.

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Version <15.01.xxxx.xxx>


> [!NOTE]
> 재정의 만드는 경우 <EM>Identity</EM> 매개 변수에서 사용 되는 값은 대/소문자 구분 합니다.



응답자 `ActiveDirectoryConnectivityConfigDCServerReboot` 20 일 동안 EXCH03 라는 서버에서 사용할 수 없도록 로컬 재정의 추가 하는이 예제입니다.

    Add-ServerMonitoringOverride -Server EXCH03 -Identity "AD\ActiveDirectoryConnectivityConfigDCServerReboot" -ItemType Responder -PropertyName Enabled -PropertyValue 0 -Duration 20.00:00:00

## 작동 여부는 어떻게 확인합니까?

을 로컬 재정의 성공적으로 만들어졌는지 확인 하려면 로컬 재정의 목록을 보려면 **Get-ServerMonitoringOverride** cmdlet을 사용 합니다.

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

재정의가 목록에 표시될 것입니다.

## 사용 하 여 로컬을 제거 하려면 Exchange 관리 셸 재정의

로컬 재정의 제거 하려면 다음 구문을 사용 합니다.

    Remove-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <PropertytoRemove>

이 예에서는 EXCH01 서버에서 설정 되는 Exchange 상태에서 `ActiveDirectoryConnectivityConfigDCServerReboot` 응답자의 기존 로컬 재정의 제거 합니다.

    Remove-ServerMonitoringOverride -Server EXCH01 -Identity Exchange\ActiveDirectoryConnectivityConfigDCServerReboot -ItemType Responder -PropertyName Enabled

## 작업이 완료되었는지 어떻게 확인합니까?

로컬 재정의 성공적으로 제거 했는지를 확인 하려면 로컬 재정의 목록을 보려면 **Get-ServerMonitoringOverride** cmdlet을 사용 합니다.

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

제거된 재정의가 목록에 표시되지 않게 됩니다.

## 사용 하 여 전역 만들려는 Exchange 관리 셸 재정의

특정 기간에 대 한 전역 재정의 만들려면 다음 구문을 사용 합니다.

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -Duration <dd.hh:mm:ss>

Exchange 의 특정 버전에 대 한 전역 재정의 만들려면 다음 구문을 사용 합니다.

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -ApplyVersion <15.01.xxxx.xxx>


> [!NOTE]
> 재정의 만드는 경우 <EM>Identity</EM> 매개 변수에서 사용 되는 값은 대/소문자 구분 합니다.



30 일 동안 `OnPremisesInboundProxy` 프로브를 사용 하지 않도록 설정 하는 전역 재정의 추가 하는이 예제입니다.

    Add-GlobalMonitoringOverride -Identity "FrontendTransport\OnPremisesInboundProxy" -ItemType Probe -PropertyName Enabled -PropertyValue 0 -Duration 30.00:00:00

Exchange 버전 15.01.0225.042를 실행 하는 모든 서버에 대 한 `StorageLogicalDriveSpaceEscalate` 응답자를 사용 하지 않도록 설정 하는 전역 재정의 추가 하는이 예제입니다.

    Add-GlobalMonitoringOverride -Identity "MailboxSpace\StorageLogicalDriveSpaceEscalate" -PropertyName Enabled -PropertyValue 0 -ItemType Responder -ApplyVersion "15.01.0225.042"

## 작동 여부는 어떻게 확인합니까?

전역 재정의가 정상적으로 작성되었는지 확인하려면 **Get-GlobalMonitoringOverride** cmdlet을 사용하여 전역 재정의 목록을 확인합니다.

    Get-GlobalMonitoringOverride

재정의가 목록에 표시될 것입니다.

## 제거할 전역 Exchange 관리 셸 재정의 사용

전역 재정의 제거 하려면 다음 구문을 사용 합니다.

    Remove-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <OverriddenProperty>

이 예제에서는 `FrontEndTransport` 상태 집합에서 `OnPremisesInboundProxy` 프로브 `ExtensionAttributes` 속성의 기존 전역 재정의 제거합니다.

    Remove-GlobalMonitoringOverride -Identity FrontEndTransport\OnPremisesInboundProxy -ItemType Probe -PropertyName ExtensionAttributes

## 작업이 완료되었는지 어떻게 확인합니까?

전역 재정의가 정상적으로 제거되었는지 확인하려면 **Get-GlobalMonitoringOverride** cmdlet을 사용하여 전역 재정의 목록을 확인합니다.

    Get-GlobalMonitoringOverride

제거된 재정의가 목록에 표시되지 않게 됩니다.

