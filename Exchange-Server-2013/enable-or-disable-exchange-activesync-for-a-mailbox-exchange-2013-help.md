---
title: '사서함에 대 한 Exchange ActiveSync를 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 사서함에 대 한 Exchange ActiveSync를 사용 하지 않도록 설정 하거나 사용
ms:assetid: dcf7c05b-b1b9-4b0f-800d-fec9f2ddc9e4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124809(v=EXCHG.150)
ms:contentKeyID: 50556094
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 대 한 Exchange ActiveSync를 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-13_

사용자 사서함에 대 한 Microsoft Exchange ActiveSync 를 사용할지 여부를 EAC 또는 셸을 사용할 수 있습니다. Exchange ActiveSync 은 사용자가 자신의 Exchange 사서함이 있는 모바일 장치를 동기화 할 수 있는 클라이언트 프로토콜입니다. Exchange ActiveSync 사용자 사서함을 만들 때 기본적으로 활성화 됩니다. 자세한 내용은 [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md)를 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "Exchange ActiveSync 설정" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 사용 하도록 설정 하거나 Exchange ActiveSync를 사용 하지 않도록 설정

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 사서함을 사용 하도록 설정 하거나, Exchange ActiveSync 사용 하지 않도록 설정 하려면을 클릭 하 고![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")**편집** 을 클릭 합니다.

3.  사서함 속성 페이지에서 **사서함 기능**을 클릭합니다.

4.  **모바일 장치** 다음 중 하나를 수행 합니다.
    
      - 사용 하지 않으려면 Exchange ActiveSync**Exchange ActiveSync 사용 하지 않도록 설정** 을 클릭 합니다.
        
        Exchange ActiveSync 를 사용 하지 않도록 설정 하려면 확실 한 경우 경고를 묻는 나타납니다. **예** 를 클릭 합니다.
    
      - Exchange ActiveSync 을 사용 하려면 **Exchange ActiveSync 사용** 을 클릭 합니다.

5.  **저장**을 클릭하여 변경 내용을 저장합니다.


> [!NOTE]
> 설정 하 고 EAC 대량 편집 기능을 사용 하 여 여러 사용자 사서함에 대 한 Exchange ActiveSync 사용 하지 않도록 설정할 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 <A href="manage-user-mailboxes-exchange-2013-help.md">사용자 사서함 관리</A>의 "사용자 사서함 대량 편집" 섹션을 참조 하십시오.



## 셸을 사용 하 여 하거나 Exchange ActiveSync를 사용 하지 않도록 설정

이 예에서는 Yan Li의 사서함에 대 한 Exchange ActiveSync 사용 하지 않도록 설정 합니다.

    Set-CASMailbox -Identity "Yan Li" -ActiveSyncEnabled $false

Elly Nkya의 사서함에 대 한 Exchange ActiveSync 설정 하는이 예제입니다.

    Set-CASMailbox -Identity Ellyn@contoso.com -ActiveSyncEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb125264\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사용자 사서함에 대 한 Exchange ActiveSync 사용 하지 않도록 설정 하거나 설정 했을 때 있는지를 확인 하려면 다음 중 하나를 수행 합니다.

  - EAC에서 **받는 사람** \> **사서함**으로 이동하여 사서함을 클릭한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

  - 사서함 속성 페이지에서 **사서함 기능**을 클릭합니다.

  - **모바일 장치** Exchange ActiveSync 기능을 사용할 수 있는지 여부를 확인 합니다.

또는

  - 셸에서 다음 명령을 실행합니다.
    
        Get-CASMailbox <identity>
    
    Exchange ActiveSync 을 사용 하도록 설정한 경우 *ActiveSyncEnabled* 속성에 대 한 값은 `True`합니다. Exchange ActiveSync 를 사용 하지 않도록 설정 하는 경우 값은 `False`.

