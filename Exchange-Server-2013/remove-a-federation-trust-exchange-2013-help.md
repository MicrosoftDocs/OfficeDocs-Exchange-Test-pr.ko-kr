---
title: '페더레이션 트러스트 제거: Exchange 2013 Help'
TOCTitle: 페더레이션 트러스트 제거
ms:assetid: dc4d126d-b567-470d-a5d0-e1402bf8f369
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657500(v=EXCHG.150)
ms:contentKeyID: 50484300
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 페더레이션 트러스트 제거

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-01-04_

페더레이션 트러스트 Microsoft Exchange 2013 조직 및 Azure Active Directory 인증 시스템 간에 트러스트 관계를 설정 하 고 다른 페더레이션 Exchange 조직과 공유를 지원 합니다. 페더레이션 트러스트를 제거 하는 온-프레미스에서 Exchange 조직의 다른 페더레이션 Exchange 조직과 및 하이브리드 배포의 일부분으로 조직에 연결 하는 Office 365 조직과 페더레이션 공유 비활성화 됩니다. 페더레이션 트러스트를 제거 하기 전에 조직에 전반적인 영향을 신중 하 게 고려해 야 합니다.

페더레이션 트러스트와 관련된 추가 관리 작업에 대한 자세한 내용은 [페더레이션 프로시저](federation-procedures-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> Exchange Server 2013의 이 기능은 현재 중국에서 21Vianet에 의해 운영되는 Office 365와는 완전히 호환되지는 않으며 일부 기능 제한이 적용될 수 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet에 의해 운영되는 Office 365 정보</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 주제의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. 벲芽燭뮌抉?및 인증서" 권한 항목.

  - 페더레이션 트러스트를 제거한 후에 각 페더레이션된 도메인에 대한 공용 DNS 서버에서 TXT 레코드를 제거할 수 있습니다. 공용 DNS 레코드를 호스트하는 조직의 TXT 레코드 제거를 위한 요구 사항을 검토하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 페더레이션 트러스트 제거

1.  온-프레미스 조직의 Exchange 2013 서버에서 **조직** \> **공유**로 이동합니다.

2.  **페더레이션 트러스트** 섹션에서 **제거**를 클릭합니다.

3.  경고에서 **예**를 클릭하여 페더레이션 트러스트를 제거할 것임을 확인합니다.

4.  페더레이션 트러스트가 제거된 후에는 **닫기**를 클릭합니다.

## 셸을 사용하여 페더레이션 트러스트 제거

이 예에서는 페더레이션 트러스트를 제거합니다.

    Remove-FederationTrust

구문과 매개 변수에 대한 자세한 내용은 [Remove-FederationTrust](https://technet.microsoft.com/ko-kr/library/dd351153\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

페더레이션 트러스트를 성공적으로 제거했는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **조직** \> **공유**로 이동합니다. 페더레이션 트러스트를 성공적으로 제거했으면 **페더레이션 트러스트**에서 **사용** 단추만 사용할 수 있게 됩니다.

  - 셀에서 다음 명령을 실행하여 Exchange 조직에 대해 페더레이션 트러스트 정보가 반환되지 않았는지 확인합니다.
    
        Get-FederationTrust
    
    구문과 매개 변수에 대한 자세한 내용은 [Get-FederationTrust](https://technet.microsoft.com/ko-kr/library/dd351262\(v=exchg.150\))를 참조하십시오.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

