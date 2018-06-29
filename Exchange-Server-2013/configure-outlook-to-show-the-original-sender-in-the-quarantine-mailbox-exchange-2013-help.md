---
title: '격리 사서함에서 원래 보낸 사람을 표시하도록 Outlook 구성: Exchange 2013 Help'
TOCTitle: 격리 사서함에서 원래 보낸 사람을 표시하도록 Outlook 구성
ms:assetid: 9249425d-1b06-48a0-ad95-c4eefb641ff4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee861109(v=EXCHG.150)
ms:contentKeyID: 50483676
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 격리 사서함에서 원래 보낸 사람을 표시하도록 Outlook 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

스팸 격리는 합법적인 메시지를 받지 못할 위험을 줄여 주는 콘텐츠 필터 에이전트의 기능입니다. 스팸 격리는 스팸으로 식별되어 조직 내부의 사용자 사서함으로 배달되서는 안 되는 메시지의 임시 저장소 위치를 제공합니다.

메시지가 스팸 격리 임계값을 충족하는 경우 NDR(배달 못 함 보고서)에 래핑되고 스팸 격리 사서함으로 배달됩니다. 격리된 메시지는 격리 사서함에 NDR로 저장되므로 조직의 전자 메일 관리자 주소는 모든 메시지에 대해 보낸 사람: 주소로 나열됩니다. 그러나 필드 목록에 원래 보낸 사람 주소, 원래 받는 사람 주소 및 원래 SCL(스팸 지수)을 추가하면 복구하려는 메시지를 더욱 쉽게 찾을 수 있습니다.

