---
title: 'Exchange 2010_NoE12ServerWarning에 대 한 Active Directory를 준비한 후 Exchange 2007 역할을 설치할 수 없습니다.: Exchange 2013 Help'
TOCTitle: Exchange 2010_NoE12ServerWarning에 대 한 Active Directory를 준비한 후 Exchange 2007 역할을 설치할 수 없습니다.
ms:assetid: 4e579f69-0de9-421c-ba31-4e63a25e6a45
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.noe12serverwarning(v=EXCHG.150)
ms:contentKeyID: 50483100
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2010\_NoE12ServerWarning에 대 한 Active Directory를 준비한 후 Exchange 2007 역할을 설치할 수 없습니다.

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft Exchange Server 2010**Setup /PrepareAD**을 실행 하면 Microsoft Exchange Server 분석기 도구는 모든 Microsoft Exchange Server 2007 서버 역할의 존재 여부를 확인 하려면 기존 Active Directory 토폴로지를 쿼리 합니다. Exchange 2007 서버 역할 감지 되지 않으면 다음과 같은 경고 메시지가 나타납니다.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>설치 프로그램은 'Setup /PrepareAD'와 역할이이 토폴로지에서 발견 된 없는 Exchange Server 2007을 통해 Exchange Server 2010에 대 한 조직 준비 하려고 합니다. 이 작업 후에 것은 불가능 모든 Exchange Server 2007 역할을 설치 합니다.</p></td>
</tr>
</tbody>
</table>


Exchange Server 2010 을 배포 하기 전에 Exchange 2007 을 배포 하기 전에 설치 하는 모든 서버 역할을 사용 하 여 Exchange 2007 서버를 배포 해야 하는 다음과 같은 요소를 고려 합니다.

  - **타사 또는 사내 개발 된 응용 프로그램**   하지 Exchange 2003 용으로 개발 된 응용 프로그램 Exchange 2010 호환 되어야 하 고 따라서 업그레이드 하거나 교체 해야할 수 있습니다. 이러한 응용 프로그램 및 Exchange 2003;에 연결 된 사용자 모집단을 유지할 수 있습니다. Exchange 2007;로 이동 또는 Exchange 2010 에 대 한 호환 되는 버전의 소프트웨어를 바꿉니다.

  - **동시 사용 또는 마이그레이션 요구 사항**   계획 하는 경우 사서함을 조직으로, Exchange 2007 를 배포 하 고 Microsoft Transporter 제품군을 사용 하 여 마이그레이션하거나 제 3 자 동시 사용 또는 마이그레이션 솔루션을 사용할 수 있습니다. Microsoft Transporter 제품군을 다운로드 하려면 Microsoft 다운로드 센터에서 [Microsoft Transporter 제품군](http://go.microsoft.com/fwlink/?linkid=82688) 이동 합니다.

또한 조직에 대 한 옵션을 평가할 때는 다음과 같은 질문을 고려 했는지 확인 합니다.

  - Exchange 2003 에 지원의 끝에 도달 하기 전에 Exchange 2010 에 종속 된 응용 프로그램을 이동 하는 전체에서 전략 있습니까? 자세한 내용은 Microsoft 지원 주기 정책 웹 페이지 ([https://go.microsoft.com/fwlink/?LinkID=55839](https://go.microsoft.com/fwlink/?linkid=55839))를 참고 하십시오.

  - 전략은 WebDAV 및 웹 서비스 동시 사용 (Exchange 2007 ) 필요 합니까?

  - Exchange 또는 동시 사용 또는 마이그레이션 요구 사항을 충족할 수 있도록 다른 Microsoft 기술을 지 원하는 타사 제품을 고려 했습니까?

  - 하드웨어 수명 주기 접근 방식을 란 (새 64 비트 서버를 구입 하는 비교 가능한 만큼 기존 32 비트 서버를 사용 하 여 계속)?

  - 마이그레이션에 대 한 계획을 문서화할 란 (모든 서버 마이그레이션 단계적된 전략에서 마이그레이션하는 방법 비교 가능한 한 빨리)? 마찬가지로, Exchange 의 다양 한 버전의 동시 사용에 대 한 일정 무엇입니까?

Exchange 2010 을 배포 하기 전에 Exchange 2007 서버를 배포 해야을 결정 하는 경우 모든 서버 역할과 단일 Exchange 2007 배포가 조직의 향후 Exchange 2007 서버 배포를 사용 하도록 설정 하는 데 충분 합니다. Exchange 2003 조직에 Exchange 2007 서버를 배포 하려면 다음이 단계를 따릅니다.

1.  Exchange 2007 **Setup /PrepareSchema**를 실행 합니다.

2.  Exchange 2007 **Setup /PrepareAD**를 실행 합니다.

3.  받는 사람, Exchange 2003 서버 또는 Exchange 서버에서 사용할 수 있는 글로벌 카탈로그를 포함 하는 모든 도메인에서 Exchange 2007**Setup /PrepareDomain** 를 실행 합니다.

4.  모든 4 명의 서버 역할과 (허브 전송, 클라이언트 액세스, 사서함 및 통합 메시징) Exchange 2007 서버를 설치 합니다.

