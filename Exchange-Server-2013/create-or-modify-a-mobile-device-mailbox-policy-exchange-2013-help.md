---
title: '모바일 장치 사서함 정책 만들기 또는 수정: Exchange 2013 Help'
TOCTitle: 모바일 장치 사서함 정책 만들기 또는 수정
ms:assetid: b4a37a81-25e3-40ff-a18a-a62ae4493635
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124315(v=EXCHG.150)
ms:contentKeyID: 50483967
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 모바일 장치 사서함 정책 만들기 또는 수정

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2012-10-16_

모바일 장치 사서함 정책을 사용하면 보안 및 모바일 장치 설정의 공통된 집합을 사용자 그룹에 적용할 수 있습니다. 여러 모바일 장치 사서함 정책을 만들 수 있습니다. 조직의 각 받는 사람에게는 모바일 장치 사서함 정책이 할당되어야 합니다. Microsoft Exchange Server 2013을 설치하면 기본 모바일 장치 사서함 정책이 만들어지고 새 사용자에게 이 정책이 자동으로 할당됩니다. 특정 사용자를 모바일 장치 사서함 정책에 할당하려면 [추가 또는 모바일 사서함 정책에서 사용자 제거](add-or-remove-users-from-a-mobile-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

모바일 장치 사서함 정책과 관련된 자세한 내용은 [모바일 장치 사서함 정책](mobile-device-mailbox-policies-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분.

  - [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 주제의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "모바일 장치 사서함 정책" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 새 모바일 장치 사서함 정책 만들기

EAC 또는 셸을 사용하여 새 모바일 장치 사서함 정책을 만들 수 있습니다.

[클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 주제의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "모바일 장치 사서함 정책" 항목.

## EAC를 사용하여 새로운 모바일 장치 사서함 정책 만들기

EAC를 사용하여 새로운 모바일 장치 사서함 정책을 만들 수 있습니다.


> [!NOTE]
> EAC에서는 모바일 장치 사서함 정책 설정의 일부만 설정할 수 있습니다. 모든 모바일 장치 사서함 정책 설정을 지정하려면 셸을 사용해야 합니다.



1.  EAC에서 <strong>모바일</strong> \> <strong>모바일 장치 사서함 정책</strong>을 클릭한 다음 <strong>새로 만들기</strong>를 클릭합니다.

2.  여러 확인란과 드롭다운 목록을 사용하여 모바일 장치 사서함 정책의 설정을 구성합니다.
    
    > [!CAUTION]
    > 새 모바일 사서함 정책을 기본 모바일 사서함 정책으로 만들려면 <strong>기본 정책입니다.</strong>를 선택합니다. 모바일 사서함 정책을 기본 정책으로 만들면 모든 새 사용자가 만들어질 때 이 정책이 자동으로 할당됩니다.


3.  <strong>저장</strong>을 클릭합니다.

## 셸을 사용하여 새로운 모바일 장치 사서함 정책 만들기

New-MobileDeviceMailboxPolicy cmdlet을 사용하여 새로운 모바일 장치 사서함 정책을 만듭니다.

> [!CAUTION]
> 새 모바일 장치 사서함 정책을 만드는 데 사용할 수 있는 cmdlet은 두 가지입니다. <strong>New-ActiveSyncMailboxPolicy</strong> cmdlet과 <strong>New-MobileDeviceMailboxPolicy</strong> cmdlet은 동일한 작업을 수행합니다. Microsoft Exchange Server의 이후 버전에서는 <strong>New-ActiveSyncMailboxPolicy</strong> cmdlet을 포함하지 않을 예정입니다. <strong>New-MobileDeviceMailboxPolicy</strong> cmdlet을 사용하려면 스크립트 및 프로시저를 업데이트하는 것이 좋습니다.


1.  셸에서 다음 명령을 실행합니다.
    
        New-MobileDeviceMailboxPolicy -Name:"Management" -AllowBluetooth:$true -AllowBrowser:$true -AllowCamera:$true -AllowPOPIMAPEmail:$false -PasswordEnabled:$true -AlphanumericPasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:10 -AllowWiFi:$true -AllowStorageCard:$true -AllowPOPIMAPEmail:$false

## 작동 여부는 어떻게 확인합니까?

모바일 장치 사서함 정책을 성공적으로 만들었는지 확인하려면 다음 옵션 중 하나를 사용하십시오.

1.  EAC에서 <strong>모바일</strong> \> <strong>모바일 장치 사서함 정책</strong>을 클릭하고 새 정책이 목록 보기에 표시되는지 확인합니다.

2.  셸에서 다음 명령을 실행합니다.
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName> 

## 기존 모바일 장치 사서함 정책 편집

모바일 장치 사서함 정책을 편집하려면 EAC 또는 셸을 사용할 수 있습니다.

[클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 주제의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "모바일 장치 사서함 정책" 항목.

## EAC를 사용하여 모바일 장치 사서함 정책 편집

EAC를 사용하여 모바일 장치 사서함 정책을 편집할 수 있습니다.


> [!NOTE]
> EAC에서는 모바일 장치 사서함 정책 설정의 일부만 편집할 수 있습니다. 모든 모바일 장치 사서함 정책 설정을 편집하려면 셸을 사용해야 합니다.



1.  EAC에서 <strong>모바일</strong> \> <strong>모바일 장치 사서함 정책</strong>을 클릭합니다.

2.  목록 보기에서 정책을 선택하고 <strong>편집</strong> 단추를 클릭합니다.

3.  <strong>일반</strong> 및 <strong>보안</strong> 탭을 사용하여 모바일 정책 사서함 정책 설정을 편집합니다.

4.  <strong>저장</strong>을 클릭하여 정책을 업데이트합니다.

## 셸을 사용하여 모바일 장치 사서함 정책 설정 편집

셸을 사용하여 모바일 장치 사서함 정책을 편집할 수 있습니다.

> [!CAUTION]
> 모바일 장치 사서함 정책을 편집하는 데 사용할 수 있는 cmdlet은 두 가지입니다. Set-ActiveSyncMailboxPolicy cmdlet과 Set-MobileDeviceMailboxPolicy cmdlet은 동일한 작업을 수행합니다. Microsoft Exchange Server의 이후 버전에서는 <strong>Set-ActiveSyncMailboxPolicy</strong> cmdlet을 포함하지 않을 예정입니다. <strong>Set-MobileDeviceMailboxPolicy</strong> cmdlet을 사용하려면 스크립트 및 프로시저를 업데이트하는 것이 좋습니다.


1.  셸에서 다음 명령을 실행합니다.
    
        Set-MobileDeviceMailboxPolicy -Identity:Default -DevicePasswordEnabled:$true -AlphanumericDevicePasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:ThreeDays -AllowWiFi:$false -AllowStorageCard:$true -AllowPOPIMAPEmail:$false -IsDefault:$true -AllowTextMessaging:$true -Confirm:$true

## 작동 여부는 어떻게 확인합니까?

모바일 장치 사서함 정책을 성공적으로 편집했는지 확인하려면 다음 중 하나를 수행하십시오.

1.  EAC에서 <strong>모바일</strong> \> <strong>모바일 장치 사서함 정책</strong>을 클릭한 다음 특정 정책을 선택합니다. 세부 정보 창에 여러 정책 설정이 표시됩니다.

2.  셸에서 다음 명령을 실행합니다.
    
    ```powershell
Get-MobileDeviceMailboxPolicy -Identity <PolicyName>
```

