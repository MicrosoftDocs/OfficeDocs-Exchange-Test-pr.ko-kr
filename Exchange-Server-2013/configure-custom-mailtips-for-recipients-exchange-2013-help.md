---
title: '받는 사람에 대해 사용자 지정 메일 설명 구성: Exchange 2013 Help'
TOCTitle: 받는 사람에 대해 사용자 지정 메일 설명 구성
ms:assetid: df8ee7ae-2486-4890-b057-cda87b4cb1ec
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638199(v=EXCHG.150)
ms:contentKeyID: 52057971
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 받는 사람에 대해 사용자 지정 메일 설명 구성

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-06-01_

*메일 설명*은 사용자가 전자 메일 메시지를 작성하는 동안 다음 중 하나를 수행할 때 Outlook Web App 및 Microsoft Outlook 2010 이상 버전의 정보 표시줄에 표시되는 정보 메시지입니다.

  - 받는 사람 추가

  - 첨부 파일 추가

  - 회신 또는 전체 회신

  - 임시 보관함 폴더에서 받는 사람의 주소가 이미 입력된 메시지 열기

기본 제공 메일 설명을 사용할 수도 있고 모든 유형의 받는 사람에 대해 사용자 지정 메일 설명을 만들 수도 있습니다. 기본 제공 메일 설명에 대한 자세한 내용은 [MailTips](mailtips-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "메일 설명" 항목

  - EAC(Exchange 관리 센터) 또는 셸에서 기본 메일 설명을 구성할 수 있습니다. 그러나 추가 메일 설명 번역은 셸에서만 구성할 수 있습니다.

  - 받는 사람에 대해 메일 설명을 추가하면 다음의 두 가지 작업이 수행됩니다.
    
      - HTML 태그가 텍스트에 자동으로 추가됩니다. 예를 들어 `This mailbox is not monitored`라는 텍스트를 입력하면 메일 설명이 자동으로 `<html><body>This mailbox is not monitored</body></html>`로 됩니다. 메일 설명의 추가 HTML 태그는 지원되지 않습니다.
    
      - 텍스트가 받는 사람의 *MailTipTranslations* 속성에 기본값으로 자동 추가됩니다. 메일 설명 텍스트를 수정하면 *MailTipTranslations* 속성에서 기본값이 자동으로 업데이트됩니다.

  - 표시되는 메일 설명의 길이는 175자를 초과할 수 없습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 받는 사람에 대해 메일 설명 구성

## EAC를 사용하여 받는 사람에 대해 메일 설명 구성

1.  EAC에서 **받는 사람**으로 이동합니다.

2.  받는 사람 유형에 따라 다음의 받는 사람 탭 중 하나를 선택합니다.
    
      - **사서함**
    
      - **그룹**
    
      - **리소스**
    
      - **연락처**
    
      - **공유**

3.  받는 사람 탭에서 수정하려는 받는 사람을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  받는 사람 속성 페이지가 나타나면 **메일 설명**을 클릭합니다.

5.  메일 설명의 텍스트를 입력합니다. 작업을 마치면 **저장**을 클릭합니다.

## 셸을 사용하여 받는 사람에 대해 메일 설명 구성

받는 사람에 대해 메일 설명을 구성하려면 다음 구문을 사용합니다.

    Set-<RecipientType> <RecipientIdentity> -MailTip "<MailTip text>"

*\<RecipientType\>*에는 모든 유형의 받는 사람을 지정할 수 있습니다. `Mailbox`, `MailUser`, `MailContact`, `DistributionGroup`, `DynamicDistributionGroup` 등을 예로 들 수 있습니다.

예를 들어 사용자가 지원 요청을 전송할 수 있는 "Help Desk"라는 사서함이 있고 이 사서함의 예정된 응답 시간이 두 시간이라고 가정해 보겠습니다. 이를 설명하는 사용자 지정 메일 설명을 구성하려면 다음 명령을 실행합니다.

    Set-Mailbox "Help Desk" -MailTip "A Help Desk representative will contact you within 2 hours."

## 셸을 사용하여 다른 언어로 추가 메일 설명 구성

기존 메일 설명 텍스트 또는 다른 기존 메일 설명 번역에 영향을 주지 않고 추가 메일 설명 번역을 구성하려면 다음 구문을 사용합니다.

    Set-<RecipientType> -MailTipTranslations @{Add="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...; Remove="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...}

*\<culture\>*는 언어와 연관된 유효한 ISO 639 두 자리 문화권 코드입니다.

예를 들어 Notifications라는 사서함에 현재 "This mailbox is not monitored."라는 메일 설명이 지정되어 있다고 가정해 보겠습니다. 스페인어 번역을 추가하려면 다음 명령을 실행합니다.

    Set-Mailbox -MailTipTranslations @{Add="ES:Esta caja no se supervisa."}

## 작동 여부는 어떻게 확인합니까?

받는 사람에 대해 메일 설명이 구성되었는지 확인하려면 다음을 수행합니다.

1.  Outlook Web App 또는 Outlook 2010 이상 버전에서 받는 사람의 주소를 지정하여 전자 메일 메시지를 작성하되 보내지는 않습니다.

2.  정보 표시줄에 메일 설명이 나타나는지 확인합니다.

3.  추가 메일 설명 번역을 구성한 경우 언어 설정이 메일 설명 번역의 언어와 일치하는 Outlook Web App에서 메시지를 작성하여 결과를 확인합니다.

