---
title: 'Windows Server 백업을 사용하여 Exchange 백업: Exchange 2013 Help'
TOCTitle: Windows Server 백업을 사용하여 Exchange 백업
ms:assetid: 188a8291-0a41-4ca2-b6d2-94242e2b1ffc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876854(v=EXCHG.150)
ms:contentKeyID: 50482566
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows Server 백업을 사용하여 Exchange 백업

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2014-06-18_

Windows Server 백업을 사용하여 Exchange 데이터베이스를 백업하고 복원할 수 있습니다. Exchange에는 Exchange 데이터의 VSS(볼륨 섀도 복사본 서비스) 기반 백업을 만들 수 있는 Windows Server 백업용 플러그 인이 포함됩니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 + 데이터 백업에 걸리는 시간

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 복구" 항목

  - Windows Server 백업 기능은 로컬 컴퓨터에 설치되어 있어야 합니다.

  - 백업 작업이 진행되는 동안, Exchange 데이터 파일의 상태가 좋아 복구에 사용할 수 있는 것인지를 검증하기 위해 일관성 확인이 실행됩니다. 일관성 확인이 성공하면 Exchange 데이터는 해당 백업에서의 복구에 사용할 수 있습니다. 일관성 확인이 실패하면 해당 Exchange 데이터는 복구에 사용할 수 없습니다. Windows Server 백업에서는 백업용으로 만든 스냅숏에 대한 일관성 검사를 실행합니다. 따라서 파일을 스냅숏에서 백업 미디어로 복사하기 전에 백업에 대한 일관성이 알려지고 일관성 검사 결과를 사용자에게 알립니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Windows Server 백업을 사용하여 Exchange 백업

1.  Windows Server 백업을 시작합니다.

2.  <strong>로컬 백업</strong>을 선택합니다.

3.  작업 창에서 <strong>한 번 백업...</strong>을 클릭하여 한 번 백업 마법사를 시작합니다.

4.  <strong>백업 옵션</strong> 페이지에서 <strong>다른 옵션</strong>을 선택하고 <strong>다음</strong>을 클릭합니다.

5.  <strong>백업 구성 선택</strong> 페이지에서 <strong>사용자 지정</strong>을 선택하고 <strong>다음</strong>을 클릭합니다.

6.  <strong>백업할 항목 선택</strong> 페이지에서 <strong>항목 추가</strong>를 클릭하여 백업할 볼륨을 선택하고 <strong>확인</strong>을 클릭합니다.
    

    > [!NOTE]
    > 개별 폴더가 아닌 볼륨을 선택합니다. 응용 프로그램 수준 백업 또는 복원을 수행하는 유일한 방법은 전체 볼륨을 선택하는 것입니다.



7.  <strong>고급 설정</strong>을 클릭합니다. <strong>제외</strong> 탭에서 <strong>제외 추가</strong>를 클릭하여 백업에서 제외할 파일 또는 파일 형식을 추가합니다.
    

    > [!NOTE]
    > 기본적으로, 운영 체제 구성 요소 또는 응용 프로그램이 있는 볼륨은 백업에 포함되며 제외할 수 없습니다.



8.  <strong>VSS 설정 탭</strong>에서 <strong>VSS 전체 백업</strong>을 선택한 다음 <strong>확인</strong>을 클릭하고 <strong>다음</strong>을 클릭합니다.

9.  <strong>대상 형식 지정</strong> 페이지에서 백업을 저장할 위치를 선택하고 <strong>다음</strong>을 클릭합니다.
    
      - <strong>로컬 드라이브</strong>를 선택하면 <strong>백업 대상 선택</strong> 페이지가 표시됩니다. <strong>백업 대상</strong> 드롭다운에서 옵션을 선택하고 <strong>다음</strong>을 클릭합니다.
    
      - <strong>원격 공유 폴더</strong>를 선택하면 <strong>원격 폴더 지정</strong> 페이지가 나타납니다. 백업 파일의 UNC 경로를 지정하고 액세스 제어 설정을 구성합니다. 특정 계정을 통해서만 백업에 액세스할 수 있게 하려면 <strong>상속 안 함</strong>을 선택합니다. 원격 폴더를 호스트하는 컴퓨터에 대한 쓰기 권한이 있는 계정의 사용자 이름과 암호를 입력하고 <strong>확인</strong>을 클릭합니다. 또는 원격 폴더에 대한 액세스 권한이 있는 모든 사용자가 백업에 액세스할 수 있도록 하려면 <strong>상속</strong>을 선택합니다. <strong>다음</strong>을 클릭합니다.

10. <strong>확인</strong> 페이지에서 백업 설정을 검토하고 <strong>백업</strong>을 클릭합니다.

11. <strong>백업 진행률</strong> 페이지에서 백업 작업의 상태와 진행률을 확인할 수 있습니다.

12. 언제든지 <strong>닫기</strong>를 클릭하여 <strong>백업 진행률</strong> 페이지를 끝낼 수 있습니다. 진행 중인 백업은 백그라운드에서 계속 실행됩니다.

## 작동 여부는 어떻게 확인합니까?

데이터 백업이 성공적으로 완료되었는지 확인하려면 다음을 수행하세요.

  - Windows Server 백업이 실행된 서버에서 마지막 백업 상태가 "성공"으로 표시됩니다. Windows Server 백업 로그를 확인하여 백업이 성공적으로 완료되었는지 확인할 수도 있습니다.

  - 이벤트 뷰어를 열고 응용 프로그램 이벤트 로그에 백업 완료 이벤트가 기록되었는지 확인합니다.

  - Exchange 관리 셸에서 다음 명령을 실행하여 선택한 볼륨의 각 데이터베이스가 성공적으로 백업되었는지 확인합니다.
    
    ```powershell
    Get-MailboxDatabase -Server <ServerName> -Status | fl Name,*FullBackup
    ```    
    데이터베이스의 *SnapshotLastFullBackup* 및 *LastFullBackup* 속성은 마지막으로 성공한 백업이 수행된 시기와 VSS 전체 백업이었는지 여부를 나타냅니다.

