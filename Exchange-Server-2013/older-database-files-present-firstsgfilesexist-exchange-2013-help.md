---
title: '이전 데이터베이스 파일 present_FirstSGFilesExist: Exchange 2013 Help'
TOCTitle: 이전 데이터베이스 파일 present_FirstSGFilesExist
ms:assetid: 907faeb8-1c6d-49fc-95a1-417f415a9d79
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.firstsgfilesexist(v=EXCHG.150)
ms:contentKeyID: 50483643
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 이전 데이터베이스 파일 present\_FirstSGFilesExist

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

대상 설치 경로에서 기존 Microsoft Exchange 데이터베이스 파일을 검색 하기 때문에 Microsoft® Exchange Server 2007 설치를 계속할 수 없습니다.

Exchange 2007 설치 프로그램을 사용 하려면 대상 설치 경로 Microsoft Exchange 데이터베이스 파일의 비어 있어야 합니다.

이 문제를 해결 하려면 대상 설치 경로에서 모든 기존 파일을 제거 하 고 설치 프로그램을 다시 실행 하십시오.

대상 설치 경로에서 기존 Exchange Server 데이터베이스 파일을 삭제 하려면

1.  내 컴퓨터 또는 Windows 탐색기에서 대상 설치 경로를 찾습니다.
    

    > [!NOTE]
    > 기본적으로 데이터베이스 파일에 있습니다.<BR>&lt; systemDrive &gt;: \program Server\Mailbox\First 저장소 그룹입니다.



2.  제거 될 파일을 마우스 오른쪽 단추로 클릭 하 고 **삭제** 를 선택 합니다.

3.  **파일 삭제 확인** 대화 상자에서 **예** 를 클릭 합니다.

4.  대상 설치 경로 있는 모든 파일에 대 한 2와 3 단계를 반복 합니다.

