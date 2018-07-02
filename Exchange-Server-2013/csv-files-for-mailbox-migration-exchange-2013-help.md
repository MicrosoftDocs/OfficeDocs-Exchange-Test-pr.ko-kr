---
title: '사서함 마이그레이션에 대 한 CSV 파일: Exchange 2013 Help'
TOCTitle: 사서함 마이그레이션에 대 한 CSV 파일
ms:assetid: e67b3455-3946-4335-b80c-97823c76ac54
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn170437(v=EXCHG.150)
ms:contentKeyID: 54651804
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 마이그레이션에 대 한 CSV 파일

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-11-16_

대량을 CSV 파일을 사용할 수 많은 수의 사용자 사서함을 마이그레이션합니다. 마이그레이션 일괄 처리를 만들려면 Exchange 관리 셸 에서 Exchange 관리 센터 (EAC) 또는 **New-MigrationBatch** cmdlet을 사용 하는 경우 CSV 파일을 지정할 수 있습니다. 여러 사용자를 마이그레이션하는 마이그레이션 일괄 처리를 지정 하는 CSV를 사용 하 여 다음과 같은 마이그레이션 시나리오에서 지원 됩니다.

  - **온-프레미스 Exchange 조직에서의 이동**
    
      - **로컬 이동:**  로컬 이동 다른 하나 이상의 사서함 데이터베이스에서 사서함을 이동 하는 위치입니다. 로컬 이동 단일 포리스트 내에 발생합니다.
    
      - **엔터프라이즈 크로스 포리스트 이동:**  엔터프라이즈 크로스 포리스트 이동, 다른 포리스트에으로 사서함 이동 합니다. 사서함을 이동 하려면 포리스트는 대상 포리스트 또는 원본 포리스트의 포리스트 현재 사서함을 호스트 하는 크로스 포리스트 이동 시작 됩니다.

  - **온보딩 및 오프보딩(Exchange Online)**
    
      - **온 보 딩 원격 이동 마이그레이션:**  Exchange 하이브리드 배포에서 Exchange Online 를 온-프레미스 Exchange 조직에서 사서함을 이동할 수 있습니다. 이런 현상이도 알려져 있는 *온 보 딩* 원격 이동 마이그레이션 온보드 사서함 Exchange Online 수 있습니다.
    
      - **오프보딩 원격 이동 마이그레이션:**  Exchange Online 사서함을 온-프레미스 Exchange 조직으로 마이그레이션하는 *오프보딩* 원격 이동 마이그레이션을 수행할 수도 있습니다.
        

        > [!NOTE]
        > 온보딩 및 오프보딩 원격 이동 마이그레이션은 모두 Exchange Online 조직에서 시작됩니다.

    
      - **미리 구성 된 Exchange 마이그레이션:**  또한 Exchange Online 를 온-프레미스 Exchange 조직에서 사서함의 하위 집합을 마이그레이션할 수 있습니다. 다른 종류의 온 보 딩 마이그레이션입니다. Exchange 2003 및 Exchange 2007 사서함만 Exchange 미리 구성 된 마이그레이션을 사용 하 여 마이그레이션할 수 있습니다. Exchange 2010 및 Exchange 2013 마이그레이션 사서함 미리 구성 된 마이그레이션을 사용 하 여 지원 되지 않습니다. 미리 구성 된 마이그레이션을 실행 하기 전에 Exchange Online 조직에서 디렉터리 동기화 또는 프로 비전 메일 사용자에 게 다른 방법을 사용 해야 합니다.
    
      - **IMAP 마이그레이션:**  이 온 보 딩 마이그레이션 유형을 Exchange Online 으로 ( Exchange 포함) IMAP 서버에서 사서함 데이터를 마이그레이션합니다. IMAP 마이그레이션에 대 한 사서함 데이터를 마이그레이션하기 전에 Exchange Online 에서 사서함을 프로 비전 해야 합니다.


> [!NOTE]
> 단독 Exchange 마이그레이션을 사용 하 여 CSV 파일을 모든 온-프레미스 사용자 사서함 Exchange Online 단일 일괄 처리에서로 마이그레이션됩니다 때문에 지원 하지 않습니다.



## 대량 이동 또는 마이그레이션용 CSV 파일에 지원되는 특성

