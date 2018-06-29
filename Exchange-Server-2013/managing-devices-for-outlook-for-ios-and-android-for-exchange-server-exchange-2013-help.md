---
title: 'IOS에 대 한 Outlook 및 Exchange 서버에 대 한 Android 장치 관리: Exchange 2013 Help'
TOCTitle: IOS에 대 한 Outlook 및 Exchange 서버에 대 한 Android 장치 관리
ms:assetid: 16ce7d24-be74-4466-b126-828a67f69b6e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt465748(v=EXCHG.150)
ms:contentKeyID: 70076235
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IOS에 대 한 Outlook 및 Exchange 서버에 대 한 Android 장치 관리

 

_**적용 대상:**Exchange Server 2010, Exchange Server 2013_

_**마지막으로 수정된 항목:**2018-04-01_

**요약**:이 문서에서 설명 하는 방법 Exchange Active Sync를 사용 하면 outlook iOS에 대 한 모바일 장치를 관리 하 고 Exchange에서 Android 온-프레미스 조직입니다.

Exchange ActiveSync 온-프레미스 환경에서 Exchange 사서함에 액세스 하는데 사용 되는 모바일 장치를 관리 하기 위한 권장 됩니다. Exchange ActiveSync는 휴대폰 Microsoft Exchange를 실행 하는 서버에서 조직의 정보에 액세스할 수 있도록 하는 Microsoft Exchange 동기화 프로토콜.

