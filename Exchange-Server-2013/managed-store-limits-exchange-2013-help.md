---
title: '저장소 제한 관리: Exchange 2013 Help'
TOCTitle: 저장소 제한 관리
ms:assetid: bea9ec15-bfb5-4716-b14e-010e389c9f9e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt741981(v=EXCHG.150)
ms:contentKeyID: 73226012
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 저장소 제한 관리

 

_**마지막으로 수정된 항목:**2016-09-15_

**요약:** 관리 되는 저장소에 대 한 연결 제한 및 구성 하는 방법입니다.

Microsoft Exchange Server 2013, 연결 및 사용 현황 제한 관리 되는 저장소를 사용할 수 있는 모든 연결을 사용 하 여 단일 응용 프로그램 또는 단일 사용자를 방지 하기 위해 Exchange 관리 되는 저장소에 배치 된가 됩니다. 단일 사용자 또는 응용 프로그램의 모든 연결을 사용 하 여 허용 되는 경우에 다른 사용자 또는 응용 프로그램 가동 중지 시간에 발생할 수 있는 관리 되는 저장소에 액세스할 수 수 없습니다.


> [!NOTE]
> 관리자 권한이 있는 계정으로 설정 되는 모든 연결, 최대 세션 제한 개로 늘어났습니다 늘어났습니다.



## 용어

다음 용어에 대 한 지식에는이 항목에서 참조 하는 연결의 종류를 이해 하는데 도움이 됩니다.

  - 세션  
    세션 관리 되는 저장소에 연결할 서비스 및 Microsoft Outlook, 등의 클라이언트 응용 프로그램에서 사용 하는 연결을 나타냅니다. 서비스와 클라이언트를 특정 시간에 여러 세션을 가질 수 있습니다. 용어 *연결* 및 *세션* 를 바꾸어 사용할 수 있습니다.

<!-- end list -->

  - 스레드 수  
    스레드는 관리 되는 저장소에 동시에 실행 되는 요청을 나타냅니다. 예, 사용자가 Outlook 에 폴더를 열, Outlook 사용자를 대신 하 여 관리 되는 저장소에 요청을 실행 합니다. 요청을 실행 하는 단일 스레드입니다.
    
    Exchange Server 2013 스레드 한도 기반 클라이언트 유형으로 구분 됩니다. 대신, 모든 클라이언트에 대 한 **사서함 데이터베이스 당** 스레드 수의 최대 수는 50 합니다. 예외는 사용자 당 16의 최대 제한 하는 가용성 서비스입니다.

맨 위로 이동

## 세션 제한

다음 표에서 관리 되는 저장소 및 해당 연결에 따라 제한에 대 한 클라이언트 연결의 목록을 표시 합니다. 세션 제한을 수정 하려는 경우 "세션 제한 구성" 바로 다음 표에를 참조 하십시오.

이전 버전의 Exchange 서버당 연결 수에 따라 관리 되는 저장소에 대 한 연결 수에 대 한도 설정 합니다. Exchange 2013, 세션 제한 기반으로 사서함 데이터베이스당 연결 합니다.

연결 제한 유형의 Exchange 2013는 다음과 같습니다.

  - **프로세스당 최대 세션**   Exchange 서비스 사서함 데이터베이스에서 한번에 열을 가질 수 있다는 세션의 최대 수를 지정 합니다.

  - **프로세스당 최대 사용자 세션**   단일 사용자에 대 한 특정 프로토콜에 대 한 세션의 최대 수를 지정 합니다.

