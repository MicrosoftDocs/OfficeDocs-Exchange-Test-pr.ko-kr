---
title: '공용 폴더 및 공용 폴더 항목에 대 한 통계 보기: Exchange 2013 Help'
TOCTitle: 공용 폴더 및 공용 폴더 항목에 대 한 통계 보기
ms:assetid: 4e412710-9a74-4649-ab01-502e969a7eda
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997949(v=EXCHG.150)
ms:contentKeyID: 50483098
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공용 폴더 및 공용 폴더 항목에 대 한 통계 보기

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-14_

이 항목에서는 표시 이름, 만든 시간, 사용자가 마지막으로 수정한 시간, 사용자가 마지막으로 액세스한 시간, 항목 크기 등 공용 폴더에 대한 통계를 가져오는 방법을 설명합니다. 이 정보를 사용하여 공용 폴더의 삭제 또는 보존에 대해 결정할 수 있습니다.


> [!NOTE]
> EAC(Exchange 관리 센터)에서 <STRONG>공용 폴더</STRONG> &gt; <STRONG>편집</STRONG><IMG title="편집 아이콘" alt="편집 아이콘" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif"> &gt; <STRONG>사서함 사용량</STRONG>으로 이동하여 공용 폴더의 일부 할당량 및 사용량 정보를 볼 수 있습니다. 단, 이 정보는 완전하지 않으므로 셸을 사용하여 공용 폴더 통계를 확인하는 것이 좋습니다.



공용 폴더 관리와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [Office 365 및 Exchange Online의 절차에서는 공용 폴더](https://technet.microsoft.com/ko-kr/library/jj966272\(v=exchg.150\))를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md) 항목의 "공용 폴더" 항목

  - 공용 폴더 통계를 검색하는 데에는 EAC를 사용할 수 없습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 공용 폴더 통계 가져오기

다음은 목록을 만드는 파이프된 명령으로 공용 폴더 Marketing에 대한 통계를 반환하는 예입니다.

    Get-PublicFolderStatistics -Identity \Marketing | Format-List


> [!NOTE]
> <EM>Identity</EM> 매개 변수의 값에는 공용 폴더 경로가 포함되어야 합니다. 예를 들어 Marketing이라는 공용 폴더가 Business라는 상위 폴더 아래에 있는 경우에는 <CODE>\Business\Marketing</CODE>



구문과 매개 변수에 대한 자세한 내용은 [Get-PublicFolderStatistics](https://technet.microsoft.com/ko-kr/library/aa998663\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 공용 폴더 항목 통계 보기

공용 폴더 내의 항목에 대해 볼 수 있는 정보는 다음과 같습니다.

  - 항목 유형

  - 제목

  - 사용자가 마지막으로 수정한 시간

  - 사용자가 마지막으로 액세스한 시간

  - 만든 시간

  - 첨부 파일

  - 메시지 크기

이 정보를 기반으로 삭제할 공용 폴더를 결정하는 등 공용 폴더에 대해 수행할 작업을 결정할 수 있습니다. 예를 들어 2년 이상 공용 폴더 항목이 액세스되지 않은 경우 폴더를 삭제하거나 문서 저장소로 사용되는 공용 폴더를 다른 클라이언트 액세스 응용 프로그램으로 변환할 수 있습니다.

이 예에서는 \\Marketing\\2013 경로에 있는 공용 폴더 Pamphlets의 모든 항목에 대한 기본 통계를 반환합니다. 기본 정보에는 항목 ID, 만든 시간 및 주제가 포함됩니다.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2013\Pamphlets"

이 예에서는 공용 폴더 Pamphlets의 항목에 대한 주제, 마지막으로 수정한 시간, 만든 시간, 첨부 파일, 메시지 크기, 항목 유형 등 추가 정보를 반환합니다. 여기에는 목록의 형식을 지정할 파이프된 명령이 포함됩니다.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2010\Pamphlets" | Format-List

구문과 매개 변수에 대한 자세한 내용은 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/ko-kr/library/ee332344\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 Get-PublicFolderItemStatistics cmdlet의 출력을 .csv 파일로 내보내기

이 예에서는 cmdlet의 출력을 PFItemStats.csv 파일로 내보냅니다. 이 .csv 파일에는 공용 폴더 \\Marketing\\Reports 내의 모든 항목에 대한 다음 정보가 들어 있습니다.

  - 메시지 제목(`Subject`)

  - 항목을 마지막으로 수정한 날짜 및 시간(`LastModificationTime`)

  - 항목에 첨부 파일이 있는지 여부(`HasAttachments`)

  - 항목 유형(`ItemType)`)

  - 항목 크기(`MessageSize`)

<!-- end list -->

    Get-PublicFolderItemStatistics -Identity "\Marketing\Reports" | Select Subject,LastModificationTime,HasAttachments,ItemType,MessageSize | Export-CSV C:\PFItemStats.csv

구문과 매개 변수에 대한 자세한 내용은 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/ko-kr/library/ee332344\(v=exchg.150\))를 참조하십시오.

