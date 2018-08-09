---
title: 'Exchange Server의 iOS 및 Android용 Outlook에서의 암호 및 보안'
TOCTitle: Passwords and Security in Outlook for iOS and Android for Exchange Server
ms:assetid: e5565beb-7ef3-47c4-8daf-6d8f1d22dceb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt465750(v=EXCHG.150)
ms:contentKeyID: 70076242
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passwords and Security in Outlook for iOS and Android for Exchange Server

 

_**적용 대상:** Exchange Server 2010, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2018-04-01_

**요약**:이 문서에서는 암호와 보안 iOS에 대 한 Outlook 및 Exchange Server와 Android에서 작동 하는 방법에 대해 설명 합니다.

IOS와 Android Outlook 응용 프로그램을 실행 하는 Exchange 온-프레미스 환경에서 처음으로 Outlook 임의의 AES 128 키를 생성 합니다. 이 키는 *장치 키* 이라고 하며 사용자의 장치에만 저장 됩니다.

## 계정 만들기 및 암호 보호

사용자가 Exchange에 로그온 할 때는 사용자 이름, 암호 및 고유 AES 128 장치 키 보내집니다 사용자의 장치에서 Outlook 서비스에 TLS 연결을 통해 장치 키 런타임 compute 메모리에 유지 되는 위치. Exchange 서버를 사용 하 여 암호를 확인 한 후 Outlook 서비스 장치 키를 사용 하 여 암호를 암호화 하 고 암호화 된 암호는 서비스에 저장 됩니다. 장치 키 한편, 메모리에서 데이터 삭제 이며 (키가만 사용자의 장치에 저장 됨) Outlook 서비스에 저장 되지 않습니다.

다음으로, 사용자가 사서함 데이터를 검색 하는 Exchange에 연결 하려고 하는 경우 장치 키가 다시 장치에서 Outlook 서비스로 전달 TLS 보안 연결을 통해이 런타임 compute 메모리에 암호를 해독 하 사용 되는 경우. 암호를 해독 암호 되거나 되지 않습니다 서비스에 저장 된 로컬 저장소 디스크에 기록 되 고 장치 키가 다시 한번 메모리에서 데이터 삭제 합니다.

Outlook 서비스 런타임에 암호 해독 해야 하므로 후 서비스 메일, 일정 및 기타 사서함 데이터를 동기화 하는 Exchange 서버에 다음 연결할 수 있습니다. 사용자를 열고 주기적으로 Outlook을 사용 하 여 계속,으로 Outlook cservice Exchange 서버에 연결 활성화 되어 있도록 유지 하는 메모리에 사용자의 암호가 해독 된 암호의 복사본을 유지 됩니다.

## 비활성 계정 하 고 메모리에서 암호를 플러시하여

비활성 3 일 후 Outlook 서비스 메모리에서 암호가 해독 된 암호를 플러시합니다. 플러시 암호가 해독 된 암호를 함께 Outlook 서비스를 사용자의 사서함에 액세스할 수 없습니다. 암호화 된 암호 Outlook 서비스에 저장 되었지만 다시 암호를 해독만 사용자의 장치에서 사용할 수 있는 장치 키가 없는 수 없습니다.

세 가지 방법으로 사용자 계정이 비활성화 될 수 있습니다.

  - IOS와 Android를 위한 outlook 사용자가 제거 됩니다.

  - 배경 app 새로고침 설정 옵션에서 비활성화 되었습니다 하 고 Outlook에 적용 되는 force 종료 합니다.

  - Exchange와의 동기화에서 Outlook을 방지 장치에서 사용할 수 있는 인터넷 연결이 없습니다.


> [!NOTE]
> Outlook 됩니다 비활성 단순히 사용자 열리지 않는 앱 시간, 기간에 대 한 같은 주말 하기 때문에 또는 휴가 중에 있습니다. 배경 app 새로고침 사용 하는 (즉, iOS에 대 한 Outlook Android에 대 한 기본 설정)으로 활동 푸시 알림 및 전자 메일의 배경 동기화와 같은 함수 계산 됩니다.



**플러시하는 중에는 하드 디스크에서 캐시를 암호 및 메시지 암호화**

Outlook 서비스 플러시 또는 삭제, 비활성 계정 매주 일정으로 합니다. 사용자 계정이 비활성화 되 면 후 암호화 된 암호와의 모든 서비스를 활용할 사용자의 캐시 된 사서함 콘텐츠 Outlook 서비스 플러시 됩니다.

**장치 및 서비스에 해당 하는 보안의 조합**

각 사용자의 고유한 장치 키 Outlook 서비스에 저장 되지 않습니다 하 고 사용자의 Exchange 암호 장치에 저장 되지 않습니다. 이 아키텍처는 사용자의 암호에 대 한 액세스 권한을 얻으려고 악의적인 당사자 순서로 필요한 Outlook 서비스에 무단으로 액세스 하 고 해당 사용자의 장치에 대 한 실제 액세스 모두 것을 의미 합니다.

PIN 정책 및 조직의 장치에에서 대 한 암호화 적용 하 고, 하 여 악의적인 사용자는 또한 물리 장치 키에 대 한 액세스를 가져오기 위해 장치를 암호화 해야 합니다. 모든 했을 사용자 장치 손상 된 및 장치에 대 한 원격 지우기 요청 수를 발견 하기 전에 수행 합니다.

## 암호 보안 FAQ

