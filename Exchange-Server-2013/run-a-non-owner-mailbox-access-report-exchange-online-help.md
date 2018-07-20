---
title: '비 소유자 사서함 액세스 보고서 실행: Exchange 2013 Help'
TOCTitle: 비 소유자 사서함 액세스 보고서 실행
ms:assetid: dbbef170-e726-4735-abf1-2857db9bb52d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150575(v=EXCHG.150)
ms:contentKeyID: 50482352
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 비 소유자 사서함 액세스 보고서 실행

 

_**적용 대상:** Exchange Online_

_**마지막으로 수정된 항목:** 2016-12-09_

비 소유자 사서함 액세스 보고서는 Exchange 관리 센터 (EAC)에서 사서함을 소유한 사용자 이외의 사용자가 액세스 한 사서함을 나열 합니다. 비 소유자가 사서함에 액세스할 때 Microsoft Exchange를 전자 메일 메시지로 감사 되는 사서함에서 숨겨진된 폴더에 저장 된 사서함 감사 로그에이 작업을이 수행 하는 방법에 대 한 정보를 기록 합니다. 이 로그 항목 검색 결과로 표시 되 고 포함 소유자가 아닌, 사서함에 액세스 한 사용자 및 비 소유자가 작업을 수행 하는 경우, 하 여 액세스 하는 사서함의 목록 작업에 성공 했는지 여부 및 합니다. 기본적으로 사서함 감사 로그의 항목에는 90 일 동안 보관 됩니다.

때 사서함 감사 비 소유자, 관리자 및 *위임 사용자*를 호출, 사서함에 사용 권한을 할당 된 사용자를 모두 포함 하 여 로그 특정 작업을 Microsoft Exchange 사서함에 대해 로깅을 사용 하도록 설정 합니다. 도 내부 또는 조직 외부의 사용자에 게 검색 범위를 좁힐 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "사서함 감사 로깅" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 사서함 감사 로깅 사용

사서함 감사에 대 한 비 소유자 사서함 액세스 보고서를 실행 하려는 각 사서함에 대 한 로깅을 사용 하도록 설정 해야 합니다. 사서함 감사 로깅 설정 되지 않은 면 보고서를 실행 하는 경우에 모든 결과 가져올 되지 않습니다.

단일 사서함에 대 한 로깅 사서함 감사를 사용 하도록 설정 하려면 다음 셸 명령을 실행 합니다.

    Set-Mailbox <Identity> -AuditEnabled $true

예, 이강주 이라는 사용자에 대 한 사서함 감사를 사용 하도록 설정 하려면 다음 명령을 실행 합니다.

    Set-Mailbox "Florence Flipo" -AuditEnabled $true

조직의 모든 사용자 사서함에 대해 사서함 감사를 사용하도록 설정하려면 다음 명령을 실행합니다.

```
$UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
```

```
$UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}
```

## 작동 여부는 어떻게 확인합니까?

사서함을 성공적으로 구성 했는지 확인 하려면 다음 명령을 실행 감사 로깅 합니다.

    Get-Mailbox | FL Name,AuditEnabled

*AuditEnabled* 속성의 `True` 값은 감사 로깅이 사용하도록 설정되었는지 확인합니다.

맨위로 돌아가기

## 비 소유자 사서함 액세스 보고서 실행

1.  EAC에서 **준수 관리** \> **감사**로 이동합니다.

2.  **비 소유자 사서함 액세스 보고서 실행** 을 클릭 합니다.
    
    기본적으로 Microsoft Exchange에서 지난 2 주 동안 조직의 모든 사서함에 비 소유자 액세스에 대 한 보고서를 실행합니다. 사서함에 대해 활성화 된 검색 결과에 나열 된 사서함 감사 로깅.

3.  특정 사서함에 대 한 비 소유자 액세스를 보려면 사서함 목록에서 사서함을 선택 합니다. 세부 정보 창에서 검색 결과 봅니다.


> [!TIP]
> 검색 결과를 좁히려면 시작 날짜, 종료 날짜 또는 둘 다를 선택하고 검색할 특정 사서함을 선택합니다. <STRONG>검색</STRONG>을 클릭하여 보고서를 다시 실행합니다.



## 특정 유형의 비 소유자 액세스에 대 한 검색

또한 사용자의 로그온 유형을 검색 하려면이 라고도 하는 비 소유자 액세스 유형을 지정할 수 있습니다. 다음은 옵션입니다.

  - **모든 비 소유자**    관리자 및 위임 된 사용자 조직 내에서 액세스에 대 한 검색 합니다. 또한 조직 외부에 있는 액세스 사용자를 포함합니다.

  - **외부 사용자**    조직 외부의 사용자 액세스를 검색 합니다.

  - **관리자 및 위임된 사용자**   조직 내의 관리자 및 위임된 사용자 액세스를 검색합니다.

  - **관리자**   조직 내의 관리자 액세스를 검색합니다.

