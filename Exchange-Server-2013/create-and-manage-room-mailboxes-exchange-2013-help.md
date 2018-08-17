---
title: '대화방 사서함 만들기 및 관리: Exchange 2013 Help'
TOCTitle: 대화방 사서함 만들기 및 관리
ms:assetid: f70752ad-fce0-4e14-8428-fc5ac63f6c54
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ215781(v=EXCHG.150)
ms:contentKeyID: 50482363
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 대화방 사서함 만들기 및 관리

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-02-02_

예상 완료 시간: 5분

대화방 사서함은 회의실, 강당, 또는 교육 회의실 등의 실제 위치에 할당 된 리소스 사서함입니다. 대화방 사서함에서 관리자를 만든 후 사용자는 모임 요청에서 대화방 사서함을 포함 하 여 대화방 쉽게 예약할 수 있습니다. 자세한 내용은 [받는 사람](recipients-exchange-2013-help.md)를 체크아웃 합니다.

다른 유형의 리소스 사서함에 대 한 정보를 [장비 사서함 관리](manage-equipment-mailboxes-exchange-2013-help.md)을 확인 합니다.

## 무슨 작업을 하고 싶으십니까?

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션.


> [!IMPORTANT]
> 하이브리드 시나리오에서 Exchange 2013을 실행 중인 경우에는 적절한 위치에 대화방 사서함을 만들어야 합니다. 온-프레미스 조직용 대화방 사서함은 온-프레미스에, Exchange Online용 대화방 사서함은 클라우드에 만들어야 합니다.




## 대화방 사서함 만들기

## Exchange 관리 센터를 사용 하 여 대화방 사서함을 만들려면

1.  Exchange 관리 센터에서 **받는 사람** 에 게 이동 \> **리소스** 입니다.

2.  대화방 사서함을 만들려면 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 클릭 \> **대화방 사서함** 입니다.

3.  새 리소스 사서함에 대한 설정을 지정하려면 페이지 옵션을 사용합니다.
    
      - **\* 방 이름**    이 상자를 사용 하 여 대화방 사서함에 대 한 이름을 입력 합니다. Exchange 관리 센터 및 조직의 주소록에서 리소스 사서함 목록에 나열 된 이름입니다. 이 이름은 필요 하 고 64 자를 초과할 수 없는 것입니다.
        

        > [!TIP]
        > 위치 및 용량과 같은 방의 세부 정보를 설명하는 다른 필드가 있지만 일관성 있는 명명 규칙을 사용하여 방 이름에 가장 중요한 세부 정보를 요약하는 것이 좋습니다. 그 이유는 사용자가 모임 요청의 주소록에서 방을 선택할 때 세부 정보를 쉽게 확인할 수 있기 때문입니다.

    
      - **\* 전자 메일 주소**   대화방 사서함에는 예약 요청을 수신할 수 있는 전자 메일 주소가 있습니다. 전자 메일 주소는 @ 기호 왼쪽의 별칭(포리스트에서 고유해야 함)과 오른쪽의 도메인 이름으로 구성됩니다. 전자 메일 주소는 필수입니다.
    
      - **위치**, **전화**, **용량**   이러한 필드를 사용하여 방에 대한 정보를 입력할 수 있습니다. 그러나 앞에서 설명한 대로 사용자가 볼 수 있도록 방 이름에 이 정보의 일부 또는 전체를 포함할 수 있습니다.

4.  작업이 끝나면 **저장**을 클릭하여 대화방 사서함을 만듭니다.

대화방 사서함을 만든 후에 예약 옵션, 메일 설명 및 사서함 위임 하는 방법에 대 한 정보를 업데이트 하 여 대화방 사서함을 편집할 수 있습니다. 대화방 사서함 속성을 변경 하려면 아래 Exchange 관리 센터 섹션을 사용 하 여 체크아웃

## Exchange PowerShell을 사용 하 여 대화방 사서함을 만들려면

이 예에서는 다음 구성을 사용하여 대화방 사서함을 만듭니다.

  - 대화방 사서함은 사서함 데이터베이스 1에 있습니다.

  - 사서함의 이름은 ConfRoom1입니다. 이 이름은 대화방의 전자 메일 주소를 만드는 데도 사용됩니다.

  - Exchange 관리 센터 및 주소록의 표시 이름은 Conference Room 1 됩니다.

  - *Room* 스위치는 이 사서함을 대화방 사서함으로 만들도록 지정합니다.

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name ConfRoom1 - -DisplayName "Conference Room 1" -Room

