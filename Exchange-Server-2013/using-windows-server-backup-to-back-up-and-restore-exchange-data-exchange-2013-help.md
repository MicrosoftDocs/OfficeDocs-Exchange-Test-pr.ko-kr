---
title: 'Windows Server 백업을 사용하여 Exchange 데이터 백업 및 복원: Exchange 2013 Help'
TOCTitle: Windows Server 백업을 사용하여 Exchange 데이터 백업 및 복원
ms:assetid: 0fac891a-5713-42b6-afd5-c91b2b88f966
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876851(v=EXCHG.150)
ms:contentKeyID: 50482488
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows Server 백업을 사용하여 Exchange 데이터 백업 및 복원

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange Server 2013 에 대 한 Microsoft의 [기본 아키텍처](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx)Exchange 네이티브 데이터 보호 라고 하는 개념을 활용 합니다. Exchange 네이티브 데이터 보호의 일반 백업을 사용 하지 않고 사서함 데이터를 보호 하기 위해 기본 Exchange 기능에 의존 합니다. 하지만 백업을 만들려는 ExchangeWindows ServerExchange 데이터의 Exchange 인식 VSS 볼륨 섀도 복사본 서비스 기반 백업을 만들 수 있게 하는 백업 (WSB)에 대 한 플러그인 포함 됩니다. Exchange 인식 백업이 되려면 WSB 기능을 설치 해야 합니다.

플러그 인 WSBExchange.exe는 Microsoft Exchange Server Extension for Windows Server Backup(이 서비스의 약식 이름은 WSBExchange)이라는 서비스로 실행됩니다. 이 서비스는 모든 사서함 서버에 자동으로 설치되며 수동으로 시작할 수 있게 구성됩니다. 이 플러그 인에서 WSB를 사용하여 Exchange 인식 VSS 백업을 만들 수 있습니다.

WSB를 사용하여 Exchange 데이터를 백업하기 전에 플러그 인의 다음 기능 및 옵션을 익히는 것이 좋습니다.

  - WSB를 사용한 백업 생성은 볼륨 수준에서 진행되며 응용 프로그램 수준 백업 또는 복원을 수행하는 유일한 방법은 전체 볼륨을 선택하는 것입니다. 데이터베이스 및 로그 스트림을 백업하려면 개별 폴더가 아니라 해당 데이터베이스와 로그가 포함된 전체 볼륨을 백업해야 합니다. 데이터가 포함된 전체 볼륨을 백업하지 않고 데이터만 백업할 수는 없습니다.

  - 백업은 백업 중인 서버에서 로컬로 실행해야 하며, 플러그 인을 사용하여 원격 VSS 백업을 수행할 수 없습니다. WSB 또는 플러그 인의 원격 관리 기능은 없지만 원격 데스크톱 서비스 또는 터미널 서비스를 사용하여 백업을 원격으로 관리할 수도 있습니다.

  - 백업은 로컬 드라이브 또는 원격 네트워크 공유에 만들 수 있습니다.

  - 전체 백업만 수행해야 합니다. Exchange 데이터베이스가 포함된 볼륨 또는 폴더의 VSS 전체 백업이 완료되어야 로그 자르기가 수행됩니다.

  - 데이터를 복원할 때 Exchange 데이터만 복원할 수 있습니다. 이 데이터는 원래 위치나 대체 위치로 복원할 수 있습니다. 데이터를 원래 위치로 복원하는 경우 WSB 및 플러그 인이 복구 프로세스를 자동으로 처리합니다. 여기에는 기존 데이터베이스를 분리하고 복구된 데이터베이스로 로그를 재생하는 작업이 포함됩니다.

  - 복원 프로세스는 Exchange RDB(복구 데이터베이스)를 지원하지 않습니다. RDB를 사용하려는 경우 데이터를 대체 위치로 복원한 다음 복원된 데이터를 해당 위치에서 RDB 폴더 구조로 수동으로 복사하거나 이동해야 합니다.

  - Exchange 데이터를 복원할 때는 백업된 데이터베이스도 모두 함께 복원해야 합니다. 단일 데이터베이스는 복원할 수 없습니다.

  - WSB를 사용하는 경우 완전 복원이 지원되지만 Exchange 서버에서 권장되는 복구 방법은 Exchange 서버를 복구한 다음 데이터를 복원하는 것입니다. 타사 백업 응용 프로그램을 사용하는 경우 백업 응용 프로그램 공급업체로부터 Exchange의 완전 복원 지원을 받을 수 있습니다.

다음 표에서는 WSB가 있는 Exchange 2013에서 사용할 수 있는 백업 및 복구 옵션의 지원 가능성을 보여 줍니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>수행하는 작업</th>
<th>결과</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>전체 서버 백업</p></td>
<td><p>VSS 복사본 백업이 수행되고 서버에서 데이터베이스의 트랜잭션 로그가 잘리지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>사용자 지정 백업을 수행하고 백업할 하나 이상의 볼륨 선택</p></td>
<td><p>VSS 전체 백업을 선택할 수 있으며 성공적으로 백업이 완료되면 선택한 볼륨의 데이터베이스에 대한 트랜잭션 로그가 잘릴 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>사용자 지정 백업을 수행하고 백업할 폴더를 하나 이상 선택</p></td>
<td><p>VSS 전체 백업을 선택할 수 있으며 로그 파일이 잘리지만 응용 프로그램 수준 복원을 옵션으로 사용할 수 없으므로 백업의 복원이 파일 복원으로 제한됩니다.</p></td>
</tr>
</tbody>
</table>


WSB를 사용한 Exchange 백업 단계에 대한 자세한 내용은 [Windows Server 백업을 사용하여 Exchange 백업](use-windows-server-backup-to-back-up-exchange-exchange-2013-help.md)을 참조하세요.

WSB로 수행한 백업에서 데이터를 복원하는 단계에 대한 자세한 내용은 [Windows Server 백업을 사용하여 Exchange 백업 복원](use-windows-server-backup-to-restore-a-backup-of-exchange-exchange-2013-help.md)을 참조하세요.

