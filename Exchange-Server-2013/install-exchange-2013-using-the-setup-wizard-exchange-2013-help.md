---
title: '설치 마법사를 사용하여 Exchange 2013 설치: Exchange 2013 Help'
TOCTitle: 설치 마법사를 사용하여 Exchange 2013 설치
ms:assetid: da690d47-3384-4430-a69e-0cd4d3bf80a7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124778(v=EXCHG.150)
ms:contentKeyID: 50484360
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.ExSetupUI.SetupWizardForm.IntroductionPage
ms.translationtype: HT
---

# 설치 마법사를 사용하여 Exchange 2013 설치

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-06-19_

이 항목에서는 Microsoft Exchange Server 2013 설치 마법사를 사용하여 컴퓨터에 Exchange 2013 사서함 및 클라이언트 액세스 역할을 설치하는 방법에 대해 설명합니다. Exchange 2013 계획 및 배포에 대한 자세한 내용은 [계획 및 배포](planning-and-deployment-for-exchange-2013-installation-instructions.md) 항목을 참조하십시오.

컴퓨터에 Exchange 2013 Edge 전송 역할을 설치하려면 [설치 마법사를 사용하여 Exchange 2013 Edge 전송 역할 설치](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)를 참조하세요. Edge 전송 역할은 사서함 또는 클라이언트 액세스 서버 역할과 같은 컴퓨터에 설치할 수 없습니다.


> [!TIP]
> Exchange Server 배포 도우미에 대해 들어보셨습니까? Exchange Server 배포 도우미는 몇 가지 질문을 하고 사용자 지정된 맞춤형 배포 검사 목록을 만들어 조직에 Exchange 2013을 신속하게 배포할 수 있도록 도와주는 무료 온라인 도구입니다. Exchange Server 배포 도우미에 대한 자세한 내용은 <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 배포 도우미</A>를 참조하세요.




> [!NOTE]
> Exchange 2013을 실행하는 컴퓨터에 서버 역할을 설치한 후 Exchange 2013 설치 마법사를 사용하여 그 컴퓨터에 다른 서버 역할을 추가할 수 없습니다. 컴퓨터에 서버 역할을 추가하려면 제어판에서 프로그램 추가/제거를 사용하거나 명령 프롬프트 창에서 Setup.exe를 사용해야 합니다.



설치 이후에 완료할 작업에 대한 자세한 내용은 [Exchange 2013 설치 후 작업](exchange-2013-post-installation-tasks-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 60분

  - Exchange 2013을 설치하기 전에 릴리스 정보를 읽으십시오. 자세한 내용은 [Exchange Server 2013 릴리스 정보](release-notes-for-exchange-2013-exchange-2013-help.md)를 참조하십시오.

  - 각 조직에 대해 적어도 클라이언트 액세스 서버 한 개와 사서함 서버 한 개가 Active Directory 포리스트에 있어야 합니다. 또한 사서함 서버가 포함된 각 Active Directory 사이트에 클라이언트 액세스 서버도 하나 이상 포함되어야 합니다. 서버 역할을 구분하려면 먼저 사서함 서버 역할을 설치하는 것이 좋습니다.

  - Exchange 2013을 설치하는 컴퓨터는 지원되는 운영 체제(예: Windows Server 2008 R2 SP1(서비스 팩 1) 또는 Windows Server 2012)를 실행하고 충분한 디스크 공간을 갖고 있어야 하며 Active Directory 도메인의 구성원이고 기타 요구 사항을 충족해야 합니다. 시스템 요구 사항에 대한 자세한 내용은 [Exchange 2013 시스템 요구 사항](exchange-2013-system-requirements-exchange-2013-help.md) 항목을 참조하십시오.

  - Exchange 2013 설치를 실행하려면 Microsoft .NET Framework 4.5, Windows Management Framework 3.0 및 기타 필수 소프트웨어를 설치해야 합니다. 모든 서버 역할의 선행 조건을 이해하려면 [Exchange 2013 필수 구성 요소](exchange-2013-prerequisites-exchange-2013-help.md)을 참조하십시오.

  - 이전에 Active Directory 스키마를 준비하지 않은 경우에는 사용하는 계정이 Schema Admins 그룹의 구성원으로 위임되었는지 확인해야 합니다. 조직에 첫 번째 Exchange 2013 서버를 설치하는 경우 사용하는 계정에 Enterprise Administrators 그룹의 구성원 자격이 있어야 합니다. 이미 스키마를 준비하고 조직에서 첫 번째 Exchange 2013 서버를 설치하지 않은 경우 사용하는 계정이 Exchange 2013 Organization Management 역할 그룹의 구성원이어야 합니다.
    
    Delegated Setup 역할 그룹의 구성원인 관리자는 Organization Management 역할 그룹 구성원에 의해 이전에 프로비전된 Exchange 2013 서버를 배포할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!WARNING]
