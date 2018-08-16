---
title: 'Exchange 2013 관리 도구 설치: Exchange 2013 Help'
TOCTitle: Exchange 2013 관리 도구 설치
ms:assetid: 71fcbe4c-783b-4f77-aabb-a21aa7a4ef23
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232090(v=EXCHG.150)
ms:contentKeyID: 50556011
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 관리 도구 설치

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2013-01-28_

Microsoft Exchange Server 2013 관리 도구를 사용하면 Exchange 조직을 원격으로 구성하고 관리할 수 있습니다. Exchange 2013 관리 도구에는 Exchange 관리 셸 및 Exchange 도구 상자가 포함되어 있습니다. 이 항목에서는 Setup.exe나 무인 설치 모드를 사용하여 Exchange 2013 관리 도구를 설치하는 방법을 설명합니다.


> [!NOTE]
> EAC(Exchange 관리 센터)를 원격으로 사용하기 위해 이 절차를 수행할 필요는 없습니다. EAC는 Exchange 2013 클라이언트 액세스 서버 역할을 실행하는 컴퓨터에서 호스트되는 웹 기반 콘솔입니다. 원격으로 EAC에 액세스하는 방법에 대한 자세한 내용은 <A href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Exchange 2013의 Exchange 관리 센터</A>를 참조하십시오.



