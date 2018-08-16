---
title: '주 DNS 접미사가 없거나,: Exchange 2013 Help'
TOCTitle: 주 DNS 접미사가 없거나,
ms:assetid: 310765bf-a650-4a3d-a5e4-6173b559d4f6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.fqdnmissing(v=EXCHG.150)
ms:contentKeyID: 61203318
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주 DNS 접미사가 없거나,

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2014-01-15_

Exchange를 설치 하는 컴퓨터에 대 한 기본 도메인 이름 시스템 (DNS) 접미사 구성 되지 않았습니다 Microsoft Exchange Server 2013 설치를 계속할 수 없습니다.

이 문제를 해결 하려면 다음 단계를 사용 하 여 컴퓨터에 주 DNS 접미사를 추가 하 고 설치 프로그램을 다시 실행 합니다.


> [!IMPORTANT]
> Exchange 2013을 설치한 후 컴퓨터 이름 또는 주 DNS 접미사 변경 지원 되지 않습니다.



1.  Edge 전송 역할을 설치할 컴퓨터에 로컬 관리자 그룹의 구성원인 사용자로 로그인합니다.

2.  **제어판**을 열고 **시스템**을 두 번 클릭합니다.

3.  **컴퓨터 이름, 도메인 및 작업 그룹 설정** 섹션에서 **설정 변경**을 클릭합니다.

4.  **시스템 속성** 창에 **컴퓨터 이름** 탭이 선택되어 있는지 확인한 다음 <strong>변경...</strong>을 클릭합니다.

5.  **컴퓨터 이름/도메인 변경**에서 <strong>자세히...</strong>를 클릭합니다.

6.  **이 컴퓨터의 주 DNS 접미사**에 Edge 전송 서버의 DNS 도메인 이름을 입력합니다. 예로 contoso.com 등을 들 수 있습니다.

7.  **확인**을 클릭하여 각 창을 닫습니다.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