"세션 제한 구성" 섹션에는 이러한 한도 수정 하는 방법을 설명 합니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>클라이언트 유형</th>
<th> </th>
<th>사서함 데이터베이스 당 최대 세션</th>
<th>기본 사서함 데이터베이스당 사용자 세션 수</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>관리자</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>가용성 서비스</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>콘텐츠 인덱싱</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td> </td>
<td><p>해당 없음</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 웹 서비스</p></td>
<td> </td>
<td><p>해당 없음</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>관리</p></td>
<td> </td>
<td><p>해당 없음</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>중간 계층 (MoMT)에서 MAPI</p></td>
<td> </td>
<td><p>해당 없음</p></td>
<td><p>32</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants: 이벤트</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxAssistants: 시간이 초과 되었습니다</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 원격 프로시저 호출</p></td>
<td> </td>
<td><p>해당 없음</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office Outlook Web App</p></td>
<td> </td>
<td><p>해당 없음</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>POP3 및 IMAP4</p></td>
<td> </td>
<td><p>해당 없음</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>전송</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>통합 메시징</p></td>
<td> </td>
<td><p>해당 없음</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>다른 사용자에 게</p></td>
<td> </td>
<td><p>해당 없음</p></td>
<td><p>16</p></td>
</tr>
</tbody>
</table>


## 세션 제한 구성

기본 세션 제한 값을 수정할 수 있습니다.


> [!NOTE]
> 세션 제한을 수정 하려는 모든 데이터베이스 가용성 그룹 (Dag) 내에서 모든 사서함 서버에서이 수정 해야. 모든 서버에서 같은 변경 작업을 지정 하지 않는, 결과 일관 됩니다. 클라이언트 액세스 서버에서 세션 한계를 늘리려면 <CODE>RCAMaxConcurrency</CODE> 값 제한 정책에서 늘려야 합니다. 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/dd298094(v=exchg.150)">Set-ThrottlingPolicy</A>을 참조 하십시오.




> [!WARNING]
> 레지스트리를 잘못 편집하면 운영 체제를 다시 설치해야 할 수 있는 심각한 문제가 발생할 수 있습니다. 잘못된 레지스트리 편집으로 인한 문제는 해결하지 못할 수도 있습니다. 레지스트리를 편집하기 전에 중요한 데이터를 백업해 두십시오.



1.  레지스트리 편집기(regedit)를 시작합니다.

2.  다음 레지스트리 하위 키로 이동 합니다.
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem** 합니다.

3.  **ParametersSystem** 를 마우스 오른쪽 단추로 클릭 하 고 **새로** 만들기를 가리킨 다음 클릭 **DWORD (32 비트) 값.**
    
    결과 창에서 새 값을 만들어집니다.

4.  다음 값 중 하나로 키 이름을 바꾼 다음 Enter 키를 누릅니다.
    
      - **사용자 당 최대 허용 된 세션**   이 제한은 사용자 당 허용 되는 최대 세션 수를 지정합니다.
    
      - **사용자 당 최대 허용 된 서비스 세션**   이 제한은 사용자 당 최대 허용 된 서비스 세션을 지정합니다.
    
      - **서비스 당 최대 허용된 Exchange 세션**   이 제한은 서비스 당 Exchange 세션을 허용 된 최대 길이 지정 합니다. 기본값은 10, 000입니다.

5.  새로 만든된 키를 마우스 오른쪽 단추로 클릭 하 고 한 다음 **수정** 을 클릭 합니다.

6.  **값** **데이터** 상자에서이 항목을 제한 하려면 개체의 수를 입력 한 다음 **확인** 을 클릭 합니다. 위 표를 사용 하 여 기본 설정을 볼 수 있습니다.

맨 위로 이동

## 항목 열기 제한

항목 열기 제한 단일 세션에서 단일 사서함에서 열 수 있는 항목 수에 대 한 제한 사항 중 있습니다. 그러나 사용자를 동시에 열 여러 세션을 가질 수 있습니다. 예는 사용자가 연 두 세션을 사용 하는 경우 사용자 1, 000 폴더를 열 수 있습니다.

