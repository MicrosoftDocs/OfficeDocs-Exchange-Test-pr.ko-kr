---
title: 'Outlook Voice Access 사용자가 검색할 수에 대 한 보조 방법 구성: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 사용자가 검색할 수에 대 한 보조 방법 구성
ms:assetid: 5cd4e0a0-d023-45a1-aa3c-b8dea6ec6d72
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998311(v=EXCHG.150)
ms:contentKeyID: 52057923
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 사용자가 검색할 수에 대 한 보조 방법 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

다이얼 플랜을 만드는 경우 발신자가 이름을 검색할 수 있는 기본 및 보조 *이름으로 전화 걸기 방법*을 구성할 수 있습니다. 발신자는 이름으로 전화 걸기 방법을 사용하여 발신자가 Outlook Voice Access 번호로 전화를 걸거나 다이얼 플랜에 연결된 UM 자동 전화 교환으로 전화를 걸 경우 사용자를 찾아서 연락할 이름을 조회합니다. 발신자는 누름 단추식 입력을 사용하여 UM 사용 가능 사용자를 찾을 수 있습니다.


> [!NOTE]
> 발신자가 이름을 검색할 수 있는 보조 방법으로 <STRONG>없음</STRONG>을 선택한 경우 발신자는 이름을 검색하는 기본 방법만 사용하여 사용자를 찾을 수 있습니다. 발신자가 이름을 검색할 수 있는 기본 방법과 보조 방법을 둘 다 구성한 경우 두 방법에 대한 안내가 제공됩니다.



다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 이름으로 전화 걸기 보조 방법 변경

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **설정**의 **이름 검색 보조 방법** 아래에서 드롭다운 목록을 사용하여 원하는 옵션을 선택합니다.
    
      - **성 이름**(기본값)
    
      - **이름 성**
    
      - **SMTP 주소**
    
      - **없음**

5.  **저장**을 클릭합니다.

## 셸을 사용하여 이름으로 전화 걸기 보조 방법 변경

이 예에서는 이름으로 전화 걸기 보조 방법을 `FirstLast`로 설정합니다. 이렇게 하면 Outlook Voice Access 번호 또는 다이얼 플랜과 연관된 UM 자동 전화 교환으로 전화를 건 사람이 UM 사용 가능 사용자를 이름으로 검색한 다음 성으로 검색할 수 있습니다.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary FirstLast

이 예에서는 이름으로 전화 걸기 보조 방법을 `LastFirst`로 설정합니다. 이렇게 하면 Outlook Voice Access 번호 또는 다이얼 플랜과 연관된 UM 자동 전화 교환으로 전화를 건 사람이 UM 사용 가능 사용자를 성으로 검색한 다음 이름으로 검색할 수 있습니다.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary LastFirst 

이 예에서는 이름으로 전화 걸기 보조 방법을 `SMTP address`로 설정합니다. 이렇게 하면 Outlook Voice Access 번호 또는 다이얼 플랜과 연관된 UM 자동 전화 교환으로 전화를 건 사람이 UM 사용 가능 사용자를 SMTP 주소로 검색할 수 있습니다.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary SMTPAddress 

이 예에서는 이름으로 전화 걸기 보조 방법을 `None`으로 설정하고, 이름으로 전화 걸기 기본 방법을 `SMTP address`로 설정합니다. 이렇게 하면 Outlook Voice Access 번호나 다이얼 플랜과 연결된 UM 자동 전화 교환으로 전화를 거는 발신자는 SMTP 주소만으로 UM 사용 가능 사용자를 검색할 수 있습니다.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary SMTPAddress -DialByNameSecondary None

