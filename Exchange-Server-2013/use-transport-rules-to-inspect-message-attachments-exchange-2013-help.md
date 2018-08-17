---
title: '전송 규칙을 사용 하 여 메시지 첨부 파일을 검사 하려면: Exchange 2013 Help'
TOCTitle: 전송 규칙을 사용 하 여 메시지 첨부 파일을 검사 하려면
ms:assetid: c0de687e-e33c-4e8a-b253-771494678795
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ674307(v=EXCHG.150)
ms:contentKeyID: 50484074
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전송 규칙을 사용 하 여 메시지 첨부 파일을 검사 하려면

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-27_

전송 규칙을 설정하여 조직의 전자 메일 첨부 파일을 조사할 수 있습니다. Exchange에는 메시징 보안 및 규정 준수 요구의 일부로 전자 메일 첨부 파일을 검사하는 기능이 제공되는 전송 규칙이 있습니다. 첨부 파일을 조사하는 경우 해당 첨부 파일의 내용이나 특성에 따라 조사한 메시지에 대해 작업을 수행할 수 있습니다. 다음은 전송 규칙을 사용하여 수행할 수 있는 첨부 파일 관련 일부 작업입니다.

  - .zip 및 .rar 파일과 같은 압축된 첨부 파일에서 파일을 검색하고 지정한 패턴과 일치하는 텍스트가 있으면 메시지 끝에 공지 사항 추가

  - 첨부 파일 내의 내용을 조사하고 지정한 키워드가 있으면 배달 전에 승인을 받기 위해 중재자에게 메시지를 리디렉션

  - 조사할 수 없는 첨부 파일이 있는 메시지를 확인한 다음 전체 메시지가 전송되지 않도록 차단

  - 특정 크기를 초과하는 첨부 파일이 있는지 확인한 다음 해당 메시지를 배달하지 않기로 결정한 경우 보낸 사람에게 문제 알림

  - 사용자가 보낸 메시지와 일치하는 전송 규칙이 있는 경우 해당 사용자에게 알려 주는 알림 만들기

  - 첨부 파일을 포함 하는 모든 메시지를 차단 합니다. 예제를 보려면 [일반적인 첨부 파일 차단 시나리오](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)를 참조 하십시오.

Exchange 관리자는 **Exchange 관리 센터** \> **메일 흐름** \> **규칙**으로 이동하여 전송 규칙을 만들 수 있습니다. 이 절차를 수행하려면 먼저 사용 권한을 할당 받아야 합니다. 새 규칙 만들기를 시작한 후에 **기타 옵션** \> **다음의 경우 이 규칙 적용**에서 **모든 첨부 파일**을 클릭하여 첨부 파일 관련 조건의 전체 목록을 표시할 수 있습니다. 첨부 파일 관련 옵션은 다음 다이어그램에 나와 있습니다.

![첨부 파일 관련 규칙을 선택하기 위한 대화 상자](images/JJ674307.2ae4a179-bfd2-4a0e-abe1-53ed4e9e3368(EXCHG.150).jpg "첨부 파일 관련 규칙을 선택하기 위한 대화 상자")

