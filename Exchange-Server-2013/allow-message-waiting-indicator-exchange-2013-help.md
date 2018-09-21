---
title: '메시지 대기 표시기를 허용 합니다.: Exchange 2013 Help'
TOCTitle: 메시지 대기 표시기를 허용 합니다.
ms:assetid: 57fb439e-8208-499f-a20b-814677843a8c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298001(v=EXCHG.150)
ms:contentKeyID: 54651816
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지 대기 표시기를 허용 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-03-09_

MWI(Message Waiting Indicator)는 대부분의 레거시 음성 메일 시스템에서 사용되는 기능으로, 사용자에게 새 음성 메일 메시지나 듣지 않은 음성 메일 메시지가 있음을 알려줍니다. 가장 일반적인 형태로, 새 음성 메시지나 듣지 않은 음성 메시지가 있음을 나타내기 위해 사용자의 전화기에서 램프가 켜집니다.

**목차**

개요

The Mailbox server's role in MWI

MWI SIP NOTIFY messages

MWI resilience

MWI administration

Text message (SMS) notifications for voice mail messages and missed calls

## 개요

MWI 알림에는 새 음성 메시지나 듣지 않은 음성 메시지가 있음을 나타내는 모든 메커니즘이 포함될 수 있습니다. 메시지는 새 전자 메일 메시지이거나 읽지 않은 상태로 표시된 전자 메일 메시지일 수 있습니다. MWI 알림에는 다음 양식 중 하나가 사용될 수 있습니다.

  - Microsoft Outlook 또는 Outlook Web App에서 볼 수 있는 새 음성 메시지

  - 문자 메시지를 수신하도록 구성된, 휴대폰으로 전송되는 텍스트 또는 SMS(Short Messaging Service) 메시지

  - Exchange UM(통합 메시징)에서 거는 아웃바운드 전화

  - 전화기의 램프

  - 특수 발신음

  - 전화기 화면의 아이콘 또는 단추

  - 소프트웨어 응용 프로그램에서 알림 강조 표시

통합 메시징에서 사용자의 음성 메일은 자신의 사서함에 저장되며, Outlook Voice Access를 사용하는 전화기, Outlook 또는 Outlook Web App을 사용하는 데스크톱이나 PC, 휴대폰 클라이언트 등에서 액세스할 수 있습니다. 사용자가 새 음성 메시지를 수신하면 음성 메일 검색 폴더에 메시지가 표시됩니다. Outlook 또는 Outlook Web App을 사용하여 음성 메시지에 액세스하는 경우 전자 메일 메시지가 음성 메시지와 함께 포함됩니다.

조직에 이전 버전의 UM이 배포되어 있으면 타사 솔루션이나 응용 프로그램을 사용하여 기존 VoIP 게이트웨이 환경이나 IP PBX 환경에서 MWI가 지원되거나 Exchange UM 일부로 포함되어 있습니다. Exchange 2010 이상에서는 Microsoft Lync Server에 UM이 배포된 경우 MWI도 지원됩니다. Lync Server에서 사용되는 MWI 알림 메커니즘은 Enterprise Voice 및 UM 사용 가능 사용자가 사용하는 VoIP 기반 전화 유형에 따라 다르며, 다음 중 하나에 있을 수 있습니다.

  - 전화기

  - 전화기 화면

  - 다이얼 패드 단추

기본적으로 MWI는 UM을 사용할 수 있는 모든 사용자에 대해 설정되며, UM 사서함 정책이나 UM 다이얼 플랜을 만들고 이 플랜에 연결된 UM IP 게이트웨이의 설정을 통해 제어됩니다. 또한 MWI는 보호된 음성 메시지에도 작동합니다.

VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX를 포함한 기존의 전화 통신 환경에서 MWI를 구현하기 위해 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버는 MWI SIP(Session Initiation Protocol) NOTIFY 메시지를 IP PBX, 레거시 PBX에 사용되는 VoIP 게이트웨이, SIP 사용 가능 PBX 중 하나로 표시되는 *SIP 피어*에 전송합니다. Lync Server를 배포한 경우에는 Lync 서버도 SIP 피어로 고려됩니다. 그러면 IP PBX 또는 PBX는 데스크톱 전화기의 램프를 켜서 사용자에게 새 음성 메시지 또는 듣지 않은 음성 메시지가 있음을 알립니다.

