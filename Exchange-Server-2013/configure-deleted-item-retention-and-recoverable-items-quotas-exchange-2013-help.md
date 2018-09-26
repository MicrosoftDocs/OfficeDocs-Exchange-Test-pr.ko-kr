---
title: '삭제 된 항목 보존 및 복구 가능한 항목 할당량 구성: Exchange 2013 Help'
TOCTitle: 삭제 된 항목 보존 및 복구 가능한 항목 할당량 구성
ms:assetid: de7d667a-1c93-4364-a4f9-2aa5e3678b12
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee364752(v=EXCHG.150)
ms:contentKeyID: 50556096
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 삭제 된 항목 보존 및 복구 가능한 항목 할당량 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

지운 편지함 기본 폴더 삭제, Shift + Delete 또는 **지운 편지함 폴더 비우기** 동작을 사용 하 여 항목을 삭제 하는 사용자, 항목을 **복구할 수 있는 Items\\Deletions** 폴더로 이동 됩니다. 기간 사서함 데이터베이스 또는 사서함에 대해 구성 된 삭제 된 항목 보존 설정에 따라는 삭제 된 항목이이 폴더에 남아 있을 수는 있습니다. 기본적으로 사서함 데이터베이스가 14 일에 대 한 삭제 된 항목을 유지 하도록 구성 하 고 경고 할당량 및 할당량 복구 가능한 항목 복구 가능한 항목 20 기가바이트 (GB)로 설정 되 고 30GB 각각 합니다.


> [!NOTE]
> 삭제 된 항목 경과 하면, Microsoft Outlook 및 Microsoft OfficeOutlook Web App 에 대 한 보존 시간 전에 사용자는 지운 편지함 복구 기능을 사용 하 여 삭제 된 항목을 복구할 수 있습니다. 이러한 기능에 대 한 자세한 내용은, <A href="https://go.microsoft.com/fwlink/p/?linkid=198206">Outlook</A> 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=198207">Outlook Web App</A>에 대 한 "지운 편지함 복구" 항목을 참조 합니다.



셸을 사용 하 여 삭제 된 항목 보존 설정 및 사서함 또는 사서함 데이터베이스에 대 한 복구 가능한 항목 할당량을 구성할 수 있습니다. 사서함의 원본 위치 유지 또는 소송 보존에 배치 될 때는 설정이 무시 됩니다 삭제 된 항목 보존 대기 합니다.

삭제된 항목 보존, 복구 가능한 항목 폴더, 원본 위치 유지 및 소송 보존에 대한 자세한 내용은 [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "메시징 레코드 관리" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 사서함에 대 한 삭제 된 항목 보존을 구성 합니다.

**EAC를 사용 하 여 사서함에 대 한 삭제 된 항목 보존을 구성 하려면**

1.  **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 사서함을 선택한 다음![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")**편집** 을 클릭 합니다.

3.  사서함 속성 페이지에서 **사서함 사용량**, **기타 옵션** 을 클릭 한 다음 다음 중 하나를 선택합니다
    
      - **사서함 데이터베이스에서 기본 보존 설정을 사용 하 여**    사서함 데이터베이스에 대해 구성 된에서 삭제 된 항목 보존 설정을 사용 하 여이 설정을 사용 합니다.
    
      - **이 사서함에 대 한 설정을 사용자 지정**    사서함에 대 한 삭제 된 항목 보존 설정을 구성 하려면이 설정을 사용 합니다.
        
        **삭제 된 항목 (일)에 대 한 보존**    영구적으로 삭제 되기 전에 사용자가 복구할 수 없는 항목을 삭제 하는 시간 보존 되이 상자를 표시 합니다. 사서함을 만들 때이 값은 사서함 데이터베이스에 대해 구성 된 삭제 된 항목 보존 설정을 기반으로 합니다. 사서함 데이터베이스는 기본적으로 14 일에 대 한 삭제 된 항목을 유지 하도록 구성 됩니다. 이 속성의 값 범위는 0부터 24,855 일에서 시작 됩니다.
    
      - **데이터베이스를 백업할 때까지는 항목을 영구적으로 삭제하지 않음**   사서함이 있는 사서함 데이터베이스가 백업되기 전에는 사서함과 전자 메일 메시지가 삭제되지 않도록 하려면 이 확인란을 선택합니다.

**셸을 사용 하 여 사서함에 대 한 삭제 된 항목 보존을 구성 하려면**

이 예에서는 30 일에 대 한 삭제 된 항목을 유지 하도록 April Stewart의 사서함을 구성 합니다.

```powershell
Set-Mailbox -Identity - "April Stewart" -RetainDeletedItemsFor 30
```

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 셸을 사용 하 여 사서함에 대 한 복구 가능한 항목 할당량을 구성 하려면


> [!NOTE]
> EAC를 사용 하 여 사서함에 대 한 복구 가능한 항목 할당량을 구성 하려면 수는 없습니다.



이 예에서는 12GB의 할당량 및 April Stewart의 사서함에 대 한 15GB의 복구 가능한 항목 할당량 경고를 복구할 수 있는 항목을 구성 합니다.

  ```powershell
  Set-Mailbox -Identity "April Stewart" -RecoverableItemsWarningQuota 12GB -RecoverableItemsQuota 15GB -UseDatabaseQuotaDefaults $false
  ```


> [!NOTE]
> 다른 복구 가능한 항목 할당량 보다 상주 하는 사서함 데이터베이스를 사용 하 여 사서함을 구성 하려면 <CODE>$false</CODE>를 <EM>UseDatabaseQuotaDefaults</EM> 매개 변수를 설정 해야 합니다.



구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 셸을 사용 하 여 사서함 데이터베이스에 대 한 삭제 된 항목 보존을 구성 하려면


> [!NOTE]
> EAC를 사용 하 여 사서함 데이터베이스에 대 한 삭제 된 항목 보존을 구성 하려면 수는 없습니다.



이 예에서는 사서함 데이터베이스 m d b 2에 대 한 일의 삭제 된 항목 보존 기간을 구성 합니다.

```powershell
Set-MailboxDatabase -Identity MDB2 -DeletedItemRetention 10
```

구문과 매개 변수에 대한 자세한 내용은 [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\))를 참조하십시오.

## 셸을 사용 하 여 사서함 데이터베이스에 대 한 복구 가능한 항목 할당량을 구성 하려면


> [!NOTE]
> 사서함 데이터베이스에 대 한 복구 가능한 항목 할당량을 구성 하 여 EAC를 사용할 수 없습니다.



이 예에서는 15GB 할당량과 사서함 데이터베이스 m d b 2에서 20 g B의 복구 가능한 항목 할당량 경고를 복구할 수 있는 항목을 구성 합니다.

```powershell
Set-MailboxDatabase -Identity MDB2 -RecoverableItemsWarningQuota 15GB -RecoverableItemsQuota 20GB
```

구문과 매개 변수에 대한 자세한 내용은 [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\))를 참조하십시오.