이러한 한도 수정 하려는 경우 "제한 구성 참조 열기 항목" 바로 다음 표에 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>항목 종류</th>
<th>레지스트리 개체 유형</th>
<th>최대 세션 당 열</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ACL 보기</p></td>
<td><p>objtACLView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Attachment</p></td>
<td><p>objtAttachment</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>첨부 파일 보기</p></td>
<td><p>objtAttachmentView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>CStream</p></td>
<td><p>objtCStream</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>폴더</p></td>
<td><p>objtFolder</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>폴더 보기</p></td>
<td><p>objtFolderView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>FX 대상 스트림</p></td>
<td><p>objtFXDstStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>FX 원본 스트림</p></td>
<td><p>objtFXSrcStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>메시지</p></td>
<td><p>objtMessage</p></td>
<td><p>250</p></td>
</tr>
<tr class="even">
<td><p>메시지 보기</p></td>
<td><p>objtMessageView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>알림</p></td>
<td><p>objtNotify</p></td>
<td><p>500,000</p></td>
</tr>
<tr class="even">
<td><p>규칙 보기</p></td>
<td><p>objtRulesView</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>스트림</p></td>
<td><p>objtStream</p></td>
<td><p>250</p></td>
</tr>
</tbody>
</table>


## 항목 열기 제한 구성

MAPI 클라이언트를 동시에 사용할 수 있는 자원의 최대 수를 제한할 수 있습니다.


> [!NOTE]
> 항목 열기 한도 수정 하려는 경우 모든 Dag 및 클라이언트 액세스 배열 내에서 모든 사서함 서버에서이 수정 해야 합니다. 모든 서버에서 같은 변경 작업을 지정 하지 않는, 결과 일관 됩니다.




> [!WARNING]
> 레지스트리를 잘못 편집하면 운영 체제를 다시 설치해야 할 수 있는 심각한 문제가 발생할 수 있습니다. 잘못된 레지스트리 편집으로 인한 문제는 해결하지 못할 수도 있습니다. 레지스트리를 편집하기 전에 중요한 데이터를 백업해 두십시오.



1.  레지스트리 편집기(regedit)를 시작합니다.

2.  다음 레지스트리 하위 키로 이동 합니다.
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**

3.  **ParametersSystem**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.
    
    새 키의 콘솔 트리에서에 만들어집니다.

4.  **MaxObjsPerMapiSession** 키 이름을 바꾸고 Enter 키를 누릅니다.

5.  **MaxObjsPerMapiSession** 를 마우스 오른쪽 단추로 클릭 하 고 **새로** 만들기를 가리킨 다음 **DWORD (32 비트) 값** 을 클릭 합니다.
    
    결과 창에서 새 값을 만들어집니다.

6.  *\<Object\_type\>*, 여기서 *\<Object\_type\>* 는 수정 하려는 레지스트리 개체 형식의 이름을 키를 이름을 바꿉니다. 예 열 수 있는 메시지 수를 수정 하려면 *objtMessage*를 사용 합니다. Enter 키를 누릅니다.

7.  새로 만든된 키를 마우스 오른쪽 단추로 클릭 하 고 한 다음 **수정** 을 클릭 합니다.

8.  **값 데이터** 상자에서이 항목을 제한 하려면 개체의 수를 입력 한 다음 **확인** 을 클릭 합니다. 예, **350** 개체에 대 한 값을 높일 수를 입력 합니다.

9.  Microsoft Exchange 정보 저장소 서비스를 다시 시작 합니다.

맨 위로 이동

## 항목 크기 제한

항목 크기 제한은 사용자의 사서함 내의 항목에 배치 하는 제한 합니다. 이러한는 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) cmdlet에서 *MaxSendSize* 및 *MaxReceiveSize* 매개 변수를 사용 하 여 구성할 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>항목 종류</th>
<th>제한</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>메시지 (저장)</p></td>
<td><p>SendLimit, ReceiveLimit의 최대 크기</p></td>
</tr>
<tr class="even">
<td><p>메시지 (전송)</p></td>
<td><p>SendLimit의 최대 크기</p></td>
</tr>
<tr class="odd">
<td> </td>
<td> </td>
</tr>
</tbody>
</table>


맨 위로 이동

