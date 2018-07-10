---
title: '감사 보고서를 교환 합니다.: Exchange 2013 Help'
TOCTitle: 감사 보고서를 교환 합니다.
ms:assetid: 2b3e1529-1677-4564-be0b-ce22757ddc0d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150497(v=EXCHG.150)
ms:contentKeyID: 50482183
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 감사 보고서를 교환 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

감사 로깅을 사용하면 관리자가 수행한 특정 변경을 추적하여 구성 문제를 해결하고 규정, 규정 준수 및 소송 요구 사항을 따르는 데 도움이 될 수 있습니다. Microsoft Exchange에서는 두 가지 유형의 감사 로깅을 제공합니다.

  - *관리자 감사 로깅* 관리자가 수행 하는 Exchange 관리 셸 cmdlet에 따라 특정 작업을 기록 합니다. 이 구성 문제를 해결 하거나 보안 또는 규정 준수 관련 문제의 원인을 파악 하는데 도움이 됩니다. Exchange Online 작업 Microsoft 관리자가 수행 하 고 위임 관리자, 기록 됩니다.

  - *사서함 감사 로깅* 레코드 관리자, 위임된 된 사용자 또는 사서함을 소유한 사용자가 사서함에 액세스 한 경우. 이 사용자가 사서함에 액세스 하 고 완료 했을 때 어떤 결정 수 있습니다.

이 항목에서는 다음에 대해 설명합니다.

  - Export audit logs

  - Run auditing reports

  - Configure audit logging
    
      - Enable mailbox audit logging
    
      - Give users access to auditing reports
    
      - Configure Outlook Web App to allow XML attachments

## 감사 로그 내보내기

