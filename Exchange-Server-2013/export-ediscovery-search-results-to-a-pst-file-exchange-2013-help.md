---
title: 'PST 파일로 eDiscovery 검색 결과 내보내기: Exchange 2013 Help'
TOCTitle: PST 파일로 eDiscovery 검색 결과 내보내기
ms:assetid: bc47f5f9-d056-4b69-b669-ae65fad541c8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn440164(v=EXCHG.150)
ms:contentKeyID: 59635484
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# PST 파일로 eDiscovery 검색 결과 내보내기

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-09-07_

원본 위치 eDiscovery 검색의 결과 PST 파일로 라고도 하는 Outlook 데이터 파일을 내보내려면 Exchange 관리 센터 (EAC) eDiscovery 내보내기 도구를 사용할 수 있습니다. 관리자는 인사 관리자 또는 레코드 관리자와 같은 조직 내에서 다른 사람에 게 또는 법적 경우에서 자문 반대 하는 검색 결과 배포할 수 있습니다. 검색 결과 PST 파일을 내보낸 후 또는 다른 사용자가 열기 전에 검토 또는 검색 결과에 반환 되는 메시지를 인쇄 하는 Outlook에서 합니다. 제 3 자 eDiscovery 및 보고 응용 프로그램에서 PST 파일을 열 수도 있습니다. 이 항목에서는이 작업을 수행 하 고 되었을 수 있는 문제를 해결 하는 방법을 보여줍니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 시간은 내보내는 검색 결과의 양과 크기에 따라 달라집니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "원본 위치 eDiscovery" 항목.

  - 검색 결과 PST 파일로 내보내는 데 사용 하는 컴퓨터에는 다음과 같은 시스템 요구 사항을 충족 해야 합니다.
    
      - 32 비트 또는 64 비트 버전의 Windows 7 이상 버전
    
      - Microsoft.NET Framework 4.7
    
      - 지원되는 브라우저:
        
          - Internet Explorer 10 이상 버전
            
            또는
        
          - Mozilla Firefox 또는 Google Chrome 합니다. 이러한 브라우저 중 하나를 사용 하는 경우 *ClickOnce* 확장을 설치 해야 합니다. ClickOnce 추가 기능을 설치, [Mozilla ClickOnce 추가 기능이](https://addons.mozilla.org/en-us/firefox/search/?q=clickonce%26cat=1%2c0%26appver=%26platform=) 또는 [Google chrome ClickOnce](https://chrome.google.com/webstore/search/clickonce?_category=extensions)을 참조 합니다.

  - 내보낼 것인지 계정에 연결 된 활성 사서함이 있는 해야 합니다.

  - 로컬 인트라넷 설정 Internet Explorer에서 올바르게 설치 되었는지 확인 합니다. 해당 **https://\*.outlook.com** 로컬 인트라넷 영역에 추가 되 고 있는지 확인 합니다.

  - 신뢰할 수 있는 사이트 영역에는 다음 URL을 나열 되지 않은 있는지 확인 합니다.
    
      - https://\*.outlook.com
    
      - https://r4.res.outlook.com
    
      - https://\*.res.outlook.com

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## Exchange 관리 센터 를 사용 하 여 원본 위치 eDiscovery 검색 결과 pst 내보내기

1.  **규정 준수 관리** \> **원본 위치 eDiscovery 및 유지**로 이동합니다.

2.  목록 보기에서 결과를 내보내려는 원본 유지 eDiscovery 검색을 선택한 다음 **PST 파일로 내보내기**를 클릭합니다.
    
    ![PST 파일로 내보내기](images/Dn440164.1ebee2ac-89b3-49fa-b70c-a07c9a65f958(EXCHG.150).gif "PST 파일로 내보내기")  

3.  **eDiscovery PST 내보내기 도구** 창에서 다음을 수행합니다.
    
      - **찾아보기**를 클릭하여 PST 파일을 다운로드하려는 위치를 지정합니다.
    
      - **중복 제거 사용** 확인란을 클릭하여 중복 메시지를 제외합니다. 단일 메시지 인스턴스만 PST 파일에 포함됩니다.
    
      - **검색할 수 없는 항목 포함** 확인란을 클릭하여 검색할 수 없는 사서함 항목(예: Exchange 검색에서 인덱싱할 수 없는 파일 형식이 첨부된 메시지)을 포함합니다. 그러면 검색할 수 없는 항목이 별도의 PST 파일로 내보내집니다.
        

        > [!IMPORTANT]
        > eDiscovery 검색 결과를 내보낼 때 사서함에 검색할 수 없는 항목이 포함되어 있는데 그 수가 많으면 시간이 오래 걸릴 수 있습니다. 검색 결과를 내보내는 데 걸리는 시간을 단축하고 PST 내보내기 파일이 너무 커지지 않도록 하려면 다음 권장 사항을 고려하세요. 
        > <UL>
        > <LI>
        > <P>각각 더 적은 수의 원본 사서함을 검색할 여러 eDiscovery 검색을 만들어 수행합니다.</P>
        > <LI>
        > <P>검색 조건에서 키워드를 지정하지 않음으로써 특정 날짜 범위 내의 모든 사서함 콘텐츠를 내보내는 경우 해당 날짜 범위 내의 검색할 수 없는 항목이 모두 검색 결과에 자동으로 포함됩니다. 그러므로 <STRONG>검색할 수 없는 항목 포함</STRONG> 확인란을 선택하지 마세요.</P></LI></UL>



4.  **시작**을 클릭하여 검색 결과를 PST 파일로 내보냅니다.
    
    내보내기 프로세스에 대한 상태 정보가 포함된 창이 표시됩니다.

## 추가 정보

  - 검색할 수 없는 항목에만 내보내기 (영문) PST 내보내기 fileby의 크기를 줄일 수 있습니다. 이 작업을 수행 하려면 만들고 또는 편집 검색, 나중에 시작 날짜를 지정 하 고 **키워드** 상자에서 모든 키워드를 제거 합니다. 이렇게 하면 반환 되 고 검색 결과 없음. 검색 결과 복사 내보내고 **검색할 수 없는 항목 포함** 확인란을 선택 하는 경우 검색할 수 없는 항목에만 검색 사서함으로 복사 하거나 PST 파일로 내보낼 됩니다.

  - 중복 제거를 사용하도록 설정하면 모든 검색 결과가 단일 PST 파일로 내보내집니다. 중복 제거를 사용하도록 설정하지 않으면 별도의 PST 파일이 검색에 포함된 각 사서함으로 내보내집니다. 앞서 설명한 바와 같이 검색할 수 없는 항목은 별도의 PST 파일로 내보내집니다.

  - 또한 다음과 같이 검색 결과가 포함된 PST 파일인 다른 두 파일도 내보내집니다.
    
      - 내보낸 eDiscovery 검색 이름, 내보낸 날짜/시간, 중복 제거 및 검색되지 않는 항목의 사용 설정 여부, 검색 쿼리, 검색된 원본 사서함 등 PST 내보내기 요청에 대한 정보가 포함된 구성 파일(.txt 파일 형식)
    
      - 검색 결과에서 반환된 각 메시지의 항목이 포함된 검색 결과 로그(.csv 파일 형식) 각 항목은 메시지가 위치한 원본 사서함을 식별합니다. 중복 제거를 사용하도록 설정하면 중복 메시지가 포함된 사서함을 모두 식별할 수 있습니다.

  - 검색 이름은 내보낸 각 파일의 첫 번째 파일 이름에 해당하는 부분입니다. 각 PST 파일과 결과 로그의 파일 이름에는 내보내기 요청의 날짜/시간도 추가됩니다.

  - 중복 제거 및 검색되지 않는 항목에 대한 자세한 내용은 다음을 참조하세요.
    
      - [Estimate, preview, and copy search results](in-place-ediscovery-exchange-2013-help.md)
    
      - [Exchange eDiscovery의 검색할 수 없는 항목](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

  - SharePoint 또는 SharePoint Online에서 eDiscovery 센터에서 eDiscovery 검색 결과 내보내려는 [eDiscovery 콘텐츠 내보내기 및 보고서 만들기](https://go.microsoft.com/fwlink/p/?linkid=324757)를 참조 하십시오.

## 문제 해결


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>문제</th>
<th>가능한 원인</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PST 파일로 내보낼 수 없습니다.</p></td>
<td><ul>
<li><p>계정에 연결 된 활성 사서함이 없는지 방법이 있습니다. PST를 내보내려면 활성 계정이 있어야 합니다.</p></li>
<li><p>Internet Explorer의 버전은 오래입니다. 10 이상 버전으로 업데이트 IE 시도 합니다. 또는 다른 브라우저를 시도 합니다.</p></li>
<li><p><strong>필터 조건에 따라</strong> 쿼리에 입력 한 검색 조건을 올바르지 않습니다. 전자 메일 주소 대신 사용자 이름을 입력 되는 예입니다. 기준에 따라 필터링 하는 방법에 대 한 자세한 내용은 <a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">원본 위치 eDiscovery 검색 수정</a>를 참조 하십시오.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>특정 컴퓨터에서 검색 결과 내보낼 수 없습니다. 다른 컴퓨터에 예상 대로 작동을 내보냅니다.</p></td>
<td><p>잘못 된 Windows 자격 증명의 <strong>자격 증명 관리자</strong> 에 저장 합니다. 사용자의 자격 증명의 선택을 취소 하 고 다시 로그인 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>eDiscovery PST 내보내기 도구 시작 되지 않습니다.</p></td>
<td><p>로컬 인트라넷 영역 설정은 Internet Explorer에서 올바르게를 설정 되지 않습니다. 있는지 확인 *. outlook.com, *. office365.com, *. sharepoint.com 하 고 *. onmicrosoft.com 로컬 인트라넷 영역 신뢰할 수 있는 사이트에 추가 됩니다.</p>
<p>IE의 신뢰할 수 있는 영역에 이러한 사이트를 추가할 참조 <a href="https://windows.microsoft.com/en-us/windows/security-zones-adding-removing-websites#1tc=windows-7">보안 영역: 추가 또는 제거 하는 웹사이트</a>합니다.</p></td>
</tr>
</tbody>
</table>

