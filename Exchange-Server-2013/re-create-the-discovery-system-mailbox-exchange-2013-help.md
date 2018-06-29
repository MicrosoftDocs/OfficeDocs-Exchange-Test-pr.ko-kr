---
title: '검색 시스템 사서함을 다시 만들려면: Exchange 2013 Help'
TOCTitle: 검색 시스템 사서함을 다시 만들려면
ms:assetid: 5ae8426b-5661-4ecb-99c4-cdd342107fb1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg588318(v=EXCHG.150)
ms:contentKeyID: 50483191
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 검색 시스템 사서함을 다시 만들려면

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2018-01-17_

원본 위치 eDiscovery 시스템 사서함을 사용 하 여 원본 위치 eDiscovery 검색 메타 데이터를 저장 합니다. 검색 시스템 사서함이 이름이 표시 **SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}** 입니다. 시스템 사서함에서 Exchange 관리 센터 (EAC) 또는 Exchange 주소 목록에 표시 되지않는, 때문에 실수로 삭제 거의 됩니다.

그러나 검색 시스템 사서함을 실수로 삭제 하는 경우 검색 관리자 됩니다 하지 원본 위치 eDiscovery 검색을 수행 하거나 기존 검색을 관리할 수 있습니다. 이 경우 eDiscovery 기능을 활성화 하려면 다시 만들어야 검색 시스템 사서함입니다.

## 알고 있어야 시작 하기 전에

  - 예상 완료 시간: 10분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 셸을 사용 하 여 검색 시스템 사서함을 다시 만들려면

1.  있는 경우 Active Directory SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 사용자 계정을 삭제 합니다. 기본적으로 Exchange Server 2013 설치 Active Directory 의 Users 컨테이너에 사서함을 만듭니다. Active Directory 에서 사용자 계정을 삭제 하는 방법에 대 한 자세한 내용은, [사용자 계정을 삭제](https://go.microsoft.com/fwlink/p/?linkid=215850)을 참조 하십시오.

2.  셸을 사용 하 여 검색 시스템 사서함을 사용 하도록 설정 합니다.
    

    > [!NOTE]
    > EAC를 사용 하 여 검색 시스템 사서함을 사용 하도록 설정 하려면 수는 없습니다.<BR>다음 명령은 Exchange 설치 미디어의 압축을 푼 같은 디렉터리에서 실행 되어야 합니다.

    
    검색 시스템 사서함을 다시 만들려면 다음 명령을 실행 합니다.
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## 작동 여부는 어떻게 확인합니까?

성공적으로 다시를 만들었다고 검색 시스템 사서함을 확인 하려면 시스템 사서함을 검색 하려면 *Arbitration* 스위치와 함께 **Get-Mailbox** cmdlet을 사용 합니다. 시스템 사서함 `SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}` 다시 만든 되었는지 확인 하려면 명령의 결과 보기


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


