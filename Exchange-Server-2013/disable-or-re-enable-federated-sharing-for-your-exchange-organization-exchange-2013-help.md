---
title: 'Exchange 조직에 대 한 페더레이션 공유를 사용 하거나 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: Exchange 조직에 대 한 페더레이션 공유를 사용 하거나 사용 하지 않도록 설정
ms:assetid: d36490d8-0268-47b9-a6d4-e56427f1b02e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657497(v=EXCHG.150)
ms:contentKeyID: 50484221
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 조직에 대 한 페더레이션 공유를 사용 하거나 사용 하지 않도록 설정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-02-17_

조직의 페더레이션 공유를 일시적으로 사용할 수 없도록 설정해야 하는 경우가 있습니다. 이 경우 기존 페더레이션 트러스트를 삭제하거나 나중에 필요할 수 있는 조직 관계 및 공유 정책을 삭제하는 대신 간단히 페더레이션 트러스트에 대한 OrgID(조직 식별자)를 사용하지 않도록 설정할 수 있습니다.


> [!WARNING]
> Office 365가 포함된 하이브리드 배포에서 온-프레미스 서버에 대한 페더레이션 트러스트를 사용하지 않도록 설정하면 공유 약속 있음/없음 일정 정보, 메일 설명 및 메시지 추적 같은 하이브리드 기능 또한 사용할 수 없게 됩니다. 단, 온-프레미스 조직에 대한 페더레이션 트러스트가 사용되지 않는 경우에도 보안 메일 전송은 하이브리드 배포에서 계속 사용할 수 있습니다.



페더레이션 트러스트에 대한 자세한 내용은 [페더레이션](federation-exchange-2013-help.md)를 참조하십시오. 페더레이션 공유에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md)를 참조하십시오.

페더레이션 공유와 관련된 추가 관리 작업에 대한 자세한 내용은 [페더레이션 프로시저](federation-procedures-exchange-2013-help.md) 항목을 참조하십시오.


> [!IMPORTANT]
> Exchange Server 2013의 이 기능은 현재 중국에서 21Vianet에 의해 운영되는 Office 365와는 완전히 호환되지는 않으며 일부 기능 제한이 적용될 수 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet에 의해 운영되는 Office 365 정보</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 항목의 *Federation and certificates* 권한 항목을 참조하십시오.

  - 다른 페더레이션 Exchange 조직에 대한 공유 정책과 기존 조직 관계는 수정되거나 비활성화되지 않습니다. 인터넷 받는 사람에게 일정 정보에 대한 액세스를 제공하기 위해 구성된 공유 정책은 영향을 받지 않습니다.

  - 페더레이션 트러스트에 대한 OrgID를 사용하거나 사용하지 않도록 설정하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

## 셸을 사용하여 페더레이션 공유를 사용하지 않거나 다시 사용하도록 설정

이 예에서는 OrgID를 사용하지 않도록 설정하고, Exchange 조직에 대한 페더레이션 및 페더레이션 공유를 사용하지 않도록 설정합니다.

    Set-FederatedOrganizationIdentifier -Enabled $false

이 예에서는 OrgID를 사용하도록 설정하고, Exchange 조직에 대한 페더레이션 및 페더레이션 공유를 다시 사용하도록 설정합니다.

    Set-FederatedOrganizationIdentifier -Enabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/ko-kr/library/dd351037\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

**Set-OrganizationIdentifier** cmdlet이 성공적으로 완료되면 OrgID를 사용하지 않거나 사용하도록 제대로 설정한 것입니다.

성공 여부를 추가로 알아보려면 다음 셸 명령을 실행하고 *Enabled* 매개 변수에서 반환되는 값을 확인합니다.

    Get-FederatedOrganizationIdentifier


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