발신자는 두 가지 방법 즉 전화 응답 및 Outlook Voice Access 중 하나를 사용하여 음성 메시지를 남길 수 있습니다. 전화 응답에서는 사서함 서버가 수신 전화에 응답하고 발신자가 사용자에게 음성 메시지를 남길 수 있습니다. Outlook Voice Access에서는 발신자가 Outlook Voice Access 번호로 전화를 걸어 메뉴 시스템을 사용하여 UM 사용 가능 사용자에게 음성 메시지를 남길 수 있습니다.

맨 위로 이동

## MWI에서의 사서함 서버의 역할

발신자가 UM 사용 가능 사용자에게 전화를 걸었을 때 사용자가 전화를 받지 않으면 사서함 서버의 Microsoft Exchange 통합 메시징 서비스는 MWI 상태 변경 정보를 수신하고 SIP NOTIFY 메시지를 사용하여 VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX로 알림 변경 요청을 전송합니다. 알림 변경에는 다음 정보가 포함됩니다.

  - Message Waiting Indicator 사용 설정(예 또는 아니요)

  - 새 음성 메시지 또는 표시된 듣지 않은 음성 메시지 수

  - 이전에 수신하거나 표시된 들은 음성 메시지 수

  - 새 긴급 음성 메시지 또는 표시된 듣지 않은 긴급 음성 메시지 수

  - 이전에 수신한 긴급 음성 메시지 또는 표시된 들은 긴급 음성 메시지 수

  - 기본 UM 다이얼 플랜의 기본 내선 번호

  - SIP NOTIFY 메시지에 사용할 SIP 피어의 IP 주소 또는 FQDN(정규화된 도메인 이름)

  - UM 다이얼 플랜의 보안 유형(보안되지 않음, SIP 보안 또는 보안). 이 정보는 SIP over TCP 또는 SIP over TLS 중 어떤 VoIP 게이트웨이나 IP PBX 연결을 사용해야 할지를 결정하는 데 사용됩니다. TLS(전송 계층 보안)는 MWI SIP NOTIFY에 지원됩니다.

사서함 서버는 수신 전화의 헤더에 대한 전환 정보를 사용하여 UM 사용 가능 사용자의 내선 번호 또는 전화 번호를 확인합니다. 내선 번호 또는 전화 번호를 확인하면 사서함 서버는 SIP 피어에 요청을 전송합니다. 그런 다음 SIP 피어는 MWI 상태를 변경하고 사용자 전화기의 알림을 켭니다.


> [!NOTE]
> PBX 중단은 없어야 하지만 UM은 모든 사서함의 MWI 상태를 적어도 12시간마다 한 번씩 자동으로 새로 고칩니다. 새로 고침을 강제로 수행할 방법은 없지만 PBX나 IP PBX가 꺼지고 모든 MWI 램프가 꺼지면 모든 램프가 6시간 내에 올바른 상태로 복원되어야 합니다.



맨 위로 이동

## MWI SIP NOTIFY 메시지

MWI 알림은 SIP NOTIFY 메시지를 사용하여 SIP 피어와 통신합니다. MWI 상태 변경 정보는 SIP NOTIFY 메시지에 포함되어 MWI 알림이 사용자에게 전송될지 여부를 나타냅니다. MWI 상태가 변경될 때마다 사서함 도우미가 이 정보를 사서함 서버에서 실행되는 Microsoft Exchange 통합 메시징 서비스로 전송합니다. 통합 메시징 서비스가 이 정보를 수신한 후에는 메시지를 분석하여 대상 SIP 피어 및 MWI 상태 변경 정보를 가져옵니다. 그런 다음에는 메시지 본문의 MWI 상태 변경 정보로 SIP NOTIFY 메시지를 구성하여 SIP 피어로 해당 정보를 전송합니다.

