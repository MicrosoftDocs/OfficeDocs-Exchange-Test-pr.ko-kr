---
title: '저널링 관리: Exchange 2013 Help'
TOCTitle: 저널링 관리
ms:assetid: d517f27e-f80a-4a06-988c-cbbf981c701d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ651670(v=EXCHG.150)
ms:contentKeyID: 50484229
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 저널링 관리

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

저널링에는 인바운드 및 아웃 바운드 전자 메일 통신을 기록 하 여 법적, 규정 및 조직 규정 준수 요구 사항에 응답 하 여 조직의 데 도움이 됩니다. 이 항목에서는 Exchange 2013 및 Exchange Online 저널링 관리와 관련 된 기본 작업을 수행 하는 방법을 보여줍니다.

표준 저널링은 사서함 데이터베이스에서 구성됩니다. 저널링 에이전트가 특정 사서함 데이터베이스에 있는 사서함에서 주고받는 모든 메시지를 저널링할 수 있게 합니다. 고급 저널링을 사용하면 저널링 에이전트가 저널 규칙을 사용하여 보다 세부적인 저널링을 수행할 수 있습니다. 사서함 데이터베이스에 있는 모든 사서함을 저널링하는 대신 개별 받는 사람 또는 메일 그룹의 구성원을 저널링하여 조직의 요구 사항에 맞게 저널 규칙을 구성할 수 있습니다. 고급 저널링을 사용하려면 Exchange Enterprise CAL(클라이언트 액세스 라이선스)이 있어야 합니다.

저널링에 대한 자세한 내용은 [저널링](journaling-exchange-2013-help.md)를 참조하십시오.

**내용**

저널 규칙 만들기

저널 규칙 보기 또는 수정

저널 규칙을 사용 하지 않도록 설정 하거나 사용

저널 규칙 제거

사서함 단위 데이터베이스 저널링을 사용 하지 않도록 설정 하거나 사용

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "저널링" 항목

  - 저널링 사서함 만들어진 또는 기존 사서함을 저널링 사서함으로 사용할 수 있습니다. 저널링 사서함으로 Exchange Online 사서함을 지정할 수는 없습니다. 온-프레미스를 저널 보고서를 전달할 수 시스템 또는 타사 보관 서비스를 보관 합니다. 하이브리드 배포를 실행 하는 온-프레미스 서버와 Exchange Online 로 분할 하 여 사서함이 있는 경우 Exchange Online 및 온-프레미스 사서함에 대 한 온-프레미스 사서함을 저널링 사서함으로 지정할 수 있습니다.
    

    > [!IMPORTANT]
    > 존재 하지 않거나 잘못 된 대상에 저널링 사서함을 저널 보고서를 보낼 수 Exchange Online 저널링 규칙을 구성한 경우 저널 보고서 Microsoft 데이터 센터 서버에서 전송 큐에 남아 있습니다. 이러한 상황이 발생 하는 경우 Microsoft 데이터 센터 담당자는 조직에 게 문의 하 고 저널 보고서 저널링 사서함에 성공적으로 전달 될 수 있도록 문제를 해결 하는 메시지가 표시 하려고 합니다. 연결할 수 없거나의 2 일 후 문제를 해결 하지 않은 경우 Microsoft 문제가 있는 저널링 규칙 사용 하지 않도록 설정 됩니다.



  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A><STRONG>JournalingReportDNRTo</STRONG> 사서함에 문제가 있는 경우 <A href="https://go.microsoft.com/fwlink/p/?linkid=331674">전송 및 Exchange Online의 사서함 규칙이 예상 대로 작동 하지 않는</A>를 참조 하십시오.



## 저널 규칙 만들기

## EAC를 사용하여 저널 규칙 만들기

1.  EAC에서 **규정 준수 관리** 로 이동 \> **저널 규칙** 을 한 후 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭 합니다.

