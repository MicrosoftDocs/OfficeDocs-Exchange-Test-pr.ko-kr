---
title: 'Outlook에서 스팸 방지 스탬프 보기: Exchange 2013 Help'
TOCTitle: Outlook에서 스팸 방지 스탬프 보기
ms:assetid: cddb5dbf-ad1e-471c-9fc8-28ddcf7ec1d0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124595(v=EXCHG.150)
ms:contentKeyID: 50484181
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook에서 스팸 방지 스탬프 보기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-03_

Microsoft Outlook을 사용하여 Microsoft Exchange가 전자 메일 메시지에 적용한 스팸 방지 스탬프를 볼 수 있습니다. 스팸 방지 스탬프를 사용하면 보낸 사람별 정보, 퍼즐 유효성 검사 결과 및 콘텐츠 필터링 결과 등의 진단 메타데이터 또는 스탬프를 인터넷에서 인바운드 메시지를 필터링하는 스팸 방지 에이전트를 통과하는 메시지에 적용함으로써 스팸 관련 문제를 진단할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 15분

  - [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 주제의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "사서함 액세스" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## Outlook 2010 또는 Outlook 2013을 사용하여 스팸 방지 스탬프 보기

1.  클라이언트 컴퓨터에 있는 Outlook 2010 또는 Outlook 2013의 **메일** 보기에서 메시지를 두 번 클릭하여 엽니다.

2.  리본의 **태그** 섹션에서 **옵션** 아이콘을 클릭하여 메시지 **속성** 대화 상자를 표시합니다.

3.  다음 예와 같이 **속성** 대화 상자의 **인터넷 헤더** 섹션에서 스크롤 막대를 사용하여 스팸 방지 스탬프를 봅니다.
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

## Outlook 2007을 사용하여 스팸 방지 스탬프 보기

1.  클라이언트 컴퓨터에 있는 Outlook 2007의 **메일** 보기에서 메시지를 두 번 클릭하여 엽니다.

2.  **메시지** 탭의 **옵션** 그룹에서 **메시지 옵션**을 클릭합니다.

3.  다음 예와 같이 **메시지 옵션** 대화 상자 **인터넷 헤더** 섹션에서 스크롤 막대를 사용하여 스팸 방지 스탬프를 봅니다.
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

