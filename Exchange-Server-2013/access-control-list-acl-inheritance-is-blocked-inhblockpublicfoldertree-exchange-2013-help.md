---
title: '액세스 제어 목록 (ACL) 상속이 blocked_InhBlockPublicFolderTree: Exchange 2013 Help'
TOCTitle: 액세스 제어 목록 (ACL) 상속이 blocked_InhBlockPublicFolderTree
ms:assetid: e3b89c8a-d6f8-4864-8bf0-35a78ce87cc4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.inhblockpublicfoldertree(v=EXCHG.150)
ms:contentKeyID: 50484341
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 액세스 제어 목록 (ACL) 상속이 blocked\_InhBlockPublicFolderTree

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

필요한 사용 권한을 전파할 수 되었기 때문에 Microsoft Exchange Server 2007 또는 Exchange Server 2010 설치를 계속할 수 없습니다.

Exchange 설치 하려면 사용 권한 상속 다음 Exchange 개체에 사용할 수 있어야 합니다.

  - Exchange 조직 개체

  - Exchange 관리 그룹 개체

  - Exchange 서버 컨테이너 개체

  - Exchange 주소 목록 개체

  - Exchange 공용 폴더 개체

  - Exchange 공용 폴더 트리에서 개체

이러한 개체에 대 한 사용 권한 상속을 사용 하도록 설정 하는 오류는 메일 흐름 문제가 발생할 저장소 탑재 문제 및 기타 서비스 중단 될 수 있습니다.

이 문제를 해결 하려면 있는지 확인 하는 "이 개체 및 자식 개체에 전파할 허용 권한" 설정이 개체의 경우 사용 되 고 다음 Exchange Server 2007 또는 Exchange 2010 설치 프로그램을 다시 실행 하십시오.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 Exchange System Manager를 사용 하 여 Exchange 구성 개체에 대 한 사용 권한 상속을 다시 사용 하도록 설정 하려면</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>레지스트리 매개 변수를 설정 하 여 Exchange System Manager의 개체 속성 상자에 대 한 <strong>보안</strong> 탭을 사용 합니다.</p>
<ol>
<li><p>레지스트리 편집기 (Regedt32.exe)를 시작 합니다.</p></li>
<li><p>레지스트리에 다음 키를 찾습니다.</p>
<p><strong>HKEY_CURRENT_USER\Software\Microsoft\Exchange\EXAdmin</strong></p></li>
<li><p><strong>편집</strong> 메뉴에서 <strong>새로</strong> 만들기를 클릭 하 고 다음 레지스트리 값을 추가 합니다.</p>
<p><strong>값 이름</strong>: ShowSecurityPage</p>
<p><strong>데이터 형식</strong>: REG_DWORD</p>
<p><strong>기 수</strong>: 이진</p>
<p><strong>값</strong>: 1</p></li>
<li><p>레지스트리 편집기를 끝냅니다.</p></li>
</ol>

> [!NOTE]
> 기본적으로 구성 개체 속성 상자에서 <STRONG>보안</STRONG> 탭을 사용할 수 없습니다.


</li>
<li><p>Exchange System Manager를 열고, 문제의 개체를 찾을 하, 개체를 마우스 오른쪽 단추로 클릭 하 고 <strong>속성</strong> 을 선택 합니다.</p></li>
<li><p><strong>보안</strong> 탭을 선택 하 고 <strong>고급</strong> 을 클릭 합니다.</p></li>
<li><p>다시 사용 권한 상속을 사용 하도록 설정 하려면 <strong>이 개체 및 모든 자식 개체에 전파 하는 부모 로부터 상속 가능한 사용 권한을 허용</strong> 선택 합니다.</p></li>
<li><p>Exchange 서버를 다시 시작 합니다.</p></li>
</ol></td>
</tr>
</tbody>
</table>



> [!WARNING]
> 잘못 수정 하면 Active Directory 개체의 특성을 ADSI 편집, LDP 도구 또는 다른 LDAP 버전 3 클라이언트를 사용 하는 경우, 하는 경우에 심각한 문제가 발생할 수 있습니다. 이러한 문제는 다시 설치 하는 Microsoft Windows Server™ 2003, Exchange 서버 또는 둘 모두 필요할 수 있습니다. 위험은 사용자가 자신의 Active Directory 개체 특성을 수정 합니다.




<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2007 또는 Exchange Server 2010에서 ADSIEdit를 사용 하 여 Exchange 구성 개체에 대 한 사용 권한 상속을 다시 사용 하도록 설정 하려면</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>ADSI 편집을 설치합니다.</p></li>
<li><p>ADSI 편집을 시작 합니다. <strong>시작</strong>, <strong>실행</strong> 을 클릭 하, 텍스트 상자에 <strong>adsiedit.msc</strong> 를 입력 한 다음 확인을 클릭 합니다.</p></li>
<li><p>질문에 있는 개체를 이동한 개체를 마우스 오른쪽 단추로 클릭 <strong>속성</strong> 을 선택 합니다.</p></li>
<li><p><strong>보안</strong> 탭을 선택 하 고 <strong>고급</strong> 을 클릭 합니다.</p></li>
<li><p>다시 사용 권한 상속을 사용 하도록 설정 하려면 <strong>이 개체 및 모든 자식 개체에 전파 하는 부모 로부터 상속 가능한 사용 권한을 허용</strong> 선택 합니다.</p></li>
<li><p><strong>확인</strong> 하면 변경 내용은 적용을 두번 선택 합니다.</p></li>
<li><p>Active Directory 복제가를 전파 하 여 변경 내용을 하거나 Microsoft 기술 자료 문서 232072, &quot;시작 하려면 복제 간의 Active Directory 직접 복제 파트너&quot; (<a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=232072" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=232072</a>)에 대 한 지침을 수행 하 여 Active Directory 복제를 적용 될 때까지 기다립니다.</p></li>
</ol></td>
</tr>
</tbody>
</table>

