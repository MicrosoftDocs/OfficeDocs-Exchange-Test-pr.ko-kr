---
title: '오프라인 주소록: Exchange 2013 Help'
TOCTitle: 오프라인 주소록
ms:assetid: a6bcb072-4ab9-400e-a5d0-c05264629097
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232155(v=EXCHG.150)
ms:contentKeyID: 50483890
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 오프라인 주소록

 

_**적용 대상:** Exchange Server 2010, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-11-16_

OAB(오프라인 주소록)는 다운로드된 주소 목록 모음의 복사본이므로 Microsoft Outlook 사용자는 서버에서 연결이 끊긴 동안에도 주소록에 액세스할 수 있습니다. Microsoft Exchange에서는 새 OAB 파일을 생성한 다음 압축하여 로컬 공유에 저장합니다. 오프라인으로 작업하는 사용자가 사용할 수 있는 주소 목록을 결정할 수 있으며 주소록 배포 방법을 구성할 수도 있습니다.

주소 목록에 대한 자세한 내용은 [주소 목록](address-lists-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> OAB 데이터는 사서함 도우미인 Microsoft Exchange OABGen 서비스에서 생성합니다. 보안 설명자를 사용하여 사용자가 Active Directory의 특정 받는 사람을 볼 수 없게 된 경우에도 OAB를 다운로드한 사용자는 그러한 숨겨진 받는 사람을 볼 수 있습니다. 따라서 받는 사람을 주소 목록에서 숨기려면 <A href="https://technet.microsoft.com/ko-kr/library/aa998596(v=exchg.150)">Set-PublicFolder</A>, <A href="https://technet.microsoft.com/ko-kr/library/aa995950(v=exchg.150)">Set-MailContact</A>, <A href="https://technet.microsoft.com/ko-kr/library/aa995971(v=exchg.150)">Set-MailUser</A>, <A href="https://technet.microsoft.com/ko-kr/library/bb123796(v=exchg.150)">Set-DynamicDistributionGroup</A>, <A href="https://technet.microsoft.com/ko-kr/library/bb123981(v=exchg.150)">Set-Mailbox</A> 및 <A href="https://technet.microsoft.com/ko-kr/library/bb124955(v=exchg.150)">Set-DistributionGroup</A> cmdlet에서 <EM>HiddenFromAddressListsEnabled</EM> 매개 변수를 설정해야 합니다. 또는 숨겨진 받는 사람이 들어 있지 않은 새로운 기본 OAB를 만들 수도 있습니다. OAB에서 주소 목록을 추가 또는 제거하는 방법에 대한 자세한 내용은 <A href="add-an-address-list-to-or-remove-an-address-list-from-an-offline-address-book-exchange-2013-help.md">주소 목록에 추가 하거나 오프 라인 주소록에서 주소 목록을 제거합니다</A> 항목을 참조하십시오.



OAB와 관련된 관리 작업에 대한 자세한 내용은 [오프 라인 주소록 절차](offline-address-book-procedures-exchange-2013-help.md) 항목을 참조하십시오.

**목차**

Moving OABs between Exchange versions

OAB version 4 and Outlook clients

Web-based distribution

OAB considerations

## Exchange 버전 간에 OAB 이동

Exchange 2007 및 Exchange 2010에서는 **Move-OfflineAddressBook** cmdlet을 사용하여 OAB 생성을 다른 사서함 서버로 이동할 수 있습니다. Exchange 2013에서는 OAB 버전 4만 지원합니다. 이 버전은 Exchange 2010의 기본 버전과 같습니다. 다른 OAB 버전을 생성하도록 Exchange 2013을 구성할 수 없으며 OAB 생성은 조직 사서함이 상주하는 사서함 서버에서 수행됩니다. 따라서 Exchange 2013에서 OAB 생성을 이동하려면 조직 사서함을 이동해야 합니다. OAB 생성은 다른 Exchange 2013 사서함 데이터베이스로만 이동할 수 있습니다. OAB 생성을 이전 버전의 Exchange로 이동할 수는 없습니다. Exchange 2013 OAB 조직 사서함을 찾으려면 다음 셸 명령을 실행합니다.

    Get-Mailbox -Arbitration | where {$_.PersistedCapabilities -like "*oab*"}

그러면 **MoveRequest** cmdlet을 사용하여 사서함을 이동할 수 있습니다.

## OAB 버전 4 및 Outlook 클라이언트

Exchange 2013에서는 OAB 버전 4만 지원합니다. OAB 버전 4는 Exchange 2003 SP2(서비스 팩 2)에서 도입되었으며 Outlook 2007, Outlook 2010 및 Outlook 2013에서 지원됩니다. 이 유니코드 OAB를 사용하면 클라이언트 컴퓨터에서는 전체 OAB 다운로드가 아니라 파일 크기가 더 작은 차등 업데이트를 받을 수 있습니다.

## OAB 버전 4를 사용하는 Outlook 클라이언트

Outlook 2013, Outlook 2010, Outlook 2007 및 OAB 버전 4 사용 클라이언트의 경우 changes.oab 파일의 크기가 전체 OAB 파일 크기의 1/2 이상이면 Outlook에서는 전체 OAB 다운로드를 시작합니다.

## 웹 기반 배포

*웹 기반 배포*는 Outlook 2013, Outlook 2010 또는 오프라인으로 작업하는 Outlook 2007 클라이언트가 OAB에 액세스할 수 있는 배포 방법입니다.

웹 기반 배포를 사용할 경우 다음과 같은 몇 가지 이점이 있습니다.

  - 더 많은 동시 클라이언트 컴퓨터 지원

  - 대역폭 사용 감소

  - OAB 배포 지점을 보다 강력히 제어 웹 기반 배포를 사용할 경우 배포 지점은 클라이언트 컴퓨터에서 OAB를 다운로드할 수 있는 HTTPS 웹 주소입니다.

웹 기반 배포의 장점을 최대한 활용하려면 클라이언트 컴퓨터에서 Outlook 2013, Outlook 2010 또는 Outlook 2007이 실행되고 있어야 합니다.

올바른 작동을 위해 웹 기반 배포는 다음 구성 요소에 의존합니다.

  - **OAB 생성 프로세스** Exchange에서 OAB를 만들고 업데이트하는 프로세스입니다. OAB를 만들고 업데이트하기 위해 조직 사서함이 있는 사서함 서버에서 OABGen 서비스가 실행됩니다. OAB 배포를 지원하려면 이 서버는 Exchange 사서함 서버여야 합니다.

  - **OAB 배포**   클라이언트가 OAB 배포 요청을 시작하면 해당 요청은 클라이언트 액세스 서버를 통해 전달됩니다. 클라이언트 액세스 서버는 OAB 파일을 호스트하는 사서함 서버로 이 요청을 라우팅합니다. OAB 파일은 사서함 서버에서 클라이언트로 직접 배포됩니다.

  - **OAB 가상 디렉터리** OAB 가상 디렉터리는 웹 기반 배포 방법에 사용되는 배포 지점입니다. Exchange가 설치될 때 기본적으로 IIS(인터넷 정보 서비스)의 기본 내부 웹 사이트에 **OAB**라는 새 가상 디렉터리가 만들어집니다. 조직의 방화벽 외부에서 Outlook에 연결하는 클라이언트 쪽 사용자가 있는 경우에는 외부 웹 사이트를 추가할 수 있습니다. 또는 셸에서 **New-OABVirtualDirectory** cmdlet을 실행하는 경우 로컬 Exchange 클라이언트 액세스 서버의 기본 IIS 웹 사이트에 새 가상 디렉터리 OAB가 만들어집니다. 자세한 내용은 [오프 라인 주소록 가상 디렉터리 만들기](create-an-offline-address-book-virtual-directory-exchange-2013-help.md) 항목을 참조하십시오

  - **자동 검색 서비스**   Outlook 2013, Outlook 2010, Outlook 2007 및 일부 모바일 장치에서 사용할 수 있는 기능으로, Exchange에 액세스할 수 있도록 클라이언트를 자동으로 구성합니다. 이 서비스는 클라이언트 액세스 서버에서 실행되며 특정 클라이언트 연결에 대한 올바른 OAB URL을 반환합니다.

## OAB 고려 사항

하나의 OAB를 사용하든 아니면 여러 OAB를 사용하든 OAB 전략을 계획하고 구현할 때 다음과 같은 요소를 고려하는 것이 좋습니다.

  - 조직의 각 OAB 크기. 자세한 내용은 이 항목 뒷부분의 OAB size considerations를 참조하십시오.

  - OAB 다운로드 수

  - 상위 고유 이름 변경 내용의 수와 빈도

  - SMTP 주소 불일치

  - 디렉터리에 적용된 전체 변경 수

## OAB 크기 고려 사항

일부 조직에서 OAB란 원격 사용자가 가끔씩 다운로드하는 작은 파일을 말합니다. 이러한 조직에서 OAB를 다운로드하는 것은 일반적으로 큰 문제가 되지 않습니다. 하지만 대용량 디렉터리가 있는 일부 대규모 조직이나 캐시된 Exchange 모드에서 Outlook 2003을 배포한 조직의 경우에는 문제가 될 수 있으며 특히, Exchange 서버를 지역별 데이터 센터에 통합한 조직의 경우에는 더욱 그렇습니다.

OAB 크기는 몇 MB부터 수백 MB까지 다양할 수 있는데, 다음은 OAB 크기에 영향을 주는 요소입니다.

  - 회사에서 인증서 사용. PKI(공개 키 구조) 인증서를 많이 사용할수록 OAB 크기가 커집니다. PKI 인증서 범위는 1KB부터 3KB까지로, OAB 크기에 가장 큰 영향을 주는 요소입니다.

  - Active Directory의 메일 받는 사람 수

  - Active Directory의 메일 그룹 수

  - 사서함 사용이 가능하거나 메일 사용이 가능한 각 개체와 관련하여 회사에서 Active Directory에 추가하는 정보. 예를 들어, 각 사용자에 대해 주소 속성을 채우는 조직도 있지만 그렇지 않은 조직도 있습니다.

