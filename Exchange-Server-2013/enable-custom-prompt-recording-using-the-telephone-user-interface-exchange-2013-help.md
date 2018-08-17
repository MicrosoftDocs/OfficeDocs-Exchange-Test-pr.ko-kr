---
title: '전화 사용자 인터페이스를 사용 하 여 사용자 지정 프롬프트 기록 사용: Exchange 2013 Help'
TOCTitle: 전화 사용자 인터페이스를 사용 하 여 사용자 지정 프롬프트 기록 사용
ms:assetid: f2e5c636-2be9-4d48-b5e7-37913ded62d1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb691404(v=EXCHG.150)
ms:contentKeyID: 54651844
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전화 사용자 인터페이스를 사용 하 여 사용자 지정 프롬프트 기록 사용

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2014-09-17_

셸을 사용 하 여 사용자 지정 음성 안내의 녹음/녹화를 사용 하도록 설정 하 고 인사말에 대 한 UM (통합 메시징) 다이얼 플랜 및 자동 전화 교환 (TUI)의 전화 사용자 인터페이스를 사용 하 여 키를 누릅니다. EAC 또는 셸을 사용 하 여 사용자 지정 인사말 또는 알림 변경 하려는 경우 또는 심각한 날씨로 인해 조직 닫기와 같은 응급 때 유용할 수 있습니다. 사용자 지정 인사말 또는 UM 자동 전화 교환에 대 한 알림을 변경 하는 경우 UM 자동 전화 교환에 연결 된 다이얼 플랜에 TUI prompt 기록을 사용 하도록 설정 해야 합니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 및 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용 하 여 사용자 지정 음성 안내 또는 인사말 TUI를 사용 하 여 녹음/녹화를 사용 하도록 설정 하려면

사용자 지정 음성 안내 하 고 인사말 (TUI)의 전화 사용자 인터페이스를 사용 하 여를 기록 하려면 다음이 단계를 따릅니다.

1.  대화형으로 로그온 할 수 없는 도메인 사용자 계정을 만듭니다.

2.  도메인 사용자 계정에 Exchange 조직 관리자 역할을 위임 합니다.

3.  도메인 사용자에 대 한 사서함을 만듭니다.

4.  통합 메시징에 대 한 도메인 사용자의 사서함을 사용 합니다.
    

    > [!IMPORTANT]
    > 인사말 및 음성 안내를 관리 하는 관리자만 허용 사용자 계정에 대 한 내선 번호와 PIN에 대 한 액세스 합니다. 이 사용자 계정을 사용 하 여 전화를 통해 음성 안내 관리에 대해서만.



5.  페이지를 만들고 자동 전화 교환 또는 UM 다이얼 플랜에 대 한 사용자 지정 인사말에 사용할.wav 또는.wma 파일을 저장 합니다.
    

    > [!NOTE]
    > 사용자 지정 음성 안내에 대 한 MP3 파일을 사용할 수 없습니다.



6.  EAC 또는 셸의 사용 하 여 사용자 지정 환영 인사말을 사용 하거나 비즈니스 또는 업무 시간 외 인사말을 사용 하 여 자동 전화 교환을 구성할 다이얼 플랜을 구성 합니다. 다이얼 플랜을 구성 하는 방법에 대 한 자세한 내용은, [Outlook Voice Access 사용자에 대 한 사용자 지정된 인사말을 사용 하도록 설정](enable-a-customized-greeting-for-outlook-voice-access-users-exchange-2013-help.md)을 참조 하십시오. 자동 전화 교환을 구성 하는 방법에 대 한 자세한 내용은, [사용자 지정 된 업무 시간 인사말을 사용 하도록 설정](enable-a-customized-business-hours-greeting-exchange-2013-help.md) 또는 [한 사용자 지정 된 업무 시간 외 인사말을 사용 하도록 설정](enable-a-customized-non-business-hours-greeting-exchange-2013-help.md)를 참조 하십시오.

7.  다음 cmdlet을 실행합니다.
    
        Set-UMDialPlan -identity MyUMDialPlan -TUIPromptEditingEnabled $true


> [!NOTE]
> 사용자 지정 음성 안내의 녹음/녹화를 사용 하도록 설정할 수 전이나 용으로 설정 하는 사서함에 로그인 해야 인사말을 녹음/녹화 메시지를 표시 합니다. 후 새 프롬프트를 기록 또는 인사말 필요한 경우 해야 로그 아웃 한 다음 다시 로그인 전에 TUI를 사용 하면 새 프롬프트 또는 인사말을 들 수 있습니다.



## UM 자동 전화 교환에 TUI prompt 녹음/녹화를 수행 합니다.

1.  자동 전화 교환 TUI prompt 녹음/녹화에 대 한 사용 하도록 설정 했을 때 다이얼 플랜에 연결 된 있는지 확인 합니다.

2.  UM 자동 전화 교환에 구성 된 된 전화번호를 호출 합니다.

3.  비 비즈니스 또는 업무 시간 동안 파운드 키를 눌러 재생 되 고 자동 전화 교환에 대 한 인사말 (\#)를 한 다음 별표 (\*) 키를 누릅니다.

4.  사용자에 대 한 내선 번호를 입력 하 라는 메시지가 표시 됩니다. TUI prompt 녹음/녹화를 수행할 수 있는 권한이 UM 사용이 가능한 사용자의 내선 번호를 입력 합니다.

5.  PIN에 대 한 하 라는 메시지가 표시 됩니다. 사용자의 PIN을 입력 합니다.

6.  지시에 따라 시스템을 편집 하거나 자동 전화 교환에 대 한 인사말 또는 정보 알림 업데이트 합니다.

## UM 다이얼 플랜에서 TUI prompt 녹음/녹화를 수행 합니다.

1.  Outlook Voice Access에 로그인을 사용 하 여 Outlook Voice Access 번호를 호출 합니다.

2.  환영 인사말 재생 되는 다이얼 플랜에 대 한을 하는 동안 파운드 키를 누릅니다 (\#)를 한 다음 별표 (\*) 키를 누릅니다.

3.  UM 사용이 가능한 사용자가 사용 되는 전화에서 전화 걸 PIN에 대 한 라는 메시지가 표시 됩니다. PIN을 입력 하는 대신 별표 (\*) 키를 누릅니다. 내선 번호에 대 한 하 라는 메시지가 표시 됩니다. TUI prompt 녹음/녹화를 수행할 수 있는 권한이 UM 사용이 가능한 사용자의 내선 번호를 입력 합니다.

4.  UM 사용이 가능한 사용자가 사용 되지 않은 전화에서를 호출 하는 경우 내선 번호에 대 한 메시지가 표시 되 자동으로 표시 됩니다. TUI prompt 녹음/녹화를 수행할 수 있는 권한이 UM 사용이 가능한 사용자의 내선 번호를 입력 합니다.

5.  PIN에 대 한 하 라는 메시지가 표시 됩니다. 사용자의 PIN을 입력 합니다.

6.  지시에 따라 시스템을 편집 하거나 다이얼 플랜 또는 정보 알림을 대 한 환영 인사말을 업데이트 합니다.

