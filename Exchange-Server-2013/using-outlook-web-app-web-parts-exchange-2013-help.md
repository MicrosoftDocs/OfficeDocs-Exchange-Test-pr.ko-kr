---
title: 'Outlook Web App 웹 파트를 사용 하 여: Exchange 2013 Help'
TOCTitle: Outlook Web App 웹 파트를 사용 하 여
ms:assetid: 7272e3ab-430c-4d6c-8621-9535236ce463
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt574711(v=EXCHG.150)
ms:contentKeyID: 70076236
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App 웹 파트를 사용 하 여

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-07-31_

사용 하 여 MicrosoftOfficeOutlook Web App 열려는 사서함을 지정 하려면 웹 파트를 열려면 해당 사서함 내 폴더 및 콘텐츠 보기를 사용할 수 있습니다.

Outlook Web App 웹 파트를 사용 하면 URL에서 직접 Outlook Web App 콘텐츠에 액세스 합니다. URL은 웹 브라우저에 입력 한 하거나 응용 프로그램에 포함 될 수 있습니다. 일반적으로 웹 파트 수동으로 생성 되지 않습니다. 대신, 프로그래밍 방식으로 사용자 인터페이스 (UI)에서 선택한 항목에 따라 만들어질 또는 SharePoint Server 페이지와 같은 응용 프로그램에서 직접 포함 하 합니다. UI 뒤에서 코드는 다음 URL을 만듭니다. Outlook Web App 웹 파트에 대 한 하나 사용 SharePoint 페이지에서 사용자의 받은 편지함 또는 일정을 표시 하는 것입니다.


> [!NOTE]
> Outlook Web App 웹 파트를 사용 하려면 사용자의 사서함 및 웹 파트를 통해 열리는 사서함 모두 같은 Active Directory 포리스트에 배치 되어야 합니다.



## Outlook Web Access 웹 파트를 사용 하는 것에 대 한 사용 권한

Outlook Web App 웹 파트를 사용 하려면, 여기에 최소한 이어야 열려는 콘텐츠에 대 한 권한이 위임된 "검토자" 액세스 합니다. Outlook Web App 응용 프로그램에 대 한 인증을 요구 하는 웹 파트를 포함 한 경우에 웹 파트에 대 한 요청 함께 통해 인증 정보를 전달 해야 합니다. 이 작업을 수행 하는 한 가지 방법은 Windows 통합된 인증을 사용 하 여 Outlook Web App 가상 디렉터리를 구성 하 여 됩니다. 통합 된 Windows 인증 자격 증명을 다시 입력 하지 않고도 자신의 Active Directory 계정을 사용 하 여 Outlook Web App 를 사용 하 여 이미 로그온 한 사용자 수 있습니다.

## Outlook Web App 웹 파트 구문

Outlook Web App Exchange 2013에는 /owa 가상 디렉터리에 대 한 요청에 대 한 사용 하 여 URL 형식입니다. 웹 브라우저에 직접 URL을 입력 하 여 또는 SharePoint Server 페이지와 같은 웹 응용 프로그램의 URL을 포함 하 여 이러한 요청을 수행할 수 있습니다.

Outlook Web App 웹 파트의 복잡도 각기 다른 Url을 만들 수 사용할 수 있습니다. 모든 사서함의 받은 편지함을 여 단순한 웹 파트 URL은 사용할 수 있습니다. 열려는 사서함를 열려면 해당 사서함 내 폴더 및 사용 하 여 콘텐츠 보기를 지정 하려면 보다 복잡 한 웹 파트 URL은 사용할 수 있습니다.

네트워크에 적용 된 보안 조치를 따라 웹 파트 URL에 대 한 인코딩 구성 해야할 수 있습니다. 인코딩을 구성한 후 UI 뒤에서 코드에는 URL로 인코딩된 매개 변수를 사용 하 여 URL이 만들어집니다. 공백 및 경로 구분 기호 대신 %2f 대신 20%를 사용 하는 URL로 인코딩된 매개 변수 "/"입니다. 이 항목의 모든 예제 인코딩된 매개 변수를 사용 합니다.

다음 표에서 사용 하는 방법의 예제 및 웹 파트의 매개 변수를 보여줍니다.

