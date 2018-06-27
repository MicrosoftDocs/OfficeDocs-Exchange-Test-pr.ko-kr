---
title: '릴리스 스팸 격리 사서함에서 메시지를 격리: Exchange 2013 Help'
TOCTitle: 릴리스 스팸 격리 사서함에서 메시지를 격리
ms:assetid: 7a86bfde-f868-4689-bdec-5f01e52b510d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998920(v=EXCHG.150)
ms:contentKeyID: 50483506
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 릴리스 스팸 격리 사서함에서 메시지를 격리

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Outlook을 사용하여 스팸 격리 사서함에서 격리된 메시지를 복구할 수 있습니다.

스팸 격리는 합법적인 메시지를 받지 못할 위험을 줄여 주는 콘텐츠 필터 에이전트의 기능입니다. 메시지가 스팸 격리 임계값을 충족하는 경우 NDR(배달 못 함 보고서)에 래핑되고 스팸 격리 사서함으로 배달됩니다. 스팸 격리 기능에 대한 자세한 내용은 [스팸 격리](spam-quarantine-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 15분

  - [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 주제의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "사서함 액세스" 항목.

  - 이 절차에서는 스팸 방지 격리 사서함을 구성해야 합니다. 자세한 내용은 [스팸 격리 사서함 구성](configure-a-spam-quarantine-mailbox-exchange-2013-help.md)을 참조하십시오.

  - 격리 사서함에 액세스 하려면 해당 사서함에 대 한 Outlook 프로필을 구성 하 고 Outlook을 사용 하 여 사서함을 열고 다음을 지정 해야 합니다. 구성 하 고 여러 Outlook 프로필을 사용 하는 방법에 대 한 자세한 내용은 [개요의 Outlook 전자 메일 프로필](https://go.microsoft.com/fwlink/p/?linkid=178975)을 참조 하십시오.

  - 복구할 메시지를 손쉽게 찾으려면 사용자 지정 Outlook 양식을 만들고 기본 보기를 수정하여 메시지 목록에 원래 보낸 사람 주소를 노출시킵니다. 자세한 단계는 [격리 사서함에서 원래 보낸 사람을 표시하도록 Outlook 구성](configure-outlook-to-show-the-original-sender-in-the-quarantine-mailbox-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## Outlook 2010 또는 Outlook 2013을 사용하여 스팸 격리 사서함에서 메시지 해제

1.  클라이언트 컴퓨터에서 Outlook 2010 또는 Outlook 2013을 사용하여 격리 사서함을 엽니다.

2.  **메일** 보기의 **받은 편지함**에서 복구할 메시지를 찾고 메시지를 두 번 클릭하여 엽니다.

3.  리본 메뉴의 **이동** 섹션에서 **작업** \> **메시지 다시 전송**을 클릭합니다.

4.  메시지가 열리면 **보내기**를 클릭하여 지정된 받는 사람에게 메시지를 다시 보냅니다.

## Outlook 2007을 사용하여 스팸 격리 사서함에서 메시지 해제

1.  클라이언트 컴퓨터에서 Outlook 2007을 사용하여 격리 사서함을 엽니다.

2.  **메일 폴더** 보기의 **받은 편지함**에서 복구할 메시지를 찾고 메시지를 두 번 클릭하여 엽니다.

3.  **보고서** 탭의 **응답** 그룹에서 **다시 보내기**를 클릭합니다.

4.  메시지가 열리면 **보내기**를 클릭하여 지정된 받는 사람에게 메시지를 다시 보냅니다.

## 작동 여부는 어떻게 확인합니까?

스팸 격리 사서함에서 메시지가 해제되었는지 확인하려면 받는 사람에게 연락하여 메시지를 받았는지 확인합니다.

