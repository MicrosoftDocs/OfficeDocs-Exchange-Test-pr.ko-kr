---
title: '테스트 및 Test-umconnectivity cmdlet과 함께 문제해결: Exchange 2013 Help'
TOCTitle: 테스트 및 Test-umconnectivity cmdlet과 함께 문제해결
ms:assetid: 08e67a99-e37f-4afd-bd58-455b62580af7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa995978(v=EXCHG.150)
ms:contentKeyID: 56270322
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 테스트 및 Test-umconnectivity cmdlet과 함께 문제해결

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-06-25_

클라이언트 액세스와 사서함 서버를 설치하고 통합 메시징을 구성한 후에는 여러 진단 테스트와 소프트웨어 기반 전화 응용 프로그램을 사용하여 전화 통신 연결 및 통합 메시징 서비스 작업을 테스트할 수 있습니다.

## Test-UMConnectivity

**Test-UMConnectivity** cmdlet을 사용하면 cmdlet과 함께 사용된 매개 변수에 따라 다양한 방법으로 클라이언트 액세스 및 사서함 서버에 대한 연결을 확인할 수 있습니다. 다음 테스트를 사용하여 통합 메시징 기능을 테스트합니다.

  - **로컬**   **Test-UMConnectivity** cmdlet은 동일한 로컬 컴퓨터에서 실행되는 사서함 서버와의 VoIP(Voice over IP) 통신을 확인합니다.

  - **TUILogon을 사용하는 로컬**   **Test-UMConnectivity** cmdlet은 동일한 컴퓨터에서 실행되는 사서함 서버와의 VoIP 통신을 설정하려고 시도합니다. 연결에 성공하면 사서함의 내선 번호와 PIN을 전송하여 UM 사용이 가능하도록 설정된 하나 이상의 사서함에 로그인을 시도합니다. *–TUILogon* 매개 변수가 제공되는 경우 테스트 사서함에 해당하는 정보와 함께 다음 매개 변수 값도 제공되어야 합니다.
    
      - *–Phone*   이 매개 변수는 테스트 사서함의 내선 번호를 포함해야 합니다.
    
      - *–PIN*   이 매개 변수는 UM 사용이 가능한 사서함의 PIN을 포함해야 합니다.
    
      - *–UMDialPlan*   이 매개 변수는 테스트 사서함에 연결된 다이얼 플랜을 포함해야 합니다.

  - **원격**   **Test-UMConnectivity** cmdlet은 VoIP 게이트웨이를 통한 호출을 수행하여 원격 클라이언트 액세스 서버에 연결하려고 시도합니다. 연결되면 원격 클라이언트 액세스 서버 및 미디어 경로에서 연결을 확인합니다.
    

    > [!NOTE]  
    > 다음 메시지가 표시되는 경우 MicrosoftExchange 통합 메시징 서비스가 중지되었거나 응답하지 않는 것이므로 이 서비스를 다시 시작해야 합니다. "Test-UMConnectivity 작업에서 전화를 거는 동안 오류가 발생했습니다. 세부 정보: 연결할 수 없습니다."


