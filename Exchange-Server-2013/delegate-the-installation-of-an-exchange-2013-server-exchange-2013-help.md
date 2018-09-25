---
title: 'Exchange 2013 서버의 설치 위임: Exchange 2013 Help'
TOCTitle: Exchange 2013 서버의 설치 위임
ms:assetid: f2fc8680-0c7c-4a29-b8f5-d77404fec280
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201741(v=EXCHG.150)
ms:contentKeyID: 62614006
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 서버의 설치 위임

 

_**적용 대상:** Exchange Online, Exchange Server, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-07-31_

Exchange Server 2013 를 사용 하면 Exchange 2013 조직 관리 역할 그룹의 구성원 없는 사람에 게 Exchange 서버 설치를 위임할 수 있습니다. 이 종종 유용 대기업의 위치를 설치 하 고 서버 설정 사람 없는 Exchange 와 같은 서비스를 관리 하는 동일한 사람입니다. 수행 하려는 것 처럼 소리이 하는 경우이 항목은 있습니다.

일반적으로 Exchange 를 설치할 때 업데이트를 설치 하는 사용자 필요는 [조직 관리](organization-management-exchange-2013-help.md) 역할 그룹의 구성원 이어야 합니다. 이 없기 때문 Exchange 를 설치할 때 Active Directory 변경 사항이 조직 관리 역할 그룹의 구성원 인 Exchange 관리자만 이러한 변경을 수행할 수 있습니다. 다음 목록에는 변경 된 내용이 보여줍니다.

  - 서버 개체를 **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<Organization Name\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<Root Domain\>** 구성 파티션에 만들어집니다.

  - 다음 액세스 제어 항목 (Ace) Delegated Setup 역할 그룹에 대 한 구성 파티션 내에서 서버 개체에 추가 됩니다.
    
      - 서버 개체 및 해당 하위 개체에 대 한 모든 권한
    
      - 액세스 제어 항목의 이름으로 보내기 권한을 확장에 대 한 거부
    
      - 액세스 제어 항목으로 받기 오른쪽 확장에 대 한 거부
    
      - 공용 폴더 저장소 개체 변수가 CreateChild 및 DeleteChild 권한 Exchange 에 대 한 거부
    

    > [!NOTE]
    > 공용 폴더는 조직 수준 관리 따라서 작성 및 삭제 되는 공용 폴더 저장소 Exchange 는 관리자에 게 제한 됩니다.



  - 서버에 대 한 Active Directory 컴퓨터 계정은 Exchange 서버 그룹에 추가 됩니다.

  - 서버는 Exchange 관리 센터 프로 비전 된 서버로 추가 됩니다.

대기업을 설치 하 고 새 서버를 자주 설정 사람 Exchange 관리자를 없습니다. Exchange 를 설치할 수 있도록, Exchange 관리자에 *프로 비전* 서버 Active Directory 에 수 있습니다. 서버를 구축 하는 경우 모든 함수에는 새 Exchange 서버에 필요한 변경 내용 된 Active Directory 별도로에서 실제 Exchange 컴퓨터에 설치 합니다. Exchange 관리자 Active Directory 시간 또는 짝수 일 Exchange 를 새 컴퓨터에 설치 하기 전에 새 서버를 프로 비전 할 수 있습니다. 서버를 한 후 프로 비전 된, Exchange 를 설치 하려면 [위임 설치](delegated-setup-exchange-2013-help.md) 역할 그룹의 구성원 수에 설치 요구를 수행 하는 사용자입니다. Delegated Setup 역할 그룹 구성원 프로 비전 된 서버를 설치 하는 것을 허용 합니다.

답변을 사용 하는 방법에 대 한 위임 설치 하는 경우 다음을 염두에 두십시오.

  - Exchange 2013 서버를 하나 이상 추가 서버 설치를 위임할 수 전에 이미 설치 되어 있음 첫번째 서버를 설치 하는 사람 Exchange 관리자가 있어야 합니다. 자세한 내용은 [검사 목록: Exchange 2013의 새로운 설치를 수행 합니다.](checklist-perform-a-new-installation-of-exchange-2013-exchange-2013-help.md)를 체크아웃 합니다.

  - 위임 된 사용자는 Exchange 서버를 제거할 수 없습니다. Exchange 서버를 제거 하려면 Exchange 관리자 해야 합니다.

