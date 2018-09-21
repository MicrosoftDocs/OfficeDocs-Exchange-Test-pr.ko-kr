---
title: 'Exchange 검색 사용 또는 사용 안 함: Exchange 2013 Help'
TOCTitle: Exchange 검색 사용 또는 사용 안 함
ms:assetid: 195b25be-53fb-4215-90a5-04340d640bcc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996416(v=EXCHG.150)
ms:contentKeyID: 52058056
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 검색 사용 또는 사용 안 함

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-05-07_

기본적으로 Exchange 검색은 모든 새 사서함 데이터베이스에 대해 사용하도록 설정되어 있으며 추가 구성이 필요하지 않습니다. 그러나 Exchange 검색에서 사서함 콘텐츠의 인덱싱을 중지하도록 하려면 개별 사서함 데이터베이스 또는 전체 사서함 서버에 대해 Exchange 검색을 사용하지 않도록 설정할 수 있습니다.


> [!WARNING]
> Exchange 검색을 사용하지 않도록 설정하면 사용자가 온라인 모드 또는 Windows Mobile 장치에서 Outlook을 사용하여 수행하는 전체 텍스트 검색의 기능과 성능에 영향을 미칩니다.<BR><A href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery">원본 위치 eDiscovery</A> 또한 Exchange 검색을 사용합니다. 사서함 데이터베이스 또는 사서함 서버에 대해 Exchange 검색을 사용하지 않도록 설정하는 경우 원본 위치 eDiscovery 검색은 데이터베이스 또는 서버에서 메시지를 반환하지 않습니다.



Exchange 검색과 관련된 추가 관리 작업에 대한 자세한 내용은 [Exchange 검색 절차](exchange-search-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 1분

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 서버 또는 사서함 데이터베이스에 대해 Exchange 검색을 사용하거나 사용하지 않도록 설정할 수는 있지만 개별 사서함 사용자에 대해서는 설정할 수 없습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

## 무슨 작업을 하고 싶으십니까?

## 사서함 데이터베이스에 대해 Exchange 검색을 사용하거나 사용하지 않도록 설정

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "Exchange 검색" 항목


> [!NOTE]
> EAC를 사용하여 사서함 데이터베이스에 대해 Exchange 검색을 사용하거나 사용하지 않도록 설정할 수는 없습니다.



다음 명령은 EXCH01이라는 사서함 데이터베이스에 대해 Exchange 검색을 사용하지 않도록 설정합니다.

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $false

다음 명령은 EXCH01이라는 사서함 데이터베이스에 대해 Exchange 검색을 사용하도록 설정합니다.

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\))를 참조하십시오.

## 사서함 서버에 대해 Exchange 검색을 사용하거나 사용하지 않도록 설정

사서함 서버에 대해 Exchange 검색을 사용하지 않도록 설정하려면 Microsoft Exchange Search Service를 사용하지 않도록 설정하고 중지해야 합니다. 마찬가지로 사서함 서버에 대해 Exchange 검색을 사용하도록 설정하려면 Microsoft Exchange Search Service를 사용하도록 설정하고 시작해야 합니다. 서비스 콘솔 또는 셸을 사용하여 이 작업을 수행할 수 있습니다.

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 서버의 Exchange 검색 서비스 관리" 항목

**서비스 콘솔 사용**

1.  **시작** \> **관리 도구** \> **서비스**로 이동합니다.

2.  **서비스** 세부 정보 창에서 **Microsoft Exchange Search** 서비스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.

3.  **일반** 탭의 **시작 유형** 목록에서 **사용 안 함**을 선택하여 서비스를 사용하지 않도록 설정하거나 **자동**을 선택하여 서비스를 자동으로 시작합니다.
    

    > [!NOTE]
    > 시작 유형은 다음에 서비스를 시작하려고 할 때 즉, 서버가 다시 시작된 후에 자동으로 서비스에 적용되거나 서비스를 수동으로 시작하여 서비스에 적용할 수 있습니다. 다음 단계에서 서비스를 수동으로 중지하거나 시작합니다.



4.  서비스를 중지하려면 **중지**를 클릭하고 서비스를 시작하려면 **시작**을 클릭합니다.

5.  **확인**을 클릭하여 변경 내용을 저장합니다.

**셸 사용**

다음 명령을 실행하여 Microsoft Exchange Search Service를 중지하고 사용하지 않도록 설정합니다.

```
    Stop-Service MSExchangeFastSearch
```

```
    Set-Service MSExchangeFastSearch -StartupType Disabled
```

다음 명령을 실행하고 Exchange Search Service가 자동으로 시작되도록 구성한 후 이 서비스를 시작합니다.

```
    Set-Service MSExchangeFastSearch -StartupType Automatic
```
```
    Start-Service MSExchangeFastSearch
```