Exchange 2013 관리에 대한 자세한 내용은 [Exchange 2013의 Exchange 관리 센터](exchange-admin-center-in-exchange-2013-exchange-2013-help.md) 및 [PowerShell을 사용 하 여 Exchange 2013 (Exchange 관리 셸)](https://technet.microsoft.com/ko-kr/library/bb123778\(v=exchg.150\))을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분

  - Exchange 2013을 설치하기 전에 릴리스 정보를 읽으십시오. 자세한 내용은 [Exchange Server 2013 릴리스 정보](release-notes-for-exchange-2013-exchange-2013-help.md)를 참조하십시오.

  - 관리 도구를 설치하는 컴퓨터에는 지원되는 운영 체제(예: Windows Server 2012 또는 Windows 8)와 충분한 디스크 공간이 있어야 하고, Active Directory 도메인의 구성원이어야 하며 기타 요구 사항을 충족해야 합니다. 시스템 요구 사항에 대한 자세한 내용은 [Exchange 2013 시스템 요구 사항](exchange-2013-system-requirements-exchange-2013-help.md) 항목을 참조하십시오.

  - Exchange 2013 설치 프로그램을 실행하려면 Microsoft .NET Framework 4.5, Windows Management Framework 3.0 및 기타 필수 소프트웨어를 설치해야 합니다. 모든 서버 역할의 선행 조건을 이해하려면 [Exchange 2013 필수 구성 요소](exchange-2013-prerequisites-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 설치 프로그램을 사용하여 Exchange 2013 관리 도구 설치

1.  Exchange 2013을 설치할 컴퓨터에 로그온합니다.

2.  Exchange 2013 설치 파일의 네트워크 위치로 이동합니다.

3.  `Setup.exe`를 두 번 클릭하여 Exchange 2013 설치 시작
    

    > [!IMPORTANT]
    > UAC(사용자 액세스 제어)가 사용되도록 설정된 경우 <CODE>Setup.exe</CODE>를 마우스 오른쪽 단추로 클릭하고 <STRONG>관리자 권한으로 실행</STRONG>을 선택합니다.



4.  <strong>업데이트 확인</strong> 페이지에서 인터넷에 연결하여 Exchange 2013용 제품 및 보안 업데이트를 다운로드할지 여부를 선택합니다. <strong>인터넷 연결 및 업데이트 확인</strong>을 선택하면 업데이트가 다운로드되어 적용된 다음에 설치가 계속됩니다. <strong>지금 업데이트를 확인하지 않음</strong>을 선택하면 나중에 수동으로 업데이트를 다운로드하여 설치할 수 있습니다. 지금 업데이트를 다운로드하여 설치하는 것이 좋습니다. <strong>다음</strong>을 클릭하여 계속합니다.

5.  
    
    <strong>소개</strong> 페이지에서는 조직에 Exchange를 설치하는 프로세스를 시작합니다. 여기서 설치 과정을 안내합니다. 유용한 배포 내용에 대한 몇 가지 링크가 나열됩니다. 설치를 계속하기 전에 이러한 링크를 방문하는 것이 좋습니다. <strong>다음</strong>을 클릭하여 계속합니다.

6.  
    
    <strong>사용권 계약</strong> 페이지에서 소프트웨어 사용 조건을 검토합니다. 약관에 동의하면 <strong>동의함</strong>을 선택하고 <strong>다음</strong>을 클릭합니다.

7.  
    
    <strong>권장 설정</strong> 페이지에서 권장 설정을 사용할지 여부를 선택합니다. <strong>권장 설정 사용</strong>을 선택하면 컴퓨터 하드웨어 및 Exchange 사용 방법에 대한 오류 보고서와 정보가 Microsoft에 자동으로 전송됩니다. <strong>권장 설정 사용 안 함</strong>을 선택하면 이러한 설정은 비활성화 상태를 유지하지만 설치가 완료된 후에 언제든지 다시 사용하도록 설정할 수 있습니다. 이러한 설정과 Microsoft에 전송된 정보가 사용되는 방식에 대한 자세한 내용을 보려면 <strong>?</strong>를 클릭하십시오.

8.  
    
    <strong>서버 역할 선택</strong> 페이지에서 <strong>관리 도구</strong>가 선택되어 있는지 확인합니다.
    
    <strong>Exchange Server에 필요한 Windows Server 역할 및 기능을 자동으로 설치합니다.</strong>를 선택하여 설치 마법사가 필요한 Windows 필수 구성 요소를 설치하도록 합니다. 일부 Windows 기능의 설치를 완료하기 위해 컴퓨터를 다시 부팅해야 할 수 있습니다. 이 옵션을 선택하지 않으면 Windows 기능을 수동으로 설치해야 합니다.
    

    > [!NOTE]
    > 이 옵션은 Exchange에 필요한 Windows 기능만 설치합니다. 다른 필수 구성 요소는 수동으로 설치해야 합니다. 자세한 내용은 <A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 필수 구성 요소</A>를 참조하십시오.

    
    <strong>다음</strong>을 클릭하여 계속합니다.

9.  <strong>설치 공간 및 위치</strong> 페이지에서 기본 설치 위치를 그대로 사용하거나 <strong>찾아보기</strong>를 클릭하여 새 위치를 선택합니다. Exchange를 설치하려는 위치에 충분한 디스크 공간이 있는지 확인합니다. <strong>다음</strong>을 클릭하여 계속합니다.

10. 
    
    조직에서 Exchange 2013 설치 프로그램을 처음 실행한 경우 <strong>Exchange 조직</strong> 페이지에서 Exchange 조직의 이름을 입력합니다. Exchange 조직 이름에는 다음 문자만 사용할 수 있습니다.
    
      - A-Z
    
      - a-z
    
      - 0-9
    
      - 공백(선행 또는 후행 아님)
    
      - 하이픈 또는 대시
        

        > [!NOTE]
        > 조직 이름은 64자를 초과할 수 없으며, 비워 둘 수 없습니다.

    
    Active Directory 사용 분할 권한 모델을 사용하려면 <strong>Exchange 조직에 Active Directory 사용 분할 권한 모델 적용</strong>을 선택합니다.
    

    > [!WARNING]
    > 대부분의 조직에서는 Active Directory 사용 분할 권한 모델을 적용할 필요가 없습니다. Active Directory 보안 주체 및 Exchange 구성을 별도로 관리해야 하는 경우 RBAC(역할 기반 액세스 제어) 사용 분할 권한이 적절할 수 있습니다. 자세한 내용을 보려면 <STRONG>?</STRONG>를 클릭합니다.

    
    <strong>다음</strong>을 클릭하여 계속합니다.

11. 
    
    <strong>준비 검사</strong> 페이지에서 상태를 보고 조직 및 서버 역할 선행 조건 검사가 완료되었는지 확인합니다. 완료되지 않은 경우 Exchange 2013을 설치하려면 보고된 오류를 해결해야 합니다. 일부 선행 조건 오류는 설치 프로그램을 종료하지 않고도 해결할 수 있습니다. 보고된 오류를 해결했으면 <strong>뒤로</strong>를 클릭한 후 <strong>다음</strong>을 클릭하여 선행 조건 검사를 실행합니다. 또한 보고된 경고를 검토해야 합니다. 준비 검사가 완료되었으면 <strong>다음</strong>을 클릭하여 Exchange 2013을 설치합니다.

12. 
    
    <strong>완료</strong> 페이지에서 <strong>마침</strong>을 클릭합니다.

13. Exchange 2013이 완료된 후 컴퓨터를 다시 시작합니다.

## 무인 설치 모드를 사용하여 Exchange 2013 관리 도구 설치

1.  Exchange 2013 관리 도구를 설치할 컴퓨터에 로그온합니다.

2.  Exchange 2013 설치 파일의 네트워크 위치로 이동합니다.

3.  명령 프롬프트에서 다음 명령을 실행합니다.
    

    > [!IMPORTANT]
    > UAC(사용자 액세스 제어)를 사용하도록 설정한 경우 관리자 권한 명령 프롬프트에서 <CODE>Setup.exe</CODE>를 실행해야 합니다.

    
        Setup.exe /Role:ManagementTools /IAcceptExchangeServerLicenseTerms

자세한 내용은 [무인 모드로 Exchange 2013 설치](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)를 참조하십시오.

