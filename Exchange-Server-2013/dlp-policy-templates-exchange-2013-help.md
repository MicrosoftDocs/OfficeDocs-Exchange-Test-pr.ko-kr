---
title: 'DLP 정책 템플릿: Exchange 2013 Help'
TOCTitle: DLP 정책 템플릿
ms:assetid: c7b1a8e4-30d9-4409-85c5-f85ae023737d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657730(v=EXCHG.150)
ms:contentKeyID: 50484127
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DLP 정책 템플릿

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-14_

Microsoft Exchange 2013 에서 DLP 솔루션을 사용 하는 데이터 손실 방지 (DLP) 정책 템플릿을 사용할 수 있습니다. DLP 정책 서식 파일은 정책에 대 한 모델입니다. 사용자 고유의 사용자 지정된 DLP 정책 만들기 (영문)의 프로세스를 시작 하려면 서식 파일을 선택할 수 있습니다. DLP 정책 내에서 데이터 손실 방지에 대 한 비즈니스 요구를 충족 하는지 확인 하는 규칙을 사용자 지정할 수 있습니다. 여러 정책 템플릿 Microsoft에서 제공 되지만 이러한 Exchange 에서 데이터 손실 방지 솔루션을 구현 하는 유일한 방법은 없습니다.

DLP 정책 템플릿에 관련된 관리 작업을 찾고 있습니까? [DLP 절차](dlp-procedures-exchange-2013-help.md)를 참조하십시오.

**목차**

Extend the templates and information types to meet your needs

Create your own new DLP policy template

Include DLP functionality with existing transport rules

Use DLP policies created by Microsoft

For more information

## 요구 사항을 충족하도록 템플릿 및 정보 유형 확장

중요한 콘텐츠 정의와 Microsoft 파트너가 제공한 정책 템플릿 또는 Exchange 2013에서 기본 제공되는 DLP 정책 템플릿, 정보 유형 및 규칙에 대한 추가로서 직접 개발한 파일의 정책 템플릿을 통합할 수 있습니다. 여기에는 자신만의 고유한 DLP 콘텐츠를 추가하고 DLP 기능을 확장할 수 있는 몇 가지 방법이 나와 있습니다. Microsoft에서 기본으로 제공하는 템플릿은 DLP 솔루션을 시작하기에 편리한 방법입니다. 자신만의 고유한 DLP 정책 템플릿 파일을 사용하여 DLP 기능을 확장하려면 Exchange와는 별도로 만들어지는 정책 템플릿에 대한 XML 스키마 요구 사항을 이해해야 합니다. DLP 정책 템플릿에 연결된 Exchange 관리 셸 cmdlet에 대한 자세한 내용은 [정책 및 규정 준수 Cmdlet](https://technet.microsoft.com/ko-kr/library/dd298082\(v=exchg.150\))에서 `Get-DlpPolicyTemplate`에 관련된 cmdlet을 참조하십시오. 아울러 통합을 위한 형식과 절차를 이해한 후에는 자신만의 중요한 콘텐츠 유형을 정의할 수 있습니다. DLP 정책 템플릿에 연결된 Exchange 관리 셸 cmdlet에 대한 자세한 내용은 [정책 및 규정 준수 Cmdlet](https://technet.microsoft.com/ko-kr/library/dd298082\(v=exchg.150\))에서 `Get-ClassificationRuleCollection`에 관련된 cmdlet을 참조하십시오.


> [!WARNING]
> DLP 정책을 프로덕션 환경에서 실행하기 전에 테스트 모드에서 설정해야 합니다. 그러한 테스트 중에, 샘플 사용자 사서함을 구성한 다음 결과 확인을 위해 테스트 정책을 호출하는 테스트 메시지를 전송해 보는 것이 좋습니다.



## 분류 규칙 패키지에 자신만의 새로운 DLP 정책 템플릿 또는 중요한 정보 유형 만들기

Microsoft에서 정의한 특정 XML 스키마 정의를 준수하는 Exchange와는 별개인 DLP 정책 템플릿 파일을 만든 다음 해당 파일을 시스템에 가져와 DLP 정책을 만들 수 있습니다. 자신만의 템플릿 파일을 만들면 Microsoft에서 기본 제공하지 않는 DLP 정책에 대한 모델을 직접 정의할 수 있습니다. 이는 일반적으로 정책 템플릿을 사용할 수 있게 된 후에 Exchange 관리 센터를 사용하여 DLP 정책을 만드는 것과는 다릅니다. Exchange와는 별도로 정책 템플릿을 만들 경우 이 템플릿을 사용하여 메시지를 검사하려면 먼저 템플릿을 가져와야 합니다. 또한 Exchange에서 Microsoft가 정의한 정보 정의 외에 자신만의 중요한 정보 정의를 만들 수 있습니다. DLP 정책 템플릿 파일 및 분류 규칙 패키지에 대한 별도의 XML 스키마 정의가 있습니다. 시작하려면 다음 정보를 참조하십시오.

  -  [자체 DLP 템플릿 및 정보 유형 정의](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

  -  [파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

## 기존 전송 규칙에 DLP 기능 포함

새 DLP 정책을 만들지 않고 기존 전송 규칙에 DLP 검색 기능을 통합할 수 있습니다. Exchange의 이전 버전에서 복잡한 규칙 집합을 만들었고 이를 복제하거나 Exchange 2013에 중요한 정보 검색을 추가하려는 경우 Exchange 관리 센터의 전송 규칙 편집기 또는 Exchange 관리 셸을 사용하여 이러한 두 기능을 통합할 수 있습니다. 시작하려면 다음 정보를 참조하십시오.

  -  [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

  -  [Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\)) (Exchange Online)

  -  [메일 흐름 규칙 관리](manage-mail-flow-rules-exchange-2013-help.md)
    
    [정책 및 규정 준수 Cmdlet](https://technet.microsoft.com/ko-kr/library/dd298082\(v=exchg.150\))

## Microsoft에서 만든 DLP 정책 사용

Microsoft에서는 매우 다양한 DLP 정책을 제공하고 있습니다. 이러한 DLP 정책을 사용하면 가장 쉽게 유연하면서도 구현하기 쉬운 DLP 솔루션을 시작할 수 있습니다. 언제든 제공된 정책을 시작점으로 사용하여 이를 요구 사항에 맞도록 사용자 지정할 수 있습니다. 시작하려면 다음 정보를 참조하십시오.

  - [Exchange에서 제공 하는 DLP 정책 템플릿](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)

  - [템플릿에서 DLP 정책 만들기](how-to-new-dlp-data-loss-prevention-policy-template.md)

## 자세한 내용

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