## Exchange 2013 서버를 프로 비전 하는 어떻게 합니까?

Exchange 에 대 한 서버를 구축 하려면 Exchange 2013 를 사용 하 여 명령줄 설치 합니다. Windows 명령 프롬프트 매우 익숙한 모르는 경우 걱정 하지 마십시오. 이 항목 정확 하 게 필요한 작업을 수행 하기에 대해 설명 합니다. 시작 하기 전에 염두에는 문서는 관련 된 몇가지 사항은 다음과 같습니다.

  - 해야 하는 서버를 구축 하는 조직 관리 역할 그룹의 구성원 이어야 합니다.

  - Exchange 2013 의 최신 릴리스가 있어야 합니다. [Exchange 2013용 업데이트](updates-for-exchange-2013-exchange-2013-help.md)에서 다운로드 링크를 얻을 수 있습니다.

프로 비전 하는 컴퓨터에서 설치 프로그램을 실행 중인 여부 또는 여부 다른 컴퓨터에서 실행 중인 서버를 구축 하는데 사용 하는 명령에 따라 달라 집니다. 설치 프로그램을 실행 하는 위치와 일치 하는 다음 단계에서 명령을 선택 합니다.

1.  Windows 키 + R을 누릅니다 '' **실행** 창을 엽니다.

2.  **열** 을에서**cmd.exe**를 입력 하 고 enter 키를 눌러 **Windows 명령 프롬프트** 를 엽니다.

3.  다운로드 및 Exchange 2013 설치 파일을 확장 하는 디렉터리를 변경 합니다. 설치 파일을 `C:\Downloads\Exchange 2013`에 있는 경우에 다음 명령을 사용 합니다.
    
    ```powershell
    CD "C:\Downloads\Exchange 2013"
    ```

4.  설치 프로그램을 실행 하는 위치와 일치 하는 명령을 선택 합니다.
    
      - **구축 하는 컴퓨터에서 설치 프로그램을 실행 중인 경우**, 다음 명령을 실행 합니다.
        
        ```powershell
        Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
        ```
    
      - **다른 컴퓨터에서 설치 프로그램을 실행 하는 경우**, 다음 명령을 실행 합니다.
        
        ```powershell
        Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms
        ```

5.  서버를 프로 비전 한 후에 Exchange Delegated Setup 역할 그룹에 프로 비전 된 서버에 설치할 수 있어야 하는 사용자를 추가 했을 때 있는지 확인 해야 합니다. 역할 그룹에 사용자를 추가 하는 방법을 [관리 역할 그룹 구성원](manage-role-group-members-exchange-2013-help.md)을 참조 하십시오.

다음이 단계를 마치면 컴퓨터 Exchange 를 설치할 준비가 됩니다. Exchange 2013[설치 마법사를 사용하여 Exchange 2013 설치](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)의 단계를 사용 하 여 프로 비전 된 서버에 설치할 수 있습니다.

## 작동 여부를 확인하려면 어떻게 해야 합니까?

서버를 올바르게 Exchange 에 대 한 프로 비전 하려면 다음을 수행할 수 있습니다.

1.  **시작** 을 이동 \> **관리 도구** 및 다음 open **Active Directory 사용자 및 컴퓨터** 입니다.

2.  **Microsoft Exchange 보안 그룹** 을 선택 하 고 **Exchange 서버** 두번클릭 **구성원** 탭을 선택 합니다.

3.  **구성원** 탭에서 방금 프로 비전 하는 서버는 보안 그룹의 구성원으로 나열 하는 경우를 확인 합니다.

서버에는 Exchange 서버 보안 그룹의 구성원으로 나열 되어있는지, 구축 제대로 않았습니다. Exchange 해당 서버에 설치할 수 Delegated Setup 역할 그룹의 구성원 인 사용자입니다.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

