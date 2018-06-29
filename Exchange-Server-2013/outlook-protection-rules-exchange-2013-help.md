---
title: 'Outlook 보호 규칙: Exchange 2013 Help'
TOCTitle: Outlook 보호 규칙
ms:assetid: bd7d0ad7-1f8e-46da-a74b-58c58f3eff93
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638178(v=EXCHG.150)
ms:contentKeyID: 50484042
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook 보호 규칙

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

매일, 정보 근로자가 전자 메일, 재무 보고서 및 데이터, 고객 및 직원 정보 및 기밀 제품 정보 및 사양을 포함 하 여 중요 한 정보를 교환 합니다. Microsoft Exchange Server 2013, Microsoft Outlook, 및 Microsoft OfficeOutlook Web App 에서 사용자는 Active Directory (AD RMS) Rights Management Services 권한 정책 템플릿을 적용 하 여 메시지에 정보 권한 관리 (IRM) 보호를 적용할 수 있습니다. 이 경우 조직에서 AD RMS 배포를 해야 합니다. AD RMS에 대 한 자세한 내용은 [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823)을 참조 하십시오.

그러나 사용자의 재량에 달려 있는 경우 메시지를 IRM 보호 없이 일반 텍스트로 보낼 수 있습니다. 전자 메일을 호스트된 서비스로 사용하는 조직에서는 메시지가 클라이언트를 떠나서 조직 경계 외부로 라우팅 및 저장될 때 정보가 누출될 위험이 있습니다. 전자 메일 호스팅 회사가 정보 누출 위험을 완화하는 데 도움이 되는 적절하게 정의된 절차와 검사를 갖춘 경우에도 메시지가 조직 경계를 벗어나면 조직에서 정보를 더 이상 제어할 수 없습니다. Outlook 보호 규칙은 이러한 유형의 정보 누출을 방지하는 데 도움이 될 수 있습니다.

IRM 관리와 관련된 관리 작업에 대해서는 [정보 권한 관리 절차](information-rights-management-procedures-exchange-2013-help.md)를 참조하십시오.

## Outlook의 자동 IRM 보호

Exchange 2013에서 Outlook 보호 규칙은 IRM 보호를 Exchange 2013의 메시지에 자동으로 적용하여 조직에서 정보 누출 위험을 방지할 수 있게 합니다. 메시지는 Outlook 클라이언트에서 나가기 전에 IRM으로 보호됩니다. 또한 이 보호는 지원되는 파일 형식을 사용하는 모든 첨부 파일에 적용됩니다.

Outlook 서버에서 Exchange 2013 보호 규칙을 만들 경우 Outlook 2010 웹 서비스를 사용하여 규칙은 Exchange에 자동으로 배포됩니다. Outlook 2010에서 규칙을 적용하려면 지정한 AD RMS 권한 정책 템플릿을 사용자의 컴퓨터에서 사용할 수 있어야 합니다.


> [!IMPORTANT]
> 권한 정책 템플릿을 AD RMS 서버에서 제거 되 면 제거 된 서식 파일을 사용 하는 모든 Outlook 보호 규칙을 수정 해야 합니다. 제거 된 권한 정책 서식 파일을 사용 하 여 계속 실행 하면 Outlook 보호 규칙 전송 암호 해독은 조직에서 사용 하도록 설정 하는 경우 암호 해독 에이전트는 더이상 사용할 수 있는 템플릿을 사용 하 여 보호 된 메시지를 암호 해독에 실패 합니다. 전송 암호 해독을 필수 항목으로 구성 하는 경우 전송 서비스 메시지를 거부를 업데이트 하 고 보낸 사람에 게 배달 못함 보고서 (NDR)를 보낼 됩니다. 전송 암호 해독 하는 방법에 대 한 자세한 내용은 <A href="transport-decryption-exchange-2013-help.md">전송 암호 해독</A>을 참조 하십시오. AD RMS 권한 정책 서식 파일에 대 한 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=179455">AD RMS 정책 템플릿 고려 사항</A>을 참조 하십시오.<BR>Windows Server 2008 이상에서는 권한 정책 템플릿을 삭제하는 대신 보관할 수 있습니다. 보관된 템플릿을 계속 사용하여 콘텐츠의 사용을 허가할 수 있지만 Outlook&nbsp;보호 규칙을 만들거나 수정할 경우 보관된 템플릿은 템플릿 목록에 포함되지 않습니다.



