---
title: '보낸사람 ID: Exchange 2013 Help'
TOCTitle: 보낸사람 ID
ms:assetid: 0f628f83-df8c-43fb-bf49-7aaa9ec69ab1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996295(v=EXCHG.150)
ms:contentKeyID: 50482486
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보낸사람 ID

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

보낸 사람 ID 에이전트는 Microsoft Exchange Server 2013에서 사용할 수 있는 스팸 방지 에이전트입니다. 받는 사람 ID 에이전트는 RECEIVED SMTP 헤더와 보내는 시스템의 DNS 서비스에 대한 쿼리에 따라 수신 메시지에 대해 수행할 작업(있는 경우)을 결정합니다.

보낸 사람 ID는 보낸 사람과 도메인을 가장하는 *스푸핑*을 퇴치하는 방법입니다. *스푸핑된 메일*은 실제로 메시지를 보내지 않은 사람이 전자 메일 메시지를 보낸 것처럼 보이도록 주소가 수정된 전자 메일 메시지입니다.

스푸핑된 메일에는 보통 특정 조직에서 온 것으로 가장하는 보낸 사람 주소가 포함됩니다. 전에는 헤더의 유효성을 검증하지 않았기 때문에 MAIL FROM: 헤더와 보낸 사람: "Masato Kawai" masato@contoso.com 등의 RFC 2822 메시지 데이터와 같은 두 가지 SMTP 세션 모두에서 보낸 사람 주소를 스푸핑하기가 비교적 쉬웠습니다.

**목차**

Using Sender ID to combat spoofing

Updating your organization's Internet-facing DNS to support Sender ID

Specifying recipients and sender domains to exclude from Sender ID filtering

## 보낸 사람 ID를 사용하여 스푸핑 퇴치

보낸 사람 ID를 사용하면 스푸핑이 어려워집니다. 보낸 사람 ID를 사용하도록 설정하면 각 메시지의 메시지 메타데이터에 보낸 사람 ID 상태가 포함됩니다. 전자 메일 메시지를 받으면 Exchange 서버에서는 메시지를 보낸 IP 주소가 메시지 헤더에 지정된 도메인으로 메시지를 보낼 권한이 있는지 보낸 사람의 DNS 서버에 쿼리합니다. 권한이 부여된 보내는 서버의 IP 주소를 PRA(Purported Responsible Address)라고 합니다.