이 문서는 특정 Exchange ActiveSync 기능 및 Android 및 iOS에 대 한 Outlook을 실행 하는 모바일 장치에 대 한 시나리오에 중점을 둡니다. Microsoft Exchange 동기화 프로토콜에 대 한 자세한 내용은 [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md)에서 제공 됩니다. 또한 [Office 블로그](https://go.microsoft.com/fwlink/p/?linkid=623922) 암호 적용 및 Exchange ActiveSync를 사용 하 여 iOS에 대 한 Outlook 및 Android 실행 장치와 다양 한 이점을 대 한 상세한 정보가 됩니다.

## PIN 잠금 및 장치 암호화

조직의 Exchange ActiveSync 정책 전자 메일을 동기화 하는 사용자의 모바일 장치에 암호를 요구 하는 경우 Outlook 장치 수준에서이 정책을 적용 합니다. IOS 장치 및 Android 장치, Apple 및 Google에서 제공 하는 사용할 수 있는 컨트롤에 따라 다르게 작동 합니다.

IOS 장치에서 Outlook 되는지를 확인 하는 암호 또는 PIN 제대로 설정 합니다. 이벤트는 이벤트에 암호를 설정 하지 않으면 Outlook 사용자가 iOS 설정에서 암호를 만들 수를 표시 합니다. 암호는 설치 될 때까지 사용자 iOS에 대 한 Outlook에 액세스할 수 없습니다.

IOS에 대 한 outlook ios 버전 8.0 이상에 실행합니다. 이러한 장치는 iOS 장치에 Outlook을 로컬로 저장 된 모든 데이터를 암호화 하는 암호를 사용 하도록 설정 하는 Outlook을 사용 하는 기본 제공 암호화와 함께 제공 됩니다. 따라서이 ActiveSync 정책에 의해 수행 해야 하는지 여부는 PIN 사용 하 여 iOS 장치 암호화 됩니다.

Android 장치에서 Outlook 화면 잠금 규칙이 적용 됩니다. 그리고 Google Android 암호 길이 및 복잡성에 대 한 Exchange 정책 준수를 위한 Outlook을 허용 하는 제어 기능을 제공 허용 가능한 수가 화면 잠금해제 전화 사항이 제거 하기 전에 시도 합니다. Android 용 outlook 저장소 암호화 설정 되지 않은 경우, 단계별 연습을 사용 하 여이 프로세스를 통해 사용자를 안내 하는 경우 하는 것을 권장도 됩니다.

iOS 및 이러한 암호 보안 설정을 지원 하지 않는 Android 장치를 Exchange 사서함에 연결할 수 되지 않습니다.

## Exchange ActiveSync와 원격 지우기

Exchange ActiveSync 사용 하면 관리자가 장치를 원격으로 초기화를, 손상 될 경우 등입니다. IOS에 대 한 Outlook 및 Android 원격 지우기는 자체를 하 고 전체 장치 지우기 하지 Outlook 응용 프로그램에서 수행 됩니다.

원격 지우기 명령 관리자가 요청 되 면 후 Outlook 응용 프로그램의 Exchange에 대 한 다음 연결의 초 이내 지우기를 발생 합니다. Outlook 응용 프로그램을 다시 설정 하 고 모든 Outlook 전자 메일, 일정, 연락처 및 파일 데이터를 제거할 뿐만아니라 Outlook 서비스는 장치에서 키를 누릅니다. 지우기는 사용자의 개인 응용 프로그램 및 Outlook 외부에 있는 정보에 영향을 주지 않습니다.

원격 지우기 명령 데이터를 제거 하 고 동기화 관계와 관련 된 Outlook (iPhone, iPad, Android)을 실행 하는 모든 장치에서 삭제 됩니다 iOS에 대 한 Outlook 및 Android Exchange 사용자의 모바일 장치에서 단일 모바일 장치 연결으로 표시, 이후 해당 사용자입니다.


> [!NOTE]
> IOS에 대 한 Outlook 및 Android 뒤에 클라우드 아키텍처,으로 인해 Exchange에 원격 장치 지우기 결과 다시으로 보고 되지 않습니다. 지우기를 성공 하는 경우에 상태 <STRONG>보류 중</STRONG> 으로 표시 됩니다. 이 알려진된 문제 및 솔루션을 개발 하는 합니다.



## 장치 식별자 및 액세스 제어

IOS에 대 한 Outlook 및 Android의 클라우드 기반 아키텍처도 인해 Outlook 연결은으로 표시 되어 각 사용자에 대 한 단일 모바일 장치 식별자 (ID) Exchange 합니다. 즉, 각 사용자에 대 한 모바일 장치 액세스 제어 장치 ID와 연결 된 모든 장치에 적용 됩니다. 이 구현을 컨트롤의 작동 방식을 기존의 Exchange ActiveSync 장치 액세스에서로 다른 두 조건을 만듭니다.

  - **차단:** 차단 규칙을 모든 장치에서 Outlook을 차단 하 고 지원 되는 운영 체제입니다. 개별 장치 또는 운영 체제를 차단할 수 없습니다.

  - **격리:** 장치별으로 아닌 사용자 단위로에서 격리 프로세스의 작동 합니다. 사용자가 격리에서 릴리스 장치를 설치 하 고 세대인 만큼의 추가 장치에서 Outlook을 구성할 수 있습니다. 사용자 격리에서 해제 되었습니다, 때문에 해당 사용자와 관련 된 모든 새 장치 격리 되지 않습니다.

모바일 장치 사서함 정책을 배치 하는 경우 모든 관련된 장치에 적용 합니다. 따라서 특정 사서함에 대 한 PIN 잠금을 적용 하는 경우 해당 사서함에 연결 하는 모든 장치 PIN이 필요 합니다.


> [!NOTE]
> 장치 Id는 영향을 받지 않는 모든 <EM>실제 장치</EM> ID, 때문에 예 고 없이 변경할 수 있습니다. 이 경우에 기존 '허용 된' 장치를 예기치 않게 차단 하 or Exchange에서 격리 된 수로 사용자 장치를 관리 하기 위한 장치 Id 사용 되는 경우 예기치 않은 결과가 발생할 발생할 수 있습니다. 따라서 관리자에는 장치 유형 또는 장치 모델에 따라 장치 허용/차단 되는 모바일 장치 정책을 설정 하는 것이 좋습니다.



## Exchange ActiveSync FAQ와 장치 관리

다음은 질문과 대답 암호, Pin, 및 암호화 정책에 대 한 iOS에 대 한 Outlook 및 Android를 실행 하는 장치에 대 한 합니다.

## IOS에서 네이티브 메일 응용 프로그램 암호 길이 및 복잡성 요구 사항에 대 한 Exchange ActiveSync 정책 강제 적용합니다. Outlook 하지 않는 이유는?

Outlook을 Microsoft에 사용할 수 있는 타사 응용 프로그램 개발자 컨트롤을 활용 합니다. Apple 더 많은 컨트롤을 사용할 수 있도록 개발자도이 기능을 개선 하기 위해 계속 될 예정입니다.

## 이유는 iOS에 대 한 Outlook 및 Android 적용 app 수준이 아닌 장치 수준에서 핀?

IOS와 Android에서 사용할 수 있는 기능을 평가한 후 Microsoft 편리 하 고 보안 모두 측면에서 고객을 위한 최상의 경험을 제공 하는 장치 수준 PIN은 생각 합니다. 응용 프로그램 수준 PIN 의미 사용자 방법은 바람직하지 않을 수 있는 전자 메일에 액세스 하기 위해 두개의 서로 다른 Pin을 입력 합니다. 또한 장치 수준 PIN iOS에서 TouchID 및 Android에 대 한 스마트 잠금을 네이티브 장치 암호화와 같은 기능을 활용 취할 수를 의미 합니다. 원격 지우기는 여전히 사용자의 개인 응용 프로그램을 의미 하는 응용 프로그램 수준에서 구현 하 고 Outlook 지워지도록 때 데이터를 적용 되지 않습니다.

## Android 지원 장치 암호화에 대 한 Outlook는 무엇이 있습니까?

예, Android에 대 한 Outlook Exchange 모바일 장치 사서함 정책을 통해 장치 암호화를 지원합니다. 그러나 Android 7.0 하기 전에 가용성과이 프로세스를 구현 하에 따라 다르게 Android 운영 체제 버전 및 장치 제조업체는 암호화 프로세스 동안을 취소 하려면 사용자를 허용 하는 합니다. Google Android 7.0에 도입 된 변경 내용으로 Android에 대 한 Outlook 이제은 Android 7.0을 실행 하는 장치에서 암호화를 적용할 수 이상 있습니다. 이러한 운영 체제를 실행 하는 장치를 사용 하는 사용자는 암호화 프로세스를 취소 수 없습니다.

Android 장치는 암호화 하 고 장치 PIN을 사용 하도록 설정 하기만 하면 공격자가 장치를 소유 중인, 경우에 Outlook 데이터베이스 액세스할 수 없는 상태로 유지 됩니다. USB 디버깅 사용 하도록 설정 하 고 Android SDK가 설치 되어 있어도 그렇습니다. 공격자가이 정보에 대 한 액세스 권한을 얻으려고 PIN 사용 하지 않으려면 장치 루트에 루 팅 프로세스 모든 장치 저장소를 제거 하 고 모든 Outlook 데이터를 제거 합니다. 암호화 되지 않은 장치는 도난 하기 전에 사용자가 루트가 아닌 경우, 공격자가 USB 장치에서 디버깅을 사용 하 여 Outlook 데이터베이스에 액세스 하는 것이 불가능 하 고 설치 Android SDK를 사용 하 여 컴퓨터에는 장치를 연결 합니다.