기본적으로 이러한 필드는 Microsoft Outlook에서 선택할 수 없습니다. 메시지 보기에서 이러한 필드를 추가하려면 먼저 원래 보낸 사람, 원래 받는 사람 및 원래 SCL을 사용자가 선택할 수 있는 선택적 필드로 추가하는 Outlook 양식을 만들어야 합니다. 이 사용자 지정 양식을 만든 후 메시지 보기에 이러한 필드를 표시하도록 Outlook을 구성할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 이 절차의 예상 완료 시간: 15분

  - [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 주제의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "사서함 액세스" 항목.

  - 이 절차에서는 스팸 방지 격리 사서함을 구성해야 합니다. 자세한 내용은 [스팸 격리 사서함 구성](configure-a-spam-quarantine-mailbox-exchange-2013-help.md)을 참조하십시오.

  - 격리 사서함에 액세스 하려면 해당 사서함에 대 한 Outlook 프로필을 구성 하 고 Outlook을 사용 하 여 사서함을 열고 다음을 지정 해야 합니다. 구성 하 고 여러 Outlook 프로필을 사용 하는 방법에 대 한 자세한 내용은 [개요의 Outlook 전자 메일 프로필](https://go.microsoft.com/fwlink/p/?linkid=178975)을 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 1단계: 메모장을 사용하여 사용자 지정 Outlook 양식 만들기

1.  메모장을 열고 다음 코드를 문서에 복사합니다.
    
        [Description]
        MessageClass=IPM.Note
        CLSID={00020D31-0000-0000-C000-000000000046}
        DisplayName=Quarantine Extension Form
        Category=Standard
        Subcategory=Form
        Comment=This form allows the Original Sender (ReceivedRepresentingEmailAddress), Original Recipient (To), and Original SCL (OriginalScl) values to be viewed as columns.
        LargeIcon=IPML.ico
        SmallIcon=IPMS.ico
        Version=3.0
        Locale=enu
        Hidden=1
        Owner=Microsoft Corporation
        Contact=Your Name
        
        [Platforms]
        Platform1=Win16
        Platform2=NTx86
        Platform9=Win95
        
        [Platform.Win16]
        CPU=ix86
        OSVersion=Win3.1
        
        [Platform.NTx86]
        CPU=ix86
        OSVersion=WinNT3.5
        
        [Platform.Win95]
        CPU=ix86
        OSVersion=Win95
        
        [Properties]
        Property01=ReceivedRepresentingEmailAddress
        Property02=DisplayTo
        Property03=OriginalScl
        
        [Property.ReceivedRepresentingEmailAddress]
        Type=31
        NmidInteger=0x0078
        DisplayName=ReceivedRepresentingEmailAddress
        
        [Property.DisplayTo]
        Type=31
        NmidInteger=0x0E04
        DisplayName=DisplayTo
        
        [Property.OriginalScl]
        Type=3
        NmidPropset={41F28F13-83F4-4114-A584-EEDB5A6B0BFF}
        NmidString=OriginalScl
        DisplayName=OriginalScl
        
        [Verbs]
        Verb1=1
        
        [Verb.1]
        DisplayName=&Open
        Code=0
        Flags=0
        Attribs=2
        
        [Extensions]
        Extensions1=1
        
        [Extension.1]
        Type=31
        NmidPropset={00020D0C-0000-0000-C000-000000000046}
        NmidInteger=1
        Value=1000000000000000

2.  다음 값을 사용하여 Office 양식 폴더에 파일을 저장합니다.
    
      - **경로**   *\<Office Install Path\>*\\\<*OfficeVersion\>*\\Forms\\*\<LCID\>*
        
          - *\<Office Install Path\>*   32비트 버전의 Microsoft Windows에 32비트 버전의 Office를 설치하거나 64비트 버전의 Windows에 64비트 버전의 Office를 설치한 경우 기본 경로는 `C:\Program Files\Microsoft Office`입니다. 64비트 버전의 Windows에 32비트 버전의 Office를 설치한 경우 기본 경로는 `C:\Program Files (x86)\Microsoft Office`입니다.
        
          - *\<OfficeVersion\>*   Outlook 2007의 경우 값은 `Office12`입니다. Outlook 2010의 경우 값은 `Office14`입니다. Outlook 2013의 경우 값은 `Office15`입니다.
        
          - *\<LCID\>*   LCID(로캘 ID) 값입니다. 예를 들어 미국 영어의 LCID는 1033입니다. 자세한 내용은 [KB221435: Word에서 지원되는 로캘 식별자 목록](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=221435)(기계 번역)을 참조하십시오.
    
      - **이름**   이 절차의 나머지 부분에서는 파일 이름이 `QTNE.cfg`라고 가정합니다. 파일 이름은 중요하지 않지만, 값을 따옴표로 묶어야 파일이 QTNE.cfg.txt가 아닌 QTNE.cfg로 저장됩니다.
    
    예를 들어 64비트 버전의 Windows에 32비트 미국 영어 버전의 Outlook 2013을 설치한 경우 파일을 다음과 같이 저장합니다.
    
        "C:\Program Files (x86)\Microsoft Office\Office15\Forms\1033\QTNE.cfg"
    

    > [!NOTE]
    > Windows 사용자 UAC (액세스 제어) 올바른 위치에 파일을 저장 하지 않게, 임시 위치에 먼저 저장 한 다음 복사 합니다.



## 2단계: 사용자 지정 Outlook 양식을 사용하도록 Outlook 구성

컴퓨터에 설치한 Outlook 버전에 따라 다음 절차 중 하나를 사용합니다.

## Outlook 2010 또는 Outlook 2013 구성

1.  Outlook 2010 또는 Outlook 2013에서 **파일** \> **옵션** \> **고급**을 클릭합니다.

2.  **개발자** 섹션에서 **사용자 지정 양식**을 클릭합니다.

3.  **옵션** 대화 상자에서 **양식 관리**를 클릭합니다.

4.  **양식 관리자** 대화 상자에서 **설치** 를 클릭 합니다. `QTNE.cfg` 파일의 위치를 찾습니다 선택한 **열기** 를 클릭 합니다. **양식 속성** 대화 상자에서 정보를 검토 하 고을 개인 양식 라이브러리에 Quarantine Extension Form을 설치 하려면 **확인** 클릭 합니다.

5.  **양식 관리자** 대화 상자에서 **닫기**를 클릭합니다. **확인**을 두 번 클릭하여 나머지 대화 상자를 닫고 Outlook 주 인터페이스로 돌아갑니다.

6.  받은 편지함의 **메일** 보기에 있는 **홈** 탭에서 열 머리글 행을 마우스 오른쪽 단추로 클릭하고(열을 보기 위해 메시지 폭을 확장해야 할 수도 있음) **보기 설정**을 선택합니다.

7.  **고급 보기 설정** 대화 상자에서 **열**을 클릭합니다.

8.  **열 표시** 대화 상자의 **사용 가능한 열 선택** 드롭다운 목록에서 목록 끝으로 스크롤하고 **양식**을 선택합니다.

9.  **이 폴더에 대한 엔터프라이즈 양식 선택** 대화 상자의 **선택한 양식** 필드에서 **메시지**를 선택하고 **제거**를 클릭합니다. **개인 양식** 필드에서 **Quarantine Extension Form**을 선택하고 **추가**를 클릭합니다. 작업을 마치면 **닫기**를 클릭합니다.

10. **열 표시** 대화 상자의 **사용 가능한 열** 섹션에서 하나 이상의 각 필드를 선택하고 필드를 선택할 때마다 **추가**를 클릭합니다.
    
      - **ReceivedRepresentingEmailAddress**   원래 보낸 사람
    
      - **의**   원래 받는 사람 (메모를 추가한 후 **다른 이름으로** 표시 하는이)
    
      - **OriginalScl**   원래 SCL
    
    **위로 이동** 또는 **아래로 이동** 단추를 사용 하 여 열의 보기의 위치를 변경 합니다. 최상의 결과 **첨부 파일** 필드 및 필드에서 하기 전에 세 새 필드의 위치입니다. 완료 했으면 Outlook 주 인터페이스로 돌아갑니다를 두번 **확인** 클릭 합니다.

## Outlook 2007 구성

1.  Outlook 2007에서 **도구** \> **옵션**을 클릭합니다.

2.  **옵션** 대화 상자의 **기타** 탭을 클릭한 다음 **일반**에서 **고급 옵션**을 클릭합니다.

3.  **고급 옵션** 대화 상자에서 **사용자 지정 양식**을 클릭한 후 **사용자 지정 양식** 대화 상자에서 **양식 관리**를 클릭합니다.

4.  **양식 관리자** 대화 상자에서 **설치** 를 클릭 합니다. `QTNE.cfg` 파일의 위치를 찾습니다 선택한 **열기** 를 클릭 합니다. **양식 속성** 대화 상자에서 정보를 검토 하 고을 개인 양식 라이브러리에 Quarantine Extension Form을 설치 하려면 **확인** 클릭 합니다.

5.  **양식 관리자** 대화 상자를 닫습니다 한 다음 **확인** 을 세 번 클릭 하 여 나머지 대화 상자를 닫고 및 Outlook 2007 주 인터페이스로 돌아갑니다.

6.  받은 편지함의 **메일** 보기에서 열 머리글 행 (해야할 수 있습니다는 열을 볼 메시지 목록의 너비를 확장)을 마우스 오른쪽 단추로 클릭 하 고 **현재 보기를 사용자 지정** 을 선택 합니다.

7.  **보기 사용자 지정: 메시지** 대화 상자에서 **필드 표시** 를 클릭 합니다.

8.  **필드 표시** 대화 상자에서 **사용 가능한 필드 선택** 드롭다운 목록에서 목록 끝으로 스크롤하고 **양식** 을 선택 합니다.

9.  **이 폴더에 대한 엔터프라이즈 양식 선택** 대화 상자의 **선택한 양식** 필드에서 **메시지**를 선택하고 **제거**를 클릭합니다. **개인 양식** 필드에서 **Quarantine Extension Form**을 선택하고 **추가**를 클릭합니다. 작업을 마치면 **닫기**를 클릭합니다.

10. **필드 표시** 대화 상자의 **사용 가능한 필드** 섹션에서 다음 필드 중 하나 이상을 선택 하 고 각 필드를 선택한 다음 **추가** 클릭 합니다.
    
      - **ReceivedRepresentingEmailAddress**   원래 보낸 사람
    
      - **의**   원래 받는 사람 (메모를 추가한 후 **다른 이름으로** 표시 하는이)
    
      - **OriginalScl**   원래 SCL
    
    **위로 이동** 또는 **아래로 이동** 단추를 사용 하 여 열의 보기의 위치를 변경 합니다. 최상의 결과 **첨부 파일** 필드 및 필드에서 하기 전에 세 새 필드의 위치입니다. 완료 했으면 Outlook 2007 주 인터페이스로 돌아갑니다를 두번 **확인** 클릭 합니다.

## 작동 여부는 어떻게 확인합니까?

Outlook을 사용하여 스팸 격리 사서함에서 격리된 메시지에 대한 원래 보낸 사람, 원래 받는 사람 또는 원래 SCL 값을 볼 수 있으면 이 절차가 제대로 작동한 것입니다.