2.  **저널 규칙**에서 저널 규칙의 이름을 입력하고 다음 필드를 완성합니다.
    
      - **다른 사람에게 메시지를 보내거나 받는 경우**   규칙의 대상이 될 받는 사람을 지정합니다. 특정 받는 사람을 선택하거나 모든 메시지에 규칙을 적용할 수 있습니다.
    
      - **다음 메시지 저널링**   저널 규칙의 범위를 지정합니다. 내부 메시지만 또는 외부 메시지만 저널링하거나, 원본 또는 대상에 상관없이 모든 메시지를 저널링할 수 있습니다.
    
      - **다음 사람에게 저널 보고서 보내기**   모든 저널 보고서를 받을 저널링 사서함의 주소를 입력합니다.
        

        > [!NOTE]
        > 저널 사서함으로 표시 이름 또는 메일 사용자 또는 메일 연락처의 별칭을 입력할 수도 있습니다. 이 경우 저널 보고서는 메일 사용자 또는 메일 연락처의 외부 전자 메일 주소로 전송 됩니다. 하지만 앞에서 설명한 것 처럼 메일 사용자 또는 메일 연락처의 외부 전자 메일 주소를 Exchange Online 사서함의 주소 수 없습니다.



3.  **저장**을 클릭하여 저널 규칙을 만듭니다.

## 셸을 사용하여 저널 규칙 만들기

이 예에서는 받는 사람 user1@contoso.com과 주고받는 모든 메시지를 저널링하는 Discovery Journal Recipients 저널 규칙을 만듭니다.

    New-JournalRule -Name "Discovery Journal Recipients" -Recipient user1@contoso.com -JournalEmailAddress "Journal Mailbox" -Scope Global -Enabled $True

## 작동 여부는 어떻게 확인합니까?

저널 규칙이 성공적으로 만들어졌는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 만든 새 저널 규칙이 **저널 규칙** 탭에 표시되는지 확인합니다.

  - 셸에서 다음 명령을 실행하여 새 저널 규칙이 있는지 확인합니다(아래 예에서는 위의 셸 예에서 만든 규칙을 확인함).
    
        Get-JournalRule "Discovery Journal Recipients"

맨위로 돌아가기

## 저널 규칙 보기 또는 수정

## EAC를 사용하여 저널 규칙을 보거나 수정

1.  EAC에서 **규정 준수 관리** 로 이동 \> **저널 규칙** 입니다.

2.  목록 보기에 조직의 모든 저널 규칙이 표시됩니다.

3.  보거나 수정할 규칙을 두 번 클릭합니다.

4.  **저널 규칙**에서 원하는 설정을 수정합니다. 이 대화 상자의 설정에 대한 자세한 내용은 이 항목의 전반부에 나오는 Use the EAC to create a journal rule 절차를 참조하십시오.

## 셸을 사용하여 저널 규칙을 보거나 수정

이 예에서는 Exchange 조직의 모든 저널 규칙 요약 목록을 표시합니다.

    Get-JournalRule

이 예에서는 저널 규칙 Brokerage Journal Rule을 검색하고 출력을 **Format-List** 명령으로 파이프하여 목록 형식으로 규칙 속성을 표시합니다.

    Get-JournalRule "Brokerage Journal Rule" | Format-List

