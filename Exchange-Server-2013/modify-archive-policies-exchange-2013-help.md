---
title: '보관 정책 수정: Exchange 2013 Help'
TOCTitle: 보관 정책 수정
ms:assetid: 1e3002c2-801a-43ea-ae00-52ab34d76b9c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh529919(v=EXCHG.150)
ms:contentKeyID: 50482620
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보관 정책 수정

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-02-01_

Exchange Server 2013 및 Exchange Online 에서 자동으로 항목을 이동할 사서함 개인 (온-프레미스) 또는 클라우드 기반 보관 사서함에 보관 정책을 사용할 수 있습니다. 보관 정책에는 **보관 사서함으로 이동** 보존 작업을 사용 하는 보존 태그입니다.

Exchange 설치 프로그램은 **기본 MRM 정책**이라는 보존 정책을 만듭니다. 이 정책에는 2년 후에 항목을 보관 사서함으로 이동하는 기본 정책 태그(DPT)가 할당되었습니다. 이 정책에는 사용자가 메시지를 자동으로 이동하거나 삭제할 폴더나 사서함 항목에 적용할 수 있는 여러 가지 개인 태그가 포함되어 있습니다. 사서함에 할당된 보존 정책이 없지만 사서함을 보관할 수 있는 경우 Exchange가 **기본 MRM 정책**을 자동으로 적용합니다. 고유한 사서함 및 보존 정책을 만들어 사서함 사용자에게 적용할 수도 있습니다. 자세한 내용은 [보존 태그 및 보존 정책](retention-tags-and-retention-policies-exchange-2013-help.md) 항목을 참조하십시오.

비즈니스 요구 사항에 맞게 기본 정책에 포함된 보존 태그를 수정할 수 있습니다. 예를 들면 2년이 아니라 3년 후에 항목을 보관함으로 이동하도록 보관함 DPT를 수정할 수 있습니다. 추가 개인 태그를 만들어 **기본 MRM 정책**을 포함한 보존 정책에 이를 추가하거나, 사용자가 Outlook Web App 옵션에서 자신의 사서함으로 개인 태그를 추가하도록 할 수 있습니다.

보관 관련 된 추가 관리 작업에 대 한 참조:

  - **Exchange Server 2013:**  [Exchange 2013에서 원본 위치 보관 관리](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:**  [Exchange Online의 보관 사서함을 사용 하지 않도록 설정 하거나 사용](https://technet.microsoft.com/ko-kr/library/jj984357\(v=exchg.150\))


> [!NOTE]
> Exchange 하이브리드 배포에서 온-프레미스 기본 사서함에 대해 클라우드 기반 보관 사서함을 사용하도록 설정할 수 있습니다. 온-프레미스 사서함에 보관 정책을 할당하면 항목이 클라우드 기반 보관함으로 이동됩니다. 항목이 보관 사서함으로 이동되면 온-프레미스 사서함에 해당 복사본이 유지되지 않습니다. 온-프레미스 사서함에 보류 상태가 적용되면 보관 정책은 항목을 클라우드 기반 보관 사서함 항목으로 이동하여 보류로 지정된 기간 동안 유지되도록 합니다.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "메시징 레코드 관리" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 기본 보관 정책 수정

1.  **규정 준수 관리** \> **보존 태그**로 이동합니다.

2.  목록 보기에서 **기본 2년 후 보관함으로 이동** 태그를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.
    

    > [!TIP]
    > <STRONG>유형</STRONG> 열을 클릭하여 보존 태그를 유형별로 정렬할 수 있습니다. 기본 보관 정책은 <STRONG>기본값</STRONG> 유형으로 표시되며 <STRONG>보관</STRONG> 보존 작업이 있습니다. 또는 <STRONG>이름</STRONG>을 클릭하여 보존 태그를 이름으로 정렬합니다.



3.  
    
    **보존 태그**에서 다음 설정을 보거나 수정한 다음 **저장**을 클릭합니다.
    
      - **이름**   페이지 맨 위에 있는 이 상자에서 태그 이름을 보거나 변경할 수 있습니다.
    
      - **보존 태그 형식**   이 읽기 전용 필드에는 태그 형식이 표시됩니다.
    
      - **보존 작업**   보관 정책에 대해 이 필드를 수정하지 마십시오.
    
      - **보존 기간** 다음 옵션 중 하나를 선택합니다.
        
          - **사용 안 함**   태그를 사용하지 않으려면 이 버튼을 클릭합니다. DPT를 사용하지 않도록 설정하면 더 이상 태그가 사서함에 적용되지 않습니다.
            

            > [!IMPORTANT]
            > 사용하지 않도록 설정한 보존 태그를 적용한 항목이 사서함 도우미에서 처리되지 않습니다. 태그를 항목에 적용하지 않도록 하려면 태그를 삭제하는 것보다 태그를 사용하지 않도록 설정하는 것이 좋습니다. 태그를 삭제하면 태그 구성이 Active Directory에서 삭제되며 사서함 도우미가 삭제된 태그를 제거하도록 모든 메시지를 처리합니다.

            

            > [!NOTE]
            > 사용자가 삭제되지 않는다고 생각하는 항목에 태그를 적용하는 경우, 나중에 태그를 사용하도록 설정하면 사용자가 기본 사서함에 보존하고자 하는 항목이 이동될 수 있습니다.

        
          - **항목이 다음 보존 기간(일)에 도달할 경우**   특정 기간 후 항목을 보관함으로 이동하도록 지정하려면 이 버튼을 클릭합니다. 기본적으로 이 설정은 2년(730일) 후에 항목을 보관함으로 이동하도록 구성됩니다. 이 설정을 수정하려면 해당 텍스트 상자에 보존 기간 일 수를 입력합니다. 값 범위는 1일부터 24,855일까지입니다.
    
      - **설명**   이 상자를 사용하여 Outlook 및 Outlook Web App 사용자에게 표시할 설명을 입력합니다.

## 셸을 사용하여 보관 정책 수정

이 예에서는 1,095일(3년) 후에 항목을 이동하도록 `Default 2 year move to archive` 태그를 수정합니다.

    Set-RetentionPolicyTag "Default 2 year move to archive" -Name "Default 3 year move to archive" -AgeLimitForRetention 1095

이 예에서는 `Default 2 year move to archive` 태그를 사용하지 않도록 설정합니다.

    Set-RetentionPolicyTag "Default 2 year move to archive" -RetentionEnabled $false

이 예에서는 모든 보관 DPT와 개인 태그를 검색하고 사용하지 않도록 설정합니다.

    Get-RetentionPolicyTag | ? {$_.RetentionAction -eq "MoveToArchive"} | Set-RetentionPolicyTag -RetentionEnabled $false

구문과 매개 변수에 대한 자세한 내용은 [Set-RetentionPolicyTag](https://technet.microsoft.com/ko-kr/library/dd298042\(v=exchg.150\)) 및 [Get-RetentionPolicyTag](https://technet.microsoft.com/ko-kr/library/dd298009\(v=exchg.150\)) 항목을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

[Get-RetentionPolicyTag](https://technet.microsoft.com/ko-kr/library/dd298009\(v=exchg.150\)) cmdlet를 사용하여 보존 태그의 설정을 검색합니다.

이 명령은 `Default 2 year move to archive` 보존 태그의 속성을 검색하고 출력을 **Format-List** cmdlet로 파이프하여 모든 속성을 목록 형식으로 표시합니다.

    Get-RetentionPolicyTag "Default 2 year move to archive" | Format-List

