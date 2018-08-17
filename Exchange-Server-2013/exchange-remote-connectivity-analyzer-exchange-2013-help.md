---
title: 'Exchange 원격 연결 분석기: Exchange 2013 Help'
TOCTitle: Exchange 원격 연결 분석기
ms:assetid: dd26698e-d00c-47f5-a7aa-c3894fe86c75
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff701693(v=EXCHG.150)
ms:contentKeyID: 50484370
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 원격 연결 분석기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-09-22_

ExRCA(MicrosoftExchange 원격 연결 분석기)를 통해 Exchange 서버 연결이 올바르게 설정되었는지 확인할 수 있습니다. 또한 문제가 있는 경우 해당 문제를 찾아서 해결할 수 있습니다. ExRCA 웹 사이트에서 테스트를 실행하여 MicrosoftExchange ActiveSync, Exchange 웹 서비스, MicrosoftOutlook 및 인터넷 전자 메일 연결을 확인할 수 있습니다.

## 원격 연결 분석기 테스트

ExRCA를 사용하여 몇 가지 테스트를 수행할 수 있습니다. 다음 테스트는 Exchange 2007 이상 버전에서 작동합니다.

  - Exchange ActiveSync

  - Exchange 웹 서비스

  - Outlook

  - 인터넷 전자 메일

## Exchange ActiveSync 테스트

Exchange ActiveSync에 대해 다음 테스트를 실행할 수 있습니다.

  - **Exchange ActiveSync:**  이 테스트에서는 모바일 장치에서 Exchange ActiveSync를 사용하여 Exchange 서버에 연결하는 데 사용하는 단계를 시뮬레이션합니다.

  - **Exchange ActiveSync Autodiscover:**  이 테스트에서는 Exchange ActiveSync 장치에서 자동 검색 서비스를 통해 설정을 가져오는 데 사용되는 단계를 살펴봅니다.

## Exchange 웹 서비스 연결 테스트

Exchange 웹 서비스 테스트에는 다양 한 Exchange 웹 서비스 대 한 설정을 확인합니다. Exchange 웹 서비스에 대 한 다음 테스트를 실행할 수 있습니다.

  - **동기화, 알림, 가용성 및 자동 회신:**  이 테스트에서는 작동 상태를 확인하는 여러 가지 기본 Exchange 웹 서비스 작업을 살펴봅니다. 이 테스트는 IT 관리자가 Entourage EWS 또는 다른 웹 서비스 클라이언트를 사용하여 외부 액세스 문제를 해결하는 데 유용합니다.

  - **서비스 계정 액세스(개발자):**  이 테스트에서는 서비스 계정에서 지정된 사서함에 액세스하고, 해당 사서함에서 항목을 만들거나 삭제하고, Exchange 가장을 통해 사서함에 액세스할 수 있는지 확인합니다. 이 테스트는 응용 프로그램 개발자가 대체 자격 증명으로 사서함에 액세스할 수 있는지 테스트하는 데 주로 사용됩니다.

## Microsoft Office Outlook 연결 테스트

Outlook 연결에 대해 다음 테스트를 실행할 수 있습니다.

  - **Outlook Anywhere(RPC over HTTP):**  이 테스트에서는 Outlook에서 Outlook Anywhere(RPC over HTTP)를 통해 연결하는 데 사용되는 단계를 살펴봅니다.

  - **Outlook Autodiscover:**  이 테스트에서는 Outlook에서 자동 검색 서비스를 통해 설정을 가져오는 데 사용되는 단계를 살펴봅니다. 실제로 이 테스트에서는 사서함에 연결하지 않습니다.

## 인터넷 전자 메일 테스트

인터넷 전자 메일에 대해 다음 테스트를 실행할 수 있습니다.

  - **인바운드 SMTP** **전자 메일:**  이 테스트에서는 내부 전자 메일 서버에서 도메인으로 인바운드 SMTP 전자 메일을 보내는 데 사용되는 단계를 살펴봅니다.

  - **아웃바운드 SMTP 전자 메일:**  이 테스트에서는 아웃바운드 IP 주소에 대한 특정 요구 사항을 살펴봅니다. 여기에는 역방향 DNS, 보낸 사람 ID 및 RBL 확인이 포함됩니다.

  - **POP 전자 메일:**  이 테스트에서는 전자 메일 클라이언트에서 POP3을 사용하여 사서함에 연결하는 데 사용되는 단계를 살펴봅니다.

  - **IMAP 전자 메일:**  이 테스트에서는 전자 메일 클라이언트에서 IMAP를 사용하여 사서함에 연결하는 데 사용되는 단계를 살펴봅니다.

