---
title: 'Exchange에서 검색 사서함의 크기 줄이기: Exchange 2013 Help'
TOCTitle: Exchange에서 검색 사서함의 크기 줄이기
ms:assetid: fa762d14-f942-4728-8813-887d11441a68
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn750895(v=EXCHG.150)
ms:contentKeyID: 62371329
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange에서 검색 사서함의 크기 줄이기

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-07_

50GB 제한을 초과하는 검색 사서함이 있습니까? 새 검색 사서함을 만들고 큰 검색 사서함의 검색 결과를 새 검색 사서함으로 복사하여 이 문제를 해결할 수 있습니다.

## 이 작업을 수행하려는 이유는 무엇입니까?

Exchange Server 2013 및 Exchange Online 을 원본 위치 eDiscovery 검색 결과 저장 하는데 사용 되는 검색 사서함의 최대 크기를 50GB 됩니다. 현재 크기 제한 하기 전에 개 이상의 50GB로, 50GB 보다 훨씬 더 큰 검색 사서함을 가진를 발생 하는 저장소 할당량을 늘릴 수 있었습니다. 50GB 보다 큰 경우에 검색 사서함이 있는 문제를 세 가지가 있습니다.

  - 지원되지 않습니다.

  - Office 365로 마이그레이션할 수 없습니다.

  - 검색 사서함 Exchange Server 2010 의 경우 Exchange Server 2013 으로 업그레이드할 수 없습니다.

## 프로세스 살펴보기

다음은 50GB 제한을 초과하는 검색 사서함 크기를 줄이기 위해 수행해야 하는 작업에 대한 간단한 설명입니다.

1.  검색 결과를 배포할 추가 검색 사서함 Create

2.  기존 검색 사서함의 검색 결과를 하나 이상의 새 검색 사서함으로 Copy

3.  원본 검색 사서함에서 eDiscovery 검색을 Delete하여 크기 줄이기

여기에 제공된 전략은 원본 검색 사서함의 검색 결과를 날짜 범위에 따른 별도의 eDiscovery 검색으로 그룹화합니다. 이 방법으로 많은 검색 결과를 새 검색 사서함으로 빠르게 복사할 수 있습니다. 다음 그림에는 이 방법이 나와 있습니다.

![검색 사서함의 크기 줄이기](images/Dn750895.4400df18-c7ed-4c62-b304-f9060ffbdba5(EXCHG.150).gif "검색 사서함의 크기 줄이기")

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 시간은 다른 검색 사서함으로 복사되는 검색 결과의 양과 크기에 따라 달라집니다.

  - 다음 명령을 실행하여 조직의 검색 사서함 크기를 확인합니다.
    
        Get-Mailbox -RecipientTypeDetails DiscoveryMailbox | Get-MailboxStatistics | FL DisplayName,TotalItemSize

  - 50GB 제한을 초과하는 검색 사서함의 검색 결과 일부 또는 전체를 보관할지를 결정합니다. 이 항목의 단계에 따라 검색 결과를 다른 검색 사서함으로 복사하여 보존합니다. 특정 eDiscovery 검색 결과를 보존할 필요가 없는 경우 3단계에 설명된 대로 검색을 삭제할 수 있습니다. 검색을 삭제하면 검색 사서함에서 검색 결과가 삭제됩니다.

  - 50GB 제한을 초과하는 검색 사서함의 일부 검색 결과가 필요 없는 경우 삭제해도 됩니다. Exchange 조직이 프로비저닝되었을 때 만들어진 기본 검색 사서함의 경우 다시 만들 수 있습니다 자세한 내용은 [Exchange에서 기본 검색 사서함 삭제 및 다시 만들기](delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md)를 참조하세요.

  - 현재 진행되는 법률 소송의 경우에는 선택한 eDiscovery 검색 결과를 .pst 파일로 내보낼 수 있습니다. 이렇게 하면 특정 검색의 결과가 그대로 보존됩니다. 검색 결과를 포함하는 .pst 파일 외에, 검색 결과에서 반환된 각 메시지의 항목을 포함하는 검색 결과 로그(.csv 파일 형식)도 내보내집니다. 이 파일의 각 항목은 메시지가 위치한 원본 사서함을 식별합니다. 자세한 내용은 [PST 파일로 eDiscovery 검색 결과 내보내기](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)를 참조하세요.
    
    검색 결과를 .pst 파일로 내보낸 후에 새 검색 사서함으로 가져오려면 Outlook을 사용해야 합니다.