MWI는 RFC 3842를 기반으로 합니다. RFC 3842는 SIP 이벤트 알림을 메시지 대기 알림에 사용하도록 명시하고 있습니다. MWI는 SIP 모델을 기반으로 하며, 통합 메시징 시스템에 있는 끝점에 의해 작동합니다. MWI 정보를 가져오는, SIP 피어라고도 하는 SIP 끝점은 통합 메시징 서비스로 SIP SUBSCRIBE 메시지를 전송해야 합니다. 서비스에서 구독을 수락하는 NOTIFY 메시지와 함께 회신합니다. 모든 MWI 상태 변경 정보는 이전에 만들어진 구독에 포함된 NOTIFY 메시지를 사용하여 통합 메시지 시스템에서 SIP 끝점으로 전달됩니다. SIP 피어로 전송되는 SIP NOTIFY 메시지의 정확한 구문은 RFC 3842에 명시된 형식을 기반으로 합니다.

사서함 서버의 통합 메시징 서비스가 SIP 피어로 MWI NOTIFY 메시지를 전송하면 이벤트 헤더가 MWI 관련 NOTIFY 메시지임을 나타내는 "메시지-요약"으로 설정됩니다. 받는 사람 헤더 필드는 MWI 서비스가 제공될 SIP 끝점을 나타냅니다. 구독-상태 헤더는 "활성"이 아닌 "종료"로 설정해야 합니다. SIP NOTIFY 메시지에 응답하여 다음 작업이 수행됩니다.

1.  SIP 피어는 SMDI와 같은 회로 전환 프로토콜을 사용하여 PBX로 이 정보를 전달합니다.

2.  PBX는 회로 전환 프로토콜을 통해 성공 메시지를 전송합니다.

3.  SIP 피어가 응답으로 사용할 수 있는 메시지는 200 OK(성공) 또는 480(일시적으로 사용할 수 없음)입니다. 사서함 서버는 이 두 가지 응답과 추가 실패 응답을 모두 처리할 수 있습니다.

## 기존 전화 통신 환경의 MWI

기존의 전화 통신 환경에서는 수신 전화가 PBX에서 수신된 후 VoIP 게이트웨이로 전송되거나 IP PBX 또는 SIP 사용 가능 PBX에서 수신됩니다. 사서함 서버 및 사서함 도우미는 UM 사용 가능 사용자의 MWI 상태를 확인하는 데 사용되며, SIP 알림을 VoIP 게이트웨이, 레거시 PBX, IP PBX 또는 SIP 사용 가능 PBX로 다시 전달합니다.

기존의 전화 통신 환경에서 전화 흐름과 MWI 알림은 다음과 같습니다.

1.  수신 전화를 레거시 PBX가 수신한 후에는 VoIP 게이트웨이, IP PBX 또는 SIP 사용 가능 PBX로 전달된 후 UM 사용 가능 사용자의 내선 번호로 전달됩니다. 사용자가 전화를 받지 않으면 발신자에게 음성 메시지를 남기라는 메시지가 전달됩니다.

2.  VoIP 게이트웨이나 IP PBX가 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버로 전화를 전달합니다.

3.  사서함 서버는 사용자의 내선 번호 및 개인 인사말과 같이 UM 사용 가능 사용자 정보를 찾기 위한 LDAP 쿼리를 수행합니다. UM 사용 가능 사용자를 위한 인사말이 재생됩니다.

4.  통합 메시징 서비스에서 만들어진 음성 메시지는 동일한 사서함 서버의 Microsoft Exchange 전송 서비스로 전달됩니다.

5.  사서함 서버의 전송 서비스는 음성 메시지를 사용자 사서함이 있는 사서함 서버에 전달합니다. 사서함 도우미는 새 음성 메시지에 대한 MAPI 이벤트를 수신합니다.

6.  사서함 도우미는 UM 다이얼 플랜 및 UM 사서함 정책을 읽고 MWI 알림을 UM 사용 가능 사용자에게 전송할지 여부를 결정합니다. 사서함 도우미는 UM 사용 가능 사용자의 UM 다이얼 플랜과 연결된 모든 사서함 서버를 쿼리합니다. 사서함 도우미는 첫 번째로 반환된 사서함 서버에 RPC 이벤트를 전송하려고 시도합니다. 전송이 실패하면 다시 한 번 시도합니다. 5분 동안 또는 모든 사서함 서버에 대해 계속 다시 시도합니다. 모든 RPC 호출이 실패하면 사서함 도우미는 이벤트 뷰어에 오류를 기록합니다. 사서함 서버는 UM 사용 가능 사용자 사서함의 UM 다이얼 플랜과 연결된 모든 UM IP 게이트웨이를 쿼리합니다.