특정 규칙의 속성을 수정하려면 [Set-JournalRule](https://technet.microsoft.com/ko-kr/library/bb125010\(v=exchg.150\)) cmdlet을 사용해야 합니다. 다음 예에서는 저널 규칙의 이름을 `JR-Sales`에서 `TraderVault`로 변경합니다. 다음 규칙 설정도 변경됩니다.

  - 받는 사람

  - JournalEmailAddress

  - 범위

<!-- end list -->

    Set-JournalRule JR-Sales -Name TraderVault -Recipient traders@woodgrovebank.com -JournalEmailAddress tradervault@woodgrovebank.com -Scope Internal

## 작동 여부는 어떻게 확인합니까?

저널 규칙이 성공적으로 수정되었는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 **준수 관리** \> **저널 규칙**으로 이동합니다. 수정할 규칙을 두 번 클릭하고 변경 내용이 저장되었는지 확인합니다.

  - 셸에서 다음 명령을 실행하여 저널 규칙이 성공적으로 수정되었는지 확인합니다. 이 명령을 실행하면 수정한 속성과 함께 규칙의 이름이 표시됩니다(아래 예에서는 위의 셸 예에서 수정한 규칙을 확인).
    
        Get-TransportRule "TraderVault" | Format-List Name,Recipient,JournalEmailAddress,Scope

맨위로 돌아가기

## 저널 규칙 사용 또는 사용 안 함


> [!IMPORTANT]
> 저널 규칙을 사용하지 않으면 저널링 에이전트가 해당 규칙의 대상이 되는 메시지 저널링을 중지합니다. 저널 규칙을 사용하지 않는 동안에는 규칙에 의해 정상적으로 저널링될 메시지가 저널링되지 않습니다. 저널 규칙을 사용하지 않음으로써 조직의 규정 또는 준수 요구 사항을 위태롭게 해서는 안 됩니다.



## EAC를 사용하여 저널 규칙을 사용하거나 사용하지 않도록 설정

1.  EAC에서 **규정 준수 관리** 로 이동 \> **저널 규칙** 입니다.

2.  목록 보기의 규칙 이름 옆에 있는 **설정** 열에서 규칙을 사용하려면 확인란을 선택하고, 사용하지 않으려면 확인란을 선택하지 않습니다.

## 셸을 사용하여 저널 규칙을 사용하거나 사용하지 않도록 설정

이 예에서는 Contoso 규칙을 사용하도록 설정합니다.

    Enable-JournalRule "Contoso Journal Rule"

이 예에서는 Contoso 규칙을 사용하지 않도록 설정합니다.

    Disable-JournalRule "Contoso Journal Rule"

## 작동 여부는 어떻게 확인합니까?

저널 규칙을 사용하거나 사용하지 않도록 성공적으로 설정했는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 저널 규칙 목록의 **설정** 열 확인란 상태를 확인합니다.

  - 셸에서 다음 명령을 실행하여 조직의 모든 저널 규칙의 목록과 상태를 반환합니다.
    
        Get-JournalRule | Format-Table Name,Enabled

맨위로 돌아가기

## 저널 규칙 제거

## EAC를 사용하여 저널 규칙 제거

1.  EAC에서 **규정 준수 관리** 로 이동 \> **저널 규칙** 입니다.

2.  목록 보기에서 제거할 규칙을 선택하고 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")을 클릭합니다.

## 셸을 사용하여 저널 규칙 제거

이 예제에서는 Brokerage Journal Rule 저널 규칙을 제거합니다.

    Remove-JournalRule "Brokerage Journal Rule"

## 작동 여부는 어떻게 확인합니까?

저널 규칙이 성공적으로 제거되었는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 제거한 저널 규칙이 **저널 규칙** 탭에 더 이상 표시되지 않음을 확인합니다.

  - 셸에서 다음 명령을 실행하여 제거한 규칙이 더 이상 표시되지 않음을 확인합니다.
    
        Get-JournalRule

맨위로 돌아가기

## 사서함 단위 데이터베이스 저널링 사용 또는 사용 안 함


> [!WARNING]
> 사서함 데이터베이스에서 메시지 저널링을 사용하지 않으면 조직이 적용되는 메시징 보존 정책 준수를 위반할 수 있습니다. 또한 해당 사서함 데이터베이스의 사서함에서 주고받는 메시지에 대해 더 이상 저널 수신이 보내지지 않습니다.



## EAC를 사용하여 사서함 단위 데이터베이스 저널링을 사용하거나 사용하지 않도록 설정

1.  EAC에서 **서버** \> **데이터베이스**로 이동합니다.

2.  목록 보기에서 저널링을 사용할 사서함 데이터베이스를 두 번 클릭합니다.

3.  **유지 관리**를 클릭한 다음 **저널 받는 사람** 옆에 있는 **찾아보기**를 클릭하여 저널링 사서함을 선택합니다. 저널 받는 사람을 지정하면 데이터베이스에 대해 저널링을 사용할 수 있습니다.
    
    저널링을 사용하지 않으려면 **X 제거**를 클릭하여 저널 받는 사람을 제거합니다.

## 셸을 사용하여 사서함 단위 데이터베이스 저널링을 사용하거나 사용하지 않도록 설정

이 예에서는 사서함 데이터베이스 Sales Database에 대해 저널링을 사용하도록 설정하고 Sales Database 저널 사서함을 저널 받는 사람으로 설정합니다.

    Set-MailboxDatabase "Sales Database" -JournalRecipient "Sales Database Journal Mailbox"

이 예에서는 Sales Database 사서함 데이터베이스에서 사서함 단위 데이터베이스 저널링을 사용하도록 설정합니다.

    Set-MailboxDatabase "Sales Database" -JournalRecipient $Null

이 예에서는 Exchange 조직의 모든 사서함 데이터베이스에서 사서함 단위 데이터베이스 저널링을 사용하도록 설정합니다. [Get-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb124924\(v=exchg.150\)) cmdlet은 Exchange 조직의 모든 사서함 데이터베이스를 검색하는 데 사용되고, [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\)) cmdlet에 파이프되는 cmdlet의 결과로 발생합니다.

    Get-MailboxDatabase | Set-MailboxDatabase -JournalRecipient $Null

