---
title: '크로스 포리스트 토폴로지에서 Exchange 2013 배포: Exchange 2013 Help'
TOCTitle: 크로스 포리스트 토폴로지에서 Exchange 2013 배포
ms:assetid: 65be650f-d435-4f60-9ff0-5cb88a726abb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998597(v=EXCHG.150)
ms:contentKeyID: 51407702
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 크로스 포리스트 토폴로지에서 Exchange 2013 배포

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

이 항목에서는 Microsoft Forefront Identity Manager 2010 R2 SP1을 사용하여 포리스트 간 토폴로지에서 Exchange 2013을 배포하는 방법에 대해 설명합니다. 포리스트 간 토폴로지에서 Exchange 2013을 배포하려면 각 포리스트에 Exchange 2013을 설치한 다음 포리스트를 연결하여 사용자가 포리스트 전체에서 주소와 가용성 데이터를 확인할 수 있도록 해야 합니다.

다음 그림은 두 Exchange 2013 포리스트 간 사용자 동기화를 보여줍니다.

**Exchange 2013 포리스트 간 동기화 예**

![Exchange 2010 다중 포리스트 예](images/Aa998597.df0ba5dd-cb96-4542-98bd-2a425defe317(EXCHG.150).gif "Exchange 2010 다중 포리스트 예")

