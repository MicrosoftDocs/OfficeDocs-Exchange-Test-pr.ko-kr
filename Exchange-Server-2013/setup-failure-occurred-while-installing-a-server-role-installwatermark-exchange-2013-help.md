---
title: '서버 role_InstallWatermark를 설치 하는 동안 설치 프로그램 오류가 발생 했습니다.: Exchange 2013 Help'
TOCTitle: 서버 role_InstallWatermark를 설치 하는 동안 설치 프로그램 오류가 발생 했습니다.
ms:assetid: ad89ebd5-f9bb-40c1-8811-09b145c2b341
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.installwatermark(v=EXCHG.150)
ms:contentKeyID: 50483922
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 서버 role\_InstallWatermark를 설치 하는 동안 설치 프로그램 오류가 발생 했습니다.

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft Exchange Server 2007 설치 프로그램은 이전에 설치 오류가 발생 한 서버 역할을 설치 하는 동안 발생 했기 때문에 계속할 수 없습니다.

Exchange 2007 설치 프로그램에서는 실패 한 서버 역할 설치를 성공적으로 되어야 다시 설치 하거나 다른 설치 작업을 계속 하기 전에 설치 과정에서 제거 합니다.

이 문제를 해결 하기 위해 방금 오류가 발생 한 서버 역할을 다시 설치 또는 서버 역할을 제거 합니다.

명령줄에서 오류가 발생 한 서버 역할을 다시 설치 하려면

1.  명령 프롬프트 창을 열고 설치 파일을 이동 합니다.

2.  다음 명령을 실행합니다.
    
        Setup /roles:<Failed Server Role>
    
    하나 이상의 쉼표로 구분 된 목록에서 다음 역할에서이 옵션을 선택 합니다.
    
    ClientAccess (또는 CA 또는 C)
    
    EdgeTransport (또는 ET, 또는 E)
    

    > [!NOTE]
    > Edge 전송 서버 역할은 다른 서버 역할과 함께 동일한 컴퓨터에 함께 사용할 수 없습니다.

    

    > [!NOTE]
    > 경계 네트워크에 및 Active Directory 포리스트 외부 Edge 전송 서버 역할을 배포 해야 합니다.

    
    HubTransport (또는 HT, 또는 H)
    
    사서함 (또는 MB, 또는 M)
    
    UnifiedMessaging (또는 UM, 또는 U)
    
    ManagementTools (또는 체, 또는 T)
    

    > [!NOTE]
    > ManagementTools를 지정 하는 경우 Exchange 관리 콘솔, Exchange 관리 셸, Exchange 도움말 파일, Exchange 모범 사례 분석기 도구 대 한 Exchange cmdlet 및 Exchange 문제해결 도우미 설치 합니다. 다른 서버 역할을 설치 하는 경우 관리 도구는 자동으로 설치 됩니다.

    
    예, 기존 사서함 서버에 허브 전송 서버 역할을 추가 하려면 다음을 입력: **%LocalExchangeInstallationDir%\\bin\\Setup.com /role:HubTransport /Mode:Install**


> [!NOTE]
> 모든 Exchange Server 2007 서버 역할 이전에 설치 된 경우 성공적으로 사용 하 여 설치 마법사가 유지 관리 모드에서 실행 됩니다. 이전에 Exchange 2007 서버 역할이 성공적으로 설치 된, 설치 마법사에서 중지 한 위치에서 시작 합니다.



오류가 발생 한 서버 역할을 다시 설치를 유지 관리 모드에서 Exchange Server 2007 설치 마법사를 사용 하 여

1.  서버 역할을 다시 설치 하려는 서버에 로그온 합니다.

2.  제어판을 열고 **프로그램 추가 / 제거** 를 두번클릭 합니다.

3.  **프로그램 변경 / 제거** 페이지에서 **Microsoft Exchange 서버** 를 선택한 다음 **변경** 을 클릭 합니다.

4.  Exchange Server 2007 설치 마법사의 **Exchange 유지 관리 모드** 페이지에서 **다음** 을 클릭 합니다.

5.  **서버 역할 선택** 페이지에서 서버 역할을 설치 하려는 대 한 확인란을 선택 하 고 을 클릭 합니다.
    

    > [!NOTE]
    > Edge 전송 서버 역할은 다른 서버 역할과 함께 동일한 컴퓨터에 함께 사용할 수 없습니다.

    

    > [!NOTE]
    > 경계 네트워크에 및 Active Directory 포리스트 외부 Edge 전송 서버 역할을 배포 해야 합니다.

    

    > [!NOTE]
    > 관리 도구를 선택 하는 경우 Exchange 관리 콘솔, Exchange 관리 셸 대 한 Exchange cmdlet 및 Exchange 도움말 파일을 설치 합니다. 다른 서버 역할을 설치 하는 경우 관리 도구를 자동으로 설치 됩니다.



6.  **허브 전송 역할** 선택 하 고 포리스트의 Exchange 2007 를 설치 하는 경우는는 기존 Exchange Server 2003 또는 Exchange 2000 Server 조직 하는 경우 **메일 흐름 설정** 페이지에서 선택 브리지 헤드 서버 Exchange 2003 의 구성원 인 기존 조직 또는 라우팅 그룹 커넥터를 만들려면 Exchange 2000 라우팅 그룹에 있습니다.

7.  **준비 검사** 페이지에서 조직 및 서버 역할 필수 구성 요소를 확인 하는 경우를 확인 하려면 상태 보기는 성공적으로 완료 합니다. 성공적으로 완료 한, Exchange 2007 를 설치 하려면 **설치** 를 클릭 합니다.

8.  **완료** 페이지에서 **마침**을 클릭합니다.

서버 역할이 없는 경우 오류가 발생 한 서버 역할을 다시 설치 하는 Exchange Server 2007 설치 마법사를 사용 하 여 이전에 성공적으로 설치 되었으면

1.  Exchange Server 2007 제품 설명서에서 "어떻게 수행을 사용자 지정 설치를 사용 하 여 Exchange Server 2007 설치 프로그램을" ([https://go.microsoft.com/fwlink/?LinkId=86648](https://go.microsoft.com/fwlink/?linkid=86648))의 지침을 따릅니다.

오류가 발생 한 서버 역할을 제거 하려면

1.  Exchange Server 2007 제품 설명서에서 "어떻게에 Exchange 2007 서버 역할 제거" ([https://go.microsoft.com/fwlink/?LinkId=86649](https://go.microsoft.com/fwlink/?linkid=86649))의 지침을 따릅니다.

## 자세한 내용

무인 모드로 Exchange 2007을 설치 하는 방법에 대 한 자세한 내용은 "어떻게를 설치 Exchange 2007에서 무인 모드" ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476))을 참조 하십시오.

