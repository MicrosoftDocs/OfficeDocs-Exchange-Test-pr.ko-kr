---
title: '사이트 사서함 프로 비전 정책 관리: Exchange 2013 Help'
TOCTitle: 사이트 사서함 프로 비전 정책 관리
ms:assetid: 2f160d1a-a031-461f-8d29-c9cd49ca1645
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ710340(v=EXCHG.150)
ms:contentKeyID: 50482792
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사이트 사서함 프로 비전 정책 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-21_

사이트 사서함 프로비전 정책은 사이트 사서함 내외로 전송되는 전자 메일과 Exchange 서버의 사이트 사서함 크기에만 적용됩니다.

사이트 사서함에 대한 자세한 내용은 [사이트 사서함](site-mailboxes-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md)의 "사이트 사서함" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

  - 사이트 사서함 프로비전 정책을 여러 개 만들 수 있지만 기본 프로비전 정책만 모든 사이트 사서함에 적용됩니다. 조직 내에 여러 정책을 적용할 수 없습니다.

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 사이트 사서함 프로비전 정책 만들기

이 예에서는 다음과 같은 설정이 있는 기본 프로비전 정책 SM\_ProvisioningPolicy를 만듭니다.

  - 사이트 사서함에 대한 경고 할당량은 9GB입니다.

  - 사서함 크기가 10GB에 도달하면 사이트 사서함이 메시지를 수신하지 못하게 됩니다.

  - 사이트 사서함에 전송할 수 있는 전자 메일 메시지의 최대 크기는 50MB입니다.

<!-- end list -->

    New-SiteMailboxProvisioningPolicy -Name SM_ProvisioningPolicy -IsDefault -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB -MaxReceiveSize 50MB

## 사이트 사서함 프로비전 정책의 설정 보기

이 예에서는 조직에 있는 모든 사이트 사서함 프로비전 정책에 대한 자세한 정보를 반환합니다.

    Get-SiteMailboxProvisioningPolicy | Format-List

이 예에서는 조직의 모든 정책을 반환하지만 어떤 정책이 기본 정책인지 식별하는 `IsDefault` 정보만 표시합니다.

    Get-SiteMailboxProvisioningPolicy | Format-List IsDefault

## 기존 사이트 사서함 프로비전 정책 변경

이 예에서는 Default라는 사이트 사서함 프로비전 정책을 사이트 사서함에서 최대 크기 25MB까지의 전자 메일 메시지를 수신할 수 있도록 변경합니다. Exchange를 설치하면 이름이 **Default**인 프로비전 정책이 만들어집니다.

    Set-SiteMailboxProvisioningPolicy -Identity Default -MaxReceiveSize 25MB

이 예에서는 경고 할당량을 9.5GB로 변경하고 보내기 및 받기 금지 할당량을 10GB로 변경합니다.

    Set-SiteMailboxProvisioningPolicy -Identity Default -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB

## 사이트 사서함 이름 접두사 구성

새 사이트 사서함을 만들면 기본적으로 해당 전자 메일 주소에 접두사가 붙습니다. 전자 메일 주소 접두사를 사용하면 사이트 사서함을 쉽게 검색 및 쿼리할 수 있고 사용자가 사이트 사서함을 확인하는 데에도 도움이 될 수 있습니다. 원하는 경우에는 접두사를 사용하지 않도록 설정하거나 Office 365의 테넌트 또는 온-프레미스 배포의 지정된 포리스트에 대해 접두사를 변경할 수 있습니다. 기본 접두사 동작을 적용하는 경우 Office 365에서 사이트 사서함을 만들면 기본 접두사 **SMO-**가 추가됩니다. 온-프레미스 배포에서 사이트 사서함을 만드는 경우의 접두사는 **SM-**입니다. 하이브리드 고객이 사이트 사서함을 두 위치에서 만든 다음 프레미스 간에 동기화하는 경우 충돌이 발생하지 않도록 하기 위해 이 두 프레미스 간의 기본 동작은 서로 다릅니다.

이 예에서는 *DefaultAliasPrefixEnabled* 매개 변수를 $false로 설정하여 접두사 이름 지정을 사용하지 않도록 설정합니다.

    Set-SiteMailboxProvisioningPolicy -Identity Default -DefaultAliasPrefixEnabled $false -AliasPrefix $null

이 예에서는 기본 프로비전 정책을 변경하고 *AliasPrefix*를 FOREST01로 설정합니다.


> [!NOTE]
> 여러 포리스트가 포함된 배포에서는 둘 이상의 포리스트에서 이름이 같은 사이트 사서함을 만든 경우 개체를 포리스트 간에 동기화할 때 충돌을 방지하기 위해 각 포리스트에서 서로 다른 접두사를 사용하는 것이 좋습니다.



    Set-SiteMailboxProvisioningPolicy -Identity Default -AliasPrefix FOREST01 -DefaultAliasPrefixEnabled $false


> [!NOTE]
> Exchange 온-프레미스와 Office 365를 모두 사용하는 하이브리드 배포에서는 모든 클라우드 기반 사이트 사서함을 만들 때 접두사 <STRONG>SMO-</STRONG>가 추가됩니다. 하이브리드 고객이 사이트 사서함을 두 위치에서 만든 다음 프레미스 간에 동기화하는 경우 충돌이 발생하지 않도록 하기 위해 Office 365 와 Exchange 온-프레미스의 접두사는 서로 다릅니다. AliasPrefix 매개 변수가 DefaultAliasPrefixEnabled 매개 변수보다 우선하므로 <EM>AliasPrefix</EM> 매개 변수를 null이 아닌 유효한 문자열로 설정하면 새 사이트 사서함 각각의 별칭 앞에 해당 문자열이 추가됩니다.



## 사이트 사서함 프로비전 정책 삭제

이 예에서는 Exchange 설치 중에 만들어진 기본 사이트 사서함 정책을 삭제합니다.

    Remove-SiteMailboxProvisioningPolicy -Identity Default


> [!IMPORTANT]
> <STRONG>Default</STRONG> 정책을 제거하려면 먼저 다른 기본 정책을 만들고 지정해야 합니다.



## 자세한 내용

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

[New-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/ko-kr/library/jj218647\(v=exchg.150\))

[Get-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/ko-kr/library/jj218617\(v=exchg.150\))

[Set-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/ko-kr/library/jj218624\(v=exchg.150\))

[Remove-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/ko-kr/library/jj218672\(v=exchg.150\))

