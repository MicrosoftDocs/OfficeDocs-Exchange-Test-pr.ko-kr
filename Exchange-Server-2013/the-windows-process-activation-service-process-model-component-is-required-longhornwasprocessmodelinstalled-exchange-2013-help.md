---
title: 'Windows Process Activation Service-프로세스 모델 구성 요소는 required_LonghornWASProcessModelInstalled: Exchange 2013 Help'
TOCTitle: Windows Process Activation Service-프로세스 모델 구성 요소는 required_LonghornWASProcessModelInstalled
ms:assetid: 8cc13dbb-4921-4c07-8602-d26613d7730a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.longhornwasprocessmodelinstalled(v=EXCHG.150)
ms:contentKeyID: 50483614
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows Process Activation Service-프로세스 모델 구성 요소는 required\_LonghornWASProcessModelInstalled

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2015-04-07_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Exchange Server 2010 설치 Windows Server 2008 에서 설치를 계속할 수- Windows Server 2008 R2 기반 컴퓨터 또는 서버에 Windows Process Activation Service-프로세스 모델 기능이 설치 되지 않아 합니다.

Windows Process Activation Service를 인터넷 정보 서비스 (IIS) 프로세스 모델을 일반화 HTTP에 대 한 종속성을 제거 합니다. 이전에 HTTP 응용 프로그램에만 사용할 수 있었던 IIS의 모든 기능을 비 HTTP 프로토콜을 사용 하 여 Windows Communication Foundation (WCF) 서비스를 호스팅하는 응용 프로그램에 제공 됩니다. IIS 7.0는 또한 HTTP를 통한 메시지 기반 정품 인증에 대 한 Windows Process Activation Service를 사용합니다.

웹 서버 및 WCF 서비스를 호스트 하는 프로세스 모델입니다. IIS 6.0 프로세스 모델에서에서 도입 된은 새 아키텍처 해당 기능 신속한 오류 보호 상태를 모니터링 하 고 재생 합니다.

이 문제를 해결 하려면 Windows Process Activation Service-이 서버에서 프로세스 모델 기능을 설치 하 고 Exchange 2010 설치 프로그램을 다시 실행 하십시오.

Windows Process Activation Service-서버 관리자 도구를 사용 하 여 프로세스 모델 기능을 설치 합니다.

1.  **시작**, **관리 도구** 를 선택한 다음 **서버 관리자** 를 클릭 합니다.

2.  왼쪽된 탐색 창의 **기능** 을 마우스 오른쪽 단추로 클릭 하 고 **기능 추가** 클릭 합니다.

3.  **기능 선택** 창에서 **Windows Process Activation Service** 까지 아래로 스크롤하십시오.

4.  **프로세스 모델** 에 대 한 확인란을 선택 합니다.

5.  **기능 선택** 창에서 **다음** 을 클릭 하 고 **설치 선택 사항 확인** 창에서 **설치** 를 클릭 합니다.

6.  **Close** 역할 서비스 추가 마법사를 종료를 클릭 합니다.

