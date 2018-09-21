---
title: '사서함에 대 한 저장소 할당량 구성: Exchange 2013 Help'
TOCTitle: 사서함에 대 한 저장소 할당량 구성
ms:assetid: 5f5fe292-c80e-4a0b-b3e6-e193ea5171d0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998353(v=EXCHG.150)
ms:contentKeyID: 50555998
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 대 한 저장소 할당량 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-07-07_

**요약:**  EAC 또는 셸을 사용 하 여 특정 사서함에 대 한 저장소 할당량을 설정 합니다.

저장소 할당량을 사용 하면 사서함의 크기를 제어 하 고 사서함 데이터베이스의 증가 관리할 수 있습니다. 사서함에 도달 또는 지정 된 저장소 할당량을 초과 하는 경우 Exchange 사서함 소유자 설명이 포함 된 알림을 보냅니다.


> [!NOTE]
> 저장소 할당량 <CODE>Get-MailboxStatistics</CODE>cmdlet 실행 하는 경우 <CODE>TotalItemSize</CODE> 속성 의해 정의 되는 지정 된 사서함 크기에 대해 적용 됩니다. 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/bb124612(v=exchg.150)">Get-MailboxStatistics</A>을 참조 하십시오.



저장소 할당량은 일반적으로 데이터베이스당 별로 구성 됩니다. 즉, 해당 데이터베이스에 있는 모든 사서함에 사서함 데이터베이스에 대해 구성 된 할당량을 적용 합니다. 데이터베이스 당 사서함 설정을 관리 하는 방법에 대 한 자세한 내용은 [Exchange 2013의 사서함 데이터베이스를 관리 합니다.](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)을 참조 하십시오.

이 항목에서는 사서함 데이터베이스의 저장소 설정을 사용 하는 대신 특정 사서함에 대 한 저장소 설정을 사용자 지정 하는 방법을 보여줍니다. 사용자 사서함에 관련 된 추가 관리 작업을 [사용자 사서함 관리](https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 사서함에 대 한 저장소 할당량을 구성 하려면

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 저장소 할당량을 변경 하려는 사서함을 클릭 하 고![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")**편집** 을 클릭 합니다.

3.  사서함 속성 페이지에서 **사서함 사용량** 를 클릭 한 다음 **기타 옵션** 을 클릭 합니다.

4.  **이 사서함에 대 한 설정을 사용자 지정** 을 클릭 하 고 다음 상자를 구성 합니다. 저장소 할당량 설정에 대 한 값 범위는 0부터 2047 기가바이트 (GB)에서 시작 됩니다.
    
      - **다음 크기(GB)일 때 경고 표시**   이 상자에는 사용자에게 경고가 표시되기까지의 최대 저장소 제한이 표시됩니다. 사서함 크기가 지정된 값에 도달하거나 초과하면 사용자에게 경고 메시지가 전송됩니다.
        

        > [!IMPORTANT]
        > 이 설정의 값은 <STRONG>보내기 금지</STRONG> 할당량에 지정 된 값의 50%를 초과 하지 않는 한 사용자에 게 <STRONG>경고 보내기</STRONG> 할당량와 관련 된 메시지를 보낼 수 없습니다. 예, 8 MB를 <STRONG>보내기 금지</STRONG> 할당량을 설정 하는 경우 <STRONG>경고 보내기</STRONG> 할당량 최소 4MB를 설정 해야 합니다. 를 지정 하지 않으면 <STRONG>경고 보내기</STRONG> 할당량 메시지를 보낼 수 없습니다.

    
      - **다음 크기(GB)일 때 보내기 금지**   이 상자에는 사서함에 대한 *보내기 금지* 제한이 표시됩니다. 사서함 크기가 지정된 제한에 도달하거나 초과하면 사용자가 새 메시지를 보내지 못하도록 설정되며 설명 형식의 오류 메시지가 표시됩니다.
    
      - **다음 크기(GB)일 때 보내기 및 받기 금지**   이 상자에는 사서함에 대한 *보내기 및 받기 금지* 제한이 표시됩니다. 사서함 크기가 지정된 제한에 도달하거나 초과하면 사서함 사용자가 새 메시지를 보내지 못하도록 설정되며 새 메시지가 사서함에 배달되지 않습니다. 사서함으로 전송된 모든 메시지가 설명이 포함된 오류 메시지와 함께 보낸 사람에게 반환됩니다.

5.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용 하 여 사서함에 대 한 저장소 할당량을 구성 하려면

문제 경고를 설정 하는이 예제, 보내기, 금지 하 고 보내기 및 받기 금지 할당량 24.5 g B, 24.75 g B 및 25GB Joe Healy의 사서함에 대 한 각각 합니다.


> [!NOTE]
> 사서함에 대 한 사용자 지정 설정을 사용 하는 대신 사서함 데이터베이스의 기본값은 되도록 <CODE>$false</CODE>를 <EM>UseDatabaseQuotaDefaults</EM> 매개 변수를 설정 해야 합니다.



    Set-Mailbox -Identity "Joe Healy" -IssueWarningQuota 24.5gb -ProhibitSendQuota 24.75gb -ProhibitSendReceiveQuota 25gb -UseDatabaseQuotaDefaults $false

문제 경고를 설정 하는이 예제, 보내기, 금지 하 고 보내기 및 받기 금지 900 메가바이트 (MB), 950 MB Ayla Kol의 사서함에 대 한 할당량 및 1GB 각각, 사용자 지정 설정을 사용 하 여 사서함을 구성 합니다.

    Set-Mailbox -Identity "Ayla Kol" -IssueWarningQuota 900mb -ProhibitSendQuota 950mb -ProhibitSendReceiveQuota 1gb -UseDatabaseQuotaDefaults $false

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사서함에 대 한 저장소 할당량을 성공적으로 설정 했을 때를 확인 하려면 다음 중 하나를 수행 합니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 저장소 할당량을 확인 하려는 사서함을 클릭 하 고![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")**편집** 을 클릭 합니다.

3.  사서함 속성 페이지에서 **사서함 사용량** 를 클릭 한 다음 **기타 옵션** 을 클릭 합니다.

4.  **이 사서함에 대 한 설정을 사용자 지정** 을 선택 했는지 확인 합니다.

5.  저장소 할당량 설정을 확인 합니다.

또는

셸에서 다음 명령을 실행합니다.

    Get-Mailbox <identity> | fl IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

