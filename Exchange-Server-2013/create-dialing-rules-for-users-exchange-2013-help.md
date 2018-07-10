---
title: '사용자에 대 한 전화걸기 규칙 만들기: Exchange 2013 Help'
TOCTitle: 사용자에 대 한 전화걸기 규칙 만들기
ms:assetid: c11e3d62-3eb1-4d7e-8741-9bede593e2df
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ898502(v=EXCHG.150)
ms:contentKeyID: 51407731
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자에 대 한 전화걸기 규칙 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-03-09_

전화 걸기 규칙 그룹은 전화 걸기 규칙 항목으로 구성됩니다. 전화 걸기 규칙은 전화 번호를 발신 전화용으로 온-프레미스 전화 시스템(PBX) 또는 IP PBX로 보내기 전에 수정하는 데 사용됩니다. 전화 걸기 규칙에는 두 가지 목적이 있습니다.

  - 전화 걸기 규칙은 발신 전화를 위해 전화를 걸 수 있는 번호를 지정합니다. 전화 걸기 규칙을 만들 때 전화를 걸 수 있는 번호 형식을 지정합니다. 지정한 형식 중 하나와 일치하지 않는 모든 번호는 거부됩니다. 전화 걸기 규칙을 설정하지 않는 경우 전화 건 사람은 조직 내에서 전화를 걸 수 있지만 발신 전화는 걸 수 없습니다.

  - 전화 걸기 규칙은 전화를 건 번호를 온-프레미스 전화 시스템으로 전송하기 전에 변환합니다. 전화 걸기 규칙은 전화를 건 번호에서 숫자를 제거하거나 추가할 수 있습니다. 예를 들어 전화 걸기 규칙을 사용하여 전화 시스템의 외부 회선 액세스 코드를 추가하거나 시외 또는 시내 전화 번호의 국가/지역 코드를 추가 또는 제거할 수 있습니다.

UM 다이얼 플랜에 대해 허용할 발신 전화 유형을 지정하려면 전화 걸기 규칙을 포함하여 전화 걸기 규칙 그룹을 만든 다음 해당 규칙을 사용해 UM 자동 전화 교환으로 전화를 거는 Outlook Voice Access 사용자 및 발신자에 대해 발신 전화 권한을 부여합니다. 국내/지역 통화와 국제 통화에 대해 서로 다른 전화 걸기 규칙 그룹을 만듭니다.


> [!NOTE]
> UM과 Microsoft Lync Server를 통합하는 경우에는 전화 걸기 규칙 그룹을 하나 이상 만들고 해당 그룹에 SIP URI 다이얼 플랜, UM 사서함 정책 및 UM 자동 전화 교환에 대한 권한을 부여하여 Lync Server로 모든 발신 전화의 전달을 허용하는 것이 좋습니다.



외부로 전화 걸기를 위한 기타 관리 작업에 대한 자세한 내용은 [사용자가 통화 절차를 수행 하도록 허용](allowing-users-to-make-calls-procedures-exchange-2013-help.md)를 참조하십시오.

## 흔히 사용되는 전화 걸기 규칙의 예


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>번호 패턴</strong></p></td>
<td><p><strong>전화 건 번호</strong></p></td>
<td><p><strong>어떤 경우에 이 전화 걸기 규칙을 사용합니까?</strong></p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>*</p></td>
<td><p>모든 발신 전화를 허용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>1425xxxxxxx</p></td>
<td><p>91425xxxxxxx</p></td>
<td><p>사용자가 외부 액세스 회선 번호를 누르지 않는 경우 내부 내선 번호 제공 또는 오류 발생을 방지합니다.</p></td>
</tr>
<tr class="even">
<td><p>1xxxxxxxxxx</p></td>
<td><p>1xxxxxxxxxx</p></td>
<td><p>1로 시작되는 모든 번호를 허용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>xxxxxxx</p></td>
<td><p>1425xxxxxxx</p></td>
<td><p>1과 지역 코드 425를 7자리 번호에 추가합니다.</p></td>
</tr>
</tbody>
</table>


## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 전화 걸기 규칙 그룹을 UM 사서함 정책에 적용하려면 UM 사서함 정책이 작성되었는지 확인해야 합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 전화 걸기 규칙 그룹을 UM 자동 전화 교환에 적용하려면 UM 자동 전화 교환이 작성되었는지 확인해야 합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## EAC를 사용하여 전화 걸기 규칙 만들기

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지 \> **전화 걸기 규칙**에서 **국내/지역 전화 걸기 규칙** 또는 **국제 전화 걸기 규칙** 아래의 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **새 전화 걸기 규칙** 페이지에서 다음 정보를 입력합니다.
    
      - **전화 걸기 규칙 이름**   이 규칙이 속할 전화 걸기 규칙 그룹의 이름을 입력합니다. 이 규칙을 다른 규칙과 결합하려면 동일한 그룹 이름을 사용합니다. 새 전화 걸기 규칙 그룹을 만들려면 새 고유 이름을 입력합니다.
    
      - **변환할 숫자 패턴(숫자 마스크)**   전화를 걸기 전에 변환할 숫자 패턴을 입력합니다(예: 91425xxxxxxx). 전화 건 사람이 일치하는 번호를 입력하면 UM은 전화를 연결하기 전에 해당 번호를 전화 건 번호로 변환합니다. 숫자와 와일드카드(x)만 입력하십시오. 숫자 패턴을 *숫자 마스크*라고도 합니다.
    
      - **전화 건 번호   **전화 걸 번호를 입력합니다. 숫자 및 와일드카드(x)만 번호 패턴 9xxxxxxx와 같이 사용합니다. 와일드카드(x)는 사용자가 전화를 건 원래 번호의 숫자로 대체됩니다. 전화 건 번호의 와일드카드 수는 번호 패턴의 와일드카드 수와 같아야 합니다.
    
      - **설명   **이 전화 걸기 규칙에 대한 설명을 입력합니다. 설명을 사용하여 "발신 전화에 9 추가"와 같이 규칙이 수행하는 작업을 설명할 수 있습니다.

5.  **확인**을 클릭하여 전화 걸기 규칙을 저장합니다. 함께 권한을 부여할 규칙에 대해 같은 전화 걸기 규칙 그룹 이름을 사용하여 계속 규칙을 입력할 수 있습니다.

