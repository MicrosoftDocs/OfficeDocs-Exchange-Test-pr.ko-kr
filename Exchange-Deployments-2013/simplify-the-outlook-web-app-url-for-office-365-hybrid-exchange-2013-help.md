---
title: 'Office 365 Hybrid용 Outlook Web App URL을 단순화: Exchange 2013 Help'
TOCTitle: Office 365 Hybrid용 Outlook Web App URL을 단순화
ms:assetid: 19449aee-3796-4298-90c6-c7579b8d2f7a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt791749(v=EXCHG.150)
ms:contentKeyID: 74259169
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Office 365 Hybrid용 Outlook Web App URL을 단순화

 

_<strong>마지막으로 수정된 항목:</strong>2016-11-11_

하이브리드 환경에서 클라우드 사서함 사용자의 웹에서 Outlook(Outlook Web App)용 URL을 구성하는 방법을 알아보세요.

온-프레미스 Exchange에서 Office 365로 이동하는 조직에서 중요한 사항은 사용자 환경입니다. 사용자는 자신의 사서함이 언제 어디로 이동했는지와 상관없이 사서함에 대해 중단 없는 액세스 권한이 필요합니다. 이를 염두에 둔다면 웹에서 Outlook(이전의 Outlook Web App) 동시 사용 기능이 중요합니다.

다음 시나리오를 살펴보세요(온-프레미스 Exchange의 일부 사서함을 Office 365로 이동하기 위해 회사에서 하이브리드 배포를 사용하는 경우). 금요일에 사용자가 이동하기 전에 URL(https://mail.contoso.com/owa)을 통해 온-프레미스 사서함에 액세스했습니다. 월요일에 이동한 후에 해당 사용자가 이 URL을 사용하여 자신의 사서함에 액세스하려 할 때 오류가 발생합니다.

웹에서 Outlook를 사서함에 연결하기 위해 영향을 받는 사용자를 허용하려면 다음과 같은 두 가지 옵션을 사용할 수 있습니다.

  - **사용자에게 새 URL(예: https://outlook.com/owa/contoso.com)을 알림**   이 옵션에는 다음과 같은 문제점이 있습니다.
    
      - URL이 복잡합니다.
    
      - 영향을 받는 사용자에 대한 환경이 원활하지 않습니다.

  - **조직 관계에 TargetOWAUrl 설정 구성**   이 옵션에는 다음과 같은 문제점이 있습니다.
    
      - 클라우드 사서함에 대한 끝점이 외부에 있습니다(사용자에게 필요한 도메인에 없음).
    
      - 끝점에 URL의 도메인이 필요합니다(Office 365 Business 및 Outlook.com 소비자 제품 간을 구분하기 위해).
    
      - 끝점을 사용하면 사용자에게 인증서 불일치 경고가 표시됩니다.

클라우드 사서함이 있는 사용자에 대해 이러한 문제가 발생하는 것을 방지하려면 다음 단계를 수행합니다.

1.  **mail.office365.com을 가리키는 DNS의 CNAME 레코드(예: cloudowa.contoso.com)를 만듭니다.**
    
      - 사용자가 내부 또는 외부 인터넷 연결에서 연결할 수도 있으므로 내부 및 외부(공용) DNS에 이 CNAME 레코드를 만들어야 합니다.
    
      - 이 예에서는 contoso.com 도메인이 요청에 사용됩니다(cloudowa 부분이 삭제됨). 즉, URL에 도메인을 지정할 필요가 없습니다.

2.  **온-프레미스 조직 관계에 웹에서 Outlook 리디렉션을 구성합니다.**   구성하려면 온-프레미스 Exchange의 Exchange 관리 셸에 있는 다음 구문을 사용합니다.
    
        Set-OrganizationRelationship -TargetOWAUrl http://<CNAME value>/owa
    
    예를 들어 1단계에서 만든 CNAME 레코드가 cloudowa.contoso.com이면 다음 명령을 실행합니다.
    
        Set-OrganizationRelationship -TargetOWAUrl http://cloudowa.contoso.com/owa
    
    **참고:**
    
      - https가 아닌 http를 사용합니다.
    
      - 조직 관계에 후행 값 /owa가 필요하지만 사용자가 URL에 /owa를 입력할 필요는 없습니다.

## 여러 인증 프롬프트

다음에 따라 사용자가 여러 개의 인증 프롬프트를 받을 수 있습니다.

  - 내부 또는 외부 인터넷 연결의 연결 위치

  - 컴퓨터가 가입된 도메인인지 여부

  - 하이브리드 환경에서 ID 페더레이션을 사용 중인 경우

다음 표에는 사용자에게 필요할 수 있는 인증 프롬프트 환경이 설명되어 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>인증 방법</th>
<th>클라이언트 컴퓨터</th>
<th>인증 프롬프트 환경</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ID 페더레이션</p></td>
<td><p>내부 인터넷 연결</p></td>
<td><p>단일 프롬프트</p></td>
</tr>
<tr class="even">
<td><p>ID 페더레이션</p></td>
<td><p>외부 인터넷 연결</p></td>
<td><p>이중 프롬프트</p></td>
</tr>
<tr class="odd">
<td><p>ID 페더레이션 없음</p></td>
<td><p>가입된 도메인(내부 또는 외부)</p></td>
<td><p>이중 프롬프트</p></td>
</tr>
<tr class="even">
<td><p>ID 페더레이션의 유무</p></td>
<td><p>가입된 도메인이 아님(내부 또는 외부)</p></td>
<td><p>이중 프롬프트</p></td>
</tr>
</tbody>
</table>


**참고:** ID 페더레이션을 사용하려면 [https://go.microsoft.com/fwlink/p/?linkid=834460](https://go.microsoft.com/fwlink/p/?linkid=83446) 항목에 설명된 것처럼 AD FS 끝점이 Internet Explorer의 인트라넷 영역에 구성되어야 하고, 해당 AD FS가 일반 Office 365 지침별로 구성되어야 합니다.

