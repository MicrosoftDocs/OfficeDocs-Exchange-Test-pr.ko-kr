---
title: '저널 보고서 암호 해독: Exchange 2013 Help'
TOCTitle: 저널 보고서 암호 해독
ms:assetid: c063e2bd-2444-480d-8b35-73f31064a31b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876936(v=EXCHG.150)
ms:contentKeyID: 50484063
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 저널 보고서 암호 해독

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-16_

Microsoft Exchange Server 2013에서는 Microsoft Outlook 2010 이상 버전 및 Microsoft Office Outlook Web App 사용자가 IRM(정보 권한 관리)을 통해 메시지를 보호할 수 있습니다. Outlook 2010 클라이언트에서 메시지를 보내기 전에 IRM 보호를 자동으로 적용하는 Outlook 보호 규칙을 만들 수 있습니다. 뿐만 아니라 규칙 조건과 일치하는 전송 메시지에 IRM 보호를 적용하는 전송 보호 규칙도 만들 수 있습니다.

Outlook 보호 규칙에 대한 자세한 내용은 [Outlook 보호 규칙](outlook-protection-rules-exchange-2013-help.md)를 참조하십시오.

## 표준 암호화 솔루션의 제한 사항

조직에서 S/MIME와 같은 기존 솔루션을 사용하여 메시지를 암호화하는 경우 레코드 관리자가 암호화된 콘텐츠를 검사하거나 검색할 수 없습니다. 액세스 및 검색할 수 없는 콘텐츠가 들어 있는 암호화된 메시지를 보관할 경우 비즈니스 요구 사항, 규정 또는 규정 준수 요구 사항에 위배될 소지가 있습니다. 이 경우 전자 검색(eDiscovery) 요청이 있을 경우 암호화된 메시지를 해독하고 검색하는 데 어려움을 겪고, 결국 조직이 법적/금전적 손해를 입을 수 있습니다.

eDiscovery 도구, 자동화된 프로세스 또는 저널링 사서함을 액세스하는 레코드 관리자가 액세스할 수 있도록 저널링된 메시지를 암호 해독할 것을 규정하는 조직의 메시징 정책도 적용될 수 있습니다. Exchange 2010의 저널 보고서 암호 해독 기능은 이러한 요구 사항을 준수하는 데 도움을 줍니다.

저널링에 대한 자세한 내용은 [저널링](journaling-exchange-2013-help.md)를 참조하십시오.

## 저널 보고서 암호 해독

저널 보고서 암호 해독 기능을 사용하면 IRM 보호 메시지의 일반 텍스트 복사본을 원본 IRM 보호 메시지와 함께 저널 보고서에 저장할 수 있습니다. IRM 보호 메시지에 포함된 지원되는 첨부 파일이 조직의 AD RMS(Active Directory Rights Management Services) 클러스터에서 보호되는 경우 해당 첨부 파일도 암호 해독됩니다.


> [!IMPORTANT]
> 저널링 보고서 암호 해독 기능을 사용하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 있어야 합니다. 저널 보고서 암호 해독 기능은 고급 저널링만 지원합니다.



암호 해독 작업은 규정 준수 중심 전송 에이전트인 저널 보고서 암호 해독 에이전트에서 수행됩니다. 저널 보고서 암호 해독 에이전트는 **OnCategorizedMessage** 이벤트가 발생하면 실행됩니다. 전송되는 동안 전송 보호 규칙을 사용하여 보호되는 메시지는 저널 보고서 암호 해독 에이전트에 전달되기 전에 이미 **OnRoutedMessage** 이벤트 발생 시에 실행되는 암호 에이전트를 통해 암호화되어 있습니다. 저널 보고서 암호 해독 에이전트는 이러한 메시지를 암호 해독합니다.


> [!NOTE]
> Exchange 2013에서 저널 보고서 암호 해독 에이전트는 기본 제공 에이전트입니다. 기본 제공 에이전트는 <STRONG>Get-TransportAgent</STRONG> cmdlet에서 반환되는 에이전트 목록에 포함되지 않습니다. 자세한 내용은 <A href="transport-agents-exchange-2013-help.md">전송 에이전트</A>를 참조하십시오.



저널 보고서 암호 해독 에이전트는 다음과 같은 유형의 IRM 보호 메시지를 암호 해독합니다.

  - Outlook Web App에서 사용자가 IRM를 통해 보호한 메시지

  - Outlook 2010에서 사용자가 IRM를 통해 보호한 메시지

  - Outlook 2010에서 Outlook 보호 규칙을 사용하여 자동으로 IRM을 통해 보호된 메시지

  - 전송 보호 규칙을 사용하여 자동으로 IRM을 통해 보호된 전송 메시지


> [!IMPORTANT]
> 조직의 AD&nbsp;RMS 서버에서 IRM을 통해 보호된 메시지만 저널 보고서 암호 해독 에이전트에서 암호 해독됩니다. 메시지와 동시에 보호되지 않아 동일한 사용 라이선스가 없는 첨부 파일이나 보호되지 않은 메시지에 첨부된 IRM 보호 파일은 이 에이전트에서 암호 해독되지 않습니다.



## 저널 보고서 암호 해독 구성

저널 보고서 암호 해독은 Exchange 관리 셸에서 [Set-IRMConfiguration](https://technet.microsoft.com/ko-kr/library/dd979792\(v=exchg.150\)) cmdlet을 사용하여 구성할 수 있습니다. 단, 저널 보고서 암호 해독을 구성하려면 먼저 AD RMS 서버에서 IRM을 통해 보호된 콘텐츠를 암호 해독할 수 있는 권한을 Exchange 2013 서버에 할당해야 합니다. 이를 위해서는 조직의 AD RMS 클러스터에 있는 Super Users 그룹에 페더레이션 사서함을 추가해야 합니다. 자세한 내용은 [AD RMS 슈퍼 사용자 그룹에는 페더레이션 사서함을 추가 합니다.](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> 각 포리스트에 AD&nbsp;RMS 클러스터가 배포되는 포리스트 간 AD RMS 배포 환경에서는 각 포리스트의 AD&nbsp;RMS 클러스터에 대한 Super Users 그룹에 페더레이션 사서함을 추가하여 Exchange 2013 전송 서비스에서 각 AD&nbsp;RMS 클러스터에 대해 보호된 메시지를 암호 해독할 수 있도록 해야 합니다.



저널 보고서 암호 해독을 구성하는 방법에 대한 자세한 내용은 [저널 보고서 암호 해독을 사용 하지 않도록 설정 하거나 사용](enable-or-disable-journal-report-decryption-exchange-2013-help.md)을 참조하십시오.

저널 보고서 암호 해독 기능을 사용하도록 설정한 후에는 중요 정보가 들어 있는 저널 보고서가 암호화되지 않은 형식으로 저널링 사서함에 포함될 수 있습니다. 따라서 저널링 사서함에 대한 액세스를 자세히 모니터링하고 권한 있는 사용자만 액세스하도록 제한해야 합니다. 전자 메일에 IRM 보호 기능을 사용하지 않는 경우에도 마찬가지입니다.

