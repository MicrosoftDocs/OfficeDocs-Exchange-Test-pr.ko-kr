---
title: '사서함에 대 한 메시지 크기 제한 구성: Exchange 2013 Help'
TOCTitle: 사서함에 대 한 메시지 크기 제한 구성
ms:assetid: d1220685-14c0-4c4f-abb2-3920f3046212
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124708(v=EXCHG.150)
ms:contentKeyID: 50556091
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 대 한 메시지 크기 제한 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-12_

EAC 및 셸을 사용하여 사용자 사서함의 메시지 크기 제한을 구성할 수 있습니다. 이 구성을 통해 사용자가 보내고 받을 수 있는 메시지의 크기가 제한됩니다. 사서함이 만들어졌을 때는 기본적으로 보내고 받는 메시지에 대한 크기 제한이 없습니다.

Exchange 조직에는 사서함에서 보내고 받을 수 있는 최대 메시지 크기를 결정하는 다른 설정(예: 사서함 서버에 대해 구성된 최대 메시지 크기)도 있다는 사실을 유의하십시오. 메시지 크기 제한 유형을 포함한 Exchange의 메시지 크기 제한에 대한 자세한 내용은 [메시지 크기 제한](message-size-limits-exchange-2013-help.md)을 참조하십시오.

사용자 사서함과 관련된 추가 관리 작업에 대한 자세한 내용은 [사용자 사서함 관리](manage-user-mailboxes-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> 메일 사용자가 보내고 받은 메시지 및 공유 사서함에서 보내고 받은 메시지의 크기도 제어할 수 있습니다.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 메시지 크기 제한 구성

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 메시지 크기 제한을 변경할 사서함을 클릭한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  사서함 속성 페이지에서 **사서함 기능**을 클릭합니다.

4.  **메시지 크기 제한** 아래에서 **세부 정보 보기**를 클릭하여 다음 메시지 크기 제한을 보고 변경합니다.
    
      - **보낸 메시지**   이 사용자가 보내는 메시지의 최대 크기를 지정하려면 **최대 메시지 크기(KB)** 확인란을 선택하고 상자에 값을 입력합니다. 메시지 크기는 0KB에서 2,097,151KB 사이여야 합니다. 사용자가 지정된 크기보다 큰 메시지를 보내는 경우 해당 메시지는 설명이 포함된 오류 메시지와 함께 사용자에게 반환됩니다.
    
      - **받은 메시지**   이 사용자가 받는 메시지의 최대 크기를 지정하려면 **최대 메시지 크기(KB)** 확인란을 선택하고 상자에 값을 입력합니다. 메시지 크기는 0KB에서 2,097,151KB 사이여야 합니다. 지정된 크기보다 큰 메시지를 사용자에게 보내는 경우 해당 메시지는 설명이 포함된 오류 메시지와 함께 보낸 사람에게 반환됩니다.

5.  **확인**을 클릭한 후 **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용하여 메시지 크기 제한 구성

이 예에서는 Debra Garcia의 사서함에서 보낸 메시지의 최대 크기를 25MB로, 받은 메시지의 최대 크기를 35MB로 설정합니다.

    Set-Mailbox "Debra Garcia" -MaxSendSize 25mb -MaxReceiveSize 35mb

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사서함에 대한 메시지 크기 제한을 성공적으로 구성했는지 확인하려면 다음 중 하나를 수행합니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 메시지 크기 제한을 확인할 사서함을 클릭한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  사서함 속성 페이지에서 **사서함 기능**을 클릭합니다.

4.  **메시지 크기 제한** 아래에서 **세부 정보 보기**를 클릭하여 사서함에 대한 메시지 크기 제한을 확인합니다.

또는

셸에서 다음 명령을 실행합니다.

    Get-Mailbox <identity> | fl MaxSendSize,MaxReceiveSize

