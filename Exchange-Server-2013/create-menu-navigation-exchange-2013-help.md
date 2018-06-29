---
title: '메뉴 탐색 만들기: Exchange 2013 Help'
TOCTitle: 메뉴 탐색 만들기
ms:assetid: 3cfc9a01-0a61-4d15-9561-621568dc30d9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997471(v=EXCHG.150)
ms:contentKeyID: 50482917
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantKeyMappingControl
ms.translationtype: MT
---

# 메뉴 탐색 만들기

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-11-05_

자동 전화 교환에 대 한 업무 시간 외 주 메뉴 음성 안내 하거나 비즈니스에 대 한 단일 만들려는 **새 메뉴 탐색 항목** 페이지 또는 여러 키 매핑을 사용할 수 있습니다. 전화기 키패드의 키를 누를 때, 예는 내선 번호 또는 다른 자동 전화 교환에 대 한 호출을 전송 수행 될 작업을 정의할 수 있습니다.

UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 UM 자동 전화 교환 탐색 메뉴를 구성 하려면

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지에서 **UM 자동 전화 교환** 메뉴 탐색 만들려는 UM 자동 전화 교환을 선택 합니다. 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")를 클릭 합니다.

3.  **UM 자동 전화 교환** 페이지에서 **메뉴 탐색** 을 클릭, **업무 시간 외 메뉴 탐색을 사용 하도록 설정** 또는 **업무 시간 외 메뉴 탐색 사용** 을 선택 하 고![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**추가** 클릭 합니다.

4.  **새 메뉴 탐색 항목** 페이지에서 다음을 구성 합니다.
    
      - **음성 안내**   이 입력란에 새로운 탐색 메뉴의 이름을 입력합니다. 탐색 메뉴 이름은 표시를 위해서만 사용됩니다. 이 항목은 필수 필드입니다.
        
        여러 개의 새로운 탐색 메뉴를 지정하고자 하기 때문에 키 매핑에 대해 의미 있는 이름을 사용하는 것이 좋습니다. 키 매핑 이름의 최대 길이는 64자이며 공백이 포함될 수 있습니다. 그러나 다음 문자는 사용할 수 없습니다. " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **이 키를 누르는 경우**   이 목록을 사용하여 키 매핑을 사용하도록 설정합니다. 키 매핑은 호출자를 다른 자동 전화 교환이나 교환원에게 전달하는 작업과 같은 특정 작업을 자동 전화 교환에서 수행하도록 하기 위해 호출자가 누르는 숫자 키입니다. 기본적으로는 항목이 정의되지 않습니다.
        
        드롭다운 목록을 사용 하 여 발신자가 눌러야 하는 1-9 까지의 숫자 키를 선택 합니다. 자동 전화 교환 연산자 영 (0)으로 예약 됩니다.
        
        드롭다운 목록에서 **시간 제한**을 선택하면, 호출자가 전화 키패드의 키를 누르지 않는 경우 내선 번호나 다른 자동 전화 교환으로 연결됩니다. 예를 들어, "전화를 끊지 마십시오. 다음의 가능한 담당자가 귀하의 호출에 응답합니다."입니다. 기본 설정은 5초입니다. 이 옵션을 사용하면 비어있는 키 매핑이 만들어집니다.
    
      - **다음과 같은 오디오 파일 재생**    이 옵션을 사용 하 여 발신자에 대 한 이전에 기록 된 오디오 파일을 선택 합니다. **변경** 을 클릭 한 다음 오디오 파일을 찾으려면 **찾아보기** 를 클릭 합니다.
    
      - **이 추가 작업 수행**   자동 전화 교환 기능이 호출자를 위해 수행하도록 하려는 추가 작업을 정의하려면 다음 옵션 중 하나를 선택합니다.
        
          - **없음**    확장에 또는 다른 자동 전화 교환으로 통화를 전송 하거나 사용자에 대 한 메시지를 남길 자동 전화 교환으로 않으려면이 옵션을 사용 합니다.
        
          - **다음 내선 번호로 연결**   통화를 내선 번호로 연결하려면 이 옵션을 선택합니다. 이 옵션을 사용하는 경우, 입력란에 통화를 연결할 내선 번호를 입력합니다. 이 필드에는 숫자만 입력할 수 있습니다. 다음 문자는 사용할 수 없습니다. " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **다음 UM 자동 전화 교환으로 연결**   통화를 자동 전화 교환으로 연결하려면 이 옵션을 선택합니다. 사용하고자 하는 자동 전화 교환을 찾으려면 **찾아보기**를 클릭합니다. 이 옵션을 사용하기 전에 먼저 자동 전화 교환을 만들고 구성해야 합니다. 이 옵션은 UM 자동 전화 교환의 상위/하위 구조를 만드는 경우에 사용됩니다.
        
          - **이 사용자에게 음성 메시지 남기기**   구성 중인 UM 자동 전화 교환과 동일한 다이얼 플랜의 사용자에게 발신자가 음성 메일 메시지를 남기도록 하려면 이 옵션을 선택합니다. 발신자가 자동 전화 교환 메뉴에서 이 옵션을 선택하면, 선택한 사용자에게 음성 메시지를 남기라는 안내가 나옵니다. UM 사용이 가능한 사용자를 찾으려면 **찾아보기**를 클릭합니다.
        
          - **회사 위치 알림**   호출자가 자동 전화 교환 메뉴 옵션을 선택하고 UM 자동 전화 교환 기능에 구성된 회사의 위치를 들을 수 있도록 하려면 이 옵션을 클릭합니다. 이 기능이 올바르게 작동하도록 하려면 먼저 UM 자동 전화 교환의 **일반** 페이지에 있는 **회사 위치** 입력란에 회사 위치를 입력해야 합니다.
        
          - **업무 시간 알림**   호출자가 자동 전화 교환 메뉴 옵션을 선택하고 UM 자동 전화 교환 기능에 구성된 회사의 업무 시간을 들을 수 있도록 하려면 이 옵션을 클릭합니다. 이 기능이 올바르게 작동하도록 하려면 먼저 UM 자동 전화 교환의 **업무 시간** 페이지에서 업무 시간을 구성해야 합니다.

5.  **확인**을 클릭하여 새 메뉴 탐색을 만듭니다.

6.  **UM 자동 전화 교환** 페이지에서 **저장**을 클릭하여 변경 사항을 저장합니다.

## 셸을 사용 하 여 UM 자동 전화 교환 키 매핑을 구성 하려면

이 예제에서는 업무 시간 키 매핑 되도록 합니다.

  - 호출자에 게 1 누르면 `SalesAutoAttendant`라는 된 다른 UM 자동 전화 교환으로 전달 됩니다.

  - 2를 누를 때 전달 됩니다 내선 번호 12345 지원 합니다.

  - 3을 누를 때 오디오 파일을 재생 하는 다른 자동 전화 교환으로 전송 됩니다.

<!-- end list -->

    Set-UMAutoAttendant -id MyAutoAttendant -BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

쉼표로 구분 된 값 (.csv) 파일에 정의 된 키 매핑을 설정 하는이 예제입니다. 먼저.csv 파일은 다음과 같은 제목과 올바른 항목으로 만들어야: \< 키로 이동한 다음 \> \< 설명 \> \[\< 확장 \>\] \[\< 자동 전화 교환 이름 \>\] \[\< promptfilenamepath \>\] \[\< asrphrase1; asrphrase2 \>\], \[\< leavevoicemailfor \>\] \[\< transfertomailbox \>\]. 대괄호의 값은 선택 사항입니다. .Csv 파일을 만든 후 **Import-csv** cmdlet을 사용 하 여.csv 파일을 가져옵니다.

    $o = Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    Set-UMAutoAttendant MyAutoAttendant -BusinessHoursKeyMapping $o

이 예에서는 키 매핑 기존 UM 자동 전화 교환에서.csv 파일로 내보내고 다른 UM 자동 전화 교환에 동일한 키 매핑을 가져옵니다. 있습니다 수 키 매핑을.csv 파일로 내보낼 수도, 또는.csv 파일에서 키 매핑을 수정 합니다. 편집한 다음 다른 UM 자동 전화 교환에 이러한 키 매핑을 가져옵니다.

    $aa = Get-UMAutoAttendant -id MyAutoAttendant
    $aa1 = Get-UMAutoAttendant -id MyAutoAttendant2
    $aa.BusinessHoursKeyMapping | Export-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    $aa1.BusinessHoursKeyMapping = (Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv")