Outlook 보호 규칙은 전송 보호 규칙과 비슷합니다. 둘 다 메시지 조건에 기초하여 적용되며 AD RMS 권한 보호 템플릿을 적용하여 메시지를 보호합니다. 그러나 전송 보호 규칙은 전송 규칙 에이전트에 의해 사서함 서버의 전송 서비스에 적용되고, Outlook 보호 규칙은 메시지가 사용자의 컴퓨터를 떠나기 전에 Outlook 2010에 적용됩니다. Outlook 보호 규칙에 의해 보호되는 메시지는 IRM 보호가 이미 적용된 전송 파이프라인에 들어갑니다. 또한 Outlook 보호 규칙에 의해 보호되는 메시지는 보낸 사람 사서함의 보낸 편지함 폴더에서 암호화된 형식으로 저장됩니다.


> [!NOTE]
> Exchange&nbsp;조직에서 전송 암호 해독이 사용되도록 설정된 경우 조직의 AD&nbsp;RMS 서버를 사용하여 Outlook&nbsp;보호 규칙에 따라 IRM으로 보호되는 메시지는 전송 서비스의 암호 해독 에이전트에 의해 해독될 수 있습니다. 전송 서비스에 설치된 전송 규칙 에이전트 및 다른 전송 에이전트가 메시지 콘텐츠를 조사할 수 있습니다. 전송 암호 해독에 대한 자세한 내용은 <A href="transport-decryption-exchange-2013-help.md">전송 암호 해독</A>를 참조하십시오.



전송 보호 규칙을 사용할 경우 전송 서비스에서 메시지가 자동으로 보호될지 여부에 대한 표시가 사용자에게 나타나지 않습니다. Outlook에서 Outlook 2010 보호 규칙이 메시지에 적용될 경우 사용자는 메시지가 IRM으로 보호될 것인지를 알 수 있습니다. 필요한 경우 사용자는 다른 권한 정책 템플릿을 선택할 수도 있습니다.

## Outlook 보호 규칙 만들기

Outlook 보호 규칙을 만들려면 Exchange 관리 셸에서 [New-OutlookProtectionRule](https://technet.microsoft.com/ko-kr/library/dd298182\(v=exchg.150\)) cmdlet을 사용해야 합니다. 자세한 내용은 [Outlook 보호 규칙 만들기](create-an-outlook-protection-rule-exchange-2013-help.md)를 참조하십시오.

규칙을 만들 때 IRM 보호를 제거하거나 규칙에 지정된 것과 다른 AD RMS 권한 정책 템플릿을 적용하여 사용자가 규칙을 다시 정의할 수 있는지 여부를 지정할 수 있습니다. 사용자가 Outlook 보호 규칙에 의해 적용된 IRM 보호를 다시 정의할 경우 Outlook 2010에서는 `X-MS-Outlook-Client-Rule-Overridden` 헤더를 메시지에 삽입하므로 사용자에 의해 규칙이 다시 정의되었음을 알 수 있습니다.

## Outlook 보호 규칙의 조건자

Outlook 보호 규칙에서는 세 개의 조건자를 사용하여 Outlook 2010에서 IRM 보호를 자동으로 적용할 수 있습니다.

  - **FromDepartment**   *FromDepartment* 조건자는 Active Directory에서 보낸 사람의 부서 특성을 조회하고 보낸 사람의 부서가 규칙에 지정된 부서와 일치할 경우 자동으로 메시지를 IRM으로 보호합니다. 예를 들어 Outlook 보호 규칙을 만들어 연구 부서에서 보낸 모든 메시지를 자동으로 보호할 수 있습니다.

  - **SentTo**   조직에서는 모든 회사 또는 재무 메일 그룹과 같은 중요한 받는 사람에게 보내진 메시지를 보호해야 할 수 있습니다. *SentTo* 조건자를 사용하면 Outlook 보호 규칙을 만들어 지정된 받는 사람에게 보내진 메시지를 자동으로 IRM으로 보호할 수 있습니다.

  - **SentToScope**   *SentToScope* 조건자를 사용하면 Outlook 보호 규칙을 만들어 조직 내부 또는 외부로 보내진 메시지를 자동으로 IRM으로 보호할 수 있습니다. 예를 들어 *FromDepartment* 조건자와 함께 *SentToScope* 조건자를 사용하여 특정 부서가 내부 사용자에게 보낸 메시지를 IRM으로 보호할 수 있습니다.