## 1단계: 검색 사서함 만들기

첫 번째 단계는 크기 제한을 초과하는 검색 사서함의 검색 결과를 복사할 수 있도록 추가 검색 사서함을 만드는 것입니다. 검색 사서함의 50GB 크기 제한에 따라, 필요한 추가 검색 사서함의 수를 파악하고 만듭니다. 이러한 새 검색 사서함을 여는 데 필요한 사용 권한을 사용자 또는 그룹에 할당해야 합니다.

1.  다음 명령을 실행하여 새 검색 사서함을 만듭니다.
    
        New-Mailbox -Name <discovery mailbox name> -Discovery

2.  검색 사서함을 열고 검색 결과를 보기 위한 권한을 사용자나 그룹에 할당하려면 다음 명령을 실행합니다.
    
        Add-MailboxPermission <discovery mailbox name> -User <name of user or group> -AccessRights FullAccess -InheritanceType all

## 2단계: 검색 결과를 검색 사서함으로 복사

다음 단계는 **New-MailboxSearch** cmdlet을 사용하여 기존 검색 사서함의 검색 결과를 이전 단계에서 만든 새 검색 사서함으로 복사하는 것입니다. 이 절차에서는 *StartDate* 및 *EndDate* 매개 변수를 사용하여 50GB보다 크지 않은 배치로 검색 결과의 범위를 지정합니다. 여기서는 검색 결과 크기를 적절히 조정하기 위해 검색 결과 평가를 통해 진행되는 몇 가지 테스트가 필요할 수 있습니다.

1.  다음 명령을 실행하여 새 eDiscovery 검색을 만듭니다.
    
        New-MailboxSearch -Name "Search results from 2010" -SourceMailboxes "Discovery Search Mailbox" -StartDate "01/01/2010" -EndDate "12/31/2010" -TargetMailbox "Discovery Mailbox Backup 01" -EstimateOnly -StatusMailRecipients admin@contoso.com
    
    이 예에서는 다음 매개 변수가 사용됩니다.
    
      - *Name*   이 매개 변수는 새 eDiscovery 검색의 이름을 지정합니다. 검색 범위는 보낸 날짜 및 받은 날짜에 따라 지정되므로 검색 이름에 날짜 범위를 넣는 것이 도움이 됩니다.
    
      - *SourceMailboxes*   이 매개 변수는 기본 검색 사서함을 지정합니다. 크기 제한을 초과하는 다른 검색 사서함의 이름을 지정할 수도 있습니다.
    
      - *StartDate* 및 *EndDate*   이러한 매개 변수는 검색 결과에 포함할 기본 검색 사서함의 검색 결과에 대한 날짜 범위를 지정합니다.
        

        > [!NOTE]
        > 날짜를 입력할 때는 로컬 컴퓨터의 국가별 옵션 설정이 dd/mm/yyyy와 같은 다른 형식으로 구성된 경우에도 간단한 날짜 형식인 mm/dd/yyyy를 사용합니다. 예를 들어 2014년 3월 1일을 지정할 때는 <STRONG>03/01/2014</STRONG>를 사용합니다.

    
      - *TargetMailbox*   이 매개 변수는 검색 결과를 "Discovery Mailbox Backup 01"이라는 검색 사서함에 복사하도록 지정합니다.
    
      - *EstimateOnly*   이 스위치는 검색이 시작될 때 반환되는 항목 수의 예상값만 제공되도록 지정합니다. 이 스위치를 포함하지 않으면 검색이 시작될 때 대상 사서함으로 메시지가 복사됩니다. 검색 결과의 수를 늘리거나 줄여야 할 경우 이 스위치를 사용하여 날짜 범위를 조정할 수 있습니다.
    
      - *StatusMailRecipients*   이 매개 변수는 상태 메시지가 지정된 받는 사람에게 전송되도록 지정합니다.