이 항목에서는 전용 Exchange 포리스트(또는 리소스 포리스트) 토폴로지에서 Exchange 2013을 배포하는 방법에 대해서는 설명하지 *않습니다*. 리소스 포리스트 토폴로지에서 Exchange 2013을 배포하는 방법에 대한 자세한 내용은 [Exchange 리소스 포리스트 토폴로지에서 Exchange 2013 배포](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

Exchange 2013에서 다음 절차를 수행하려면 다음을 확인합니다.

  - 조직의 포리스트 전체에 걸쳐 이름 확인을 위한 DNS(Domain Name System)가 올바르게 구성되어 있습니다. DNS가 올바르게 구성되어 있는지 확인하려면 Ping 도구를 사용하여 조직의 다른 포리스트 및 GAL Sync 에이전트를 실행할 서버에서 각 포리스트에 대한 연결을 테스트합니다.

  - GALSync MA(관리 에이전트)는 Exchange 2013 PowerShell V2.0 RTM을 사용하여 Windows 포리스트와 통신합니다. 제어판으로 이동한 후 프로그램 및 기능을 클릭하여 Windows PowerShell v1.0이 이 컴퓨터에 설치되어 있지 않은지 확인합니다.

  - Windows 업데이트를 통해 Windows 원격 관리가 설치되지 않았는지 확인합니다.

  - Windows PowerShell과 Windows 원격 관리를 설치합니다. 자세한 내용은 Microsoft 기술 자료 문서 968930, [Windows Management Framework 핵심 패키지(Windows PowerShell 2.0 및 WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)를 참조하십시오.

  - Forefront Identity Manager 2010 R2 s p 1을 다운로드 합니다. [Microsoft Forefront Identity Manager 2010 R2 s p 1을 다운로드](https://go.microsoft.com/fwlink/p/?linkid=279868)를 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## Forefront Identity Manager 2010 R2 SP1을 사용하여 포리스트 간 토폴로지에서 Exchange 2013 배포

1.  각 포리스트에서 Exchange 2013을 별도로 설치합니다. Exchange 2013을 설치하려면 단일 포리스트 토폴로지에서 Exchange 2013을 설치하는 경우와 동일한 단계를 수행합니다. 자세한 단계는 다음 항목 중 하나를 참조하십시오.
    
      - [Exchange 2013 새 설치 배포](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [설치 마법사를 사용하여 Exchange 2013 설치](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)
        

        > [!NOTE]
        > 이 항목에는 기존 Exchange 2007 또는 Exchange 2010 토폴로지 하지 있다고 가정 합니다. 기존 Exchange 토폴로지 않은 업그레이드할 하는 경우에 <A href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Exchange 2010에서 Exchange 2013으로 업그레이드</A> 또는 <A href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Exchange 2007에서 Exchange 2013으로 업그레이드</A>참조 하십시오.



2.  각 포리스트에서 Active Directory 사용자 및 컴퓨터를 사용하여 FIM 2010 R2 SP1이 다른 포리스트의 각 사서함에 대한 연락처를 만드는 데 사용할 컨테이너를 만듭니다. 이 컨테이너의 이름을 **FromFIM**으로 지정하는 것이 좋습니다. 컨테이너를 만들려면 컨테이너를 만들 도메인을 선택하고 도메인을 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기** \> **조직 구성 단위**를 차례로 선택합니다. **새 개체 - 조직 구성 단위**에 **FromFIM**을 입력하고 **확인**을 클릭합니다.

3.  Forefront Identify Manager를 사용하여 각 포리스트에 대해 GALSync 관리 에이전트를 만듭니다. 이를 통해 각 포리스트의 사용자를 동기화하고 공통 GAL을 만들 수 있습니다. 자세한 단계는 다음 리소스를 참조하십시오.
    
      - [전체 주소 목록 (gal 전체) Forefront Identity Manager 2010 (FIM)와 동기화 구성](https://go.microsoft.com/fwlink/p/?linkid=279869)
    
      - [관리 에이전트를 사용한 작업](https://go.microsoft.com/fwlink/p/?linkid=279870)
    
      - [Forefront Identity Manager 2010 R2 설명서 로드맵](https://go.microsoft.com/fwlink/p/?linkid=279871)
    

    > [!IMPORTANT]
    > 리소스 Exchange 2010 논의 하는 동안 Exchange 2013 FIM 2010 R2 s p 1에 대 한 지원 됩니다. Exchange 2013 에 대 한 FIM 2010 R2 s p 1의 <STRONG>내선 번호</STRONG> 를 구성 하는 있는지 확인 하십시오.

    
    1.  **확장 구성** 페이지의 **프로비전 대상:** 옆에 있는 **파티션 표시 이름 구성**에서 **Exchange 2013**을 선택합니다. **Exchange 2013 RPS URI** 필드가 표시됩니다. Exchange 2013 클라이언트 액세스 서버의 URI를 입력하여 원격 PowerShell 연결이 작동 중인지 확인합니다. **Exchange 2013 RPS URI**는 http://CAS\_Server\_FQDN/Powershell 형식으로 되어 있어야 합니다. **확인**을 클릭합니다.
        

        > [!NOTE]
        > Exchange 2013&nbsp;포리스트에 연결하는 데 사용되는 관리자 자격 증명으로 해당 포리스트에 대한 원격 PowerShell 연결을 만들 수 있는지 확인합니다.<BR>다음 그림은 Exchange 2013에 대한 프로비전을 선택하는 방법을 보여줍니다.

        
        **Exchange 2013용 GalSync 관리 에이전트 프로비전**
        
        ![관리 에이전트 Exchange 2010 프로비전](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "관리 에이전트 Exchange 2010 프로비전")  

4.  각 포리스트에서 SMTP 송신 커넥터를 만듭니다. 자세한 단계는 [\[Wave15\] 크로스 포리스트 송신 커넥터를 구성 합니다.](configure-a-cross-forest-send-connector-exchange-2013-help.md)을 참조하십시오.

5.  각 포리스트에서 가용성 서비스를 사용하도록 설정하여 각 포리스트의 사용자가 다른 포리스트의 사용자에 대한 약속 있음/없음 데이터를 확인할 수 있도록 합니다. 자세한 내용은 [Exchange 2013의 가용성 서비스](availability-service-in-exchange-2013-exchange-2013-help.md)를 참조하십시오.

6.  조직의 전체 포리스트에서 메일을 릴레이하려면 해당 포리스트에 신뢰할 수 있는 도메인을 구성해야 합니다. 자세한 단계는 [신뢰할 수 있는 여러 도메인에 대 한 메일을 수락 하도록 Exchange 구성](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)을 참조하십시오.

