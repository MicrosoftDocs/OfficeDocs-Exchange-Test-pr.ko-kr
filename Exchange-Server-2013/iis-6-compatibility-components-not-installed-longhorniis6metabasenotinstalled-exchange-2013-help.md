---
title: 'IIS 6 호환성 구성 요소 하지 installed_LonghornIIS6MetabaseNotInstalled: Exchange 2013 Help'
TOCTitle: IIS 6 호환성 구성 요소 하지 installed_LonghornIIS6MetabaseNotInstalled
ms:assetid: 0bd52987-d3cc-496c-ac8c-d35591405195
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.longhorniis6metabasenotinstalled(v=EXCHG.150)
ms:contentKeyID: 50482479
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 6 호환성 구성 요소 하지 installed\_LonghornIIS6MetabaseNotInstalled

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft®Exchange Server 2007 설치는 다음 Windows 운영 체제에 클라이언트 액세스 서버 서버 역할, 사서함 서버 역할 또는 Exchange 2007 관리 도구를 설치 하는 시도 계속할 수 없습니다.

  - Windows Server 2008 R2

  - Windows Server 2008

  - Windows 7 (관리 도구에만 해당)

  - Windows Vista (관리 도구에만 해당)

이 문제는 인터넷 정보 서버 (IIS) 6 메타 베이스 호환성 구성 요소 및 IIS 6 관리 콘솔 구성 요소 설치 되지 않은 때문에 발생 합니다.

Exchange 2007 설치 Exchange 2007 클라이언트 액세스 서버 역할, 사서함 서버 역할 또는 Exchange 2007 관리 도구를 설치 하는 컴퓨터에 IIS 6 메타 베이스 호환성 구성 요소 및 IIS 6 관리 콘솔 구성 요소가 설치 해야 합니다.

이 문제를 해결 하려면 대상 컴퓨터에서 IIS 6 메타 베이스 호환성 구성 요소를 설치 하 고 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

서버 관리자 도구를 사용 하 여 Windows Server 또는 Windows Server 2008 r 2에는 IIS 6.0 관리 호환성 구성 요소 설치

1.  **시작**, **관리 도구**를 차례로 클릭하고 **서비스 관리자**를 클릭합니다.

2.  탐색 창에서 **역할** 을 확장, **웹 서버 (IIS)** 마우스 오른쪽 단추로 클릭 하 고 **역할 서비스 추가** 클릭 합니다.

3.  **역할 서비스 선택** 창에서 **IIS 6 관리 호환성** 까지 아래로 스크롤하십시오.

4.  **IIS 6 메타 베이스 호환성**, **IIS 6 WMI 호환성** 및 **IIS 6 관리 콘솔** 확인란을 선택 하려면이 옵션을 클릭 합니다.

5.  **역할 서비스 선택** 창에서 **다음** 을 클릭 합니다.

6.  **설치 선택 사항 확인** 창에서 **설치** 를 클릭 합니다.

7.  **Close** 역할 서비스 추가 마법사를 종료를 클릭 합니다.

제어판에서 Windows Vista 또는 Windows 7에에서는 IIS 6.0 관리 호환성 구성 요소를 설치 합니다.

1.  **시작** 을 클릭, **제어판** 을 차례로 클릭 하, **프로그램 및 기능을** 클릭 하 고 **Windows 기능 사용 설정 또는 해제** 를 클릭 합니다.

2.  **인터넷 정보 서비스** 를 엽니다.

3.  **웹 관리 도구** 를 엽니다.

4.  **IIS 6.0 관리 호환성** 을 엽니다.

5.  **IIS 6 메타 베이스 및 IIS 6 구성 호환성**, **IIS 6 WMI 호환성** 및 **IIS 6 관리 콘솔** 확인란을 선택 하려면이 옵션을 클릭 합니다.

6.  **확인**을 클릭합니다.