2.  검색이 만들어진 후에 셸 또는 EAC(Exchange 관리 센터)를 사용하여 검색을 시작합니다.
    
      - **셸 사용:** 다음 명령을 실행하여 이전 단계에서 만든 검색을 시작합니다. *EstimateOnly* 스위치는 검색이 만들어질 때 포함되므로 검색 결과가 대상 검색 사서함으로 복사되지 않습니다.
        
            Start-MailboxSearch "Search results from 2010"
    
      - **EAC 사용:** **규정 준수 관리** \> **원본 위치 eDiscovery 및 유지**로 이동합니다. 이전 단계에서 만든 검색을 선택하고 **검색**![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘")을 클릭한 다음 **검색 결과 예상**을 클릭합니다.

3.  필요한 경우 날짜 범위를 조정하여 반환되는 검색 결과의 양을 늘리거나 줄입니다. 날짜 범위를 변경하는 경우 검색을 다시 실행하여 새로운 결과 예상값을 가져옵니다. 새 날짜 범위를 반영하도록 검색 이름을 변경하는 것을 고려할 수 있습니다.

4.  검색 테스트가 끝나면 셸 또는 EAC를 사용하여 검색 결과를 대상 검색 사서함으로 복사합니다.
    
      - **셸 사용:** 다음 명령을 실행하여 검색 결과를 복사합니다. 검색 결과를 복사하려면 먼저 *EstimateOnly* 스위치를 제거해야 합니다.
        
            Set-MailboxSearch "Search results from 2010" -EstimateOnly $false
        
            Start-MailboxSearch "Search results from 2010"
    
      - **EAC 사용:** **규정 준수 관리** \> **원본 위치 eDiscovery 및 유지**로 이동합니다. 해당 검색을 선택하고 **검색**![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘")을 클릭한 후 **검색 결과 복사**를 클릭합니다.
    
    자세한 내용은 [EDiscovery 검색 결과 검색 사서함으로 복사](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)를 참조하세요.

5.  추가 날짜 범위에 대한 검색을 새로 만들려면 1~4단계를 반복합니다. 새 검색의 이름이 날짜 범위를 포함하여 결과 범위를 나타냅니다. 50GB 제한을 초과하는 검색 사서함이 없도록 하려면 다른 검색 사서함을 대상 사서함으로 사용합니다.

## 3단계: eDiscovery 검색 삭제

원본 검색 사서함에서 다른 검색 사서함으로 검색 결과를 복사한 후에는 원본 eDiscovery 검색을 삭제할 수 있습니다. eDiscovery 검색을 삭제하면 해당 검색 결과가 저장된 검색 사서함에서 검색 결과가 삭제됩니다.

검색을 삭제하기 전에 다음 명령을 실행하여 조직의 모든 검색에 대한 검색 사서함으로 복사된 검색 결과 크기를 확인할 수 있습니다.

    Get-MailboxSearch | FL Name,TargetMailbox,ResultSizeCopied

셸 또는 EAC를 사용하여 eDiscovery 검색을 삭제할 수 있습니다.

  - **셸 사용:** 다음 명령을 실행합니다.
    
        Remove-MailboxSearch -Identity <name of search>

  - **EAC 사용:** **규정 준수 관리** \> **원본 위치 eDiscovery 및 유지**로 이동합니다. 삭제할 검색을 선택한 다음 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")을 클릭합니다.

## 작동 여부는 어떻게 확인합니까?

eDiscovery 검색을 삭제하여 검색 결과가 저장된 검색 사서함에서 결과를 제거한 후에 다음 명령을 실행하여 선택한 검색 사서함의 크기를 표시합니다.

    Get-Mailbox <name of discovery mailbox> | Get-MailboxStatistics | FL TotalItemSize

