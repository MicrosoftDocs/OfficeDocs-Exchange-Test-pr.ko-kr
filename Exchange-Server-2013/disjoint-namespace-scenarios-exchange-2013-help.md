---
title: '분리 된 네임 스페이스 시나리오: Exchange 2013 Help'
TOCTitle: 분리 된 네임 스페이스 시나리오
ms:assetid: 90101d49-6f45-44be-8a93-eeb2c8283e3b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb676377(v=EXCHG.150)
ms:contentKeyID: 50483661
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 분리 된 네임 스페이스 시나리오

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

이 항목에서는 분리된 네임스페이스의 개념 및 분리된 네임스페이스가 있는 도메인에서 Microsoft Exchange 2013을 배포하는 데 지원되는 시나리오를 제공합니다.

**목차**

DNS and NetBIOS domain names

Disjoint namespaces

Exchange 2013 and disjoint namespaces

Allow Exchange 2013 servers to access domain controllers that are disjoint

View DNS and NetBIOS name-related information of a computer running Windows Server 2008

## DNS 및 NetBIOS 도메인 이름

첫째, 특정 배경입니다. 인터넷상의 모든 컴퓨터에는 DNS(Domain Name System) 이름이 있습니다. 이 이름을 *컴퓨터 이름* 또는 *호스트 이름*이라고도 합니다. 네트워킹 기능이 있는 Windows 운영 체제를 실행하는 모든 컴퓨터에는 NetBIOS 이름도 있습니다.

Active Directory 도메인에서 Windows를 실행 중인 컴퓨터에는 다음과 같이 DNS 도메인 이름과 NetBIOS 도메인 이름이 모두 있습니다.

  - **DNS 도메인 이름**   DNS 도메인 이름은 점(**.**)으로 구분된 하나 이상의 하위 도메인으로 구성되며 최상위 도메인 이름으로 끝납니다. 예를 들어 corp.contoso.com이라는 DNS 도메인 이름에서 하위 도메인은 corp와 contos이고 최상위 도메인 이름은 com입니다.

  - **NetBIOS 도메인 이름**   일반적으로 NetBIOS 도메인 이름은 DNS 도메인 이름의 하위 도메인입니다. 예를 들어, DNS 도메인 이름이 contoso.com인 경우 NetBIOS 도메인 이름은 contoso입니다. DNS 도메인 이름이 corp.contoso.com인 경우 NetBIOS 도메인 이름은 corp입니다.


> [!NOTE]
> Windows Server 2008을 실행 중인 컴퓨터의 DNS 및 NetBIOS 정보를 찾으려면 View DNS and NetBIOS name-related information of a computer running Windows Server 2008 항목을 참조하십시오.



또한 Active Directory 도메인의 컴퓨터에도 주 DNS 접미사가 있으며 추가 DNS 접미사가 있을 수 있습니다. 기본적으로 주 DNS 접미사는 DNS 도메인 이름과 같습니다. 주 DNS 접미사를 변경하는 방법에 대한 자세한 내용은 이 항목의 뒤에 나오는 절차를 참조하십시오.

