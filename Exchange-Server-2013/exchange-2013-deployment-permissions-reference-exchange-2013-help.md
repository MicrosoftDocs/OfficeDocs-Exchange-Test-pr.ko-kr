---
title: 'Exchange 2013 배포 권한 참조: Exchange 2013 Help'
TOCTitle: Exchange 2013 배포 권한 참조
ms:assetid: b13412d0-0cc4-4c1d-bf31-cae3d3e211a9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee681663(v=EXCHG.150)
ms:contentKeyID: 59635546
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 배포 권한 참조

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

이 항목에서는 Microsoft Exchange Server 2013 조직을 설정하는 데 필요한 사용 권한에 대해 설명합니다. 관리 역할 그룹과 연결된 USG(유니버설 보안 그룹)와 기타 Windows 보안 그룹 및 보안 주체는 다양한 Active Directory 개체의 ACL(액세스 제어 목록)에 추가됩니다. ACL은 각 개체에서 수행할 수 있는 작업을 제어합니다. 각 역할 그룹, 보안 그룹 또는 보안 주체에 부여되는 사용 권한을 이해하면 Exchange 2013을 설치하는 데 필요한 최소한의 사용 권한을 결정할 수 있습니다.

경우에 따라 ACL은 일반 속성인 **ntSecurityDescriptor**에는 적용되지 않고 **msExchMailboxSecurityDescriptor** 같은 다른 속성에 적용됩니다. 디렉터리 서비스는 Windows 보안 설명자에 지정되지 않은 보안을 적용할 수 없습니다. 대부분의 경우 이러한 ACL은 저장소 서비스가 적절한 개체에 ACL을 저장할 수 있도록 복제됩니다. 그러나 원시 이진 데이터 이외에는 이러한 ACL을 볼 수 있는 도구가 없습니다.

각 사용 권한 표의 열에는 다음 정보가 들어 있습니다.

  - **계정**   사용 권한이 부여되거나 거부된 보안 주체입니다.

  - **ACE 유형**   ACE(액세스 제어 항목) 유형입니다.
    
      - **허용 ACE**   허용 ACE는 ACE와 연결된 사용자 또는 그룹이 항목에 액세스하도록 허용합니다.
    
      - **거부 ACE**   거부 ACE는 ACE와 연결된 사용자 또는 그룹이 항목에 액세스하지 못하도록 합니다.

  - **상속**   자식 개체에 사용되는 상속의 유형입니다.
    
      - **모두**는 사용 권한이 개체 및 모든 하위 개체에 적용됨을 나타냅니다.
    
      - **설명**은 사용 권한이 속성/적용 대상 행에 나열된 개체 클래스에 적용됨을 나타냅니다.
    
      - **없음**은 해당 사용 권한이 개체에만 적용됨을 나타냅니다.

  - **사용 권한**   개체에 부여되는 사용 권한입니다.

  - **속성/적용 대상**   경우에 따라 사용 권한은 지정된 속성, 속성 집합 또는 개체 클래스에만 적용됩니다. 여기에는 이러한 제한된 사용 권한이 지정됩니다.

  - **설명**   적용되는 경우 이 열에서는 사용 권한이 필요한 이유를 설명하거나 사용 권한에 대한 기타 정보를 제공합니다.

사용 권한은 보통 **보기/편집** 탭의 **고급** 보기에 있는 ADSI(Active Directory 서비스 인터페이스) 편집(AdsiEdit.msc) **보안** 속성 페이지에서 사용되는 이름별로 표에 나열됩니다. ADSI 편집 **보안** 속성 페이지에는 사용 권한이 훨씬 압축되어 표시되어 있습니다. LDP 도구(Ldp.exe)는 액세스 마스크를 숫자 값으로 직접 표시합니다. 설치 코드는 미리 정의된 상수를 기준으로 사용 권한을 참조합니다.

