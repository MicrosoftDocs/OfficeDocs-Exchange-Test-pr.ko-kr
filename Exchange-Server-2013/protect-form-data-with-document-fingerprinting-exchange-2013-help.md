---
title: '문서 지문을 사용 하 여 양식 데이터를 보호 합니다.: Exchange 2013 Help'
TOCTitle: 문서 지문을 사용 하 여 양식 데이터를 보호 합니다.
ms:assetid: 110c839b-7693-42f6-aa5d-58ce64f4c357
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn635175(v=EXCHG.150)
ms:contentKeyID: 61203316
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 문서 지문을 사용 하 여 양식 데이터를 보호 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-09-11_

조직에서 양식을 사용하여 중요한 정보를 수집하는 경우 사용자가 외부 연락처에게 해당 양식을 전자 메일로 보내려고 시도할 수 있으며, 그러면 보안 위험이 발생합니다. Exchange의 DLP(데이터 손실 방지) 기능을 사용하면 [문서 지문](overview-of-document-fingerprinting-in-exchange.md)을 통해 해당 정보를 보호할 수 있습니다. 문서 지문을 사용하려면 지적 재산 문서, 정부 양식 또는 조직에서 사용하는 기타 표준 양식과 같은 빈 양식을 업로드하기만 하면 됩니다. 그런 다음 생성된 문서 지문을 DLP 정책 또는 전송 규칙에 추가합니다. 이 작업을 수행하는 방법은 다음과 같습니다.

