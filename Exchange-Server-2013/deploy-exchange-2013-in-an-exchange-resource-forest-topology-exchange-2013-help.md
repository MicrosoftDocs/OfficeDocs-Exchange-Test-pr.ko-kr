---
title: 'Exchange 리소스 포리스트 토폴로지에서 Exchange 2013 배포: Exchange 2013 Help'
TOCTitle: Exchange 리소스 포리스트 토폴로지에서 Exchange 2013 배포
ms:assetid: 537a7b2b-d002-40a6-84ae-fd02635f9e23
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998031(v=EXCHG.150)
ms:contentKeyID: 51407696
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 리소스 포리스트 토폴로지에서 Exchange 2013 배포

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

이 항목에서는 Microsoft Exchange 2013Exchange 리소스 포리스트 토폴로지에서 배포 하는 방법에 설명 합니다. Exchange 리소스 포리스트는 전용된 Exchange 포리스트를 라고도 합니다. 이 항목에서는 기존 Exchange 2013 토폴로지를 없는 가정 합니다.

다음 그림은 리소스 포리스트가 있는 Exchange 조직을 보여줍니다.

**Exchange 리소스 포리스트가 있는 Exchange 조직의 예**

![리소스 포리스트가 있는 복잡한 Exchange 조직](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "리소스 포리스트가 있는 복잡한 Exchange 조직")

## 시작하기 전에 알아야 할 내용

Exchange 2013 에서 다음 절차를 수행 하려면 다음을 확인 합니다.

  - 다음 두 개의 Active Directory 포리스트가 있습니다.
    
      - 두 포리스트 중 하나에는 조직에 대한 사용자 계정이 있습니다. 이 절차에서는 이 포리스트를 *계정 포리스트*라고 합니다.
    
      - 하나의 사용자 계정은 포함 하지 않습니다 포리스트와 아직 되지 않은 Exchange 설치 합니다. 이 절차에서는이 포리스트에 *Exchange 포리스트*라고 합니다. 절차를 사용 하 여 Exchange 2013 이 포리스트에 설치 됩니다.

  - 올바르게 구성한 상태 여야 시스템 DNS (Domain Name) 이름 확인을 위한 포리스트 전체 조직에서 합니다. DNS를 올바르게 구성 했는지를 확인 하려면 다른 포리스트 또는 조직에서 포리스트에서 각 포리스트에 ping을 수행 합니다. DNS를 구성 하는 방법에 대 한 자세한 내용은 [DNS 서버 운영 가이드](https://go.microsoft.com/fwlink/p/?linkid=282295)를 참조 하십시오.

## Exchange 리소스 포리스트 토폴로지에서 Exchange 2013 배포

1.  Exchange 포리스트의 도메인 컨트롤러에서 계정 포리스트를 신뢰 하는 Exchange 포리스트 있도록 단방향 보내는 트러스트를 만듭니다. 자세한 단계는 [트러스트의 양쪽 모두에 대 한 단방향, 보내는, 포리스트 트러스트 만들기](https://go.microsoft.com/fwlink/p/?linkid=69130)을 참조 하십시오.
    

    > [!NOTE]
    > 포리스트 트러스트를 만드는 것이 좋지만 포리스트 트러스트 또는 외부 트러스트 중 하나를 만들어도 됩니다. 외부 트러스트를 만드는 경우 3단계에서 연결된 사서함을 만들 때 새 사서함 마법사의 <STRONG>마스터 계정</STRONG> 페이지에서 트러스트된 포리스트의 도메인 컨트롤러에 액세스할 수 있는 사용자 계정을 지정해야 합니다. 현재 로그온할 때 사용된 자격 증명은 사용할 수 없습니다. <STRONG>New-Mailbox</STRONG> cmdlet을 사용하여 연결된 사서함을 만드는 경우에는 <EM>LinkedCredential</EM> 매개 변수를 사용하여 트러스트된 포리스트의 도메인 컨트롤러에 액세스할 수 있는 사용자 계정을 지정해야 합니다.



2.  Exchange 포리스트에 Exchange 2013 를 설치 합니다. 단일 포리스트 시나리오에서 Exchange 경우에 동일한 방식으로 설치 합니다. Exchange 2013 를 설치 하는 방법에 대 한 자세한 단계는 다음 항목 중 하나를 참조 합니다.
    
      - [Exchange 2013 새 설치 배포](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [설치 마법사를 사용하여 Exchange 2013 설치](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

3.  Exchange 포리스트의 Exchange 포리스트에 있는 사서함을 갖습니다 계정 포리스트에 있는 각 사용자에 대 한 외부 계정과 연결 된 사서함을 만듭니다. 자세한 단계 [연결 된 사서함 관리](manage-linked-mailboxes-exchange-2013-help.md)를 참조 하십시오.

