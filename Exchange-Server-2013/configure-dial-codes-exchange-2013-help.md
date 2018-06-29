---
title: '전화걸기 코드를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 전화걸기 코드를 구성 합니다.
ms:assetid: e5b5efee-b734-4f70-8357-11be07b23bd0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124992(v=EXCHG.150)
ms:contentKeyID: 51407761
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전화걸기 코드를 구성 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

전화걸기 코드, 번호 접두사 및 UM을 사용할 수 있는 사용자에 대 한 수신 및 발신 전화를 전화 통합 메시징에 사용 되는 숫자 형식을 구성할 수 있습니다. 대부분의 경우에서 전화걸기 코드, 접두사 및 전화 통신 네트워크에 현재 구성 된 숫자 형식으로 다이얼 플랜을 구성 합니다.

전화걸기 코드 및 번호 접두사는 UM 사용이 가능한 사용자가 거는 발신 통화에 대 한 전화를 걸려면 올바른 번호를 확인 하는데 사용 됩니다. *Outdialing* 는 사용자를 UM 다이얼 플랜에서 나가는 호출을 시작 하는 프로세스를 설명 하기 위해 사용 되는 용어입니다. 특정 국가 또는 지역, 국제 전화 또는 다이얼 플랜 내에 배치 되는 통화 내에서 걸려오는 전화에 대 한 숫자 서식은 사용 됩니다. 국내/지역 및 국제 모두 번호에 대 한 수신 전화 숫자 형식에 맞게 다이얼 플랜을 구성할 수 있습니다. 국내/지역 및 국제 번호 형식을 구성할 때 다이얼 플랜과 연결 된 사용자에 대 한 수신 전화를 제한할 수 있습니다.

외부로 전화 걸기와 관련된 추가 관리 작업에 대한 자세한 내용은 [사용자가 통화 절차를 수행 하도록 허용](allowing-users-to-make-calls-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 구성 하려면 EAC를 사용 하 여 전화 코드, 접두사 및 번호 형식

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  을 관리 하려는 UM 다이얼 플랜을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **UM 다이얼 플랜** 페이지에서 \> **코드 전화** 를 다음 옵션을 구성 합니다.
    
      - **외부 회선 액세스 코드**
    
      - **국가별 액세스 코드**
    
      - **국가 번호 접두사**
    
      - **국가/지역 코드**

5.  **번호 매기기 전화를 걸려면 다이얼 플랜 간의 형식**, 아래에서 다음을 구성 합니다.
    
      - **국가/지역 번호 형식입니다.**
    
      - **국제 번호 형식**
    
      - **동일한 다이얼 플랜 내에서 걸려오는 전화에 대 한 숫자 형식**    숫자 형식을 추가 하려면 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭 합니다.

6.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 구성 하려면 셸을 사용 하 여 전화 코드, 접두사 및 번호 형식

이 예제에서-국가 또는 지역 번호 형식, 국제 번호 형식으로 다음 전화걸기 코드와 `MyUMDialPlan` 이라는 UM 다이얼 플랜을 구성 합니다.

  - 외부 회선 액세스 코드에 대 한 9

  - 국가별 액세스 코드에 대 한 011

  - 국가 번호 접두사에 대 한 1

  - 국가 또는 지역 코드에 대 한 1

<!-- end list -->

    Set-UMDialPlan -Identity MyUMDialPlan -OutsideLineAccessCode 9 -InternationalAccessCode 011 -NationalNumberPrefix 1 CountryorRegionCode 1 -InCountryOrRegionNumberFormat 1425xxxxxxx -InternationalNumberFormat 441425xxxxxxx

