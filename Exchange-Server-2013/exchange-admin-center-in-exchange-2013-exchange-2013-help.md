---
title: 'Exchange 2013의 Exchange 관리 센터: Exchange 2013 Help'
TOCTitle: Exchange 2013의 Exchange 관리 센터
ms:assetid: a9aea11a-6ba3-4f4a-a76e-79072e7cfc7d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150562(v=EXCHG.150)
ms:contentKeyID: 50483839
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013의 Exchange 관리 센터

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-17_

EAC(Exchange 관리 센터)는 Microsoft Exchange Server 2013의 웹 기반 관리 콘솔로서, 온-프레미스, 온라인 또는 하이브리드 Exchange 배포에 최적화되어 있습니다. EAC는 Exchange Server 2010 관리에 사용한 두 인터페이스인 EMC(Exchange 관리 콘솔) 및 ECP(Exchange 제어판)를 대신합니다.

웹 기반 EAC의 장점 중 하나로 ECP IIS 가상 디렉터리 내에서 인터넷 및 인트라넷 액세스를 분할할 수 있다는 점을 들 수 있습니다. 이 기능을 사용하면 Outlook Web App 옵션에 대한 최종 사용자의 액세스는 여전히 허용하면서 조직 외부에서 인터넷을 통해 EAC에 액세스하려고 하는 사용자의 액세스는 제어할 수 있습니다. 자세한 내용은 [Exchange 관리 센터에 대 한 액세스를 해제](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md)를 참조하세요.

