---
title: '사서함 감사 로그 내보내기: Exchange 2013 Help'
TOCTitle: 사서함 감사 로그 내보내기
ms:assetid: b458a95a-3321-4647-8884-cf97f8e7186a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150552(v=EXCHG.150)
ms:contentKeyID: 50482285
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 감사 로그 내보내기

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

사서함에 대해 사서함 감사를 사용하도록 설정하면 소유자 이외의 사용자가 해당 사서함에 액세스할 때마다 *사서함 감사 로그*에 정보가 기록됩니다. 각각의 로그 항목에는 사서함에 액세스한 사람 소유자가 아닌 사람이 수행한 작업과 작업 시기 및 작업이 성공했는지 여부에 대한 정보가 포함됩니다. 사서함 감사 로그의 항목은 기본적으로 90일 동안 유지됩니다. 사서함 감사 로그를 사용하여 소유자 이외의 사용자가 사서함에 액세스했는지 여부를 확인할 수 있습니다.

사서함 감사 로그의 항목을 내보내면 항목이 XML 파일로 저장되고 해당 파일이 지정된 받는 사람에게 보내는 전자 메일 메시지에 첨부됩니다.

**목차**

시작하기 전에

사서함 감사 로깅 구성

사서함 감사 로그 내보내기

사서함 감사 로그 보기

추가 정보

