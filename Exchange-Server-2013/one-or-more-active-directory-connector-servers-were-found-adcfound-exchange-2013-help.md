---
title: '하나 이상의 Active Directory Connector 서버 된 found_ADCFound: Exchange 2013 Help'
TOCTitle: 하나 이상의 Active Directory Connector 서버 된 found_ADCFound
ms:assetid: a874f51f-09a2-4a76-9695-d61fb1ee6c1c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.adcfound(v=EXCHG.150)
ms:contentKeyID: 50483830
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 하나 이상의 Active Directory Connector 서버 된 found\_ADCFound

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2016-12-15_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

현재 Microsoft Exchange 환경에서 하나 이상의 Active Directory 커넥터 (ADC)를 찾았습니다 Microsoft Exchange Server 2007 및 Exchange Server 2010 설치를 계속할 수 없습니다.

ADC 혼합된 모드 Microsoft Exchange 환경에서 Active Directory 디렉터리 서비스에 Exchange Server 5.5 버전에서에서 개체를 복제 하 고 Exchange 2007 또는 Exchange 2010에서 지원 되지 않습니다.

Exchange 2007 또는 Exchange 2010 설치 ADC에 대 한 구성 요소를 모두 제거 해야 합니다.

이 문제를 해결 하려면 모든 ADC 구성 요소를 제거 하 고 Exchange 2007 또는 Exchange 2010 설치 프로그램을 다시 실행 하십시오.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Active Directory Connector 구성 요소를 제거 하려면</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>서비스를 실행 하는 서버에서 ADC 서비스를 사용 하지 않으려면 바탕 화면에서 <strong>내 컴퓨터</strong> 를 마우스 오른쪽 단추로 클릭 하 고 <strong>관리</strong> 를 클릭 합니다.</p></li>
<li><p><strong>서비스 및 응용 프로그램</strong> 노드를 확장 하 고 <strong>서비스</strong> 노드를 클릭 합니다.</p></li>
<li><p>오른쪽 창에서 <strong>Microsoft Active Directory Connector</strong> 를 마우스 오른쪽 단추로 클릭 하 고 <strong>속성</strong> 을 클릭 합니다.</p></li>
<li><p><strong>시작 유형이</strong> <strong>사용 안함</strong> 으로 변경 합니다. 컴퓨터를 시작 하는 다음에 서비스를 시작 되지 않습니다.</p></li>
<li><p><strong>적용</strong>을 클릭한 다음 <strong>확인</strong>을 클릭합니다.</p></li>
<li><p>서비스를 제거 하려면 Microsoft Exchange 2000 Server 또는 Microsoft Exchange Server 2003 CD에서 Active Directory 설치 마법사를 사용 합니다. \ADC\I386 폴더를 열고 Setup.exe 프로그램을 두번클릭 합니다. ADC 서비스 구성 요소를 <strong>모두 제거</strong> 하 고 지시를 따릅니다.</p>

> [!IMPORTANT]
> 6 단계와이 문제를 해결 하려면 <STRONG>모두 제거</STRONG> ADC 구성 요소를 완료 해야 합니다. 서비스를 사용 하지 않도록 설정 하려면 충분 하지 않습니다.


</li>
</ol></td>
</tr>
</tbody>
</table>


ADC에 대 한 자세한 내용은 다음 Microsoft 기술 자료 문서를 참조 하십시오.

  - 325300, "웹캐스트 지원: Active Directory Connector 소개" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325300](https://go.microsoft.com/fwlink/?linkid=3052&kbid=325300)).

  - 325221, "웹캐스트: Microsoft Active Directory Connector 고급" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325221](https://go.microsoft.com/fwlink/?linkid=3052&kbid=325221)).

  - 312632, "설치 및 Exchange 2000 Server의 Active Directory 커넥터를 구성 하는 방법" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=312632](https://go.microsoft.com/fwlink/?linkid=3052&kbid=312632)).

