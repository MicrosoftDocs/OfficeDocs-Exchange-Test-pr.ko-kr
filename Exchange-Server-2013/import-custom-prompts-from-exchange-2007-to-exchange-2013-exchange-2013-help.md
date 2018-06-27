---
title: 'Exchange 2013을 Exchange 2007에서 사용자 지정 음성 안내 가져오기: Exchange 2013 Help'
TOCTitle: Exchange 2013을 Exchange 2007에서 사용자 지정 음성 안내 가져오기
ms:assetid: 70c0b0bc-c0de-4e3c-8144-1fe59f86ebf4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg309147(v=EXCHG.150)
ms:contentKeyID: 54651819
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013을 Exchange 2007에서 사용자 지정 음성 안내 가져오기

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2015-04-08_

Exchange 2007 UM(통합 메시징)의 사용자 지정 인사말, 알림, 메뉴 및 음성 안내 등을 포함하는 오디오 파일을 Exchange 2013 통합 메시징으로 가져올 수 있습니다. 셸 스크립트를 사용하면 음성 안내를 {e0dc1c29-89c3-4034-b678-e6c29d823ed9}라는 Exchange 시스템 사서함으로 가져오게 되며, 이 사서함은 Microsoft Exchange 2013 설치 시 만들어집니다. 이 시스템 사서함은 통합 메시징에서 다이얼 플랜, 자동 전화 교환 사용자 지정 인사말, 알림, 메뉴, 음성 안내 및 UM 보고서를 저장하는 데 사용됩니다.

.wav 또는 .wma 형식의 오디오 파일은 다음과 같이 사용됩니다.

  - UM 다이얼 플랜에서는 오디오 파일이 사용자 지정 환영 인사말 및 정보 알림에 사용됩니다. Outlook Voice Access 사용자가 Outlook Voice Access 번호로 전화를 걸면 해당 오디오 파일이 재생됩니다.

  - UM 자동 전화 교환에서 오디오 파일은 사용자 지정된 업무 시간 및 업무 시간 외 환영 인사말, 정보 알림, 메뉴 음성 안내 및 탐색 메뉴에 사용되며, 발신자가 UM 자동 전화 교환으로 전화를 걸면 해당 오디오 파일이 재생됩니다.

MigrateUMCustomPrompts.ps1 스크립트를 사용하여 모든 Exchange Server 2007 UM 사용자 지정 인사말, 알림, 메뉴 및 음성 안내 복사본을 모든 Exchange 2007 UM 다이얼 플랜 및 UM 자동 전화 교환용 Exchange 2013 UM으로 마이그레이션할 수 있습니다.

MigrateUMCustomPrompts.ps1 스크립트는 기본적으로 Exchange 2013 서버의 \<Program Files\>\\Microsoft\\Exchange Server\\V15\\Scripts 폴더에 있습니다.


> [!NOTE]
> MigrateUMCustomPrompts.ps1 스크립트는 Exchange 2013에 포함되어 있으며, Exchange 2007 UM 서버와 같은 조직의 Exchange 2013 사서함 서버에서 실행되어야 합니다.



다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "UM 다이얼 플랜" 및 "UM 자동 전화 교환? [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 의 항목입니다.

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## MigrateUMCustomPrompts.ps1 스크립트를 사용하여 UM 다이얼 플랜 및 자동 전화 교환에 대한 모든 사용자 지정 음성 안내의 복사본 마이그레이션

1.  **시작** \> **모든 프로그램** \> **Microsoft Exchange Server 2013** \> **Exchange 관리 셸**을 클릭합니다.

2.  셸 프롬프트에 스크립트 경로를 입력합니다. 예를 들어, **cd "D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"**를 입력하고 Enter 키를 누릅니다.

3.  셸 프롬프트에 **".\\MigrateUMCustomPrompt"**를 입력한 다음 Enter 키를 누릅니다.