> [!VIDEO https://www.microsoft.com/ko-kr/videoplayer/embed/0f803e16-397a-4b83-8a85-06cd4264aaca]

## EAC를 사용하여 문서 지문 만들기

![강조 표시된 EAC의 문서 핑거프린팅 경로](images/Dn635175.e8562ea7-40ba-4feb-adde-2e81f029fcda(EXCHG.150).png "강조 표시된 EAC의 문서 핑거프린팅 경로")

1.  EAC(Exchange 관리 센터)에서 **준수 관리** \> **데이터 손실 방지**로 이동합니다.

2.  **문서 지문 관리**를 클릭합니다.

3.  문서 지문 페이지에서 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 새 문서 지문을 만듭니다.

4.  문서 지문의 **이름** 및 **설명**을 지정합니다. 선택하는 이름이 중요한 정보 유형 목록에 표시됩니다.

5.  양식을 업로드하려면 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

6.  폼을 선택 하 고 **열기** 를 클릭 합니다. (업로드 파일 텍스트가 있는지 확인, 암호 보호 및 전송 규칙에서 지원 되는 파일 형식 중 하나에 되지 않습니다. 지원 되는 파일 형식 목록에 대 한 [메일 흐름 규칙을 사용 하 여 Office 365의 메시지 첨부 파일을 검사 하려면](https://technet.microsoft.com/ko-kr/library/jj919236\(v=exchg.150\))를 참조 합니다. 그렇지 않은 경우 가져옵니다 오류를 지문 만들기 (영문)을 시도 하는 경우.) 이 문서 지문에 대 한 문서 목록에 추가 하려는 파일의 다른 파일에 대해 반복 합니다. 추가 하거나에서 파일을 제거이 문서 지문 나중에 사용할 경우 수 있습니다.

7.  **저장**을 클릭합니다.

문서 지문 이제 중요 한 정보 유형의 속하며 DLP 정책에 추가 하거나 **메시지에 중요 한 정보가... 포함** 조건을 통해 전송 규칙에 추가할 수 있습니다.

![강조 표시된 "다음의 경우 이 규칙 적용" 조건 강조](images/Dn635175.9355a513-a790-48eb-a61b-575ba2ecdfa6(EXCHG.150).png "강조 표시된 \"다음의 경우 이 규칙 적용\" 조건 강조")

DLP 정책에 규칙을 추가하는 방법에 대한 자세한 내용은 [DLP 정책 관리](manage-dlp-policies-exchange-2013-help.md)의 "DLP 정책 변경" 섹션을 참조하세요. 전송 규칙을 수정하는 방법에 대한 자세한 내용은 [전송 규칙에 중요 한 정보 규칙 통합 (영문)](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)을 참조하세요. 새 정책을 만들려면 [템플릿에서 DLP 정책 만들기](how-to-new-dlp-data-loss-prevention-policy-template.md)를 참조하세요.

## 셸을 사용하여 문서 지문을 기반으로 분류 규칙 패키지 만들기


> [!TIP]
> 수를 만들고 셸에서 분류 규칙 패키지를 수정 하는 경우에는 문서 지문 만들기 (영문)이 더 간단 EAC에서 찾을 수 있습니다. 셸에서이 절차를 시도 하기 전에 다음과 같은 것을 시도 하는 것이 좋습니다.



DLP는 분류 규칙 패키지를 사용하여 메시지의 중요한 내용을 검색합니다. 문서 지문을 기준으로 분류 규칙 패키지를 만들려면 **New-Fingerprint** 및 **New-DataClassification** cmdlet을 사용합니다. **New-Fingerprint**의 결과는 데이터 분류 규칙 외부에 저장되지 않으므로 **New-Fingerprint**와 **New-DataClassification** 또는 **Set-DataClassification**은 항상 같은 PowerShell 세션에서 실행합니다. 다음 예에서는 C:\\My Documents\\Contoso Employee Template.docx 파일을 기반으로 새 문서 지문을 만듭니다. 새 지문은 같은 PowerShell 세션의 **New-DataClassification** cmdlet에서 사용할 수 있도록 변수로 저장합니다.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Employee Template.docx" -Encoding byte
    $Employee_Fingerprint = New-Fingerprint -FileData $Employee_Template -Description "Contoso Employee Template"

C:\\My Documents\\Contoso Customer Information Form.docx 파일의 문서 지문을 사용하는 "Contoso Employee Confidential"이라는 새 데이터 분류 규칙을 만들어 보겠습니다.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Customer Information Form.docx" -Encoding byte
    $Customer_Fingerprint = New-Fingerprint -FileData $Customer_Form -Description "Contoso Customer Information Form"
    New-DataClassification -Name "Contoso Customer Confidential" -Fingerprints $Customer_Fingerprint -Description "Message contains Contoso customer information." 

이제 **Get-DataClassification** cmdlet을 사용하여 모든 DLP 데이터 분류 규칙 패키지를 사용할 수 있습니다. 이 예에서는 "Contoso Customer Confidential"이 데이터 분류 규칙 패키지 목록에 포함됩니다.

마지막으로 "Contoso Customer Confidential" 데이터 분류 규칙 패키지를 DLP 정책에 추가합니다.

    New-TransportRule -Name "Notify :External Recipient Contoso confidential" -NotifySender NotifyOnly -Mode Enforce -SentToScope NotInOrganization -MessageContainsDataClassification @{Name=" Contoso Customer Confidential"}

이제 DLP 에이전트가 Contoso Customer Form.docx 문서 지문과 일치하는 문서를 검색합니다.

구문과 매개 변수에 대한 자세한 내용은 [New-Fingerprint](https://technet.microsoft.com/ko-kr/library/dn584142\(v=exchg.150\)), [New-DataClassification](https://technet.microsoft.com/ko-kr/library/dn584139\(v=exchg.150\)), [Set-DataClassification](https://technet.microsoft.com/ko-kr/library/dn584141\(v=exchg.150\)) 및 [Get-DataClassification](https://technet.microsoft.com/ko-kr/library/jj215720\(v=exchg.150\))을 참조하세요.

## 자세한 내용

[문서 지문](overview-of-document-fingerprinting-in-exchange.md)

[DLP 정책 관리](manage-dlp-policies-exchange-2013-help.md)

[전송 규칙에 중요 한 정보 규칙 통합 (영문)](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

