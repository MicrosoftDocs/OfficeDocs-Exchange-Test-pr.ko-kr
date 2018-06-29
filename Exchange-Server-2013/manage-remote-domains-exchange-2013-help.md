---
title: '원격 도메인 관리: Exchange 2013 Help'
TOCTitle: 원격 도메인 관리
ms:assetid: 41a86907-bd9e-40d0-94d3-6deb95a0bffa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997639(v=EXCHG.150)
ms:contentKeyID: 52057944
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewRemoteDomainWizardForm.NewRemoteDomainWizardPage
ms.translationtype: MT
---

# 원격 도메인 관리

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-13_

원격 도메인은 Microsoft Exchange 조직 외부에 있는 SMTP 도메인입니다. 원격 도메인 항목을 만들어 Exchange 조직과 특정 외부 도메인 간에 전송되는 메시지에 대한 설정을 정의할 수 있습니다. 특정 외부 도메인에 대한 원격 도메인 항목의 설정은 모든 외부 받는 사람에게 보통 적용되는 기본 원격 도메인의 설정보다 우선합니다. 원격 도메인 설정은 Exchange 조직 전체에 적용됩니다.

원격 도메인 항목을 제거하면 메시지 전송 설정이 원격 도메인에 보낸 메시지에 더 이상 적용되지 않습니다. 원격 도메인 항목을 제거해도 해당 원격 도메인으로 메일 흐름이 유지됩니다. 원격 도메인 항목이 제거된 후에는 기본 원격 도메인의 구성 설정이 해당 도메인으로 보낸 새 메시지에 적용됩니다. 기본 원격 도메인은 제거할 수 없습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "원격 도메인" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 조직에서 허용 도메인으로 구성된 주소 공간에 대한 원격 도메인은 만들 수 없습니다. 예를 들어 조직에서 fabrikam.com의 메일을 허용하는 경우 fabrikam.com에 대한 원격 도메인을 만들 수 없습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 수행할 작업

## 셸을 사용하여 원격 도메인 만들기

새 원격 도메인 항목을 만들려면 다음 구문을 사용합니다.

    New-RemoteDomain -Name <Descriptive Name> -DomainName <SMTP address space>

이 예에서는 contoso.com 도메인으로 보내는 메시지에 대한 원격 도메인 항목을 만듭니다.

    New-RemoteDomain -Name Contoso -DomainName contoso.com

이 예에서는 fabrikam.com 도메인 및 모든 하위 도메인으로 보내는 메시지에 대한 원격 도메인 항목을 만듭니다.

    New-RemoteDomain -Name Fabrikam -DomainName *.fabrikam.com

## 작동 여부는 어떻게 확인합니까?

원격 도메인을 만들었는지 확인하려면 다음을 수행합니다.

1.  **Get-RemoteDomain** 명령을 실행하여 원격 도메인이 나열되는지 확인합니다.

2.  `Get-RemoteDomain <Remote Domain Name> | Format-List` 명령을 실행하여 새 원격 도메인의 설정을 확인합니다. 새 원격 도메인 항목에서 지정된 주소 공간의 받는 사람에게 테스트 메시지를 보내고 메시지 설정이 새 원격 도메인 항목에서 지정된 설정과 일치하는지 확인합니다.

## 셸을 사용하여 원격 도메인 구성

**Set-RemoteDomain** cmdlet을 사용하여 원격 도메인 항목의 설정을 구성할 수 있습니다. 자동 회신, 메시지 형식 및 인코딩, 기타 메시지 설정과 관련한 여러 설정이 있습니다. 자세한 내용은 [Set-RemoteDomain](https://technet.microsoft.com/ko-kr/library/aa997857\(v=exchg.150\))을 참조하십시오.

특정 시나리오에 대해 원격 도메인을 구성하려면 다음 항목을 참조하십시오.

  - [부재중 회신 원격 도메인 구성](configure-remote-domain-out-of-office-replies-exchange-2013-help.md)

  - [자동 회신을 원격 도메인 구성](configure-remote-domain-automatic-replies-exchange-2013-help.md)

  - [원격 도메인 메시지 보고 구성](configure-remote-domain-message-reporting-exchange-2013-help.md)

## 셸을 사용하여 원격 도메인 제거

원격 도메인 항목을 제거하려면 다음 구문을 사용합니다.

    Remove-RemoteDomain <RemoteDomainName>

이 예에서는 원격 도메인 항목 Contoso를 제거합니다.

    Remove-RemoteDomain Contoso

## 작동 여부는 어떻게 확인합니까?

원격 도메인이 제거되었는지 확인하려면 다음을 수행합니다.

1.  **Get-RemoteDomain** 명령을 실행하여 원격 도메인이 나열되지 않는지 확인합니다.

2.  `Get-RemoteDomain Default | Format-List` 명령을 실행하여 기본 원격 도메인의 설정을 확인합니다. 제거된 원격 도메인에서 지정된 주소 공간의 받는 사람에게 테스트 메시지를 보내고 메시지 설정이 기본 원격 도메인 항목에서 지정된 설정과 일치하는지 확인합니다.

