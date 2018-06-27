---
title: 'Exchange 2013 사서함 이동: Exchange 2013 Help'
TOCTitle: Exchange 2013 사서함 이동
ms:assetid: 9c0a0bc9-2a39-4cf0-aa6e-6e5ef3fd38b5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150543(v=EXCHG.150)
ms:contentKeyID: 50483763
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 사서함 이동

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-07_

사서함을 이동할 때는 *원본 사서함 데이터베이스*에서 *대상 사서함 데이터베이스*로 이동합니다. 대상 사서함 데이터베이스는 동일한 서버, 다른 서버, 다른 도메인, 다른 Active Directory 사이트, 다른 포리스트에 있을 수 있습니다.

## 사서함 이동의 이유

다음 시나리오에서 사서함을 이동해야 할 수 있습니다.

  - **업그레이드**   기존 Microsoft Exchange Server 2007 또는 Exchange Server 2010 조직에서 Exchange Server 2013으로 업그레이드할 때 기존 Exchange 서버에서 Exchange 2013 사서함 서버로 사서함을 이동합니다.

  - **재배치**   재배치 목적으로 사서함을 이동할 수 있습니다. 예를 들어, 사서함 크기 제한이 더 큰 데이터베이스로 사서함을 이동할 수 있습니다.

  - **문제 조사**   사서함의 문제를 조사해야 하는 경우 해당 사서함을 다른 서버로 이동할 수 있습니다. 예를 들어, 사용량이 많은 모든 사서함을 다른 서버로 이동할 수 있습니다.

  - **손상된 사서함**   사서함이 손상된 경우 다른 서버나 데이터베이스로 사서함을 이동할 수 있습니다. 손상된 메시지는 이동할 수 없습니다.

  - **물리적 위치 변경**   다른 Active Directory 사이트에 있는 서버로 사서함을 이동할 수 있습니다. 예를 들어, 사용자가 다른 물리적 위치로 이동하는 경우, 이 사용자의 사서함을 해당 위치에 더 가까운 서버로 이동할 수 있습니다.

  - **관리 역할 분리**   Exchange 운영 체제 계정 관리에서 Windows 관리를 분리해야 할 수 있습니다. 이렇게 하려면 단일 포리스트에서 리소스 포리스트 시나리오로 사서함을 이동하면 됩니다. 이 시나리오에서는 Exchange 사서함이 한 포리스트에 있고 관련 Windows 사용자 계정은 별도의 포리스트에 있습니다.

  - **전자 메일 관리 아웃소싱**   전자 메일 관리를 아웃소싱하고 Windows 사용자 계정 관리를 유지해야 하는 경우가 있습니다. 이렇게 하려면 단일 포리스트에서 리소스 포리스트 시나리오로 사서함을 이동하면 됩니다.

  - **전자 메일 및 사용자 계정 관리 통합**   별도의 아웃소싱 전자 메일 관리 모델을 동일한 포리스트 내에서 전자 메일과 사용자 계정을 관리할 수 있는 모델로 변경해야 하는 경우가 있습니다. 이렇게 하려면 리소스 포리스트 시나리오에서 단일 포리스트로 사서함을 이동하면 됩니다. 이 시나리오에서는 Exchange 사서함과 Windows 사용자 계정이 동일 포리스트에 있습니다.

## Exchange 2013 이동

Microsoft Exchange Server 2013에는 *일괄 이동* 및 *마이그레이션 끝점*이라는 개념이 도입되었습니다. 마이그레이션 끝점은 원격 서버와 하나 이상의 일과 처리와 연결될 수 있는 연결을 설명하는 관리 개체입니다. 또한 새로운 일괄 이동 아키텍처는 향상된 관리 기능을 통해 MRS(사서함 복제 서비스) 이동을 향상시킵니다. Exchange 2013의 일괄 이동 아키텍처에는 다음과 같은 기능이 있습니다.

  - 대량 일괄 처리에서 여러 개의 사서함 이동 가능

  - 보고 기능을 사용하여 이동 중 전자 메일 알림

  - 이동의 자동 재시도 및 우선 순위 지정

  - 기본 및 개인 보관 사서함을 함께 또는 따로 이동 가능

  - 이동을 완료하기 전에 검토할 수 있게 하는 수동 이동 요청 완료 옵션

  - 마이그레이션 변경 내용을 업데이트하기 위한 주기적인 증분 동기화

