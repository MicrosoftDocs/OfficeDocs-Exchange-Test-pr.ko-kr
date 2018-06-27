---
title: '오프 라인 주소록 배포 속성 구성: Exchange 2013 Help'
TOCTitle: 오프 라인 주소록 배포 속성 구성
ms:assetid: 8df985e9-75ba-47ea-9cc3-aa98a5d8acf4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123710(v=EXCHG.150)
ms:contentKeyID: 50483648
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.ClientAccess.OabDistributionGeneralPage
ms.translationtype: MT
---

# 오프 라인 주소록 배포 속성 구성

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-14_

Exchange의 각 OAB(오프라인 주소록) 배포 지점에 대해 내부 회사 네트워크에서만 액세스할 수 있는 내부 URL과 인터넷에서 액세스할 수 있는 외부 URL의 두 가지 URL을 구성할 수 있습니다.

OAB와 관련된 추가 관리 작업에 대한 자세한 내용은 [오프 라인 주소록 절차](offline-address-book-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "오프라인 주소록" 항목

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 OAB 배포 속성 구성

이 예에서는 OAB 가상 디렉터리 OAB(기본 웹 사이트)의 OAB 배포 폴링 간격을 6시간으로 설정합니다.

    Set-OABVirtualDirectory "OAB (Default Web Site)" -PollInterval 360

이 예에서는 기본 OAB 가상 디렉터리 OAB(기본 웹 사이트)의 외부 배포 지점을 https://contoso.com/OAB로 설정합니다.

    Set-OABVirtualDirectory "OAB (Default Web Site)" -ExternalUrl https://contoso.com/OAB

구문과 매개 변수에 대한 자세한 내용은 [Set-OabVirtualDirectory](https://technet.microsoft.com/ko-kr/library/bb124707\(v=exchg.150\))를 참조하십시오.

## 자세한 내용

[오프라인 주소록](offline-address-books-exchange-2013-help.md)