CSV 파일의 머리글 행을 확인 하는 첫번째 행 사용 되는 마이그레이션 사용자 목록에 대 한 다음에 있는 행에 지정 된 특성 또는 필드의 이름입니다. 각 특성 이름은 쉼표로 구분 됩니다. 머리글 행에서 각 행 개별 사용자를 나타내며 마이그레이션에 대 한 필요한 정보를 제공 합니다. 각 개별 사용자 행의 특성은 머리글 행의 특성 이름와 같은 순서로에 있어야 합니다. 각 특성 값은 쉼표로 구분 합니다. 특정 레코드에 대 한 특성 값이 null 이면 해당 특성에 대 한 아무런 내용을 입력 하지 마십시오. 그러나 다음 특성에서 null 값을 구분 하려면 쉼표를 포함 하는 확인 합니다.

CSV 파일의 특성 값 EAC 또는 Exchange 관리 셸 마이그레이션 일괄 처리를 만들 때 해당 동일한 매개 변수를 사용 하는 경우 해당 매개 변수 값을 재정의 합니다. 자세한 내용과 예제에 대 한 CSV 파일의 특성 값이 마이그레이션 일괄 처리에 대 한 값을 재정의하는 섹션을 참조 하십시오.


> [!TIP]
> 모든 텍스트 편집기를 사용 하 여 CSV 파일을 만들 수 있습니다 있지만 Microsoft Excel와 같은 응용 프로그램을 사용 하는 간편 하 게 데이터를 가져올 및 구성 하 고 CSV 파일을 구성 합니다. CSV 파일을.csv 또는.txt 파일로 저장 해야 합니다.



다음 섹션에서는 각 마이그레이션 유형에 대 한 CSV 파일의 머리글 행에 대 한 지원 되는 특성에 설명 합니다. 각 섹션 필요한의 특성 및 설명을 사용 하 여 값을 예로 여부 각 지원 되는 특성을 나열 하는 테이블을 포함 합니다.


> [!NOTE]
> 다음 섹션에서 <EM>원본 환경</EM> 사용자 사서함 또는 데이터베이스의 현재 위치를 나타냅니다. <EM>대상 환경</EM> 으로 이동할 사서함 데이터베이스 또는 사서함으로 마이그레이션되는 위치를 나타냅니다.



## 로컬 이동

다음 표에서 로컬 이동에 대 한 CSV 파일에 대 한 지원 되는 특성을 설명합니다. 자세한 내용은 [온-프레미스 이동 관리](manage-on-premises-moves-exchange-2013-help.md)을 참조 하십시오.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>특성</th>
<th>필수 또는 옵션</th>
<th>사용할 수 있는 값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>필수</p></td>
<td><p>사용자의 SMTP 주소</p></td>
<td><p>이동할 사용자를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>옵션</p></td>
<td><p>데이터베이스 이름</p></td>
<td><p>사용자의 기본 사서함으로 이동할 사서함 데이터베이스를 지정 합니다. 다른 데이터베이스를 동일한 마이그레이션 일괄 처리의 사서함을 이동 하는데 사용할 수 있는 CSV 파일의 다른 행에 있는 다른 데이터베이스를 지정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>옵션</p></td>
<td><p>데이터베이스 이름</p></td>
<td><p>사용자의 보관 사서함 (있는 경우)으로 이동할 사서함 데이터베이스를 지정 합니다. 다른 데이터베이스를 동일한 마이그레이션 일괄 처리의 보관 사서함을 이동 하는데 사용할 수 있는 CSV 파일의 다른 행에 있는 다른 데이터베이스를 지정할 수 있습니다.</p>

> [!NOTE]
> 보관 데이터베이스를 지정 하지 않으면 하는 경우 기본 사서함와 동일한 데이터베이스의 보관 사서함 이동 됩니다.


</td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>옵션</p></td>
<td><p><code>Unlimited</code> 또는 <code>0</code>(기본값)에서 <code>2147483647</code>(최대값) 사이의 음수가 아닌 정수</p></td>
<td><p>마이그레이션 서비스에서 사서함에 손상 된 항목을 발견 하는 경우에 건너뛸 잘못 된 항목 수를 지정 합니다. CSV 파일에서이 특성을 포함 하는 경우 기본값 또는 EAC 또는 Exchange 관리 셸 를 사용 하 여 마이그레이션 일괄 처리를 만들 때 <em>BadItemLimit</em> 매개 변수를 포함 하는 경우 사용자가 지정한 값을 재정의 합니다.</p>