선택 가능한 전체 조건 및 작업을 비롯한 전송 규칙에 대한 자세한 내용은 [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)을 참조하세요. EOP(Exchange Online Protection) 및 하이브리드 고객은 [EOP 구성을 위한 모범 사례](https://technet.microsoft.com/ko-kr/library/jj723164\(v=exchg.150\))에서 제공되는 전송 규칙 모범 사례를 활용할 수 있습니다. 규칙을 만들 준비가 되었으면 [메일 흐름 규칙 관리](manage-mail-flow-rules-exchange-2013-help.md)를 참조하세요.

## 첨부 파일 내의 콘텐츠 조사

다음 표의 전송 규칙 조건을 사용하여 메시지 첨부 파일의 내용을 검사할 수 있습니다. 이러한 조건의 경우 첨부 파일의 처음 150KB만 조사됩니다. 메시지 조사 시 이러한 조건을 사용하려면 전송 규칙에 해당 조건을 추가해야 합니다. [메일 흐름 규칙 관리](manage-mail-flow-rules-exchange-2013-help.md)에서 규칙 만들기 또는 변경에 대해 자세히 알아보세요.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC의 조건 이름</th>
<th>셸의 조건 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>모든 첨부 파일 내용에 다음 단어 포함</strong></p></td>
<td><p><code>AttachmentContainsWords</code></p></td>
<td><p>이 조건은 지원되는 파일 형식 첨부 파일에 지정된 문자열 또는 문자 그룹이 포함된 메시지를 찾습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>모든 첨부 파일 내용이 다음 텍스트 패턴과 일치</strong></p></td>
<td><p><code>AttachmentMatchesPatterns</code></p></td>
<td><p>이 조건은 지원되는 파일 형식 첨부 파일의 텍스트 패턴이 지정된 정규식과 일치하는 메시지를 찾습니다.</p></td>
</tr>
</tbody>
</table>


여기에 표시된 조건의 Exchange 관리 셸 이름은 `TransportRule` cmdlet이 필요한 매개 변수입니다.

  -  [New-TransportRule](https://technet.microsoft.com/ko-kr/library/bb125138\(v=exchg.150\))에서 cmdlet에 대해 자세히 알아보세요.

  -  [Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)에서 이러한 조건의 속성 유형에 대해 자세히 알아보세요.

전송 규칙은 지원되는 파일 형식의 콘텐츠만 조사할 수 있습니다. 전송 규칙 에이전트가 지원되는 파일 형식 목록에 없는 첨부 파일을 발견하면 `AttachmentIsUnsupported` 조건이 트리거됩니다. 지원되는 파일 형식은 다음 섹션에 나와 있습니다. 나열되지 않은 파일은 `AttachmentIsUnsupported` 조건을 트리거합니다.

## 압축된 보관 파일

메시지에 .zip 또는 .cab 파일 같은 압축된 보관 파일이 포함되어 있으면 전송 규칙 에이전트는 해당 첨부 파일에 포함된 파일을 검사합니다. 이러한 메시지는 첨부 파일이 여러 개 있는 메시지와 유사한 방식으로 처리됩니다. 압축된 보관 파일의 속성은 조사되지 않습니다. 예를 들어 컨테이너 파일 형식이 설명을 지원할 경우 해당 필드는 조사되지 않습니다.

## 전송 규칙 내용을 조사할 수 있는 파일 형식

다음 표에는 전송 규칙에서 지원하는 파일 형식이 나와 있습니다. 시스템은 실제 파일 확장명이 아닌 파일 속성을 검사하여 파일 형식을 자동으로 검색합니다. 따라서 악성 해커가 파일 확장명을 바꿔 전송 규칙 필터링을 무시할 수 없도록 합니다. 전송 규칙 컨텍스트 내에서 검사할 수 있는 실행 코드가 있는 파일 형식 목록이 이 항목 뒷부분에 나와 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>범주</th>
<th>파일 확장명</th>
<th>참고</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Office 2013, Office 2010 및 Office 2007</p></td>
<td><p>.docm, .docx, .pptm, .pptx, .pub, .one, .xlsb, .xlsm, .xlsx</p></td>
<td><p>Microsoft Onenote와 Microsoft Publisher 파일은 기본적으로 지원되지 않습니다. IFilter 통합을 사용하면 이러한 파일 형식을 지원하도록 설정할 수 있습니다. 자세한 내용은 <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Exchange 2013으로 Filter Pack IFilter 등록</a>을 참조하십시오.</p>
<p>이러한 파일 유형 안에 있는 포함된 모든 부분의 콘텐츠도 조사됩니다. 하지만 링크된 문서와 같이 포함되지 않은 모든 개체는 조사되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>Office 2003</p></td>
<td><p>.doc, .ppt, .xls</p></td>
<td><p>없음</p></td>
</tr>
<tr class="odd">
<td><p>추가 Office 파일</p></td>
<td><p>.rtf, .vdw, .vsd, .vss, .vst</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>Adobe PDF</p></td>
<td><p>.pdf</p></td>
<td><p>없음</p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p>.html</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>XML</p></td>
<td><p>.xml, .odp, .ods, .odt</p></td>
<td><p>없음</p></td>
</tr>
<tr class="odd">
<td><p>텍스트</p></td>
<td><p>.txt, .asm, .bat, .c, .cmd, .cpp, .cxx, .def, .dic, .h, .hpp, .hxx, .ibq, .idl, .inc, inf, .ini, inx, .js, .log, .m3u, .pl, .rc, .reg, .txt, .vbs, .wtx</p></td>
<td><p>없음</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument</p></td>
<td><p>.odp, .ods, .odt</p></td>
<td><p>.odf 파일의 어떠한 부분도 처리되지 않습니다. 예를 들어 .odf 파일에 포함된 문서가 있다면 해당 포함 문서의 콘텐츠는 조사되지 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p>AutoCAD Drawing</p></td>
<td><p>.dxf</p></td>
<td><p>AutoCAD 2013 파일은 지원되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>이미지</p></td>
<td><p>.jpg, .tiff</p></td>
<td><p>이러한 이미지 파일에 연결된 메타데이터 텍스트만 조사하며 광학 문자 인식은 수행되지 않습니다.</p></td>
</tr>
</tbody>
</table>


## 첨부 파일의 파일 속성 조사

다음 전송 규칙 조건은 메시지에 첨부된 파일의 속성을 조사합니다. 메시지 조사 시 이러한 조건을 사용하려면 전송 규칙에 해당 조건을 추가해야 합니다. 전송 규칙 컨텍스트 내에서 검사할 수 있는 실행 코드가 있는 지원되는 파일 형식 목록이 여기에 나와 있습니다. 규칙 만들기 또는 변경에 대한 자세한 내용은 [메일 흐름 규칙 관리](manage-mail-flow-rules-exchange-2013-help.md)를 참조하세요.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC의 조건 이름</th>
<th>셸의 조건 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>다음 텍스트 패턴과 일치하는 첨부 파일 이름</strong></p></td>
<td><p><code>AttachmentNameMatchesPatterns</code></p></td>
<td><p>이 조건은 해당 첨부 파일이 사용자가 지정한 문자를 포함하는 이름을 갖는 경우 지원되는 파일 형식 첨부 파일이 있는 메시지를 찾습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>다음 단어를 포함하는 첨부 파일 확장명</strong></p></td>
<td><p><code>AttachmentExtensionMatchesWords</code></p></td>
<td><p>이 조건은 첨부 파일 확장명이 사용자가 지정한 확장명과 일치할 때 지원되는 파일 형식 첨부 파일이 있는 메시지를 찾습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>다음 크기보다 크거나 같은 첨부 파일</strong></p></td>
<td><p><code>AttachmentSizeOver</code></p></td>
<td><p>이 조건은 해당 첨부 파일이 사용자가 지정한 크기보다 큰 경우 지원되는 파일 형식 첨부 파일이 있는 메시지를 찾습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>첨부 파일의 검사를 완료하지 않음</strong></p></td>
<td><p><code>AttachmentProcessingLimitExceeded</code></p></td>
<td><p>이 조건은 해당 첨부 파일이 전송 규칙 에이전트의 조사를 받지 않은 메시지를 찾습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>첨부 파일에 실행 가능한 콘텐츠가 있음</strong></p></td>
<td><p><code>AttachmentHasExecutableContent</code></p></td>
<td><p>이 조건은 실행 파일이 첨부 파일로 포함된 메시지를 찾습니다. 지원되는 파일 형식은 아래에 나와 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>첨부 파일이 암호로 보호됨</strong></p></td>
<td><p><code>AttachmentIsPasswordProtected</code></p></td>
<td><p>이 조건은 해당 첨부 파일이 암호로 보호될 경우 지원되는 파일 형식 첨부 파일이 있는 메시지를 찾습니다.</p></td>
</tr>
</tbody>
</table>


여기에 표시된 조건의 Exchange 관리 셸 이름은 `TransportRule` cmdlet이 필요한 매개 변수입니다.

  -  [New-TransportRule](https://technet.microsoft.com/ko-kr/library/bb125138\(v=exchg.150\))에서 cmdlet에 대해 자세히 알아보세요.

  -  [Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)에서 이러한 조건의 속성 유형에 대해 자세히 알아보세요.

## 전송 규칙 검사에 지원되는 실행 파일 형식

전송 에이전트는 파일 확장명뿐만이 아니라 파일 속성도 검사하는 진정한 의미의 형식 검사를 사용합니다. 따라서 악의적인 해커가 파일 확장명을 바꿔 규칙을 무시할 수 없습니다. 다음 표에는 이러한 조건에서 지원되는 실행 파일 형식이 나와 있습니다. 여기에 나와 있지 않은 파일이 발견되면 `AttachmentIsUnsupported` 조건이 트리거됩니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>파일 형식</th>
<th>기본 확장</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WinRAR 보관기를 사용하여 작성되는 자동 압축 풀기 보관 파일입니다.</p></td>
<td><p>.rar</p></td>
</tr>
<tr class="even">
<td><p>동적 연결 라이브러리 확장이 포함된 32비트 Windows 실행 파일입니다.</p></td>
<td><p>.dll</p></td>
</tr>
<tr class="odd">
<td><p>자동 압축 풀기 실행 프로그램 파일입니다.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>Java 보관 파일입니다.</p></td>
<td><p>.jar</p></td>
</tr>
<tr class="odd">
<td><p>제거 실행 파일입니다.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>프로그램 바로 가기 파일입니다.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>컴파일된 소스 코드 파일이나 3D 개체 파일 또는 시퀀스 파일입니다.</p></td>
<td><p>.obj</p></td>
</tr>
<tr class="even">
<td><p>32비트 Windows 실행 파일입니다.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Visio XML 드로잉 파일입니다.</p></td>
<td><p>.vxd</p></td>
</tr>
<tr class="even">
<td><p>OS/2 운영 체제 파일입니다.</p></td>
<td><p>.os2</p></td>
</tr>
<tr class="odd">
<td><p>16비트 Windows 실행 파일입니다.</p></td>
<td><p>.w16</p></td>
</tr>
<tr class="even">
<td><p>디스크 운영 체제 파일입니다.</p></td>
<td><p>.dos</p></td>
</tr>
<tr class="odd">
<td><p>European Institute for Computer Antivirus Research 표준 바이러스 백신 테스트 파일입니다.</p></td>
<td><p>.com</p></td>
</tr>
<tr class="even">
<td><p>Windows 프로그램 정보 파일입니다.</p></td>
<td><p>.pif</p></td>
</tr>
<tr class="odd">
<td><p>Windows 실행 프로그램 파일입니다.</p></td>
<td><p>.exe</p></td>
</tr>
</tbody>
</table>


## 지원되는 파일 형식의 수 확장

이 항목에 나오는 지원되는 파일 형식은 IFilter 통합을 사용하여 언제든지 수정할 수 있습니다. 자세한 내용은 [Exchange 2013으로 Filter Pack IFilter 등록](register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md)을 참조하십시오.

이 프로세스를 사용하여 추가한 파일 형식은 지원되는 파일 형식이 되며 `AttachmentIsUnsupported` 조건을 트리거하지 않습니다.

## 데이터 손실 방지 정책 및 첨부 파일 전송 규칙

전자 메일에 포함된 중요한 비즈니스 정보를 관리하기 위해 첨부 파일 관련 조건과 DLP(데이터 손실 방지) 정책의 규칙을 포함할 수 있습니다. 예를 들어 암호 번호가 있는 메시지는 암호로 보호된 첨부 파일에 포함되어 있는 경우에만 전송되도록 할 수 있습니다. 이렇게 하려면 다음을 수행하세요.

  - 암호 관련 중요 정보가 있는지 메일을 조사하는 DLP 정책을 만듭니다. 자세한 내용은 [DLP 절차](dlp-procedures-exchange-2013-help.md)를 참조하세요.

  - **다음의 경우 제외...** 전송 규칙 영역에 **첨부 파일이 암호로 보호됨** 예외를 추가합니다.

  - 암호 번호가 보호된 파일에 들어 있지 않은 메일에 대해 수행할 작업을 정의합니다.

DLP 정책 및 첨부 파일 관리 조건은 비즈니스 요구를 전송 규칙 조건, 예외 및 작업으로 정의하여 이러한 비즈니스 요구를 적용하는 데 도움이 될 수 있습니다. 중요한 정보 조사를 DLP 정책에 포함하면 메시지 첨부 파일에서 해당 정보만 조사됩니다. 그렇지만 크기 또는 파일 형식과 같은 첨부 파일 관련 조건은 이 항목에 표시된 조건을 추가해야만 포함됩니다. DLP는 모든 Exchange 버전에서 사용할 수 있습니다. 자세한 내용은 [데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)를 참조하세요.

## 자세한 내용

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[전송 규칙 조건 (조건자)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[메일 흐름 규칙을 사용 하 여 Office 365의 메시지 첨부 파일을 검사 하려면](https://technet.microsoft.com/ko-kr/library/jj919236\(v=exchg.150\)) in Exchange Online

