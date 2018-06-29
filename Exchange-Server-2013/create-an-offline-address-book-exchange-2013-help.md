---
title: '오프 라인 주소록 만들기: Exchange 2013 Help'
TOCTitle: 오프 라인 주소록 만들기
ms:assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124339(v=EXCHG.150)
ms:contentKeyID: 50483972
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage
ms.translationtype: MT
---

# 오프 라인 주소록 만들기

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-24_

Exchange Server 2013의 OAB(오프라인 주소록)는 Outlook 사용자가 서버와의 연결이 끊어진 동안에도 정보에 액세스할 수 있도록 하는 다운로드된 주소록 복사본입니다. Exchange 관리자는 오프라인으로 작업하는 사용자가 사용할 수 있는 주소록을 결정할 수 있으며 웹 기반 배포, 공용 폴더 배포 등의 주소록 배포 방법을 구성할 수도 있습니다.

OAB와 관련된 추가 관리 작업에 대한 자세한 내용은 [오프 라인 주소록 절차](offline-address-book-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md)의 "오프라인 주소록" 항목

  - Exchange Online에서는 기본적으로 주소 목록 역할이 어떤 역할 그룹에도 할당되지 않습니다. 주소 목록 역할이 필요한 cmdlet을 사용하려면 역할 그룹에 이 역할을 추가해야 합니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 항목의 "역할 그룹에 역할 추가" 섹션을 참조하세요.

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 웹 기반 배포로 OAB 만들기

이 예에서는 기본 가상 디렉터리를 사용하여 Outlook 2007 이상의 클라이언트에 대해 웹 기반 배포를 사용하는 OAB\_Contoso라는 OAB를 만듭니다.

    New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List" -VirtualDirectories $Null -GlobalWebDistributionEnabled $True

구문과 매개 변수에 대한 자세한 내용은 [New-OfflineAddressBook](https://technet.microsoft.com/ko-kr/library/bb123692\(v=exchg.150\))을 참조하십시오.