도메인의 첫번째 도메인 컨트롤러를 구성 하는 경우 DNS 도메인 이름 및 Active Directory 도메인의 NetBIOS 도메인 이름을 정의 합니다. 도메인 컨트롤러를 구성 하는 방법에 대 한 자세한 내용은 [도메인 컨트롤러 역할](https://go.microsoft.com/fwlink/p/?linkid=268367) 및 [Active Directory 도메인 서비스 개요](https://go.microsoft.com/fwlink/p/?linkid=268366)를 참조 하십시오.

## 연결되지 않은 네임스페이스

대부분의 도메인 토폴로지에서 도메인에 있는 컴퓨터의 주 DNS 접미사는 DNS 도메인 이름과 동일합니다.

서로 다른 네임스페이스가 필요한 경우가 있을 수 있습니다. 이를 *연결되지 않은 네임스페이스*라고 합니다. 예를 들어, 합병 또는 인수로 인해 연결되지 않은 네임스페이스가 있는 토폴로지를 갖게 될 수도 있고, 회사의 DNS 관리를 Active Directory 관리자와 네트워크 관리자로 분리하여 수행하는 경우 연결되지 않은 네임스페이스가 있는 토폴로지가 필요할 수도 있습니다.

연결되지 않은 네임스페이스 시나리오는 컴퓨터의 주 DNS 접미사와 해당 컴퓨터가 있는 DNS 도메인 이름이 일치하지 않는 시나리오입니다. 주 DNS 접미사가 일치하지 않는 컴퓨터를 *연결되지 않은* 컴퓨터라고 합니다. 연결되지 않은 네임스페이스의 또 다른 시나리오는 도메인 컨트롤러의 NetBIOS 도메인 이름과 DNS 도메인 이름이 일치하지 않는 경우입니다.

## Exchange 2013 및 연결되지 않은 네임스페이스

Exchange 2013은 연결되지 않은 네임스페이스가 있는 도메인에 Exchange를 배포하는 데 대해 다음과 같은 세 가지 시나리오를 지원합니다.

  - **주 DNS 접미사와 DNS 도메인 이름이 다른 경우**   도메인 컨트롤러의 주 DNS 접미사가 DNS 도메인 이름과 다릅니다. 도메인의 구성원인 컴퓨터가 연결된 컴퓨터이거나 연결되지 않은 컴퓨터일 수 있습니다.

  - **구성원 컴퓨터가 연결되지 않은 경우**   도메인 컨트롤러는 연결되었지만 Active Directory 도메인의 구성원 컴퓨터는 연결되지 않았습니다.

  - **도메인 컨트롤러의 NetBIOS 이름이 해당 DNS 도메인 이름의 하위 도메인과 다른 경우**   도메인 컨트롤러의 NetBIOS 도메인 이름이 해당 도메인 컨트롤러의 DNS 도메인 이름의 하위 도메인과 다릅니다.

다음 섹션에서는 이러한 시나리오에 대해 자세히 설명합니다.


> [!NOTE]
> 이 항목에서 설명 하는 분리 된 네임 스페이스 시나리오에서 Exchange 2013 를 실행 하려면 지원 됩니다. 그러나이 항목에 설명 된 시나리오 중 하나를 없는 분리 된 네임 스페이스 시나리오를 사용 하는 경우 Exchange 2013 를 배포 하려면 Microsoft 서비스와 함께 작동 해야 합니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=94845">Microsoft 서비스</A>를 참조 하십시오.



## 시나리오: 주 DNS 접미사와 DNS 도메인 이름이 다른 경우

이 시나리오에서는 도메인 컨트롤러의 주 DNS 접미사가 DNS 도메인 이름과 동일하지 않습니다. 이 시나리오에서는 도메인 컨트롤러가 연결되어 있지 않습니다. Exchange 서버 및 Microsoft Outlook 클라이언트 컴퓨터를 비롯하여 도메인의 구성원인 컴퓨터에는 도메인 컨트롤러의 주 DNS 접미사와 일치하거나 DNS 도메인 이름과 일치하는 주 DNS 접미사가 있을 수 있습니다.

## 시나리오: 구성원 컴퓨터가 연결되지 않은 경우

이 시나리오에서는 도메인 컨트롤러의 주 DNS 접미사가 DNS 도메인 이름과 동일하지만 Exchange 2013이 설치되어 있는 구성원 컴퓨터의 주 DNS 접미사가 DNS 도메인 이름과 동일하지 않습니다. 그리고 분리되지 않은 도메인 컨트롤러와 분리된 구성원 컴퓨터가 있습니다. Outlook을 실행 중인 구성원 컴퓨터에는 연결되지 않은 Exchange 서버의 주 DNS 접미사와 일치하거나 DNS 도메인 이름과 일치하는 주 DNS 접미사가 있을 수 있습니다.

## 시나리오: 도메인 컨트롤러의 NetBIOS 이름이 해당 DNS 도메인 이름과 다른 경우

이 시나리오에서는 도메인 컨트롤러의 NetBIOS 도메인 이름이 이 도메인 컨트롤러의 DNS 도메인 이름과 동일하지 않습니다.

**NetBIOS 도메인 이름이 DNS 도메인 이름과 일치하지 않는 경우**

![NetBIOS 도메인 이름이 DNS 도메인 이름과 일치하지 않는 경우](images/Bb676377.1ee18cb6-0296-4875-b572-0ddf33f65f7c(EXCHG.150).gif "NetBIOS 도메인 이름이 DNS 도메인 이름과 일치하지 않는 경우")

## Exchange 2013 서버에서 분리된 도메인 컨트롤러에 액세스하도록 허용

Exchange 2013 서버에 연결 되는 도메인 컨트롤러를 액세스를 허용 하려면 도메인 개체 컨테이너에 **msDS-AllowedDNSSuffixes**Active Directory 특성을 수정 해야 합니다. 특성에 모두 DNS 접미사를 추가 해야 합니다. 특성을 수정 하는 방법에 대 한 자세한 단계 [컴퓨터의 주 DNS 접미사 트가 있는 도메인의 FQDN 일치 하지 않는](https://go.microsoft.com/fwlink/p/?linkid=98848)을 참조 하십시오.

또한 조직 내에 배포된 모든 DNS 네임스페이스를 DNS 접미사 검색 목록에 포함하려면 도메인에 있는 연결되지 않은 각 컴퓨터에 대한 검색 목록을 구성해야 합니다. 네임스페이스 목록에는 도메인 컨트롤러의 주 DNS 접미사와 DNS 도메인 이름뿐 아니라 Exchange가 상호 작용할 수 있는 다른 서버(모니터링 서버 또는 타사 응용 프로그램용 서버 등)의 추가 네임스페이스도 포함되어야 합니다. 이 작업은 도메인에 대한 그룹 정책을 설정하여 수행할 수 있습니다. 그룹 정책에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [그룹 정책 자주 묻는 질문 (FAQ)](https://go.microsoft.com/fwlink/p/?linkid=100128)

  - [Windows Server 2003의 DNS에 대한 새 그룹 정책](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=294785)

  - [그룹 정책](https://go.microsoft.com/fwlink/p/?linkid=268043)

DNS 접미사 검색 목록 그룹 정책을 구성하는 방법에 대한 자세한 단계는 [분리 된 네임 스페이스에 대 한 DNS 접미사 검색 목록을 구성 합니다.](configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md)을 참조하십시오.

## Windows Server 2008을 실행 중인 컴퓨터의 DNS 및 NetBIOS 이름 관련 정보 보기

1.  **시작**을 클릭하고 **컴퓨터**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

2.  **시스템**에서 **전체 컴퓨터 이름** 옆의 **컴퓨터 이름, 도메인 및 작업 그룹 설정** 아래에 DNS 호스트 이름 및 주 DNS 접미사가 표시됩니다. **도메인** 옆에 DNS 도메인 이름이 표시됩니다.

3.  **설정 변경**을 클릭합니다.

4.  **시스템 속성**의 **컴퓨터 이름** 탭에서 **변경**을 클릭합니다.

5.  **컴퓨터 이름/도메인 변경**에서 **자세히**를 클릭합니다. **이 컴퓨터의 주 DNS 접미사** 아래에 주 DNS 접미사가 표시됩니다. **NetBIOS 컴퓨터 이름** 아래에 NetBIOS 컴퓨터 이름이 표시됩니다.
    
    주 DNS 접미사를 변경하려면 **이 컴퓨터의 주 DNS 접미사** 아래에 새로운 주 DNS 접미사를 입력한 다음 **확인**을 클릭합니다.

6.  명령 프롬프트 창에서 **set**를 입력합니다. 변수 USERDNSDOMAIN은 DNS 도메인 이름을 표시하고 변수 USERDOMAIN은 NetBIOS 도메인 이름을 표시합니다.

