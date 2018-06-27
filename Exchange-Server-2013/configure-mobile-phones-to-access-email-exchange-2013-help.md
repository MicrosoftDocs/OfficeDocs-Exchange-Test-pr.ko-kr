---
title: '전자 메일에 액세스 하려면 휴대폰을 구성 합니다.: Exchange 2013 Help'
TOCTitle: 전자 메일에 액세스 하려면 휴대폰을 구성 합니다.
ms:assetid: 8d6e2cea-265a-43d9-a074-076f35658436
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123704(v=EXCHG.150)
ms:contentKeyID: 52057941
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전자 메일에 액세스 하려면 휴대폰을 구성 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-12_

Microsoft Exchange ActiveSync를 사용하도록 Windows Phone 등의 휴대폰을 구성할 수 있습니다. 조직에 있는 각 휴대폰에서 이 절차를 수행해야 합니다.

## 선행 조건

  - 구성할 휴대폰 제조업체의 설명서를 검토합니다.

  - 조직에서 Exchange ActiveSync를 사용하고 있어야 합니다.


> [!NOTE]
> Microsoft를 설정 하는 방법에 대 한 장치 관련 정보에 대 한 Exchange 기반 전자 메일에서 휴대폰 또는 태블릿, <A href="https://support.office.com/en-us/article/set-up-a-mobile-device-using-office-365-for-business-7dabb6cb-0046-40b6-81fe-767e0b1f014f">비즈니스를 위한 Office 365를 사용 하 여 모바일 장치를 설정</A>를 참조 합니다.



## Exchange ActiveSync를 사용하여 휴대폰 구성

대부분의 휴대폰 및 모바일 장치에서는 자동 검색을 사용하여 Exchange ActiveSync를 사용하도록 모바일 전자 메일 클라이언트를 구성할 수 있습니다. 대부분의 휴대폰에서 전자 메일 계정을 구성하려면 다음과 같은 두 가지 유형의 정보가 있어야 합니다.

  - 사용자의 전자 메일 주소

  - 사용자 암호

휴대폰 Exchange 서버 자동 검색을 통해 자동으로 연결할 수 없는 경우에 휴대폰을 수동으로 설정 하려면 필요 합니다. 수동 설치 프로그램 사용자의 전자 메일 주소 및 암호를으로 Exchange ActiveSync 서버 이름이 필요합니다. 대부분의 조직에서 Exchange ActiveSync 서버 이름은 /owa, 등 mail.contoso.com 없이 Outlook Web App 서버 이름과 같습니다.

## Windows Phone 동기화

Exchange ActiveSync를 사용하여 Exchange 사서함과 동기화하도록 Windows Phone 휴대폰을 구성하는 경우 모바일 장치 사서함 정책 설정의 하위 집합만 지원됩니다. 이러한 정책 설정은 [Windows 전화 및 장치에 대 한 모바일 장치 사서함 정책 지원](supported-mobile-device-mailbox-policies-for-windows-phones-and-devices-exchange-2013-help.md)에 설명되어 있습니다.

사용 중인 Windows Phone에서 지원하지 않는 모바일 장치 사서함 정책 설정을 구성하는 경우 **AllowNonProvisionableDevices** 정책 설정을 true로 설정하거나 Windows Phone 휴대폰에 대해 별도의 모바일 장치 사서함 정책을 만들어야 합니다.

