---
title: '보존 정책 만들기: Exchange 2013 Help'
TOCTitle: 보존 정책 만들기
ms:assetid: d8806c98-fea5-492f-906d-f514e25361b2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150573(v=EXCHG.150)
ms:contentKeyID: 50484262
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보존 정책 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange Online 및 Exchange Server 2013 에서 전자 메일 수명 주기를 관리 하려면 보존 정책을 사용할 수 있습니다. 보존 태그 만들기 (영문), 보존 정책에 추가 하 고 사서함 사용자에 게 정책을 적용 하 여 보존 정책이 적용 됩니다.

보존 정책을 만들고 Exchange Online 의 사서함에 적용 하는 방법을 보여주는 [비디오](https://go.microsoft.com/fwlink/?linkid=825854) 다음과 같습니다.

보존 정책과 관련 된 추가 관리 작업에 대 한 [메시징 레코드 관리 절차](messaging-records-management-procedures-exchange-2013-help.md)를 참조 합니다.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 30분

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 보존 정책을 적용할 사서함 Exchange Server 2010 또는 이상 서버에 있어야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 어떻게 해야 합니까?

## 1 단계: 보존 태그 만들기

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "메시징 레코드 관리" 항목.

**EAC를 사용 하 여 보존 태그를 만들려면**

1.  **규정 준수 관리** 로 이동 \> **보존 태그** 를 다음![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**추가** 클릭 하 고

2.  다음 옵션 중 하나를 선택합니다.
    
      - **전체 사서함 (기본값)에 자동으로 적용 되며**    기본 정책 태그 (DPT)를 만들려면이 옵션을 선택 합니다. DPTs를 사용 하 여 기본 삭제 정책 및 사서함의 모든 항목에 적용 되는 기본 보관 정책을 만들 수 있습니다.
        

        > [!NOTE]
        > EAC를 사용 하 여 음성 메일 항목을 삭제 하려면 DPT를 만들려면 수는 없습니다. 음성 메일 항목을 삭제 하려면 DPT를 만드는 방법에 대 한 자세한 내용은 아래 셸 예제를 참조 하십시오.

    
      - **특정 폴더에 자동으로 적용 되며**    예: **받은 편지함** 또는 **지운 편지함** 기본 폴더에 대 한 보존 정책 태그 (RPT)를 만들려면이 옵션을 선택 합니다.
        

        > [!NOTE]
        > <STRONG>삭제 및 복구 허용</STRONG> 또는 <STRONG>영구 삭제</STRONG> 작업에만 Rpt를 만들 수 있습니다.

    
      - **항목 및 폴더 (개인)에 사용자가 적용 되며**    개인 태그를 만들려면이 옵션을 선택 합니다. 이러한 태그 메시지 또는 상위 폴더 또는 전체 사서함에 적용 되는 설정에서로 다른 폴더에 보관 또는 삭제 설정을 적용 하려면 Outlook 및 Outlook Web App 사용자를 허용 합니다.

3.  **새 보존 태그** 페이지 제목 및 옵션을 선택한 태그의 유형에 따라 달라 집니다. 다음 필드에 입력 합니다.
    
      - **이름**    보존 태그에 대 한 이름을 입력 합니다. 태그 이름은 표시 하기 위해 되며 폴더 또는 항목에 적용 되는 태그에 모든 영향을 줄 하지 않습니다. 사용자에 대 한 프로 비전 개인 태그를 Outlook 및 Outlook Web App 에서 사용할 수 있는 것이 좋습니다.
    
      - **다음과 같은 기본 폴더에이 태그 적용**    이 옵션은 **특정 폴더에 자동으로 적용 되며** 선택한 경우에 사용할 수 있습니다.
    
      - **보존 작업**    항목의 보존 기간에 도달 하면 수행할 다음 작업 중 하나를 선택 합니다.
        
          - **삭제 및 복구 허용**    항목을 삭제 하지만 사용자가 Outlook에서 **지운 편지함 복구** 옵션을 사용 하 여 복구할 수 있도록 하려면이 동작을 선택 또는 Outlook Web app. 항목은 사서함 데이터베이스 또는 사서함 사용자에 대해 구성 된 삭제 된 항목 보존 기간에 도달할 때까지 유지 됩니다.
        
          - **영구적으로 삭제**    사서함 데이터베이스에서 항목을 영구적으로 삭제 하려면이 옵션을 선택 합니다.
            

            > [!IMPORTANT]
            > 사서함 이나 항목의 원본 위치 유지 또는 소송 보존에 따라 달라 집니다 보존 및 원본 위치 eDiscovery 검색에서 반환 됩니다. 자세한 내용은 <A href="in-place-hold-and-litigation-hold-exchange-2013-help.md">원본 위치 유지 및 소송 보존</A>를 참조 하십시오.

        
          - **보관 사서함으로 이동**    이 작업은 DPT 또는 개인 태그를 만드는 경우에 사용할 수 있습니다. 항목을 이동 하는 사용자의 원본 위치 보관이이 작업을 선택 합니다.
    
      - **보존 기간**    다음 옵션 중 하나를 선택 합니다.
        
          - **안함**    지정 하는 항목 해야 안함 수 삭제 되거나 보관 사서함으로 이동 하려면이 옵션을 선택 합니다.
        
          - **항목에는 다음 기간 (일)에 도달 하는 경우**    이 옵션을 선택 하 고 옮겨졌거나 삭제 하기 전에 항목을 유지 하는 일 수를 지정 합니다. 항목을 수신 하거나 만든 날짜부터 일정 및 작업을 제외한 모든 지원 되는 항목에 대 한 보존 기간 계산 됩니다. 종료 날짜부터 일정 및 작업 항목에 대 한 보존 기간 계산 됩니다.
    
      - **메모**    사용자를 관리 메모 또는 설명 입력이 선택적 필드입니다. 이 필드는 사용자에 게 표시 되지 않습니다.

**셸을 사용 하 여 보존 태그를 만들려면**

**New-RetentionPolicyTag** cmdlet를 사용 하 여 보존 태그를 만듭니다. Cmdlet에서 사용할 수 있는 다른 옵션을 사용 하 다양 한 유형의 보존 태그를 만들 수 있습니다. *Type* 매개 변수를 사용 하 여 DPT를 만들려면 (`All`) RPT ( `Inbox`와 같은 기본 폴더 유형 지정) 또는 개인 태그 (`Personal`).

이 예제에서는 7 년 (2,556 일) 후 사서함에 있는 모든 메시지를 삭제 하려면 DPT를 만듭니다.

    New-RetentionPolicyTag -Name "DPT-Corp-Delete" -Type All -AgeLimitForRetention 2556 -RetentionAction DeleteAndAllowRecovery

이 예제에서는 2 년 (730 일)의 모든 메시지 원본 위치 보관 사서함으로 이동 하는 DPT를 만듭니다.

    New-RetentionPolicyTag -Name "DPT-Corp-Move" -Type All -AgeLimitForRetention 730 -RetentionAction MoveToArchive

이 예제에서는 20 일 후 음성 메일 메시지를 삭제 하려면 DPT를 만듭니다.

    New-RetentionPolicyTag -Name "DPT-Corp-Voicemail" -Type All -MessageClass Voicemail -AgeLimitForRetention 20 -RetentionAction DeleteAndAllowRecovery

이 예제에서는 30 일 후 정크 메일 폴더에 메시지를 영구적으로 삭제 하는 RPT를 만듭니다.

    New-RetentionPolicyTag -Name "RPT-Corp-JunkMail" -Type JunkEmail -AgeLimitForRetention 30 -RetentionAction PermanentlyDelete

이 예제에서는 메시지를 삭제 하지 않도록 개인 태그를 만듭니다.

    New-RetentionPolicyTag -Name "Never Delete" -Type Personal -RetentionAction DeleteAndAllowRecovery -RetentionEnabled $false

## 2단계: 보존 정책 만들기

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "메시징 레코드 관리" 항목.

**EAC를 사용 하 여 보존 정책을 만들려면**

1.  **규정 준수 관리** 로 이동 \> **보존 정책**, 다음![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**추가** 클릭 하 고

2.  **새 보존 정책** 다음 필드에 입력 합니다.
    
      - **이름**    보존 정책에 대 한 이름을 입력 합니다.
    
      - **보존 태그**    이 보존 정책에 추가 하려는 태그를 선택 하려면![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**추가** 클릭 합니다.
        
        보존 정책에는 다음과 같은 태그 포함 될 수 있습니다.
        
          - **보관함으로 이동** 작업이 있는 DPT 하나
        
          - **삭제 및 복구 허용** 또는 **영구 삭제** 작업이 할당된 DPT 하나
        
          - **삭제 및 복구 허용** 또는 **영구 삭제** 작업이 포함된 음성 사서함 메시지에 대한 DPT 하나
        
          - 항목을 삭제 하려면 **받은 편지함** 같은 기본 폴더 당 RPT 하나
        
          - 개인 태그의 번호
            

            > [!NOTE]
            > 보존 정책에 개인 태그의 번호를 추가할 수 있지만 다른 보존 설정 사용 하 여 여러 개인 태그를 가진 사용자가 혼동할 수 있습니다. 보존 정책에 10 개 미만의 개인 태그를 연결 하는 것이 좋습니다.

        
        보존 정책, 보존 태그를 추가 하지 않고 만들 수 있지만 정책이 적용 되는 사서함의 항목을 이동 되거나 삭제 될 되지 않습니다. 추가 하 고 만들어진 후 보존 정책에서 보존 태그를 제거할 수도 있습니다.

**셸을 사용 하 여 보존 정책을 만들려면**

보존 정책 Retentionpolicy-corp를 만들고 *RetentionPolicyTagLinks* 매개 변수를 사용 하 여 정책 5 개 태그를 연결 하는이 예제입니다.

    New-RetentionPolicy "RetentionPolicy-Corp"  -RetentionPolicyTagLinks "DPT-Corp-Delete","DPT-Corp-Move","DPT-Corp-Voicemail","RPT-Corp-JunkMail","Never Delete"

구문과 매개 변수에 대한 자세한 내용은 [New-RetentionPolicy](https://technet.microsoft.com/ko-kr/library/dd297970\(v=exchg.150\))를 참조하십시오.

## 3 단계: 사서함 사용자에 게 보존 정책 적용

보존 정책을 만든 후 사서함 사용자에 게 적용 해야 합니다. 다른 사용자 집합에 다른 보존 정책을 적용할 수 있습니다. 자세한 내용은 [사서함에 보존 정책 적용](apply-a-retention-policy-to-mailboxes-exchange-2013-help.md)을 참조 하십시오.

## 이 작업의 작동 여부는 어떻게 확인합니까?

보존 태그를 만들 하 고 보존 정책에 추가할 한 사서함 사용자에 게 정책을 적용 한 후 다음에 사서함을 처리 하는 MRM 사서함 도우미 메시지는 이동 되거나 삭제 보존 태그에 구성에 따라 설정 합니다.

보존 정책 적용 했는지를 확인 하려면 다음을 수행 합니다.

1.  단일 사서함에 대해 MRM 도우미를 수동으로 실행 하려면 다음 셸 명령을 실행 합니다.
    
        Start-ManagedFolderAssistant -Identity <mailbox identity>

2.  Outlook 또는 Outlook Web App 를 사용 하 여 사서함에 로그온 하 고 메시지가 삭제 되거나 정책 구성에 따라 보관으로 이동 되었는지 확인 합니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