## 작동 여부는 어떻게 확인합니까?

사서함 단위 데이터베이스 저널링을 사용하거나 사용하지 않도록 성공적으로 설정했는지 확인하려면 다음 중 하나를 수행하십시오.

1.  EAC에서 **서버** \> **데이터베이스**로 이동합니다.

2.  확인할 데이터베이스를 두 번 클릭하고 **유지 관리** 탭을 선택합니다.

3.  올바른 저널링 받는 사람이 **저널 받는 사람** 입력란에 표시되면 사서함 데이터베이스에 대해 저널링을 사용하도록 성공적으로 설정한 것입니다. 저널링 받는 사람이 표시되지 않을 경우 데이터베이스에 대해 저널링이 사용되지 않습니다.

<!-- end list -->

  - 셸에서 다음 명령을 실행하여 사서함 데이터베이스와 연결된 저널 받는 사람을 비롯하여, 조직의 모든 사서함 데이터베이스 목록을 반환합니다. 저널 받는 사람이 표시된 데이터베이스에 대해 저널링을 사용하도록 설정되어 있습니다. 그렇지 않은 경우 저널링이 사용되지 않습니다.
    
        Get-MailboxDatabase | Format-Table Name,JournalRecipient

맨위로 돌아가기

## 자세한 내용

[저널링](journaling-exchange-2013-help.md)

[사용 하지 않거나 음성 메일 및 부재중된 전화 알림의 저널링을 사용 하도록 설정](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md)

[New-JournalRule](https://technet.microsoft.com/ko-kr/library/bb125242\(v=exchg.150\))

[Get-JournalRule](https://technet.microsoft.com/ko-kr/library/aa998866\(v=exchg.150\))

[Set-JournalRule](https://technet.microsoft.com/ko-kr/library/bb125010\(v=exchg.150\))

[Enable-JournalRule](https://technet.microsoft.com/ko-kr/library/bb123902\(v=exchg.150\))

[Disable-JournalRule](https://technet.microsoft.com/ko-kr/library/aa995925\(v=exchg.150\))

[Remove-JournalRule](https://technet.microsoft.com/ko-kr/library/bb123489\(v=exchg.150\))

[Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\))

