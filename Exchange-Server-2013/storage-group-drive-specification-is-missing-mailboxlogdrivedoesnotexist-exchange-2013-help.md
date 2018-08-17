---
title: '저장소 그룹 드라이브 사양은 missing_MailboxLogDriveDoesNotExist: Exchange 2013 Help'
TOCTitle: 저장소 그룹 드라이브 사양은 missing_MailboxLogDriveDoesNotExist
ms:assetid: fe210f29-60cb-4d34-877e-1356a21dc02a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.mailboxlogdrivedoesnotexist(v=EXCHG.150)
ms:contentKeyID: 50484604
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 저장소 그룹 드라이브 사양은 missing\_MailboxLogDriveDoesNotExist

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft® Exchange Server 2007 재해 복구를 계속할 수 없습니다 재해 복구 저장소 그룹 데이터베이스에 액세스할 수 없습니다 사양이 서버의 이전 설치에 사용 된 드라이브입니다.

Microsoft Exchange 재해 복구 설치는 복원 하는 동안 동일한 저장소 그룹 데이터베이스 드라이브 사양을이 서버에 대해 이전에 사용 되는 사용할 수 있어야 합니다.

이 문제를 해결 하려면 원래 논리 드라이브 구성과 일치 하 고 Microsoft Exchange 재해 복구 설치 프로그램을 다시 실행 하는 드라이브를 구성 합니다.

할당 또는 드라이브 문자를 변경 합니다.

1.  **컴퓨터 관리** **(로컬)를** 엽니다.

2.  콘솔 트리에서 **컴퓨터 관리 (로컬)를** 클릭 하 고 **저장소**, **디스크 관리** 를 차례로 클릭 합니다.

3.  파티션, 논리 드라이브 또는 볼륨을 마우스 오른쪽 단추로 누른 다음 **변경 드라이브 문자 및 경로** 합니다.

4.  다음 절차 중 하나를 사용 합니다.
    
      - 드라이브 문자를 할당 하려면 **추가** 클릭 하 고, 사용 하려는 드라이브 문자를 클릭 한 다음 **확인** 을 클릭 합니다.
    
      - 드라이브 문자를 수정 하려면 클릭 하 여, **변경** 을 클릭를 사용 하 여 원하는 드라이브 문자를 클릭 하 고 **확인** 을 클릭 합니다.

드라이브 문자를 할당 하는 방법에 대 한 자세한 내용은 "할당, 변경 또는 드라이브 문자를 제거"를 참조 하십시오. ([https://go.microsoft.com/fwlink/?LinkId=66764](https://go.microsoft.com/fwlink/?linkid=66764)).