다음 표에서는 이러한 값 간의 관계를 보여 줍니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ADSI 편집 요약 페이지</th>
<th>ADSI 편집 고급 보기, 보기/편집 탭</th>
<th>지정된 개체에 적용된 ACL 항목</th>
<th>이진값 (LDP의 액세스 마스크)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>모든 권한</p></td>
<td><p>모든 권한</p></td>
<td><p><code>WRITE_OWNER | WRITE_DAC | READ_CONTROL | DELETE | ACTRL_DS_CONTROL_ACCESS | ACTRL_DS_LIST_OBJECT | ACTRL_DS_DELETE_TREE | ACTRL_DS_WRITE_PROP | ACTRL_DS_READ_PROP | ACTRL_DS_SELF | ACTRL_DS_LIST | ACTRL_DS_DELETE_CHILD | ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x000F01FF</code></p></td>
</tr>
<tr class="even">
<td><p>읽기</p></td>
<td><p>내용 보기 + 모든 속성 읽기 + 사용 권한 읽기</p></td>
<td><p><code>ACTRL_DS_LIST | ACTRL_DS_READ_PROP | READ_CONTROL</code></p></td>
<td><p><code>0x00020014</code></p></td>
</tr>
<tr class="odd">
<td><p>쓰기</p></td>
<td><p>모든 속성 쓰기 + 모든 유효한 쓰기</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP | ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000028</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>내용 보기</p></td>
<td><p><code>ACTRL_DS_LIST</code></p></td>
<td><p><code>0x00000004</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>모든 속성 읽기</p></td>
<td><p><code>ACTRL_DS_READ_PROP</code></p></td>
<td><p><code>0x00000010</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>모든 속성 쓰기</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP</code></p></td>
<td><p><code>0x00000020</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>삭제</p></td>
<td><p><code>DELETE</code></p></td>
<td><p><code>0x00010000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>하위 트리 삭제</p></td>
<td><p><code>ACTRL_DS_DELETE_TREE</code></p></td>
<td><p><code>0x00000040</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>사용 권한 읽기</p></td>
<td><p><code>READ_CONTROL</code></p></td>
<td><p><code>0x00020000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>사용 권한 수정</p></td>
<td><p><code>WRITE_DAC</code></p></td>
<td><p><code>0x00040000</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>소유자 수정</p></td>
<td><p><code>WRITE_OWNER</code></p></td>
<td><p><code>0x00080000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>모든 유효한 쓰기</p></td>
<td><p><code>ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000008</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>모든 확장 권한</p></td>
<td><p><code>ACTRL_DS_CONTROL_ACCESS</code></p></td>
<td><p><code>0x00000100</code></p></td>
</tr>
<tr class="even">
<td><p>모든 자식 개체 만들기</p></td>
<td><p>모든 자식 개체 만들기</p></td>
<td><p><code>ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x00000001</code></p></td>
</tr>
<tr class="odd">
<td><p>모든 자식 개체 삭제</p></td>
<td><p>모든 자식 개체 삭제</p></td>
<td><p><code>ACTRL_DS_DELETE_CHILD</code></p></td>
<td><p><code>0x00000002</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
<td><p><code>ACTRL_DS_LIST_OBJECT</code></p></td>
<td><p><code>0x00000080</code></p></td>
</tr>
</tbody>
</table>


확장 권한은 개별 응용 프로그램에서 지정하는 사용자 지정 권한으로, ACL에서 지정합니다. 하지만 Active Directory에서는 의미가 없습니다. 확장 권한은 특정 응용 프로그램에서 적용됩니다. Exchange 확장 권한의 예로는 "공용 폴더 만들기" 또는 "정보 저장소에 명명된 속성 만들기" 등이 있습니다.

