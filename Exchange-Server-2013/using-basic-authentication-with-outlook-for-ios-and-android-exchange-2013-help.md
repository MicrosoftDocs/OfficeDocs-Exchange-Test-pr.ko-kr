---
title: 'Outlook for iOS and Android: Exchange 2013 Help'
TOCTitle: Outlook for iOS and Android
ms:assetid: 3a66817c-30da-4965-a6db-2955b5365b0f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt465744(v=EXCHG.150)
ms:contentKeyID: 70061464
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook for iOS and Android

 

_**적용 대상:**Exchange Server 2010, Exchange Server 2013_

_**마지막으로 수정된 항목:**2018-04-02_

**요약**:이 문서에서는 아키텍처 및 iOS에 대 한 Outlook과 Exchange 2013의 Android 하는 방법에 대 한 관리자를 위한 보안 정보 온-프레미스 환경입니다.

전자 메일, 일정, 연락처 및 조직에서 사용자가 많은 작업을 할 수 있도록 하는 기타 파일을 함께 불러 모을 iOS와 Android Outlook 응용 프로그램 설계를 통해 모바일 장치에서 합니다. 이 문서에서는 Exchange 관리자가 배포 하 고 Exchange 조직에서 iOS에 대 한 Outlook 및 Android를 유지 관리할 수 있도록 아키텍처의 개요 및 앱의 저장소 설계를 제공 합니다.


> [!NOTE]
> <A href="https://support.office.com/en-us/article/outlook-for-ios-and-android-help-center-cd84214e-a5ac-4e95-9ea3-e07f78d0cde6">IOS와 Android 도움말 센터에 대 한 Outlook</A> 는 특정 장치에서 응용 프로그램을 사용 하 여 및 문제해결 정보에 대 한 도움말을 비롯 한 사용자 수 있습니다.



## iOS 및 Android 아키텍처용 Outlook

IOS와 Android에 대 한 outlook 모바일 장치 및 *Outlook 서비스*라고 백엔드에 안전 하 고 확장 가능한 클라우드 서비스에 설치 된 프런트엔드 응용 프로그램으로 이루어져 있습니다. 고급 기능을 Outlook 환경으로 향상 된 성능과 안정성을 향상 시키는 기능 지원 Outlook 서비스에 대 한 정보를 처리 합니다. 이 아키텍처 처리, 사용자의 장치에서 필요한 리소스를 최소화를 많이 사용에 대 한 Outlook 서비스에 의존 합니다.

사용자에 대 한 Outlook 서버에서 제공 하는 것의 예는 다음과 같습니다.

  - 포커스가 받은 편지함에 대 한 분류 합니다.

  - 한번 클릭 메일 그룹에서 기능을 취소 합니다.

  - 검색 속도 효율성을 향상 시킵니다.

  - 음성 메일로 착신 전환 하 고 첫번째 다운로드 하지 않고 모바일 장치에 큰 파일을 보낼 수 있습니다.

## 데이터 캐싱 (영문)

성능 향상된을 위해 전자 메일, 일정 및 각 사용자의 사서함에서 파일 데이터의 하위 집합은 Outlook 서비스에 캐시 됩니다. 이 서비스는 현재 Microsoft Azure 에서 실행합니다. Office 365를 Outlook 서비스를 이동 하는 하 고 곧 완료 하는 이동을 계획 합니다.

Outlook 서비스의 정보는 미국 또는 유럽, 연결 클라이언트의 IP 주소에 따라 현재 캐시 됩니다. Outlook 서비스 Office 365로 이동 하는 것에 따라 지역이 데이터 센터 전략와 Office 365 보안 센터의 원칙에 정렬 됩니다 했습니다. Office 365에서 고객의 국가 또는 지역 고객의 관리자는 서비스의 초기 설치 하는 동안 입력을 하는 해당 고객의 데이터에 대 한 기본 저장소 위치를 결정 합니다. 자세한 내용은 [Office 365 보안 센터](https://go.microsoft.com/fwlink/p/?linkid=525776)을 참조 하십시오.

## 데이터 캐싱 FAQ

다음은 질문과 대답 iOS에 대 한 Outlook 및 Android에서 데이터를 저장 하는 방법에 대 한 합니다.

## 사용자의 사서함 데이터의 양을에서 캐시 되는 Outlook 서비스?

전자 메일, 일정 및 연락처 데이터의 약 1 달 합니다. 캐싱 프로세스 계정, 다른 요소 (등 기본 받은 편지함 폴더는 사용자가 만든 폴더에 비해), 사서함 내에서 지정된 된 폴더의 상대적 중요도 사서함의 크기는 알고리즘에 의해 결정 됩니다 및 빈도 사용자가 지정된 된 폴더에 액세스 합니다.

Outlook 서비스는 첨부 파일 데이터를 다음과 같이 저장:을 사용자의 요청을 Outlook에서 전자 메일 첨부 파일을 열 때 서비스 Exchange 서버에서 첨부 파일을 검색 하 고 일시적으로 저장 합니다. 이때 첨부 파일은 사용자의 모바일 장치에서 응용 프로그램에 전달 됩니다. 첨부 파일을 가리키도록 하는 한 달에는 서비스가 중단 플러시 정기적으로 보다 오래 된 데이터는 Exchange 서버에서 사용할 수만 있습니다.

## 내 정보 Outlook 서비스에서 제거 하려면 어떻게 해야 합니까?

Outlook 서비스에서 사용자의 정보를 제거 하기 위한 다음과 같은 세가지 옵션이 있습니다.

  - 옵션 1: Office 365 또는 Exchange에 연결할 iOS Outlook 응용 프로그램을 사용 하는 각 사용자에 대 한 원격 지우기 및 Android를 시작 합니다.

  - 옵션 2: Outlook 응용 프로그램을 삭제 하는 모든 사용자를 포함 합니다. 모든 데이터는 약 3-7 일에서 제거 됩니다.

  - 옵션 3: 각 사용자를 Outlook 응용 프로그램에서 해당 계정을 제거할 한 다음 모바일 장치에서 응용 프로그램을 삭제 합니다. 계정의 제거 하려면 다음이 단계를 수행 하는 사용자가 합니다.
    
    1.  Outlook 응용 프로그램 **설정** 에서 **계정 설정** 을 누릅니다.
    
    2.  **계정을 선택** 하십시오 누른 다음, 선택한 계정을 사용 하 여 **계정 제거** 를 누릅니다.
    
    3.  **장치 및 원격 데이터를** 누릅니다.

## 어떻게 일시적으로 캐시 된 사서함 데이터를 보호 하는 Outlook 서비스에 저장 하는 동안

방법을 사용해 데이터를 현재 [Azure 보안 센터](https://azure.microsoft.com/support/trust-center/)에서 보호 하는 방법에 대 한 읽을 수 있습니다. 이전에 설명한 것 처럼 Office 365로 Azure에서 이동 하는 합니다. [Office 365 보안 센터](https://go.microsoft.com/fwlink/p/?linkid=525776)에서 이러한 서비스의 보안을 다룹니다.

