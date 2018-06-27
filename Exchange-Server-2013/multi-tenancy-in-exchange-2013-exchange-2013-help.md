---
title: 'Exchange 2013의 다중 테 넌 트: Exchange 2013 Help'
TOCTitle: Exchange 2013의 다중 테 넌 트
ms:assetid: df09257d-dd98-4f59-b830-1818cedda15c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ862352(v=EXCHG.150)
ms:contentKeyID: 50556106
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013의 다중 테 넌 트

 

_**적용 대상:**Exchange Online, Exchange Server, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

다중 테 넌 트 (호스트) Exchange 2013 배포 다중 호스트 하도록 구성 된 Exchange 조직 곳으로 정의 된 및 개별 조직 또는 비즈니스 단위 (테 넌 트의)에서는 일반적으로 공유 하지 않는 전자 메일, 데이터, 사용자, 전체 주소 목록 (Gal) 또는 기타 일반적으로 사용 되는 Exchange 개체입니다. 이 공유 하드웨어, 소프트웨어 및 리소스 (테 넌 트 간의 논리적 구분을 유지 하면서), 모두의 다중 테 넌 트 기능 및 호스팅 자신의 요구를 충족 하는 서비스를 제공 하는 동안 사용 되는 표준 Exchange 배포의 간단 하 게 활용 하는 조직은 수 있습니다.

## Exchange 2013 조직에서 다중 테 넌 트

Exchange 2013 표준, 접근 방식을 지 Exchange 2010 서비스 팩 2 (SP2)에 사용 되는 비슷한 온-프레미스 Exchange 설치를 사용 하 여 호스팅을 지원 하기 위해 계속 합니다. `/hosting` 모드 스위치를 지원 하 고 만들고 강조 주소록 정책 (Abp) 호스팅 관리 솔루션 및 승인 된 독립 소프트웨어 공급 업체 (Isv)에서 제공 하는 자동화 도구와 함께에서 사용 됩니다. 이러한 솔루션 사례 및 Microsoft 승인 구성 지침 프레임 워크 기반으로 만들어진 및 Exchange 조직 호스팅 서비스 및 기능을 제공 하는 보다 쉽게, 보다 강력한 방법을 제공 합니다.

Exchange 2013 에서는 다음과 같은 기본 구성 요소 및 기능을 활용 하 여 다중 테 넌 트를 지원 합니다.

  - **Active Directory**   다중 테 넌 트 Exchange 조직에 있는 각 사업부에 대 한 Active Directory 컨테이너에 별도 *ExchangeOrganization* 대신 단일 *ExchangeOrganization* Active Directory 컨테이너를 사용 하 여 Exchange 2013 다중 테 넌 트 지원 됩니다. 이 통해 간단 Active Directory 구조에 대 한 Active Directory와 관련 된 사용 권한 문제가 발생할 가능성을 줄입니다.
    
    Exchange 2013 의 Active Directory 변경 사항에 대 한 자세한 내용은, [Active Directory](active-directory-exchange-2013-help.md)를 참조 하십시오.

  - **주소록 정책 (Abp)**   Exchange 2010 s p 2에에서 도입 된, Abp Exchange 2013 에서 주소 목록에 대 한 사용자 액세스를 제어 하, 전체 주소 목록, gal (전체) 사용되며이 오프 라인 주소록이 (Oab) Exchange 조직에 합니다. Abp 다중 테 넌 트 조직 구조를 따라 이러한 리소스의 논리적 그룹을 만들려면 하 고 개별 사용자에 게 할당할 수 있는 단일, 가상 개체에 이러한 다른 Active Directory 개체를 그룹화 합니다. Exchange 2013 에서 ABP 기능은 된 Exchange 2010 s p 2에서에서와 비슷합니다.
    
    에 대 한 자세한 Abp Exchange 2013 에서 [주소록 정책](address-book-policies-exchange-2013-help.md)를 참조 하십시오.

  - **관리 솔루션 호스팅**   Exchange 2013 를 사용 하 여 호스팅된 Exchange 솔루션을 제공 하는 일부 관리자가 사용자 지정 된 호스팅 관리 방식을 사용 하 여 이점을 얻을 수 있습니다. Exchange 관리 센터 (EAC)의 일부 제한 사항으로 인해 Microsoft는 호스팅된 Exchange 2013 조직에 대해 승인 된 프레임 워크와 지침을 준수 하는 컨트롤 패널 및 자동화 솔루션 개발에이 지원 하기 위해 타사 공급 업체와 함께 작동 합니다. 호스팅된 Exchange 솔루션을 구성 하는 조직에서는 호스팅된 조직 같은 상황에서는 필요를 관리 하는 이러한 도구를 활용 하는 것이 좋습니다.
    
    유효성이 검사 된 솔루션 공급 업체를 비롯 하 여 솔루션을 호스팅된 관리 하는 방법에 대 한 자세한 내용은 Exchange Server 2013 호스팅 및 다중 테 넌 시 솔루션 및 지침[](https://go.microsoft.com/fwlink/?linkid=275036)

