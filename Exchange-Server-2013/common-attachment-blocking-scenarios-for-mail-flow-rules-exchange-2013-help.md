---
title: '일반적인 첨부 파일 차단 시나리오: Exchange 2013 Help'
TOCTitle: 일반적인 첨부 파일 차단 시나리오
ms:assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn950026(v=EXCHG.150)
ms:contentKeyID: 65210913
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 일반적인 첨부 파일 차단 시나리오

 

_**적용 대상:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-02-23_

특정 유형의 메시지 차단 되거나 거부 법률 또는 규정 준수 요구 사항을 충족 하기 위해 또는 특정 비즈니스 요구를 구현 하는 조직 필요할 수 있습니다. Exchange 에서 전송 규칙을 사용 하 여 설정할 수 있는 모든 첨부 파일을 차단 하기 위한 일반적인 시나리오에 대 한 예가 다음과 같습니다.

  -  예 1:, 첨부 파일이 있는 메시지를 차단 하 고 보낸사람에 게 알리기

  -  예 2: 알림 인바운드 메시지가 차단 되는 경우 받는 사람에 게 대상

  -  알림 제목 줄을 수정 하는 예제 3:

  -  시간 제한 규칙을 적용 하는 예제 4:

다른 특정 첨부 파일을 차단 하는 방법을 보여주는 예제를 보려면 다음을 참조 합니다.

  - [전송 규칙을 사용 하 여 메시지 첨부 파일을 검사 하려면](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013)

  - [메일 흐름 규칙을 사용 하 여 Office 365의 메시지 첨부 파일을 검사 하려면](https://technet.microsoft.com/ko-kr/library/jj919236\(v=exchg.150\)) (Exchange Online, Exchange Online Protection)

맬웨어 필터 공용 첨부 파일 형식 필터를 포함합니다. Exchange 관리 센터 (EAC), **보호** 이동 하 고 **새로 만들기** (![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")) 필터를 추가 하려면를 클릭 합니다. Exchange Online 포털에서 **보호** 이동 하 고 **맬웨어 필터** 를 선택 합니다.

특정 메시지 형식을 차단 하도록 이러한 시나리오 중 하나를 구현을 시작 하기:

1.  Exchange 관리 센터 에 로그인 합니다.

2.  **메일 흐름** 으로 이동 \>**규칙** 입니다.

3.  **새로 만들기** (![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")) 를클릭하고 **새 규칙 만들기** 를 선택 합니다.

4.  **이름** 상자에는 규칙에 대 한 이름을 지정 하 고 **기타 옵션** 을 클릭 합니다.

5.  조건 및 동작을 선택 합니다.

**참고:**  EAC를 입력할 수 있는 가장 작은 첨부 파일 크기는 대부분 첨부 파일을 검색 해야 하는 1kb입니다. 그러나 모든 규모의 가능한 모든 첨부 파일을 검색 하려면 PowerShell을 사용 하 여 EAC의 규칙을 만든 후에 1 바이트를 첨부 파일 크기를 조정 해야 합니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요. Windows PowerShell을 사용하여 Exchange Online에 연결하는 방법을 알아보려면 [Exchange Online PowerShell에 연결](https://go.microsoft.com/fwlink/p/?linkid=396554)을 참조하세요. Windows PowerShell을 사용하여 Exchange Online Protection에 연결하는 방법을 알아보려면 [Exchange Online Protection PowerShell에 연결](https://go.microsoft.com/fwlink/p/?linkid=627290)을 참조하세요.

*\<Rule Name\>* 기존 규칙의 이름을 바꿉니다 하 고 1 바이트를 첨부 파일 크기를 설정 하려면 다음 명령을 실행 합니다.

    Set-TransportRule -Identity "<Rule Name>" -AttachmentSizeOver 1B

1 바이트를 첨부 파일 크기를 조정한 후 EAC의 규칙에 대해 표시 되는 값은 **0.00 KB**.

## 예 1:, 첨부 파일이 있는 메시지를 차단 하 고 보낸사람에 게 알리기

첨부 파일을 주고받을를 조직에서 사람들이 않으려면 첨부 파일이 있는 모든 메시지를 차단 하는 전송 규칙을 설정할 수 있습니다.

이 예제에서는 첨부 파일이 있는 조직에서 주고받은 모든 메시지가 차단 됩니다.

![모든 첨부 파일을 차단하는 규칙](images/Dn950026.38094183-166f-4ba5-a9cf-242e7d0f4e04(EXCHG.150).png "모든 첨부 파일을 차단하는 규칙")

메시지 블록만 수행 하려는 경우에이 규칙이 일치 하는 규칙 처리를 중지 하는 것이 좋습니다. 규칙 대화 상자에서 아래로 스크롤하고 **추가 규칙 처리 중지** 확인란을 선택 합니다.

## 예 2: 알림 인바운드 메시지가 차단 되 면 받는 사람을 위한

메시지를 거부 하지만 셰이프시트에서 변경 된 알고 의도 한 수신자에 게 하려는 경우 **메시지와 함께 받는 사람에 게 알림** 동작을 사용할 수 있습니다.

원본 메시지에 대 한 정보 포함 되도록 알림 메시지에서 자리 표시자를 포함할 수 있습니다. 자리 표시자 두 백분율 기호 (%), 묶어야 합니다 하 고 원본 메시지의 정보로 자리 표시자는 알림 메시지를 보낼 때 키를 누릅니다. \< B r \>와 같은 기본 HTML을 사용할 수도 있습니다 \< b \> \< i \> 및 \< img \> 메시지에 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>이러한 유형의 정보</strong></p></td>
<td><p><strong>개체 틀</strong></p></td>
</tr>
<tr class="even">
<td><p>메시지를 보낸 사람이 합니다.</p></td>
<td><p>% %에서 % %</p></td>
</tr>
<tr class="odd">
<td><p>받는 사람에 게 &quot;를&quot; 행에 나와 있습니다.</p></td>
<td><p>% %를 % %</p></td>
</tr>
<tr class="even">
<td><p>받는 사람에 게 &quot;참조&quot; 행에 나와 있습니다.</p></td>
<td><p>% % 참조 % %</p></td>
</tr>
<tr class="odd">
<td><p>원본 메시지의 제목입니다.</p></td>
<td><p>% % 주제 % %</p></td>
</tr>
<tr class="even">
<td><p>원본 메시지의 헤더입니다. 원본 메시지에 대해 생성 된 배달 상태 알림 (DSN)에서 머리글의 목록에는 것과 비슷합니다.</p></td>
<td><p>% % 헤더 % %</p></td>
</tr>
<tr class="odd">
<td><p>원본 메시지를 보낸 날짜입니다.</p></td>
<td><p>%%MessageDate%%</p></td>
</tr>
</tbody>
</table>


이 예제에서는 첨부 파일을 포함 하 고 조직 내 사람에 게 전송 되는 모든 메시지를 차단 하 고 받는 사람에 게 알립니다.

![인바운드 메시지에 차단된 경우 받는 사람에게 알려 주는 규칙](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "인바운드 메시지에 차단된 경우 받는 사람에게 알려 주는 규칙")

## 알림 제목 줄을 수정 하는 예제 3:

알림을 받는 사람에 게 보내면 제목 줄은 원본 메시지의 제목입니다. 받는 사람에 게 명확 하 게 하는 주체를 수정 하려는 경우 두 전송 규칙을 사용 해야 합니다.

  - 모든 첨부 파일이 있는 메시지의 제목 시작 부분에 "배달할 수 없는" 라는 단어를 추가 하는 첫번째 규칙이입니다.

  - 두번째 규칙이 메시지를 차단 하 고 원본 메시지의 새 주제를 사용 하 여 발신자에 게 알림 메시지를 보냅니다.


> [!IMPORTANT]
> 두 규칙에는 동일한 조건 있어야 합니다. 규칙 "배달할 수 없음" 라는 단어를 추가 하는 첫번째 규칙이 하 고 두번째 규칙이 메시지를 차단 하 고 받는 사람에 게 알리는 순서로 처리 됩니다.



하는 경우 추가 하려는 제목에 "배달할 수 없는"와 같은 확인 하는 첫번째 규칙은 다음과 같습니다.

![첨부 파일이 포함된 메시지 앞에 배달할 수 없음을 추가하는 규칙](images/Dn950026.2552b0bd-c69d-48b4-9e69-267fcaf20e70(EXCHG.150).png "첨부 파일이 포함된 메시지 앞에 배달할 수 없음을 추가하는 규칙")

하 고 두번째 규칙을 차단 하며 알림 (예제 2에서 동일한 규칙) 작업을 수행 합니다.

![인바운드 메시지에 차단된 경우 받는 사람에게 알려 주는 규칙](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "인바운드 메시지에 차단된 경우 받는 사람에게 알려 주는 규칙")

## 시간 제한 규칙을 적용 하는 예제 4:

맬웨어로 인 경우에 첨부 파일을 일시적으로 차단 하는 시간 제한 된 규칙을 적용 하는 것이 좋습니다. 예, 다음 규칙에는 시작 및 중지 날짜와 시간을 모두에:

![제한 시간을 보여주는 규칙](images/Dn950026.bdc8c4d8-72fa-4c5b-97f2-5fe76d50e643(EXCHG.150).png "제한 시간을 보여주는 규칙")

## 참고 항목


[메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)  


[Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\))  
[Exchange Online Protection의 메일 흐름 규칙(전송 규칙)](https://technet.microsoft.com/ko-kr/library/dn271424\(v=exchg.150\))