맨위로 돌아가기

## 작동 여부는 어떻게 확인합니까?

비 소유자 사서함 액세스 보고서를 실행 하 고 성공적으로 했을 때 있는지를 확인 하려면 검색 결과 창을 확인 합니다. 사서함에 대 한 보고서를 실행 하는이 창에 표시 됩니다. 특정 사서함에 대 한 결과 없는 경우에 비 소유자 액세스 또는 비 소유자 액세스 지정된 된 날짜 범위 내에서 전체 하지 않은 발생 시 키 지 않은 가능한 합니다. 앞에서 설명한 대로 감사 로깅 비 소유자 액세스에 대 한 검색 하려는 사서함에 대해 활성화 된 되었는지 확인 해야 합니다.

맨위로 돌아가기

## 사서함 감사 로그에 기록 가져옵니다 무엇입니까?

비 소유자 사서함 액세스 보고서를 실행 하는 경우에 사서함 감사 로그 항목 EAC에서 검색 결과에 표시 됩니다. 각 보고서 항목이 정보가 표시 됩니다.

  - 사서함에 액세스 한 사용자 및 사용 해야하는 경우

  - 비 소유자가 수행한 작업

  - 영향을 받는 메시지와 해당 폴더 위치

  - 작업이 성공 했는지 여부

다음 표에서 수행 하는 작업이 비 소유자 사서함으로 기록 될 수 있는 감사 로깅. 테이블에서 **예** 나타내며 해당 로그온 형식에 대 한 작업을 로깅할 수 있습니다 **No** 나타냅니다 동작을 기록할 수 없습니다. 별표 (**\***) 동작 기록한 나타냅니다 사서함 감사 로깅 때 기본적으로는 사서함에 대해 활성화 되어 합니다. 기본적으로 기록 되지 않은 작업을 추적 하려면 PowerShell을 사용 하 여 해당 작업의 로깅을 사용 하도록 설정 해야 합니다.


> [!NOTE]
> 관리자에 게 사용자의 사서함에 대 한 전체 액세스 권한을 할당 된 위임 된 사용자로 간주 됩니다.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>작업</th>
<th>설명</th>
<th>관리자</th>
<th>위임 된 사용자</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>복사</strong></p></td>
<td><p>메시지가 다른 폴더에 복사되었습니다.</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p><strong>만들기</strong></p></td>
<td><p>항목이 사서함의 일정, 연락처, 메모 또는 작업 폴더에 만들어집니다. 예를 들면 새 모임 요청이 만들어집니다. 메시지나 폴더 만들기는 감사되지 않습니다.</p></td>
<td><p>예*</p></td>
<td><p>예*</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderBind</strong></p></td>
<td><p>사서함 폴더가 액세스 되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p><strong>영구 삭제</strong></p></td>
<td><p>메시지가 복구 가능한 항목 폴더에서 제거되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예*</p></td>
</tr>
<tr class="odd">
<td><p><strong>MessageBind</strong></p></td>
<td><p>메시지가 미리 보기 창에 표시되거나 열렸습니다.</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p><strong>이동</strong></p></td>
<td><p>메시지가 다른 폴더로 이동했습니다.</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p><strong>삭제 된 항목으로 이동</strong></p></td>
<td><p>메시지가 지운 편지함 폴더로 이동했습니다.</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p><strong>다른 사람 이름으로 보내기</strong></p></td>
<td><p>메시지가 SendAs 권한을 사용하여 전송되었습니다. 즉, 사서함 소유자가 보낸 것처럼 보이도록 하여 다른 사용자가 메시지를 보냈습니다.</p></td>
<td><p>예*</p></td>
<td><p>예*</p></td>
</tr>
<tr class="odd">
<td><p><strong>대신 보내기</strong></p></td>
<td><p>메시지가 SendOnBehalf 권한을 사용하여 전송되었습니다. 즉, 다른 사용자가 사서함 소유자 대신에 메시지를 보냈습니다. 받는 사람은 메시지가 대신 전송된 사용자와 메시지를 실제로 보낸 사용자를 메시지에서 확인할 수 있습니다.</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p><strong>일시 삭제</strong></p></td>
<td><p>메시지가 지운 편지함 폴더에서 삭제되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예*</p></td>
</tr>
<tr class="odd">
<td><p><strong>업데이트</strong></p></td>
<td><p>메시지가 변경되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예*</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> *&nbsp; 사서함에 대해 감사가 사용되는 경우 기본적으로 감사됩니다.



맨위로 돌아가기