> [!TIP]
> 기본값인 0을 사용하고 특정 사용자에 대한 이동이나 마이그레이션이 실패하는 경우에만 해당 사용자에 대해 잘못된 항목 제한 값을 높이는 것이 좋습니다.


<p></p></td>
</tr>
<tr class="odd">
<td><p>MailboxType</p></td>
<td><p>옵션</p></td>
<td><p>다음 값 중 하나를 사용합니다.</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code>(기본값)</p></li>
</ul></td>
<td><p>사용자의 기본 사서함, 보관 사서함 또는 둘 모두 이동 하려면 여부를 지정 합니다.</p></td>
</tr>
</tbody>
</table>


## 하이브리드 배포의 온보딩 원격 이동 마이그레이션

하이브리드 배포에서 Exchange Online 를 온-프레미스 Exchange 조직에서 사서함을 이동할 수 있습니다. 때 온 보 딩 사서함이 마이그레이션 일괄 처리 Exchange Online 조직에서 생성 하 고 Exchange Online 관리자가 시작 됩니다. 자세한 내용은 [하이브리드 배포에서 온-프레미스 및 Exchange Online 조직 간의 사서함 이동](https://technet.microsoft.com/ko-kr/library/jj906432\(v=exchg.150\))을 참조 하십시오.

다음 표에서는 온보딩 원격 이동 마이그레이션을 위한 CSV 파일에서 지원되는 특성을 설명합니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>특성</th>
<th>필수 또는 옵션</th>
<th>사용할 수 있는 값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>필수</p></td>
<td><p>사용자의 SMTP 주소</p></td>
<td><p>마이그레이션할 온-프레미스 사용자 사서함에 해당되는 Exchange Online 조직의 메일 사용 가능 사용자에 대한 전자 메일 주소를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>옵션</p></td>
<td><p><code>Unlimited</code> 또는 <code>0</code>(기본값)에서 <code>2147483647</code>(최대값) 사이의 음수가 아닌 정수</p></td>
<td><p>마이그레이션 서비스에서 사서함에 손상 된 항목을 발견 하는 경우에 건너뛸 잘못 된 항목 수를 지정 합니다. CSV 파일에서이 특성을 포함 하는 경우 기본값 또는 EAC 또는 Exchange 관리 셸 를 사용 하 여 마이그레이션 일괄 처리를 만들 때 <em>BadItemLimit</em> 매개 변수를 포함 하는 경우를 지정 하는 값을 재정의 합니다.</p>

> [!TIP]
> 기본값인 0을 사용하고 특정 사용자에 대한 이동이나 마이그레이션이 실패하는 경우에만 해당 사용자에 대해 잘못된 항목 제한 값을 높이는 것이 좋습니다.


</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>옵션</p></td>
<td><p><code>Unlimited</code> 또는 <code>0</code>(기본값)에서 최대값 사이의 음수가 아닌 정수</p></td>
<td><p>건너뜁니다 사용자의 사서함에서 큰 항목 수를 지정 합니다. 큰 항목 수가이 값을 초과 하면 사서함에 대 한 마이그레이션이 실패 합니다.</p>
<p>기본값은 0입니다. 즉, 사서함에 크기 제한 초과 항목이 하나라도 있으면 마이그레이션이 실패합니다.</p>
<p>Exchange Online으로 사서함을 온보딩할 때는 최대 35MB의 항목이 마이그레이션됩니다.</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>옵션</p></td>
<td><p>다음 값 중 하나를 사용합니다.</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code>(기본값)</p></li>
</ul></td>
<td><p>사용자의 기본 사서함, 보관 사서함 또는 둘 모두 이동 하려면 여부를 지정 합니다.</p></td>
</tr>
</tbody>
</table>


## 하이브리드 배포의 포리스트 간 엔터프라이즈 이동 및 오프보딩 원격 이동 마이그레이션

앞서 설명한 것, 크로스 포리스트 이동 대상 포리스트 또는 원본 포리스트의에서 시작한 됩니다. 오프 보 딩 원격 이동 마이그레이션 Exchange Online 조직에서 시작 됩니다. 자세한 내용은 다음을 참조 합니다.

  - [크로스 포리스트 이동 요청에 대 한 사서함을 준비](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [하이브리드 배포에서 온-프레미스 및 Exchange Online 조직 간의 사서함 이동](https://technet.microsoft.com/ko-kr/library/jj906432\(v=exchg.150\))

다음 표에서는 Exchange 하이브리드 배포의 포리스트 간 엔터프라이즈 이동 및 오프보딩 원격 이동 마이그레이션을 위한 CSV 파일에서 지원되는 특성을 설명합니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>특성</th>
<th>필수 또는 옵션</th>
<th>사용할 수 있는 값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>필수</p></td>
<td><p>사용자의 SMTP 주소</p></td>
<td><p>포리스트 간 엔터프라이즈 이동의 경우 이 특성은 원본 포리스트의 사서함 또는 메일 사용 가능 사용자를 지정합니다.</p>
<p>오프보딩 원격 이동 마이그레이션의 경우에는 Exchange Online 사서함을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>원본 포리스트에서 시작 되는 엔터프라이즈 크로스 포리스트 이동 및 오프 보 딩 원격 이동 마이그레이션에 대 한 필요 합니다. 또는 EAC 또는 Exchange 관리 셸 를 사용 하 여 마이그레이션 일괄 처리를 만들 때이 특성을 지정할 수 있습니다.</p>
<p>대상 포리스트에서 시작되는 포리스트 간 엔터프라이즈 이동의 경우 이 특성은 옵션입니다.</p></td>
<td><p>데이터베이스 이름</p></td>
<td><p>사용자의 기본 사서함을 이동할 대상 포리스트의 사서함 데이터베이스를 지정 합니다. 다른 데이터베이스를 동일한 마이그레이션 일괄 처리의 사서함을 이동 하는데 사용할 수 있는 CSV 파일의 다른 행에 있는 다른 데이터베이스를 지정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>옵션</p></td>
<td><p>데이터베이스 이름</p></td>
<td><p>사용자의 보관 사서함을 이동할 대상 포리스트의 사서함 데이터베이스를 지정 합니다. 다른 데이터베이스를 동일한 마이그레이션 일괄 처리의 보관 사서함을 이동 하는데 사용할 수 있는 CSV 파일의 다른 행에 있는 다른 데이터베이스를 지정할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>옵션</p></td>
<td><p><code>Unlimited</code> 또는 <code>0</code>(기본값)에서 <code>2147483647</code>(최대값) 사이의 음수가 아닌 정수</p></td>
<td><p>마이그레이션 서비스에서 사서함에 손상 된 항목을 발견 하는 경우에 건너뛸 잘못 된 항목 수를 지정 합니다. CSV 파일에서이 특성을 포함 하는 경우 기본값 또는 EAC 또는 Exchange 관리 셸 를 사용 하 여 마이그레이션 일괄 처리를 만들 때 <em>BadItemLimit</em> 매개 변수를 포함 하는 경우를 지정 하는 값을 재정의 합니다.</p>

> [!TIP]
> 기본값인 0을 사용하고 특정 사용자에 대한 이동이나 마이그레이션이 실패하는 경우에만 해당 사용자에 대해 잘못된 항목 제한 값을 높이는 것이 좋습니다.


</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>옵션</p></td>
<td><p><code>Unlimited</code> 또는 <code>0</code>(기본값)에서 최대값 사이의 음수가 아닌 정수</p></td>
<td><p>건너뜁니다 사용자의 사서함에서 큰 항목 수를 지정 합니다. 큰 항목 수가이 값을 초과 하면 사서함에 대 한 마이그레이션이 실패 합니다.</p>
<p>기본값은 0입니다. 즉, 사서함에 크기 제한 초과 항목이 하나라도 있으면 마이그레이션이 실패합니다.</p>
<p>Exchange Online으로 사서함을 온보딩할 때는 최대 35MB의 항목이 마이그레이션됩니다.</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>옵션</p></td>
<td><p>다음 값 중 하나를 사용합니다.</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code>(기본값)</p></li>
</ul></td>
<td><p>사용자의 기본 사서함, 보관 사서함 또는 둘 모두 이동 하려면 여부를 지정 합니다.</p></td>
</tr>
</tbody>
</table>


## 미리 구성된 Exchange 마이그레이션

CSV 파일을 사용 하 여 Exchange 2003으로 마이그레이션하는 미리 구성 된 Exchange 마이그레이션을 사용 하 여 원하는 및 Exchange 2007 온-프레미스 사서함을 Exchange Online 때 마이그레이션 일괄 처리에 대 한 사용자의 그룹을 식별 해야 합니다. 미리 구성 된 Exchange 마이그레이션을 사용 하 여 클라우드로 마이그레이션할 수 있는 사서함의 수에 대 한 제한이 없습니다. 그러나 마이그레이션 일괄 처리에 대 한 CSV 파일에는 1, 000 행의 최대를 포함할 수 있습니다. 1, 000 개 이상의 사서함을 마이그레이션할 추가 CSV 파일을 만들고 다음 각 하나를 사용 하 여 새 마이그레이션 일괄 처리 만들기 해야 합니다. 미리 구성 된 Exchange 마이그레이션에 대 한 자세한 내용은 [미리 구성 된 마이그레이션와 Exchange Online으로 사서함 마이그레이션](https://technet.microsoft.com/ko-kr/library/jj874018\(v=exchg.150\))을 참조 하십시오.

다음 표에서는 미리 구성된 Exchange 마이그레이션을 위한 CSV 파일에서 지원되는 특성을 설명합니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>특성</th>
<th>필수 또는 옵션</th>
<th>사용할 수 있는 값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>필수</p></td>
<td><p>사용자의 SMTP 주소</p></td>
<td><p>마이그레이션되는 온-프레미스 사용자 사서함에 해당 하는 Exchange Online 에서 메일 사용이 가능한 사용자 (또는 사서함 마이그레이션을 다시 시도 하는 경우)에 대 한 전자 메일 주소를 지정 합니다. 메일 사용이 가능한 사용자가 디렉터리 동기화의 결과 Exchange Online 또는 다른 프로 비전 프로세스에 생성 됩니다. 메일 사용이 가능한 사용자의 전자 메일 주소에는 해당 온-프레미스 사서함에 대 한 <em>WindowsEmailAddress</em> 속성은 일치 해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>Password</p></td>
<td><p>옵션</p></td>
<td><p>8자 이상이며 Office 365 조직에 적용되는 암호 제한을 충족하는 암호</p></td>
<td><p>마이그레이션 중에 Exchange Online의 해당 메일 사용 가능 사용자가 사서함으로 변환되면 해당 사용자 계정에 대해 이 암호가 설정됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>ForceChangePassword</p></td>
<td><p>옵션</p></td>
<td><p><code>True</code> 또는 <code>False</code></p></td>
<td><p>사용자가 Exchange Online 사서함에 처음 로그인할 때 암호를 변경해야 하는지 여부를 지정합니다.</p>

> [!NOTE]
> 온-프레미스 조직에서 Active Directory Federation Services 2.0 (AD FS 2.0)를 배포 하 여 single sign-on 솔루션을 구현한을 하는 경우에이 특성의 값에 대 한 <CODE>False</CODE> 를 사용 해야 합니다.


</td>
</tr>
</tbody>
</table>


## IMAP 마이그레이션

IMAP 마이그레이션 일괄 처리에 대 한 CSV 파일에는 최대 50, 000 행의 가질 수 있습니다. 하지만 여러 더 작은 일괄 처리에서 사용자를 마이그레이션하는 것이 좋습니다. IMAP 마이그레이션에 대 한 자세한 내용은 다음 항목을 참조 하십시오.

  - [IMAP 서버에서 Exchange Online 사서함으로 전자 메일 마이그레이션](https://technet.microsoft.com/ko-kr/library/jj874015\(v=exchg.150\))

  - [IMAP 마이그레이션 일괄 처리에 대 한 CSV 파일](https://technet.microsoft.com/ko-kr/library/jj200730\(v=exchg.150\))

다음 표에서는 IMAP 마이그레이션을 위한 CSV 파일에서 지원되는 특성을 설명합니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>특성</th>
<th>필수 또는 옵션</th>
<th>사용할 수 있는 값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>필수</p></td>
<td><p>사용자의 SMTP 주소</p></td>
<td><p>사용자의 Exchange Online 사서함에 대한 사용자 ID를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p>UserName</p></td>
<td><p>필수</p></td>
<td><p>IMAP 서버에서 지원하는 형식으로 IMAP 메시징 시스템의 사용자를 식별하는 문자열</p></td>
<td><p>IMAP 메시징 시스템 (원본 환경)에서 사용자의 계정에 대 한 로그온 이름을 지정합니다. 사용자 이름 외에도 IMAP 서버에서 사서함에 액세스 하는데 필요한 권한을 할당 된 계정의 자격 증명을 사용할 수 있습니다. 자세한 내용은 <a href="https://technet.microsoft.com/ko-kr/library/jj200730(v=exchg.150)">IMAP 마이그레이션 일괄 처리에 대 한 CSV 파일</a>을 참조 하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>Password</p></td>
<td><p>필수</p></td>
<td><p>암호 문자열</p></td>
<td><p>UserName 특성으로 지정된 사용자 계정의 암호를 지정합니다.</p></td>
</tr>
</tbody>
</table>


## 마이그레이션 일괄 처리의 값을 재정의하는 CSV 파일의 특성 값

CSV 파일의 특성 값 EAC 또는 Exchange 관리 셸 마이그레이션 일괄 처리를 만들 때 해당 동일한 매개 변수를 사용 하는 경우 해당 매개 변수 값을 재정의 합니다. 사용자에 게 적용할 마이그레이션 일괄 처리 값을 원하는 CSV 파일에 빈 그 셀을 남길이 있습니다. 이렇게 하면을 혼합 하 고 하나의 마이그레이션 일괄 처리에서 선택한 사용자에 대 한 특정 특성 값과 일치 합니다.

예 한다고 가정 하면 만들어보겠습니다 일괄 처리를 엔터프라이즈 크로스 포리스트 이동 하려면 이동 사용자의 기본 및 다음 Exchange 관리 셸 명령 사용 하 여 대상 포리스트를 보관 사서함에 대 한 Exchange 관리 셸 에서 합니다.

    New-MigrationBatch -Name CrossForestBatch1 -SourceEndpoint ForestEndpoint1 -TargetDeliveryDomain forest2.contoso.com -TargetDatabases @(EXCH-MBX-02,EXCH-MBX-03) -TargetArchiveDatabases @(EXCH-MBX-A02,EXCH-MBX-A03) -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\CrossForestBatch1.csv")) -AutoStart


> [!NOTE]
> 기본 이동 및 보관 사서함 기본 이기 때문에 명시적으로 Exchange 관리 셸 명령에 지정할 필요가 없습니다.



CrossForestBatch1.csv 파일에서 이 마이그레이션 일괄 처리를 위한 부분은 다음과 같습니다.

    EmailAddress,TargetDatabase,TargetArchiveDatabase
    user1@contoso.com,EXCH-MBX-01,EXCH-MBX-A01
    user2@contoso.com,,
    user3@contoso.com,EXCH-MBX-01,
    ...

CSV 파일의 값이 기본 마이그레이션 일괄 처리에 대 한 값을 재정의 하 고 대상 포리스트에서 각각 c h X-MBX-01 및 EXCH-MBX-a 01 user1에 대 한 보관 사서함이 이동 합니다. 기본 및 사용자 2에 대 한 보관 사서함 EXCH-MBX-02 또는 EXCH-MBX-03으로 이동 됩니다. C h X-MBX-01에 user3에 대 한 기본 사서함이 이동 하 고 EXCH-MBX-A02 또는 EXCH-MBX-A03으로 보관 사서함이 이동 합니다.

다른 예에 다음 명령을 사용 하 여 Exchange Online 보관 사서함을 이동 하는 하이브리드 배포에는 온 보 딩 원격 이동 마이그레이션에 대 한 일괄 처리를 만들 가정해 보겠습니다.

    New-MigrationBatch -Name OnBoarding1 -SourceEndpoint RemoteEndpoint1 -TargetDeliveryDomain cloud.contoso.com -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\OnBoarding1.csv")) -MailboxType ArchiveOnly -AutoStart

단, 이 경우에는 선택한 사용자의 기본 사서함도 이동하려고 합니다. 따라서 OnBoarding1.csv 파일에서 이 마이그레이션 일괄 처리에 해당하는 부분은 다음과 같습니다.

    EmailAddress,MailboxType
    user1@contoso.com,
    user2@contoso.com,
    user3@cloud.contoso.com,PrimaryAndArchive
    user4@cloud.contoso.com,PrimaryAndArchive
    ...

CSV 파일의 사서함 형식에 대 한 값 명령 일괄 처리 만들기에 *MailboxType* 매개 변수의 값을 재정의 하는 경우 때문에 1 및 사용자 2에 대 한 보관 사서함은 Exchange Online 로 마이그레이션됩니다. 하지만 기본 user3 및 user4에 대 한 보관 사서함 Exchange Online 로 이동 됩니다.

