---
title: 'Exchange 검색 및 원본 위치 eDiscovery에 대 한 IRM 구성: Exchange 2013 Help'
TOCTitle: Exchange 검색 및 원본 위치 eDiscovery에 대 한 IRM 구성
ms:assetid: d96790e9-93ad-4a56-b90f-2dbfa2f2073c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg588319(v=EXCHG.150)
ms:contentKeyID: 50484265
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 검색 및 원본 위치 eDiscovery에 대 한 IRM 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-16_

Microsoft Exchange Server 2013, Exchange 검색 IRM으로 보호 된 메시지를 인덱싱할 수 있도록 정보 권한 관리 (IRM)를 구성할 수 있습니다.

검색 관리 역할 그룹의 구성원 [원본 위치 eDiscovery](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery) 검색을 수행 하는 경우 IRM으로 보호 된 메시지 검색 결과에 반환 되며 검색에 지정 된 검색 사서함으로 복사 됩니다. 또한, 검색 관리 역할 그룹의 구성원 검색 검색의 결과 검색 사서함으로 복사 된 IRM으로 보호 된 메시지에 액세스 하려면 Outlook Web App 를 사용할 수 있습니다.


> [!NOTE]
> 검색 관리 역할 그룹의 구성원 다른 사서함 또는.pst 파일 검색 사서함에서 내보낸 IRM으로 보호 된 메시지에 액세스할 수 없습니다. IRM으로 보호 된 메시지를 검색 사서함에 Outlook Web App 를 통해서만 액세스할 수 있습니다.



IRM과 관련된 추가 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "권한 보호" 항목

  - Exchange 2013 조직에서 IRM은 구성 해야 합니다. 자세한 내용은 [내부 메시지에 대 한 IRM을 사용 하지 않도록 설정 하거나 사용](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)를 참조 하십시오.

  - 페더레이션 사서함 Active Directory 권한 관리 서비스 (AD RMS) 고급 사용자 그룹에 추가 되어야 합니다. 자세한 내용은 [AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)를 참조 하십시오.

  - Exchange 관리 센터 (EAC)를 사용 하 여 Exchange 검색 및 원본 위치 eDiscovery에 대해 IRM을 구성할 수는 없습니다. 셸을 사용 해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용 하 여 Exchange 검색에 대 한 IRM을 구성 하려면

이 예에서는 Exchange 검색 인덱스를 IRM으로 보호 된 메시지를 허용 하도록 IRM 구성 합니다.


> [!NOTE]
> 기본적으로 <EM>SearchEnabled</EM> 매개 변수는 <CODE>$true</CODE>로 설정 됩니다. IRM으로 보호 된 메시지의 인덱싱을 사용 하지 않으려면 <CODE>$false</CODE>로 설정 합니다. IRM으로 보호 된 메시지의 인덱싱을 사용 하지 않도록 설정 하거나 검색 관리자에서 원본 위치 eDiscovery를 사용 하 여 사용자가 자신의 사서함을 검색 하는 경우 검색 결과에 반환 되지 않습니다.



    Set-IRMConfiguration -SearchEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\))를 참조하십시오.

## 셸을 사용 하 여 원본 위치 eDiscovery에 대해 IRM을 구성 하려면

검색 사서함에 있는 IRM으로 보호 된 메시지에 액세스 하려면 검색 관리 역할 그룹의 구성원을 설정 하는이 예제입니다.


> [!NOTE]
> 기본적으로 <EM>EDiscoverySuperUserEnabled</EM> 매개 변수는 <CODE>$true</CODE>로 설정 됩니다. 검색 관리 역할 그룹의 구성원에 대 한 IRM으로 보호 된 메시지에 대 한 액세스를 사용 하지 않도록 설정, <CODE>$false</CODE>를 설정 합니다.



    Set-IRMConfiguration -EDiscoverySuperUserEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

Exchange 검색 하 고 원본 위치 eDiscovery에 대 한 IRM을 성공적으로 구성 했는지를 확인 하려면 IRM 구성 정보를 검색 하려면 **Get-IRMConfigurtaion** cmdlet을 사용 합니다. IRM 구성을 검색 하는 방법의 예 **Get-IRMConfiguration**에서 [예](https://technet.microsoft.com/ko-kr/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) 를 참조 하십시오.