구문과 매개 변수에 대한 자세한 내용은 [New-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997663\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

만든 대화방 사서함 올바르게 다양 한 방법으로 메시지를 몇 있는지 항목을 확인할 수 있습니다.:

  - Exchange 관리 센터에서 **받는 사람** 에 게 이동 \> **리소스** 입니다. 새 대화방 사서함은 사서함 목록에 표시 됩니다. **사서함 유형** 아래에서 형식이 **룸**입니다.

  - Exchange PowerShell에서 새 대화방 사서함에 대 한 정보를 표시 하려면 다음 명령을 실행 합니다.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## 방 목록 만들기

1백 개가 넘는 대화방을 만들 계획이거나 이미 만든 경우에는 방 목록을 사용하여 대화방을 구성할 수 있습니다. 회사의 여러 건물에 회의를 위해 예약할 수 있는 대화방이 있으면 각 건물에 대해 방 목록을 만들면 유용할 수 있습니다. 방 목록은 메일 그룹과 같은 방식으로 사용할 수 있는 특수하게 표시된 메일 그룹입니다. 그러나 방 목록은 Exchange 관리 셸을 통해서만 만들 수 있습니다.

## Exchange PowerShell을 사용 하 여 방 목록 만들기

이 예에서는 건물 32의 방 목록을 만듭니다.

    New-DistributionGroup -Name "Building 32 Conference Rooms" -OrganizationalUnit "contoso.com/rooms" -RoomList

## Exchange PowerShell을 사용 하 여 방 목록에 방 추가 하려면

이 예에서는 건물 32 방 목록에 confroom3223을 추가합니다.

    Add-DistributionGroupMember -Identity "Building 32 Conference Rooms" -Member confroom3223@contoso.com

## Exchange PowerShell을 사용 하 여 메일 그룹을 방 목록으로 변환 하려면

회의실이 포함되어 있는 메일 그룹을 이전에 이미 만들었을 수 있습니다. 이 경우 그룹을 다시 만들 필요가 없으며 방 목록으로 빠르게 변환할 수 있습니다.

이 예에서는 메일 그룹(건물 34 회의실)을 방 목록으로 변환합니다.

    Set-DistributionGroup -Identity "Building 34 Conference Rooms" -RoomList

## 대화방 사서함 속성 변경

대화방 사서함을 만든 후 변경 하 고 Exchange 관리 센터 또는 Exchange PowerShell을 사용 하 여 추가 속성을 설정할 수 있습니다.

## Exchange 관리 센터를 사용 하 여 대화방 사서함 속성을 변경 하려면

1.  Exchange 관리 센터에서 **받는 사람** 에 게 이동 \> **리소스** 입니다.

2.  리소스 사서함 목록에서 속성을 변경하려는 대화방 사서함을 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  대화방 사서함 속성 페이지에서 다음 섹션 중 하나를 클릭하여 속성을 보거나 변경합니다.
    
      - General
    
      - Delegates
    
      - Booking Options
    
      - Contact Information
    
      - Email Address
    
      - MailTip

## 일반

리소스에 대한 기본 정보를 보거나 변경하려면 **일반** 섹션을 사용합니다.

  - **\* 방 이름**    이 이름은 조직의 주소록 및 Exchange 관리 CenterExchange 관리 센터에서 리소스 사서함 목록에 나타납니다. 변경 하는 경우 64 자를 초과할 수 없습니다 것입니다.

  - **\* 전자 메일 주소**   이 읽기 전용 상자에는 대화방 사서함의 전자 메일 주소가 표시됩니다. Email Address 섹션에서 변경할 수 있습니다.

  - **용량**   이 상자에는 해당 대화방에 포함하기 적절한 최대 사람 수를 입력합니다.

다음과 같은 추가 속성을 보거나 변경하려면 **기타 옵션**을 클릭합니다.

  - **조직 구성 단위**   이 읽기 전용 상자에는 대화방 사서함의 계정이 포함된 OU(조직 구성 단위)가 표시됩니다. 계정을 다른 OU로 이동하려면 Active Directory 사용자 및 컴퓨터를 사용해야 합니다.

  - **사서함 데이터베이스**    이 읽기 전용 상자를 표시 하는 대화방 사서함을 호스팅하는 사서함 데이터베이스의 이름입니다. Exchange 관리 센터에서 **마이그레이션** 페이지를 사용 하 여 사서함을 다른 데이터베이스로 이동 합니다.

  - **\* 별칭** 이 상자에서는 대화방 사서함의 별칭을 변경합니다.

  - **주소 목록에서 숨기기**   해당 주소록 및 Exchange 조직에 정의된 기타 주소 목록에 대화방 사서함이 표시되지 않도록 하려면 이 확인란을 선택합니다. 이 확인란을 선택한 후에도 사용자는 전자 메일 주소를 사용하여 대화방 사서함으로 예약 메시지를 보낼 수 있습니다.

  - **부서**   대화방이 연결된 부서 이름을 지정하는 데 이 상자를 사용합니다. 이 속성을 사용하여 동적 메일 그룹과 주소 목록에 대한 받는 사람 조건을 만들 수 있습니다.

  - **회사**   대화방이 연결된 회사(적용 가능한 경우)를 지정하는 데 이 상자를 사용합니다. Department 속성과 마찬가지로 이 속성을 사용하여 동적 메일 그룹과 주소 목록에 대한 받는 사람 조건을 만들 수 있습니다.

  - **주소록 정책**   대화방 사서함에 대한 ABP(주소록 정책)를 지정하려면 이 옵션을 사용합니다. ABP에는 GAL(전체 주소 목록), OAB(오프라인 주소록), 방 목록 및 일련의 주소 목록이 들어 있습니다. 자세한 내용은 [주소록 정책](address-book-policies-exchange-2013-help.md)를 참조하십시오.
    
    드롭다운 목록에서 이 사서함에 연결할 정책을 선택합니다.

  - **사용자 지정 특성**   이 섹션에는 대화방 사서함에 대해 정의된 사용자 지정 특성이 표시됩니다. 사용자 지정 특성 값을 지정하려면 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다. 받는 사람에 대해 최대 15개의 사용자 지정 특성을 지정할 수 있습니다.

## 위임

이 섹션에서는 대화방 사서함이 예약 요청을 처리하는 방식을 보거나 변경하고, 예약 요청이 자동으로 수락 또는 거절되지 않을 경우 이 작업을 수행할 수 있는 사람을 정의할 수 있습니다.

  - **예약 요청**   예약 요청을 처리하려면 다음 옵션 중 하나를 선택합니다.
    
      - **예약 요청을 자동으로 수락 또는 거절**   모임 요청이 유효한 경우 대화방이 자동으로 예약됩니다. 기존 예약과의 일정 충돌이 있는 경우나 예약 요청이 리소스의 일정 제한을 위반하는 경우(예: 예약 기간이 너무 긴 경우) 모임 요청이 자동으로 거부됩니다.
    
      - **예약 요청을 수락하거나 거절할 대리인 선택**   리소스 대리인은 대화방 사서함에 전송되는 모임 요청을 수락 또는 거절합니다. 둘 이상의 리소스 대리인을 할당하는 경우 이 중 한 대리인만 특정 모임 요청에 대해 작업을 수행해야 합니다.

  - **대리인**   대리인에게 예약 요청을 보내도록 요구하는 옵션을 선택한 경우 지정된 대리인이 나열됩니다. **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 또는 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")을 클릭하여 이 목록에서 대리인을 추가하거나 제거합니다.

## 예약 옵션

**예약 옵션** 섹션에서는 대화방을 예약할 수 있는 경우, 예약 가능 기간, 얼마나 미리 예약할 수 있는지를 정의하는 예약 정책에 대한 설정을 보거나 변경합니다.

  - **되풀이 모임 허용**   이 설정을 사용하여 대화방의 되풀이 모임을 허용하거나 방지합니다. 기본적으로 이 설정은 사용하도록 설정되어 있으므로 되풀이 모임이 허용됩니다.

  - **작업 시간 중에만 예약 허용**   이 설정은 대화방에 대해 정의된 작업 기간에 포함되지 않는 모임 요청을 수락하거나 거부합니다. 기본적으로 이 설정은 사용하지 않도록 설정되어 있으므로 업무 시간 외의 모임 요청이 허용됩니다. 기본적으로 업무 시간은 월요일에서 금요일까지, 오전 8시에서 오후 5시까지입니다. 일정 페이지의 모양 섹션에서 대화방 사서함의 작업 시간을 구성할 수 있습니다.

  - **종료 날짜가 이 한도를 넘으면 항상 거부**   이 설정은 최대 예약 지연 시간 설정으로 지정된 날짜를 넘어가는 되풀이 모임의 동작을 제어합니다.
    
      - 이 설정을 사용하도록 설정하는 경우 예약이 **최대 예약 리드 타임** 상자의 값으로 지정된 날짜 또는 이전에 시작되면 되풀이 예약 요청이 자동으로 거부됩니다. 기본 설정입니다.
    
      - 이 설정을 사용하지 않도록 설정하는 경우 예약 요청이 **최대 예약 리드 타임** 상자의 값으로 지정된 날짜 또는 이전에 시작되면 되풀이 예약 요청이 자동으로 수락됩니다. 그러나 지정된 날짜 이후에 모임이 발생하지 않도록 예약 수가 감소합니다.

  - **최대 예약 리드 타임(일)**   이 설정은 대화방을 미리 예약할 수 있는 최대 일 수를 지정합니다. 유효한 입력은 0에서 1080 사이의 정수입니다. 기본값은 180일입니다.

  - **최대 기간(시간)**   이 설정은 예약 요청에서 대화방을 예약할 수 있는 최대 기간을 지정합니다. 기본값은 24시간입니다.
    
    되풀이 예약 요청의 경우 최대 예약 기간은 Exchange Admin Centerh 되풀이 예약 요청 인스턴스의 길이에 적용 됩니다.

이 페이지에는 대화방을 예약하기 위해 예약 요청을 전송하는 사용자에게 전송되는 메시지를 작성하는 데 사용할 수 있는 상자도 포함되어 있습니다.

## 연락처 정보

**연락처 정보** 섹션에서는 대화방의 연락처 정보를 보거나 변경할 수 있습니다. 이 페이지의 정보는 주소록에 표시됩니다.


> [!TIP]
> <STRONG>시/도</STRONG> 상자를 사용하여 동적 메일 그룹, 전자 메일 주소 정책 또는 주소 목록에 대한 받는 사람 조건을 만들 수 있습니다.



## 전자 메일 주소

**전자 메일 주소** 섹션에서는 대화방 사서함과 연결된 전자 메일 주소를 보거나 변경할 수 있습니다. 여기에는 사서함의 기본 SMTP 주소와 모든 관련 프록시 주소가 포함됩니다. 기본 SMTP 주소(*회신 주소*)는 주소록에 굵게 표시되며 대문자로 된 **SMTP** 값이 **유형** 열에 표시됩니다.

  - **추가**   이 사서함에 대해 새 전자 메일 주소를 추가하려면 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭합니다. 다음 주소 형식 중 하나를 선택합니다.
    
      - **SMTP**   기본 주소 유형입니다. 이 단추를 클릭하고 **\* 전자 메일 주소** 상자에 새 SMTP 주소를 입력합니다.
    
      - **EUM**   EUM(Exchange 통합 메시징) 주소는 Microsoft Exchange 통합 메시징 서비스가 Exchange 조직 내의 UM 사용 가능 보낸 사람을 찾는 데 사용됩니다. EUM 주소는 UM 사용 가능 사용자의 UM 다이얼 플랜과 내선 번호로 구성되어 있습니다. 이 단추를 클릭하고 **주소/내선 번호** 상자에 내선 번호를 입력합니다. 그런 다음 **찾아보기**를 클릭하고 사서함에 대한 다이얼 플랜을 선택합니다.
    
      - **사용자 지정 주소 유형**   이 단추를 클릭하고 **\* 전자 메일 주소** 상자에 지원되는 SMTP 이외의 전자 메일 주소 유형 중 하나를 입력합니다.
        

        > [!NOTE]
        > X.400 주소를 제외하고 Exchange는 사용자 지정 주소 형식이 올바른지 확인하지 않습니다. 지정하는 사용자 지정 주소는 해당 주소 유형에 대한 형식 요구 사항을 충족해야 합니다.

    

    > [!NOTE]
    > 새 전자 메일 주소를 추가하는 경우 해당 전자 메일 주소를 기본 SMTP 주소로 만드는 옵션이 있습니다.



  - **이 받는 사람에게 적용된 전자 메일 주소 정책에 따라 전자 메일 주소를 자동으로 업데이트**   조직의 전자 메일 주소 정책에 대한 변경 내용에 따라 받는 사람의 전자 메일 주소가 자동으로 업데이트되도록 하려면 이 확인란을 선택합니다.

## MailTip

**메일 설명** 섹션에서는 메일 설명을 추가하여 대화방 사서함으로 예약 요청을 보낼 경우 발생할 수 있는 문제를 사용자에게 알릴 수 있습니다. 메일 설명은 새 전자 메일 메시지의 받는 사람, 참조 또는 숨은 참조 필드에 이 받는 사람이 추가될 때 정보 표시줄에 표시되는 텍스트입니다.


> [!NOTE]
> 메일 설명은 HTML 태그를 포함할 수 있지만 스크립트는 사용할 수 없습니다. 표시되는 사용자 지정 메일 설명의 길이는 175자를 초과할 수 없습니다. 단, HTML 태그는 길이 제한 계산에 포함되지 않습니다.



## Exchange PowerShell을 사용 하 여 대화방 사서함 속성을 변경 하려면

다음 cmdlet 집합을 사용하여 대화방 사서함 속성을 보고 변경할 수 있습니다. 대화방 사서함의 일반 속성과 전자 메일 주소를 보고 변경하려면 **Get-Mailbox** 및 **Set-Mailbox** cmdlet을 사용합니다. 대리인과 예약 옵션을 보고 변경하려면 **Get-CalendarProcessing** 및 **Set-CalendarProcessing** cmdlet을 사용합니다.

  - **Get-User** 및 **Set-User**   이러한 cmdlet으로는 위치, 부서 및 회사 이름과 같은 일반 속성을 보고 설정할 수 있습니다.

  - **Get-Mailbox** 및 **Set-Mailbox**   전자 메일 주소, 사서함 데이터베이스 같은 사서함 속성을 보고 설정하려면 이러한 cmdlet을 사용합니다.

  - **Get-CalendarProcessing** 및 **Set-CalendarProcessing**   예약 옵션과 대리인을 보고 설정하려면 이러한 cmdlet을 사용합니다.

이러한 cmdlet에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Get-User](https://technet.microsoft.com/ko-kr/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/ko-kr/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/ko-kr/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/ko-kr/library/dd335046\(v=exchg.150\))

다음은 Exchange PowerShell을 사용 하 여 대화방 사서함 속성을 변경 하려면의 몇가지 예입니다.

이 예에서는 표시 이름, 기본 SMTP 주소(기본 회신 주소) 및 대화방 용량을 변경합니다. 또한 이전 회신 주소는 프록시 주소로 보관됩니다.

    Set-Mailbox "Conf Room 123" -DisplayName "Conf Room 31/123 (12)" -EmailAddresses SMTP:Rm33.123@contoso.com,smtp:rm123@contoso.com -ResourceCapacity 12

이 예에서는 예약 요청이 업무 시간 중으로만 예약되도록 대화방 사서함을 구성하고 최대 기간을 9시간으로 설정합니다.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true -MaximumDurationInMinutes 540

이 예에서는 **Get-User** cmdlet을 사용하여 전용 회의실에 해당하는 모든 대화방 사서함을 찾은 다음 **Set-CalendarProcessing** cmdlet을 사용하여 대리인 Robin Wood에게 예약 요청을 전송하여 수락하거나 거절하도록 합니다.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox') -and (DisplayName -like 'Private*')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Robin Wood"

## 작동 여부는 어떻게 확인합니까?

대화방 사서함의 속성을 성공적으로 변경했는지 확인하려면 다음을 수행하십시오.

  - Exchange 관리 센터에서 사서함을 선택 하 고 해당 속성이 나 사용자가 변경한 기능을 보려면 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘") 를 클릭 합니다. 사용자가 변경한 속성에 따라 선택한 사서함에 대 한 세부 정보 창에 표시 될 수 있습니다.

  - Exchange PowerShell에서 변경 된 내용을 확인 하려면 **Get-Mailbox** cmdlet을 사용 합니다. 하나의 장점은 Exchange PowerShell을 사용 하 여 여러 사서함에 대 한 여러 속성을 볼 수 있는 점입니다. 위의 예에서 여기서 예약 요청이 근무 시간 동안에 예약할 수 있고 최대 기간을 9 시간에 새 값을 확인 하려면 다음 명령을 실행 합니다.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours,MaximumDurationInMinutes

이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