## 시작하기 전에

  - 각 절차의 예상 완료 시간: 시간은 가변적입니다. Exchange Online에서 사서함 감사 로그는 내보낸 후 며칠 이내에 보내집니다.

  - Exchange Online 이 항목의 다양 한 절차를 수행 하려면 원격 Windows PowerShell을 사용 해야 합니다. 자세한 내용은 [원격 PowerShell을 사용하여 Exchange Online에 연결](https://technet.microsoft.com/ko-kr/library/jj984289\(v=exchg.150\))를 참조 합니다.

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 사서함 감사 로깅 구성

사서함 감사 로그를 내보내고 보려면 감사할 각 사서함에 대해 사서함 감사 로깅을 사용하도록 설정해야 합니다. 또한 Microsoft Outlook Web App를 사용하여 감사 로그에 액세스하려면 Outlook Web App가 XML 첨부 파일을 허용하도록 구성해야 합니다.

## 1단계: 사서함 감사 로깅 사용

비소유자 사서함 액세스 보고서를 실행할 각 사서함에 대해 사서함 감사 로깅을 사용하도록 설정해야 합니다. 사서함에서 사서함 감사 로깅을 사용하지 않으면 사서함 감사 로그를 내보낼 때 해당 사서함에 대한 결과를 얻을 수 없습니다.

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "사서함 감사 로깅" 항목

단일 사서함에서 사서함 감사 로깅을 사용하도록 설정하려면 셸에서 명령을 실행합니다.

    Set-Mailbox <Identity> -AuditEnabled $true

조직의 모든 사용자 사서함에서 사서함 감사 로깅을 사용하도록 설정하려면 다음 명령을 실행합니다.

```
$UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
```

```
$UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}
```

## 2단계: XML 첨부 파일을 허용하도록 Outlook Web App 구성

사서함 감사 로그를 내보내면 XML 파일인 감사 로그가 전자 메일 메시지에 첨부됩니다. 그러나 Outlook Web App는 XML 첨부 파일을 기본적으로 차단합니다. 내보낸 감사 로그에 액세스하려면 Microsoft Outlook을 사용하거나 Outlook Web App가 XML 첨부 파일을 허용하도록 구성해야 합니다.

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "Outlook Web App 사서함 정책" 항목

Outlook Web App 에서 XML 첨부 파일을 허용 하려면 다음 절차를 수행 합니다. Exchange Server 2013*Identity* 매개 변수에 대 한 `Default` 값 사용 합니다.

1.  XML Outlook Web App 에서 허용 되는 파일 형식 목록에 추가 하려면 다음 명령을 실행 합니다.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -AllowedFileTypes @{add='.xml'}

2.  Outlook Web App 에서 차단 된 파일 형식 목록에서 XML을 제거 하려면 다음 명령을 실행 합니다.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -BlockedFileTypes @{remove='.xml'}

## 작동 여부는 어떻게 확인합니까?

사서함 감사 로깅이 성공적으로 구성되었는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행하여 사서함에 대해 감사 로깅이 구성되어 있는지 확인합니다.
    
        Get-Mailbox | FL Name,AuditEnabled
    
    *AuditEnabled* 속성의 `True` 값은 감사 로깅이 사용하도록 설정되었는지 확인합니다.

2.  Outlook Web App 에서 XML 첨부 파일이 허용 되는지 확인 하려면 다음 명령을 실행 합니다.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty AllowedFileTypes
    
    `.xml`이 허용되는 파일 형식 목록에 포함되어 있는지 확인합니다.

3.  Outlook Web App 에서 차단 된 파일 목록에서 XML 첨부 파일을 제거 했는지 확인 하려면 다음 명령을 실행 합니다.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty BlockedFileTypes
    
    확인 해당 `.xml` 차단 된 파일 형식 목록에 포함 되지 않습니다.

맨 위로 이동

## 사서함 감사 로그 내보내기

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "관리자 감사 로깅만 보기" 항목

1.  (EAC)의 Exchange 관리 센터에서 이동 **규정 준수** 관리 \> **감사** 합니다.

2.  **사서함 감사 로그 내보내기**를 클릭합니다.

3.  사서함 감사 로그에서 항목을 내보내기 위한 다음 검색 조건을 구성합니다.
    
      - **시작 날짜 및 종료 날짜**   내보낸 파일에 포함할 항목의 날짜 범위를 선택합니다.
    
      - **감사 로그를 검색할 사서함**   감사 로그 항목을 검색할 사서함을 선택합니다.
    
      - **비소유자 액세스 유형**   항목을 검색할 비소유자 액세스 유형을 정의하려면 다음 옵션 중 하나를 선택합니다.
        
          - **모든 비소유자**   조직 내의 관리자 및 위임된 사용자 액세스와 Exchange Online의 Microsoft 데이터 센터 관리자 액세스를 검색합니다.
        
          - **외부 사용자**   Microsoft 데이터 센터 관리자 액세스만 검색합니다.
        
          - **관리자 및 위임된 사용자**   조직 내의 관리자 및 위임된 사용자 액세스를 검색합니다.
        
          - **관리자**   조직 내의 관리자 액세스를 검색합니다.
    
      - **받는 사람**   사서함 감사 로그를 보낼 사용자를 선택합니다.

4.  **내보내기**를 클릭합니다.
    
    사서함 감사 로그에서 검색 조건을 충족하는 항목이 검색되어 SearchResult.xml이라는 파일에 저장된 다음 이 XML 파일이 지정한 받는 사람에게 보내는 전자 메일 메시지에 첨부됩니다.

## 작동 여부는 어떻게 확인합니까?

사서함 감사 로그를 보낸 하는 사서함에 로그인 합니다. 성공적으로 내보낸 감사 로그를 하는 경우 Exchange에서 보내는 메시지를 받게 됩니다. Exchange Online 이 메시지를 받으려면 며칠 걸릴 수 있습니다. 사서함 감사 로그 (SearchResult.xml 라는)이이 메시지에 첨부 됩니다. XML 첨부 파일을 허용 하도록 Outlook Web App 올바르게 구성 하는 경우에 연결 된 XML 파일을 다운로드할 수 있습니다.

맨 위로 이동

## 사서함 감사 로그 보기

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)의 "관리자 감사 로깅만 보기" 항목

저장 하 고 SearchResult.xml 파일을 봅니다.

1.  사서함 감사 로그를 보낸 사서함에 로그인합니다.

2.  받은 편지함에서 Microsoft Exchange에서 보낸 XML 첨부 파일이 포함된 메시지를 엽니다. 전자 메일 메시지의 본문에 검색 조건이 포함되어 있습니다.

3.  첨부 파일을 클릭 하 고 XML 파일을 다운로드 하려면 선택 합니다.

4.  다음은 Microsoft Excel에서의 SearchResult.xml를 엽니다.

맨 위로 이동

