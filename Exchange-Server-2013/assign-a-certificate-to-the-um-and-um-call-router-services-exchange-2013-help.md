---
title: 'UM 및 UM 통화 라우터 서비스에 인증서 할당: Exchange 2013 Help'
TOCTitle: UM 및 UM 통화 라우터 서비스에 인증서 할당
ms:assetid: 8a900e5f-9779-4213-92d7-ec157b15fbc5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn205140(v=EXCHG.150)
ms:contentKeyID: 54651824
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 및 UM 통화 라우터 서비스에 인증서 할당

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-04-29_

EAC 또는 셸을 사용하여 특정 Exchange 서비스에 대해 자체 서명된, 내부 PKI(공개 키 인프라) 또는 상업용 타사 인증서를 할당할 수 있습니다. *Services* 매개 변수와 함께 **New-ExchangeCertificate** cmdlet을 사용하여 인증서를 Exchange 서비스에 할당할 경우 인증서를 Exchange 서비스에 할당하라는 메시지가 표시됩니다. EAC를 사용하여 인증서를 만들 때는에는 새 Exchange 인증서 마법사에 인증서를 Exchange 서비스에 할당하라는 메시지가 표시되지 않습니다. 인증서 속성을 편집하고 인증서를 할당할 서비스를 선택하여 인증서를 할당해야 합니다.

각 서비스마다 인증서 요구 사항이 다릅니다. 예를 들어 일부 서비스에서는 인증서의 **주체 이름** 또는 **주체 대체 이름** 상자에 서버 이름만 필요할 수 있지만 다른 서비스에서는 FQDN(정규화된 도메인 이름)이 필요할 수 있습니다. 사용하도록 설정하려는 서비스에서 필요한 대로 인증서 이름을 사용할 수 있는지 확인하십시오.


> [!WARNING]
> UM(통합 메시징)을 Microsoft Lync Server에 통합한 경우에는 자체 서명된 인증서를 사용할 수 없습니다.



통합 메시징용 인증서 관리와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 절차에 대 한 인증서를 배포합니다.](deploying-certificates-for-um-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "인증서 관리" 항목 및 [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 서비스" 항목 역시 해당 컴퓨터의 로컬 관리자 그룹 구성원인 계정을 사용하여 로그온해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 통합 메시징 및 UM 통화 라우터 서비스에 인증서 할당

1.  EAC에서 **서버** \> **인증서**로 이동합니다.

2.  목록 보기에서 통합 메시징 및 UM 통화 라우터 서비스에 할당할 인증서를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  *\<인증서 이름\>* 페이지에서 **서비스**를 선택한 후 **UM**, **UM 통화 라우터**를 선택합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 통합 메시징 및 UM 통화 라우터 서비스에 인증서 할당

이 예에서는 인증서를 통합 메시징 및 UM 통화 라우터 서비스에 할당합니다.

    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