> 서버에 Exchange를 설치한 후 서버 이름을 변경하면 안 됩니다. Exchange 서버 역할을 설치한 후에는 서버 이름 바꾸기가 지원되지 않습니다.



## Exchange Server 2013 설치

조직에 첫 번째 Exchange 2013 서버를 설치하는 경우 Active Directory 준비 단계를 수행하지 않았으면 사용하는 계정에 엔터프라이즈 관리자 그룹의 구성원 자격이 있어야 합니다. Active Directory 스키마를 이전에 준비하지 않은 경우 계정이 Schema Admins 그룹의 구성원이어야 합니다. Active Directory용 Exchange 2013을 준비하는 방법에 대한 자세한 내용은 [Active Directory 및 도메인 준비](prepare-active-directory-and-domains-exchange-2013-help.md)를 참조하세요. 스키마 및 Active Directory 준비 단계를 이미 수행한 경우에는 사용하는 계정이 위임 설치 관리 역할 그룹 또는 조직 관리 역할 그룹의 구성원이어야 합니다.


> [!NOTE]
> 최신 버전의 Exchange 2013을 다운로드하려면 <A href="updates-for-exchange-2013-exchange-2013-help.md">Exchange 2013용 업데이트</A>를 참조하세요.



1.  Exchange 2013을 설치할 컴퓨터에 로그온합니다.

2.  Exchange 2013 설치 파일의 네트워크 위치로 이동합니다.

3.  `Setup.exe`를 두 번 클릭하여 Exchange 2013 설치 시작
    

    > [!IMPORTANT]
    > UAC(사용자 액세스 제어)가 사용되도록 설정된 경우 <CODE>Setup.exe</CODE>를 마우스 오른쪽 단추로 클릭하고 <STRONG>관리자 권한으로 실행</STRONG>을 선택합니다.



4.  **업데이트 확인** 페이지에서 인터넷에 연결하여 Exchange 2013용 제품 및 보안 업데이트를 다운로드할지 여부를 선택합니다. **인터넷 연결 및 업데이트 확인**을 선택하면 업데이트가 다운로드되어 적용된 다음에 설치가 계속됩니다. **지금 업데이트를 확인하지 않음**을 선택하면 나중에 수동으로 업데이트를 다운로드하여 설치할 수 있습니다. 지금 업데이트를 다운로드하여 설치하는 것이 좋습니다. **다음**을 클릭하여 계속합니다.

5.  
    
    **소개** 페이지에서는 조직에 Exchange를 설치하는 프로세스를 시작합니다. 여기서 설치 과정을 안내합니다. 유용한 배포 내용에 대한 몇 가지 링크가 나열됩니다. 설치를 계속하기 전에 이러한 링크를 방문하는 것이 좋습니다. **다음**을 클릭하여 계속합니다.

6.  
    
    **사용권 계약** 페이지에서 소프트웨어 사용 조건을 검토합니다. 약관에 동의하면 **동의함**을 선택하고 **다음**을 클릭합니다.

7.  
    
    **권장 설정** 페이지에서 권장 설정을 사용할지 여부를 선택합니다. **권장 설정 사용**을 선택하면 Exchange에서 컴퓨터 하드웨어 및 Exchange 사용 방법에 대한 오류 보고서와 정보가 Microsoft에 자동으로 전송됩니다. **권장 설정 사용 안 함**을 선택하면 이러한 설정은 비활성화 상태를 유지하지만 설치가 완료된 후에 언제든지 다시 사용하도록 설정할 수 있습니다. 이러한 설정과 Microsoft에 전송된 정보가 사용되는 방식에 대한 자세한 내용을 보려면 **?**를 클릭하십시오.

