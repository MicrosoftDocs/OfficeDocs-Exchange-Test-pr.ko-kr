---
title: '가져오기 주소 다시 쓰기 항목 Edge 전송 서버에서: Exchange 2013 Help'
TOCTitle: 가져오기 주소 다시 쓰기 항목 Edge 전송 서버에서
ms:assetid: bd0942c6-9c66-4b4c-b9bc-2f5f783def76
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb331966(v=EXCHG.150)
ms:contentKeyID: 61060549
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 가져오기 주소 다시 쓰기 항목 Edge 전송 서버에서

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

CSV(쉼표로 구분된 값) 파일을 사용하여 주소 다시 쓰기 정보를 대량으로 만들거나 Edge 전송 서버로 가져올 수 있습니다. 다음 목록에서는 이 작업을 수행해야 하는 일반적인 시나리오에 대해 설명합니다.

  - 주소 다시 쓰기 솔루션을 Edge 전송 서버로 대체하는 경우

  - 타사 솔루션 공급자와 계약을 체결하여 해당 공급자의 전자 메일 주소를 다시 써야 하는 경우

  - 다른 조직을 인수하여 인수 대상 조직의 전자 메일 주소를 일시적으로 다시 써야 하는 경우

메모장 등의 텍스트 편집기나 Microsoft Excel 등의 응용 프로그램을 사용하여 CSV 파일을 만들 수 있습니다. 이 항목에 설명된 대로 파일 서식을 지정하여 .csv 파일로 저장합니다.

CSV 파일의 첫 번째 행(*머리글 행*이라고도 함)에는 매개 변수 이름이 나열됩니다. 각 매개 변수는 쉼표로 구분됩니다. 다음 표에서는 필수 매개 변수와 선택적 매개 변수에 대해 설명합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>필수 또는 옵션</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>필수</p></td>
<td><p>주소 다시 쓰기 항목을 설명하는 고유한 이름입니다.</p></td>
</tr>
<tr class="even">
<td><p><em>InternalAddress</em></p></td>
<td><p>필수</p></td>
<td><p>변경할 주소입니다. 다음 값을 사용할 수 있습니다.</p>
<ul>
<li><p>단일 전자 메일 주소(chris@contoso.com)</p></li>
<li><p>단일 도메인 또는 하위 도메인(contoso.com 또는 sales.contoso.com)</p></li>
<li><p>도메인 및 모든 하위 도메인(*.contoso.com)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAddress</em></p></td>
<td><p>필수</p></td>
<td><p>사용하려는 최종 전자 메일 주소입니다. 다음 값을 사용할 수 있습니다.</p>
<ul>
<li><p><em>InternalAddress</em>에 대한 단일 전자 메일 주소를 지정한 경우 단일 전자 메일 주소</p></li>
<li><p>기타 모든 <em>InternalAddress</em> 값의 경우 단일 도메인 또는 하위 도메인</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ExceptionList</em></p></td>
<td><p>선택</p></td>
<td><p>도메인 및 모든 하위 도메인(*.contoso.com)의 전자 메일 주소를 다시 쓰는 경우에만 사용 가능합니다. 주소 다시 쓰기에서 제외할 하나 이상의 하위 도메인을 지정합니다. 값은 큰따옴표로 묶고 값이 여러 개이면 쉼표로 구분합니다. 예: <code>&quot;marketing.contoso.com&quot;</code> 또는 <code>&quot;marketing.contoso.com,legal.contoso.com&quot;</code></p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundOnly</em></p></td>
<td><p>선택</p></td>
<td><p><code>False</code>로 지정하면 인바운드 및 아웃바운드 메일에서 주소를 다시 씁니다. <code>True</code>로 지정하면 아웃바운드 메일에서만 주소를 다시 쓰며, 해당되는 받는 사람에 대해 다시 쓴 전자 메일 주소를 프록시 주소로 수동 구성해야 합니다.</p>
<p>기본값은 <code>False</code>이지만 <em>InternalAddress</em>에 *.contoso.com과 같이 와일드카드 문자가 포함되어 있으면 값을 <code>True</code>로 설정해야 합니다.</p>
<p>CSV 파일의 <em>OutboundOnly</em> 매개 변수 값은 <code>$True</code> 또는 <code>$False</code>가 아니라 <code>True</code> 또는 <code>False</code>입니다.</p></td>
</tr>
</tbody>
</table>


