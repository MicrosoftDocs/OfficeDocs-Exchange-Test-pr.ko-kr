---
title: 'Outlook Web App 사서함 정책: Exchange 2013 Help'
TOCTitle: Outlook Web App 사서함 정책
ms:assetid: 213b8b7a-1c29-49ee-8c98-d0364ddf4f9d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335142(v=EXCHG.150)
ms:contentKeyID: 50482713
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App 사서함 정책

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-05_

Microsoft Outlook Web App 사서함 정책을 사용하여 Outlook Web App의 기능에 대한 액세스를 관리하는 조직 수준의 정책을 만들 수 있습니다.

**목차**

Outlook Web App mailbox policies

Creating or deleting Outlook Web App mailbox policies

Configuring Outlook Web App mailbox policies

Applying Outlook Web App mailbox policies

## Outlook Web App 사서함 정책

Exchange 2013에서는 여러 개의 Outlook Web App 사서함 정책을 만들어 개별 사서함에 적용할 수 있습니다. Outlook Web App 사서함 정책을 사서함에 적용하면 가상 디렉터리의 설정을 재정의합니다.

Outlook Web App 가상 디렉터리를 구성하여 Outlook Web App 기능을 관리할 수도 있습니다. 가상 디렉터리 설정은 사서함 정책이 적용되지 않은 모든 사서함에 사용됩니다.

## Outlook Web App 사서함 정책 만들기 또는 삭제

기본 Outlook Web App 사서함 정책은 Exchange를 설치할 때 자동으로 생성됩니다. 기본적으로 기본 Outlook Web App 사서함 정책의 모든 옵션이 사용하도록 설정되어 있습니다. 조직의 요구를 충족시키는 데 필요한 개수만큼 Outlook Web App 사서함 정책을 만들 수 있습니다.


> [!NOTE]
> 기본 Outlook Web App 사서함 정책은 사서함에 자동으로 적용되지 않습니다.



사서함 정책 만들기 또는 제거에 대한 자세한 내용은 [Outlook Web App 사서함 정책 만들기](https://docs.microsoft.com/ko-kr/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/create-outlook-web-app-mailbox-policy) 및 [Exchange에서 Outlook Web App 사서함 정책 제거](https://docs.microsoft.com/ko-kr/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/remove-outlook-web-app-mailbox-policy) 항목을 참조하십시오.

## Outlook Web App 사서함 정책 구성

기본 Outlook Web App 사서함 정책의 모든 옵션은 기본적으로 사용하도록 설정됩니다. Outlook Web App 사서함 정책에 대한 자세한 내용은 [Outlook Web App 사서함 정책 속성 보기 또는 구성](https://docs.microsoft.com/ko-kr/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/configure-outlook-web-app-mailbox-policy-properties) 항목을 참조하십시오.

## Outlook Web App 사서함 정책 적용

각 사서함에 Outlook Web App 사서함 정책 하나만 적용할 수 있습니다.

Outlook Web App 사서함 정책이 사서함에 적용되어 있지 않으면 가상 디렉터리에 정의된 설정이 적용됩니다.

EAC(Exchange 관리 센터)를 사용하여 기존 사서함을 수정하거나 셸 및 [Set-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb125264\(v=exchg.150\)) cmdlet를 사용하여 사서함 정책을 적용하여 Outlook Web App 사서함 정책을 사서함에 적용할 수 있습니다. 자세한 내용은 [사서함에는 Outlook Web App 사서함 정책 적용 또는 제거](https://docs.microsoft.com/ko-kr/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/apply-or-remove-outlook-web-app-mailbox-policy) 항목을 참조하십시오.