Microsoft Exchange Server 2010 설치 중에 설정 하는 사용 권한에 대 한 정보를 [Exchange 2010 배포 권한 참조 (영문)](https://go.microsoft.com/fwlink/p/?linkid=402924)을 참조 하십시오.

## Active Directory 준비 사용 권한

이 섹션의 사용 권한 표에서는 `Setup /PrepareAD` 명령을 실행할 때 설정되는 사용 권한을 보여 줍니다.


> [!NOTE]
> 이 섹션에 설명된 권한은 공유 권한 모델을 사용하여 Exchange 2013을 배포할 때 구성된 기본 권한입니다. Active Directory 분할 권한 모델을 사용하여 Exchange 2013을 배포한 경우 기본 권한은 달라집니다. Active Directory 분할 권한 모델과 공유 및 분할 권한 모델을 사용할 때 기본 권한이 어떻게 달라지는지 알아보려면 <A href="understanding-split-permissions-exchange-2013-help.md">분할 권한 이해</A>의 <A href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</A>을 참조하세요. Exchange을 설치할 때 Active Directory 분할 권한을 사용하도록 선택하지 않으면 Exchange는 공유 권한을 사용합니다.



## Microsoft Exchange 컨테이너 사용 권한

다음 표에서는 구성 파티션 내에서 Microsoft Exchange 컨테이너에 설정되는 사용 권한을 보여 줍니다.

### 개체의 고유 이름: CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<도메인\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Installation Account</p></td>
<td><p>허용 ACE</p></td>
<td><p>모두</p></td>
<td><p>모든 권한</p></td>
<td><p></p></td>
<td><p><code>/PrepareAD</code>를 실행하는 데 사용되는 계정입니다.</p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>허용 ACE</p></td>
<td><p>없음</p></td>
<td><p>속성 읽기</p>
<p>내용 보기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 수정</p></td>
<td><p>msExchSmtpRceiveConnector</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Delegated Setup</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 자동 검색 컨테이너 사용 권한

다음 표에서는 구성 파티션 내에서 Microsoft Exchange 자동 검색 컨테이너에 설정되는 사용 권한을 보여 줍니다.

### 개체의 고유 이름: CN=Microsoft Exchange Autodiscover,CN=Services,CN=Configuration,DC=\<도메인\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 조직 컨테이너 사용 권한

이 섹션의 사용 권한 표에서는 구성 파티션 내에서 Microsoft Exchange 조직 및 하위 컨테이너에 설정되는 사용 권한을 보여 줍니다.

### 개체의 고유 이름: CN=\<조직\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<도메인\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Enterprise Admins</p>
<p>Root Domain Admins</p>
<p>설치 계정</p>
<p>조직 관리</p></td>
<td><p>거부 ACE</p></td>
<td><p>All</p></td>
<td><p>다른 사람 이름으로 보내기</p>
<p>다음으로 받기</p></td>
<td><p></p></td>
<td><p>Windows 관리자는 사서함을 열 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>엔터프라이즈 관리자</p>
<p>Schema Admins</p>
<p>루트 도메인 관리자</p>
<p>설치 계정</p>
<p>조직 관리</p></td>
<td><p>거부 ACE</p></td>
<td><p>All</p></td>
<td><p>Exchange 웹 서비스 가장</p>
<p>Exchange 웹 서비스 토큰 직렬화</p></td>
<td><p></p></td>
<td><p>확장 권한</p></td>
</tr>
<tr class="odd">
<td><p>엔터프라이즈 관리자</p>
<p>스키마 관리자</p>
<p>루트 도메인 관리자</p>
<p>설치 계정</p></td>
<td><p>거부 ACE</p></td>
<td><p>All</p></td>
<td><p>전송 액세스 저장</p>
<p>제한된 위임 저장</p>
<p>읽기 권한 저장</p>
<p>읽기/쓰기 권한 저장</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>로컬 시스템</p></td>
<td><p>허용</p></td>
<td><p>All</p></td>
<td><p>모든 확장 권한</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>거부 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpace</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>인증된 사용자</p></td>
<td><p>허용</p></td>
<td><p>없음</p></td>
<td><p>읽기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>NT Authority\Network Service</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>관리되는 가용성 서버</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 확장 권한</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchOwningServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchDatabaseCreated</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUserCulture</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>siteFolderGUID</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>siteFolderServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchEDBOffline</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchPatchMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>publicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>최상위 공용 폴더 만들기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>최상위 공용 폴더 만들기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>정보 저장소 상태 보기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>정보 저장소 상태 보기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>정보 저장소 관리</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>정보 저장소 관리</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>정보 저장소에 명명된 속성 만들기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>정보 저장소에 명명된 속성 만들기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 ACL 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 ACL 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 할당량 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 할당량 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 관리 ACL 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 관리 ACL 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 만료 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 만료 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 복제본 목록 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 복제본 목록 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 삭제된 항목 보존 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 삭제된 항목 보존 수정</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 만들기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 만들기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>메일 사용 가능 공용 폴더</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Everyone</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>정보 저장소에 명명된 속성 만들기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Everyone</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>공용 폴더 만들기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Everyone</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p><code>/ msExchPrivateMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Everyone</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p><code>/ siteAddressing</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=All Address Lists,CN=Address Lists Container,CN=\<조직\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>내용 보기</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Offline Address Lists,CN=Address Lists Container, CN=\<조직\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>오프라인 주소록 다운로드</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Addressing,CN=\<조직\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated users</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Recipient Policies,CN=\<조직\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


## 구성 파티션 컨테이너 사용 권한

이 섹션의 사용 권한 표에서는 구성 파티션 내 다양한 컨테이너의 `Setup /PrepareAD` 명령에 의해 설정되는 사용 권한을 보여 줍니다.

### 개체의 고유 이름: CN=Sites,CN=Configuration,DC=\<도메인\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchVersion / site</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchVersion / site-link</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchPartnerId / site</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchMinorPartnerId / site</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchResponsibleforSites / site</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p></p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchTransportSiteFlags / site</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchCost / site-link</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p>
<p>로컬 시스템</p>
<p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p><code>/ msExchEdgeSyncEHFConnector</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p>
<p>로컬 시스템</p>
<p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p><code>/ msExchEdgeSyncMservConnector</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>자식</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p>
<p>트리 삭제</p></td>
<td><p><code>msExchEdgeSyncServiceConfig / site</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p>
<p>로컬 시스템</p>
<p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p><code>/ msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>자식</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p>
<p>트리 삭제</p></td>
<td><p><code>msExchEdgeSyncMservConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>자식</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p>
<p>트리 삭제</p></td>
<td><p><code>msExchEdgeSyncEHFConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Deleted Objects,CN=Configuration,DC=\<도메인\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>내용 보기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Administration</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>설치 계정</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>사용 권한 쓰기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p><code>/PrepareAD</code>를 실행하는 데 사용되는 계정입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>네트워크 서비스</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>내용 보기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Exchange 관리 그룹 사용 권한

`Setup /PrepareAD` 명령은 또한 조직 내의 관리 그룹에 대해 다음 사용 권한을 구성합니다.

### 개체의 고유 이름: CN=\<관리자 그룹\>,CN=Administrative Groups,CN=\<조직\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>받는 사람 업데이트 서비스 액세스</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Exchange 받는 사람 관리자가 프록시 주소 정보를 사용하여 받는 사람을 스탬프 처리할 수 있도록 허용합니다.</p></td>
</tr>
<tr class="even">
<td><p>로컬 시스템</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>받는 사람 업데이트 서비스 액세스</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>서버에서 프록시 주소 정보를 사용하여 받는 사람을 스탬프 처리할 수 있도록 허용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>받는 사람 업데이트 서비스 액세스</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Exchange 공용 폴더 관리자가 프록시 주소 정보를 사용하여 받는 사람을 스탬프 처리할 수 있도록 허용합니다.</p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Advanced Security Settings,CN=\<관리자 그룹\>,CN=Administrative Groups,CN=\<조직\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>없음</p></td>
<td><p>내용 보기</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Encryption,CN=Advanced Security Settings,CN=\<관리자 그룹\>,CN=Administrative Groups,CN=\<조직\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>없음</p></td>
<td><p>속성 읽기</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Arrays,CN=\<관리자 그룹\>,CN=Administrative Groups,CN=\<조직\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>없음</p></td>
<td><p>내용 보기</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Database Availability Groups,CN=\<관리자 그룹\>,CN=Administrative Groups,CN=\<조직\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>없음</p></td>
<td><p>내용 보기</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Databases,CN=\<관리자 그룹\>,CN=Administrative Groups,CN=\<조직\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>없음</p></td>
<td><p>내용 보기</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Servers,CN=\<관리자 그룹\>,CN=Administrative Groups,CN=\<조직\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>거부 ACE</p></td>
<td><p>All</p></td>
<td><p>다음으로 받기</p></td>
<td><p></p></td>
<td><p>Exchange Servers는 사서함을 열 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>없음</p></td>
<td><p>내용 보기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 보안 그룹 컨테이너 사용 권한

이 섹션의 사용 권한 표에서는 루트 도메인 파티션 내에서 Microsoft Exchange 보안 그룹 컨테이너에 설정되는 사용 권한을 보여 줍니다.

### 개체의 고유 이름: OU=Microsoft Exchange Security Groups,DC=\<루트 도메인\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p></td>
<td><p><code>/ Group</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>삭제</p></td>
<td><p><code>/ group</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Member / group</code></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Organization Management,OU=Microsoft Exchange Security Groups,DC=\<루트 도메인\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Public Folder Management,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=ExchangeLegacyInterop,OU=Microsoft Exchange Security Groups,DC=\<루트 도메인\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Exchange Servers,OU=Microsoft Exchange Security Groups,DC=\<루트 도메인\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Root Domain Administrators</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>구성원 읽기</p>
<p>구성원 쓰기</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Child Domain Administrators</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>구성원 읽기</p>
<p>구성원 쓰기</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 도메인 준비

다음 표에서는 `Setup /PrepareDomain` 명령을 실행할 때 설정되는 사용 권한을 보여 줍니다.


> [!NOTE]
> 이 섹션에 설명된 권한은 공유 권한 모델을 사용하여 Exchange 2013을 배포할 때 구성된 기본 권한입니다. Active Directory 분할 권한 모델을 사용하여 Exchange 2013을 배포한 경우 기본 권한은 달라집니다. Active Directory 분할 권한 모델과 공유 및 분할 권한 모델을 사용할 때 기본 권한이 어떻게 달라지는지 알아보려면 <A href="understanding-split-permissions-exchange-2013-help.md">분할 권한 이해</A>의 <A href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</A>을 참조하세요. Exchange을 설치할 때 Active Directory 분할 권한을 사용하도록 선택하지 않으면 Exchange는 공유 권한을 사용합니다.



### 개체의 고유 이름: DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>전송 서비스 읽기 권한을 부여합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>복제 동기화</p></td>
<td><p></p></td>
<td><p>확장 권한</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p>
<p>자식 표시</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p>
<p>자식 표시</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>WriteDACL</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>WriteDACL</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>트리 삭제</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>트리 삭제</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>삭제</p></td>
<td><p><code>/ contact</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>삭제</p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>삭제</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>삭제</p></td>
<td><p><code>/ organizationUnit</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>삭제</p></td>
<td><p><code>/ group</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p></td>
<td><p><code>/ computer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>다음 로그온 시 암호 다시 설정</p></td>
<td><p></p></td>
<td><p>확장 권한</p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>암호 변경</p></td>
<td><p><code> / user</code></p></td>
<td><p>확장 권한</p></td>
</tr>
<tr class="odd">
<td><p>위임 설치</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=AdminSDHolder,CN=System,DC=\<도메인\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>전송 서비스 읽기 권한을 부여합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>복제 동기화</p></td>
<td><p></p></td>
<td><p>확장 권한</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p>
<p>자식 표시</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p>
<p>자식 표시</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>위임 설치</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Deleted Objects,DC=\<domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>내용 보기</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Microsoft Exchange System Objects,DC=\<도메인\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p>
<p>내용 보기</p>
<p>사용 권한 읽기</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
</tr>
<tr class="even">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>adminDisplayName</code></p></td>
</tr>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>modifyTimeStamp</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>거부 ACE</p></td>
<td><p>All</p></td>
<td><p>트리 삭제</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기 트리 삭제</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 삭제</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 삭제</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>암호 변경</p>
<p>다음 로그온 시 암호 다시 설정</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p>legacyExchangeDN / publicFolder</p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p>
<p>속성 쓰기</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Exchange Install Domain Servers,CN=Microsoft Exchange System Objects,DC=\<domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 서버 역할 설치

클라이언트 액세스 및 사서함 서버 역할을 설치하는 동안 설치 프로그램은 Organization Management라는 관리 역할 그룹의 구성원이 서버를 관리할 수 있도록 로컬 컴퓨터의 관리자 보안 그룹에 Organization Management USG를 추가합니다.

다음 사용 권한 표에서는 클라이언트 액세스 또는 사서함 서버 역할을 설치할 때 설정되는 사용 권한을 보여 줍니다.

### 개체의 고유 이름: CN=\<서버\>,CN=Servers,CN=\<관리자 그룹\>,CN=Administrative Groups,CN=\<조직\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MACHINE$</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>MACHINE$</p></td>
<td><p>허용 ACE</p></td>
<td><p>없음</p></td>
<td><p>속성 쓰기</p></td>
<td><p><code>msExchServerSite</code></p>
<p><code>msExchEdgeSyncCredential</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>전송 액세스 저장</p>
<p>제한된 위임 저장</p>
<p>읽기 전용 권한 저장</p>
<p>읽기 및 쓰기 권한 저장</p></td>
<td><p></p></td>
<td><p>확장 권한</p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>Exchange 웹 서비스 토큰 직렬화</p></td>
<td><p></p></td>
<td><p>확장 권한</p>
<p>사서함 서버 역할 개체에만 부여됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>로컬 시스템</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>사용 권한 읽기</p>
<p>내용 보기</p>
<p>속성 읽기</p>
<p>개체 나열</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>위임 설치</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 권한</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>위임 설치</p></td>
<td><p>거부 ACE</p></td>
<td><p>All</p></td>
<td><p>자식 만들기</p>
<p>자식 삭제</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 읽기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>위임 설치</p></td>
<td><p>거부 ACE</p></td>
<td><p>All</p></td>
<td><p>다음으로 받기</p>
<p>다른 사람 이름으로 보내기</p></td>
<td><p></p></td>
<td><p>확장 권한</p></td>
</tr>
</tbody>
</table>


## 데이터베이스 가용성 그룹

이 섹션의 사용 권한 표에서는 데이터베이스 가용성 그룹 및 해당 구성원에 대해 설정되는 사용 권한을 보여 줍니다.

### 개체의 고유 이름: CN=\<DAG 이름\>,CN=Database Availability Groups,CN=\<관리자 그룹\>,CN=Administrative Groups,CN=\<조직\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>없음</p></td>
<td><p>속성 읽기</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Edge 전송

Edge 전송 서버를 설치하고 Exchange 조직에 대해 Edge 구독을 설정하는 경우 Edge 전송 서버를 조직 내에서 인스턴스화하면 다음 사용 권한 표의 사용 권한이 설정됩니다.

### 개체의 고유 이름: CN=\<서버\>,CN=Servers,CN=\<관리자 그룹\>,CN=Administrative Groups,CN=\<조직\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>속성 쓰기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>없음</p></td>
<td><p>속성 읽기</p></td>
<td><p></p></td>
<td><p>ACE는 <code>msExchExchangeServer</code> 클래스 개체 <code>defaultSecurityDescriptor</code>의 스키마에 정의됩니다.</p></td>
</tr>
</tbody>
</table>


## 사서함 서버 설치

다음 컨테이너가 없는 경우 첫 번째 사서함 서버를 설치하는 동안 만들어집니다. 다음 사용 권한 표에서는 적용되는 사용 권한을 보여 줍니다.

### 개체의 고유 이름: CN=Availability Configuration,CN=\<조직\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>설명</p></td>
<td><p>속성 읽기</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpaceObjects</code></p></td>
<td><p>확장 권한</p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Default \<Server\>,CN=SMTP Receive Connectors,CN=Protocols,CN=\<서버\>,CN=Servers,CN=\<관리자 그룹\>,CN=\<조직\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>거부 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>거부 ACE</p></td>
<td><p>All</p></td>
<td><p>조직 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID(보안 식별자)입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>EXCH50 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>EXCH50 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>EXCH50 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>EXCH50 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>EXCH50 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XShadow 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XShadow 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XSessionParams 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XSessionParams 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XSessionParams 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 헤더 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 헤더 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>xAttr 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>xAttr 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>xAttr 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XProxyFrom 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 XProxyFrom 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 XProxyFrom 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XSysProbe 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 XSysProbe 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 XSysProbe 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 확장 속성 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 확장 속성 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 확장 속성 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 빠른 인덱스 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 빠른 인덱스 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 빠른 인덱스 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext AD 받는 사람 캐시 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext AD 받는 사람 캐시 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext AD 받는 사람 캐시 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>인증 플래그 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>인증 플래그 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>인증 플래그 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>인증 플래그 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>인증 플래그 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>메시지 크기 제한 무시</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>메시지 크기 제한 무시</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>메시지 크기 제한 무시</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>메시지 크기 제한 무시</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>메시지 크기 제한 무시</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>조직 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>조직 헤더 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>조직 헤더 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>신뢰할 수 있는 도메인 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>신뢰할 수 있는 도메인 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>신뢰할 수 있는 도메인 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>신뢰할 수 있는 도메인 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>신뢰할 수 있는 도메인 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 개체의 고유 이름: CN=Client \<Server\>,CN=SMTP Receive Connectors,CN=Protocols,CN=\<서버\>,CN=Servers,CN=\<관리자 그룹\>,CN=\<조직\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>인증된 사용자</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XSessionParams 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XSessionParams 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XSessionParams 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID(보안 식별자)입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>Exch50 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>Exch50 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>Exch50 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>Exch50 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>모든 받는 사람에게 메시지 전송</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XShadow 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XShadow 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 헤더 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 헤더 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>xAttr 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>xAttr 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>xAttr 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XProxyFrom 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 XProxyFrom 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 XProxyFrom 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>인증 플래그 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>인증 플래그 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>인증 플래그 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>인증 플래그 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XSysProbe 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 XSysProbe 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 XSysProbe 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>인증 플래그 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>스팸 방지 무시</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 확장 속성 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 확장 속성 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 확장 속성 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 빠른 인덱스 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 빠른 인덱스 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext 빠른 인덱스 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>메시지 크기 제한 무시</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>메시지 크기 제한 무시</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>메시지 크기 제한 무시</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>메시지 크기 제한 무시</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>조직 헤더 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>조직 헤더 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>조직 헤더 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext AD 받는 사람 캐시 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext AD 받는 사람 캐시 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XMessageContext AD 받는 사람 캐시 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>서버로 메시지 전송</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>신뢰할 수 있는 도메인 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>신뢰할 수 있는 도메인 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>신뢰할 수 있는 도메인 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>신뢰할 수 있는 도메인 보낸 사람 허용</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## SMTP 송신 커넥터 만들기

다음 표에서는 송신 커넥터를 만들 때 설정되는 사용 권한을 보여 줍니다.

### 개체의 고유 이름: CN=\<커넥터 이름\>,CN=Connections,CN=\<라우팅 그룹\>,CN=Routing Groups, CN=\<관리자 그룹\>,CN=\<조직\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>계정</th>
<th>ACE 유형</th>
<th>상속</th>
<th>사용 권한</th>
<th>속성/적용 대상</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\ANONYMOUS LOGON</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>조직 헤더 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>조직 헤더 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>조직 헤더 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 헤더 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 헤더 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>포리스트 헤더 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XShadow 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XShadow 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>XShadow 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-10</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 보내기</p></td>
<td><p></p></td>
<td><p>파트너 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 보내기</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>라우팅 헤더 보내기</p></td>
<td><p></p></td>
<td><p>레거시 Exchange Servers의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>Exch50 보내기</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>Exch50 보내기</p></td>
<td><p></p></td>
<td><p>사서함 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>Exch50 보내기</p></td>
<td><p></p></td>
<td><p>Edge 전송 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>Exch50 보내기</p></td>
<td><p></p></td>
<td><p>외부 보안 서버의 잘 알려진 SID입니다.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>허용 ACE</p></td>
<td><p>All</p></td>
<td><p>Exch50 보내기</p></td>
<td><p></p></td>
<td><p>레거시 Exchange Servers의 잘 알려진 SID입니다.</p></td>
</tr>
</tbody>
</table>

