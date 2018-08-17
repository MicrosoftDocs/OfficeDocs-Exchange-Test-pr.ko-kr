---
title: '검색 카탈로그 다시 시드: Exchange 2013 Help'
TOCTitle: 검색 카탈로그 다시 시드
ms:assetid: 9d873bd4-0422-4975-b5e2-82a347479115
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633475(v=EXCHG.150)
ms:contentKeyID: 52058108
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 검색 카탈로그 다시 시드

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

사서함 데이터베이스 복사본의 콘텐츠 인덱스 카탈로그가 손상된 경우 카탈로그를 다시 시드해야 할 수 있습니다. 손상된 콘텐츠 인덱스는 응용 프로그램 이벤트 로그에서 다음 이벤트로 표시됩니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>이벤트 ID</th>
<th>수준</th>
<th>원본</th>
<th>세부 정보</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>123</p></td>
<td><p>오류</p></td>
<td><p>ExchangeStoreDB</p></td>
<td><p>&lt;<em>타임스탬프</em>&gt;에 이 서버에 있는 Microsoft Exchange 정보 저장소 데이터베이스 &lt;<em>ID</em>&gt; 복사본에서 손상된 검색 카탈로그가 발견되었습니다. 오류에 대한 자세한 내용은 서버의 이벤트 로그에서 다른 &quot;ExchangeStoreDb&quot; 및 &quot;MSExchange Search Indexer&quot; 이벤트를 참조하십시오. 'Update-MailboxDatabaseCopy' 작업을 통해 카탈로그를 다시 시드하는 것이 좋습니다.</p></td>
</tr>
</tbody>
</table>


사서함 데이터베이스 복사본이 DAG(데이터베이스 가용성 그룹)에 속하는 서버에 있는 경우 다른 DAG 구성원에서 콘텐츠 인덱스 카탈로그를 다시 시드할 수 있습니다.

사서함 데이터베이스 복사본이 유일한 복사본인 경우 새 콘텐츠 인덱스 카탈로그를 수동으로 만들어야 합니다.

Exchange 검색과 관련된 다른 관리 작업에 대한 자세한 내용은 [Exchange 검색 절차](exchange-search-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분 다시 시드하는 데 실제로 소요되는 시간은 다시 시드 중인 콘텐츠 인덱스 카탈로그 크기에 따라 다를 수 있습니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "Exchange 검색" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

## 사서함 데이터베이스가 DAG에 속할 경우 콘텐츠 인덱스 다시 시드

사서함 데이터베이스가 DAG에 속하는 서버에 있는 경우 다음 절차 중 하나를 사용합니다.

## 모든 원본에서 콘텐츠 인덱스 카탈로그 다시 시드

이 예에서는 데이터베이스 복사본이 있는 DAG의 모든 원본 서버의 사서함 서버 MBX1에서 데이터베이스 복사본 DB1에 대한 콘텐츠 인덱스 카탈로그를 다시 시드합니다.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

구문과 매개 변수에 대한 자세한 내용은 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd335201\(v=exchg.150\))를 참조하십시오.

## 특정 원본에서 콘텐츠 인덱스 카탈로그 다시 시드

이 예에서는 데이터베이스 복사본이 있는 사서함 서버 MBX2에서 사서함 서버 MBX1의 데이터베이스 복사본 DB1에 대한 콘텐츠 인덱스 카탈로그를 다시 시드합니다.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2 -CatalogOnly

구문과 매개 변수에 대한 자세한 내용은 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd335201\(v=exchg.150\))를 참조하십시오.

## 사서함 데이터베이스의 복사본이 하나만 있는 경우 콘텐츠 인덱스 카탈로그 다시 시드

사서함 데이터베이스 복사본이 하나만 있는 경우 콘텐츠 인덱스 카탈로그를 다시 만들어 검색 카탈로그를 수동으로 다시 시드해야 합니다.

1.  다음 명령을 실행하여 Microsoft Exchange Search 및 Microsoft Exchange Search Host Controller 서비스를 중지합니다.
    
    ```
    Stop-Service MSExchangeFastSearch
    ```

    ```
    Stop-Service HostControllerService
    ```

2.  Exchange 콘텐츠 인덱스 카탈로그가 포함된 폴더를 삭제하거나 이동하거나 이름을 바꿉니다. 이 폴더의 이름은 `%ExchangeInstallPath\Mailbox\<name of mailbox database>_Catalog\<GUID>12.1.Single`입니다. 예를 들어 폴더 `C:\Program Files\Microsoft\Exchange Server\V15\Mailbox\Mailbox Database 0657134726_Catalog\F0627A72-9F1D-494A-839A-D7C915C279DB12.1.Single_OLD`의 이름을 바꿀 수 있습니다.
    

    > [!NOTE]
    > 이 폴더를 삭제하면 추가 디스크 공간을 사용할 수 있게 됩니다. 또한 문제 해결을 위해 폴더 이름을 바꾸거나 이동하여 보관할 수도 있습니다.



3.  다음 명령을 실행하여 Microsoft Exchange Search 및 Microsoft Exchange Search Host Controller 서비스를 다시 시작합니다.
    
    ```
    Start-Service MSExchangeFastSearch
    ```

    ```
    Start-Service HostControllerService
    ```
    
    이러한 서비스를 다시 시작하면 Exchange Search가 콘텐츠 인덱스 카탈로그를 다시 작성합니다.

## 작동 여부는 어떻게 확인합니까?

Exchange Search에서 콘텐츠 인덱스 카탈로그를 다시 시드하려면 다소 시간이 걸릴 수 있습니다. 다음 명령을 실행하여 다시 시드 프로세스의 상태를 표시합니다.

    Get-MailboxDatabaseCopyStatus | FL Name,*Index*

검색 카탈로그의 다시 시드가 진행 중이면 *ContentIndexState* 속성의 값은 **Crawling**입니다. 다시 시드가 완료되면 이 값은 **Healthy**로 바뀝니다.

