---
title: 'IIS 7 구성 요소가 설치되지 않음'
TOCTitle: IIS 7 구성 요소 하지 installed_LonghornIIS7HttpCompressionStaticNotInstalled
ms:assetid: 87fb8068-8c11-45cd-b18c-7d4ba97dedda
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.longhorniis7httpcompressionstaticnotinstalled(v=EXCHG.150)
ms:contentKeyID: 50483596
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 7 구성 요소 하지 installed\_LonghornIIS7HttpCompressionStaticNotInstalled

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft Exchange Server 2010 설치 프로그램 또는 Microsoft Exchange Server 2007 설치 설치할 수 없습니다 클라이언트 액세스 서버 (CA) 역할 또는 사서함 서버 역할은 Microsoft Windows Server 2008 기반 컴퓨터에서 또는 Windows Server 2008 R2 기반 컴퓨터에서 필요한 인터넷 정보 서버 (IIS) 7 구성 요소 설치 되지 않습니다.

Exchange 2010 설치 및 Exchange 2007 설치에 Windows Server 2008 기반 컴퓨터 또는 Windows Server 2008 R2 기반 컴퓨터에 설치 하는 CA 역할 이미 설치 된 IIS 7 다음 구성 요소에 필요 합니다.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>CAS 서버 역할에 필요한 IIS 7 구성 요소</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>동적 콘텐츠 압축</p></td>
</tr>
<tr class="even">
<td><p>정적 콘텐츠 압축</p></td>
</tr>
<tr class="odd">
<td><p>기본 인증</p></td>
</tr>
<tr class="even">
<td><p>Windows 인증</p></td>
</tr>
<tr class="odd">
<td><p>IIS 7 다이제스트 인증</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>클라이언트 인증서 매핑</p></td>
</tr>
<tr class="even">
<td><p>디렉터리 찾아보기</p></td>
</tr>
<tr class="odd">
<td><p>HTTP 오류</p></td>
</tr>
<tr class="even">
<td><p>HTTP 로깅</p></td>
</tr>
<tr class="odd">
<td><p>HTTP 리디렉션</p></td>
</tr>
<tr class="even">
<td><p>추적</p></td>
</tr>
<tr class="odd">
<td><p>ISAPI 필터</p></td>
</tr>
<tr class="even">
<td><p>요청 모니터</p></td>
</tr>
<tr class="odd">
<td><p>정적 콘텐츠</p></td>
</tr>
</tbody>
</table>


Exchange 2010 설치 및 Exchange 2007 설치에 Windows Server 2008 기반 컴퓨터 또는 Windows Server 2008 R2 기반 컴퓨터에 설치 하는 사서함 서버 역할은 이미 설치 된 IIS 7 다음 구성 요소에 필요 합니다.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>사서함 서버 역할에 필요한 IIS 7 구성 요소</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 인증</p></td>
</tr>
<tr class="even">
<td><p>Windows 인증</p></td>
</tr>
</tbody>
</table>


이 문제를 해결 하기 위해 대상 컴퓨터에 필요한 IIS 7 구성 요소를 설치 하려면 적절 한 단계를 수행 하 고 Microsoft Exchange 설치 프로그램을 다시 실행 합니다.

Windows Server 2008 서버 관리자를 사용 하 여 CAS 서버 역할에 대 한 IIS 7 구성 요소를 설치 합니다.

1.  **시작**, **관리 도구**를 차례로 클릭하고 **서비스 관리자**를 클릭합니다.

2.  탐색 창에서 **역할** 을 확장, **웹 서버 (IIS)를** 마우스 오른쪽 단추로 클릭 하 고 **역할 서비스 추가** 클릭 합니다.

3.  **역할 서비스 선택** 창에서 **IIS** 까지 아래로 스크롤하십시오.

4.  **보안** 영역에서 다음 확인란을 선택 하려면 클릭 합니다.
    
      - **기본 인증**
    
      - **다이제스트 인증**
    
      - **Windows 인증**

5.  **성능** 영역에서 다음 확인란을 선택 하려면 클릭 하십시오.
    
      - **정적 압축**
    
      - **동적 압축**

6.  **역할 서비스 선택** 창에서 **다음** 을 클릭 하 고 **설치 선택 사항 확인** 창에서 **설치** 를 클릭 합니다.

7.  **Close** 역할 서비스 추가 마법사를 종료를 클릭 합니다.

Windows Server 2008 서버 관리자를 사용 하 여 사서함 서버 역할에 대 한 IIS 7 구성 요소를 설치 합니다.

1.  **시작**, **관리 도구**를 차례로 클릭하고 **서비스 관리자**를 클릭합니다.

2.  탐색 창에서 **역할** 을 확장, **웹 서버 (IIS)를** 마우스 오른쪽 단추로 클릭 하 고 **역할 서비스 추가** 클릭 합니다.

3.  **역할 서비스 선택** 창에서 **IIS** 까지 아래로 스크롤하십시오.

4.  **보안** 영역에서 다음 확인란을 선택 하려면 클릭 합니다.
    
      - **기본 인증**
    
      - **Windows 인증**

5.  **역할 서비스 선택** 창에서 **다음** 을 클릭 하 고 **설치 선택 사항 확인** 창에서 **설치** 를 클릭 합니다.

6.  **Close** 역할 서비스 추가 마법사를 종료를 클릭 합니다.

