---
title: '메시지 서명 및 암호화를 위한 S/MIME: Exchange 2013 Help'
TOCTitle: 메시지 서명 및 암호화를 위한 S/MIME
ms:assetid: 887c710b-0ec6-4ff0-8065-5f05f74afef3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn626158(v=EXCHG.150)
ms:contentKeyID: 61212686
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 메시지 서명 및 암호화를 위한 S/MIME

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

S/MIME(Secure/Multipurpose Internet Mail Extensions)은 디지털 서명된 메시지와 암호화된 메시지를 보내는 데 널리 사용되는 방법(정확하게는 프로토콜)입니다. S/MIME을 사용하면 전자 메일을 암호화하고 디지털로 서명할 수 있습니다. 전자 메일 메시지에 S/MIME을 사용하면 해당 메시지를 받는 사람이 받은 편지함에 표시된 메시지가 보낸 사람이 작성한 것과 정확히 일치하는 메시지이며, 특정 보낸 사람을 가장하는 사람이 아닌 실제 보낸 사람이 메시지를 보냈음을 확신할 수 있습니다. 이를 위해 S/MIME에서는 디지털 서명을 사용하여 인증, 메시지 무결성, 원본 거부 없음 등의 암호화 보안 서비스가 제공됩니다. 또한 전자 방식 메시징을 위해 암호화를 사용하여 개인 정보와 데이터 보안이 개선될 수 있도록 합니다. 전자 메일 분야에서 S/MIME의 발전 이력과 구조에 대한 전체 배경 정보를 파악하려면 [S/MIME 이해](https://go.microsoft.com/fwlink/?linkid=393948)를 참조하세요.

Exchange 2013 SP1 또는 Exchange Online(Office 365의 일부분)에 사서함이 있는 경우 관리자는 조직에 대해 S/MIME 기반 보안을 사용하도록 설정할 수 있습니다. 아래에 링크되어 있는 항목의 지침에 따라 Exchange 관리 셸을 사용하여 S/MIME을 설정합니다. Exchange 2013 SP1 또는 Exchange Online을 통해 지원되는 Outlook 또는 ActiveSync 버전에서 S/MIME을 사용하려면 조직의 사용자에게 서명 및 암호화용으로 발급된 인증서가 있어야 하며 데이터를 온-프레미스 AD DS(Active Directory 도메인 서비스)에 게시해야 합니다. AD DS는 인터넷의 클라우드 서비스 또는 원격 시설이 아닌 관리자가 제어할 수 있는 물리적 위치의 컴퓨터에 있어야 합니다. AD DS에 대한 자세한 내용은 [Active Directory 도메인 서비스](https://go.microsoft.com/fwlink/?linkid=394064)를 참조하세요.

## 지원되는 시나리오 및 기술 고려 사항

조직에서 Exchange 2013 SP1 또는 Exchange Online을 사용하는 경우 다음 끝점에서 작동하도록 S/MIME을 설정할 수 있습니다.

  - Outlook 2010

  - Outlook 2013

  - Outlook Web App

  - EAS(Exchange ActiveSync)

이러한 각 끝점에 대해 S/MIME을 설정하기 위해 수행하는 단계는 선택하는 항목에 따라 약간씩 다릅니다. 일반적으로는 다음 작업을 수행해야 합니다.

  - S/MIME 인증서를 발급하도록 Windows 기반 인증 기관을 설치하고 공개 키 인프라를 설정합니다. 타사 인증서 공급자가 발급한 인증서도 지원됩니다. 자세한 내용은 [Active Directory 인증서 서비스 개요](https://technet.microsoft.com/library/hh831740.aspx)를 참조하세요.

  - UserSMIMECertificate 및/또는 UserCertificate 특성의 온-프레미스 AD DS 계정으로 사용자 인증서를 게시합니다.

  - Exchange Online 조직의 경우 해당하는 DirSync 버전을 사용하여 AD DS에서 Azure Active Directory로 사용자 인증서를 동기화합니다. 그러면 이러한 인증서가 Azure Active Directory에서 Exchange Online 디렉터리로 동기화되며 받는 사람에 대한 메시지를 암호화할 때 사용됩니다.

  - S/MIME의 유효성을 검사하기 위해 가상 인증서 모음을 설정합니다. 전자 메일의 서명 유효성을 검사하여 전자 메일이 신뢰할 수 있는 인증서를 통해 서명되었음을 확인할 때 OWA에서 이 정보가 사용됩니다.

  - S/MIME을 사용하도록 Outlook 또는 EAS 끝점을 설정합니다.

## Outlook Web App에서 S/MIME 설정

Outlook Web App이 포함된 Exchange 2013 SP1 또는 Exchange Online에 대해 S/MIME을 설정하려면 다음 주요 단계를 수행합니다.

1.  [Outlook Web App에 대 한 S/MIME 설정 구성](configure-s-mime-settings-for-outlook-web-app-exchange-2013-help.md)

2.  [S/MIME 유효성을 검사 하려면 가상 인증서 컬렉션 설정](set-up-virtual-certificate-collection-to-validate-s-mime-exchange-2013-help.md)

3.  [S/MIME용으로 Office 365에 사용자 인증서 동기화](https://technet.microsoft.com/ko-kr/library/dn626159\(v=exchg.150\)) 이 단계는 Exchange Online에만 적용됩니다.

## 관련 메시지 암호화 기술

메시지 보안의 중요도가 높아지면서 관리자는 메시지 보호 원칙 및 개념을 이해해야 합니다. 특히 S/MIME 등의 다양한 보호 관련 기술이 제공되면서 이러한 이해의 중요성도 더욱 높아지고 있습니다. S/MIME 및 전자 메일과 관련하여 S/MIME이 작동하는 방식에 대해 자세히 알아보려면 [S/MIME 이해](https://go.microsoft.com/fwlink/?linkid=393948)를 참조하세요. 다양한 암호화 기술이 연동되어 저장된 메시지 및 전송 중인 메시지를 보호합니다. S/MIME은 다음 기술과 동시에 사용할 수 있지만 이러한 기술에 종속되는 것은 아닙니다.

  -  <strong>TLS(전송 계층 보안)</strong>는 스누핑 및 도청을 방지하기 위해 전자 메일 서버 간의 터널/경로를 암호화합니다.

  -  <strong>SSL(Secure Sockets Layer)</strong>은 전자 메일 클라이언트와 Office 365 서버 간의 연결을 암호화합니다.

  -  **BitLocker**는 데이터 센터의 하드 드라이브에 저장된 데이터를 암호화하여 무단으로 액세스하는 사용자가 해당 데이터를 읽을 수 없도록 합니다.

## Office 365 메시지 암호화와 S/MIME 비교

S/MIME을 사용하려면 대개 기업 간, 그리고 기업과 소비자 간에 사용되는 게시 인프라와 인증서가 필요합니다. 사용자는 S/MIME의 암호화 키를 제어하며 보내는 각 메시지에 해당 키를 사용할지 여부를 선택할 수 있습니다. Outlook 등의 전자 메일 프로그램에서는 디지털 서명 및 서명 확인을 수행하기 위한 신뢰할 수 있는 루트 인증 기관 위치를 검색합니다. Office 365 메시지 암호화는 조직 내부 또는 외부의 모든 사용자에게 보내는 메일을 암호화하기 위해 개별 사용자가 아닌 관리자가 구성할 수 있는 정책 기반 암호화 서비스이며, RMS(Azure 권한 관리)를 기반으로 구축되며 공개 키 인프라를 사용하지 않는 온라인 서비스입니다. 또한 Office 365 메시지 암호화에서는 조직의 브랜드로 메일을 사용자 지정하는 기능 같은 추가 기능도 제공됩니다. Office 365 메시지 암호화에 대한 자세한 내용은 [Office 365 메시지 암호화](https://go.microsoft.com/fwlink/?linkid=392525)를 참조하세요.

## 추가 정보

[Outlook Web App](outlook-web-app-exchange-2013-help.md)

[보안 메일(2000)](http://technet.microsoft.com/ko-kr/library/cc962043.aspx)