7.  UM은 쿼리에서 반환된 첫 번째 VoIP 게이트웨이나 IP PBX로 SIP NOTIFY 메시지를 전송합니다. 전송이 실패하면 사서함 서버는 다음 VoIP 게이트웨이나 IP PBX를 선택합니다. 사서함 서버는 5분 동안 VoIP 게이트웨이나 IP PBX 찾기를 계속 시도합니다. VoIP 게이트웨이나 IP PBX를 찾는 시도가 모두 실패하면 사서함 서버는 오류를 기록합니다. VoIP 게이트웨이나 IP PBX를 찾은 경우 VoIP 게이트웨이가 PBX에 알림을 전송하며, 그런 다음 PBX는 사용자 전화기에 MWI 이벤트 알림을 전송하여 전화기 램프를 켭니다. IP PBX가 사용된 경우 MWI 알림이 IP PBX에서 처리된 후 IP PBX가 사용자 전화기의 램프를 켭니다. 그 이외의 MWI 알림 메커니즘은 개요 섹션에 나와 있습니다. 알림 유형은 PBX 또는 IP PBX 하드웨어 공급업체에 따라 그리고 Lync Server 사용 여부에 따라 결정되며, 사용 중인 전화기 유형(아날로그, 디지털 또는 VoIP)에 따라 결정되기도 합니다.

맨 위로 이동

## Lync Server 환경의 MWI

Lync Server를 포함한 전화 통신 환경에서는 수신 전화를 외부 전화기에서 중재 서버로 전송하거나 Lync 클라이언트, UC(통합 통신) 또는 그 이외의 VoIP 기반 전화기에서 전송할 수 있습니다. 전화가 수신된 후에는 Lync Server 프런트 엔드 서버 풀로 전송됩니다. 사서함 서버 및 사서함 도우미는 UM 사용 가능 사용자에 대한 MWI 상태를 확인하고 Lync 클라이언트, 아날로그, 디지털, UC 또는 VoIP 기반 전화기에 이 알림을 전달하는 데 사용됩니다.

Lync Server를 포함한 전화 통신 환경의 전화 흐름 및 MWI 알림은 다음과 같이 이루어집니다.

1.  전화가 다음 중 하나로부터 전송됩니다.
    
      - 조직 외부 전화기에서 중재 서버로
    
      - Lync 기반 클라이언트
    
      - UC 또는 기타 VoIP 기반 전화기

2.  수신 전화는 Lync Server 프런트 엔드 서버 풀에서 수신되어 UM 사용 가능 사용자의 전화기나 SIP 끝점으로 전송됩니다. 사용자가 전화를 받지 않으면 발신자에게 음성 메시지를 남기라는 메시지가 전달됩니다.

3.  Lync Server 프런트 엔드 서버 풀이 전화를 온-프레미스 네트워크의 사용자 사서함이 있는 사서함 서버로 전달합니다.

4.  사서함 서버는 내선 번호 및 인사말과 같이 UM 사용 가능 사용자 정보를 찾기 위한 LDAP 쿼리를 수행합니다. 인사말이 재생되고 발신자에게 음성 메시지를 남기라는 메시지가 전달됩니다.

5.  통합 메시징 서비스에서 만들어진 음성 메시지는 동일한 사이트의 동일한 사서함 서버의 전송 서비스로 전달됩니다.

6.  전송 서비스는 음성 메시지를 사용자 사서함이 있는 사서함 서버에 전달합니다. 사서함 도우미는 새 음성 메시지에 대한 MAPI 이벤트를 수신합니다.

7.  사서함 도우미는 UM 다이얼 플랜 및 UM 사서함 정책을 읽고 MWI 알림을 사용자에게 전송할지 여부를 결정합니다. 사서함 도우미는 사용자의 UM 다이얼 플랜과 연관된 모든 사서함 서버를 쿼리합니다. 사서함 도우미는 첫 번째로 반환된 사서함 서버에 RPC 이벤트를 전송하려고 시도합니다. 시도가 실패하면 사서함 도우미는 다음 전송을 시도합니다. 5분 동안 또는 모든 서버에 대해 계속해서 사서함 서버 찾기를 시도합니다. 모든 RPC 호출이 실패하면 사서함 도우미는 이벤트 뷰어에 오류를 기록합니다. 사서함 서버는 UM 사용 가능 사용자 사서함의 UM 다이얼 플랜과 연결된 모든 UM IP 게이트웨이에 대한 Active Directory를 쿼리합니다.

