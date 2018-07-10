---
title: '받는 사람 업데이트 service_RUSMissing를 찾을 수 없음: Exchange 2013 Help'
TOCTitle: 받는 사람 업데이트 service_RUSMissing를 찾을 수 없음
ms:assetid: 920fbf51-d5e4-4ac6-869f-7f1c5d9a3024
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.rusmissing(v=EXCHG.150)
ms:contentKeyID: 50483669
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 받는 사람 업데이트 service\_RUSMissing를 찾을 수 없음

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2016-12-15_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft® Exchange Server 2007 또는 Exchange Server 2010 설치 프로그램은 받는 사람 업데이트 서비스 (러시아어) 기존 Exchange 조직에 도메인에 대 한 책임을 찾을 수 없어서 계속할 수 없습니다.

Microsoft Exchange 설치 하려면 받는 사람 업데이트 서비스의 인스턴스는 기존 Exchange 조직에서 각 도메인에 있어야 합니다.

받는 사람 업데이트 서비스의 인스턴스를 도메인에 대 한 누락 된 경우 도메인에 생성 되는 새 사용자 개체가 자신에 게 발급 된 전자 메일 주소를 받지 않습니다.

이 문제를 해결 하려면 각 도메인에 대 한 받는 사람 업데이트 서비스의 인스턴스가 있는지 확인 하 고 한 단어가 일치 하지 않으며 다음 Microsoft Exchange 설치 프로그램을 다시 실행 하는 도메인에 대 한 받는 사람 업데이트 서비스의 인스턴스를 만듭니다.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>도메인에 대 한 받는 사람 업데이트 서비스 인스턴스를 생성 하려면</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Exchange System Manager를 엽니다.</p></li>
<li><p><strong>받는 사람</strong> 을 확장 합니다.</p></li>
<li><p><strong>받는 사람 업데이트 서비스</strong> 노드를 마우스 오른쪽 단추로 클릭 하 고 <strong>새로</strong> 만들기를 클릭 <strong>받는 사람 업데이트 서비스</strong> 를 차례로 클릭 합니다.</p></li>
<li><p>새 개체 창에서 도메인의 이름을 찾는 <strong>찾아보기</strong> 를 클릭 합니다.</p></li>
<li><p>도메인의 이름을 선택한 다음 <strong>확인</strong> 을 클릭 합니다.</p></li>
<li><p>새 개체 창에서 <strong>다음</strong> 을 한 다음 <strong>완료</strong> 를 클릭 합니다.</p></li>
</ol></td>
</tr>
</tbody>
</table>


받는 사람 업데이트 서비스에 대 한 자세한 내용은 다음 Microsoft 기술 자료 문서를 참조 하십시오.

  - "받는 사람 업데이트 서비스에서 적용 하는 방법의 받는 사람 정책을" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=328738](https://go.microsoft.com/fwlink/?linkid=3052&kbid=328738)).

  - "방법: 받는 사람 업데이트 서비스도 채웁니다 주소 목록" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253828](https://go.microsoft.com/fwlink/?linkid=3052&kbid=253828))입니다.

  - "Exchange 받는 사람 업데이트 서비스의 진행률을 확인 하는 방법" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=246127](https://go.microsoft.com/fwlink/?linkid=3052&kbid=246127))입니다.

  - "Exchange 받는 사람 업데이트 서비스에 의해 수행 되는 작업" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253770](https://go.microsoft.com/fwlink/?linkid=3052&kbid=253770))입니다.

