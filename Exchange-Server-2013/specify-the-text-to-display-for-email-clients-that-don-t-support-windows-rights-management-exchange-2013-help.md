---
title: 'Windows 권한 관리를 지원 하지 않는 전자 메일 클라이언트에 대해 표시할 텍스트를 지정 합니다.: Exchange 2013 Help'
TOCTitle: Windows 권한 관리를 지원 하지 않는 전자 메일 클라이언트에 대해 표시할 텍스트를 지정 합니다.
ms:assetid: a9b2238a-b534-469c-a0c3-2768bc3d005b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423552(v=EXCHG.150)
ms:contentKeyID: 52058023
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows 권한 관리를 지원 하지 않는 전자 메일 클라이언트에 대해 표시할 텍스트를 지정 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

사용자가 보호된 음성 메시지를 받았는데 전자 메일 클라이언트가 IRM(정보 권한 관리) 또는 Windows Rights Management를 지원하지 않는 경우 사용자에게 전송되는 텍스트를 지정할 수 있습니다.

Windows Rights Management를 지원하는 전자 메일 클라이언트를 통해서나, UM 사용 가능 사용자가 Outlook Voice Access를 사용해 보호된 음성 메시지에 액세스하는 경우에는 보호된 음성 메일에 액세스할 수 있습니다.

보호된 음성 메일은 암호화됩니다. 음성 메시지가 보호된 경우에는 다음이 적용됩니다.

  - Microsoft Outlook 및 Outlook Web App에서 메시지가 비공개로 표시됩니다.

  - 음성 메시지는 받는 사람만이 열 수 있습니다.

  - 받는 사람은 음성 메시지에 회신할 수 있지만 원래 음성 메시지에 포함되지 않은 사람에게는 음성 메시지를 전달할 수 없습니다.

전자 메일 클라이언트가 Windows Rights Management를 지원하지 않으며 Outlook Voice Access를 사용해 메시지에 액세스하지 않는 사람에게 보호된 음성 메시지를 보내면 지정한 텍스트가 포함된 전자 메일 메시지가 해당 받는 사람에게 전송됩니다. 이 텍스트에는 수신자가 보호된 음성 메시지를 받기 위해 해야 할 작업에 대한 지침이 들어 있습니다.

보호된 음성 메일 절차와 관련된 추가 관리 작업에 대한 자세한 내용은 [보호 된 음성 메일 절차](protected-voice-mail-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 Windows Rights Management를 지원하지 않는 전자 메일 클라이언트에 표시할 텍스트 지정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 관리할 UM 사서함 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지 \> **보호된 음성 메일**의 **Windows Rights Management가 지원되지 않는 사용자에게 보낼 메시지** 아래 텍스트 상자에 메시지 텍스트를 입력합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 Windows Rights Management를 지원하지 않는 전자 메일 클라이언트에 표시할 텍스트 지정

이 예에서는 UM 사서함 정책 `MyUMMailboxPolicy`에 연결되어 있으며 Windows Rights Management를 지원하지 않는 전자 메일 클라이언트를 사용하는 사용자에게 표시할 텍스트를 지정합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectedVoiceMailText "Your email client software does not support Protected Voice Mail. Please contact the Help Desk."