8.  UM은 쿼리에서 반환된 첫 번째 VoIP 게이트웨이나 IP PBX로 SIP NOTIFY 메시지를 전송합니다. 전송이 실패하면 사서함 서버는 다음 VoIP 게이트웨이나 IP PBX를 선택합니다. 사서함 서버는 5분 동안 VoIP 게이트웨이나 IP PBX 찾기를 계속 시도합니다. VoIP 게이트웨이나 IP PBX에 연결하는 시도가 모두 실패하면 사서함 서버는 오류를 기록합니다. 성공하는 경우 VoIP 게이트웨이나 IP PBX가 Lync Server 프런트 엔드 서버 풀에 알림을 전송하면 MWI 이벤트 알림은 다시 사용자가 사용한 SIP 끝점, 사용자의 전화기나 Lync 클라이언트로 전송됩니다.

맨 위로 이동

## MWI 복구

사서함 서버, 클라이언트 액세스 서버, UM 다이얼 플랜 및 UM IP 게이트웨이를 배포할 때 UM 사용 가능 사용자에 대해 MWI를 사용하는 경우에는 여러 사서함 서버, 클라이언트 액세스 서버와 여러 VoIP 게이트웨이 및 IP PBX를 배포하여 내결함성 및 복구 기능을 만드는 것이 가장 좋습니다. 그렇게 하면 이전 섹션에서 설명한 대로 MWI 알림을 전송하는 여러 방법이 제공되어 MWI 복구 기능도 만들어집니다.

통합 메시징에서 MWI에 대한 내결함성을 사용하도록 설정하려면 다음 중 한 가지 이상을 만들어 구성해야 합니다.

  - MWI 알림을 수신할 UM 사용 가능 사용자와 연결된 UM 다이얼 플랜

  - MWI 알림을 수신할 UM 사용 가능 사용자와 연결된 UM 사서함 정책

  - MWI 알림을 수신할 UM 사용 가능 사용자와 연결된 UM 다이얼 플랜과 연결된 UM IP 게이트웨이

  - Lync Server가 사용된 경우 클라이언트 액세스 서버 및 사서함 서버를 MWI 알림을 수신하는 UM 사용 가능 사용자와 연결된 UM SIP URI 다이얼 플랜에 추가해야 합니다.

## MWI 관리

MWI는 UM 구성 요소인 UM 사서함 정책과 UM IP 게이트웨이의 설정을 구성하여 관리할 수 있습니다. 두 UM 구성 요소 모두에서 Exchange 관리 셸의 **Set-UMMailboxPolicy** cmdlet 또는 **Set-UMIPgateway** cmdlet을 사용하여 MWI 알림를 사용하도록 설정하거나 사용하지 않도록 설정할 수 있습니다. EAC(Exchange 관리 센터)를 사용하여 설정을 구성할 수도 있습니다. 셸에서 **Get-UMMailboxPolicy** cmdlet 및 **Get-UMIPgateway** cmdlet을 사용하거나 EMC에서 설정을 보고 MWI 알림 상태를 확인할 수 있습니다.

## UM 사서함 정책 및 MWI

UM 사서함 정책을 만들어 일련의 공용 UM 정책 설정을 UM 사용 가능 사서함 모음에 적용할 수 있습니다. 예를 들어, UM 사서함 정책을 사용하여 PIN 정책 설정, 전화 걸기 제한 및 MWI 알림 설정을 적용할 수 있습니다. UM 사서함 정책에서 MWI를 사용하도록 설정하거나 사용하지 않도록 설정하면 해당 UM 사서함 정책과 연결된 모든 UM 사용 가능 사용자에 대해 MWI를 사용하거나 사용할 수 없게 됩니다. MWI 설정은 UM 다이얼 플랜과 연결된 사용자 하위 집합에도 적용됩니다. UM 사용 가능 사용자 그룹에 대해 MWI를 사용하도록 설정하거나 사용하지 않도록 설정하는 방법을 포함하여 UM 사서함 정책에 대한 자세한 내용은 [UM 사서함 정책 절차](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policy-procedures)를 참조하십시오.

