---
title: '외부 전자 메일 관리자 주소를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 외부 전자 메일 관리자 주소를 구성 합니다.
ms:assetid: 6b0c8675-3238-462d-8973-b52305fb90d2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb430765(v=EXCHG.150)
ms:contentKeyID: 52058084
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 외부 전자 메일 관리자 주소를 구성 합니다.

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

외부 전자 메일 관리자 주소는 Microsoft Exchange Server 2013 조직 외부에 있는 메시지 보낸 사람에게 시스템 생성 메시지 및 알림을 보내는 보낸 사람으로 사용됩니다. 외부 보낸 사람은 조직의 허용 도메인으로 구성되지 않은 도메인에 전자 메일 주소가 있는 모든 보낸 사람입니다.

기본적으로 외부 전자 메일 관리자 주소 설정 값은 비어 있습니다. 이 기본값은 Exchange 조직에서 다음과 같이 동작합니다.

  - 모든 사서함 서버 및 가입된 Edge 전송 서버에 대해 외부 전자 메일 관리자 주소는 postmaster@\<*기본 허용 도메인*\>이 됩니다.

  - 가입되지 않은 모든 Edge 전송 서버에 대해 외부 전자 메일 관리자 주소는 postmaster@\<*Edge Transport server FQDN*\>이 됩니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 구성" 항목

  - 사용자 지정 외부 전자 메일 관리자 주소를 구성할 경우 해당 값은 Exchange 조직의 모든 Exchange 2013 사서함 서버 및 Exchange 2010 허브 전송 서버에 적용됩니다. 단, 이 값은 Edge 전송 서버에는 복제되지 않습니다. 외부 전자 메일 관리자 주소의 사용자 지정 값을 지정하는 경우 모든 Edge 전송 서버에 대해 외부 전자 메일 관리자 주소 값을 수동으로 구성해야 합니다.

  - 조직에서 모든 Exchange 2007 허브 전송 서버 또는 Edge 전송 서버를 포함 하는 경우 **Set-TransportServer** cmdlet을 사용 하 여 이러한 서버 중 하나에 각 사용자 지정 외부 전자 메일 관리자 주소를 구성 해야 합니다. 자세한 내용은 [외부 전자 메일 관리자 주소 관리](https://go.microsoft.com/fwlink/?linkid=279922)를 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 외부 전자 메일 관리자 주소 구성

1.  EAC에서 **메일 흐름** \> **수신 커넥터** \> **기타 옵션**![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘") \> **조직 전송 설정** \> **배달** 탭으로 이동합니다.

2.  **외부 전자 메일 관리자 주소** 필드에 SMTP 전자 메일 주소를 입력합니다(예: `postmaster@contoso.com`). 외부 전자 메일 관리자 주소를 기본값으로 되돌리려면 기존 값을 삭제하여 필드를 비웁니다.

3.  작업을 마친 후 **저장**을 클릭합니다.

## 셸을 사용하여 외부 전자 메일 관리자 주소 구성

외부 전자 메일 관리자 주소를 구성하려면 다음 구문을 사용합니다.

    Set-TransportConfig -ExternalPostmasterAddress <postmaster address>

예를 들어 외부 전자 메일 관리자 주소를 `postmaster@contoso.com` 값으로 설정하려면 다음 명령을 실행합니다.

    Set-TransportConfig -ExternalPostmasterAddress postmaster@contoso.com

외부 전자 메일 관리자 주소를 기본값으로 되돌리려면 다음 명령을 실행합니다.

    Set-TransportConfig -ExternalPostmasterAddress $null

## 작동 여부는 어떻게 확인합니까?

외부 전자 메일 관리자 주소가 구성되었는지 확인하려면 다음을 수행합니다.

1.  사서함 서버에 대해 다음 명령을 실행하여 외부 전자 메일 관리자 주소 값을 확인합니다.
    
        Get-TransportConfig | Format-List ExternalPostmasterAddress

2.  외부 전자 메일 계정에서 DSN(배달 상태 알림)을 생성하는 Exchange 조직으로 메시지를 보냅니다. 예를 들어 해당 보낸 사람의 특정 키워드가 포함된 메시지에 대해 배달 못 함 보고서(NDR)를 보내도록 전송 규칙을 구성할 수 있습니다. DSN의 보낸 사람 전자 메일 주소가 지정한 값과 일치하는지 확인합니다.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

