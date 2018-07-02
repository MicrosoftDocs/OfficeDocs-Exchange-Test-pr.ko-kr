---
title: '사서함에 대 한 단일 항목 복구를 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 사서함에 대 한 단일 항목 복구를 사용 하지 않도록 설정 하거나 사용
ms:assetid: 2e7f1bcd-8395-45ad-86ce-22868bd46af0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633460(v=EXCHG.150)
ms:contentKeyID: 54651783
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 대 한 단일 항목 복구를 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-13_

셸을 사용 하 여 사서함에서 단일 항목 복구를 사용할지 여부를 수 있습니다. Exchange Online 단일 항목 복구는 새 사서함을 만들 때 기본적으로 활성화 됩니다. Exchange 2013 사서함을 만들 때 단일 항목 복구 불가능 합니다. 단일 항목 복구를 사용 하는 경우 메시지를 영구적으로 삭제 (비우기) 사용자가 삭제 된 항목 보존 기간이 만료 될 때까지 사서함의 복구 가능한 항목 폴더에 유지 됩니다. 그러면 관리자가 삭제 된 항목 보존 기간이 만료 되기 전에 사용자가 제거 된 메시지를 복구할 수 있습니다. 또한, 사용자 또는 프로세스에 의해 메시지를 변경 하는 경우 단일 항목 복구를 사용할 때 원본 항목의 복사본 유지도 됩니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "보존 및 법적 보존이" 항목.

  - 단일 항목 복구를 사용할지 여부를 Exchange 관리 센터 (EAC)를 사용할 수 없습니다.

  - Exchange Online 기본적으로 삭제 된 항목 보존 기간을 14 일로 설정 됩니다. 최대 30 일에이 설정을 변경할 수 있습니다. 자세한 내용은 [Exchange Online 사서함에 대 한 변경 얼마나 오래 영구적으로 삭제 된 항목 보관 됩니다.](https://technet.microsoft.com/ko-kr/library/dn163584\(v=exchg.150\)) 을 참조 하십시오.

  - Exchange 2013 사서함 기본적으로 사서함 데이터베이스의 삭제 된 항목 보존 설정을 사용합니다. 사서함 데이터베이스에 대 한 삭제 된 항목 보존 기간을 14 일로 설정 되어 있지만 사서함으로이 설정을 구성 하 여 기본값을 재정의할 수 있습니다. 자세한 내용은 [삭제 된 항목 보존 및 복구 가능한 항목 할당량 구성](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)를 참조 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## 셸을 사용 하 여 단일 항목 복구를 사용 하도록 설정 하려면

4 월 Summers의 사서함에 대 한 단일 항목 복구를 설정 하는이 예제입니다.

    Set-Mailbox -Identity "April Summers" -SingleItemRecoveryEnabled $true

Pilar Pinilla 및 항목을 삭제 하는 일 수는 30 일에 유지 되는 설정의 사서함에 대 한 단일 항목 복구를 설정 하는이 예제입니다.

    Set-Mailbox -Identity "Pilar Pinilla" -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

조직에서 모든 사용자 사서함에 대 한 단일 항목 복구를 설정 하는이 예제입니다.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true

조직 및 항목을 삭제 하는 일 수는 30 일에 유지 되는 설정의 모든 사용자 사서함에 대해 단일 항목 복구를 사용 하는이 예제

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 셸을 사용 하 여 단일 항목 복구를 사용 하지 않도록 설정 하려면

사용자의 사서함에 대 한 단일 항목 복구를 사용 하지 않도록 설정 해야 합니다. 예 전에 **Search-Mailbox –DeleteContent** 을 사용 하 여 사서함에서 콘텐츠를 영구적으로 삭제 수를 단일 항목 복구를 사용 하지 않도록 설정 해야 합니다. 자세한 내용은 [메시지-관리자 도움말에 대 한 검색 및 삭제](search-for-and-delete-messages-admin-help-exchange-2013-help.md)을 참조 하십시오.

이 예에서는 Ayla Kol의 사서함에 대 한 단일 항목 복구를 비활성화합니다.

    Set-Mailbox -Identity "Ayla Kol" -SingleItemRecoveryEnabled $false

## 작동 여부는 어떻게 확인합니까?

사서함에 대 한 단일 항목 복구를 사용 했을 때 하 고 표시 (일)에서 삭제 된 항목을 보존할 기간에 대 한 값을 확인 하려면 다음 명령을 실행 합니다.

    Get-Mailbox <Name> | FL SingleItemRecoveryEnabled,RetainDeletedItemsFor

사서함에 대해 단일 항목 복구가 비활성화 되었는지 확인 하려면이 동일한 명령을 사용할 수 있습니다.

## 추가 정보

  - 단일 항목 복구 하는 방법에 대 한 자세한 내용은, [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)를 참조 하십시오. 삭제 된 항목 보존 기간 하기 전에 사용자가 제거 된 메시지를 복구 하려면 만료 [사용자의 사서함에서 삭제 된 메시지를 복구 합니다.](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md)를 참조 하십시오.

  - 사서함의 원본 위치 유지 또는 소송 보존에 배치 되 면 복구 가능한 항목 폴더에서 메시지 보존 기간이 만료 될 때까지 유지 됩니다. 보존 기간을 제한 하지 않으면 보존이 제거 되거나 보류 기간 변경 될 때까지 항목이 유지 됩니다.

