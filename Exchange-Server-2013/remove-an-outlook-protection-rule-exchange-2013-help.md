---
title: 'Outlook 보호 규칙을 제거 합니다.: Exchange 2013 Help'
TOCTitle: Outlook 보호 규칙을 제거 합니다.
ms:assetid: 569fc3be-b269-43f5-8797-73ab0691e685
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633467(v=EXCHG.150)
ms:contentKeyID: 50483147
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook 보호 규칙을 제거 합니다.

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Outlook 보호 규칙을 사용 하는 메시지 전송 하기 전에 Outlook 2010 에 [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) 서식 파일을 적용 하 여 정보 권한 관리 (IRM)와 메시지를 보호할 수 있습니다. Outlook 보호 규칙 적용 되 고 하지 못하도록 하려면 규칙을 비활성화할 수 있습니다. Active Directory 에서 규칙 정의 제거 하면 Outlook 보호 규칙을 제거 합니다.

IRM과 관련된 추가 관리 작업에 대한 자세한 내용은 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "권한 보호" 항목

  - Outlook 보호 규칙을 제거하는 데에는 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 Outlook 보호 규칙 제거

이 예에서는 OPR-DG-Finance라는 Outlook 보호 규칙을 제거합니다.

    Remove-OutlookProtectionRule -Identity "OPR-DG-Finance"

구문과 매개 변수에 대한 자세한 내용은 [Remove-OutlookProtectionRule](https://technet.microsoft.com/ko-kr/library/dd297961\(v=exchg.150\))을 참조하십시오.

## 셸을 사용하여 모든 Outlook 보호 규칙 제거

이 예에서는 Exchange 조직의 모든 Outlook 보호 규칙을 제거합니다.

    Get-OutlookProtectionRule | Remove-OutlookProtectionRule

구문과 매개 변수에 대한 자세한 내용은 [Get-OutlookProtectionRule](https://technet.microsoft.com/ko-kr/library/dd298004\(v=exchg.150\)) 및 [Remove-OutlookProtectionRule](https://technet.microsoft.com/ko-kr/library/dd297961\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

Outlook 보호 규칙이 제거되었는지 확인하려면 [Get-OutlookProtectionRule](https://technet.microsoft.com/ko-kr/library/dd298004\(v=exchg.150\)) cmdlet을 사용하여 Outlook 보호 규칙을 검색합니다. Outlook 보호 규칙을 검색하는 방법의 예를 보려면 **Get-OutlookProtectionRule**의[Examples](https://technet.microsoft.com/ko-kr/dd298004\(exchg.150\)#examples) 항목을 참조하십시오.