8.  
    
    **서버 역할 선택** 페이지에서 컴퓨터에 **사서함 역할**이나 **클라이언트 액세스 역할** 중 하나만 설치할지 또는 두 역할을 모두 설치할지, **관리 도구**만 설치할지를 선택합니다. 이번 설치에서 서버 역할을 설치하지 않도록 선택한 경우 나중에 추가할 수 있습니다. 하나의 조직에는 하나 이상의 사서함 역할과 하나 이상의 클라이언트 액세스 서버 역할이 설치되어 있어야 합니다. 이러한 역할을 같은 컴퓨터나 별도의 컴퓨터에 설치할 수 있습니다. 서버 역할을 설치하는 경우 해당 관리 도구가 자동으로 설치됩니다.
    
    **Exchange 서버에 필요한 Windows Server 역할 및 기능을 자동으로 설치합니다.**를 선택하여 설치 마법사가 필요한 Windows 필수 구성 요소를 설치하도록 합니다. 일부 Windows 기능의 설치를 완료하기 위해 컴퓨터를 다시 부팅해야 할 수 있습니다. 이 옵션을 선택하지 않으면 Windows 기능을 수동으로 설치해야 합니다.
    

    > [!NOTE]
    > 이 옵션은 Exchange에 필요한 Windows 기능만 설치합니다. 다른 필수 구성 요소는 수동으로 설치해야 합니다. 자세한 내용은 <A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 필수 구성 요소</A> 항목을 참조하십시오.

    
    **다음**을 클릭하여 계속합니다.

9.  **설치 공간 및 위치** 페이지에서 기본 설치 위치를 그대로 사용하거나 **찾아보기**를 클릭하여 새 위치를 선택합니다. Exchange를 설치하려는 위치에 충분한 디스크 공간이 있는지 확인합니다. **다음**을 클릭하여 계속합니다.

10. 
    
    이 서버가 조직 내 첫 번째 Exchange 서버인 경우 **Exchange 조직** 페이지에서 Exchange 조직의 이름을 입력합니다. Exchange 조직 이름에는 다음 문자만 사용할 수 있습니다.
    
      - A-Z
    
      - a-z
    
      - 0-9
    
      - 공백(선행 또는 후행 아님)
    
      - 하이픈 또는 대시
        

        > [!NOTE]
        > 조직 이름은 64자를 초과할 수 없으며, 비워 둘 수 없습니다.

    
    Active Directory 분할 권한 모델을 사용하려면 **Exchange 조직에 Active Directory 사용 분할 권한 모델 적용**을 선택합니다.
    

    > [!WARNING]
    > 대부분의 조직에서는 Active Directory 분할 권한 모델을 적용할 필요가 없습니다. Active Directory 보안 주체 및 Exchange 구성을 별도로 관리해야 하는 경우 RBAC(역할 기반 액세스 제어) 사용 분할 권한이 적절할 수 있습니다. 자세한 내용을 보려면 <STRONG>?</STRONG>를 클릭합니다.

    
    **다음**을 클릭하여 계속합니다.

11. 사서함 역할을 설치하는 경우 **맬웨어 보호 설정** 페이지에서 맬웨어 검사를 사용할지 또는 사용하지 않을지를 선택합니다. 맬웨어 검사를 사용하지 않도록 설정한 경우 나중에 사용하도록 설정할 수 있습니다. **다음**을 클릭하여 계속합니다.

12. 
    
    **준비 검사** 페이지에서 상태를 보고 조직 및 서버 역할 선행 조건 검사가 완료되었는지 확인합니다. 완료되지 않은 경우 Exchange 2013을 설치하려면 보고된 오류를 해결해야 합니다. 일부 선행 조건 오류는 설치 프로그램을 종료하지 않고도 해결할 수 있습니다. 보고된 오류를 해결했으면 **뒤로**를 클릭한 후 **다음**을 클릭하여 선행 조건 검사를 실행합니다. 또한 보고된 경고를 검토해야 합니다. 준비 검사가 완료되었으면 **다음**을 클릭하여 Exchange 2013을 설치합니다.

13. 
    
    **완료** 페이지에서 **마침**을 클릭합니다.

14. Exchange 2013이 완료된 후 컴퓨터를 다시 시작합니다.

15. [Exchange 2013 설치 후 작업](exchange-2013-post-installation-tasks-exchange-2013-help.md)에서 제공된 작업을 수행하여 배포를 완료합니다.

## 작동 여부는 어떻게 확인합니까?

Exchange 2013이 성공적으로 설치되었는지 확인하려면 [Exchange 2013 설치를 확인 합니다.](verify-an-exchange-2013-installation-exchange-2013-help.md) 항목을 참조하십시오.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