**규정 준수 관리** \> **감사** 페이지 관리자에서 내보내기 항목 감사 로그 및 사서함 감사 로그 및 (EAC)의 Exchange 관리 센터에서 검색할 수 있습니다.

  - **관리자 감사 로그 내보내기**   셸 cmdlet을 기반으로 하며 동사 **Get**, **Search**또는 **Test** 로 시작 하지는 관리자가 수행 된 모든 작업은 관리자 감사 로그에 기록 됩니다. 감사 로그 항목 실행 된 매개 변수 및 cmdlet을 사용 하 고 작업이 성공적으로 완료 하는 경우 사용 되는 값은 cmdlet이 포함 됩니다. 검색할 수 있으며 관리자 감사 로그에서 항목을 내보낼 수 있습니다. 검색 결과 내보낼 때 Microsoft Exchange XML 파일에 저장 하 고 전자 메일 메시지에 연결 합니다. 자세한 내용은 다음을 참조 합니다.
    
      - [역할 그룹 변경 내용을 검색 또는 관리자 감사 로그](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)
    
      - [보기 및 외부 관리자 감사 로그 내보내기](https://technet.microsoft.com/ko-kr/library/dn505728\(v=exchg.150\))
    

    > [!NOTE]
    > 기본적으로 관리자 감사 로그 항목은 90 일 동안 보관 됩니다. 90 일 보다 오래 된 항목이 때 삭제 됩니다. 클라우드 기반 조직에서이 설정을 변경할 수 없습니다. 그러나 변경할 수 있습니다는 온-프레미스 Exchange 조직에서 <STRONG>Set-AdminAuditLog</STRONG> cmdlet을 사용 하 여 합니다.



  - **사서함 감사 로그 내보내기**   사서함 감사 하는 경우 사서함에 대 한 로깅이 활성화 되는지, Microsoft Exchange 사서함 데이터에 대해 감사 되는 사서함의 숨겨진된 폴더에 저장 되는 사서함 감사 로그에 비 소유자가 수행한 작업에 대 한 레코드를 저장 합니다. 사서함 감사 로깅 소유자 작업 로그를 구성할 수도 있습니다. 이 로그의 항목에는 사서함에 액세스 한 사용자를 나타내는 경우, 작업을 수행 하 고 작업에 성공 했는지 여부와 편집 합니다. 에 대 한 검색 하는 경우의 사서함 감사 로그 항목과 내보내야, Microsoft Exchange 저장 검색 XML 파일에서 결과 전자 메일 메시지에 연결 합니다. 자세한 내용은 [사서함 감사 로그 내보내기](export-mailbox-audit-logs-exchange-2013-help.md)을 참조 하십시오.

## 감사 보고서 실행

EAC의 **감사** 페이지에서 다음 보고서 중 하나를 실행 하는 경우 결과 보고서의 세부 정보 창에 표시 됩니다.

  - **비 소유자 사서함 액세스 보고서 실행**   이 보고서를 사용 하 여 사서함을 소유한 사용자 이외의 사용자가 액세스 한 사서함을 검색 합니다. 자세한 내용은 [비 소유자 사서함 액세스 보고서 실행](run-a-non-owner-mailbox-access-report-exchange-online-help.md)을 참조 하십시오.

  - **관리자 역할 그룹 보고서 실행**   관리자 역할 그룹의 변경 내용을 검색하려면 이 보고서를 사용합니다. 자세한 내용은 [역할 그룹 변경 내용을 검색 또는 관리자 감사 로그](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)을 참조하십시오.

  - **원본 위치 검색 및 보관 보고서 실행**   원본 위치 유지에 추가되었거나 여기서 제거된 사서함을 찾으려면 이 보고서를 사용합니다. 자세한 내용은 다음을 참조하십시오.
    
      - [원본 위치 유지 및 소송 보존](in-place-hold-and-litigation-hold-exchange-2013-help.md)
    
      - [원본 위치 eDiscovery](in-place-ediscovery-exchange-2013-help.md)

  - **사서함 단위 소송 보존 보고서 실행**   이 보고서를 추가 또는 소송 보류에서 제거 된 사서함을 찾으려면을 사용 합니다. 자세한 내용은 다음을 참조 합니다.
    
      - [사서함 단위 소송 보존 보고서 실행](run-a-per-mailbox-litigation-hold-report-exchange-2013-help.md)
    
      - [전체 사서함에 소송 보존으로 설정](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - **관리자 감사 로그 보고서를 실행 합니다.**   이 보고서를 사용 하 여 관리자 감사 로그 항목을 볼 수 있습니다. 전자 메일 메시지로 수신 24 시간까지 걸릴 수 있습니다를 하는 관리자 감사 로그 내보내기 (영문) 하는 대신 EAC에서이 보고서를 실행할 수 있습니다. 이 보고서를 조직에서 관리자가 수행한 구성 변경 내용을 기록 합니다. 5000 항목 최대 여러 페이지에 표시할 수 됩니다. 검색 범위를 좁힐, 날짜 범위를 지정할 수 있습니다. 자세한 내용은 다음을 참조 합니다.
    
      - [관리자 감사 로그 보기](view-the-administrator-audit-log-exchange-2013-help.md)
    
      - [관리자 감사 로깅](administrator-audit-logging-exchange-2013-help.md)

  - **외부 관리자 감사 로그 보고서를 실행 합니다.**   이 보고서는 에서만 Exchange Online 및 Exchange Online Protection 사용할 수 있습니다. Microsoft 관리자가 작업 수행 또는 위임 된 관리자는 관리자 감사 로그에 기록 됩니다. 외부 관리자 감사 로그 보고서를 사용 하 여 검색 하 고 관리자가 조직 외부의 Exchange Online 조직 구성에 대해 수행 되는 작업을 확인 합니다. 자세한 내용은 [보기 및 외부 관리자 감사 로그 내보내기](https://technet.microsoft.com/ko-kr/library/dn505728\(v=exchg.150\))을 참조 하십시오.

## 감사 로깅 구성

감사 보고서를 실행하고 감사 로그를 내보내려면 조직에 대해 감사 로깅을 구성해야 합니다.

## 사서함 감사 로깅 사용

비소유자 사서함 액세스 보고서를 실행할 각 사서함에 대해 사서함 감사 로깅을 사용하도록 설정해야 합니다. 사서함에 대해 사서함 감사 로깅을 사용하도록 설정하지 않은 경우에는 보고서를 실행하거나 사서함 감사 로그를 내보낼 때 결과를 얻을 수 없습니다.

단일 사서함에 대해 사서함 감사 로깅을 사용하도록 설정하려면 셸에서 다음 명령을 실행합니다.

    Set-Mailbox <Identity> -AuditEnabled $true

조직의 모든 사용자 사서함에 대해 사서함 감사를 사용하도록 설정하려면 다음 명령을 실행합니다.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

동작이 로깅됩니다 구성 하는 방법에 대 한 자세한 내용은 다음을 참조 합니다.

  - **Exchange 2013**    [사서함 감사 사서함에 대해 로깅을 사용 하지 않도록 설정 하거나 사용](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)

  - **Exchange Online** Office 365의 감사 사서함 사용https://go.microsoft.com/fwlink/p/?LinkId=626109   

## 사용자에게 감사 보고서 액세스 권한 부여

기본적으로 관리자는 EAC의 감사 페이지에서 보고서에 액세스하고 보고서를 실행할 수 있습니다. 그러나 레코드 관리자, 법무 직원 등의 다른 사용자는 필요한 권한을 할당 받아야 합니다.

사용자가 액세스할 수 있도록 하는 것이 가장 편리 방법은 레코드 관리 역할 그룹에 추가 합니다. 사용자에 게 감사 로그 역할을 할당 하 여 EAC의 **감사** 페이지에 대 한 사용자 액세스를 제공 하려면 셸을 사용할 수도 있습니다.

## 레코드 관리 역할 그룹에 사용자 추가

1.  **사용 권한** \> **관리 역할**로 이동합니다.

2.  역할 그룹 목록에서 **레코드 관리**를 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **구성원** 아래에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **구성원 선택** 대화 상자에서 사용자를 선택합니다. 표시 이름의 일부 또는 전체를 입력하고 **검색**![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘")을 클릭하여 사용자를 검색할 수 있습니다. **이름** 또는 **표시 이름** 열 머리글을 클릭하여 목록을 정렬할 수도 있습니다.

5.  **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭한 다음 **확인**을 클릭하여 역할 그룹 페이지로 돌아갑니다.

6.  **저장**을 클릭하여 역할 그룹에 대한 변경 내용을 저장합니다.

세부 정보 창에서는 사용자가 **구성원** 아래에 나열되고 EAC의 감사 페이지에 액세스할 수 있으며, 감사 보고서를 실행하고 감사 로그를 내보낼 수 있습니다.

## 사용자에게 감사 로그 역할 할당

감사 로그 역할을 사용자에게 할당하려면 다음 명령을 실행합니다.

    New-ManagementRoleAssignment -Role "Audit Logs" -User <Identity>

이렇게 하면 사용자는 EAC에서 **규정 준수 관리** \> **감사**를 선택하여 보고서를 실행할 수 있습니다. 또한 사용자는 사서함 감사 로그를 내보낼 수 있으며 관리자 감사 로그를 내보내고 볼 수도 있습니다.


> [!NOTE]
> 사용자가 감사 보고서를 실행할 수만 있고 감사 로그를 내보낼 수는 없도록 하려면 앞의 명령을 사용하여 보기 전용 감사 로그 역할을 할당합니다.



## XML 첨부 파일을 허용하도록 Outlook Web App 구성

사서함 감사 로그나 관리자 감사 로그를 내보내면 XML 파일인 감사 로그가 전자 메일 메시지에 첨부됩니다. 그러나 Outlook Web App은 XML 첨부 파일을 기본적으로 차단합니다. Outlook Web App을 사용하여 이 감사 로그에 액세스하려면 XML 첨부 파일을 허용하도록 Outlook Web App을 구성해야 합니다.

Outlook Web App에서 XML 첨부 파일을 허용하려면 다음 명령을 실행합니다.

    Set-OwaMailboxPolicy -Identity Default -AllowedFileTypes '.rpmsg','.xlsx','.xlsm','.xlsb','.tiff','.pptx','.pptm','.ppsx','.ppsm','.docx','.docm','.zip','.xls','.wmv','.wma','.wav','.vsd','.txt','.tif','.rtf','.pub','.ppt','.png','.pdf','.one','.mp3','.jpg','.gif','.doc','.bmp','.avi','.xml'

