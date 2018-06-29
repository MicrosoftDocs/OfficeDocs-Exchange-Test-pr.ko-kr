---
title: '조직 관계: Exchange 2013 Help'
TOCTitle: 조직 관계
ms:assetid: 4c48db61-3370-462b-a3f8-2a6311c6e4ee
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657445(v=EXCHG.150)
ms:contentKeyID: 50483057
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 조직 관계

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-02-20_

외부 비즈니스 파트너와 일정 정보를 공유하려면 조직 관계를 설정합니다. Exchange 관리자는 Office 365 조직 또는 다른 Exchange 온-프레미스 조직과의 조직 관계를 설정할 수 있습니다. 다른 온-프레미스 Exchange 조직과 일정을 공유하려면 두 온-프레미스 Exchange 관리자가 모두 클라우드와의 인증 관계("페더레이션"이라고도 함)를 설정해야 하며 최소 소프트웨어 요구 사항을 충족해야 합니다.

조직 관계는 각 조직의 사용자가 일정 약속 있음/없음 정보를 확인할 수 있도록 하는 기업 간의 일대일 관계입니다. 조직 관계를 설정할 때는 자신의 조직이 관계에서 어느 쪽인지를 설정하고 외부 조직의 사용자가 볼 수 있는 정보의 수준을 지정합니다. 외부 조직도 관계 측면에 대해 같거나 다른 설정을 지정할 수 있습니다. 예를 들어 Contoso에서 Tailspin Toys와 조직 관계를 만드는 경우 Tailspin Toys의 사용자는 모임 초대에 자신의 전자 메일 주소를 추가하여 Contoso의 사용자와 모임을 예약할 수 있습니다. 이 경우 초대를 받은 Contoso 사용자의 약속 있음/없음 정보가 Tailspin Toys 사용자에게 표시됩니다. 그러나 Contoso에서 Tailspin Toys 사용자의 약속 있음/없음 정보를 보려면 Tailspin Toys 관리자가 Contoso와의 조직 관계를 설정해야 합니다.

다음의 세 가지 액세스 수준을 지정할 수 있습니다.

  - 권한 없음

  - 약속 있음/없음 시간에만 액세스 가능

  - 시간, 제목, 위치를 비롯한 약속 있음/없음 정보에 액세스 가능


> [!NOTE]
> 다른 사람과 약속 있음/없음 정보를 공유하지 않으려는 사용자는 Outlook에서 기본 권한 항목을 변경할 수 있습니다. 이렇게 하려면 <STRONG>일정 속성</STRONG> &gt; <STRONG>사용 권한</STRONG> 탭으로 이동하여 <STRONG>기본</STRONG> 권한을 선택하고 <STRONG>권한 수준</STRONG> 목록에서 <STRONG>없음</STRONG>을 선택합니다. 그러면 조직 관계가 있더라도 약속 있음/없음 정보가 내부 또는 외부 사용자에게 표시되지 않습니다. 즉, 사용자가 설정하는 권한이 적용됩니다.



다음 항목은 조직에 대한 공유의 일부로 조직 관계를 구성하고 관리하는 데 도움이 됩니다.

[조직 관계 만들기](create-an-organization-relationship-exchange-2013-help.md)

[조직 관계 수정](modify-an-organization-relationship-exchange-2013-help.md)

[조직 관계 제거](remove-an-organization-relationship-exchange-2013-help.md)

페더레이션 공유에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md) 항목을 참조하십시오.

