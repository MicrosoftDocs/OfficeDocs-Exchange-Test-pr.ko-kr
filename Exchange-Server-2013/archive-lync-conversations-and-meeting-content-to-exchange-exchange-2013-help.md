---
title: 'Lync 대화 및 모임 콘텐츠 Exchange에 보관: Exchange 2013 Help'
TOCTitle: Lync 대화 및 모임 콘텐츠 Exchange에 보관
ms:assetid: 3cff970e-e5ed-4a54-88e6-3665d84b5ed7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn508399(v=EXCHG.150)
ms:contentKeyID: 59678848
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lync 대화 및 모임 콘텐츠 Exchange에 보관

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange Online 에서 사용자의 사서함에 IM 대화와 같은 Lync Online 콘텐츠를 보관할 수 있습니다. 온-프레미스 배포에서 Exchange 2013 사서함에 Lync 2013 콘텐츠를 보관할 수 있습니다. 온라인에서 모두에서 온-프레미스 환경에서는이 위해서는 사용자의 사서함에 소송 보존 또는 In-place Hold를 배치 합니다. 보관 사서함이에 있는 사용자가 Lync 콘텐츠는 영구적으로 삭제 내용이 사용자의 사서함에서 복구 가능한 항목 폴더에 보존 되 보관 된 Lync 합니다. 사용자가 볼 수 있지만 eDiscovery 검색에 포함 됩니다.

소송 보존으로 설정에서 사서함을 할 때 Lync 항목을 포함 하 여 모든 콘텐츠 형식에 유지 됩니다. 기본적으로이 대/소문자 In-place Hold를 만들면 됩니다. 그러나 Lync 항목만 유지 하는 원본 위치 유지를 사용 하려는 경우 있습니다 수 옵션을 사용 **메시지 종류를 선택원본 위치 eDiscovery 및 유지** 마법사에서 **Lync 항목** 을 선택 하려면 아래 스크린샷에 표시 된 대로.

![Lync 항목 보유](images/Dn508399.691d2324-9fac-4689-8527-c78d387e0e3e(EXCHG.150).jpg "Lync 항목 보유")


> [!NOTE]
> Lync 항목을 제외 하는 원본 위치 유지를 구성할 수도 있습니다. 예, 조직 다른 콘텐츠 형식 보다 시간이 더 짧은 기간에 대 한 인스턴트 메시지 및 음성 메일 항목을 보존 하 선호 될 수 있습니다. 이 유형의 보존 정책을 구현 하려면 오랜 시간 (예: 7 년)에 대 한 콘텐츠를 보존 하 고이 보류에서 Lync 항목을 제외 하는 원본 위치 유지을 만듭니다. 그런 다음 사용 하 여 만듭니다 다른 원본 위치 유지 Lync 항목만 유지 하는 짧은 대기 기간입니다. 콘텐츠를 보존 하는 기간을 지정할 수 있습니다. 특정 기간으로 보류 만들기 (영문) 하는 방법에 대 한 자세한 내용은 <A href="in-place-hold-and-litigation-hold-exchange-2013-help.md">원본 위치 유지 및 소송 보존</A>을 참조 하십시오.



보류에서 사용자를 배치 하기 위한 단계별 지침은 다음 항목을 참조 합니다.

  - [만들기 또는 In-place Hold 제거](create-or-remove-an-in-place-hold-exchange-2013-help.md)

  - [전체 사서함에 소송 보존으로 설정](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

보관과 관련 된 추가 관리 작업에 대 한 참조 하십시오.

  - [Exchange Online의 보관 사서함을 사용 하지 않도록 설정 하거나 사용](https://technet.microsoft.com/ko-kr/library/jj984357\(v=exchg.150\))

  - [Exchange 2013에서 원본 위치 보관 관리](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

## 추가 정보

  - 사용자의 [대화 내용 폴더에 Lync IM 대화를 저장](https://go.microsoft.com/fwlink/p/?linkid=400589)하도록 구성 된 Lync 클라이언트에 있는지 여부에 관계 없이 서버에서 발생 Lync 콘텐츠를 보관 합니다.

  - 원본 위치 유지 또는 소송 보존으로 설정 된 사용자가 배치 후 Lync 콘텐츠 보관을 시작 합니다. 사용자의 Lync를 확인 하려면 통신을 자신의 계정이 생성 되는 계정에 보류를 만든 후에 즉시 전체 시간에서 보관 됩니다.

온-프레미스 Exchange 2013 및 Lync 2013 배포에서 또한:

  - Lync 2013 및 Exchange 2013 간의 OAuth 인증을 구성 해야 합니다. 자세한 내용은 [SharePoint 및 Lync와의 통합](integration-with-sharepoint-and-lync-exchange-2013-help.md)를 참조 합니다.

  - 또한 Lync 2013Exchange 2013 대기는 사용자가 배치 여부에 관계 없이 콘텐츠를 보관할 수 있습니다. 이 작업은 사용자의 Exchange 보관 정책을 구성 하 여 수행 됩니다. `ArchivingToExchange`을 Lync 사용자의 *ExchangeArchivingPolicy* 속성을 설정 하려면 Lync 2013 서버의 `Set-CsUser` cmdlet을 사용 합니다.

  - 온-프레미스 배포에서 Lync 콘텐츠를 보관 하는 방법에 대 한 자세한 내용은 Lync 2013 설명서에서 [보관을 위한 계획](https://go.microsoft.com/fwlink/p/?linkid=400590) 를 참조 합니다.