다음 표에 표시된 대로 EAC를 사용하거나 셸에서 **Set-UMMailboxPolicy** cmdlet을 사용하여 MWI 설정을 구성할 수 있습니다.

### UM 사서함 정책의 Message Waiting Indicator 설정

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>셸 매개 변수</th>
<th>EAC에서 사용할 수 있는 설정인지 여부</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowMessageWaitingIndicator</em></p></td>
<td><p>예</p></td>
<td><p><em>AllowMessageWaitingIndicator</em> 매개 변수는 UM 사서함 정책에 연결된 사용자가 새 음성 메시지가 도착했다는 MWI 알림을 받을 수 있는지 여부를 지정합니다. 기본값은 <code>$true</code>입니다.</p>
<p>이 설정으로 UM IP 게이트웨이가 받은 전화에 대한 단일 UM 사서함 정책과 연결된 사용자에게 MWI 알림을 보낼 수 있습니다. 이 설정을 사용하면 UM IP 게이트웨이가 UM 사용 가능 사용자의 전화나 SIP 끝점에 SIP NOTIFY 메시지를 보내고 받을 수 있습니다.</p>
<p></p></td>
</tr>
</tbody>
</table>


UM 사서함 정책에서 MWI 설정을 관리하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [UM 사서함 정책 관리](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy)

  - [사용자에 대 한 메시지 대기 표시기 (MWI)를 사용 하도록 설정](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/enable-mwi-for-users)

  - [사용자에 대 한 메시지 대기 표시기 (MWI)를 사용 하지 않도록 설정](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/disable-mwi-for-users)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/ko-kr/library/bb124903\(v=exchg.150\))

## UM IP 게이트웨이 및 MWI

UM IP 게이트웨이에서 MWI를 사용하지 않도록 설정하면 UM IP 게이트웨이로 표시되는 VoIP 게이트웨이나 IP PBX에 연결된 모든 사용자가 MWI 알림을 사용할 수 없게 됩니다. 따라서 UM 다이얼 플랜에 연결된 단일 UM IP 게이트웨이에서 MWI를 사용하지 않도록 설정하면 하나 또는 여러 UM 다이얼 플랜이나 UM 사서함 정책과 연관된 모든 UM 사용 가능 사용자가 MWI 알림을 사용할 수 없게 됩니다. UM 사용 가능 사용자 그룹에 대해 MWI를 사용하도록 설정하거나 사용하지 않도록 설정하는 방법을 포함하여 UM 사서함 정책에 대한 자세한 내용은 [UM 사서함 정책 관리](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy)를 참조하십시오.

다음 표에 표시된 대로 EAC를 사용하거나 셸에서 **Set-UMMailboxPolicy** cmdlet을 사용하여 MWI 설정을 구성할 수 있습니다.

### UM IP 게이트웨이의 Message Waiting Indicator 설정

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>셸 매개 변수</th>
<th>EAC에서 사용할 수 있는 설정인지 여부</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>MessageWaitingIndicatorAllowed</em></p></td>
<td><p>예</p></td>
<td><p><em>MessageWaitingIndicatorAllowed</em> 매개 변수는 UM IP 게이트웨이가 UM 다이얼 플랜과 연결된 사용자에게 SIP NOTIFY 메시지를 보낼 수 있도록 할지 여부를 지정합니다. 기본값은 <code>$true</code>입니다.</p>
<p>이 설정을 사용할 수 있도록 설정하면 UM IP 게이트웨이가 수신하는 전화에 대한 음성 메일 알림을 사용자에게 전송할 수 있습니다. 이 설정을 사용하면 UM IP 게이트웨이가 UM 사용 가능 사용자에게 메시지 대기 알림을 전송할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