### 웹 파트 매개 변수 및 사용 하는 방법

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>URL 매개 변수</th>
<th>설명</th>
<th>값 및 예</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>서버 이름 및 디렉터리 (필수)</p></td>
<td><p>Outlook Web App 가상 디렉터리의 URL입니다.</p></td>
<td><p>이 사용자가 Outlook Web App 대 한 로그인을 사용 하는 동일한 URL 수 있습니다.</p>
<p>https://&lt;<em>server name</em>&gt; / owa</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 명시적 로그온 사서함 id (선택 사항)</p></td>
<td><p>사서함을 열 수와 관련 된 모든 SMTP 주소입니다.</p>
<p>이 섹션의 URL의 누락 된 경우 인증된 된 사용자의 기본 사서함 열릴 수 있습니다.</p>
<p>추가 매개 변수 없이 구성 요소를 지정 하는 경우 받은 편지함을 여는 기본 동작은입니다.</p></td>
<td><p>SMTP 주소가 tsmith@fourthcoffee.com 인 사서함을 열려면 다음 URL을 사용 합니다.</p>
<p>https://&lt;<em>server name</em>&gt;/owa/tsmith@fourthcoffee.com</p></td>
</tr>
<tr class="odd">
<td><p>cmd (명시적 로그온 사서함 id 이외의 매개 변수를 지정 하는 경우 필요)</p></td>
<td><p>? cmd = contents 표시 Outlook Web App 전체 Outlook Web App 사용자 인터페이스 대신 매개 변수로 지정 된 웹 파트입니다.</p></td>
<td><p>사서함이 없는지를 지정 하는 경우 cmd 매개 변수 뒤에 오는 로그인 주소 다음과 같습니다.</p>
<p>https://&lt;,<em>server name</em>&gt;/owa/?cmd =</p>
<p>사서함을 지정 하는 경우 cmd 매개 변수 뒤에 오는 명시적 사서함 id 다음과 같이 합니다.</p>
<p>https://&lt;<em>server name</em>&gt; /owa/ &lt;<em>SMTP address</em>&gt; / ?cmd =</p>
<p>추가 매개 변수 없이 구성 요소를 지정 하는 경우 받은 편지함을 여는 기본 동작은입니다.</p></td>
</tr>
<tr class="even">
<td><p>exsvurl</p></td>
<td><p>Live Id 인증을 사용 하는 경우이 매개 변수를 포함 되어야 합니다.</p>
<p>하는 경우 LiveID 인증 하는 동안 모든 매개 변수를 무시 됩니다 &quot;exsvurl = 1&quot; 나타나지 않습니다. 이 매개 변수는 Office 365 사서함만입니다.</p></td>
<td><p>https://&lt;server 이름 &gt; /owa/? cmd = 내용을 &amp; exsvurl = 1</p></td>
</tr>
<tr class="odd">
<td><p>fpath (옵션)</p></td>
<td><p>URL의이 부분 방화벽을 통해 전달할 수 있도록 URL 인코딩을 사용 하 여 작성 되어야 할 수 있습니다.</p>
<p>URL 인코딩을 사용할 때 공백은 %20이 되 고 경로 구분 기호 (/)는 %2f가 됩니다.</p>
<p>폴더 계층은 사서함 루트에서 시작 해야 합니다.</p>
<p>이 폴더 경로 가리킬 하거나 검색 폴더 수 있습니다.</p></td>
<td><p>받은 편지함의 하위 프로젝트를 열려면 다음 URL을 사용 합니다.</p>
<p>https://&lt;,<em>server name</em>&gt;/owa/?cmd 내용 (영문) fpath 받은 편지함 %2fprojects =</p></td>
</tr>
<tr class="even">
<td><p>모듈 (선택 사항)</p></td>
<td><p>지역화 된 이름을 모르는 기본 폴더 중 하나를 지정 하려면이 매개 변수를 사용할 수 있습니다.</p></td>
<td><p>매개 변수는 모듈에 대 한 값 대/소문자를 구분 하지 하 고는 다음이 포함 됩니다.</p>
<ul>
<li><p>Inbox</p></li>
<li><p>일정</p></li>
<li><p>Teammailbox</p></li>
</ul>
<p>지역화에 관계 없이 사서함의 일정을 열려면 다음 URL을 사용 합니다.</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd 내용을 /resources/msdn/en-us/office/media/courseviewer/sharepoint2013trainingitpro_mod1.xml&amp;operation = = 달력</p></td>
</tr>
<tr class="odd">
<td><p>(선택 사항) 보기</p></td>
<td><p>이 매개 변수는 폴더에 대해 표시할 보기를 지정 합니다.</p>
<p>이 매개 변수가 없는 경우 기본 보기는 다음과 같습니다.</p>
<ul>
<li><p>Calendar 일별</p></li>
<li><p>Messages 메시지</p></li>
</ul>

> [!NOTE]
> 기본 보기에 대 한 문자열은 자동으로 URL 인코딩됩니다.