Exchange 2013에서는 EAC(Exchange 2013 관리 센터) 및 Exchange 관리 셸을 사용하여 Exchange 2007, Exchange 2010 및 Exchange 2013 간 사서함을 이동해야 합니다.


> [!NOTE]
> EAC나 이동 요청 또는 마이그레이션 일괄 cmdlet을 사용하여 Exchange Server 2010과 비슷한 단일 사서함 이동을 Exchange 2013에서 수행할 수도 있습니다.




> [!NOTE]
> 온-프레미스 사서함을 Exchange Server 2003에서 Exchange 2013으로 이동할 수 없습니다.



새 이동 및 기존 이동 관리에 대한 자세한 내용은 [온-프레미스 이동 관리](manage-on-premises-moves-exchange-2013-help.md)을 참조하십시오.

## 마이그레이션 끝점

마이그레이션 끝점은 원격 서버 정보를 캡처하고 데이터 및 원본 제한 설정을 마이그레이션하기 위해 필요한 자격 증명을 유지합니다. 마이그레이션 끝점을 사용하여 원격 및 크로스 포리스트 이동에 대한 설정을 구성할 수 있습니다. 로컬 이동에서는 끝점을 사용할 필요가 없습니다. 로컬 이동은 두 개의 서로 다른 온-프레미스 Exchange 데이터베이스 간에 사서함을 이동하는 이동입니다.

다음 목록은 마이그레이션 끝점을 지원하는 이동 유형을 보여 줍니다.

  - **포리스트 간 이동** 두 개의 서로 다른 온-프레미스 Exchange 포리스트 간에 사서함을 이동합니다. 포리스트 간 이동에는 Exchange RemoteMove 끝점을 사용해야 합니다.

  - **원격 이동**   하이브리드 배포에서는 원격 이동에 *온보딩* 또는 *오프보딩* 마이그레이션이 포함됩니다. 원격 이동에서는 RemoteMove 끝점을 사용해야 합니다. 온보딩의 경우 온-프레미스 Exchange 조직에서 Microsoft Exchange의 Office 365 Online으로 사서함을 이동하고 마이그레이션 일괄 처리의 원본 끝점으로 RemoteMove 끝점을 사용합니다. 오프보딩의 경우 Exchange의 Office 365 Online에서 온-프레미스 Exchange 조직으로 사서함을 이동하고 마이그레이션 일괄 처리의 대상 끝점으로 Exchange RemoteMove 끝점을 사용합니다.

다음 표에서는 Exchange 2013에서 관리할 수 있는 마이그레이션 끝점 유형 및 값을 보여줍니다.

### 마이그레이션 끝점 유형의 값

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange RemoteMove</th>
<th>Exchange LocalMove</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MaxConcurrentMigrations</p></td>
<td><p>MaxConcurrentMigrations</p></td>
</tr>
<tr class="even">
<td><p>RemoteServer</p></td>
<td><p>Site</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDomain</p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>BadItemLimit</p></td>
</tr>
<tr class="even">
<td><p>Databases</p></td>
<td><p>LargeItemLimit</p></td>
</tr>
<tr class="odd">
<td><p>TargetDeliveryDomain</p></td>
<td><p>PrimaryOnly</p></td>
</tr>
<tr class="even">
<td><p>PrimaryOnly</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDatabase</p></td>
<td><p>DAG</p></td>
</tr>
<tr class="even">
<td><p>ArchiveOnly</p></td>
<td><p>Forest</p></td>
</tr>
</tbody>
</table>


마이그레이션 끝점에 대한 자세한 내용은 EAC의 **마이그레이션** 사용자 인터페이스와 [New-MigrationEndpoint](https://technet.microsoft.com/ko-kr/library/jj218611\(v=exchg.150\))를 참조하십시오.

새 이동 및 기존 이동 관리에 대한 자세한 내용은 [온-프레미스 이동 관리](manage-on-premises-moves-exchange-2013-help.md)을 참조하십시오.