MWI 설정을 관리하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [UM IP 게이트웨이 관리](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/manage-um-ip-gateway)

  - [UM IP 게이트웨이에 메시지 대기 표시기 (MWI)을 허용 합니다.](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-mwi-on-um-ip-gateway)

  - [UM IP 게이트웨이에서 메시지 대기 표시기 (MWI) 방지](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/prevent-mwi-on-um-ip-gateway)

  - [Set-UMIPGateway](https://technet.microsoft.com/ko-kr/library/aa996577\(v=exchg.150\))

맨 위로 이동

## 음성 메일 메시지 및 부재 중 전화에 대한 문자 메시지(SMS) 알림

앞서 언급했듯이 MWI 알림은 새 음성 메일 메시지가 있음을 나타내는 메커니즘입니다. 앞에서 설명한 메커니즘 외에도 사용자는 SMS(Short Message Service) 메시지라고도 하는 문자 메시지를 통해 음성 메시지 대기가 있음을 사용자에게 알릴 수 있습니다. 이는 기존의 조명이나 기타 메커니즘과는 다른 유형의 새 음성 메시지에 대한 MWI 알림입니다.

발신자가 새 음성 메시지를 남기면 사용자의 휴대폰에 문자 메시지가 전송됩니다. 사용자가 전화를 받지 못하고 발신자가 음성 메시지를 남기지 않은 경우에도 사용자는 이를 알리는 문자 메시지를 수신할 수 있습니다. 부재 중 전화 알림 문자 메시지가 새 음성 메일 알림과 함께 사용자에게 전송될 수 있습니다.


> [!NOTE]
> 사용자에게 전송된 문자 메시지에는 음성 메일 미리 보기가 포함됩니다.



문자 메시지 알림에는 UM IP 게이트웨이나 UM 사서함 정책의 MWI 설정과는 다른 설정이 사용됩니다. UM 사서함 정책 및 UM 사서함에서 새 음성 메일 및 부재 중 전화에 대한 문자 메시지 알림이 구성됩니다. 셸에서 **Set-UMMailboxPolicy** cmdlet 및 **Set-UMMailbox** cmdlet을 사용하여 문자 메시지 알림을 사용하도록 설정하거나 사용하지 않도록 설정할 수 있습니다. **Get-UMMailboxPolicy** cmdlet 및 **Get-UMMailbox** cmdlet을 사용하여 문자 메시지 알림의 상태를 볼 수 있습니다. EAC에서는 문자 메시지 알림을 구성할 수 없습니다.

다음 표에는 사용자가 음성 메일 및 부재 중 전화 알림에 대해 문자 메시지를 수신하기 위해 구성해야 하는, UM 사서함의 매개 변수가 나와 있습니다.

### 사용자 사서함의 문자 메시지 알림 설정

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em>UMSMSNotificationOption</em></p></td>
<td><p>아니요</p></td>
<td><p><em>UMSMSNotificationOption</em> 매개 변수는 UM 사용 가능 사용자가 음성 메일에 대해서만 문자 메시지 알림을 받을지, 음성 메일과 부재 중 전화에 대해 알림을 받을지, 아니면 알림을 받지 않을지를 지정합니다. 이 매개 변수에 허용되는 값은 <code>VoiceMail</code>, <code>VoiceMailAndMissedCalls</code> 및 <code>None</code>입니다. 기본값은 <code>None</code>입니다.</p>
<p></p></td>
</tr>
</tbody>
</table>


사용자 사서함에서 문자 메시지 알림 설정을 관리하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [사용자에 대 한 음성 메일 설정 관리](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-voice-mail-settings)

  - [Set-UMMailbox](https://technet.microsoft.com/ko-kr/library/bb124893\(v=exchg.150\))

다음 표에는 사용자가 음성 메일 및 부재 중 전화 알림에 대해 문자 메시지를 수신하기 위해 구성해야 하는, UM 사서함 정책의 매개 변수가 나와 있습니다.

### UM 사서함 정책의 문자 메시지 및 부재 중 전화 알림 설정

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>셸 매개 변수</th>
<th>EAC에서 사용할 수 있는 설정인지 여부</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowSMSNotification</em></p></td>
<td><p>아니요</p></td>
<td><p><em>AllowSMSNotification</em> 매개 변수는 사서함이 UM 사서함 정책에 연결된 UM 사용 가능 사용자가 자신의 휴대폰으로 문자 메시지 알림을 받을 수 있는지 여부를 지정합니다. 이 매개 변수를 <code>$true</code>로 설정한 경우에는 <strong>Set-UMMailbox</strong> cmdlet을 사용하고 UM 사용 가능 사용자의 <em>UMSMSNotificationOption</em> 매개 변수를 <code>voicemail</code> 또는 <code>VoiceMailAndMissedCalls</code>로 설정해야 합니다. 기본값은 <code>$true</code>입니다.</p>
<p></p></td>
</tr>
</tbody>
</table>


문자 메시지 알림 설정을 관리하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [UM 사서함 정책 관리](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/ko-kr/library/bb124903\(v=exchg.150\))

음성 메일 및 부재 중 전화에 대해 문자 메시지 알림이 제대로 작동하도록 하려면 다음 작업을 수행해야 합니다.

1.  EAC 또는 셸을 사용하여 사용자가 UM을 사용하도록 설정하고 사용자를 올바른 UM 사서함 정책에 연결합니다.

2.  사용자에 연결된 UM 사서함 정책에서 *AllowSMSNotification* 매개 변수가 `$true`로 설정되었는지 확인합니다. 매개 변수를 `$true`로 설정하려면 다음 명령을 실행합니다. `Set-UMMailboxPolicy -id MyUMMailboxPolicy - AllowSMSNotification $true`.

3.  사용자 사서함에서 *UMSMSNotificationOption* 매개 변수를 `VoiceMailAndMissedCalls` 또는 `VoiceMail`로 설정하여 문자 메시지 알림을 사용하도록 설정합니다.

4.  기본 설정이 `None`이므로 셸에서 다음 명령을 실행하고 문자 메시지 알림 옵션을 `VoiceMailAndMissedCalls` 또는 `VoiceMail`로 설정해야 합니다. 예를 들면 다음과 같습니다. `Set-UMMailbox- -id MyUMMailbox -UMSMSNotificationOption VoiceMailAndMissedCalls`.
    

    > [!IMPORTANT]
    > SMS 알림이 작동하려면 UM 사서함 정책의 <EM>AllowSMSNotification</EM> 매개 변수 및 사용자 사서함의 <EM>UMSMSNotificationOption</EM> 매개 변수가 모두 <CODE>$true</CODE>로 설정되어야 합니다.



사용자는 새 음성 메일 및 부재 중 전화에 대해 문자 메시지 알림을 사용하도록 UM 사서함 정책 및 사용자 사서함을 구성하는 것 외에도 Outlook Web App에 로그인할 때 문자 메시지 알림을 사용하도록 설정하고 구성해야 합니다. 문자 메시지 알림을 설정 및 구성하려면 사용자는 다음을 수행해야 합니다.

1.  Outlook Web App에 로그인하고 **옵션** \> **전화** \> **음성 메일**로 이동합니다.

2.  **음성 메일** 페이지의 **알림**에서 **알림 설정**을 클릭합니다.

3.  **문자 메시지** 페이지에서 **알림 사용** 단추를 클릭합니다.
    
    > [!CAUTION]
    > <strong>음성 메일 알림</strong>을 클릭하지 마십시오. 클릭하면 <strong>음성 메일</strong> 페이지로 이동됩니다.


4.  **문자 메시지** 페이지의 **로캘**에 있는 드롭다운 목록에서 문자 메시지 통신사의 위치나 로캘을 선택합니다.

5.  **문자 메시지** 페이지의 **통신사**에 있는 드롭다운 목록에서 문자 메시지 통신사를 선택하고 **다음**을 클릭합니다.

6.  **문자 메시지** 페이지의 **전화 번호를 입력하고 \[다음\]을 클릭하십시오.** 상자에서 문자 메시지 알림에 사용되는 휴대폰 번호를 입력하고 **다음**을 클릭합니다. 6자리 암호가 휴대폰으로 전송됩니다. 암호를 수신하지 못한 경우 **암호를 받지 못했으므로 다시 보내야 합니다.**를 클릭합니다.

7.  **암호** 상자에 암호를 입력하고 **마침**을 클릭합니다.

8.  문자 메시지 알림을 사용할 수 있게 되면 사용자는 **문자 메시지** 페이지에서 **음성 메일 알림 설정**을 클릭할 수 있습니다. 그러면 음성 메일 페이지로 이동되며, 이 페이지에서 **알림** 섹션까지 아래로 스크롤하여 부재 중 전화 및 음성 메일에 대한 문자 메시지 알림 옵션을 설정할 수 있습니다.

맨 위로 이동

