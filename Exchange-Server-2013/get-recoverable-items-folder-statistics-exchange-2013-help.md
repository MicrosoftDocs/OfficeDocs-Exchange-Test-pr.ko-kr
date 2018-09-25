---
title: '복구 가능한 항목 폴더 통계 가져오기: Exchange 2013 Help'
TOCTitle: 복구 가능한 항목 폴더 통계 가져오기
ms:assetid: dee77958-ee87-4908-85e4-ad053bacd8b0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff714343(v=EXCHG.150)
ms:contentKeyID: 52058125
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 복구 가능한 항목 폴더 통계 가져오기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-22_

복구 가능한 항목 폴더에는 Microsoft Outlook 및 Microsoft OfficeOutlook Web App 사용자 또는 사서함 도우미에 의해 삭제 한 항목이 들어 있습니다. 기간 사서함 데이터베이스 또는 사서함에 대해 구성 된 삭제 된 항목 보존 설정에 따라는 삭제 된 항목이이 폴더에 남아 있을 수는 있습니다. 기본적으로 사서함 데이터베이스가 14 일에 대 한 삭제 된 항목을 유지 하도록 구성 하 고 복구 가능한 항목 경고 보내기 할당량 및 복구 가능한 항목 할당량 20 기가바이트 (GB)로 설정 되 고 30GB 각각 합니다. 그러나 원본 위치 유지 또는 소송 보존으로 설정 된 사서함에 대 한 활성화 된 경우 복구 가능한 항목 폴더에 누적 될 수 있습니다 지정된 된 보존 기간 이외의 항목을 삭제 및 수정 된 사서함 항목의 다양 한 버전을 유지할 수도 있습니다.

복구 가능한 항목 폴더의 복구 가능한 항목 경고 할당량에 도달 하면 경고 이벤트를 응용 프로그램 이벤트 로그에 기록 됩니다. 사서함을 소송 보존에 없는 경우 fifo (처음) 별로에서 처음에 다음이 항목이 제거 됩니다. 그러나 사서함이 소송 보존 대기 상태인 경우 사서함 되지 비워지고 복구 가능한 항목 할당량에 도달 시 사서함 기능 영향을 받는 합니다.

따라서이 사서함 복구 가능한 항목 할당량에 도달할 때 생성 된 경고에 대 한 이벤트 로그를 모니터링 하는 것이 중요 합니다. 보고서 통계에이 절차를 사용 하 여 특히 소송 보존에 배치 하는 사서함에 대 한 복구 가능한 항목 폴더에 대 한 수도 있습니다.

자세한 내용은 다음 항목을 참조 합니다.

  - [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)

  - [원본 위치 유지 및 소송 보존](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-and-litigation-holds)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "사서함 폴더" 항목.

  - Exchange 관리 센터 (EAC)를 사용 하 여 사서함에 대 한 복구 가능한 항목 폴더 통계를 가져올 수 없습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

## 무슨 작업을 하고 싶으십니까?

## 사서함에 대 한 복구 가능한 항목 폴더 통계를 가져오려면

이 예제에서는 Soumya Singhi 복구 가능한 항목 폴더에 대 한 폴더 통계를 가져오고 목록 형식으로 출력을 표시 합니다.

```powershell
Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-List
```

이 예제에서는 Soumya Singhi 복구 가능한 항목 폴더에 대 한 폴더 통계를 가져오고 폴더 및 표 형식에서 폴더 크기의 폴더 이름, 폴더 경로, 항목 수를 표시 하는 합니다.

```powershell
Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-Table Name,FolderPath,ItemsInFolder,FolderAndSubfolderSize
```

자세한 구문 및 매개 변수 정보에 대 한 [Get-MailboxFolderStatistics](https://technet.microsoft.com/ko-kr/library/aa996762\(v=exchg.150\))를 참조 하십시오.

## 소송 보존으로 설정에 있는 모든 사서함에 대 한 복구 가능한 항목 폴더 통계를 가져오려면

이 예제에서는 소송 보존에 배치 하는 모든 사서함의 목록을 검색 하 고 복구 가능한 항목 폴더에 대 한 사서함 폴더 통계와 각 사서함에 대 한 하위 폴더를 검색 합니다. **Identity** (사서함 폴더 id) 및 **FolderAndSubfolderSize** 속성을 테이블 형식으로 표시 됩니다.

```powershell
Get-Mailbox -ResultSize Unlimited -Filter {LitigationHoldEnabled -eq $true} | Get-MailboxFolderStatistics | Format-Table Identity,FolderAndSubfolderSize
```

자세한 구문 및 매개 변수 정보에 대 한 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) 및 [Get-MailboxFolderStatistics](https://technet.microsoft.com/ko-kr/library/aa996762\(v=exchg.150\))를 참조 하십시오.

## 사서함에 대 한 복구 가능한 항목 할당량 가져오기

할당량 및 사용자 사서함에 대 한 복구 가능한 항목 폴더에 대 한 경고 할당량을 표시 하는이 예제입니다. 또한이 예제에서는 사서함에 소송 보존 또는 In-place Hold 배치 되는 여부에 대 한 정보를 검색 합니다.

```powershell
Get-Mailbox -Identity <identity of mailbox> | Format-List RecoverableItems*,LitigationHoldEnabled,InPlaceHolds
```

조직에서 할당량 및 모든 사용자 사서함에 대 한 복구 가능한 항목 폴더에 대 한 경고 할당량을 표시 하는이 예제입니다. 또한이 예제에서는 보류 정보를 검색 합니다.

```powershell
Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Format-List Name,RecoverableItems*,LitigationHoldEnabled,InPlaceHolds
```