<p>보기에 대 한 기본 정렬 폴더 때의 정렬 방식과 Outlook Web App 클라이언트에서 연 방법은.</p>
<p>보기를 식별 하는 문자열은 지역화 되지 않은 되며 대/소문자 구분 없습니다.</p></td>
<td><p>사용할 수 있는 보기는 폴더 유형에 따라 다릅니다.</p>
<p>달력 보기:</p>
<ul>
<li><p>Daily 일별 일정 보기</p></li>
<li><p>Weekly 주별 일정 보기</p></li>
<li><p>Monthly 월별 일정 보기</p></li>
</ul>
<p>메시지 보기:</p>
<ul>
<li><p>Messages 기본 정렬 된 메시지 보기</p></li>
<li><p>%20Sender 하 여 메시지 별로 정렬 된 보기에서 위쪽에 &quot;a&quot;로 시작 되는 보낸사람 이름을</p></li>
<li><p>By %20Subject 메시지 보기 위쪽에 &quot;a&quot;로 시작 하는 주체와 제목별으로 정렬</p></li>
<li><p>By %20Conversation %20Topic 대화 보기 Outlook Web App 의 라이트 버전에서 사용할 수 없음</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>d, m, y (선택 사항)</p></td>
<td><p>일정을 표시 하는 날짜를 지정 합니다. 이러한 매개 변수 순서에 상관 없이 입력할 수의 형식과 개별적으로 또는 함께 사용할 수 있습니다.</p>
<p>이 매개 변수 중 하나라도 변수가 지정 되지 않은 경우 기본값은 현재 일, 월 및 연도 값입니다. 예, 현재 요일은 2016 년 5 월 3 일 년 9 월에 대 한 &quot;9&quot;의 월 값을 지정 하는 경우 표시 되는 날짜 2016 년 9 월 3 일이 됩니다.</p></td>
<td><p>데이터 매개 변수에 대 한 유효한 값은 다음과 같습니다.</p>
<p>d = [1-31]</p>
<p>m = [1-12]</p>
<p>y = [네자리 연도]</p>
<p>2016, 5 월 3 일 날짜를 달력을 열려면 다음 URL을 사용 하면: https://&lt;<em>server name</em>&gt;/owa/?cmd 콘텐츠 (영문) fpath 달력 (영문) 보기 매일 &amp; d = 3 &amp; m = 5 &amp; y = 2016 =</p></td>
</tr>
<tr class="odd">
<td><p>파트 (선택 사항)</p></td>
<td><p>해당 Outlook Web App 더 작은 웹 파트를 표시할지를 지정 합니다.</p></td>
<td><p>웹 파트를 사용 하 여 Outlook Web App 콘텐츠에 액세스를 UI 표시 되는 UI 전체 Outlook Web App 보다 작은 수 있습니다. 파트 매개 변수는 UI를 추가로 줄일 수 있습니다. 다음 예제에서는 URL 가장 작은 웹 파트의 형식에 작업 목록을 보여줍니다.</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd 내용 (영문) 파트 = 1</p>
<p>파트 매개 변수는 일정 모듈에 적용 되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>FolderList</p></td>
<td><p>이 파트 매개 변수는 하위 폴더 사이 전환 하는 사용자에 대 한 폴더 목록 컨트롤을 포함 합니다. 이 전자 메일 폴더에만 적용 됩니다.</p></td>
<td><p>https://&lt;server 이름 &gt; /owa/? cmd = 내용을 &amp; folderlist = 1</p></td>
</tr>
</tbody>
</table>


## Outlook Web App 웹 파트를 수동으로 입력

Outlook Web App 웹 파트도 수를 직접 입력 웹 브라우저에서 합니다. 등 사용자를 다른 사용자의 일정을 열려면 Outlook Web App 웹 파트 URL을 사용할 수 있습니다.

다음 예제에는 일반적인 Outlook Web App 보기에 직접 액세스 하는 방법을 보여줍니다.

  - **받은 편지함:** https://*\<server name\>*/owa/?cmd 내용을 /resources/msdn/en-us/office/media/courseviewer/sharepoint2013trainingitpro\_mod1.xml\&operation = = 받은 편지함

  - **(오늘) 일정:**https://*\<server name\>*/owa/?cmd 내용을 /resources/msdn/en-us/office/media/courseviewer/sharepoint2013trainingitpro\_mod1.xml\&operation = 일정 & exsvurl = = 1

  - **(매주) 일정:** https://*\<server name\>*/owa/?cmd 내용을 /resources/msdn/en-us/office/media/courseviewer/sharepoint2013trainingitpro\_mod1.xml\&operation = 일정 및 보기 = 매주 & exsvurl = = 1

  - **(월별) 일정:** https://*\<server name\>*/owa/?cmd 내용을 /resources/msdn/en-us/office/media/courseviewer/sharepoint2013trainingitpro\_mod1.xml\&operation = 일정 및 보기 = 월별 & exsvurl = = 1

## 자세한 내용

  - [Outlook Web App 로그인, 언어 선택 및 오류 페이지를 사용자 지정](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)

  - [Outlook Web App에 대 한 테마 만들기](create-a-theme-for-outlook-web-app-exchange-2013-help.md)

