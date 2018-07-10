---
title: '사서함으로 변환: Exchange 2013 Help'
TOCTitle: 사서함으로 변환
ms:assetid: dfed045e-a740-4a90-aff9-c58d53592f79
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ710164(v=EXCHG.150)
ms:contentKeyID: 50484325
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함으로 변환

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-04-26_

사서함 사서함의 다른 형식으로 변환 매우 비슷합니다 환경에서 Exchange 2010 합니다. 여전히 변환을 수행 하려면 셸에서 Set-mailbox cmdlet을 사용 해야 합니다.

다른 한 형식에서 다음과 같은 사서함을 변환할 수 있습니다.

  - 리소스 (회의실 또는 장비) 사서함을 사용자 사서함

  - 사용자 사서함에 공유 사서함

  - 리소스 사서함에 공유 사서함

  - 사용자 사서함을 리소스 사서함

  - 공유 사서함을 리소스 사서함

메모는 조직에서 하이브리드 Exchange 환경을 사용 하는 경우 필요한 온-프레미스 Exchange 관리 도구를 사용 하 여 사용자 사서함을 관리할 수 있습니다. 하이브리드 환경에서 사서함을 변환 하려면 온-프레미스 exchange 사서함을 다시 이동할 사서함 유형으로 변환 하 고 Office 365로 다시 이동 해야할 수 있습니다.


> [!IMPORTANT]
> 공유 사서함을 사용자 사서함을 변환 하는 경우의 변환 하기 전에 사서함에서 모든 모바일 장치를 제거 하거나 해야 하거나 변환 후 사서함에 대 한 모바일 액세스를 차단 해야 합니다. 즉, 모바일 기능 사서함 공유 사서함으로 변환 되 면 제대로 작동 하지 것입니다. 차단 액세스에 대 한 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=847873">Office 365에서 이전 직원 제거</A>을 참조 하십시오.



## 셸을 사용 하 여 사서함으로 변환 하려면

예상 완료 시간: 5분.

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

공유 사서함 사용자 사서함에 MarketingDept1를 변환 하는이 예제입니다.

    Set-Mailbox MarketingDept1 -Type Regular

*Type* 매개 변수는 다음 값을 사용할 수 있습니다.

  - 일반

  - 회의실

  - 장비

  - 공유

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사서함을 성공적으로 변환가 확인 하려면 다음 셸 명령을 실행 합니다.

    Get-Mailbox -Identity MarketingDept1 | Format-List RecipientTypeDetails

*RecipientTypeDetails* 에 대 한 값을 *UserMailbox*해야 합니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))를 참조하십시오.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


