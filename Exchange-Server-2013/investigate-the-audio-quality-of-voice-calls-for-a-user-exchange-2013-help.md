---
title: '사용자에 대 한 음성 통화의 오디오 품질을 확인 합니다.: Exchange 2013 Help'
TOCTitle: 사용자에 대 한 음성 통화의 오디오 품질을 확인 합니다.
ms:assetid: 0c945886-3cfa-423e-9b46-0d6b1584a145
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ659059(v=EXCHG.150)
ms:contentKeyID: 50555938
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자에 대 한 음성 통화의 오디오 품질을 확인 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-21_

사용자가 UM(통합 메시징) 통화의 오디오 품질과 관련된 문제를 보고하는 경우 사용자 호출 로그 보고서를 사용하여 문제의 원인을 파악할 수 있습니다.


> [!NOTE]
> 호출의 오디오 품질은 이 보고서에 포함되지 않은 요인에 의해서도 영향을 받을 수 있습니다. 예를 들어 Exchange 서버에서 메모리나 CPU의 부하가 지나치게 높은 경우 보고서에는 오디오 품질이 우수하다고 표시되는데도 사용자는 통화 품질이 나쁘다고 보고할 수 있습니다.



UM 보고서와 관련된 추가 작업에 대한 자세한 내용은 [UM 보고서 절차](um-reports-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 통화 데이터 및 요약 보고서 cmdlet" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## EAC를 사용하여 UM 사용 가능 사용자에 대한 호출 로그 가져오기

1.  EAC에서 **통합 메시징** \> **기타 옵션**![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘") \> **사용자 호출 로그**로 이동합니다.

2.  **사용자 선택**을 클릭한 다음 데이터를 가져올 사용자를 선택합니다.

3.  보고서 행의 오디오 품질에 대한 자세한 정보를 보려면 해당 행을 선택하고 **오디오 품질 정보**를 클릭합니다. 다음 정보를 확인할 수 있습니다.
    
      - **날짜 및 시간**   선택된 사용자가 Outlook Web App에서 설정한 표준 시간대를 기준으로 한 통화 날짜 및 시간입니다.
    
      - **사용자**   선택된 사용자입니다.
    
      - **UM 다이얼 플랜**   통화에 대한 다이얼 플랜입니다.
    
      - **UM IP 게이트웨이**   통화에 사용된 UM IP 게이트웨이입니다.
    
      - **오디오 코덱**   통화 중에 사용된 오디오 코덱입니다.
    
      - **NMOS**   통화의 NMOS(네트워크 평균 평가점)입니다. NMOS는 통화의 오디오 품질을 1(최저)에서 5(최고) 사이의 숫자로 나타냅니다.
        

        > [!NOTE]
        > 통화에서 가능한 최대 NMOS는 사용하는 오디오 코덱에 따라 달라집니다. NMOS는 10초 미만의 아주 짧은 통화에는 사용할 수 없습니다.

    
      - **NMOS 저하**   사용 중인 오디오 코덱에 대해 가능한 최고 값에서 낮아진 NMOS의 오디오 저하 값입니다. 예를 들어, 통화의 NMOS 저하 값이 1.2이고 통화에 대해 보고된 NMOS가 3.3이면 해당 통화의 최대 NMOS는 4.5(1.2 + 3.3)가 됩니다.
    
      - **지터**   통화에 대한 데이터 패킷 도착의 평균 변화입니다.
    
      - **패킷 손실**   선택한 통화에 대한 평균 데이터 패킷 손실 비율입니다. 패킷 손실은 연결 안정성을 나타냅니다.
    
      - **왕복**   선택한 통화에 대한 오디오의 평균 왕복 점수(밀리초)입니다. 왕복 점수를 통해 연결의 대기 시간을 측정합니다.
    
      - **버스트 손실 기간**   선택한 통화에 대한 손실 버스트 동안의 평균 패킷 손실 기간입니다.