머리글 행 아래의 각 행은 개별 주소 다시 쓰기 항목을 나타냅니다. 각 행의 값은 머리글 행의 매개 변수 이름과 동일한 순서로 나열되어야 합니다. 각 값은 쉼표로 구분됩니다.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 30분

  - 주소 다시 쓰기의 결과를 이해해야 합니다. 예를 들어 다시 쓴 전자 메일 주소는 Exchange 조직에서 고유해야 하며 해당되는 받는 사람에 대해 프록시 주소를 구성해야 할 수 있습니다. 자세한 내용은 [주소 Edge 전송 서버에서 다시 쓰기](address-rewriting-on-edge-transport-servers-exchange-2013-help.md) 및 [Edge 전송 서버의 주소 다시 쓰기 관리](manage-address-rewriting-on-edge-transport-servers-exchange-2013-help.md)를 참조하세요.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "주소 다시 쓰기 에이전트" 항목

  - Edge 전송 서버가 두 개 이상 있을 경우 이 항목의 절차를 사용하여 주소 다시 쓰기 항목을 단일 Edge 전송 서버로 가져온 후 해당 Edge 전송 서버의 구성을 조직의 다른 Edge 전송 서버로 복제하는 것이 좋습니다. Edge 전송 서버를 복제하는 방법에 대한 자세한 내용은 [Edge 전송 서버 복제 된 구성](edge-transport-server-cloned-configuration-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: CSV 파일 만들기

CSV 파일을 만들 때는 다음 항목을 고려합니다.

  - CSV 파일에 선택적 매개 변수의 값을 지정하는 경우 모든 행에 해당 열 값이 포함되어야 합니다. 일부 항목에만 선택적 매개 변수가 포함된 여러 개의 주소 다시 쓰기 항목을 만들려는 경우 해당 주소 다시 쓰기 항목을 분리하여 두 개의 CSV 파일을 만든 후 각 CSV 파일을 별도로 가져와야 합니다.

  - CSV 파일에 ASCII가 아닌 문자가 포함되어 있는 경우에는 CSV 파일을 UTF-8 인코딩 또는 기타 유니코드 인코딩으로 저장해야 합니다. 응용 프로그램에 따라 컴퓨터의 시스템 로캘이 CSV 파일에 사용된 언어와 일치하는 경우 CSV 파일을 UTF-8 또는 다른 유니코드 인코딩으로 저장하는 것이 보다 간단할 수 있습니다.

다음 예에서는 선택적 *ExceptionList* 및 *OutboundOnly* 매개 변수를 포함하여 CSV 파일을 채울 수 있는 방법을 보여 줍니다.

    Name,InternalAddress,ExternalAddress,ExceptionList,OutboundOnly
    "Wingtip UK",*.wingtiptoys.co.uk,tailspintoys.com,"legal.wingtiptoys.co.uk,finance.wingtiptoys.co.uk,support.wingtiptoys.co.uk",True
    "Wingtip USA",*.wingtiptoys.com,tailspintoys.com,"legal.wingtiptoys.com,finance.wingtiptoys.com,support.wingtiptoys.com,corp.wingtiptoys.com",True
    "Wingtip Canada",*.wingtiptoys.ca,tailspintoys.com,"legal.wingtiptoys.ca,finance.wingtiptoys.ca,support.wingtiptoys.ca",True

## 2단계: CSV 파일 가져오기

CSV 파일을 가져오려면 다음 구문을 사용합니다.

    Import-Csv <FileNameAndPath> | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

이 예에서는 C:\\My Documents\\ImportAddressRewriteEntries.csv에서 주소 다시 쓰기 항목을 가져옵니다.

    Import-Csv "C:\My Documents\ImportAddressRewriteEntries.csv" | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

## 이 단계의 작동 여부는 어떻게 확인합니까?

CSV 파일에서 주소 다시 쓰기 항목을 가져왔는지 확인하려면 다음을 수행합니다.

1.  모든 주소 다시 쓰기 항목을 확인하려면 `Get-AddressRewriteEntry` 명령을 실행합니다.

2.  특정 주소 다시 쓰기 항목에 대한 세부 정보를 확인하려면 `Get-AddressRewriteEntry <AddressRewriteIdentity> | Format-List` 명령을 실행합니다.