도메인 관리자가 해당 DNS 서버에 보낸 사람이 정책 프레임 워크 (SPF) 레코드를 게시 합니다. 권한이 부여 된 아웃 바운드 전자 메일 서버를 식별 하는 SPF 레코드. SPF 레코드를 보낸 사람의 DNS 서버에 구성 된 경우에 Exchange server SPF 레코드를 구문 분석 하 고 전자 메일을 보내는 메시지에 지정 된 도메인을 대신 하 여 메시지를 받은 IP 주소 권한이 있는지 여부를 결정 합니다. SPF 레코드를 포함 하는 기능 및 SPF 레코드를 만드는 방법에 대 한 자세한 내용은 [보낸사람 ID](https://go.microsoft.com/fwlink/p/?linkid=50977)을 참조 하십시오.

Exchange 서버는 SPF 레코드에 따라 보낸 사람 ID 상태로 메시지 메타데이터를 업데이트합니다. Exchange 서버가 메시지 메타데이터를 업데이트하면 메시지는 원래대로 배달됩니다.

## 보낸 사람 ID 상태 값

보낸 사람 ID 평가 프로세스에서 메시지의 보낸 사람 ID 상태가 생성됩니다. 보낸 사람 ID 상태는 메시지의 SCL(스팸 지수) 등급을 평가하는 데 사용됩니다. 다음 값 중 하나로 이 상태를 설정할 수 있습니다.

  - **Pass**   IP 주소 및 PRA(Purported Responsible Address)가 모두 보낸 사람 ID 유효성 검사를 통과했습니다.

  - **Neutral**   게시된 보낸 사람 ID 데이터가 명시적으로 확실치 않습니다.

  - **Soft fail**   PRA의 IP 주소가 허용되지 않은 집합에 포함될 수 있습니다.

  - **Fail**   IP 주소가 허용되지 않거나, 수신 메일에서 PRA를 찾을 수 없거나, 보내는 도메인이 없습니다.

  - **None**   보낸 사람의 DNS에 게시된 SPF 데이터가 없습니다.

  - **TempError**   사용할 수 없는 DNS 서버와 같은 일시적인 DNS 오류가 발생했습니다.

  - **PermError**   레코드 형식 오류와 같은 잘못된 DNS 레코드입니다.

보낸 사람 ID 상태는 메시지 메타데이터에 추가되고 나중에 MAPI 속성으로 변환됩니다. Microsoft Outlook의 정크 메일 필터에서는 SCL 값을 생성하는 동안 MAPI 속성을 사용합니다.

Outlook에서는 보낸 사람 ID 상태를 표시하거나 특정 ID 값의 메시지를 정크로 플래그 지정하지 않습니다. Outlook은 SCL 값을 계산할 때만 보낸 사람 ID 상태 값을 사용합니다.

보낸 사람 ID 상태를 생성하는 7개의 시나리오 이외에 보낸 사람 ID 평가 프로세스를 통해 보낸 사람 IP 주소가 누락된 인스턴스를 확인할 수 있습니다. 보낸 사람: IP 주소가 누락되어 있으면 보낸 사람 ID 상태를 설정할 수 없습니다. 보낸 사람 ID 상태를 설정할 수 없으면 Exchange에서 보낸 사람 ID를 메시지에 포함하지 않고 메시지를 계속 처리합니다. 메시지는 무시되거나 거부되지 않습니다. 이 시나리오에서는 보낸 사람 ID 상태가 설정되지 않고 응용 프로그램 이벤트가 기록됩니다.

메시지에 보낸 사람 ID 상태를 표시하는 방법에 대한 자세한 내용은 [스팸 방지 스탬프](anti-spam-stamps-exchange-2013-help.md)를 참조하십시오.

## 스푸핑된 메일 및 연결할 수 없는 DNS 서버 처리를 위한 보낸 사람 ID 옵션

또한 Exchange 서버에서 스푸핑된 메일로 식별된 메시지를 처리하는 방법 및 DNS 서버에 연결할 수 없는 경우 Exchange 서버에서 메시지를 처리하는 방법을 정의할 수 있습니다. Exchange 서버에서 스푸핑된 메일과 연결할 수 없는 DNS 서버를 처리하는 방법을 정의하는 옵션에는 다음 작업이 포함됩니다.

  - **상태 스탬프 처리**   이 옵션은 기본 작업입니다. 조직의 모든 인바운드 메시지에 대한 메시지 메타데이터에는 보낸 사람 ID 상태가 포함됩니다.

  - **거부**   메시지를 거부하고 보내는 서버에 SMTP 오류 응답을 보냅니다. SMTP 오류 응답은 보낸 사람 ID 상태에 대한 텍스트를 포함하는 5*xx* 수준의 프로토콜 응답입니다.

  - **삭제**   보내는 시스템에 삭제에 대해 알리지 않고 메시지를 삭제합니다. 실제로 Exchange 서버는 보내는 서버에 위장 확인 SMTP 명령을 보낸 후 메시지를 삭제합니다. 보내는 서버에서는 메시지를 보냈다고 간주하므로 같은 세션에서 메시지를 다시 보내려고 하지 않습니다.

보낸 사람 ID 에이전트를 구성하는 방법에 대한 자세한 내용은 [보낸사람 ID 관리](manage-sender-id-exchange-2013-help.md)항목을 참조하십시오.

맨 위로 이동

## 보낸 사람 ID를 지원하도록 조직의 인터넷 지향 DNS 업데이트

보낸 사람 ID의 효과성은 DNS 데이터에 따라 다릅니다. SPF 레코드를 사용하여 인터넷 지향 DNS 서버를 업데이트하는 조직이 많을수록 보낸 사람 ID를 통해 스푸핑된 전자 메일 메시지를 더 효과적으로 식별할 수 있습니다.

보낸사람 ID 인프라를 지원 하기 위해 SPF 레코드를 만들고 공용 DNS 서버에서 SPF 레코드를 호스트 하 여 인터넷 연결 DNS 데이터를 업데이트 해야 합니다. 작성 및 SPF 레코드를 배포 하는 방법에 대 한 자세한 내용은 [보낸사람 ID](https://go.microsoft.com/fwlink/p/?linkid=50977)을 참조 하십시오.

맨 위로 이동

## 보낸 사람 ID 필터링에서 제외할 받는 사람 도메인 및 보낸 사람 도메인 지정

보낸 사람 ID 필터링에서 특정 받는 사람이나 보낸 사람 도메인을 제외해야 할 수도 있습니다. 이렇게 하려면 Exchange 관리 셸에서 **Set-SenderIdConfig** cmdlet을 사용하여 받는 사람 및 보낸 사람 도메인을 지정합니다. 자세한 내용은 [Set-SenderIdConfig](https://technet.microsoft.com/ko-kr/library/aa998859\(v=exchg.150\))를 참조하십시오.

맨 위로 이동