## 추가 정보

  - **감사 로그는 사서함의 항목**   다음 예제에서는 SearchResult.xml 파일에 포함 된 사서함 감사 로그에서 항목을 표시 합니다. 각 항목 앞에 **\< 이벤트 \>** XML 태그와으로 끝나는 **\< / 이벤트 \>** XML 태그입니다. 이 항목에서는 관리자가 "**소송 보존에 대 한 알림을 유지**" David의 사서함에서 복구 가능한 항목 폴더에서 2010 년 4 월 30 일에 제목와 메시지를 제거 하는 보여줍니다.
    
        <Event MailboxGuid="6d4fbdae-e3ae-4530-8d0b-f62a14687939" 
          Owner="PPLNSL-dom\david50001-1363917750" 
          LastAccessed="2010-04-30T11:01:55.140625-07:00" 
          Operation="HardDelete" 
          OperationResult="Succeeded" 
          LogonType="Admin"
         FolderId="0000000073098C3277988F4CB882F5B82EBF64610100A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000"
          FolderPathName="\Recoverable Items\Deletions"
          ClientInfoString="Client=OWA;Action=ViaProxy" 
          ClientIPAddress="10.196.241.168" 
          InternalLogonType="Owner"
          MailboxOwnerUPN="david@contoso.com"
          MailboxOwnerSid="S-1-5-21-290112810-296651436-1966561949-1151" 
          CrossMailboxOperation="false" 
          LogonUserDN="Administrator"
          LogonUserSid="S-1-5-21-290112810-296651436-1966561949-1149">
          <SourceItems>
           <ItemId="0000000073098C3277988F4CB882F5B82EBF64610700A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000A7C317F68C24304BBD18ABE1F185E79B00000026BD540"
            Subject="Notification of litigation hold"
            FolderPathName="\Recoverable Items\Deletions" /> 
          </SourceItems>
        </Event>

  - **감사 로그의 사서함에서 유용한 필드**   사서함 감사 로그의 유용한 필드에 대 한 설명은 다음과 같습니다. 이러한 사서함의 비 소유자 액세스의 각 인스턴스에 대 한 특정 정보를 확인할 수 있습니다.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>필드</th>
    <th>설명</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Owner</strong></p></td>
    <td><p>비소유자가 액세스한 사서함의 소유자입니다.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>LastAccessed</strong></p></td>
    <td><p>사서함에 액세스한 날짜와 시간입니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Operation</strong></p></td>
    <td><p>비소유자가 수행한 작업입니다. 자세한 내용은 <a href="https://technet.microsoft.com/ko-kr/library/jj156300(v=exchg.150)">비 소유자 사서함 액세스 보고서를 실행 하는 방법에 대 한 자세한 내용은</a>의 &quot;사서함 감사 로그에는 무엇이 기록됩니까?&quot; 섹션을 참조하십시오.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OperationResult</strong></p></td>
    <td><p>비소유자가 수행한 작업이 성공했는지 여부입니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonType</strong></p></td>
    <td><p>비소유자 액세스의 유형입니다. 여기에는 administrator, delegate 및 external이 포함됩니다.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>FolderPathName</strong></p></td>
    <td><p>비소유자의 영향을 받는 메시지가 포함된 폴더의 이름입니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>ClientInfoString</strong></p></td>
    <td><p>비소유자가 사서함에 액세스하기 위해 사용하는 메일 클라이언트에 대한 정보입니다.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ClientIPAddress</strong></p></td>
    <td><p>비소유자가 사서함에 액세스하기 위해 사용하는 컴퓨터의 IP 주소입니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>InternalLogonType</strong></p></td>
    <td><p>비소유자가 이 사서함에 액세스하기 위해 사용하는 계정의 로그온 유형입니다.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>MailboxOwnerUPN</strong></p></td>
    <td><p>사서함 소유자의 전자 메일 주소입니다.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonUserDN</strong></p></td>
    <td><p>비소유자의 표시 이름입니다.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Subject</strong></p></td>
    <td><p>비소유자의 영향을 받는 전자 메일 메시지의 제목 줄입니다.</p></td>
    </tr>
    </tbody>
    </table>
    
    맨 위로 이동