다음은 질문과 대답 보안 설계 및 iOS에 대 한 Outlook Android에 대 한 설정에 대 한 합니다.

## 사용자 자격 증명에에서 저장 된 Outlook 서비스 내 Exchange 서버에 액세스 하지 못하도록 Outlook을 차단 하는 경우?

IOS에 대 한 Outlook 및 Android 온-프레미스 Exchange 서버에 액세스 하지 못하도록 차단 하도록 선택한 경우 Exchange에서 초기 연결이 거부 됩니다. Outlook 서비스에서 사용자 자격 증명을 저장할 수는 및 메모리에서 실패 한 연결 시도에 제공 된 자격 증명을 강제로 플러시한 즉시 합니다.

## Outlook 서비스에 전송 중에 고유한 장치 키와 사용자 암호를 암호화 하는 방법

암호화 된 TLS 연결을 통해 Outlook app 및 Outlook 서비스 간의 모든 통신은 됩니다. IOS에 대 한 Outlook 및 Android는 Outlook 서비스와 다른 경우 nothing에 연결 수 있습니다.

## 사용자의 자격 증명 및 사서함 정보를 Outlook 서비스에서 제거 하려면 어떻게 해야 합니까?

Outlook 서비스에서 정보를 제거 하는 방법은 다음 세 가지가 있습니다.

  - 옵션 1: Exchange에 연결할 응용 프로그램을 사용 하는 각 사용자에 대 한 원격 지우기 시작 합니다.

  - 옵션 2: iOS에 대 한 Outlook 및 Android를 삭제 하는 모든 사용자를 포함 합니다. 약 3-7 일의 모든 데이터를 Outlook 서비스에서 제거 됩니다.

  - 옵션 3:가 사용자가 자신의 계정을 Outlook 응용 프로그램에서 제거 하 고 해당 장치에서 응용 프로그램을 삭제 합니다. 응용 프로그램에서 명의 사용자 **설정**이동 후 **계정 설정**, 다음 **계정을 선택**하십시오 누른 다음 **계정 삭제**를 누릅니다.

## 앱 닫히거나 제거, 하지만 여전히 표시 내 Exchange 서버에 연결 하는 것입니다. 어떻게는이 무엇입니까?

Outlook 서비스 런타임 compute 메모리에 사용자 암호를 해독 하 고 암호가 해독 된 암호를 사용 하 여 Exchange에 연결 합니다. Outlook 서비스를 가져오고 사서함 데이터를 캐시 하기 위해 장치를 대신 하 여 Exchange에 연결 하는 이후 시간 서비스 Outlook 데이터를 요청 하 고 더이상 감지 될 때까지 잠시 동안 계속 수 없습니다.

사용자를 사용 하면 장치에서 응용 프로그램을 제거 하는 **계정 삭제** 옵션을 사용 하지 않고, 하는 경우 Outlook 서비스 머무르는 Exchange 서버에 연결 된 계정 비활성 및"플러시에서 설명한 것과 같이 계정을 비활성, 가능할 때까지 암호 메모리에서. " 이 작업을 중지 하려면 위의 FAQ에서 1 (옵션) 또는 옵션 3을 팔 로우 하 또는 [IOS에 대 한 Outlook 및 Android 차단](https://technet.microsoft.com/ko-kr/library/mt759239\(v=exchg.150\))의 설명에 따라 앱을 차단 합니다.

## 사용자 암호를 보다 안전 하지 않은 iOS에 대 한 Outlook 및 Android의 경우 다른 Exchange ActiveSync 클라이언트를 사용 하 여은?

아니요. 현재까지 EAS 클라이언트 일반적으로 사용자 자격 증명을 저장 로컬로 사용자의 장치에 있습니다. 즉, 도난 또는 손상 된 장치는 사용자의 암호에 대 한 액세스를 사용할 수 있는 악의적인 파티 될 수 있습니다. 보안 디자인 iOS에 대 한 Outlook 및 Android, 악의적인 사용자의 필요 무단으로 액세스 하는 Outlook 클라우드 서비스 **및** 떨어지기 사용자의 장치에 대 한 실제 액세스 합니다.

## 사용자가 자신의 데이터 Outlook 서비스에서 삭제 된 후 iOS에 대 한 Outlook 및 Android 사용 하려고 하면 어떻게 됩니까?

하는 경우 사용자 계정을 비활성화 됩니다 (예: 장치에 배경 app refresh를 사용 하지 않도록 설정 하거나 필요 하 여 자신의 장치 연결이 끊긴 것으로 인터넷에서 일정 시간 동안에 대 한), Outlook app는 다시 연결 Outlook 서비스에 다음에 app가 시작 되 고, 암호 암호화 및 전자 메일 캐싱 프로세스를 다시 시작 됩니다. 모든 사용자에 게 투명 하 게입니다.

## 어떻게 일시적으로 캐시 된 사서함 데이터를 보호 하는 Outlook 서비스에 저장 하는 동안

방법을 사용해 데이터를 현재 [Azure 보안 센터](https://azure.microsoft.com/support/trust-center/)에서 보호 하는 방법에 대 한 읽을 수 있습니다. 이전에 설명한 것 처럼 Office 365로 Azure에서 이동 하는 합니다. [Office 365 보안 센터](https://go.microsoft.com/fwlink/p/?linkid=525776)에서 이러한 서비스의 보안을 다룹니다.

