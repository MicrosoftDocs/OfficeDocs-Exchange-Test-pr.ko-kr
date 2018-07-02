---
title: 'Exchange 2013에서 DLP 중요 한 정보 유형 내보내기: Exchange 2013 Help'
TOCTitle: Exchange에서 DLP 중요 한 정보 유형 내보내기
ms:assetid: 8f02fbc2-dd1c-4276-be1a-517a43fe39b2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn479225(v=EXCHG.150)
ms:contentKeyID: 59635521
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013에서 DLP 중요 한 정보 유형 내보내기

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-05-04_

보거나 수 정책 내보내기 (영문)를 XML 파일로 저장 하 고 해당 XML 파일을 수정 하 여 Exchange 관리 센터 (EAC) 또는 Exchange 관리 셸 cmdlet을 사용 하지 않고 DLP 정책 내에서 세부 정보를 변경 합니다. 일반적으로 다음 파일을 가져오면 XML Exchange 에 다시 합니다. 이와 같은 방식으로 정책은 편집할 수 있습니다 독립적 Exchange 입니다. 그러나 라고도 XML 스키마를 제대로 작동 하기 위해 특정 형식 요구 사항을 충족 해야 합니다.

DLP에 관련 된 추가 관리 작업을 [DLP 정책 관리](manage-dlp-policies-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "데이터 손실 방지(DLP)" 항목을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

EAC에서 외부 파일에 DLP 정책 또는 서식 파일을 내보낼 하는 방법을 제공 하지 않습니다. Exchange 관리 셸 를 사용 하 여이 작업을 수행 합니다.

## Exchange 관리 셸 사용 하 여 DLP 중요 한 정보 유형

이 예제에서는 특성 함께 모든 DLP 중요 한 정보 유형 C:\\My Documents\\exportedInformationTypes.xml 경로에서 XML 파일을 내보냅니다. 현재 DLP 중요 한 정보 유형 컬렉션의 백업 복사본을 만드는 것이 좋습니다. 이 작업을 수행 하는 한 가지 방법은 내보내기 즉시 복사 하 고 동일한 XML 파일의 이름을 바꿀를 합니다.

1.  Exchange 관리 셸 를 엽니다.

2.  형식은 **Get-classificationrulecollection**및 조직의 중요 한 정보 유형 화면에 표시 되어야 합니다. 기본, 기본 제공 중요 한 정보 유형 컬렉션을 "Microsoft 규칙 패키지." 라는 표시 됩니다 자신만의 모든 중요 한 정보 유형을 만들지 않은 경우

3.  입력 하 여 중요 한 정보 유형을 변수에 저장 **$ruleCollections Get-classificationrulecollection =**합니다.

4.  이제 모든 데이터와 서식이 지정 된 XML 파일을 입력 하 여 확인 **집합-콘텐츠-경로 "C:\\My Documents\\exportedRules.xml"-인코딩 바이트-$ruleCollections.SerializedClassificationRuleCollection 값이**.

이제 필요에 따라 정책의 조정 하려면 XML 파일을 편집할 수 있습니다. 기본 제공 중요 한 정보 유형 사용자 지정 하는 방법을 알아보려면 [기본 제공 DLP 중요 한 정보 유형 사용자 지정](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)를 참조 하십시오. Exchange에 다시 정책 가져오기에 대 한 자세한 내용은 [파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)을 참조 하십시오.

## 자세한 내용

[Exchange의 중요 한 정보 유형 찾아보십시오](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[기본 제공 DLP 중요 한 정보 유형 사용자 지정](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)

[파일에서 사용자 지정 DLP 정책 서식 파일을 가져오려면](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

