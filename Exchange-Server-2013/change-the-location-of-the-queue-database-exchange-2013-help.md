---
title: '큐 데이터베이스의 위치를 변경 합니다.: Exchange 2013 Help'
TOCTitle: 큐 데이터베이스의 위치를 변경 합니다.
ms:assetid: f170cb0c-04a9-4fa7-b594-206e3a787e14
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125177(v=EXCHG.150)
ms:contentKeyID: 51407765
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 큐 데이터베이스의 위치를 변경 합니다.

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

*queue* 는 처리의 다음 단계를 시작 하려고 대기 중인 메시지에 대 한 임시 보관 위치입니다. 각 큐에는 특정 순서로 전송 서버에서 처리 하는 메시지의 논리 집합을 나타냅니다.

이전 버전의 Exchange와 같이 Microsoft Exchange Server 2013 큐 메시지 저장소에 대 한 확장 가능한 저장소 엔진 (ESE) 데이터베이스를 사용합니다. 다른 모든 큐는 단일 ESE 데이터베이스에 저장 됩니다. 큐에는 사서함 서버 또는 Edge 전송 서버에만 존재 합니다.

큐 데이터베이스 및 큐 데이터베이스 트랜잭션 로그의 위치는 `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML 응용 프로그램 구성 파일의 키에 의해 제어 됩니다. 이 파일은 Microsoft Exchange Transport service와 연결 합니다. 다음 표에서 각 키를 더 자세히 설명 합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>키</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p>이 키는 큐 데이터베이스 파일의 위치를 지정합니다. 이러한 파일은</p>
<ul>
<li><p>Mail.que</p></li>
<li><p>Trn.chk</p></li>
</ul>
<p>기본 위치는 <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p>이 키는 큐 데이터베이스 트랜잭션 로그 파일의 위치를 지정합니다. 이러한 파일은</p>
<ul>
<li><p>Trn.log</p></li>
<li><p>Trntmp.log</p></li>
<li><p>Trn<em>nnn</em>.log</p></li>
<li><p>Trnres00001.jrs</p></li>
<li><p>Trnres00002.jrs</p></li>
<li><p>Temp.edb</p></li>
</ul>
<p>삭제는 Microsoft Exchange Transport service를 시작 하는 경우 큐 데이터베이스 스키마를 확인 하는데 note 합니다. 하지만 삭제 하지는 않습니다 트랜잭션 로그 파일을 트랜잭션 로그 파일와 같은 위치에 저장 됩니다.</p>
<p>기본 위치는 <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>합니다.</p></td>
</tr>
</tbody>
</table>


## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분.

  - 이 항목의 절차에는 Exchange 권한이 적용되지 않습니다. 이 절차는 Exchange Server의 운영 체제에서 수행됩니다.

  - Microsoft Exchange Transport service를 다시 시작 하거나 중지 하는 경우에 서버에서 메일 흐름 중단 됩니다.

  - 큐 데이터베이스 또는 트랜잭션 로그의 위치를 변경 하면 기존 큐 데이터베이스 및 트랜잭션 로그 파일 이동 되지 않습니다. 새 큐 데이터베이스 및 트랜잭션 로그를 새 새 위치에 만들어집니다. 기존 파일은 이전 위치에 그대로 유지 합니다. 사용 더이상는 합니다. 기존 큐 데이터베이스 또는 트랜잭션 로그 파일의 새 위치를 다시 사용 하려는 경우 Microsoft Exchange Transport 서비스를 중지 한 후 하지만 서비스를 시작 하기 전에 기존 파일을 새 위치로 이동 해야 합니다.

  - 큐 데이터베이스 또는 트랜잭션 로그에 대 한 대상 폴더가 존재 하지 않는 경우 만들어집니다 하면 상위 폴더에 다음 권한이 적용 하는 경우:
    
      - 네트워크 서비스: 모든 권한
    
      - 시스템: 모든 권한
    
      - 관리자: 모든 권한

  - Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 파일 또는 사서함 서버의 EdgeTransport.exe.config 파일)에 설정하는 사용자 지정된 모든 서버 단위 설정은 Exchange CU(누적 업데이트)를 설치하면 덮어쓰게 됩니다. 설치 후 서버를 쉽게 다시 구성할 수 있도록 이 정보를 저장했는지 확인하세요. 이러한 설정은 Exchange CU를 설치한 후에 다시 구성해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## 명령 프롬프트를 사용 하 여 새 큐 데이터베이스를 만들 수 및 새 위치에서 트랜잭션 로그

1.  큐 데이터베이스 및 트랜잭션 로그를 유지 하려면 폴더를 만듭니다. 폴더에 올바른 사용 권한이 적용 되는 있는지 확인 하십시오.

2.  명령 프롬프트 창에서 다음 명령을 실행 하 여 EdgeTransport.exe.config 파일을 메모장에서에서 엽니다.
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

3.  `<appSettings>` 섹션에서 다음 키를 수정 합니다.
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    예, D:\\Queue\\QueueDB 및 D:\\Queue\\QueueLogs의 새 트랜잭션 로그에 새 큐 데이터베이스를 만들려면 다음 값을 사용 합니다.
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  작업을 마친 후 저장하고 EdgeTransport.exe.config 파일을 닫습니다.

5.  다음 명령을 실행하여 Microsoft Exchange Transport Service를 다시 시작합니다.
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 작동 여부는 어떻게 확인합니까?

성공적으로 만들어졌는지 새 큐 데이터베이스 및 트랜잭션 로그를 새 새 위치를 확인 하려면 다음을 수행 합니다.

1.  Mail.que 및 Trn.chk 존재 하 고 새 위치에서 새 데이터베이스 파일을 확인 합니다.

2.  Trn.log "," Trntmp.log "," Trnres00001.jrs "," Trnres00002.jrs, "및" 삭제 파일이 새 위치에 있는 새 트랜잭션 로그 파일을 확인 합니다.

3.  Microsoft Exchange Transport service가 시작 된 후 이전 위치에서 이전 큐 데이터베이스 및 트랜잭션 로그 파일을 삭제할 수 없습니다, 하는 경우 이러한 파일은 더이상 사용 하지 않는 합니다.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

맨 위로 이동

## 명령 프롬프트를 사용 하 여 기존 큐 데이터베이스 및 트랜잭션 로그를 새 위치로 이동 하려면

재해 복구 시나리오를 Microsoft Exchange Transport service 되지 않은 올바르게 종료 또는 하드 디스크 드라이브 오류 시 복원 하 고 기존 큐 데이터베이스와 기존 트랜잭션 로그 위치를 변경 해야 합니다.

일반적인 상황에서 기존 트랜잭션 로그를 다시 사용 해야할 하면 안됩니다. 모든 커밋되지 않은 트랜잭션 로그 항목을 큐 데이터베이스에 기록 하는 Microsoft Exchange Transport 서비스의 일반적인를 종료 합니다. 및 순환 로깅을 사용 되므로 이전에 커밋된 데이터베이스 변경 사항을 포함 하는 트랜잭션 로그 보존 되지 않습니다.

다음 절차를 사용 하 여 새 위치에서 기존 큐 데이터베이스 및 트랜잭션 로그를 이동 하려면:

1.  큐 데이터베이스 및 트랜잭션 로그를 유지 하려면 폴더를 만듭니다. 폴더에 올바른 사용 권한이 적용 되는 있는지 확인 하십시오.

2.  명령 프롬프트 창에서 다음 명령을 실행 하 여 EdgeTransport.exe.config 파일을 메모장에서에서 엽니다.
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

3.  `<appSettings>` 섹션에서 다음 키를 수정 합니다.
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    예, D:\\Queue\\QueueDB 및 D:\\Queue\\QueueLogs 트랜잭션 로그를 큐 데이터베이스의 위치를 변경 하려면 다음 값을 사용 합니다.
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  작업을 마친 후 저장하고 EdgeTransport.exe.config 파일을 닫습니다.

5.  다음 명령을 실행 하 여 Microsoft Exchange Transport service를 중지 합니다.
    
        net stop MSExchangeTransport

6.  원래 위치에서 Mail.que 및 Trn.chk 기존 데이터베이스 파일을 새 위치로 이동 합니다.

7.  이동 기존 트랜잭션 로그를 새 위치로 이전 위치에서 Trn.log, Trntmp.log, Trn*nnnnn*.log, Trnres00001.jrs, Trnres00002.jrs, 및 삭제를 파일입니다.

8.  다음 명령을 실행 하 여 Microsoft Exchange Transport service를 시작 합니다.
    
        net start MSExchangeTransport

## 작동 여부는 어떻게 확인합니까?

를 기존 큐 데이터베이스 및 트랜잭션 로그를 새 위치로 이동 되었는지 확인 하려면 다음을 수행 합니다.

1.  Mail.que 및 Trn.chk 새 위치에 있는 큐 데이터베이스 파일을 확인 합니다.

2.  Trn.log "," Trntmp.log "," Trnres00001.jrs "," Trnres00002.jrs, "및" 삭제 파일이 새 위치에 있는 트랜잭션 로그 파일을 확인 합니다.

3.  원래 위치에 없는 큐 데이터베이스 또는 트랜잭션 로그 파일이 남아 있지 확인 합니다.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

맨 위로 이동