이 항목의 Exchange Online 버전은 [Exchange Online의 Exchange 관리 센터](https://technet.microsoft.com/ko-kr/library/jj200743\(v=exchg.150\))를 참조하세요.

이 항목의 Exchange Online Protection 버전은 [Exchange Online Protection의 Exchange 관리 센터](https://technet.microsoft.com/ko-kr/library/jj723141\(v=exchg.150\))를 참조하십시오.

목차

EAC 액세스

EAC의 공통 사용자 인터페이스 요소

지원되는 브라우저

## EAC 액세스

이제 EAC는 웹 기반 관리 콘솔이므로 이 콘솔에 액세스하려면 웹 브라우저에서 ECP 가상 디렉터리 URL을 사용해야 합니다. 대부분의 경우 EAC의 URL은 다음과 같습니다.

  - **내부 URL: `https://<CASServerName>/ecp`**   내부 URL은 조직 방화벽 내에서 EAC에 액세스하는 데 사용됩니다.

  - **외부 URL: `https://mail.contoso.com/ecp`**   외부 URL은 조직 방화벽 외부에서 EAC에 액세스하는 데 사용됩니다. 일부 조직에서는 EAC에 대한 외부 액세스를 해제해야 할 경우도 있습니다. 자세한 내용은 [Exchange 관리 센터에 대 한 액세스를 해제](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md)를 참조하세요.

[Get-EcpVirtualDirectory](https://technet.microsoft.com/ko-kr/library/dd351058\(v=exchg.150\)) cmdlet을 사용하면 EAC의 내부 또는 외부 URL을 찾을 수 있습니다. 자세한 내용은 [Exchange 관리 센터에 대 한 내부 및 외부 Url 찾기](find-the-internal-and-external-urls-for-the-exchange-admin-center-exchange-2013-help.md)를 참조하세요.

한 조직에서 Exchange 2010과 Exchange 2013을 함께 실행하며 사서함은 아직 Exchange 2010 사서함 서버에 있는 경우, 브라우저에서는 기본적으로 Exchange 2010 ECP를 표시합니다. Exchange 버전을 URL에 추가하면 EAC에 액세스할 수 있습니다. 예를 들어, 가상 디렉터리가 클라이언트 액세스 서버 CAS15-NA에서 호스트되는 EAC에 액세스하려면 다음 URL을 사용합니다. `https://CAS15-NA/ecp/?ExchClientVer=15` 반대로, 사서함이 Exchange 2013 사서함 서버에 있는 경우 Exchange 2010 ECP에 액세스하려면 다음 URL을 사용합니다. `https://CAS14-NA/ecp/?ExchClientVer=14`

## EAC의 공통 사용자 인터페이스 요소

이 섹션에서는 EAC에서 공통되는 사용자 인터페이스 요소에 대해 설명합니다.

![Exchange 관리 센터](images/JJ150562.cd617bc0-19ef-47d2-bba1-4e9546b12e0c(EXCHG.150).gif "Exchange 관리 센터")

## 크로스-프레미스 탐색

크로스-프레미스 탐색을 사용하면 Exchange Online과 온-프레미스 Exchange 배포 간에 쉽게 전환할 수 있습니다. Exchange Online 조직이 없으면 링크는 Office 365 등록 페이지로 연결됩니다. 자세한 내용은 [Exchange Server 하이브리드 배포](https://technet.microsoft.com/ko-kr/library/jj200581\(v=exchg.150\))를 참조하세요.

## 기능 창

이 창은 EAC에서 수행할 대부분의 작업에 대한 첫 번째 탐색 수준입니다. 기능 창은 Exchange 2010 EMC의 콘솔 트리와 유사합니다. 그러나 Exchange 2013의 기능 창은 서버 역할이 아니라 기능 영역별로 구성되어 있으며 더 적은 횟수의 클릭으로 필요한 기능을 찾을 수 있습니다.

  - **받는 사람** 이 기능을 통해 사서함, 그룹, 리소스 사서함, 연락처, 공유 사서함, 사서함 마이그레이션 및 이동을 관리할 수 있습니다.

  - **사용 권한** 이 기능을 통해 관리자 역할, 사용자 역할 및 Outlook Web App 정책을 관리할 수 있습니다.

  - **준수 관리** 이 기능을 통해 원본 위치 eDiscovery, 원본 위치 유지, 감사, DLP(데이터 손실 방지), 보존 정책, 보존 태그 및 저널 규칙을 관리할 수 있습니다.

  - **조직** 이 기능을 통해 페더레이션 공유, Outlook App, 주소 목록을 비롯하여 Exchange 조직과 관련된 작업을 관리할 수 있습니다.

  - **보호** 이 기능을 통해 조직의 맬웨어 방지를 관리할 수 있습니다.

  - **메일 흐름** 이 기능을 통해 규칙, 배달 보고서, 허용 도메인, 전자 메일 주소 정책, 송신 및 수신 커넥터를 관리할 수 있습니다.

  - **모바일** 이 기능을 통해 조직에 연결할 수 있는 모바일 장치를 관리할 수 있습니다. 모바일 장치 액세스와 모바일 장치 사서함 정책을 관리할 수 있습니다.

  - **공용 폴더** Exchange 2010의 경우에는 도구 상자에서 EMC의 외부에 있는 공용 폴더 관리 콘솔을 사용하여 공용 폴더를 관리해야 했습니다. Exchange 2013에서는 **공용 폴더** 기능 영역 내에서 공용 폴더를 관리할 수 있습니다.

  - **통합 메시징** 이 기능을 통해 UM 다이얼 플랜과 UM IP 게이트웨이를 관리할 수 있습니다.

  - **서버** 이 기능을 통해 사서함 및 클라이언트 액세스 서버, 데이터베이스, DAG(데이터베이스 사용 가능 그룹), 가상 디렉터리, 인증서를 관리할 수 있습니다.

  - **하이브리드** 이 기능을 통해 하이브리드 조직을 설정하고 구성할 수 있습니다.

## 탭

탭은 탐색의 두 번째 수준입니다. 각 기능 영역에는 각각의 전체 기능을 나타내는 다양한 탭이 있습니다. 이 규칙에서 유일한 예외는 하이브리드 기능 영역입니다. 먼저 하이브리드 구성 마법사를 사용하여 하이브리드 배포에 대해 조직을 사용하도록 설정해야 합니다.

## 도구 모음

대부분의 탭은 클릭하면 도구 모음이 표시됩니다. 도구 모음에는 특정 작업을 수행하는 아이콘이 있습니다. 다음 표에서는 가장 일반적인 아이콘과 해당 작업에 대해 설명합니다. 아이콘을 커서로 가리키면 아이콘과 관련된 작업이 표시됩니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>아이콘</th>
<th>이름</th>
<th>작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="아이콘 추가" alt="아이콘 추가" /></p></td>
<td><p>추가, 새로 만들기</p></td>
<td><p>이 아이콘을 사용하면 새 개체를 만들 수 있습니다. 일부 아이콘에는 아래쪽 화살표가 있으며 이 화살표를 클릭하면 만들 수 있는 추가 개체가 표시됩니다. 예를 들어 <strong>받는 사람</strong> &gt; <strong>사서함</strong>에서 아래쪽 화살표를 클릭하면 <strong>사용자 사서함</strong> 및 <strong>연결된 사서함</strong>이 추가 옵션으로 표시됩니다.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="편집 아이콘" alt="편집 아이콘" /></p></td>
<td><p>편집</p></td>
<td><p>이 아이콘을 사용하면 개체를 편집할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif" title="삭제 아이콘" alt="삭제 아이콘" /></p></td>
<td><p>삭제</p></td>
<td><p>이 아이콘을 사용하면 개체를 삭제할 수 있습니다. 일부 삭제 아이콘에는 아래쪽 화살표가 있으며 이 화살표를 클릭하면 추가 옵션이 표시됩니다.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif" title="검색 아이콘" alt="검색 아이콘" /></p></td>
<td><p>검색</p></td>
<td><p>이 아이콘을 사용하면 찾으려는 개체에 대한 검색어를 입력할 수 있는 검색 상자가 열립니다. 추가 검색 옵션을 보려면 <a href="https://technet.microsoft.com/ko-kr/library/jj156853(v=exchg.150)">[받는 사람 &gt;] 고급 검색</a>을 확인하세요.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="새로 고침 아이콘" alt="새로 고침 아이콘" /></p></td>
<td><p>새로 고침</p></td>
<td><p>이 아이콘을 사용하면 목록 보기를 새로 고칠 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="기타 옵션 아이콘" alt="기타 옵션 아이콘" /></p></td>
<td><p>기타 옵션</p></td>
<td><p>이 아이콘을 사용하면 해당 탭의 개체에 대해 수행할 수 있는 기타 작업을 볼 수 있습니다. 예를 들어 <strong>받는 사람</strong> &gt; <strong>사서함</strong>에서 이 아이콘을 클릭하면 <strong>사용 안 함</strong>, <strong>열 추가/제거</strong>, <strong>CSV 파일로 데이터 내보내기</strong>, <strong>사서함 연결</strong> 및 <strong>고급 검색</strong> 옵션이 표시됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif" title="위쪽 화살표 아이콘" alt="위쪽 화살표 아이콘" /> <img src="images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif" title="아래쪽 화살표 아이콘" alt="아래쪽 화살표 아이콘" /></p></td>
<td><p>위쪽 화살표와 아래쪽 화살표</p></td>
<td><p>이 아이콘을 사용하면 개체 우선 순위를 위나 아래로 이동할 수 있습니다. 예를 들어 <strong>메일 흐름</strong> &gt; <strong>전자 메일 주소 정책</strong>에서 위쪽 화살표를 클릭하면 전자 메일 주소 정책의 우선 순위가 높아집니다. 이러한 화살표를 사용하여 공용 폴더 계층을 탐색하고 규칙을 목록 보기에서 위나 아래로 이동할 수도 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif" title="복사 아이콘" alt="복사 아이콘" /></p></td>
<td><p>복사</p></td>
<td><p>이 아이콘을 사용하면 원래 개체를 변경하는 대신 개체를 복사하여 변경할 수 있습니다. 예를 들어 <strong>사용 권한</strong> &gt; <strong>관리 역할</strong>의 목록 보기에서 역할을 선택하고 이 아이콘을 클릭하면 기존 역할을 기반으로 새 역할 그룹을 만들 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif" title="아이콘 제거" alt="아이콘 제거" /></p></td>
<td><p>제거</p></td>
<td><p>이 아이콘을 사용하면 목록에서 항목을 제거할 수 있습니다. 예를 들어 <strong>공용 폴더 사용 권한</strong> 대화 상자에서 사용자를 선택하고 이 아이콘을 클릭하면 공용 폴더에 대한 액세스가 허용되는 사용자 목록에서 사용자를 제거할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


## 목록 보기

탭을 선택하면 대부분의 경우 목록 보기가 표시됩니다. EAC의 목록 보기는 ECP에서의 제한을 극복하도록 설계되었습니다. ECP에서는 개체를 500개까지만 표시할 수 있고, 세부 정보 창에 표시되지 않은 개체를 보려면 해당 개체를 찾기 위한 검색 및 필터 옵션을 사용해야 합니다. Exchange 2013에서는 EAC 목록 보기 내에서 약 20,000개의 온-프레미스 배포용 개체와 Exchange Online의 10,000개 개체를 볼 수 있습니다. 또한 결과로 페이징할 수 있도록 페이징이 포함되어 있습니다. **받는 사람** 목록 보기에서는 페이지 크기를 구성하고 데이터를 CSV 파일로 내보낼 수도 있습니다.

## 세부 정보 창

목록 보기에서 개체를 선택하면 해당 개체에 대한 정보가 세부 정보 창에 표시됩니다. 받는 사람 개체를 사용하는 등 일부 경우에는 세부 정보 창에 빠른 관리 작업이 포함됩니다. 예를 들어 **받는 사람** \> **사서함**으로 이동하여 목록 보기에서 공유 사서함을 선택하면 해당 사서함에 대해 보관함을 사용하거나 사용하지 않도록 설정하는 옵션이 세부 정보 창에 표시됩니다. 여러 개체를 대량 편집하는 데에도 세부 정보 창을 사용할 수 있습니다. Ctrl 키를 누르고 대량 편집할 개체를 선택한 후 세부 정보 창의 옵션을 사용하면 됩니다. 예를 들어 여러 사서함을 선택하면 사용자의 연락처 및 조직 정보, 사용자 지정 특성, 사서함 할당량, Outlook Web App 설정 등에 대한 대량 업데이트가 가능합니다.

## 알림

EAC에는 오래 실행되는 프로세스의 상태를 표시하고 프로세스가 완료될 때 알림을 제공하는 알림 뷰어가 있습니다. 또한 이동 요청과 같이 특히 오래 실행되는 프로세스의 경우 전자 메일 알림을 받도록 선택할 수 있습니다.

## 내 소식 타일 및 도움말

*내 타일*을 사용하여 EAC에서 로그아웃하고 다른 사용자로 로그인할 수 있습니다. 도움말 ![도움말 아이콘](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "도움말 아이콘") 드롭다운 메뉴에서 다음 작업을 수행할 수 있습니다.

  - **도움말**   온라인 도움말 내용을 보려면 ![도움말 아이콘](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "도움말 아이콘")을 클릭합니다.

  - **풍선형 도움말 사용 안 함**   풍선형 도움말에는 개체를 만들거나 편집할 때 필드에 대한 상황에 맞는 도움말이 표시됩니다. 풍선형 도움말을 끌 수 있으며, 풍선형 도움말을 사용하지 않도록 설정한 경우에는 켤 수 있습니다.

  - **저작권 및 개인 정보 보호 정책** 개인 정보 보호 정책 또는 저작권 링크를 클릭하여 Exchange 2013의 저작권 및 개인 정보 보호 정책 정보를 읽을 수 있습니다.

## 지원되는 브라우저

최적의 EAC 환경을 구축하려면 운영 체제 및 브라우저 조합 중 "프리미엄"이라는 레이블이 붙은 것을 사용합니다.


> [!NOTE]
> 위의 표에 나열되지 않은 기타 운영 체제 및 브라우저 조합은 지원되지 않습니다(터치 포함).



  - **프리미엄:**  모든 기능이 지원되고 완벽하게 테스트됩니다.

  - **지원:**  지원되는 기능은 프리미엄과 동일합니다. 그러나 브라우저 및 운영 체제 조합에서 지원하지 않는 기능이, 지원되는 브라우저에서 누락됩니다.

  - **미지원:**  브라우저 및 운영 체제가 지원되지 않거나 테스트되지 않습니다.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>웹 브라우저</p></td>
<td><p>Windows XP 및 Windows Server 2003</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows 7 및 Windows Server 2008</p></td>
<td><p>Windows 8 및 Windows Server 2012</p></td>
<td><p>Mac OSX</p></td>
<td><p>Linux</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p>지원</p></td>
<td><p>지원</p></td>
<td><p>프리미엄</p></td>
<td><p>미지원</p></td>
<td><p>미지원</p></td>
<td><p>미지원</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p>미지원</p></td>
<td><p>지원</p></td>
<td><p>프리미엄</p></td>
<td><p>미지원</p></td>
<td><p>미지원</p></td>
<td><p>미지원</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10 이상</p></td>
<td><p>미지원</p></td>
<td><p>지원</p></td>
<td><p>프리미엄</p></td>
<td><p>프리미엄</p></td>
<td><p>미지원</p></td>
<td><p>미지원</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 11 이상</p></td>
<td><p>지원</p></td>
<td><p>지원</p></td>
<td><p>프리미엄</p></td>
<td><p>프리미엄</p></td>
<td><p>프리미엄</p></td>
<td><p>지원</p></td>
</tr>
<tr class="even">
<td><p>Safari 5.1 이상</p></td>
<td><p>미지원</p></td>
<td><p>미지원</p></td>
<td><p>미지원</p></td>
<td><p>미지원</p></td>
<td><p>프리미엄</p></td>
<td><p>미지원</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 18 이상</p></td>
<td><p>지원</p></td>
<td><p>지원</p></td>
<td><p>프리미엄</p></td>
<td><p>프리미엄</p></td>
<td><p>프리미엄</p></td>
<td><p>미지원</p></td>
</tr>
</tbody>
</table>

